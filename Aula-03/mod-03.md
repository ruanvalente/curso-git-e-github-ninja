## Git Branch
São ramificação, no controle de revisão e gerenciamento de configuração de software, é a duplicação de um objeto sob controle de revisão para que as modificações possam ocorrer em paralelo ao longo de ambas as ramificações. 

Para listar as branchs dentro de um projeto, usamos o comando **git branch** que irá listar cada branch do nosso projeto.
```git
  $ git branch
  * master
```

[Para saber mais sobre Branch](https://git-scm.com/book/pt-br/v1/Ramifica%C3%A7%C3%A3o-Branching-no-Git-O-que-%C3%A9-um-Branch)

Para criar uma nova **branch** usamos o comando **git branch nome-da-branch**.
```git
  $ git branch css
```
Agora se pedirmos para o git mostrar as branchs existentes no projeto, ele mostrar a branch que criamos. A **css**.
```git
  $ git branch
    css
  * master
```

Precisamos entender que quando criamos uma nova a branch, ela sempre irá se basear na branch atual. Ou seja, com o mesmo conteúdo com os mesmos arquivos.

Tudo que você alterar em uma branch **não será afetado** na outra. Isso quer dizer que uma difere da outra !

Para acessar a branch que criamos usamos o comando **git checkout nome-da-branch**.
```git
  $ git checkout css
Switched to branch 'css'
```

O git mostra que agora estamos trabalhando na branch **css**.

Agora dentro dessa nova branch podemos altera o que for necessário no projeto sem que isso altere algo na branch principal, no caso a master.

## Git branch ( parte 2 )
Como vimos anteriormente podemos criar uma "ambiente" separado para assim trabalhar dentro da nova funcionalidade que precisamos. E usando as branchs podemos muito bem criar uma nova funcionalidade e juntar com branch principal.

Para isso usamos o comando **git merge nome-da-branch**, assim pegamos as alterações que fizemos dentro da branch **css** e juntamos ( merge ) dentro da branch principal, no caso a **master**.
```git
  $ git merge css
Updating 601df12..83bd293
Fast-forward
 css/main.css | 0
 index.html   | 1 +
 2 files changed, 1 insertion(+)
 create mode 100644 css/main.css
```

Agora se formos acessar tanto log quanto os arquivos vamos notar que as alterações feitas dentro da nossa branch **css** agora fazem parte da branch **master**.

Podemos usar um conceito simples de como trabalhar com branchs, podemos criar uma branch **dev** e nela podemos fazer todos os testes e tudo que for relacionado a desenvolvimento.

Podemos criar uma branch relacionada a alguma funcionalidade criada para o nosso projeto. 

E por fim usamos o merge para juntar essas funcionalidades em uma nova versão do nosso projeto.

## Git branch ( parte 3 )
Podemos criar e acessar a branch usando o comando **git checkout -b nome-da-branch**

Podemos também renomear uma branch usamos o comando **git branch -m nome-da-nova-branch**

Precisamos estar dentro da branch para realizar essa modificação.
```git
  $ git checkout -b teste
Switched to a new branch 'teste'
```

Como vimos anteriormente o comando **git checkout -b nome-da-branch** já cria e entra dentro da branch. 

E agora para renomear a branch usamos o comando **git branch -m nome-da-nova-branch**
```git
  $ git branch -m nova-branch

  $ git branch
* nova-branch
```

Podemos também remover as branch usando o comando **git branch -D nome-da-branch**
```git
  $ git branch
  
  css
  dev
  js-default
  master
* nova-branch
  style-css
```
Agora podemos remover as branch que são desnecessárias para nós.
```git
  $ git branch

  dev
* master
```
Sempre trabalhando no fluxo de criar uma branch para novas funcionalidade e depois juntar isso dentro da branch dev e quando tudo estiver funcionando 100%, podemos juntar com a branch master.

Podemos também criar uma branch vázia, isso quer dizer que a branch não terá nenhum tipo de histórico de outras branch. A mesma virá sem nenhum arquivo.

Usando o comando **git checkout --orphan site**
```git
  $ git checkout --orphan site
No ramo site

Submissão inicial.

Mudanças a serem submetidas:
  (utilize "git rm --cached <arquivo>..." para não apresentar)

        new file:   .gitignore
        new file:   css/main.css
        new file:   index.html
        new file:   package-lock.json
        new file:   package.json
```

Os arquivos aparecem na stagin area como se tivéssemos adicionado eles para a stagin area. Porém se quisermos podemos remover todos os arquivos usando o **git rm .** que remove o conteúdo de um diretório atual.
```git
  $ git rm -rf .
rm '.gitignore'
rm 'css/main.css'
rm 'index.html'
rm 'package-lock.json'
rm 'package.json
```
Agora se formos verificar pelos arquivos que estão dentro do nosso Working directory nada mais é do que a pasta node_modules, porém podemos removê-la e começar um projeto totalmente do zero.
```git
  $ rm -rf node_modules
  $ git status
No ramo site

Submissão inicial.

nada para enviar (crie/copie arquivos e use "git add" para registrar)
```

Pronto, branch totalmente vázia :smile:

## Criando repositórios.
Podemos criar uma repositório local dentro da nossa máquina usando o comando **git init --bare**

Para criar o repositório local em nossa máquina precisamos definir uma pasta que por convenção  terá o mesmo nome da pasta do projeto seguinda de .git no final
```zsh
  $ mkdir my-oroject.git
```

Agora entramos na pasta que criamos e utilizamos o comando **git init --bare**
```git
  $ git init --bare
Initialized empty Git repository in /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/my-project.git/
```

Agora se formos listar o conteúdo desse diretório temos algo similar ao que acontece na pasta .git.
```git
  $ ll
total 32K
drwxrwxr-x 2 ruan ruan 4.0K Oct 22 19:31 branches
-rw-rw-r-- 1 ruan ruan   66 Oct 22 19:31 config
-rw-rw-r-- 1 ruan ruan   73 Oct 22 19:31 description
-rw-rw-r-- 1 ruan ruan   23 Oct 22 19:31 HEAD
drwxrwxr-x 2 ruan ruan 4.0K Oct 22 19:31 hooks
drwxrwxr-x 2 ruan ruan 4.0K Oct 22 19:31 info
drwxrwxr-x 4 ruan ruan 4.0K Oct 22 19:31 objects
drwxrwxr-x 4 ruan ruan 4.0K Oct 22 19:31 refs
```

## Adicionando repositórios ao seu projeto

Podemos usar o comando **git remote add origin repository**

O comando nos mostra que estamos adicionando **( add )** um repositório remoto **( remote )**, e que seu nome é **origin** e passamos o endereço do repositório que desejamos ser adicionado **( repository )**.

OBS: Toda vez que formos usar um repositório que vai ser o principal ou que vai gerenciar o projeto, chamamos ele de **origin**.
```git
  $ git remote add origin /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/my-project.git
```
Agora temos um link entre o repositório my-project.git com o repositório my-project.

Podemos verificar isso usando o comando **git remote -v**
```git
  $ git remote -v
origin  /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/my-project.git (fetch)
origin  /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/my-project.git (push)
```

## Sincronizando ambiente local com repositório remoto
Podemos usar o comando **git push origin branch** que vai sicronizar o nosso repositório.

**PUSH** = empurrar.

Então todos os arquivos contidos no nosso repositório seram "empurrados" **push** para o repositório origin na branch master do nosso repositório local.
```git
  $ git push origin master
Counting objects: 1691, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (1550/1550), done.
Writing objects: 100% (1691/1691), 1.24 MiB | 0 bytes/s, done.
Total 1691 (delta 392), reused 0 (delta 0)
To /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos
/my-project.git
 * [new branch]      master -> master
```
Agora se formos dentro do nosso repositório e executar o comando **git log** temos todos os logs do nosso repositório sincronizados.
```git
  $ git log --oneline
83bd293 Adicionado a pasta css
0763cce Adicionado link css no arquivo
601df12 Titulo do commit Corpo do commit - Item adicionado - Item removido - Outros detalhes
38a246a Adiciona DS_Store ao .gitignore
9fb06cd Modificado o arquivo package.jon e remove a pasta node_modules de dentro da Stagin area
0588724 Removido o arquivo .gitignore
851cf16 Adicionado o arquivo package.json e o arquivo package-lock.json
f340b05 Adicionado o arquivo .gitignore
fa879bc Adicionado lista de cursos no index.html e removido o style.css
afa3164 Adicionado o style.css novamente
cc7a479 Removido style.css
d5e2c8f Adicionado style.css
c13448e Adicionado o arquivo style.css
a07fdd9 Adicionado conteúdo do html5
adbbb2c Adiciona arquivo index.html
```

Podemos também clonar repositórios existentes.

Usamos o comando **git clone repository**.

Dessa forma podemos ter o seguinte caso. Estamos trabalhando em um time, e esse time está desenvolvendo um projeto. Cada pessoa do time pode clonar o respositório do projeto e fazer a suas modificações e manda-las para o servidor local, no caso o nosso repositório. Assim, cada pessoa do time poderá fazer a sua modificação de forma isolada sem mexer na master.

Agora imagine que uma pessoa do time fez a alteração e essa alteração foi commitada e está no nosso repositório local. Porém a outra pessoa do time fez também outra alteração, adicionou arquivos e fez o commit. Isso irá gerar um erro, dizendo que não foi feita a sicronização do repositório. Para isso usamos o comando **git pull origin branch**.

**PULL** = puxar.
```git 
  $ git push origin master
To /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/projeto
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to '/home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/projeto'
dica: Updates were rejected because the remote contains work that you do
dica: not have locally. This is usually caused by another repository pushing
dica: to the same ref. You may want to first integrate the remote changes
dica: (e.g., 'git pull ...') before pushing again.
dica: See the 'Note about fast-forwards' in 'git push --help' for details.
```
Agora para podemos fazer as alterações precisamos sincronizar o nosso repositório com o respositório local.
```git
  $ git pull origin master
warning: no common commits
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/projeto
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
Merge made by the 'recursive' strategy.
 index.html | 12 ++++++++++++
 1 file changed, 12 insertions(+)
 create mode 100644 index.html
```
Agora com o repositório sincronizado podemos commitar as nossas alterações.
```git
  $ git push origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (6/6), 628 bytes | 0 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To /home/ruan/Workspace/Cursos-Ninjas/git-e-github-ninja/git-e-github-exemplos/projeto
   7a5f7f2..25e0577  master -> master
```

Sempre que formos começar antes de qualquer coisa, precisamos atualizar o nosso repositório com o repositório principal usando o git pull :tada: