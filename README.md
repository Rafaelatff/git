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

* ```git restore <nome do arquivo.extensão>``` para descartar alterações locais.
* ```git clean <nome do arquivo.extensão>``` descarta alterações nunca comitadas antes.
* ```git clean -f``` deleta todos os arquivos não rastreado
* ```git clean -n``` mostra primeiro os arquivos que serão apagados.
* ```git restore --staged``` descarta alterações do stage.
* ```git restore --source <hash do commit> <nome do arquivo>``` restalra versões anteriores em um arquivo.
* ```git revert HEAD --no-edit``` desfaz ultimo commit (antes de push no ex)
* ```git revert HEAD~1``` reverte penúltimo commit.
* ```git reset --soft head~``` preserva area de stage e de trabalho, mas voltando o commit.
* ```git reset --mixed head~``` preserva area de trabalho mas não de stagin.
* ```git reset --hard head~``` nem arquivos na area de trabalho e nem stagin.
* ```git reflog``` Recupera o histórico do projeto e recupera quase tudo. Usando dai ```git checkout <commit_hash>``` é possível recuperar um commit específico e em seguida ```dir``` é possível visualizar o arquivo no diretório. Pode aparecer mensagem de erro depois por a HEAD deixar de apontar para a branch atual, caracterizando um detached HEAD. Para resovler, é possível criar uma branch temporária ```git branch branch-temp```, seguido de um ```git checkout master``` e seguido de um ```git merge branch-temp```, que deve trazer as alterações da branch-temp para a master. E por fim, deletamos a branch temporária ```git branch -d branch-temp```.

**Reset** remove o commit e não deixa rastros no histórico. **Revert** gera um novo commit que desfaz o commit selecionado.

## Seção 5 - Merges, DAG e Conflitos

### Merge e Rebase

#### Merge fast-forward (avanço rápido)

* 1. Criar branch e alternar pra ela ```$git checkout -b icone```.
* 2. Criar arquivo icone.txt ```$touch icone.txt```.
* 3. Enviar arquivo pro stage ```$git add icone.txt```.
* 4. Comitar o arquivo ```$git commit -m "adding icon"```.
* 5. Vamos checar a branch icone ```$git hist```.
* 6. E alternar para a master e checar também ```$git checkout master```  e ```$git hist```. A branch do icone deverá estar a um commit na frente da master.
* 7. Para mergear usamos ```$git merge icone```. Podemos checar a mudança na master novamente usando o ```$git hist```.

Para visualizar a o histórico de uma branch, mesmo que não seja a branch corrente, podemos utilizar ```git log <nome da branch>``` ou  mesmo  ```git hist <nome da branch>```.

#### Merge Three-Way (recursiva)

* 1. Criar branch e alternar pra ela ```$git checkout -b menu```.
* 2. Criar arquivo menu.txt ```$touch menu.txt```.
* 3. Enviar arquivo pro stage ```$git add menu.txt```.
* 4. Comitar o arquivo ```$git commit -m "adding menu"```.
* 6. E alternar para a master ```$git checkout master```.

Agora antes de realizar o merde, vamos editar o icone.txt (enviado no exemplo anterior para a master), gerando um novo commit na master.

* 7. ```$echo "icone" > icone.txt```, ```$git add icone.txt``` e ```$git commit -m "changes in icone.txt"```.
* 8. Fazemos então o merge com a branch menu ```$git merge menu```.

Neste momento, o git irá exibir o editor de texto padrão para que seja inserido uma mensagem de commit. Manteremos a mensagem padrão. Nesse momento o git usou da estratégia recursiva, uma vez que não consegue apenas mudar o ponteiro do HEAD. Neste caso, é preciso mesclar com o commit feito direto na master. Podemos conferir o ponteiro usando *git hist*.

* 9. Para fazer isso, usamos o comando ```$git push```.

#### No fast-forward

Essa técnica é utilizada quando estamos mesclando uma ramigicação e desejamos garantir que quando a branch for incorporada na master, isto esteja visível no histórico. Isto é utilizado quando desejamos manter alguma topologia de ramificação específica.
Para isto, basta utilizarmos (não é usado na recursiva) a opção ```--no--ff``` durante o merge.

### DAG - Grafo Acíclico Dirigido

A estrutura que representa o histórico linear ou bifurcado no Git pode ser definida como DAG (Directed Acyclic Graph ou Grafo Acíclico Dirigido).

