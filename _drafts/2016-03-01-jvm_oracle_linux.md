---
Boa noite,

Hoje na grande maioria das distribuições o open-jdk vem junto com os pacotes básicos instalados, se não vier, no momento em que instalar um pacote de seu repositório que seja desenvolvido em java será obrigado a instalar o openjdk.
Até ai sem problemas, a jvm que foi instalada será considerada como padrão pela sua distro, porém nem sempre queremos isso, em geral os desenvolvedores que utilizam a plataforma java tem preferência pela jvm da oracle (isso tende a mudar com o tempo).
Para que você utilize a jvm da oracle no lugar da jvm que vem com o openjdk sem desinstalar o seu precioso writer ou calc, você pode simplesmente baixar o pacote tar.gz ou rpm (eu prefiro a primeira opção por ser 100% portável entre as distros), instalar e simplesmente configurar o java_home como explicarei a seguir. O problema desta solução é que a jvm padrão do seu so continua sendo a do openjdk, como resolvemos isso? Segue os passos que resolverão este seu enigma.

Se você ainda não baixou a jvm oficial da oracle chegou a hora, você pode baixar o tar.gz ou rpm do jdk ou o tar.gz ou rpm do jre, se você chegou até este tutorial, entendo que saiba a diferença entre o jdk e jre, se não souber acompanhe meus postes pois logo falarei sobre a diferença. Chega de conversa fiada e mãos a obra.

Para fazer o download do jdk ou jre:

http://www.oracle.com/technetwork/java/javase/downloads/index.html

Para instalar os respectivos rpms:

## JDK 32-bit ##
su -c 'rpm -Uvh /local/do/download/jdk-versao-linux-i586.rpm'
## JDK 64-bit ##
su -c 'rpm -Uvh /local/do/download/jdk-versao-linux-x64.rpm'
## JRE 32-bit ##
su -c 'rpm -Uvh /local/do/download/jre-versao-linux-i586.rpm'
## JRE 64-bit ##
su -c 'rpm -Uvh /local/do/download/jre-versao-linux-x64.rpm'

Se optar pelo tar.gz como eu, bastar descompactar o pacote na pasta /opt que em sistemas que utilizam o padrão posix é o diretório padrão para aplicativos que não fazem parte da distribuição (isso é um papo para outro post)

cd /opt


##32 bits
su -c 'tar -zxvf /local/do/download/jdk-versao-linux-i586.tar.gz'

##64 bits
su -c 'tar -zxvf /local/do/download/jdk-versao-linux-x64.tar.gz'

Ao descompactar o pacote, percebemos que o nome da pasta fica parecido com isso:

jdk1.8.0_74/

Eu gosto de sempre estar com a versão mais atual da jvm, e pra facilitar minha vida sempre crio os seguintes links:

##Utilizando o jdk
su -c 'ln -s jdk1.8.0_74/ jdk'

su -c 'ln -s jdk/jre/'


##Utilizando o jre
su -c 'ln -s jre1.8.0_74/ jre'

Desta forma caso eu atualize minha versão da jdk ou jre altero apenas um link simbólico.

Agora o pulo do gato para que a jvm que você acabou de baixar se torne a padrão do seu so:

##no caso do tar.gz

su -c 'alternatives --install /usr/bin/java java /opt/jre/bin/java 200000'
su -c 'alternatives --install /usr/bin/javaws javaws /opt/jre/bin/javaws 200000'
su -c 'alternatives --install /usr/bin/javac javac /opt/jdk/bin/javac 200000'
su -c 'alternatives --install /usr/bin/jar jar /opt/jdk/bin/jar 200000'

##no caso do rpm do jdk



## java ##
alternatives --install /usr/bin/java java /usr/java/jdk[versao]/jre/bin/java 200000
## javaws ##
alternatives --install /usr/bin/javaws javaws /usr/java/jdk[versao]/jre/bin/javaws 200000
## javac ##
alternatives --install /usr/bin/javac javac /usr/java/jdk[versao]/bin/javac 200000
## javac ##
alternatives --install /usr/bin/jar jar /usr/java/jdk[versao]/bin/jar 200000
##no caso do rpm do jre
# java ##
alternatives --install /usr/bin/java java /usr/java/jre[versao]/bin/java 200000
## javaws ##
alternatives --install /usr/bin/javaws javaws /usr/java/jre[versao]/bin/javaws 200000
Agora só falta o seu java_home (só útil para desenvolvedores)
faça uma copia de segurança do arquivo chamado .bashrc que fica na pasta /home/[usuario]
cp ~/.bashrc ~/.bashrc_old
depois abra este arquivo no seu editor de texto favorito no meu caso o vi
vi ~/.bashrc

no final adicione as seguintes linhas

##no caso do tar.gz
JAVA_HOME=/opt/jdk

PATH=$PATH:$JAVA_HOME/bin

export PATH JAVA_HOME


#no caso do rpm
JAVA_HOME=/usr/java/jdk[versao]/
PATH=$PATH:$JAVA_HOME/bin

export PATH JAVA_HOME 
E pra configurar o plugin do Firefox:
primeiro crie uma pasta plugin no diretório do Firefox
##no caso de tar.gz
##64 bits
su -c 'alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /opt/jre/lib/amd64/libnpjp2.so 2000' 
##32 bits
su -c 'alternatives --install /usr/lib/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /opt/jre/lib/i386/libnpjp2.so 2000' 
##no caso de rpm jdk
##64 bits
su -c 'alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /usr/java/jdk[versao]/jre/lib/amd64/libnpjp2.so 2000' 
##32 bits
su -c 'alternatives --install /usr/lib/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /usr/java/jdk[versao]/jre/lib/i386/libnpjp2.so 2000' 



##no caso de rpm jre
##64 bits
su -c 'alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /usr/java/jre[versao]/lib/amd64/libnpjp2.so 2000' 
##32 bits
su -c 'alternatives --install /usr/lib/mozilla/plugins/libjavaplugin.so libjavaplugin.sp /usr/java/jre[versao]/lib/i386/libnpjp2.so 2000' 
Reinicie o Firefox e digite o comando na barra de endereços:
about:plubins

deve aparecer na pagina algo como o seguinte:

Java(TM) Plug-in 11.74.2

    File: libnpjp2.so
    Path: /opt/jdk1.8.0_74/jre/lib/amd64/libnpjp2.so
    Version: 11.74.2
    State: Enabled
    Next Generation Java Plug-in 11.74.2 for Mozilla browsers

 Agora pra finalizar os seguintes comandos:
su -c 'alternatives --config java'
A saída é semelhante a essa:
There are 2 programs which provide 'java'.

  Selection    Command
-----------------------------------------------
   1           /opt/jre/bin/java
*+ 2           /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.72-7.b15.fc23.x86_64/jre/bin/java

Enter to keep the current selection[+], or type selection number: 1
 
neste caso minha seleção foi a 1 para que a jvm da oracle impere 
su -c 'alternatives --config javaws'

There is 1 program that provides 'javaws'.

  Selection    Command
-----------------------------------------------
*+ 1           /opt/jre/bin/javaws

Enter to keep the current selection[+], or type selection number: 1 
su -c 'alternatives --config javac'


There is 1 program that provides 'javac'.

  Selection    Command
-----------------------------------------------
*+ 1           /opt/jdk/bin/javac

Enter to keep the current selection[+], or type selection number: 1

Pronto, seu sistema esta configurado para utilizar a jvm da oracle em qualquer situação.

Até a próxima.


Fonte: https://www.if-not-true-then-false.com/2014/install-oracle-java-8-on-fedora-centos-rhel/ 
