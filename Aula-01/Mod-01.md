# Curso Git e Github Ninja
# Mod-01 
### Pré-requistos ?

- Conhecimento do OS.
- Conhecimento básico do terminal.

### O que é o Git ?

Git é um sistema de controle de versões distribuído, usado principalmente no desenvolvimento de software, mas pode ser usado para registrar o histórico de edições de qualquer tipo de arquivo.

### Instalação

[Link para instalaçao](https://git-scm.com/)

Com isso podemos usar o comando **git** dentro do nosso sistema. Usando a flag --help
temos todas as opções e funcionalidades dentro do Git.

```
 $ git --help
```

### Inicializando o git 

Para que o git comece a assistir o nosso diretório precisamos dar o comando **git
 init** dentro da pasta que desejamos que seja versionada.

 ```
  $ git init 
 ```

 ### Git Status

Usamos esse comando para checar o estado atual do repositório.

```
 $ git status
 No ramo master

Submissão inicial.
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

        index.html

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```

## Mod-01 Aula 02 - Configurações Iniciais.

No capítulo anterior entendemos algumas funções básicas do git, e hoje vamos continar
entendendo como funciona os **estágios** dentro do git.
## Estágios do Git
![Estágios do git](https://git-scm.com/figures/18333fig0106-tn.png)

## Working Directory 
É o nosso diretório de trabalho ainda não listado dentro da árvore git.

## Staging area
Quando usamos o comando **git add file** estamos passando o nosso arquivo para a Staging area. Com isso o git ficará monitorando cada alteração do nosso arquivo.

```
  $ git add index.html
  $ git status 
  
  No ramo master

Submissão inicial.

Mudanças a serem submetidas:
  (utilize "git rm --cached <arquivo>..." para não apresentar)

        new file:   index.html

```
## Git Directory (repository)
Para que o nosso arquivo esteja no Git Directory, precisamos commitar o nosso arquivo. Usando o **git commit**, porém antes disso precisamos dizer ao git, quem irá commitar estes arquivos.
Fazendo as seguintes configurações.

```
  $ git config --global user.name = "Seu Nome"
```

Nesta linha definimos o nome do usuário que o git irá usar para referenciar o commit feito no arquivo.
E praticamente da mesma forma podemos passar o e-mail.
```
  $ git config --global user.email = "seuemail@email.com"
```
OBS: Se você quiser listar as configurações do seu git, você pode usar o comando
**git -l**

Dessa forma podemos usar o comando **git commit -m "E a menssagem de commit"**
``` 
  $ git commit -m "Minha menssagem"
```

Agora o nosso arquivo passou da Staging area para o git repository. :tada:

OBS: Quando formos commitar precisamos ser o mais claro possível naquilo que estamos
falando dentro do nosso commit. Pois outros programadores irão se basear nas nossas
menssagens de commits e também em nossos códigos.

Após isso o nosso Working Directory fica limpo, mostrando que o nosso arquivo está dentro
do git repository.

```
  $ git status

  No ramo master
  nada a submeter, diretório de trabalho vazio
```

## Mod-01 Aula 03 - Ver logs de arquivos

O git também nos permite ver os logs de arquivos usando o comando:
```
  $ git log
commit adbbb2c46ac835a7601ac96f0b0e285f2f9e7a78
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 20:06:42 2018 -0300

    Adiciona arquivo index.html
(END)
```
O comando retorna todos os commit feitos no arquivo. Quando alteramos novamente o nosso arquivo o mesmo volta para o nosso Working Directory, assim quando alteramos o arquivo podemos visualizar o que foi modificado dentro do mesmo. Para saber quais foram as linhas adicionadas ou removidas usamos o comando **git diff** que mostra em detalhes essas alterações.

```
  $ git status
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

        modified:   index.html

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
```

Agora vimos que o nosso arquivo foi modificado porém não está na Staging area, queremos verificar o seu conteúdo alterado, então usamos o comando **git diff**

```diff
  $ git diff
diff --git a/index.html b/index.html
index e69de29..0d0a326 100644
--- a/index.html
+++ b/index.html
@@ -0,0 +1,12 @@
+<!DOCTYPE html>
+<html lang="en">
+<head>
+  <meta charset="UTF-8">
+  <meta name="viewport" content="width=device-width, initial-scale=1.0">
+  <meta http-equiv="X-UA-Compatible" content="ie=edge">
+  <title>Titulo</title>
+</head>
+<body>
+  <h1>Curso Git e Github Ninja</h1>
+</body>
+</html>
\ No newline at end of file
```

## Mod-01 Aula 04 - Trabalhando com mais arquivos.

Podemos adicionar vários arquivos de uma só vez ou adicionar arquivo por arquivo.
```
  $ git add file1 file2 file3....
```
ou podemos usar o **ponto ( . )**  que simboliza o nosso diretório atual.
```diff
  $ git diff
  diff --git a/syle.css b/syle.css
index 0e113e4..736db41 100644
--- a/syle.css
+++ b/syle.css
@@ -1,10 +1,11 @@
 * {
+  box-sizing: border-box;
+  outline: none;
   padding: 0;
   margin: 0;
-  outline: none;
-  box-sizing: border-box;
 }

-h1 {
-  color: #fff;
+body {
+  font-family: Arial, Helvetica, sans-serif;
+  font-size: 18px;
 }
\ No newline at end of file
(END)
  $ git add . 
```

Porem quando precisamos verificar se o que modificamos na Staging area é igual ao conteúdo do arquivo do git repository ? Como podemos verificar a comparação desses arquivos ? Podemos usar o comando **git diff --staged**.

```diff
  $ git diff --staged
diff --git a/syle.css b/syle.css
index 0e113e4..736db41 100644
--- a/syle.css
+++ b/syle.css
@@ -1,10 +1,11 @@
 * {
+  box-sizing: border-box;
+  outline: none;
   padding: 0;
   margin: 0;
-  outline: none;
-  box-sizing: border-box;
 }

-h1 {
-  color: #fff;
+body {
+  font-family: Arial, Helvetica, sans-serif;
+  font-size: 18px;
 }
\ No newline at end of file
(END)
```
O retorno na tela do comando compara o que está na nossa **Staging area** com o nosso **Git Repository**. Porém quando usamos apenas o git diff sem a flag --staged, estamos comparando os arquivos que estão no nosso **Working Directory** com a **Staging area**. 

## Mod-01 Aula 05 - Voltando no tempo - Diff de commits

Sabemos que podemos verificar as alterações nos arquivos usando o comando diff. Podemos também vericar comparando pelo nosso Working Directory com a Staging area ou da Staging area com o Git Repository.
Usando os comandos respectivamente.
```
  $ git diff file
```

```
  $ git diff file2
```

```
  $ git diff --staged
```

E verificamos tudo usando o git log, que nos mostra o log de todos os commits feitos até então.
```
  $ git log 
  commit d5e2c8fec31bb926acdcc5cfc4766794be1ea25c
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 22:05:41 2018 -0300

    Adicionado style.css

commit c13448e7c51467c2f3395a16dee671ffb5600aeb
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 21:46:21 2018 -0300

    Adicionado o arquivo style.css

commit a07fdd97b5ee51c8c54a39b8df9d9729e3a9504a
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 21:28:23 2018 -0300

    Adicionado conteúdo do html5

commit adbbb2c46ac835a7601ac96f0b0e285f2f9e7a78
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 20:06:42 2018 -0300

    Adiciona arquivo index.html
(END)
```

A primeira linha, mostra a hash do commit, a segunda linha o nome, e-mail, data, dia e hora do commit. E por fim a menssagem do commit.

E também podemos usar o comando **git log --name-status** para visualizar os nomes dos arquivos que foram alterados.
```
  $ git log --name-status
commit d5e2c8fec31bb926acdcc5cfc4766794be1ea25c
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 22:05:41 2018 -0300

    Adicionado style.css

M       syle.css

commit c13448e7c51467c2f3395a16dee671ffb5600aeb
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 21:46:21 2018 -0300

    Adicionado o arquivo style.css

A       syle.css

commit a07fdd97b5ee51c8c54a39b8df9d9729e3a9504a
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 21:28:23 2018 -0300

    Adicionado conteúdo do html5

M       index.html

commit adbbb2c46ac835a7601ac96f0b0e285f2f9e7a78
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 20:06:42 2018 -0300

    Adiciona arquivo index.html

A       index.html
(END)
```
No caso o **A** para *adicionado* e **M** para *modificado.*

Podemos também comprar dois commits usando o diff 

```
  $ git diff commit commit2 
```
```
  $ git diff a07fdd97b5ee51c8c54a39b8df9d9729e3a9504a
```
Podemos usar a hash do nosso commit. Também podemos colocar os primeiros 7 caracteres 
para verificar atraves do diff
```
  $ git diff a07fdd9
```
que teremos o mesmo resultado.

### Mod-01 Aula 06 - Remover arquivos.
Quando precisamos remover um arquivo da nossa árvore de diretórios usamos o comando
**git rm file**.

```
  $ git rm style.css
```
Quando removemos percebemos que temos uma nova mudança a ser commitada no nosso repositório.

```
  $ git status
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    syle.css
```

Agora temos um status **Deleted**, porém quando fazemos isso precisamos commitar tal aleração. Dizendo que o mesmo foi removido e se usarmos o git log veremos mais um novo status, o **D**.

```
  $ git log --name-status
  
commit cc7a47993cb5f96e11740634e6a81cd5cff3c9b3
Author: Ruan Valente <ruanopensuselinux@gmail.com>
Date:   Wed Oct 17 22:59:39 2018 -0300

    Removido style.css

D       syle.css
```
