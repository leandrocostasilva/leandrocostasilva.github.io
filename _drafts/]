---
A jre, em ambientes linux, utiliza o /dev/random para gerar números randômicos para trabalhar com criptografia, porém este método se torna lento porque o /dev/random gera esses numeros através do ruído do ambiente e obtidos através de drivers de dispositivo e de outras origens e deve ser apropriado para usos que necessitam alta qualidade dos números aleatórios.
Em contra partida existe o /dev/urandom que apesar dele não ser projetado por especialistas em criptografia, pode ser usado em ambientes onde isso não seja problema como ambiente de desenvolvimento o que deixa tarefas como subir o weblogic ou criar domains no mesmo que exigem a geração de chaves criptográficas  bem mais rápido.
Para esta alteração é necessário editar o arquivo

JAVA_HOME/jre/lib/security/java.security

Na seção
securerandom.source=file:/dev/random

alterar para

securerandom.source=file:/dev/urandom

Fontes
http://blog.herivelto.com.br/2012/08/weblogic-start-lento.html
https://pt.wikipedia.org/wiki//dev/random
