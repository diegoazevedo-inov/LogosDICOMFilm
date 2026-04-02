# Plano: Compartilhamento de PDF via E-mail, WhatsApp e Mensageiros

> **Status**: Planejado (aguardando implementação)  
> **Data**: 2026-04-02  
> **Versão alvo**: v4.1.0  

## Contexto

O LOGOS DICOMFilm v4.0.0 atualmente gera PDFs via jsPDF e os abre em uma nova aba do navegador (`window.open`). O objetivo é adicionar opções para **compartilhar o PDF gerado** diretamente via e-mail, WhatsApp e outros mensageiros.

## Restrições Técnicas

> ⚠️ A aplicação é **100% client-side** (single HTML file, sem servidor). Isso define quais abordagens são viáveis:

| Abordagem | Viabilidade | Notas |
|---|---|---|
| **Web Share API** (`navigator.share`) | ✅ Viável | API nativa do navegador. Suporta compartilhar arquivos (PDFs) diretamente com qualquer app instalado (WhatsApp, Telegram, Email, etc.). Funciona em Chrome Android, Edge, Safari iOS. |
| **WhatsApp Web link** (`wa.me`) | ⚠️ Parcial | Só abre conversa com texto pré-preenchido. **Não suporta anexar arquivo** via URL. Útil como fallback para texto. |
| **mailto: link** | ⚠️ Parcial | Abre o client de e-mail, mas **não suporta anexar arquivo** automaticamente via `mailto:`. Útil para lembrar o usuário de anexar. |
| **Download direto** | ✅ Viável | Já existe como fallback. O usuário pode baixar e compartilhar manualmente. |
| **Envio via servidor (SMTP/API)** | ❌ Inviável | Requer backend, não há servidor. |

## Proposta: Fluxo de Compartilhamento em 2 Camadas

### Camada 1 — Web Share API (Experiência Principal)
Quando suportada pelo navegador (Chrome Android, Edge, Safari iOS/macOS):
- O PDF blob é compartilhado como **arquivo** via `navigator.share({ files: [pdfFile] })`
- O sistema operacional exibe o menu nativo de compartilhamento
- O usuário pode escolher WhatsApp, Telegram, E-mail, Google Drive, etc.
- **Esta é a melhor experiência possível** — compartilha o PDF completo como anexo

### Camada 2 — Menu de Fallback (Desktop sem Web Share API)
Quando `navigator.share` não está disponível (Firefox Desktop, navegadores antigos):
- Um **modal/dropdown** aparece com opções:
  1. **📥 Download PDF** — Baixa o arquivo diretamente (já existe)
  2. **📧 Abrir E-mail** — Abre `mailto:` com assunto pré-preenchido + instrução para anexar
  3. **💬 WhatsApp** — Abre `wa.me` com mensagem informando que o PDF deve ser anexado manualmente
  4. **📋 Copiar Link** — Se o PDF estiver em blob URL, copia para clipboard (uso limitado)

## Proposta de UX

### Botões na Sidebar (Tela de Configuração)
A seção de exportação atual tem 2 botões:
```
📄 Exportar PDF
🖨 Imprimir
```

Proposta — expandir para 3 botões:
```
📄 Exportar PDF          (mantém comportamento atual)
📤 Compartilhar PDF      (NOVO — Web Share ou modal de fallback)
🖨 Imprimir              (mantém comportamento atual)
```

### Modal de Compartilhamento (Fallback)
Quando a Web Share API não estiver disponível, um modal elegante aparece com as opções de compartilhamento estilizadas no design system existente (dark theme, IBM Plex fonts, cores accent).

## Mudanças no Arquivo `dicom_film_composer.html`

### 1. CSS — Novo modal de compartilhamento (~30 linhas)
- Estilos para `.share-modal`, `.share-overlay`, `.share-option`
- Animações de entrada/saída
- Ícones e hover states consistentes com o design system

### 2. HTML — Botão "Compartilhar PDF" + modal de compartilhamento (~25 linhas)
- Novo botão `📤 Compartilhar PDF` entre "Exportar PDF" e "Imprimir" (linha ~215-216)
- Estrutura HTML do modal de compartilhamento (share options)

### 3. JavaScript — Função `sharePDF()` (~80 linhas)
- Função principal `sharePDF()`:
  1. Gera o PDF (reutiliza lógica do `exportPDF()`)
  2. Tenta `navigator.share()` com o blob como arquivo
  3. Se falhar, exibe modal de fallback
- Função `generatePDFBlob()` — extrai a lógica de geração de PDF de `exportPDF()` em função reutilizável
- Funções auxiliares: `openShareModal()`, `closeShareModal()`, `shareViaEmail()`, `shareViaWhatsApp()`

## Decisão Pendente

**Comportamento do botão "Compartilhar":**
- **Opção A** (recomendado): O botão tenta Web Share API primeiro e só mostra modal se não disponível
- **Opção B**: O botão sempre mostra o modal com todas as opções + Web Share API como primeira opção

> Definir antes de implementar.

## Nota sobre WhatsApp e E-mail

Como a aplicação não tem servidor, não é possível anexar o PDF automaticamente nesses canais via URL. A Web Share API é a **única forma** de compartilhar o arquivo diretamente. Nos fallbacks, o texto inclui instruções para o usuário anexar o PDF que já foi baixado.

## Verificação Planejada

1. Abrir a aplicação no navegador, carregar um ZIP DICOM
2. Verificar que o botão "Compartilhar PDF" aparece na sidebar
3. Teste Web Share API (Chrome Android ou Edge com suporte)
4. Teste fallback modal (Firefox Desktop)
5. Verificar que "Exportar PDF" e "Imprimir" continuam funcionando normalmente
6. Validar que o PDF gerado pelo compartilhamento é idêntico ao do "Exportar PDF"
