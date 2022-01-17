# HA_box
Instalar HA nas box convencionais


Neste momento, ja conseguitse "instalar" o sistema operativo Linux / Armbian no "disco" da tua box, que é o mais dificil.
Agora, em ambiente linux, vais correr uma série de comandos para instalar o HA.
Cada comando deve ser feito e aguardar q esteja concluido p fazer o proximo. **Sempre q encontrares erros, pede ajuda no forum, telegram ou discord e nao avances**



1.
`su -`

> este comando serve para passares ao user root, que é o ideal para trabalhar neste contexto. Pode ser necessário colocar a password do user root q definiste anteriormente. O mais provável é até já estares como root.



2.
`apt update`

> este comando serve p iniciar a atualizacao do teu sistema, algo que faz sempre bem. Tens de ter acesso à internet p ele ser bem sucedido. O acesso à internet deve ser c cabo de rede



3.
`apt upgrade`

> este comando é o que atualiza realmente o teu sistema. Como é uma atualizacao pode demorar tempo a concluir. N faças nada até estar concluido, a nao ser que o sistema te peça p confirmar algo



4.
Faz cada um destes 3 comandos de cada vez

`sed -i "s/${$(< /etc/hostname)}/${armhassio}/g" /etc/hostname
sed -i "s/${$(< /etc/hostname)}/${armhassio}/g" /etc/hosts
hostname "${armhassio}"`

> Aqui fizeste 3 comandos para atualizar o hostname. 



5. 
`reboot`

> reiniciaste o sistema. apos reiniciar, faz login como root



6. 
`hostname`

> se o resultuado for armhassio, continua, se nao for, pede ajuda no forum ou telegram ou discord



7. 
Este comando apesar de estar em várias linhas é todo numa só linha

`apt install apparmor-utils apt-transport-https avahi-daemon ca-certificates curl dbus jq network-manager socat software-properties-common wget udisks2 libglib2.0-bin`

> Aqui vais instalar todos os paccotes (programas) necessários para instalar o HA. Vai demorar mas n deixa e só fazes algo ou quando terminar ou se te pedir para confirmar algo



8.
Faz cada um destes 4 comandos de cada vez

`echo -e "\n[device]" >> "/etc/NetworkManager/NetworkManager.conf"
echo "wifi.scan-rand-mac-address=no"  >> "/etc/NetworkManager/NetworkManager.conf"
echo -e "\n[connection]"  >> "/etc/NetworkManager/NetworkManager.conf"
echo "wifi.clone-mac-address=preserve"  >> "/etc/NetworkManager/NetworkManager.conf"`

> Estes comandos sao para configurar corretamete a rede



9. 
`curl -fsSL https://get.docker.com | sh`

> aqui instalaste o docker, confirma que ficou bem sucessido sem erros. 



10. 
`wget https://github.com/home-assistant/os-agent/releases/download/1.2.2/os-agent_1.2.2_linux_aarch64.deb`

> Fizeste o download de um pacote necessário, versao 1.2.2



11.
`sudo dpkg -i os-agent_1.2.2_linux_aarch64.deb`

> Aqui estás a executar o pacote para o instalar.



12.
`gdbus introspect --system --dest io.hass.os --object-path /io/hass/os`

> aqui, o restultado vao ser muitas linhas c letras dificeis de compreender, que começam com **" node /io/hass/os…"**, o **importante é que nao tenha nenhum ERRO/ERROR**. Se nao tiver avança, se tiver, volta a pedir ajuda



13. 
`wget https://github.com/home-assistant/supervised-installer/releases/latest/download/homeassistant-supervised.deb`

> aqui sacamos o HA



14.
`dpkg -i homeassistant-supervised.deb`

> aqui instalamos o HA. Vai perguntar que tipo de sistema temos, devemos escolher  qemuarm-64




**Se tudo correr bem, vai ser instalado sem erros, e acessivel pela rede **
