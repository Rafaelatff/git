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

### Criando e alternando entre branchs

HEAD - é a versão que estamos trabalhando (master, branch). Para visualizar basta: 
```$cat. git/head```.

CHECKOUT utilizado para criar e alternar branchs. 
* ```git checkout [<referência> | <commit>]```
* ```git branch <nome da nova branch>``` apenas cria uma nova branch
* ```git branch -c <nome da branch específica> <nome da nova branch>``` para criar a branch a partir de uma outra branch
* ```git checkout -b <new branch>``` onde cria uma nova branch e alterna para a mesma.
* ou ```git checkout <branch>~1``` para alternar para o penúltimo commit da branch em questão.

Para listar todas as nossas branchs (locais em branco e de rastreamento em vermelho), usar o camndo:
```git branch -a```. Opção com asterisco é nossa branch corrente.

Branch recém criada ainda não possuí rastreamento. Se dermos git commit e git push será retornado uma mensagem de erro.
Usar novamente o comando ```git push -u origin <branch name>```. Conferir usando ```git branch -a```, a branch deve aparecer em vermelho. 
Isso precisa ser feito porque, assim como podemos ter mais de uma cópia dos arquivos em repositórios locais, podemos ter também os mesmos arquivos em mais de um repositório remoto.
Para conferir qual o repositório remoto, usar: ```git remote get-url origin```.

Corrigir nome de branch em rep local:
* ```$git branch -m "banner"``` para mudar nome da branch atual.
* ```$git branch -m "<nome antigo>" "<nome novo>"``` para alterar o nome de outra branch.

Corrigir nome de branch rem rep remoto:
* ```$git push origin :baner``` para deletar a branch com nome errado, ou
* ```$git push origin --delete baner```, e então:
* ```$git push -u origin banner``` para criar a nova com nome correto.

### Tags

Usada para colocar versão de projeto.
* Tag leve: ```$git tag todo-primeiro-acesso``` pouco usada por não adicionar info de projeto. Usada para uso privado ou temporário.
* Tag anotadas: usando -a adiciona informações de quem criou, quando criou e uma mensagem de anotação.
* ```$git tag -a "v1.0" -m "first version"``` para criar tag.
* ```$git show v1.0``` para mostrar referência da tag.
* ```$git tag -d todo-primeiro-acesso``` para deletar tag.

Tag está apenas no rep local, para enviar a tag para o repositório remoto, git push não é suficiente.
Precisa utilizar o comando ```$git push --tags```.

Para que o *push* envie commits e tags simultaneamente, precisamos adicionar para o arquivo de configuração git a propriedade *push.followTags* com valor de *true*.
* ```git config --local push.followTags true``` adiciona em rep local
* ```git config --global push.followTags true``` adiciona em todos os rep do usuário corrente do SO
* ```git config --system push.followTags true``` adiciona para todos os usuários do SO

Para mais info consultar post do [professor](https://dev.to/rsantanarj/entenda-conceitos-basicos-sobre-git-d2f).

## Seção 4 - Descartando alterações
