<div align="center">

# 🏥 LOGOS DICOMFilm

### Compositor de Filmes DICOM para Impressão Clínica

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![HTML5](https://img.shields.io/badge/HTML5-Single%20File-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
![Version](https://img.shields.io/badge/version-4.0.0-green)

**Visualize, componha e imprima filmes DICOM diretamente no navegador.**  
Sem instalação. Sem servidor. Sem dependências locais. Apenas um arquivo HTML.

---

</div>

## ✨ Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| 📂 **Upload ZIP** | Carrega estudos DICOM compactados em `.zip` |
| 🔬 **Parser DICOM Nativo** | Suporte a Implicit VR LE e Explicit VR LE sem compressão |
| 🖼️ **Composição de Filmes** | Layouts configuráveis (1×1 até 6×6) com grid personalizável |
| 🎨 **Window/Level** | Presets clínicos (T1, T2, FLAIR, Spine, Orbit) + ajuste manual |
| 📐 **Modos de Exibição** | Contain, Cover e Stretch para ajuste das imagens |
| 📄 **Tamanhos de Papel** | 8×10", 10×12", 11×14", 14×14", 14×17", A4, A3 |
| 🔄 **Orientação** | Retrato e Paisagem |
| 🏷️ **Anotações** | Cabeçalho com logo da clínica, dados do paciente, W/L |
| 🔒 **Anonimização** | Modo anonimizado para dados sensíveis |
| 🖨️ **Impressão Nativa** | Impressão direta via diálogo do navegador |
| 📤 **Exportar PDF** | Geração de PDF de alta qualidade com jsPDF |
| 🎯 **Exclusão de Páginas** | Exclua folhas desnecessárias (sobras) da impressão/exportação |

## 🚀 Como Usar

1. **Abra** o arquivo `dicom_film_composer.html` no navegador (Chrome/Edge recomendados)
2. **Arraste** um arquivo `.zip` contendo imagens DICOM para a área de upload
3. **Selecione** as séries desejadas para composição
4. **Configure** layout, window/level, tamanho de papel e orientação
5. **Exporte** como PDF ou **imprima** diretamente

```
Não requer servidor web, Node.js, Python ou qualquer instalação.
Funciona 100% offline após o primeiro carregamento.
```

## 📋 Requisitos

- Navegador moderno (Chrome 90+, Edge 90+, Firefox 90+)
- Arquivos DICOM em formato `.zip`
- Sintaxes de transferência suportadas:
  - **✅ Implicit VR Little Endian** (1.2.840.10008.1.2)
  - **✅ Explicit VR Little Endian** (1.2.840.10008.1.2.1)
  - **⚠️ Detectadas mas não renderizadas:** Big Endian, Deflated, JPEG, JPEG2000, RLE

## 🏗️ Arquitetura

```
┌─────────────────────────────────────────────┐
│            dicom_film_composer.html         │
│                                             │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐ │
│  │  Parser   │  │ Renderer │  │  Exporter │ │
│  │  DICOM    │  │  Canvas  │  │  PDF/Print│ │
│  └────┬─────┘  └────┬─────┘  └─────┬─────┘ │
│       │              │              │       │
│  ┌────┴──────────────┴──────────────┴─────┐ │
│  │          Estado Central (state)         │ │
│  └────────────────────────────────────────┘ │
│                                             │
│  Dependências externas (CDN):               │
│  • JSZip 3.10.1 — descompressão de ZIP     │
│  • jsPDF 2.5.1 — geração de PDF            │
│  • IBM Plex Fonts — tipografia             │
└─────────────────────────────────────────────┘
```

## 📦 Dependências

| Biblioteca | Versão | Uso | CDN |
|---|---|---|---|
| [JSZip](https://stuk.github.io/jszip/) | 3.10.1 | Descompressão de arquivos ZIP | cdnjs |
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | Geração de documentos PDF | cdnjs |
| [IBM Plex](https://fonts.google.com/specimen/IBM+Plex+Sans) | — | Tipografia (Sans + Mono) | Google Fonts |

## 🔧 Configuração por Série

Cada série DICOM possui configurações independentes:

- **Layout**: Grid de imagens por folha (1×1, 2×2, 3×3, etc.)
- **Intervalo**: Selecione apenas as imagens desejadas (início, fim, passo)
- **Window/Level**: Ajuste de brilho/contraste com presets ou manual
- **Modo de Exibição**: Contain (sem corte), Cover (preenche), Stretch
- **Tamanho do Papel**: Diversos formatos clínicos e padrão
- **Cor do Fundo**: Preto (filme) ou Branco (papel)
- **Gutter**: Espaçamento entre células do grid
- **Inversão**: Inverte a escala de cinza (MONOCHROME1 ↔ MONOCHROME2)

## 📝 Versionamento

Este projeto segue o [Versionamento Semântico](https://semver.org/lang/pt-BR/) (SemVer):

- **MAJOR**: Mudanças incompatíveis na interface ou funcionalidade
- **MINOR**: Novas funcionalidades retrocompatíveis
- **PATCH**: Correções de bugs retrocompatíveis

Consulte o [CHANGELOG.md](CHANGELOG.md) para o histórico completo de versões.

## 📄 Licença

Copyright 2024-2026 **Diêgo Azevedo** — Especialista em Saúde Digital e Inteligência Artificial.

Licenciado sob a [Apache License 2.0](LICENSE). Veja o arquivo [LICENSE](LICENSE) para detalhes.

```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

## 🤝 Contribuições

Contribuições são bem-vindas! Por favor:

1. Faça um Fork do projeto
2. Crie uma Branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'feat: nova funcionalidade'`)
4. Push para a Branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## ⚠️ Aviso Legal

Este software é fornecido **"como está"** (AS IS), sem garantias de qualquer tipo. **Não é um dispositivo médico certificado** e não deve ser utilizado como substituto de sistemas PACS, visualizadores DICOM certificados, ou qualquer outro software médico aprovado por agências reguladoras (ANVISA, FDA, CE). Destina-se exclusivamente a fins educacionais e de conveniência operacional.

---

<div align="center">

**Desenvolvido por [Diêgo Azevedo](https://github.com/diegoazevedo-inov)**

*Especialista em Saúde Digital e Inteligência Artificial*

</div>
