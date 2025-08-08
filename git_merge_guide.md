# Guia Completo: Como Fazer Merge no Git

## 🎯 O que é Merge?

**Merge** é o processo de **combinar mudanças** de uma branch com outra. É como "juntar" dois caminhos de desenvolvimento em um só.

### Visualização:
```
main:     A---B---C---F  (após merge)
               \     /
feature:        D---E    (branch que foi merged)
```

---

## 🚀 Cenário Típico de Merge

Você criou uma branch `nova-feature` para desenvolver algo novo:

```bash
# Estava na main
git checkout main

# Criou branch nova
git checkout -b nova-feature

# Fez commits na nova-feature
git add .
git commit -m "Add login form"
git add .  
git commit -m "Add validation"

# Agora quer juntar com main
```

---

## Método 1: 🔄 Merge Local (Mais Comum)

### Passo 1: Voltar para branch de destino
```bash
# Voltar para main (onde você quer receber as mudanças)
git checkout main
```

### Passo 2: Atualizar main (recomendado)
```bash
# Baixar últimas mudanças do GitHub
git pull origin main
```

### Passo 3: Fazer merge
```bash
# Mergear a branch nova-feature na main
git merge nova-feature
```

### Passo 4: Enviar para GitHub
```bash
# Enviar resultado do merge
git push origin main
```

### Passo 5: Limpar branch (opcional)
```bash
# Deletar branch local após merge
git branch -d nova-feature

# Deletar branch remota (se existir)
git push origin --delete nova-feature
```

---

## Método 2: 🌐 Pull Request/Merge Request (GitHub)

### Mais usado em equipes e projetos open source

### Passo 1: Push da branch para GitHub
```bash
# Enviar sua branch para GitHub
git push origin nova-feature
```

### Passo 2: Criar Pull Request no GitHub
1. Vá para seu repositório no GitHub
2. Aparecerá banner: **"Compare & pull request"**
3. Ou clique em **"New pull request"**
4. Selecione: `main` ← `nova-feature`
5. Adicione título e descrição
6. Clique **"Create pull request"**

### Passo 3: Review e Merge
1. Outros podem revisar o código
2. Discutir mudanças nos comentários  
3. Quando aprovado, clicar **"Merge pull request"**
4. Escolher tipo de merge
5. Confirmar merge

### Passo 4: Atualizar local
```bash
# Voltar para main local
git checkout main

# Baixar mudanças merged
git pull origin main

# Deletar branch local
git branch -d nova-feature
```

---

## 🔀 Tipos de Merge

### 1. Fast-Forward Merge (Mais Simples)
Quando não há conflitos e main não mudou:

```
Antes:
main:     A---B
               \
feature:        C---D

Depois (fast-forward):
main:     A---B---C---D
```

```bash
git merge nova-feature
# Output: "Fast-forward"
```

### 2. Merge Commit (Cria commit de merge)
Quando main teve mudanças paralelas:

```
Antes:
main:     A---B---E
               \
feature:        C---D

Depois (merge commit):
main:     A---B---E---F
               \     /
feature:        C---D
```

```bash
git merge nova-feature
# Cria commit F automaticamente
```

### 3. No-Fast-Forward (Forçar merge commit)
```bash
git merge --no-ff nova-feature
# Sempre cria commit de merge, mesmo se poderia fazer fast-forward
```

---

## ⚠️ Conflitos de Merge

### Quando acontecem?
Quando **a mesma linha** foi modificada em **ambas as branches**.

### Como identificar?
```bash
git merge nova-feature
# Output:
Auto-merging arquivo.js
CONFLICT (content): Merge conflict in arquivo.js
Automatic merge failed; fix conflicts and then commit the result.
```

### Como resolver?

#### Passo 1: Ver arquivos com conflito
```bash
git status
# Mostra arquivos em vermelho com "both modified"
```

#### Passo 2: Abrir arquivo e procurar marcadores
```javascript
function login() {
<<<<<<< HEAD
    // Versão da main
    return "Login com email";
=======
    // Versão da sua branch
    return "Login com username";
>>>>>>> nova-feature
}
```

#### Passo 3: Resolver conflito manualmente
Edite o arquivo escolhendo o que manter:

```javascript
function login() {
    // Decisão: manter ambos ou escolher um
    return "Login com email ou username";
}
```

#### Passo 4: Remover marcadores de conflito
Certifique-se de remover:
- `<<<<<<< HEAD`
- `=======`
- `>>>>>>> nova-feature`

#### Passo 5: Marcar como resolvido
```bash
git add arquivo.js
```

#### Passo 6: Finalizar merge
```bash
git commit
# Abrirá editor com mensagem padrão de merge
# Ou usar: git commit -m "Resolve merge conflict"
```

---

## 🛠️ Comandos Úteis Durante Merge

### Ver status do merge
```bash
git status
# Mostra arquivos em conflito e próximos passos
```

