---
 Meu post de hoje é sobre uma solução simples e limpa que eu encontrei para criar um atalho no menu do gnome shell para o eclipse baixado do site do projeto eclipse mas que provavelmente, serve para criar atalhos para qualquer programa no gnome.

 A principio é necessário baixar o eclipse, baixei do site:

##64bits
http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-jee-mars-2-linux-gtk-x86_64.tar.gz

##32bits
http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/mars/2/eclipse-jee-mars-2-linux-gtk.tar.gz

Como podem reparar essa é a versão ja com plugins para desenvolvedores java ee, se esses plugins não são de sua necessidade você pode navegar pelo site do projeto e escolher a versão que mais se adeque as suas necessidades e até mesmo, conhecer mais dos projetos encubados la.

Ao terminar o download, descompactei o eclipse no diretorio /opt onde como falei no post sobre a configuração do sdk/jdk, é o diretório padrão em sistemas unix para aplicações que vem com a distribuição por padrão.

/opt/$su -c 'tar -zxvf /home/diretoriousuario/Downloads/eclipse-jee-mars-1-linux-gtk-x86_64.tar.gz '

Executei o comando como root pois no diretorio opt só o root pode escrever.

Feito isto começa a magica, entre no diretório:

$cd /usr/share/applications/

crie e edite um arquivo com o seguinte nome:


$su -c 'gedit eclipse.desktop '


nele coloque o seguinte conteudo:

[Desktop Entry]
Name=Eclipse
Comment=Meu Eclipse
TryExec=/opt/eclipse/eclipse
Exec=/opt/eclipse/eclipse
Icon=/opt/eclipse/icon.xpm
Type=Application
Categories=GTK;Development;IDE;
StartupNotify=true
X-GNOME-Autostart-enabled=false


Feche e salve este arquivo, vai observar que no show applications do gnome shell ja aparece o seu atalho, se clicar nele vai carregar e eclipse e consequentemente conseguirá criar um link no sidebar.

Lembrando que as configurações acima, vão dar a todos os usuários automaticamente acesso ao eclipse ou qualquer outro aplicativo que criar o atalho, mas e se eu quiser que apenas meu usuário tenha este atalho ou caso eu não tenha a senha de root ou meu usuário não esteja configurado no sudo?

Simples, basta criar o mesmo arquivo descrito acima no diretório

/home/<diretorio_do_seu_usuario>/.local/share/applications

E pronto, seu atalho estará criado só que desta vez apenas para seu usuario

Para entender melhor o que foi feito, vale uma consulta na documentação do gnome:

https://developer.gnome.org/desktop-entry-spec/

Até a próxima:

