## Como trabalhar em equipe - Melhorar o histórico de commits

1. Antes de começar qualquer coisa utilize o pull

Sempre utlize o pull antes de começar o seu projeto, sempre tenha ele sincronizado juntamente com o repositório principal do projeto.

2. Não faça commits dentro da master.

Nunca faça commits dentro da master a ideia vai ser sempre crie uma branch referente a nova funcionalidade que você está realizando. Use sempre uma branch por feature.

Em casos onde fazemos uma alteração e essa alteração for minima onde não há necessidade de ter mais um commit, usamos o comando **git commit -m 'Sua menssagem de commit' --amend**

Para que não seja necessario gerar um novo commit.
```git
  $ git status
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submet
ido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças
no diretório de trabalho)

        modified:   index.html

nenhuma modificação adicionada à submissão (utilize "git add" e/ou
 "git commit -a")
  $ git add .
  $ git commit -m 'Adiciona o novo nome do projeto'
[master 26dfee2] Adiciona o novo nome do projeto
 1 file changed, 2 insertions(+), 2 deletions(-)
```

Editamos o arquivo novamente e alteramos a sua indentação. Não tem necessidade de gerar um novo commit para isso, neste caso usamos o --amend.

```git
  $ git status
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudançasno diretório de trabalho)

        modified:   index.html

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
  $ git add .
  it commit -m 'Adiciona o novo nome do projeto e ajusta espaçamento' --amend
[master fd8f0d7] Adiciona o novo nome do projeto e ajusta espaçamento
 Date: Mon Oct 22 21:40:17 2018 -0300
 1 file changed, 2 insertions(+), 2 deletions(-
```

Agora quando exibimos o log.
```git
  $ git log --oneline
fd8f0d7 Adiciona o novo nome do projeto e ajusta espaçamento
```

Porém em alguns caso não seria bom usar o --amend. Por exemplo se os nossos arquivos já tivessem feito o push para o repositório isso iria gerar um conflito.

## Automerge - Resolver conflitos.
Imaginando a situação onde duas pessoas alteraram o mesmo arquivo e com isso gerando um conflito. Para resolver podemos usar o comando **git merge --abort**
```git
  $ git merge adiciona-texto
Mesclagem automática de index.html
CONFLITO (conteúdo): conflito de mesclagem em index.html
Automatic merge failed; fix conflicts and then commit the result.
```
Quando tentamos usar o merge o git nos mostra um conflito, usando o git diff podemos ver melhor onde se encontra o conflito.
```diff
  $ git diff
diff --cc index.html
index f8ed3ca,6beb775..0000000
--- a/index.html
+++ b/index.html
@@@ -9,7 -9,7 +9,11 @@@
  </head>
  <body>
    <h1>Curso Git e Github Ninja</h1>
++<<<<<<< HEAD
 +  <p>Git e github ninja</p>
++=======
+    <h2>Subtitulo do site</h2>
++>>>>>>> adiciona-texto
   <ul>
        <li>Curso Javascript Ninja</li>
        <li>Curso Git e Github Ninja</li>
(END)
```

Se usarmos o git merge --abort, o git irá cuidar do conflito.
```git
  $ git merger --abort
  $ git status
No ramo dev
nada a submeter, diretório de trabalho vazio
```

Ou podemos resolver o conflito de outra forma. De forma manual.

O git ele só não consegue fazer o automerge se as mesmas linhas forem alteradas de formas diferentes, se alteramos linhas distantes o git consegue fácilmente fazer o merge.

## Merge tool

Para melhorar ainda mais o nosso trabalho temos disponível dentro do git uma ferramenta chamada meld. Que nos ajuda muito a resolver conflitos.

[Para saber mais](http://meldmerge.org/)