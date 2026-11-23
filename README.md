# NeuroImagem / NeuroImaging Studio — GitHub direto

Projeto de deploy estático para **Cloudflare Workers com Static Assets**, sem Vite, sem TypeScript, sem compilação e sem `npm run build`. A versão inicial preserva o conteúdo existente do NeuroImaging Studio Fase 1; o site usa um único `public/index.html` com JS e CSS completos.

## GitHub

Baixe o ZIP e **extraia**. Entre no repositório `NeuroImagem` -> Add file -> Upload files. Selecione **tudo que está dentro** da pasta extraída (`public`, `wrangler.jsonc`, `README.md`). Confirme o commit. No GitHub, você deve ver o arquivo `wrangler.jsonc` e a pasta `public` diretamente na raiz.

## Cloudflare Workers (com GitHub)

- Worker name: `neuroimagem` (deve coincidir exatamente com `name` do wrangler.jsonc; se tiver criado outro Worker, substitua o nome pelo do Worker ou crie Worker chamado `neuroimagem`).
- Root directory: `/` (raiz do GitHub; caso mostre campo em branco, use em branco)
- **Build command: deixar VAZIO** (esta versão já vem pronta)
- Deploy command: `npx wrangler deploy`
- Não preencha Output directory para Workers; a pasta está configurada no `wrangler.jsonc`.

Não use a opção Pages para este procedimento. Não suba somente o ZIP.

## Escopo médico

Fase 1: currículo inicial de 50 capítulos (5 aulas disponíveis), 3 casos textuais, biblioteca, busca, favoritos, PWA. Não contém DICOM real, integração PlayCanvas ou casos com imagens de pacientes. Materiais são educativos e não substituem avaliação especializada.

## Fonte para desenvolvimento futuro

O projeto original React + TypeScript permanece disponível no pacote da Fase 1. O pacote presente é uma **edição de implantação simplificada**, não o código-fonte preferido para desenvolvimento contínuo. Para as próximas fases, trabalhar preferencialmente no projeto-fonte e gerar novamente os arquivos compilados.
