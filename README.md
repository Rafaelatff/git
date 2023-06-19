# git
Repositorie created to help during the course [Git - Básico ao avançado (2021)](https://www.udemy.com/course/git-basico-ao-avancado-2021/). 

## Seção 1 - Intro


### Iniciando um repositório

```git init```
  
O comando cria a pasta oculta .git (para criar rep local). Normalmente usado quando vc cria rep local e decide versionalizá-lo depois. Neste caso, rep remoto tem que ser criado sem nenhum arquivo (nem readme.md).

```git remote add origin "url"```
  
Para conectar repositório remoto + rep local.

### Configurando repositório

```git config [--local|--global|--system] <key> [<value>]```
* --system aplica as conf. para todo rep. de todos os usuários do pc.
* --global aplica para todo rep. do usuário corrente
* --local aplica para o rep. corrente
  
Sendo que, caso tenha local, prevalece local, depois caso tenha global (e nao local), prevalece global, se não, prevalece a do sistema.
```--<key>``` poderia ser user.email "email"

-> definir como global email do trabalho
-> definir como local email pessoal

### Criando Aliases

```git config [--local|--global|--system] alias.<comando curto> <comando longo>```

```$git config --global alias.hist 'log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short'```
pretty define o seguinte formato:
* %h hash abreviado
* %ad data do commit
* %s comentário
* %d head de branch ou tag info
* %an nome do autor
* --graph pede formato ASCII

### Ajuda do git

```$git <comando> --help```
Abre pelo navegador.

```$git <comando> -help```
Abre direto na CLI do git.
  
##  Seção 2 - Iniciando com Git
