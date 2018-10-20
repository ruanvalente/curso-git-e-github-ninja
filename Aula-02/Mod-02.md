# Mod-02 
## Adicionando arquivos.
Para adicionar arquivos no git, podemos pegar os exemplos das aulas anteriores.
```git
  $ touch style.css
  $ git status
No ramo master
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

        style.css

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```
O git nos mostra que o arquivo não está sendo monitorado, e precisamos usar o comando git add para que ele passe do nosso Working directory para a nossa Staging area. Usando o git add.
```git
  $ git add .
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

        new file:   style.css
```
Agora que o nosso arquivo está na Staging area podemos commitar para que o mesmo fique agora no nosso Git Repository.
```git
  $ git commit -m 'Adicionado o style.css novamente'
  $ git status
No ramo master
nada a submeter, diretório de trabalho vazio
```
Agora vamos modificar remover o style.css e modificar o index.html.
```sh
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    style.css

Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

        modified:   index.html
```
Usando o git diff podemos ver as modificações.
```diff
diff --git a/index.html b/index.html
index 0d0a326..1598140 100644
--- a/index.html
+++ b/index.html
@@ -8,5 +8,11 @@
 </head>
 <body>
   <h1>Curso Git e Github Ninja</h1>
+
+ <ul>
+       <li>Curso Javascript Ninja</li>
+       <li>Curso Git e Github Ninja</li>
+       <li>Curso React Ninja</li>
+</ul>
 </body>
-</html>
\ No newline at end of file
+</html>
```
Agora podemos usar o git add para adicionar os arquivos. Porém, temos um pequeno detalhe. Quando o git ignora um dos arquivos podemos adiciona-los através do comando **git add --all ou git add -A**
```git
  $ git add --all 
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

        modified:   index.html
        deleted:    style.css
```
Lembre-se as mudanças que forem feitas só podem ser commitadas dessa forma se forem relevantes ao que foi feito no arquivo do projeto.
```git
  $ git commit -m 'Adicionado lista de cursos no index.html e removido o style.css'
[master fa879bc] Adicionado lista de cursos no index.html e removido o style.c
ss
 2 files changed, 7 insertions(+), 1 deletion(-)
 delete mode 100644 style.css

  $ git status
No ramo master
nada a submeter, diretório de trabalho vazio
```

## O arquivo .gitignore part1
O gitignore é um arquivo simples que lista o que o Git deve ignorar quando você estiver trabalhado no repositório, de forma que seja possível evitar a adição de arquivos indesejados no repositório sem dificuldades, tornando os arquivos indesejados totalmente invisíveis ao Git.
```git
  $ git status 
No ramo master
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)
        node_modules/
        package-lock.json
        package.json

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar
```
Está pasta chamada **node_modules** ela contem os modulos da nossa aplicação node. Porém essa pasta não é necessaria ser versionada pelo git. Então assim, podemos criar o arquivo **.gitignore**.
```zsh
  $ echo "node_modules" >> .gitignore
```
E agora rodando o comando git status vemos que a nossa pasta node_modules não está mais sendo vista pelo git.
```git
  $ git status
No ramo master
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

        .gitignore
        package-lock.json
        package.json

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```
Agora podemos commitar as alterações, e também podemos ignorar qualquer outro arquivo, adicionando ele no arquivo .gitignore

## O arquivo .gitignore ( Parte 2)
E quando acontece de você sem querer adicionar todo o conteúdo da pasta node_modules ? Como podemos reverter essa situação ?
```git
commit 058872455c2bb554f67a163d2af7aa8cb44111a4
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 19:22:38 2018 -0300

    Removido o arquivo .gitignore

D       .gitignore
A       node_modules/.bin/atob
A       node_modules/.bin/color-support
A       node_modules/.bin/gulp
A       node_modules/.bin/mkdirp
A       node_modules/.bin/semver
A       node_modules/.bin/strip-bom
A       node_modules/.bin/user-home
A       node_modules/.bin/which
A       node_modules/ansi-gray/LICENSE
A       node_modules/ansi-gray/index.js
```
E o arquivo é grande....

