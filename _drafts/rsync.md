---
Como meu primeiro artigo, resolvi escrever sobre uma solução simples e gratuita que tem me sido de grande valia para executar backups com segurança e simplicidade.


rsync -hav --delete /cygdrive/c/leandro/ /cygdrive/d/trabalho/


onde:


a = (archive) faz com que todas as permissões e atributos dos arquivos sejam mantidos  

v = (verbose) mostra o progresso na tela

--delete = faz com que arquivos apagados na pasta original sejam apagados também na pasta do backup, fazendo com que ela se mantenha como uma cópia fiel

Desta forma simples e direta, você consegue protejer seus dados 
