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

Primeiro commit. Após criar um rep vazio;

```$echo "hello world" >hello.txt```

echo não é comando do git e sim do SO.

```$ls ``` to list the files.

```$cat hello.txt``` to read txt content.

Agora precisamos enviar os arquivos para a area de **staging**.

```$git add hello.txt```

Ou posso usar ```$git add . ``` para adicionar TODOS os arquivos que estão ali.

Em seguida vamos fazer o commit, e adicionar (obrigatóriamente) um comentário ```-m "comentário"``` para aquele commit.
```$git commit -m "Creating hello.txt```

Para visualizar as alterações basta usar o comando ```$git show```.

Agora para enviar as alterações para o repositório remoto.

```$git push```

A branch local master ainda não possui uma branch de **rastreamento**.

```$git push --set-upstream origin master```

Ou eu posso substituir ```--set-upstream``` por ```-u```. Os próximos commits poderão ser realizados somente com ```git push```.

Se atualizar o site do github, os arquivos devem então aparecer ali.

O git id é o nome de um objeto git (40 caracteres). ```git hist``` o hash (SHA-1) dele em 7 caracteres.

No git, os conteúdos dos arquivos são armazenados em objetos chamados **blobs**. Blob não tem metadados.

Usamos -t ```$git cat-file -t <hash do primeiro commit>``` para mostrar o tipo de objeto. E -p para imprimir o conteúdo com base no seu tipo ```$git cat-file -p <hash do primeiro commit>```. O mesmo para blob, e os comandos: ```$git cat-file -t <hash do blob>``` e ```$git cat-file -p <hash do blob>```.

Quando entra uma nova pessoa no projeto, um clone precisa ser criado.
Internamente, o ```git clone``` excecuta um ```git init``` e ```git fetch```.

```git status``` mostra o status do rep. Se está tudo okay ou se tem arquivo em staging que precisa ser commitado.
Ele mostra também se o arquivo ainda não foi adicionado.

Se editar o arquivo (quando ja no staging), precisa dar um ```git add``` novamente senão o arquivo será perdido.
```git push``` para enviar ao repositório remoto. 

Untracked -> ```git add``` -> Staged -> ```git commit``` & ```git push```-> Unmodified -> modified -> loop entre os 3 últimos.

Untracked = não rastreado pelo git, não versionado.

## Seção 3 - Referências no Git
