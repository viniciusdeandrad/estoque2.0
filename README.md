# Painel de Estoque (versão GitHub Pages)

Versão do painel feita pra rodar direto no GitHub Pages — sem servidor,
sem instalar nada. O navegador lê e grava os dados direto no repositório
do GitHub.

**Importante:** essa versão só funciona com o repositório **público**.
Isso significa que qualquer pessoa que souber o link do repositório (ou
souber procurar) consegue ver os números reais de estoque, mesmo quem
não é convidado pro painel. Se isso for um problema, essa não é a versão
certa — nesse caso use a versão com servidor (Render).

## 1. Deixe o repositório público

No repositório, vá em **Settings** → role até o final → **Danger Zone**
→ **Change visibility** → **Change to public**.

## 2. Suba os arquivos desta pasta

Pela mesma tela de upload que você já usou (**Add file** → **Upload
files**), suba os arquivos desta pasta (`index.html`, `app.js`, e a
pasta `data` com o `seed.json` dentro) direto na **raiz** do
repositório — não dentro de uma subpasta.

Se o repositório já tinha os arquivos da versão com servidor (`server.js`,
`parser.js`, `package.json`, `github.js`, a pasta `static`), pode
apagar esses — eles não são usados nessa versão. Não é obrigatório, só
deixa mais organizado.

## 3. Ative o GitHub Pages

Em **Settings** → **Pages** (no menu da esquerda):

- **Source**: "Deploy from a branch"
- **Branch**: `main`, pasta `/ (root)`
- Clique em **Save**

Depois de alguns minutos, o GitHub mostra o link do site no topo dessa
mesma página — algo como:

```
https://seu-usuario.github.io/nome-do-repositorio/
```

Esse é o link que você compartilha com todo mundo.

## 4. Gere um token de acesso (só pra quem for atualizar a planilha)

Quem só vai **olhar** o painel não precisa de nada. Só quem vai clicar
em "Atualizar planilha" precisa gerar um token, uma única vez:

1. No GitHub, clique na sua foto → **Settings** → **Developer settings**
2. **Personal access tokens** → **Tokens (classic)** → **Generate new
   token (classic)**
3. Dê um nome (ex: painel-estoque), escolha uma validade
4. Marque a caixinha **public_repo** (como o repositório é público, não
   precisa marcar o "repo" inteiro)
5. Gere e copie o código (começa com `ghp_...`) — guarde em um lugar
   seguro, ele só aparece uma vez

Na hora de atualizar a planilha pelo painel, cole esse código no campo
de token. Se marcar "Lembrar neste navegador", ele fica salvo só no seu
navegador (não é enviado a lugar nenhum além do GitHub) — não marque
isso em computador compartilhado.

## 5. Como funciona a atualização

Clique em "Atualizar planilha", envie o arquivo `.xlsx`, confira a
prévia, cole o token e confirme. O painel classifica os produtos por
marca automaticamente (comparando com a base atual) e grava o resultado
direto no arquivo `data/estoque.json` do repositório — dá pra ver cada
atualização no histórico de commits do GitHub. Pode levar alguns
segundos para o link atualizar para todo mundo (por causa de cache).

## 6. Se você usar um domínio próprio

O painel detecta sozinho o usuário e o repositório a partir do endereço
`seu-usuario.github.io/repositorio`. Se você configurar um domínio
próprio (custom domain), edite manualmente essas linhas no início do
arquivo `app.js`:

```js
const REPO_CONFIG = {
  owner: 'seu-usuario',
  repo: 'nome-do-repositorio',
  branch: 'main',
  dataPath: 'data/estoque.json',
};
```
