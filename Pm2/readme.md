## Como Instalar o PM2 e executar a aplicação

1. **Instalação do PM2**:
    - Abra o terminal.
    - Navegue até a pasta da sua aplicação.
    - Execute o seguinte comando para instalar o PM2 globalmente:
    ```bash
    npm install -g pm2
    ```

2. **Iniciar a Aplicação com PM2**:
    - Ainda no terminal, navegue até a pasta da sua aplicação.
    - Execute o seguinte comando para iniciar sua aplicação usando o PM2
    ```bash
    pm2 start server.js
    ```
    - Ou esse comando para iniciar sua aplicação com um nome customizado usando o PM2 
    ```bash
    pm2 start server.js --name "nomecustomizado"
    ```
    - Após iniciar a aplicação, caso queira que sua aplicação seja salva para ser gerenciada pelo PM2, sendo assim, toda vez que o servidor for reiniciado sua aplicação sera iniciada.
    ```bash
    pm2 save
    ```

3. **Configurar o PM2 para Inicialização Automática (Ubuntu ou Systemd)**:
    - Para garantir que o PM2 inicie automaticamente com o sistema, execute um dos seguintes comandos, dependendo do seu sistema operacional:
    - **Ubuntu**:
        ```bash
        pm2 startup ubuntu
        ```
    - **Systemd**:
        ```bash
        pm2 startup systemd
        ```

## Como configurar e executar uma aplicação Next.js em um servidor Windows usando PM2

Este guia passo a passo explica como configurar e executar uma aplicação Next.js em um servidor Windows usando o PM2 para gerenciamento de processos. Ele abrange desde a verificação da versão do Node.js até a configuração do PM2 para iniciar automaticamente na inicialização do sistema.

## Passo 1: Verificar a Versão do Node.js

1. **Acessar o Servidor via RDP:**
   - Conecte-se ao servidor Windows usando Remote Desktop (RDP).

2. **Verificar a Versão Atual do Node.js:**
   - Abra o `Command Prompt` ou `PowerShell` e execute o comando para verificar a versão do Node.js instalada:

     ```bash
     node -v
     ```

   - Verifique também a versão do npm:

     ```bash
     npm -v
     ```

3. **Atualizar o Node.js (Se Necessário):**
   - Se a versão do Node.js for inferior à versão necessária para sua aplicação Next.js (por exemplo, >= 18.17.0), desinstale a versão atual:
     - Vá para "Programas e Recursos" no Painel de Controle.
     - Encontre "Node.js" na lista, clique com o botão direito e selecione "Desinstalar".
   - Baixe e instale a versão mais recente do Node.js [aqui](https://nodejs.org/).
   - Verifique novamente a versão após a instalação:

     ```bash
     node -v
     ```

## Passo 2: Instalar o PM2

1. **Instalar o PM2 Globalmente:**
   - Após instalar o Node.js, instale o PM2 globalmente no servidor:

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
   - Usando RDP, copie e cole os arquivos diretamente para o servidor em um diretório apropriado, como `C:\XC_WMS\Frontend`.

## Passo 4: Instalar as Dependências no Servidor

1. **Navegar até o Diretório do Projeto:**
   - No `Command Prompt` ou `PowerShell`, vá até o diretório onde os arquivos do projeto foram copiados:

     ```bash
     cd C:\XC_WMS\Frontend
     ```

2. **Instalar as Dependências do Projeto:**
   - Execute o comando para instalar as dependências do projeto:

     ```bash
     npm install
     ```

3. **Criar o Build da Aplicação:**
   - Crie o build de produção da aplicação:

     ```bash
     npm run build
     ```

## Passo 5: Configurar o PM2 com `ecosystem.config.js`

1. **Criar/Editar o Arquivo `ecosystem.config.js`:**
   - No diretório raiz do projeto (`C:\XC_WMS\Frontend`), crie ou edite o arquivo `ecosystem.config.js` com o seguinte conteúdo:

     ```javascript
     module.exports = {
       apps: [
         {
           name: "xcwms",                  // Nome da aplicação para o PM2
           script: "node_modules/next/dist/bin/next", // Caminho para o binário do Next.js
           args: "start -p 5041",          // Argumentos passados para o comando start, incluindo a porta
           env: {
             NODE_ENV: "development",      // Ambiente de desenvolvimento
           },
           env_production: {
             NODE_ENV: "production",       // Ambiente de produção
           }
         }
       ]
     };
     ```

## Passo 6: Iniciar a Aplicação com PM2

1. **Iniciar a Aplicação com PM2:**
   - Use o PM2 para iniciar a aplicação com o ambiente de produção:

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

## Passo 7: Configurar o PM2 para Iniciar Automaticamente no Windows

1. **Criar um Script `.bat` para Iniciar o PM2 na Inicialização:**
   - Abra o `Bloco de Notas` e crie um novo arquivo com o seguinte conteúdo:

     ```batch
     @echo off
     pm2 resurrect
     ```

   - Salve o arquivo como `pm2-startup.bat` em `C:\XC_WMS\Frontend`.

2. **Adicionar o Script à Inicialização do Windows:**
   - Pressione `Win + R`, digite `shell:startup` e pressione Enter. Isso abrirá a pasta de inicialização do Windows.
   - Copie o arquivo `pm2-startup.bat` para essa pasta.

## Passo 8: Salvar o Estado Atual dos Processos do PM2

1. **Salvar o Estado Atual dos Processos:**
   - Salve o estado atual dos processos do PM2 para garantir que eles sejam restaurados automaticamente na inicialização do sistema:

     ```bash
     pm2 save
     ```

## Conclusão

Seguindo este guia, você poderá configurar e executar sua aplicação Next.js em um servidor Windows usando o PM2. O PM2 ajudará a gerenciar seus processos de forma eficiente e garantir que sua aplicação seja restaurada automaticamente após reinicializações do sistema. Se encontrar problemas ou precisar de mais assistência, consulte a documentação do PM2 ou procure suporte adicional.

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
