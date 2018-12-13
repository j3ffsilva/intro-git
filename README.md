## Guia Git e Github

###Sobre o Git e o Github
#### O que é o Git?
Git é um sistema de controle de versões.

#### O que é um sistema de controle de versões (SCV)?

O que é "controle de versões" e por que isso é importante? Controle de versão é um sistema que grava alterações ao longo do tempo em arquivos de forma que se possa recuperar essas versões posteriormente.

Um SCV permite que:
- reverta arquivos a estados anteriores
- reverta projetos completos a estados anteriores
- compara alterações ao longo do tempo
- vê quem introduziu uma issue e quando
- recupera arquivos danificados ou perdidos

E se o Git não estiver em uso e um bug for descoberto?
- Não é possível saber quando o bug foi introduzido e que código foi o responsável
- Não é possível reiniciar o código a uma versão anterior
- Não é possível saber quem introduziu o bug
- Não é possível ter diferentes versões do código (ex:, produção versus não-produção)


#### O que é o GitHub?
Embora o Git possa ser usado para rastrear seus próprios arquivos, o GitHub é o que permite que times grandes possa colaborar em um único projeto. GitHub é um repositório Git na web. Armazena e rastreia arquivos em seus projetos.

O GitHub fornece:
- controle de acesso (quem pode ver o que)
- wikis/documentação/READMEs para projetos
- Gerenciamento de tarefas
- Rastreamento de bugs
- Requisições de funcionalidades

Essas características fazem do GitHub excelente para colaboração. As comunidades de software aberto (SL) amam usar o GitHub. Assim como times de hackathons e recrutadores técnicos.

### Começando com o Git

