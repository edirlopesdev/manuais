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