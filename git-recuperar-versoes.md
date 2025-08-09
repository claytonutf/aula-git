# Como Recuperar Versões Específicas no Git/GitHub

## 🎯 Cenários Comuns

1. **Ver código de uma versão antiga** (só visualizar)
2. **Recuperar arquivo específico** de versão antiga
3. **Voltar o projeto inteiro** para versão antiga
4. **Desfazer último commit** (ainda não enviado)
5. **Reverter commit público** (já no GitHub)

---

## Passo 1: Identificar a Versão Desejada

### 1.1 Ver histórico de commits
```bash
# Histórico completo
git log

# Histórico resumido (mais fácil de ler)
git log --oneline

# Últimos 10 commits
git log --oneline -10

# Com gráfico de branches
git log --oneline --graph --all
```

### 1.2 Ver commits no GitHub
1. Vá para seu repositório no GitHub
2. Clique em **"commits"** (ao lado do botão verde "Code")
3. Navegue pela lista de commits
4. **Copie o hash do commit** (código como `a1b2c3d`)

### 1.3 Encontrar commit específico
```bash
# Buscar por mensagem
git log --grep="palavra-chave"

# Buscar por autor
git log --author="Nome do Autor"

# Buscar por data
git log --since="2024-01-01" --until="2024-01-31"
```

---

## Cenário 1: 👀 Ver Código de Versão Antiga (Só Visualizar)

### Método 1: Checkout temporário
```bash
# Ver commit específico
git checkout a1b2c3d

# Voltar para versão atual
git checkout main
```

⚠️ **Aviso:** Você ficará em "detached HEAD state" - é só para visualizar!

### Método 2: Ver no GitHub
1. Vá para o commit específico no GitHub
2. Clique no hash do commit
3. Navegue pelos arquivos naquela versão

---

## Cenário 2: 📁 Recuperar Arquivo Específico

### Recuperar arquivo de commit específico
```bash
# Recuperar arquivo específico
git checkout a1b2c3d -- caminho/para/arquivo.js

# Recuperar múltiplos arquivos
git checkout a1b2c3d -- src/ README.md

# Ver arquivo sem recuperar
git show a1b2c3d:caminho/para/arquivo.js
```

### Exemplo prático:
```bash
# Você quer recuperar o arquivo "index.js" de 5 commits atrás
git checkout HEAD~5 -- index.js

# Agora você precisa commitar a mudança
git add index.js
git commit -m "Recuperar versão anterior do index.js"
```

---

## Cenário 3: ⏪ Voltar Projeto Inteiro para Versão Antiga

### Método 1: Reset (CUIDADO! Perde commits)
```bash
# Ver onde você está
git log --oneline

# Voltar para commit específico (PERDE COMMITS POSTERIORES)
git reset --hard a1b2c3d

# Forçar push (se já estava no GitHub)
git push --force
```

⚠️ **PERIGO:** `reset --hard` apaga commits! Use apenas se tem certeza!

### Método 2: Revert (Mais Seguro)
```bash
# Criar novo commit que desfaz mudanças
git revert a1b2c3d

# Reverter múltiplos commits
git revert HEAD~3..HEAD
```

### Método 3: Criar branch da versão antiga
```bash
# Criar branch a partir de commit antigo
git checkout -b versao-anterior a1b2c3d

# Agora você pode trabalhar nesta versão sem afetar main
```

---

## Cenário 4: 🔄 Desfazer Último Commit (Local)

### Se ainda NÃO fez push:
```bash
# Desfazer commit mantendo mudanças
git reset --soft HEAD~1

# Desfazer commit e mudanças no staging
git reset HEAD~1

# Desfazer commit e TODAS as mudanças
git reset --hard HEAD~1
```

### Se JÁ fez push:
```bash
# NUNCA use reset --hard em commits públicos!
# Use revert em vez disso:
git revert HEAD
git push
```

---

## Cenário 5: ↩️ Reverter Commit Público (Já no GitHub)

### Revert (Recomendado para commits públicos)
```bash
# Reverter commit específico
git revert a1b2c3d

# Reverter sem fazer commit automático
git revert --no-commit a1b2c3d

# Reverter merge commit
git revert -m 1 a1b2c3d
```

---

## 🛠️ Comandos Avançados para Recuperação

### Ver diferenças entre versões
```bash
# Diferença entre commits
git diff a1b2c3d..b2c3d4e

# Diferença entre commit e versão atual
git diff a1b2c3d HEAD

# Ver só nomes dos arquivos modificados
git diff --name-only a1b2c3d HEAD
```

### Recuperar commits "perdidos"
```bash
# Ver histórico de todas as