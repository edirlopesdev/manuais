## 1. Configurações iniciais no GitHub

- **Setar usuário e email:**
    ```bash
    git config --global user.name "Edir Lopes"
    git config --global user.email "contato.edir@gmail.com"
    ```
- **Setar editor de texto padrão:**
    ```bash
    git config --global core.editor "seu_editor"
    ```
- **Setar ferramenta de merge:**
    ```bash
    git config --global merge.tool "sua_ferramenta_de_merge"
    ```
- **Listar configurações:**
    ```bash
    git config --list
    ```
## 2. Repositório local

- **Criar novo repositório local:** 
    ```bash 
    git init
    ```

- **Verificar status dos arquivos/diretórios:** 
    <!-- ```bash
    git status 
    ``` -->
    bash
    git status

- **Adicionar arquivos/diretórios à staged area:** 
    - Adicionar um arquivo específico:
        ```bash 
        git add meu_arquivo.js
        ```
    - Adicionar um diretório específico:
        ```bash 
        git add meu_diretorio
        ```
    - Adicionar todos os arquivos/diretórios:
        ```bash 
        git add .
        ```
    - Adicionar um arquivo listado no .gitignore:
        ```bash 
        git add -f arquivo_no_gitignore.txt
        ```

- **Comitar arquivos/diretórios:** 
    ```bash 
    ```

- **Remover arquivos/diretórios:** 
    ```bash 
    ```
    

## Configuração de novo projeto com GitHub

Este guia descreve como criar um novo projeto a partir de um projeto existente que já está sincronizado com o GitHub. Vamos desvincular as pastas do servidor e do cliente do repositório Git original e criar novos repositórios no GitHub para cada uma delas.

**Nota:** Se você estiver começando um projeto do zero e ainda não tem um repositório no GitHub, pule diretamente para o **Passo 2**.

**Passo 1: Desvinculando as Pastas do Repositório Git Original**

No terminal do Visual Studio Code (VSCode), siga estas etapas:

1. Acesse a pasta do servidor:
    ```bash
    cd 'C:\Projetos\XCSolucoes\XC_MIDDLEWARE\server'
    ```
2. Execute o seguinte comando para remover a pasta `.git` (repositório Git original):
    ```bash
    Remove-Item -Recurse -Force .git
    ```

3. Repita o mesmo processo para a pasta do cliente:
    ```bash
    cd 'C:\Projetos\XCSolucoes\XC_MIDDLEWARE\client'
    Remove-Item -Recurse -Force .git
    ```

**Passo 2: Criando Novos Repositórios no GitHub**

1. Acesse o GitHub e faça login na sua conta.
2. Clique no botão `+` no canto superior direito e selecione `New repository`.
3. Dê um nome ao seu repositório (por exemplo, `meuprojetoback`).
4. Escolha se deseja tornar o repositório público ou privado.
5. Clique em `Create repository`.

**Passo 3: Vinculando os Repositórios Locais aos Repositórios no GitHub**

1. Abra o terminal do VSCode.
2. Navegue até a pasta do servidor:
    ```bash
    cd 'C:\Projetos\XCSolucoes\XC_MIDDLEWARE\server'
    ```
    Execute os seguintes comandos para vincular o repositório local ao repositório no GitHub:
    ```bash
    git init
    git add .
    git commit -m "Primeiro commit"
    git branch -M main
    git remote add origin https://github.com/edirlopesdev/meuprojetoback.git
    git push -u origin main
    ```

3. Repita o mesmo processo para a pasta do cliente:
    ```bash
    cd 'C:\Projetos\XCSolucoes\XC_MIDDLEWARE\client'
    git init
    git add .
    git commit -m "Primeiro commit"
    git branch -M main
    git remote add origin https://github.com/edirlopesdev/meuprojetofront.git
    git push -u origin main
    ```
