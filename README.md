<h1><strong>Laboratório de Servidor Linux: Redes e Segurança</strong></h1>
Este projeto documenta a configuração de um servidor web Linux (Nginx) Seguro Basico em ambiente virtualizado, 
focando em acesso remoto seguro via SSH e regras de Firewall (UFW), O Foco principal foi a configuração de conectividade de Rede (Modo Bridge).



<h2>Tecnologias e Ferramentas Utilizadas</h2>
<ul>
<li>Oracle VirtualBox</li>
  
<li>SO: Ubuntu Server / Debian</li>

<li>Servidor Web: Nginx</li>

<li>Segurança: OpenSSH, UFW (Firewall)</li>

<li>Ambiente: VirtualBox (Modo Bridge)</li>
</ul>



<h2>Configurando a Rede</h2>
Diferente Do Modo Nat Padrão Da Máquina Virtual Padrão, utilizei o Modo Bridge para que a Máquina Virtual recebesse um IP real da rede local. Isso permitiu a comunicação direta entre o servidor e outros dispositivos da casa (como computador ou smartphone).
<ul>
<li>Comando Para Verificação do IP</li>

  ```ip addr```   ou
  ```ifconfig```

</ul>
  No meu caso, por ter utilizado o Bridge, Meu ip do servidor é ```192.168.x.x```





<h2>Configuração De Segurança(FireWall)</h2>
Como o servidor está exposta apenas na rede local em modo Bridge, apliquei apenas o princípio do Privilégio Mínimo, fechando todas as conexões de entrada e permitindo o estritamente necessário, desta forma permitindo apenas levantando o FireWall e permitindo o acesso do SSH e HTTP para página Web


<ul>

  <li>Comando que define a política padrão de firewall para bloquear qualquer tentativa de conexão externa que não tenha sido permitida</li>
  
  ```sudo ufw default deny incoming```

<li>Comando que abre uma "Exceção para regra na muralha, especificamente para Porta 22, A porta 22 por padrão é do SSH, Sem este comando antes de ativar o Firewall, não será possivel o acesso remoto"</li>

  ```sudo ufw allow 22/tcp```
<li>Abre a Porta 80, Porta padrão para o protocolo web HTTP</li>
  
  ```sudo ufw allow 80/tcp```
<li>Liga o FireWall e aplica as regras configuradas</li>
  
  ```sudo ufw  enable```
  
