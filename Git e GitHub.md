
# Git: Guia de Referencia

## **Comandos Essenciais**

## 1. Configuração e Inicialização

| **Comando**                                          | **Descrição**                                                     |
| ---------------------------------------------------- | ----------------------------------------------------------------- |
| `git config --global user.name "Nome"`               | Define o nome de usuário globalmente.                             |
| `git config --global user.email "email@exemplo.com"` | Define o e-mail do usuário globalmente.                           |
| **`git init`**                                       | Inicializa um novo repositório Git local na pasta atual.          |
| **`git remote add origin <url>`**                    | Vincula o repositório local a um repositório remoto (ex: GitHub). |
| `git remote -v`                                      | Lista os repositórios remotos vinculados.                         |

## 2. Fluxo de Trabalho Local (Snapshot)

|**Comando**|**Descrição**|
|---|---|
|`git status`|Exibe o estado atual (arquivos alterados, staged ou untracked).|
|`git add <arquivo>`|Adiciona um arquivo específico para a Staging Area.|
|`git add .`|Adiciona **todas** as mudanças para a Staging Area.|
|`git commit -m "msg"`|Grava o snapshot das alterações com uma descrição.|
|`git commit --amend -m "msg"`|Altera a mensagem do último commit (antes do push).|
|`git log --oneline`|Exibe o histórico de commits de forma resumida.|

## 3. Sincronização com Repositório Remoto

|**Comando**|**Descrição**|
|---|---|
|**`git push origin <branch>`**|Envia os commits locais para o servidor remoto.|
|**`git pull origin <branch>`**|Baixa as novidades do servidor e mescla com seu código local.|
|`git fetch`|Baixa as atualizações do servidor, mas **não** mescla no seu código.|
|`git clone <url>`|Clona um repositório remoto existente para sua máquina.|

## 4. Branches (Ramificações)

|**Comando**|**Descrição**|
|---|---|
|`git branch`|Lista todas as branches locais.|
|`git branch <nome>`|Cria uma nova branch.|
|`git checkout -b <nome>`|Cria uma nova branch e já muda para ela imediatamente.|
|`git switch <nome>`|Muda para uma branch existente (alternativa moderna ao checkout).|
|`git merge <nome>`|Une as alterações da branch especificada na branch atual.|

## 5. Desfazendo Alterações

| **Comando**                 | **Descrição**                                                         |
| --------------------------- | --------------------------------------------------------------------- |
| `git checkout -- <arquivo>` | Descarta as alterações locais em um arquivo (volta ao último commit). |
| `git reset HEAD <arquivo>`  | Remove um arquivo da Staging Area (volta para modified).              |
| `git revert <hash>`         | Cria um novo commit que reverte as mudanças de um commit específico.  |

---

## Gerenciamento de Branches

Branches permitem o desenvolvimento de funcionalidades em paralelo sem afetar o código principal.

- **Criar nova branch:** `git switch -c nome-da-branch`
    
- **Listar branches:** `git branch`
    
- **Mudar para branch existente:** `git switch nome-da-branch`
    
- **Mesclar branch na atual:** `git merge nome-da-branch`
    
- **Excluir branch local:** `git branch -d nome-da-branch`
    

---

## Sincronização com Repositório Remoto

- **Adicionar repositório remoto:** `git remote add origin <url>`
    
- **Enviar alterações:** `git push origin <nome-da-branch>`
    
- **Baixar e mesclar alterações:** `git pull origin <nome-da-branch>`
    
- **Baixar sem mesclar:** `git fetch origin`
    
- **Deletar um arquivo:** `git rm NOME_DO_ARQUIVO.md`
    

---

## Boas Praticas e Padronização

### Conventional Commits

Utilize prefixos nas mensagens de commit para facilitar o entendimento do histórico:

- `feat:` Adição de uma nova funcionalidade.
    
- `fix:` Correção de um erro ou bug.
    
- `docs:` Alterações apenas na documentação.
    
- `style:` Formatação, pontos e vírgulas (sem alteração de lógica).
    
- `refactor:` Mudança no código que não corrige erro nem adiciona função.
    
- `chore:` Atualização de tarefas de build, pacotes ou ferramentas.
    

### Dicas Gerais

1. **Commits frequentes:** Prefira fazer vários commits pequenos do que um único commit gigante.
    
2. **Mensagens claras:** A mensagem deve explicar o "o quê" e o "porquê", não o "como".
    
3. **Branch principal limpa:** Nunca faça commits direto na `main` ou `master` em projetos de equipe.
    
4. **Arquivo .gitignore:** Sempre configure o `.gitignore` para não subir senhas, arquivos de configuração local ou pastas de dependências (como `node_modules`).
    

---

### Exemplo de Fluxo de Trabalho (Feature Workflow)

1. Atualize sua branch principal:
    
    `git switch main`
    
    `git pull origin main`
    
2. Crie uma branch para a tarefa:
    
    `git switch -c feat/login-social`
    
3. Realize as alterações e salve os commits:
    
    `git add .`
    
    `git commit -m "feat: implementa login com conta google"`
    
4. Envie a branch para o servidor:
    
    `git push origin feat/login-social`
    
5. Após a revisão (Pull Request), mescle na main e delete a branch local:
    
    `git switch main`
    
    `git merge feat/login-social`
    
    `git branch -d feat/login-social`

### Exemplo de Fluxo: Identificar Branch, Commitar e Enviar

Este cenário assume que você já fez alterações nos seus arquivos e quer subir o trabalho.

1. Verificar em qual branch você está trabalhando: `git branch` (A branch atual aparecerá com um asterisco ao lado).
    
    Ou use: `git status` (Este comando mostra a branch e também quais arquivos foram modificados).
    
1. Preparar os arquivos (Stage): `git add .` (Adiciona todas as modificações feitas).
    
2. Criar o commit local: `git commit -m "feat: descricao da sua alteracao"`
    
3. Enviar para o GitHub (Push): Se você estiver na branch `main`: `git push origin main`
    
    Se estiver em uma branch chamada `desenvolvimento`: `git push origin desenvolvimento`