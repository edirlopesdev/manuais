## Como Instalar o PM2 e Executar a Aplicação

1. **Instalação do PM2**:
    ```bash
    npm install -g pm2
    ```

2. **Iniciar a Aplicação com PM2**:
    ```bash
    pm2 start server.js
    ```

3. **Configurar o PM2 para Inicialização Automática (Ubuntu ou Systemd)**:
    - **Ubuntu**:
        ```bash
        pm2 startup ubuntu
        ```
    - **Systemd**:
        ```bash
        pm2 startup systemd
        ```
