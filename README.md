# 🐧 Laboratório de Servidor Linux: Redes e Segurança

Este projeto documenta a configuração de um servidor web Linux (Nginx) em ambiente virtualizado, focando em conectividade de rede avançada, acesso remoto seguro e políticas de firewall. O objetivo principal foi a configuração de conectividade de rede em **Modo Bridge** e a aplicação de regras de segurança.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Virtualização:** Oracle VirtualBox
* **SO:** Ubuntu Server / Debian
* **Servidor Web:** Nginx
* **Segurança:** OpenSSH, UFW (Uncomplicated Firewall)
* **Rede:** Modo Bridge (para comunicação direta com dispositivos físicos)

---

## 🌐 1. Configurando a Rede

Diferente do modo NAT padrão, utilizei o **Modo Bridge** para que a Máquina Virtual recebesse um IP real da rede local. Isso permitiu a comunicação direta entre o servidor e outros dispositivos (como computador ou smartphone).

**Comandos para verificação do IP:**
```bash
ip addr
# ou
ifconfig
```
> No meu caso, o IP do servidor foi configurado como `192.168.x.x`.

---

## 🛡️ 2. Configuração de Segurança (Firewall)

Como o servidor está exposto na rede local, apliquei o princípio do **Privilégio Mínimo**, fechando todas as conexões de entrada e permitindo apenas o estritamente necessário (SSH e HTTP).

* **Bloquear todas as conexões de entrada por padrão:**
    ```bash
    sudo ufw default deny incoming
    ```
* **Permitir SSH (Porta 22):** Necessário para o acesso remoto.
    ```bash
    sudo ufw allow 22/tcp
    ```
* **Permitir HTTP (Porta 80):** Porta padrão para o protocolo web.
    ```bash
    sudo ufw allow 80/tcp
    ```
* **Ativar o Firewall:**
    ```bash
    sudo ufw enable
    ```

---

## 🔍 3. Verificação dos Serviços (Auditoria)

Nesta etapa, validei se todos os serviços estavam operando conforme o esperado.

* **Garantir que Nginx e SSH estão ativos:**
    ```bash
    systemctl is-active nginx
    systemctl is-active ssh
    ```
    *A resposta deve ser `active`. Caso contrário, use `systemctl restart [serviço]`.*

* **Verificar portas e regras UFW:**
    ```bash
    ss -tuln | grep -E '22|80'
    sudo ufw status verbose
    ```

---

## 🚀 4. Demonstração do Sistema

Para validar o laboratório, realizei testes de acesso de uma máquina externa com Windows e um smartphone.

### 🌐 Acesso Web (Porta 80)
Ao digitar o endereço IP no navegador, a página personalizada do servidor é carregada com sucesso.

| Smartphone (Rede Local) | Desktop (Windows / Chrome) |
| :---: | :---: |
| <img src="[https://github.com/user-attachments/assets/ea70fd81-506c-4a76-833a-00a2c02ea0f4](https://github.com/user-attachments/assets/ea70fd81-506c-4a76-833a-00a2c02ea0f4)" width="220" alt="Smartphone" /> | ![Print google](https://github.com/user-attachments/assets/53a6cde3-25f7-4839-8932-f724680a123d) |

### 💻 Acesso Remoto via SSH
Uso do terminal do Windows para acesso virtual sem necessidade de interface direta na VM.

**Comando:** `ssh vboxuser@192.168.x.x`

![Comando SSH](https://github.com/user-attachments/assets/66351cd7-2db1-4036-9398-e1f60b6ded13)
![Sucesso SSH](https://github.com/user-attachments/assets/40a0f807-bbb2-4c4c-abe1-049d2b06f1e3)

### 🛠️ Edição do HTML do Site Local
Navegação até o diretório do servidor e edição do arquivo para customização.

1. **Acessar diretório:** `cd /var/www/html`
2. **Comando de edição:** `sudo nano index.html`

![Diretorio](https://github.com/user-attachments/assets/f48b466d-3e1e-40fa-95a0-1c00791d3cab)

**Comparativo de Edição:**

| Arquivo Original | Arquivo Editado | Resultado Final |
| :---: | :---: | :---: |
| ![Original](https://github.com/user-attachments/assets/f7cacfe1-7b84-487d-91e3-2ab63cdb514a) | ![Editado](https://github.com/user-attachments/assets/c30b87a6-1847-40f4-bb8d-0e2b36b885af) | ![Resultado](https://github.com/user-attachments/assets/25169796-a80a-4bc0-85b7-4c03af2d8f47) |

---

### 🚪 Encerrando a Sessão
Para sair do acesso remoto SSH e retornar ao prompt do host local, utiliza-se o comando:
```bash
exit
```
![Finalizando SSH](https://github.com/user-attachments/assets/9bbb0ed1-2edc-4058-8f98-09ed7f9721a3)
