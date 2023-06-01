# HomeAssistant_AndroidBox

Tutorial de como instalar o Home Assistant https://www.home-assistant.io/ nas Android Box genéricas/convencionais.
É um método não suportado oficialmente https://www.home-assistant.io/installation/ e encontra-se descrito globalmente em https://github.com/home-assistant/os-agent

Pré-requesitos:
- Ter instalado o sitema operativo Armbian https://www.armbian.com/ na Box Android (difícil).
- Acesso à Internet via cabo de rede (ethernet)


Processo:
- Em ambiente Linux, vais executar vários comandos para instalar o Home Assistant.
- Os comandos devem ser sequenciais, ou seja, cada comando tem de ser executado com sucesso antes de se avançar para o próximo.

**Sempre q encontrares erros, pede ajuda, sejam em foruns, reddit, telegram, discord, etc. Avançar após erros não adiante**


1.
`su -`

> este comando serve para passares ao user root (equivale a ser Administrador no Windows), que é o ideal para trabalhar neste contexto. Pode ser necessário colocar a password do user root que definiste anteriormente na instalação do Armbian. O mais provável é até já estares como root.



2.
`apt update && apt upgrade`

> este comando serve para atualizares o teu sistema operativo. Lembra-te que tens de ter acesso à internet para ser bem sucedido. Se aparecerem perguntas de Sim e Não ( Yes | No ), geralmente deves escolher "Yes".



3.
`sed -i "s/${$(< /etc/hostname)}/${armhassio}/g" /etc/hostname`

`sed -i "s/${$(< /etc/hostname)}/${armhassio}/g" /etc/hosts`

`hostname "${armhassio}"`

> Faz cada um destes 3 comandos de cada vez, que servem para atualizar o teu hostname.



4. 
`reboot`

> Serve para reiniciar o sistema operativo. Após reiniciar, faz o login como root.



5. 
`hostname`

> se o resultuado for "armhassio" (sem as aspas), continua, se não for, pede ajuda!



6. 
`apt install apparmor-utils apt-transport-https avahi-daemon ca-certificates curl dbus jq network-manager socat software-properties-common wget udisks2 libglib2.0-bin`

> Este comando é todo numa linha, copia-o ou escreve-o todo seguido. Serve para instalar todos os pacotes (programas) necessários para instalar o Home Assistant. Vai demorar mas não importa. Só avanças quando terminar ou se te pedir para confirmar algo (que deves confirmar "Yes").



7.
`echo -e "\n[device]" >> "/etc/NetworkManager/NetworkManager.conf"`

`echo "wifi.scan-rand-mac-address=no"  >> "/etc/NetworkManager/NetworkManager.conf"`

`echo -e "\n[connection]"  >> "/etc/NetworkManager/NetworkManager.conf"`

`echo "wifi.clone-mac-address=preserve"  >> "/etc/NetworkManager/NetworkManager.conf"`

> Executa cada um destes 4 comandos de cada vez. São para configurar corretamete as definições de rede.



8. 
`curl -fsSL https://get.docker.com | sh`

> Agora com este comando vais instalar o sofwtare Docker. Confirma que o comando foi bem sucessido e sem erros. 



9. 
`wget https://github.com/home-assistant/os-agent/releases/download/1.2.2/os-agent_1.2.2_linux_aarch64.deb`

> Serve para fazeres o download de um pacote necessário do Home Assistant, na versão 1.2.2. Mesmo podendo não ser a versão mais recente (1.2.2), é este que deves "sacar" e usar.



10.
`sudo dpkg -i os-agent_1.2.2_linux_aarch64.deb`

> Agora vamos instalar o pacote que "sacamos" no passo anterior.



11.
`gdbus introspect --system --dest io.hass.os --object-path /io/hass/os`

> O resultado deste comando vai ser diversas linhas com conteúdo dificil de compreender, que começam com **" node /io/hass/os…"**, o **importante é que não tenha nenhum ERRO/ERROR**. Se não aparecerem errros, avança, se aparecerem, já sabes, pede ajuda!



12. 
`wget https://github.com/home-assistant/supervised-installer/releases/latest/download/homeassistant-supervised.deb`

> Agora vamos fazer download de outro pacote do Home Assistantaqui (Supervised).



13.
`dpkg -i homeassistant-supervised.deb`

> Com este comando concluímos a instalação do Home Assistant. Vai perguntar que tipo de sistema operativo temos, deves escolher  **qemuarm-64**



**Se tudo correr bem, vai ser instalado sem erros, e acessivel pela rede **
