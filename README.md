# apiwhatsnew

#INSTALAR E CONFIGURAR A VPS 

#INSTALANDO O PODMAN
sudo su -
dnf module install container-tools
loginctl enable linger opc
exit

#INICIANDO O CONTAINER DA API
podman run -it -d --name apiwhats -p5000:8080 docker.io/jcvn/apiwhatsnew:1.1

# ATUALIZANDO A API:
podman exec -it apiwhats npm update
podman exec -it apiwhats npm fund 

#CONFIGURANDO O CONTAINER COMO SERVIÇO NO SYSTEMD
mkdir -p /home/opc/.config/systemd/user
cd /home/opc/.config/systemd/user
podman generate systemd --name apiwhats -f -n
systemctl --user daemon-reload
systemctl --user enable container-apiwhats.service

#CONFIGURANDO O FIREWALL DA  VPS
firewall-cmd --add-port=5000/tcp --permanent
firewall-cmd --reload

#AJUSTANDO A API
podman exec -it apiwhats vim token.json
Adicionar o token no arquivo
ab12cd34ef56
podman exec -it apiwhats vim node_modules/whatsapp-web.js/src/util/Constants.js
Adicionar a linha abaixo no arquivo abaixo de "headless: true,"
args: ['--no-sandbox', '--disable-setuid-sandbox'],

# LEITURA DO QR COM O MOBILE
http://IP-DA-VPS:5000

#TESTANDO A API
http://IP-DA-VPS:5000/enviar?destino=55DDDCELULAR-DESTINO&mensagem=Hello%20Word!&token=ab12cd34ef56

#CONF TRACCAR.XML
vim /opt/traccar/conf/traccar.xml
<entry key='notificator.types'>web,sms</entry>
<entry key='notificator.sms.manager.class'>org.traccar.sms.HttpSmsClient</entry>
<entry key='sms.http.url'>http://IP_DA_API:5000/enviar?</entry>
<entry key='sms.http.template'>
{"destino": "{phone}","mensagem": "{message}", "token": "ab12cd34ef56"}
</entry>

SÓ SEGUIR A RECEITA QUE NÃO TEM ERRO
USEM A INSTANCIA DISPONIVEL GRATUITA NA OCI COM OL8
DEPOIS DE CRIAR A INSTANCIA É LOGAR COM PUTTY E IR PARA O ABRAÇO
FUI!!!!
