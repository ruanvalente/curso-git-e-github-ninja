## Trabalhando em equipe part 1 e 2
OBS: No exemplo do curso é dado que podemos usar o github para trabalhar em equipe. As anotações serão apenas de conceitos importantes de como devemos trabalhar em 
equipe.

No curso é configurado duas contas no github que mostra como seria um workflow de
trabalho em um projeto real.

Após ser configurado cada conta e realizado o fork do projeto. Precisamos que as pessoas do time tenham configurado o repositório que chamamos de **upstream**, que nada mais é uma nomenclatura que damos dentro do projeto. O upstream é o repositório da nossa aplicação. Configuramos o **origin** apontando para o fork que realizamos com o comando.
```git
  $ git remote set-url url-do-projeto-forkado
```
Essa configuração é setada quando temos **origin** apontando para outro repositório. Caso não esteja usamos apenas o comando:
```git
  $ git remote add origin url-do-projeto-forkado
```

Agora precisamos ter todas as informações do repositório principal sempre atualizadas usando o comando:

```git
  $ git fetch upstream
```

Esse comando ele vai baixar na memória do git todas as alterações realizadas dentro do repositório apontado para o **upstream**.

Baixada as atualizações podemos atualizar a nossa branch usando o comando **git merge**.
```git
  $ git merge upstream/master
```

Porém poderiamos usar o comando **git pull**, que faria as atualizações e o processo de junção ( merge ) automaticamente.
```git
  $ git pull upstream master
```

## Trabalhando em equipe part 3

Um tipo de workflow podemos usar uma branch chamada **dev** onde a mesma será a nossa **master** para desenvolvimento.

Obs: Sempre que formos trabalhar em um projeto, sempre precisamos criar uma branch **dev** baseada na branch de desenvolvimento do repositório principal. 
```git
  $ git checkout upstream/dev -b dev
```

Usando a branch que foi criada a cima podemos trabalhar nas novas funcionalidade do projeto. Sempre criando uma nova branch para uma nova funcionalidade baseando-se na branch **dev** que acabamos de criar.
```git
  $ git checkout -b content
```

Feitas as alterações precisamos commitar.
```git
  $ git add .
  $ git commit -m 'Adicionado conteúdo no index.html'
  $ git push origin content
```

Na hora de realizar o pull request, sempre vamos realizar para a branch de desenvolvimento. Que no exemlo é a nossa branch **dev** comprando com a branch criada **content**. Onde foi realizado as modificações.

Sempre é bom lembrar que podemos realizar CR **( coding review )** onde um membro da equipe irá avaliar e mostrar se algo está errado em nosso código.

Agora se tudo estiver ok, dentro do github podemos fazer o pull request e ainda no github podemos deletar a branch que realizamos tal funcionalidade.

E agora precisasmos atualizar a nossa branch de desenvolvimento. 

O restante da equipe irá atualizar da seguinte maneira:
```git
  $ git fetch upstream
  $ git merge upstream/dev
```

Já a pessoa responsável pelo repositório fará da seguinte maneira:
```git
  $ git fetch origin
  $ git merge origin/dev
```

## Trabalhando em equipe part 4

Precisamos sempre nos atentar que quando estamos trabalhando em uma nova funcionalidade em uma branch sempre precisamos verificar se a branch de desenvolvimento está atualizada. O que interessa para um colaborador é se algo foi alterado na branch de desenvolvimento. Caso nada disso tenha acontecido continuamos o trabalho e mandamos o pull request.

## Ferramentas de CI
### Alguns artigos sobre o assunto.
- [Diferenças entre Integração, deploy e entrega contínua - 4Linux](https://www.4linux.com.br/diferencas-entre-integracao-deploy-e-entrega-continua)

- [Ferramentas devops - OneBitCode](https://onebitcode.com/ferramentas-devops/)