### Ver diferenças
```bash
# Ver conflitos não resolvidos
git diff

# Ver diferenças entre branches
git diff main nova-feature
```

### Abortar merge (se der problema)
```bash
git merge --abort
# Volta ao estado anterior ao merge
```

### Ver merge em progresso
```bash
# Ver quais arquivos ainda têm conflito
git diff --name-only --diff-filter=U
```

---

## 📋 Fluxo Completo: Exemplo Prático

### Cenário: Você desenvolveu login numa branch separada

```bash
# 1. Criar branch para feature
git checkout main
git checkout -b feature/login

# 2. Desenvolver feature
echo "Login form" > login.html
git add login.html
git commit -m "Add login form"

echo "Login validation" >> login.html  
git add login.html
git commit -m "Add login validation"

# 3. Voltar para main e fazer merge
git checkout main
git pull origin main  # Atualizar main
git merge feature/login

# 4. Enviar resultado
git push origin main

# 5. Limpar
git branch -d feature/login
```

### Se houver conflito:
```bash
# Durante merge aparece conflito
git merge feature/login
# CONFLICT (content): Merge conflict in login.html

# Editar arquivo manualmente
nano login.html
# (resolver conflitos)

# Marcar como resolvido
git add login.html
git commit -m "Resolve login merge conflict"

# Continuar fluxo normal
git push origin main
git branch -d feature/login
```

---

## 🎯 Merge vs Rebase

| Característica | Merge | Rebase |
|----------------|-------|--------|
| **Histórico** | Preserva branches | Lineariza histórico |
| **Commits** | Cria merge commit | Não cria merge commit |
| **Complexidade** | Mais simples | Mais complexo |
| **Uso recomendado** | Features publicas | Branches privadas |

### Merge (cria histórico de branches):
```
main:     A---B---E---F
               \     /
feature:        C---D
```

### Rebase (histórico linear):
```
main:     A---B---E---C'---D'
```

### Quando usar cada um?
- **Merge**: Quando quer preservar histórico de desenvolvimento
- **Rebase**: Quando quer histórico limpo e linear

---

## ✅ Boas Práticas de Merge

### 1. Sempre atualizar branch base antes
```bash
git checkout main
git pull origin main
git checkout feature/login  
git merge main  # Atualizar sua branch com main
```

### 2. Testar antes do merge
```bash
# Na sua branch de feature
npm test  # ou seus testes
# Só fazer merge se tudo passar
```

### 3. Mensagens de commit claras
```bash
# ❌ Ruim
git commit -m "merge"

# ✅ Bom  
git commit -m "Merge feature/login into main"
```

### 4. Deletar branches após merge
```bash
# Local
git branch -d feature/login

# Remota
git push origin --delete feature/login
```

### 5. Use Pull Requests para revisão
- Permite code review
- Discussão das mudanças
- Testes automatizados
- Histórico de decisões

---

## 🚨 Problemas Comuns e Soluções

### Problema 1: "Please enter a commit message"
```bash
# Git abre editor para mensagem de merge
# Pressione 'i' (insert), digite mensagem, ESC, :wq
# Ou configure editor mais amigável:
git config --global core.editor "code --wait"
```

### Problema 2: Merge em branch errada
```bash
# Se fez merge na branch errada
git reset --hard HEAD~1  # Desfaz merge (CUIDADO!)
git checkout branch-correta
git merge feature/login
```

### Problema 3: Conflitos muito complexos
```bash
# Abortar e tentar rebase
git merge --abort
git rebase main  # Resolve conflitos um commit por vez
```

### Problema 4: Histórico muito poluído
```bash
# Use squash merge para juntar commits
git merge --squash feature/login
git commit -m "Add complete login feature"
```

---

## 🎉 Resumo dos Comandos Essenciais

```bash
# Merge básico
git checkout main
git pull origin main
git merge feature-branch
git push origin main
git branch -d feature-branch

# Com conflitos
git merge feature-branch
# (resolver conflitos em arquivos)
git add arquivo-resolvido.js
git commit -m "Resolve merge conflicts"
git push origin main

# Abortar merge
git merge --abort

# Tipos especiais
git merge --no-ff feature-branch    # Força merge commit
git merge --squash feature-branch   # Junta todos commits em um
```

---

## 🏆 Checklist de Merge

- [ ] ✅ Branch de feature está atualizada e testada
- [ ] ✅ Mudei para branch de destino (`git checkout main`)
- [ ] ✅ Atualizei branch de destino (`git pull origin main`)
- [ ] ✅ Executei merge (`git merge feature-branch`)
- [ ] ✅ Resolvi conflitos (se houver)
- [ ] ✅ Testei resultado do merge
- [ ] ✅ Enviei para repositório (`git push origin main`)
- [ ] ✅ Deletei branch antiga (`git branch -d feature-branch`)

**Agora você está pronto para fazer merges como um pro! 🚀**