## Seção 6 - Trabalho colaborativo

### Fetch

Fetch fará o download do conteúdo remoto, mas não atualizará o  estado de funcionamento do seu repositório local, deixando intacto o trabalho atual.

Usando checkout na branch de rastreamento é possível então visualizar os arquivos. Precisa então fazer o merge para puchar para a área de trabalho.

### Pull
Ele baixa as alterações do repositório remoto e mescla com a área de trabalho (fetch e merge juntos).

## Seção 7 - Reescrevendo o histórico

### Rebase

* ```$git checkout -b notificacoes```, cria e muda para branch notificacoes.
* ```$touch notificacoes.txt``` gera arquivo txt.
* ```$git add .``` adiciona arquivos para area de stage.
* ```$git commit -m "adding notificacoes.txt``` commita o arquivo.
* ```$git checkout master``` volta para branch master.
* ```$echo "menu">menu.txt``` edita arquivo menu.
* ```$git add menu.txt``` envia para area de stage.
* ```$git commit -m "changes in menu"``` commita arquivo.
* ```$git checkout notificacoes``` volta para branch recém criada.
* ```$git rebase master``` neste momento, é como se o último commit fosse criado a partir do momento depois da modificação do arquivo menu, e não antes (como realmente aconteceu). Isso é feito para evitar um histórico cheio de bifurcações, ele fica mais linear.
* Terminamos então com um ```$git checkout master``` para ir para a branch master e ```$git merge notificacoes``` para, em modo fast-foward concretizar esta mudança na master.

Não recrie commits que existam fora do seu repositório e nos quais as pessoas possam ter trabalhado. O rebase recria commit então deve ser usado com cuidado.

Push forçado ```$git push -f```.

### Pull com rebase

* Pode ser criado pull com rebase ```$git pull --rebase```.

### Emendar commit

Quando esquecemos de commitar algo e queremos unir um novo commit ao anterior. Para isto: ```$git commit --amend -m "Adding brindes.txt with content"```. No entanto é preciso ter certeza que ninguém gerou uma branch nova baseada no commit anterior ou mesmo modificou o commit anterior.

### Squash merge

Junta diversos commits em um único. Basta usar ```$git merge --squash esquecisenha```, onde esquecisenha é o nome da branch. Termina com um ```$git commmit -m "message"```.


## Seção 8 - Outros conceitos e comandos

### Stash

No caso se eu trabalhar em brancha "nao master", e não comitar algo, ao eu dar um checkout e voltar para a branch master, eu acabo perdendo as coisas não commitadas em "nao master". 
Para isto, eu preciso usar o comando stash para salvar minhas modificações locais em uma pilhar e limpar minha área de trabalho para o último commit feito.

* ```git stash``` -> se não passar nada, ele executa um push junto por padrão. Por padrão ele não inclui arquivos untracked. Para salvar essas alterações precisa adicionar o comando *include untracked*.
* ```git stash list``` -> ele mostra o estado da pilha.
* ```git checkout banner``` -> agora é possível alternar para outra branch sem perder o trabalho não commitado.
* ```git stash apply stash@{1}``` para aplicar alterações de uma entrada específica.
* ```git stash pop``` -> remove o último, e do topo, item da pilha.
* ```git stash clear``` para limpar a lista.

### Blame

Blame mostra quem fez alteração em determinado arquivo commitado.

### Bisect 

Para identificar versão do projeto que esteja sem bug. 

### Pull Request

Permite uma revisão das alterações antes de realizar o processo de mesclagem de uma branch para a outra.
Ai você pode colocar outra pessoa para aprovar o *Merge pull request*. 

### Cherry-pick

Pode gerar commits duplicados no histórico, idealmente usar merge ou rebase para integrar os commits. Ele é usado para ajustar um commit em uma branch incorreta.
Usado para criar *hotfixes de bugs*. Usado para restaurar commits perdidos. 

### .gitignore

Arquivo utilizado para identificar componentes não versionados.

* ```arquivo*``` dentro do arquivo *.gitignore*, ignora todos os arquivos que começam com o nome *arquivo*.
* ```$mkdir build``` usando a CLI para gerar um diretório dentro daquele local com nome *build*.
* ```build/```dentro do arquivo *.gitignore*, ignora todo um diretório.
* O .gitignore não ignora arquivos e diretórios que já fazem parte do repositório ou da área do staging.
* ```$git restore --staged .``` remove todos os arquivos da area de staging.  
* ```$git rm --cached <nome do arquivo> <diretorio/nome do arquivo>``` usado para remover arquivos já versionados. O comando **--cached**, garante que os arquivos permaneçam na area de trabalho, mas com status untracked. Se não fosse utilizado este comando *--cached**, ele teria deletado os arquivos e diretório.

