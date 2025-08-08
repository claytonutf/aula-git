# Do `git init` ao GitHub - Guia Passo a Passo

## 🎯 O que vamos fazer:
1. Criar um projeto local do zero
2. Inicializar Git
3. Fazer primeiro commit
4. Criar repositório no GitHub
5. Conectar local com GitHub
6. Fazer push

---

## Passo 1: Criar e Inicializar Projeto Local

### 1.1 Criar pasta do projeto
```bash
# Criar pasta
mkdir meu-projeto
cd meu-projeto

# Ou se já estiver na pasta do projeto:
# cd caminho/para/seu/projeto
```

### 1.2 Inicializar Git
```bash
git init
```
📝 **O que acontece:** Git cria uma pasta oculta `.git` que vai armazenar todo o histórico do projeto.

### 1.3 Criar alguns arquivos (exemplo)
```bash
# Criar arquivo README
echo "# Meu Projeto" > README.md

# Criar arquivo de código (exemplo)
echo "console.log('Hello World!');" > index.js

# Criar .gitignore (opcional mas recomendado)
echo "node_modules/
.env
*.log" > .gitignore
```

---

## Passo 2: Primeiro Commit

### 2.1 Verificar status
```bash
git status
```
📝 **Você verá:** Lista de arquivos não rastreados (em vermelho)

### 2.2 Adicionar arquivos ao staging
```bash
# Adicionar todos os arquivos
git add .

# Ou adicionar arquivos específicos
git add README.md index.js .gitignore
```

### 2.3 Verificar status novamente
```bash
git status
```
📝 **Agora verá:** Arquivos prontos para commit (em verde)

### 2.4 Fazer primeiro commit
```bash
git commit -m "Initial commit: Add README, main file and gitignore"
```

### 2.5 Verificar histórico
```bash
git log --oneline
```

---

## Passo 3: Criar Repositório no GitHub

### 3.1 Acessar GitHub
1. Vá para [github.com](https://github.com)
2. Faça login na sua conta
3. Clique no botão **"+"** no canto superior direito
4. Selecione **"New repository"**

### 3.2 Configurar repositório
- **Repository name:** `meu-projeto` (mesmo nome da pasta local)
- **Description:** (opcional) "Meu primeiro projeto com Git"
- **Visibility:** Public ou Private
- ⚠️ **IMPORTANTE:** NÃO marque essas opções:
  - ❌ Add a README file
  - ❌ Add .gitignore
  - ❌ Choose a license

### 3.3 Criar repositório
Clique em **"Create repository"**

---

## Passo 4: Conectar Local com GitHub

Após criar o repositório, GitHub mostrará instruções. Para projeto existente, use:

### 4.1 Adicionar remote origin
```bash
git remote add origin https://github.com/SEU-USUARIO/meu-projeto.git
```
📝 **Substitua:** `SEU-USUARIO` pelo seu nome de usuário do GitHub

### 4.2 Verificar remote
```bash
git remote -v
```
📝 **Deve mostrar:**
```
origin  https://github.com/SEU-USUARIO/meu-projeto.git (fetch)
origin  https://github.com/SEU-USUARIO/meu-projeto.git (push)
```

### 4.3 Renomear branch para main (se necessário)
```bash
# Verificar nome da branch atual
git branch

# Se estiver como 'master', renomear para 'main'
git branch -M main
```

---

## Passo 5: Fazer Push para GitHub

### 5.1 Primeiro push
```bash
git push -u origin main
```

📝 **O que significa:**
- `push`: Enviar commits para repositório remoto
- `-u`: Configurar upstream (conexão padrão)
- `origin`: Nome do repositório remoto
- `main`: Nome da branch

### 5.2 Autenticação
GitHub pode pedir autenticação:

**Opção 1: Token de Acesso Pessoal (Recomendado)**
1. GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. Selecione scopes: `repo`
4. Use o token como senha

**Opção 2: GitHub CLI**
```bash
# Instalar GitHub CLI
# https://cli.github.com/

# Fazer login
gh auth login
```

---

## Passo 6: Verificar se Funcionou

### 6.1 Atualizar página do GitHub
Vá para seu repositório no GitHub e atualize a página. Você deve ver:
- ✅ Arquivos que você criou
- ✅ README.md sendo exibido
- ✅ Histórico de commits

### 6.2 Verificar conexão local
```bash
git status
```
📝 **Deve mostrar:** "Your branch is up to date with 'origin/main'"

---

## 🚀 Próximos Passos - Fluxo de Trabalho

Agora que está conectado, seu fluxo será:

```bash
# 1. Fazer mudanças nos arquivos
# (editar arquivos...)

# 2. Ver o que mudou
git status
git diff

# 3. Adicionar mudanças
git add .

# 4. Fazer commit
git commit -m "Descrição das mudanças"

# 5. Enviar para GitHub
git push
```

---

## 🔧 Comandos Úteis para o Dia a Dia

```bash
# Ver status
git status

# Ver diferenças
git diff

# Histórico resumido
git log --oneline

# Desfazer mudanças não commitadas
git checkout -- nome-arquivo.js

# Desfazer último commit (mantém mudanças)
git reset --soft HEAD~1
```

---

## ❌ Problemas Comuns e Soluções

### Erro: "remote origin already exists"
```bash
# Remover e adicionar novamente
git remote remove origin
git remote add origin https://github.com/SEU-USUARIO/meu-projeto.git
```

### Erro: "Updates were rejected"
```bash
# Baixar mudanças do GitHub primeiro
git pull origin main

# Ou se quiser sobrescrever (CUIDADO!)
git push --force
```

### Esqueceu de configurar user.name e user.email
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
```

---

## 📋 Checklist Completo

- [ ] ✅ Criar pasta do projeto
- [ ] ✅ `git init`
- [ ] ✅ Criar arquivos (README.md, etc.)
- [ ] ✅ `git add .`
- [ ] ✅ `git commit -m "Initial commit"`
- [ ] ✅ Criar repositório no GitHub (vazio!)
- [ ] ✅ `git remote add origin <url>`
- [ ] ✅ `git branch -M main` (se necessário)
- [ ] ✅ `git push -u origin main`
- [ ] ✅ Verificar no GitHub se apareceu

---

## 🎉 Parabéns!

Agora você tem:
- ✅ Projeto local versionado com Git
- ✅ Repositório no GitHub
- ✅ Sincronização entre local e GitHub
- ✅ Conhecimento do fluxo básico

**Próximo passo:** Comece a desenvolver seu projeto e pratique o fluxo de `add` → `commit` → `push`!