## Como Instalar o PM2 e Executar a Aplicação

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
## :handshake: Colaboradores
<table>
  <tr>
    <td align="center">
      <a href="http://github.com/edirlopesdev">
        <img src="https://avatars.githubusercontent.com/u/128933712?v=4" width="100px;" alt="Edir Lopes Lima"/><br>
        <sub>
          <b>Welington Oliveira</b>
        </sub>
      </a>
    </td>
  </tr>
</table>