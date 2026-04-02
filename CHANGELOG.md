# Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

O formato é baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/),
e este projeto adere ao [Versionamento Semântico](https://semver.org/lang/pt-BR/).

## [Unreleased]

### Adicionado
- Documentação de planejamento para funcionalidade de compartilhamento de PDF via Web Share API (`docs/PLAN_SHARE_PDF.md`)

### Modificado
- Reformulação da interface (`dicom_film_composer.html`) para total suporte e responsividade em dispositivos móveis. Foram adicionados breakpoints para ajustar a barra lateral de configuração, permitindo melhor interação e visibilidade do preview em telas menores.

## [4.0.0] - 2026-03-31
### Adicionado
- Parser DICOM nativo com suporte a Implicit VR LE e Explicit VR LE
- Composição multi-série com configurações independentes por série
- Layouts configuráveis de 1×1 até 6×6
- Presets de Window/Level: T1 Brain, T2 Brain, FLAIR, Spine, Orbit, Auto, Full Range
- Modos de exibição: Contain, Cover, Stretch
- Tamanhos de papel clínicos: 8×10", 10×12", 11×14", 14×14", 14×17", A4, A3
- Orientação Retrato/Paisagem
- Exportação PDF de alta qualidade via jsPDF
- Impressão nativa via janela dedicada (popup)
- Anotações de cabeçalho/rodapé com logo da clínica
- Upload e exibição de logo personalizado (JPG/PNG)
- Campo de nome da clínica/hospital
- Modo de anonimização forte para dados sensíveis
- Exclusão seletiva de páginas (sobras) da impressão/exportação
- Inversão de escala de cinza (MONOCHROME1 ↔ MONOCHROME2)
- Gutter configurável entre células do grid
- Indicadores de séries com modalidade e número de frames
- Validação e detecção de sintaxes de transferência não suportadas
- Cache de renderização para melhoria de desempenho
- Interface dark mode com design system baseado em IBM Plex

### Técnico
- Arquitetura single-file HTML (zero dependências locais)
- Dependências externas via CDN: JSZip 3.10.1, jsPDF 2.5.1
- Tipografia: IBM Plex Sans + IBM Plex Mono (Google Fonts)
- Renderização DICOM via Canvas 2D API
- Conversão Canvas→Image para compatibilidade com spooler de impressão
- Popup window dedicado para impressão (contorna limitações do Chrome @media print)

## [3.0.0] - 2026-03-15

### Adicionado
- Primeira versão pública com funcionalidades base de composição DICOM

---

[4.0.0]: https://github.com/diegoazevedo-inov/LogosDICOMFilm/releases/tag/v4.0.0
[3.0.0]: https://github.com/diegoazevedo-inov/LogosDICOMFilm/releases/tag/v3.0.0