Curso recomenda este site, [toptal](https://www.toptal.com/developers/gitignore) para criar o arquivo .gitignore de acordo com o projeto. A seguir 2 exemplos:

No Altium: 
```
# Created by https://www.toptal.com/developers/gitignore/api/altium
# Edit at https://www.toptal.com/developers/gitignore?templates=altium

### Altium ###
# Previews Folders
**/__Previews/

# History Folders
**/History/*

# Project Logs
Project\ Logs*/

# Project Outputs
Project\ Outputs*/

# Auto-conversion notices
*.PcbDoc.htm

# Access lock file for dbLib sources
**/*.ldb


# End of https://www.toptal.com/developers/gitignore/api/altium
```

E no STM32CubeIDE (sad):
```
No results found
```

Encontrei recomendação em forum sobre usar o do *Eclipse*
```
# Created by https://www.toptal.com/developers/gitignore/api/eclipse
# Edit at https://www.toptal.com/developers/gitignore?templates=eclipse

### Eclipse ###
.metadata
bin/
tmp/
*.tmp
*.bak
*.swp
*~.nib
local.properties
.settings/
.loadpath
.recommenders

# External tool builders
.externalToolBuilders/

# Locally stored "Eclipse launch configurations"
*.launch

# PyDev specific (Python IDE for Eclipse)
*.pydevproject

# CDT-specific (C/C++ Development Tooling)
.cproject

# CDT- autotools
.autotools

# Java annotation processor (APT)
.factorypath

# PDT-specific (PHP Development Tools)
.buildpath

# sbteclipse plugin
.target

# Tern plugin
.tern-project

# TeXlipse plugin
.texlipse

# STS (Spring Tool Suite)
.springBeans

# Code Recommenders
.recommenders/

# Annotation Processing
.apt_generated/
.apt_generated_test/

# Scala IDE specific (Scala & Java development for Eclipse)
.cache-main
.scala_dependencies
.worksheet

# Uncomment this line if you wish to ignore the project description file.
# Typically, this file would be tracked if it contains build/dependency configurations:
#.project

### Eclipse Patch ###
# Spring Boot Tooling
.sts4-cache/

# End of https://www.toptal.com/developers/gitignore/api/eclipse
```

### Diff

* ```git diff``` compara a area de trabalho com a versão que a HEAD está apontando.
* ```git diff <nome do arquivo>``` compara as diferenças de apenas aquele arquivo.
* ```git diff head~..head``` compara penúltimo e último commit.
* ```git diff head~2..head``` compara anti-penúltimo com penúltimo commit.

### HTTPS x SSH

**Hypertext Transfer Protocol Secure**
Hypertext Transfer Protocol Secure (https) is a combination of the Hypertext Transfer Protocol (HTTP) with the Secure Socket Layer (SSL)/Transport Layer Security (TLS) protocol.

**Secure Socket Shell**
SSH, also known as Secure Shell or Secure Socket Shell, is a network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.

Platafomas de hospegagem GIT podem possuir repositórios públicos e privados, sendo necessário transferi-los de forma segura.
HTTPS não exige muita configuração, apenas usuário e senha.
SSH oferece mais segurança (> número de bits), sendo necessário gerar uma chave SSH localmente e cadastrá-la na plataforma de hospedagem.

* Para gerar chave SSH usar comando ```ssh-keygen```. Funciona tanto no Git Bash quanto CMD.

![image](https://github.com/Rafaelatff/git/assets/58916022/ae4c52b9-3f0f-4e6b-8595-0d4a7fc66654)

E então é gerado um par de chaves (criptografia de chave assimétrica) para ser configurado no repositório git.

![image](https://github.com/Rafaelatff/git/assets/58916022/b50b89a4-2ee5-4b62-a126-e4dc3c101694)

### Bare

Repositório Bare é gerado para ser o repositório de armazenamento, portanto não caracteriza como área de trabalho quando inicializamos com ```git init --bare```.
Usado quando a empresa usa um servidor local, e não um bitbucket ou github.
