# NeuroImaging Studio · VOLUME ROOM

**FASE 1 / FOUNDATION** — pacote inicial executável, com código React + TypeScript, infraestrutura Vite e PWA offline. Nesta fase, **não** há visualizador DICOM, modelos anatômicos 3D, exames reais ou casos com imagens. A interface mostra diagramas autorais **esquemáticos** e permite prévia local de PNG/JPEG/WebP, sem envio ao servidor.

## O que já funciona

- Identidade VOLUME ROOM: Obsidian `#0B0E14`, Graphite Steel `#202734`, Electric Iris `#9A91F5`, Coral Signal `#F2787A`; modo claro/escuro.
- Tela IMAGE VAULT, layout responsivo, transições simples e navegação nativa **STUDY / VIEW / EXPLORE / DIAGNOSE / LIBRARY**.
- Currículo com **50 títulos em 10 eixos**, sendo **5 aulas inaugurais** com conteúdo, recuperação ativa e avaliação curta. Os 45 capítulos restantes estão rotulados como **roteiro curricular, a produzir** (não declarados concluídos).
- WORKSTATION educativa com três planos esquemáticos e controle do indicador de corte. Importação **local** de PNG/JPEG/WebP para prévia, com zoom e brilho — **não** DICOM, **não** janela/nível.
- Atlas introdutório com 6 descrições anatômicas, sem correspondência espacial real ou visualizador 3D.
- Três casos didáticos **inteiramente textuais e sintéticos**, com perguntas e feedback, sem atribuir exames fictícios a pacientes reais.
- Biblioteca com pesquisa/favoritos e glossário, busca rápida (`Ctrl+K` ou `⌘K`).
- Progresso, notas, favoritos e tema persistidos em IndexedDB com alternativa local; backup/restauração JSON.
- `manifest.webmanifest`, ícones 192/512, service worker, fallback offline e cache do shell. Publicação por GitHub + Cloudflare Workers Static Assets.

## Publicação via GitHub → Cloudflare Workers (recomendado)

1. Descompacte o **ZIP**. Crie no GitHub um repositório vazio, por exemplo `neuroimaging-studio`, e envie **os arquivos e pastas de dentro do ZIP**, sem colocar tudo em uma pasta extra. `package.json`, `wrangler.jsonc` e `index.html` precisam estar na raiz.
2. No Cloudflare, abra **Workers & Pages → Create → Workers → Import a repository / Connect to Git** (a redação varia). Selecione o repositório.
3. Configure o **diretório raiz** como `/`. Use `npm run build` como comando de build, `npx wrangler deploy` como comando de deploy, quando os dois campos estiverem disponíveis. O comando `npm run build` desta edição valida os arquivos estáticos pré-compilados na pasta `dist`, evitando recompilação da aplicação durante o deploy. O provedor precisa disponibilizar o Wrangler para executar `npx wrangler deploy`.
4. O `wrangler.jsonc` define `assets.directory: "./dist"` e `not_found_handling: "single-page-application"`. **Não** configure simultaneamente publicação do mesmo projeto como Pages e Workers; escolha **Workers** para este fluxo.
5. Publique, abra o link `*.workers.dev` e teste a navegação e a instalação do PWA. Configuração de GitHub/Cloudflare, domínio, permissões e deploy dependem das suas contas; esta entrega **não publicou nem conectou nenhuma delas**.

> Se aparecer “Output directory”: a pasta gerada é `dist`. Se aparecer “Root directory”: use a raiz do projeto. Se aparecer “Deploy command”: use `npx wrangler deploy`, e não apenas `npm run build`.

### Teste local

Com Node.js 20+ e rede para instalar pacotes:

```bash
npm install
npm run check
npm run dev
npm run build:source
npm run preview
```

Para testar a versão pré-compilada **sem `npm install`**, sirva o diretório `dist` com um servidor de arquivos local (por exemplo, `python -m http.server 8000 -d dist`) e acesse `http://localhost:8000`.

**Importante:** não abra o arquivo `dist/index.html` como `file://`, pois os caminhos do PWA são absolutos e a instalação requer origem segura (HTTPS, ou localhost para desenvolvimento).

### Organização

```text
src/main.tsx            React + TypeScript, dados inaugurais, navegação, persistência
index.html              Entrada do Vite
vite.config.ts          Build Vite
wrangler.jsonc          Worker com Static Assets e fallback SPA
public/styles.css       Design system VOLUME ROOM
public/vendor/          Runtime React vendorizado nesta fundação
public/sw.js            Service worker
public/manifest...      Metadados PWA
public/icons/           Ícones
public/                 Recursos que o Vite copia para dist
dist/                   Build autônomo pré-compilado para teste
scripts/                Verificações offline de estrutura
docs/                   Roadmap, contratos, testes, licenças
```

### Nota de engenharia da Fase 1

Para entregar um build funcional mesmo sem acesso ao registro npm neste ambiente, a primeira versão usa React **16 vendorizado** (licença MIT) e TypeScript TSX, com frontend compilável pelo Vite. O runtime é autônomo e não depende de CDN. **Antes da utilização como produto público**, a Fase 2 deverá migrar para uma versão atual e suportada do React/ReactDOM, adicionar o lockfile gerado pelo install, rodar regressão e atualizar a estratégia de service worker. A atualização não deve alterar o conteúdo médico.

Não há backend, autenticação, sincronização entre dispositivos, armazenamento de exames no servidor ou uso de IA nesta fase. Nenhum estudo médico real deve ser incorporado ao build público sem revisão de anonimização, licença e controle de acesso.

## Precisão médica e status

Materiais são introdutórios e educativos, **não** substituem protocolos atualizados ou interpretação especializada. Referências institucionais são indicadas nas aulas para posterior verificação editorial; não há alegação de revisão científica externa concluída.

Veja [`docs/ROADMAP.md`](docs/ROADMAP.md) e [`docs/TEST_REPORT.md`](docs/TEST_REPORT.md) para o alcance e os testes desta versão.

## GitHub: pacote corrigido (upload pelo navegador)

Descompacte o ZIP e envie **todo o seu conteúdo**, não o ZIP compactado, para a raiz do GitHub. O arquivo `wrangler.jsonc` e a pasta `dist` precisam ficar na raiz. Consulte `INSTRUCOES_GITHUB_CLOUDFLARE.txt` para passos simples. O build de publicação `npm run build` valida os arquivos pré-compilados; o build real do código-fonte continua disponível via `npm run build:source` para futuras fases.