| Sistema operacional | Download/Instalação                                                                                                                                                                                                                                                                                                            |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OS X             | Download em [http://git-scm.com/download/mac](http://git-scm.com/download/mac)                                                                                                                                                                                                                                            |
| Windows          | Download em [http://git-scm.com/download/win](http://git-scm.com/download/win) -

Dois programas irão instalar: Git Bash e Git GUI. Use o Git Bash! Embora uma GUI pode fazer quase todas as funções que o BASH, é ótimo ganhar familiaridade ao trabalhar da linha de comando. Você pode usar comandos Unix/Linux dentro do Bash. |
| Linux            | usuários Ubuntu, Debian, e Mint podem rodar de seus terminais:  `sudo apt-get install git`. Usuários Fedora: `sudo yum install git`                                                                                                                                                                            |

#### Configurações (Globais)
Existem algumas configurações (tais como suas informações, e que editor você usa, aliases etc) Git tem dois arquivos, `~/.gitconfig` e `~/.gitignore` localizada em seu diretório home. `~/.gitconfig` stores settings that you can configure. '~/.gitignore` stores information about what files git should not keep track of. (Maybe you don't want git to track any files with the extension ".catvideo").  You can also make repo-specific .gitignore files (for example, if you don't want to track .class files in a repo).

Você pode configurar seu nome e email (anexada aos commits que você escreve):

 `$ git config --global user.name "John Doe"`
o git usa:
  `$ git config --global user.email johndoe@example.com`

  Se você não está familiarizado com vim, altere o editor-padrão que o Git utiliza:

  - Mac: `git config --global core.editor open`
  - Windows: `git config --global core.editor notepad`
  - Linux: `git config --global core.editor nano`

  Se você quer fazer a saída do git agradável e colorida, aqui vai uma maneira de fazer:
  Abra seu git config:

  - Mac: `open ~/.gitconfig`
  - Windows: `start ~/.gitconfig`
  - Linux: `nano ~/.gitconfig`
  - Adicione as seguintes linhas:

```
[color]
	ui = true
[color "branch"]
	current = yellow reverse
	local = yellow
	remote = green
[color "diff"]
	meta = yellow bold
	frag = magenta bold
	old = red
	new = green
```

Quanto mais se utiliza o git mais interessante fica utilizar comandos alias (geralmente ao torná-los mais curtos para que se digite menos!) Para mais exemplos de maneiras de customizar o git, você pode olhar para um exemplo de um arquivo de configuração `git_recursos`.


### O Básico do Git
#### Comandos Unix Básicos
É sempre útil saber alguns comandos Unix básicos para quem utiliza o terminal. Digite o comando, e então pressione enter.

-`pwd` informa o diretório (pasta) corrente
-`ls` mostra os arquivos no diretório corrente
-`cd [NOME_DA_PASTA]` faz com que o diretório corrente seja alterado para NOME_DA_PASTA
-`cd ..` faz com que o diretório corrente seja alterado para o diretório pai (a pasta em que o diretório *corrente* está dentro)

No Windows, pode-se clicar com o botão direito do mouse na pasta que se deseja entrar e clicar em `git Bash`. Esta ação irá abrir o git BASH com o diretório corrente apontado para a pasta que se quer. No Macs, pode-se digitar `cd ` e então arrastar a pasta que se quer entrar e a janela do terminal irá preencher com o caminho da pasta.

Se achar esses passos confusos, procure ajuda. A linha de comando pode ser assustadora para os novatos, mas fica mais fácil com a prática.

#### Obtendo um repositório Git

  - **Clonando um repositório existente**
    - A maior parte das vezes neste clube e por aí você irá o git para trabalhar em projetos existentes no GitHub. Use o seguinte comando para clonar o projeto em seu computador.

    `git clone https://github.com/pucsp-open/intro-git.git`

    -Esta ação copia (clona) um repositório git para a máquina local, para uma pasta com o mesmo nome do repositório
    -`cd [NOME_DO_REPOSITÓRIO]` para mudar o diretório corrente para uma pasta recém criada

  - **Iniciando o repositório em um diretório existente**
    - Se você já possui um diretório em seu computador que você deseja rastrear com o git, use o comando `git init` para começar a rastrear aquela pasta com o git.

  - O diretório `.git` permite que comandos git possam ser reconhecidos dentro do diretório pai (onde você digitou o `git init`)
    Se você não estiver dentro de um repositório git, o sistema operacional acusa erros quando se tenta digitar comandos git.
    ```
    $ cd ~
    $ git status
    fatal: Not a git repository (or any of the parent directories): .git
    ``

#### Registrar alterações no repositório

Você diz ao git o que registrar (o Git se importa se você fez alterações ou não?), e então o git irá te mostrar se quaisquer um dos arquivos **rastreados** foram **modificados**, se eles estão **staged** para commit, e em que **branch** você está. O seguinte comando fornece todas as informações:

`git status`

Se você digitar este comando em uma pasta recém clonada (ou uma recém inicializada), o sistema irá mostrar as informações a seguir (porque nenhuma mudança foi feita ainda):

```
$ git status
On branch master

Initial commit

nothing to commit
```

A primeira linha significa que você está no **master branch** (uma tradução em Português é **ramo mestre**) (que é o padrão). A segunda linha significa que não se fez commits de alterações ainda, e a terceira linha significa que você ainda nem fez mudanças aos arquivos nem adicionou arquivos ainda.

So you want to start working on the files in your newly git-tracked folder. To do so, follow these steps:

1. Create a new "branch" and "check out" that branch for your work.

2. Make changes to the file(s) in your directory.

3. "add" those files so git tracks the changes.

4. Commit the changes you've made.

Detailed explanation of each step is below.

#####1. Create a new branch
Git and github keep track of your work with branches. The topic is covered further in the "Other Topics" section below. For now, just know that before making changes on any of the files, you should create a new branch so you are *not* working directly under the branch "master" or "develop."

Create a new branch with:

`git branch [branch name]`

Usually you will name your branch something like "feature/something" or "bug-fix/something" to clearly identify what you are working on.

Checkout or "switch" to that newly created branch with:

`git checkout [branch name]`

To check that you are on the branch you want to be, run `git status` and the first line will tell you what branch you have checked out.

#####2. Make Changes
If you create a new text file named "hello.txt", and then run `git status`, you'll see the following:

```
$ git status
On branch master

Initial commit

Untracked files:
	hello.txt

nothing added to commit but untracked files present
```

hello.txt is **untracked** by git. The last line means that git does not see any *tracked* changes, but it reminds you that there is an *untracked* file (hello.txt).

#####3. Add files
You want to "add" hello.txt, so that it is **tracked** by git. Use:

`git add hello.txt`

If you want to add multiple files, just enter each filename separated by a space like so

`git add file1 file2 file3 etc.`

If you want to add *all* the files in the working directory, use the following:

`git add -A`

You should see the following:

```
$ git add hello.txt
On branch master

Initial commit

Changes to be committed:
	new file:   hello.txt
```

Now git knows there aren't any untracked files, and instead considers hello.txt as a **tracked** file, waiting to be committed. You can go back and make more changes to hello.txt or any other file. Just make sure to re-add hello.txt and the other files you have modified.

#####4. Commit Changes
Once you have made all the changes you want and added those files, you are ready to "commit" your changes. Use the following command:

`git commit -m "message explaining the changes"`

If all goes well, something like this should show up:

```
$ git commit -m "Created hello.txt which contains a greeting"
[master (root-commit) f6f7407] Created hello.txt which contains a greeting
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```

Now git is tracking a file called hello.txt, and you have one commit with your initial changes to it.

Congrats, you've made you're first commit. You probably want to publish those changes to Github, which is covered below.

##### Recap

If you type `git status` again, you'll notice we're kind of back to where we started.  That's because we made and now git is tracking the changes between your most recent commit and now.  This is the typical flow of using git:

 1.  `git branch [branch name]` and `git checkout [branch name]"`

 2.  Create file/make changes to file(s)

 3.  `git add <file>`

 4.  `git commit -m "changes to <file(s)>"`

 5.  Publish those changes (covered below)


#### Looking at Changes, Commits, and Undoing Things

If you want to see the commits you've made so far:

```
 $ git log
 Fri Jan 23 17:38:42 2015 -0800 025aabe (HEAD, master) Changed text of hello.txt  [Melanie Cebula]
 Fri Jan 23 17:35:13 2015 -0800 f6f7407 Created hello.txt which contains a greeting  [Melanie Cebula]
```

If you haven't yet committed your changes, you can look at *what* you changed by performing `$ git diff`.  Go ahead and make some more changes to hello.txt.  In my case, my evil twin sister stole my laptop and furiously typed some things.  I want to know what she changed!!!

```
 $ git diff
 diff --git i/hello.txt w/hello.txt
 index 092bfb9..da5d515 100644
 --- i/hello.txt
 +++ w/hello.txt
 @@ -1 +1,3 @@
 -yo
 +Hahahahahaha I'm Melanie's evil twin Emily and I changed the text of this file!
 +Deal with it!!!!
 +-Emily
```
She deleted you (in red) and added a message (in green).  How do we undo this?
Since this is unstaged, we basically need to **un-modify the modified changes**.

Here's on way to do that (use with caution):
`$ git checkout -- hello.txt`

However, if you want to **undo something you've already committed (say your last commit)**:

Undo commit with `git reset` (use with caution):
`$ git reset --soft HEAD~1 `

Note: You can recover from undoing things (see [http://stackoverflow.com/questions/2510276/undoing-git-reset](http://stackoverflow.com/questions/2510276/undoing-git-reset)) but you should be careful in general, because it can get complicated.

Okay cool, so git can be used to keep track of modifications you make to the files that it tracks.

#### Pushing/Pulling Changes

![](https://illustrated-git.readthedocs.org/en/latest/_images/git-flows.svg)

So far, you've only dealt with a local git repo.  

But nowadays, most people use Github to have a **remote** repository (the hosted on [Github](https://github.com) itself) in addition to their local repository.  

This especially makes sense if you're working in teams.  Each teammate has their own **local** git repo, but they all push to the same project repo on Github.

Lets go over the the technical terms so we all know what wer're talking about.

**Pushing** is the action of sending code to a remote repository ([github](https://github.com) in our case). Think of pushing as you shipping your packages ("commits") to their destination ("remote repository") in the mail ("internet").

If you push commits to a remote respository, the commits still stay on your computer, but the remote repository gets update with the chages you've made. Here's an example push to a remote repository:

```
$ git push origin feature/mongoose-orm

Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 1.36 KiB | 0 bytes/s, done.
Total 13 (delta 7), reused 0 (delta 0)
To git@github.com:dvcoders/dvcoders-backend.git
   905dd73..39b510b  feature/mongoose-orm -> feature/mongoose-orm
```

However, if the code on your computer is **behind** the code on the remote, you'll be rejected, and told that you need to "catch up" with `git pull`

```
$ git push origin master
To https://github.com/[username]/[name-of-project.git]
! [rejected]		master -> master (non-fast-forward)
```

**Pulling** is the opposite of pushing, instead of sending commits to the remote repository, we're **getting** code from the remote repository. We want to do this when other people working on the project have update our remote repository but we're not caught up yet. Think of pulling as getting a delivery of several packages ("commits") to your house ("local repository")

```
$ git pull

remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:dvcoders/intro-git
   eaf2834..2e5a31a  master     -> origin/master
Updating eaf2834..2e5a31a
Fast-forward
 README.md | 34 +++++++++++++++++-----------------
 1 file changed, 17 insertions(+), 17 deletions(-)
```

However, sometimes something called a **merge conflix** can happen when trying to pull from a repository. A merge conflict happens when the code on your computer and the code on the remote repository have both been changd and git doesn't know which one you want to use (overwrite your local work or ignore the changes from the remote?)

As a result, we sometimes get this kind of error:

```
$ git pull
Auto-merging introductions.py
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Git is telling us that there are multiple changes to the README.md file in this example. So in order to fix this issue, open the file listed in the "merge conflixt in ___________" and you should see **conflict markers**.

```
<<<<<<< HEAD
### Learning Git
git is awesome
=======
### Learning Git
git sucks
>>>>>>> [commit hash shows up here - 77976da35a...: README.md]
```

Git is telling us that these lines of code are different between our local computer and the remote we just tried to pull. In order to resolve this we ned to make a choice between which code we want to keep.

Everything from `<<<<<<< HEAD` to `=======` is the code we have on our local machine.

Everything from `=======` to `>>>>>>> [commit hash...]` is the code from our remote repo.

Simply delete the half you don't want and clean up all `=======` or `<<<<<<<` markings.

Finally, to resolve this merge conflict we simple add and commit our changes!

```
$ git add -A
$ git commit -m "Resolved merge conflict"
# Optionally push the commit when appropriate
```

### Other Topics:

#### Git Branching Summarized
![](http://4.bp.blogspot.com/-t4yLz-et74A/UBIES98QPmI/AAAAAAAADGY/S5lwne9xpcM/s1600/releaseFlow.png)
([Image]( http://nxvl.blogspot.com/2012/07/a-continous-delivery-git-branching-model.html))

- A branch in Git is simply a lightweight movable pointer to your latest commit
- The default branch name in Git is master
- Each branch points to the latest commit made on that branch (each time you commit, it moves forward automatically)

**Create** a new branch <branchName> with `$ git branch <branchName>`
- This creates a new pointer at the same commit you’re currently on.

**Switch** to branch <branchName> with `$ git checkout <branchName>`

**IMPORTANT: Switching branches CHANGES files in your working directory**:
- If you switch to an older branch, your working directory will be reverted to look like it did the last time you committed on that branch
- If Git cannot do this cleanly, it will not let you switch at all.

**Update** a branch: All you have to do is `checkout` the branch you wish to merge into and then use the `git merge` command:
```
$ git checkout master
Switched to branch 'master'
$ git merge hot-fix
```
This code switches to **branch** master, and then merges the changes from **branch** hot-fix into master.  Now master is up-to-date! You may need to correct a merge-conflict at this point, which is covered in the Pushing/Pulling section above.

**List** your local branches with `git branch`. An asterisk indicates the branch you are currently on. `git branch -a` will list all the local branches, and all the *remote* branches also. Remote branches are discussed below.

**Note:** When making changes on your projects, don't work under the branch "master" or "develop." It's better to work on another branch, which can be merged with the "develop" branch later on.

#### Remote Branches:
**Remote branches** are references (pointers) to the state of branches in your **remote** repositories.
- They take the form `(remote)/(branch)`
- **Add** a remote: `$ git remote add REMOTE-NAME REMOTE-LOCATION`
For example:  We add a **remote** called `origin` from the git repo `git://git.whatever.com`

`$ git remote add origin git://git.whatever.com`

**Note:** When you `git clone` a repository from github, git will automatically add the remote branches.

- **List** remotes: `$ git remote -v`
- **Push** to a remote:  `$ git push (remote) (branch)`

A remote is simply a repository (folder being tracked by git) which lives somewhere other than you computer - *github for example*!

For example, if you are working on a branch called "feature/css-styling" and you want to push to github:

`$ git push origin feature/css-styling`

This tells git to push the commit(s) from the feature/css-styling branch to the "remote" url called "origin".

Git branching and remotes are confusing!  The main thing to remember is that **when you switch branches, your code changes**! Use `$ git log` liberally if you forget which changes are on which branches.

### Best Practices:

- **USE GITHUB FLOW**: [Github Flow - Branch, Commit, PR, Discuss, Merge](https://guides.github.com/introduction/flow/)

- Write a descriptive commit message (50 characters or less)
- Break up commits into small changes.
- Keep master clean. Work on your own local branch and merge changes into master when you know they work.
- **Add your SSH key to github so you don't have to type in your user/password every time:** 			   
[https://help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys/)
- git checkout [filename] to restore it to the state of the latest commit.
- git stash if you want to (temporarily) undo changes (git stash apply to re-apply it)
- **use a .gitignore file in each repo (ignore node_modules in javascript, *.class files in java, *pyc for python files, etc)**

### Learning Resources
- [Got 15 Minutes? Learn Git](https://try.github.io/levels/1/challenges/1) - Awesome interactive command line which guides you through the commands we covered above.
- [Git Cheatsheat](./git-resources/github-git-cheat-sheet.pdf) - basically summarizes this entire guide in two pages for quick reference.
- Again, [use Github Flow](https://guides.github.com/introduction/flow/), it's "kind of" important.
- [git-cheat CLI (Command Line Interface)](https://github.com/0xAX/git-cheat) - nifty command line tool where you can type `git-cheat remote` and it will give great summaries of what each command does.
- Have any other good learning resources? *Make a pull request on this repo*!

### Parting Words:
Using Git takes practice!  Make sure you have the add-commit-(pull)-push workflow down and you're halfway there!