E agora como resolver ?
Podemos remover a pasta node_modules de dentro do nosso arquivo isso resolveria ? Sim, porém digamos que precisamos da pasta, mas só queremos que o arquivo da node_modules seja removido da Staging area sem remover o arquivo da nossa maquina. Usamos o comando **git rm -rf node_modules --cached**.
```git
  $ git rm -rf node_modules/ --cached
rm 'node_modules/has-ansi/package.json'
rm 'node_modules/has-ansi/readme.md'
rm 'node_modules/has-gulplog/LICENSE'
rm 'node_modules/has-gulplog/README.md'
rm 'node_modules/has-gulplog/index.js'
rm 'node_modules/has-gulplog/package.json'
rm 'node_modules/has-value/LICENSE'
rm 'node_modules/has-value/README.md'
rm 'node_modules/has-value/index.js'
rm 'node_modules/has-value/package.json'
```
E por ai vai.....

Agora podemos adicionar a nossa pasta node_modules dentro do arquivo .gitignore para que assim a mesma não seja vista pelo git.
```git
  $ echo node_modules >> .gitignore
  $ git status
        deleted:    node_modules/is-plain-object/index.d.ts
        deleted:    node_modules/is-plain-object/index.js
        deleted:    node_modules/is-plain-object/package.json
        deleted:    node_modules/is-relative/LICENSE
        deleted:    node_modules/is-relative/README.md
        deleted:    node_modules/is-relative/index.js
        deleted:    node_modules/is-relative/package.json
        deleted:    node_modules/is-unc-path/LICENSE
        deleted:    node_modules/is-unc-path/README.md
```

E por ai vai...

## O arquivo .gitignore ( Parte 3 )
Agora como podemos adicionar um arquivo ao .gitignore sendo que o mesmo já se encontra na Staging area ?
Assim como no exemplo a cima, usamos o comando:
```git
  $ git rm -rf package.json --cached
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

        modified:   package.json

Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

        .gitignore
        package-lock.json
```
Podemos também adicionar e commitar ao mesmo tempo. Usando o comando: **git add -a -m 'Mais uma menssagem de commit'**. ou usando **git add -am 'Mais uma menssagem de commit'**.

PS: O comando **am** funciona em alguns sistemas operacionais.

```git
  $ git commit -a -m 'Adiciona DS_Store ao .gitignore'
[master 38a246a] Adiciona DS_Store ao .gitignore
 1 file changed, 1 insertion(+)
  $ git status
No ramo master
nada a submeter, diretório de trabalho vazio
```
Já mostra para nos que foi realizado a adição e o commit ao mesmo tempo.

Podemos também adicionar um arquivo .gitignore na raiz da nossa pasta de usuário e através das configurações globais do git, podemos apontar para essa pasta e realizar a configuração.
```
  $ git config core.excludefiles
  $ git config --global core.excludesfiles ~/.gitignore
```
Passamos para o core.excludesfiles o nosso arquivo .gitignore criado na nossa raiz do usuário.

## Commit sem parâmetro
Podemos criar commits personalizados de forma que podemos detalhar ainda mais o que o que está sendo feito no arquivo.

```git
  $ git status
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

        modified:   .gitignore

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
  $ git add .
  $ git status
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

        modified:   .gitignore
  $ git commit 
```
Relizando apenas essa opção o git irá abrir o seu editor configurado o padrão no meu caso é o nano ( Ubuntu ), e assim podemos começar a detalhar o nosso commit no inicio do documento.

Agora verificando através do git log temos como as menssagems de commit.
```git
  $ git log 
commit 601df12f4f08f969c3baf32fc9e45b3d48d1e97f
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 20:16:23 2018 -0300

    Titulo do commit
    Corpo do commit
    - Item adicionado
    - Item removido
    - Outros detalhes
```
Podemos configurar o editor e também outra configurações para nos ajudar no processo do git.

