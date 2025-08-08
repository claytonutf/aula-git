# Tutorial Completo de Git - Do Básico ao Avançado

## 📚 Sumário
1. [O que é Git?](#o-que-é-git)
2. [Instalação](#instalação)
3. [Configuração Inicial](#configuração-inicial)
4. [Conceitos Fundamentais](#conceitos-fundamentais)
5. [Comandos Básicos](#comandos-básicos)
6. [Trabalhando com Branches](#trabalhando-com-branches)
7. [Repositórios Remotos](#repositórios-remotos)
8. [Comandos Intermediários](#comandos-intermediários)
9. [Comandos Avançados](#comandos-avançados)
10. [Boas Práticas](#boas-práticas)
11. [Resolução de Problemas](#resolução-de-problemas)

---

## O que é Git?

Git é um **sistema de controle de versão distribuído** criado por Linus Torvalds em 2005. Ele permite:

- 📝 **Rastrear mudanças** no código ao longo do tempo
- 🔄 **Colaborar** com outros desenvolvedores
- 🌿 **Criar branches** para desenvolvimento paralelo
- ⏪ **Reverter** para versões anteriores quando necessário
- 🔍 **Visualizar histórico** completo do projeto

### Por que usar Git?
- **Backup automático** do seu código
- **Colaboração eficiente** em equipe
- **Experimentação segura** com branches
- **Histórico completo** de todas as mudanças

---

## Instalação

### Windows
1. Baixe em: https://git-scm.com/download/win
2. Execute o instalador
3. Use as configurações padrão (recomendado)

### macOS
```bash
# Usando Homebrew
brew install git

# Ou usando Xcode Command Line Tools
xcode-select --install
```

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### Verificar instalação
```bash
git --version
```

---

## Configuração Inicial

### Configurar identidade (OBRIGATÓRIO)
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
```

### Configurações úteis
```bash
# Editor padrão
git config --global core.editor "code --wait"  # VS Code
# git config --global core.editor "vim"        # Vim

# Configurar quebras de linha
git config --global core.autocrlf true   # Windows
git config --global core.autocrlf input  # macOS/Linux

# Visualizar configurações
git config --list
```

---

## Conceitos Fundamentais

### 📁 Working Directory (Diretório de Trabalho)
Onde você edita seus arquivos.

### 📋 Staging Area (Área de Preparação)
Onde ficam os arquivos prontos para serem commitados.

### 📦 Repository (Repositório)
Onde ficam armazenadas todas as versões do projeto.

### Fluxo básico:
```
Working Directory → Staging Area → Repository
     (add)              (commit)
```

---

## Comandos Básicos

### 1. Inicializar um repositório
```bash
# Criar novo repositório
git init

# Clonar repositório existente
git clone https://github.com/usuario/projeto.git
```

### 1.1 Quick setup — if you’ve done this kind of thing before
```bash
https://github.com/claytonutf/aula-git-testes.git
```

### 1.2 …or create a new repository on the command line
```bash
echo "# aula-git-testes" >> README.md
git init
git add codigo1.py
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/USUARIO/aula-git-testes.git
git push -u origin main
```

### 1.3 …or push an existing repository from the command line
```bash
git remote add origin https://github.com/USUARIO/aula-git-testes.git
git branch -M main
git push -u origin main
```

### 2. Verificar status
```bash
git status
```

### 3. Adicionar arquivos ao staging
```bash
# Adicionar arquivo específico
git add arquivo.txt

# Adicionar vários arquivos
git add arquivo1.txt arquivo2.js

# Adicionar todos os arquivos modificados
git add .

# Adicionar todos os arquivos de um tipo
git add *.js
```

### 4. Fazer commit
```bash
# Commit com mensagem
git commit -m "Adicionar funcionalidade X"

# Commit detalhado (abre editor)
git commit

# Adicionar e commitar arquivos já rastreados
git commit -am "Atualizar função Y"
```

### 5. Ver histórico
```bash
# Histórico completo
git log

# Histórico resumido
git log --oneline

# Histórico com gráfico
git log --graph --oneline --all

# Últimos 5 commits
git log -5
```

### 6. Ver diferenças
```bash
# Diferenças não commitadas
git diff

# Diferenças no staging area
git diff --staged

# Diferenças entre commits
git diff HEAD~1 HEAD
```

---

## Trabalhando com Branches

### O que são branches?
Branches são **linhas de desenvolvimento paralelas** que permitem trabalhar em features diferentes simultaneamente.

### Comandos de Branch

```bash
# Listar branches
git branch

# Criar nova branch
git branch nova-feature

# Mudar para branch
git checkout nova-feature

# Criar e mudar para nova branch
git checkout -b nova-feature

# Renomear branch atual
git branch -m novo-nome

# Deletar branch
git branch -d nome-branch
git branch -D nome-branch  # Forçar deleção
```

### Merge (Fusão)
```bash
# Mudar para branch de destino
git checkout main

# Fazer merge
git merge nova-feature
```

### Rebase (alternativa ao merge)
```bash
# Rebase da branch atual
git rebase main
```

**Diferença entre Merge e Rebase:**
- **Merge**: Mantém histórico de branches
- **Rebase**: Cria histórico linear (mais limpo)

---

## Repositórios Remotos

### Adicionar repositório remoto
```bash
git remote add origin https://github.com/usuario/projeto.git
```

### Ver repositórios remotos
```bash
git remote -v
```

### Push (enviar para remoto)
```bash
# Primeira vez
git push -u origin main

# Próximas vezes
git push

# Enviar branch específica
git push origin nova-feature
```

### Pull (baixar do remoto)
```bash
# Baixar e fazer merge
git pull

# Baixar sem fazer merge
git fetch
```

### Clone (clonar repositório)
```bash
git clone https://github.com/usuario/projeto.git
```

---

## Comandos Intermediários

### Desfazer mudanças
```bash
# Descartar mudanças no working directory
git checkout -- arquivo.txt
git restore arquivo.txt  # Comando mais novo

# Remover do staging area
git reset HEAD arquivo.txt
git restore --staged arquivo.txt  # Comando mais novo

# Desfazer último commit (mantém mudanças)
git reset --soft HEAD~1

# Desfazer último commit (descarta mudanças)
git reset --hard HEAD~1
```

### Stash (guardar mudanças temporariamente)
```bash
# Guardar mudanças
git stash

# Guardar com mensagem
git stash push -m "Work in progress"

# Listar stashes
git stash list

# Aplicar último stash
git stash pop

# Aplicar stash específico
git stash apply stash@{0}

# Deletar stash
git stash drop stash@{0}
```

### Tags (marcar versões)
```bash
# Criar tag
git tag v1.0.0

# Criar tag com mensagem
git tag -a v1.0.0 -m "Versão 1.0.0"

# Listar tags
git tag

# Enviar tags para remoto
git push origin --tags
```

---

## Comandos Avançados

### Cherry-pick (aplicar commit específico)
```bash
git cherry-pick abc123def
```

### Interactive Rebase
```bash
# Reescrever últimos 3 commits
git rebase -i HEAD~3
```

### Bisect (encontrar commit que introduziu bug)
```bash
git bisect start
git bisect bad          # Commit atual tem bug
git bisect good v1.0    # Versão que funcionava
# Git vai testando automaticamente
git bisect reset        # Finalizar
```

### Blame (ver quem modificou cada linha)
```bash
git blame arquivo.txt
```

### Reflog (histórico de referências)
```bash
git reflog
```

---

## Boas Práticas

### ✅ Mensagens de Commit
```bash
# ❌ Ruim
git commit -m "fix"
git commit -m "mudanças"

# ✅ Bom
git commit -m "Fix: Corrigir validação de email"
git commit -m "Add: Nova funcionalidade de login"
git commit -m "Update: Melhorar performance da consulta"
```

### ✅ Estrutura de mensagem completa
```
Tipo: Resumo em até 50 caracteres

Descrição mais detalhada do que foi feito e por quê,
limitada a 72 caracteres por linha.

- Mudança específica 1
- Mudança específica 2

Fixes #123
```

### ✅ Convenções de tipo
- **feat**: Nova funcionalidade
- **fix**: Correção de bug
- **docs**: Documentação
- **style**: Formatação, pontos e vírgulas
- **refactor**: Refatoração de código
- **test**: Adição ou correção de testes
- **chore**: Manutenção

### ✅ Fluxo de trabalho recomendado
1. Criar branch para cada feature: `git checkout -b feature/login`
2. Fazer commits pequenos e frequentes
3. Usar pull requests para code review
4. Deletar branches após merge
5. Manter main/master sempre estável

---

## Resolução de Problemas

### 🔧 Conflitos de Merge
Quando dois commits modificam a mesma linha:

```bash
# Durante merge/pull, aparecerá:
Auto-merging arquivo.txt
CONFLICT (content): Merge conflict in arquivo.txt
```

1. Abrir arquivo e procurar por:
```
<<<<<<< HEAD
Sua versão
=======
Versão do outro commit
>>>>>>> branch-name
```

2. Editar manualmente e remover marcadores
3. Adicionar e commitar:
```bash
git add arquivo.txt
git commit -m "Resolver conflito de merge"
```

### 🔧 Desfazer commits públicos
```bash
# Criar novo commit que desfaz mudanças
git revert abc123def
```

### 🔧 Recuperar arquivo deletado
```bash
# Recuperar arquivo do último commit
git checkout HEAD -- arquivo.txt

# Recuperar de commit específico
git checkout abc123def -- arquivo.txt
```

### 🔧 Mudanças não aparecem
```bash
# Verificar arquivos ignorados
cat .gitignore

# Forçar adicionar arquivo ignorado
git add -f arquivo.txt
```

### 🔧 Limpar repositório
```bash
# Remover arquivos não rastreados
git clean -f

# Remover arquivos e diretórios não rastreados
git clean -fd

# Preview do que será removido
git clean -n
```

---

## 🎯 Resumo dos Comandos Essenciais

| Comando | Descrição |
|---------|-----------|
| `git init` | Inicializar repositório |
| `git clone <url>` | Clonar repositório |
| `git add <arquivo>` | Adicionar ao staging |
| `git commit -m "msg"` | Fazer commit |
| `git status` | Ver status |
| `git log` | Ver histórico |
| `git push` | Enviar para remoto |
| `git pull` | Baixar do remoto |
| `git branch` | Listar branches |
| `git checkout -b <branch>` | Criar e mudar branch |
| `git merge <branch>` | Fazer merge |
| `git stash` | Guardar mudanças temporárias |

---

## 📖 Próximos Passos

1. **Pratique** criando um repositório local
2. **Experimente** com branches
3. **Configure** um repositório no GitHub
4. **Colabore** em projetos open source
5. **Aprenda** sobre Git Flow ou GitHub Flow

**Lembre-se:** Git é uma ferramenta poderosa, mas pode parecer complexa no início. A prática constante é a chave para dominar!

---

*Criado com ❤️ para ajudar desenvolvedores a dominar o Git*