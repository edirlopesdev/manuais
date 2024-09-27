# Guia de Configuração e Execução de Aplicação Next.js com PM2 em um Servidor Windows via RDP

## Introdução

Este guia fornece instruções detalhadas para configurar e executar uma aplicação Next.js em um servidor Windows usando o PM2 para gerenciamento de processos. O manual abrange duas abordagens: 
1. **Execução direta sem o arquivo `ecosystem.config.js`.**
2. **Configuração com o arquivo `ecosystem.config.js`.**

## Pré-requisitos

- A aplicação Next.js já deve estar pronta no seu ambiente de desenvolvimento local.
- Acesso ao servidor Windows via Remote Desktop Protocol (RDP).
- Node.js e PM2 devem estar instalados no servidor Windows.

## Passo 1: Verificar a Versão do Node.js

1. **Acessar o Servidor via RDP:**
   - Conecte-se ao servidor Windows usando Remote Desktop (RDP).

2. **Verificar a Versão Atual do Node.js:**
   - Abra o `Command Prompt` ou `PowerShell` e execute o seguinte comando para verificar a versão do Node.js instalada:

     ```bash
     node -v
     ```

   - Verifique também a versão do npm:

     ```bash
     npm -v
     ```

3. **Atualizar o Node.js (Se Necessário):**
   - Se a versão do Node.js for inferior à necessária para sua aplicação Next.js (por exemplo, >= 18.17.0), atualize a versão:
     - Desinstale a versão antiga em "Programas e Recursos" no Painel de Controle.
     - Baixe e instale a versão mais recente do Node.js em [nodejs.org](https://nodejs.org/).
     - Verifique a nova versão:

       ```bash
       node -v
       ```

## Passo 2: Instalar o PM2 no Servidor Windows

1. **Instalar o PM2 Globalmente:**
   - No `Command Prompt` ou `PowerShell`, instale o PM2 globalmente no servidor:

     ```bash
     npm install -g pm2
     ```

2. **Verificar a Instalação do PM2:**
   - Verifique se o PM2 foi instalado corretamente:

     ```bash
     pm2 -v
     ```

## Passo 3: Transferir os Arquivos da Aplicação via RDP

1. **Copiar os Arquivos do Projeto para o Servidor:**
   - No seu computador local, selecione os arquivos do projeto.
   - Usando o RDP, copie e cole os arquivos diretamente para o servidor em um diretório apropriado, como `C:\XC_WMS\Frontend`.

## Passo 4: Instalar Dependências e Executar a Aplicação

1. **Navegar até o Diretório do Projeto:**
   - No `Command Prompt` ou `PowerShell`, vá até o diretório onde os arquivos do projeto foram copiados:

     ```bash
     cd C:\XC_WMS\Frontend
     ```

2. **Instalar as Dependências do Projeto:**
   - Execute o seguinte comando para instalar as dependências:

     ```bash
     npm install
     ```

3. **Criar o Build de Produção:**
   - Crie o build de produção da aplicação:

     ```bash
     npm run build
     ```

---

## Opção 1: Executar a Aplicação Diretamente com PM2 (Sem `ecosystem.config.js`)

### Passo 5: Executar a Aplicação Diretamente com PM2

1. **Iniciar a Aplicação Diretamente:**
   - Se preferir não usar o arquivo `ecosystem.config.js`, inicie a aplicação diretamente com o seguinte comando:

     ```bash
     pm2 start src/app/index.js --name "xcwms"
     ```

2. **Verificar o Status da Aplicação:**
   - Verifique o status para confirmar que a aplicação está rodando corretamente:

     ```bash
     pm2 status
     ```

3. **Salvar o Estado da Aplicação:**
   - Após a aplicação estar rodando corretamente, salve o estado dos processos do PM2 para garantir que eles sejam restaurados automaticamente após reinicializações do sistema:

     ```bash
     pm2 save
     ```

### Passo 6: Atualização do Projeto e Reinicialização da Aplicação

1. **Parar a Aplicação para Atualizar:**
   - Antes de atualizar a aplicação, pare o serviço:

     ```bash
     pm2 stop xcwms
     ```

2. **Executar o `npm install` para Instalar Novas Dependências:**
   - Caso haja novas dependências no projeto, rode o `npm install`:

     ```bash
     npm install
     ```

3. **Reiniciar a Aplicação:**
   - Reinicie a aplicação com o PM2 após a atualização:

     ```bash
     pm2 start xcwms
     ```

4. **Salvar Novamente o Estado:**
   - Salve o estado após a atualização para garantir que ele seja preservado:

     ```bash
     pm2 save
     ```

---

## Opção 2: Executar a Aplicação com `ecosystem.config.js`

### Passo 5: Configurar o PM2 com `ecosystem.config.js`

1. **Criar/Editar o Arquivo `ecosystem.config.js`:**
   - No diretório raiz do projeto (`C:\XC_WMS\Frontend`), crie ou edite o arquivo `ecosystem.config.js` com o seguinte conteúdo:

     ```javascript
     module.exports = {
       apps: [
         {
           name: "xcwms", // Nome da aplicação para o PM2
           script: "node_modules/next/dist/bin/next", // Caminho para o binário do Next.js
           args: "start -p 5041", // Argumentos passados para o comando start, incluindo a porta
           env: {
             NODE_ENV: "development", // Ambiente de desenvolvimento
           },
           env_production: {
             NODE_ENV: "production", // Ambiente de produção
           }
         }
       ]
     };
     ```

### Passo 6: Iniciar a Aplicação com PM2 Usando `ecosystem.config.js`

1. **Iniciar a Aplicação com o PM2:**
   - Use o PM2 para iniciar a aplicação com o ambiente de produção, utilizando o arquivo `ecosystem.config.js`:

     ```bash
     pm2 start ecosystem.config.js --env production
     ```

2. **Verificar o Status da Aplicação:**
   - Verifique se a aplicação está rodando corretamente:

     ```bash
     pm2 status
     ```

3. **Verificar os Logs da Aplicação:**
   - Veja os logs para garantir que a aplicação não encontrou nenhum erro ao iniciar:

     ```bash
     pm2 logs xcwms
     ```

---

## Passo 7: Configurar o PM2 para Iniciar Automaticamente no Windows

1. **Criar um Script `.bat` para Iniciar o PM2 na Inicialização:**
   - Crie um arquivo `.bat` com o seguinte conteúdo:

     ```batch
     @echo off
     pm2 resurrect
     ```

   - Salve o arquivo como `pm2-startup.bat` em `C:\XC_WMS\Frontend`.

2. **Adicionar o Script à Inicialização do Windows:**
   - Pressione `Win + R`, digite `shell:startup` e pressione Enter.
   - Copie o arquivo `pm2-startup.bat` para essa pasta.

---

## Conclusão

Este guia aborda as duas abordagens principais para gerenciar a execução da sua aplicação Next.js com PM2: executando diretamente com PM2 (sem `ecosystem.config.js`) e utilizando o arquivo `ecosystem.config.js`. O PM2 simplifica o gerenciamento de processos e garante que sua aplicação seja restaurada automaticamente após reinicializações do servidor.

Se encontrar problemas ou precisar de mais suporte, consulte a documentação oficial do PM2 ou procure ajuda adicional.

---

**:handshake: Colaborador**
<table>
  <tr>
    <td align="center">
      <a href="http://github.com/edirlopesdev">
        <img src="https://avatars.githubusercontent.com/u/128933712?v=4" width="100px;" alt="Edir Lopes Lima"/><br>
        <sub>
          <b>Edir Lopes Lima</b>
        </sub>
      </a>
    </td>
  </tr>
</table>