Usamos o comando **git config --list** para listar as configurações do git.
```git
  $ git config --list
user.name=Ruan Valente
user.email=ruanopensuselinux@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```
Para configurar o editor usamos o a configuração global.
```git
  $ git config --global core.editor vim
```
Agora o nosso editor está configurado.

## Git log
Dentro do comando git log temos alguns comando interessantes para melhorar ainda mais a nossa vida, um deles é o **git log --pretty=oneline**.

Que retorna todos os commits em uma unica linha de forma que fica ainda mais simples de se visualizar.

```git
  $ git log --pretty=oneline
601df12f4f08f969c3baf32fc9e45b3d48d1e97f Titulo do commit Corpo do commit - Item adicionado - Item removido - Outros detalhes
38a246a80e63e3280a957c36ef6e8477bb9037c2 Adiciona DS_Store ao .gitignore
9fb06cd1920bf7ed12d38319a5cc8cdf5136a83f Modificado o arquivo package.jon e remove a pasta node_modules de dentro da Stagin area
058872455c2bb554f67a163d2af7aa8cb44111a4 Removido o arquivo .gitignore
851cf1686aeb9e5660b1d626ecbe6188a0396679 Adicionado o arquivo package.json e o arquivo package-lock.json
f340b0598f990c7f2de0cc16e808f8981f58a1cf Adicionado o arquivo .gitignore
fa879bc60cabb848dc54fd5ac25b4051e691493d Adicionado lista de cursos no index.html e removido o style.css
afa316469399a52cd0f671eb86237abc6d3b0bed Adicionado o style.css novamente
cc7a47993cb5f96e11740634e6a81cd5cff3c9b3 Removido style.css
d5e2c8fec31bb926acdcc5cfc4766794be1ea25c Adicionado style.css
c13448e7c51467c2f3395a16dee671ffb5600aeb Adicionado o arquivo style.css
a07fdd97b5ee51c8c54a39b8df9d9729e3a9504a Adicionado conteúdo do html5
adbbb2c46ac835a7601ac96f0b0e285f2f9e7a78 Adiciona arquivo index.html
```
Temos também o **git log --abbrev-commit** que vai abreviar o nosso commit, e deixando a nossa hash do os 7 primeiros digitos.

```git
commit 601df12
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 20:16:23 2018 -0300

    Titulo do commit
    Corpo do commit
    - Item adicionado
    - Item removido
    - Outros detalhes

commit 38a246a
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 19:57:25 2018 -0300

    Adiciona DS_Store ao .gitignore

commit 9fb06cd
```
Também podemos juntar comandos de log para ter uma saida ainda melhor.

```git
  $ git log --pretty=oneline --abbrev-commit
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
Também temos o **git log --stat** que mostras as estatísticas de commit.
```git
  $ git log --stat
commit 601df12f4f08f969c3baf32fc9e45b3d48d1e97f
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 20:16:23 2018 -0300

    Titulo do commit
    Corpo do commit
    - Item adicionado
    - Item removido
    - Outros detalhes

 .gitignore | 1 -
 1 file changed, 1 deletion(-)
```

Outro comando interessante é o **git log -p** que mostra o log das alterações do arquivo.

```git
  $ git log -p
commit 601df12f4f08f969c3baf32fc9e45b3d48d1e97f
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Fri Oct 19 20:16:23 2018 -0300

    Titulo do commit
    Corpo do commit
    - Item adicionado
    - Item removido
    - Outros detalhes

diff --git a/.gitignore b/.gitignore
index 6db4ce0..3c3629e 100644
--- a/.gitignore
+++ b/.gitignore
@@ -1,2 +1 @@
 node_modules
-DS_Store
```
OBS: Podemos passar também um número, cujo a função é determinar o número de commit que será mostrado.