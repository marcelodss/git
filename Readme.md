# Git e Github
Arquivo da aula de Git e Github para iniciantes.

## Sobre o controle de versão
o que é "controle de versão" e por que você deveria se importar? O controle de versão é um sistema que registra alterações em um arquivo ou conjunto de arquivos ao longo do tempo, para que você possa recuperar versões específicas mais tarde.

é aqui que os Sistemas Distribuídos de Controle de Versão (DVCSs) entram em cena. Em um DVCS (como Git, Mercurial, Bazaar ou Darcs), os clientes não apenas conferem o último instantâneo dos arquivos; em vez disso, espelham completamente o repositório, incluindo seu histórico completo. Portanto, se algum servidor morrer, e esses sistemas estiverem colaborando por esse servidor, qualquer um dos repositórios do cliente poderá ser copiado para o servidor para restaurá-lo. Todo clone é realmente um backup completo de todos os dados.

[saiba mais em git-scm.com](https://git-scm.com/)

[![Git_ciclo.vida_.png](Git_ciclo.vida_.png)](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

## Básico do Git 

### Gravando alterações no repositório

* git init
* git status

**Ignorando arquivos**

Muitas vezes, você tem uma classe de arquivos que não deseja que o Git adicione automaticamente ou até mostre como não rastreado. Geralmente, são arquivos gerados automaticamente, como arquivos de log ou arquivos produzidos pelo seu sistema de construção. Nesses casos, você pode criar um padrão de listagem de arquivos para corresponder aos nomeados no arquivo `.gitignore`

* git diff - Para ver o que você alterou, mas ainda não foi preparado

Com `git diff --name-only` é possível ver apenas a lista de arquivos modificados.

* git add - Rastreando novos arquivos
* git commit - Confirmando suas alterações

com `git commit -am` é possível adicionar e commitar em uma única operação

* git rm - Removendo arquivos
* git mv file_from file_to - Movendo arquivos

[mais sobre alterações no repositório...](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

### Vendo o histórico de consolidação
Veja mais em

* git log

[mais sobre histórico de consolidação...](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

### Desfazendo coisas

* git commit --amend - Uma forma comum de desfazer as coisas no Git ocorre quando você confirma muito cedo e possivelmente esquece de adicionar alguns arquivos ou estraga sua mensagem de confirmação. Se você deseja refazer a confirmação, faça as alterações adicionais que você esqueceu, prepare-as e use o `commit` novamente usando a opção `--amend`
* git checkout - "_Desmodificando_" um arquivo modificado, mas não adicionado
* git reset HEAD - "_Desmodificando_" um arquivo modificado e adicionado (ver [--soft, --mixed e --hard](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified#_git_reset))

Após aplicar o `git reset HEAD`, utilize o `git checkout` 

[mais sobre desfazer as coisas...](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)

### Reverter alguns commits existentes

`git-revert`, reverte um commit sem apagá-lo do histórico de commits, diferentemente do `git checkout` e do  `git reset`  

[mais sobre revert...](https://git-scm.com/docs/git-revert)

## Trabalhando com controles remotos

### Criando um repositório no Github

[Gerando uma chave SSH do Github para o seu projeto](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

no terminal digite: 

>`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

>copie a chave contida no arquivo **__id_rsa_.pub_**

no Github:
>acesse o menu _**settings**_ e, na coluna de opções do seu perfil, clique em _**SSH and GPG Keys**_. Clique em **_New SSH Keys_**, informe o _**título**_ e cole a chave contida no arquivo _**id_rsa.pub**_

### Ligando o repositório local a um remoto (Github)

1. crie um repositório no Github, por exemplo **git_github_course.git**;
2. envie um repositório existente a partir da linha de comando:

`git remote add origin git@github.com:marcelodss/git_github_course.git`

digite `git remote` para que o git mostre se já existe um repositório chamado _**origin**_ preparado para ser enviado ao github. `git remote -v`, para mais informações ou se você quiser ver mais informações sobre um controle remoto específico, use o comando `git remote show <remote>`

`git push -u origin master`

o `-u` é utilizado no primeiro push para *trackear* para onde vai (*origin*) e de onde vem (*master*). Nos seguintes basta utilizar `push`

> Sempre que um repositório é criado, o Github sugere que você "_Comece criando um novo arquivo ou carregando um arquivo existente . Recomendamos que cada repositório inclua um README , LICENSE e .gitignore._";

> ... Ou crie um novo repositório na linha de comando
```
echo "# django_ud002_course" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:marcelodss/django_ud002_course.git
git push -u origin main
```

> ... Ou envie um repositório existente a partir da linha de comando
```
git remote add origin git@github.com:marcelodss/django_ud002_course.git
git branch -M main
git push -u origin main
```



 


### Enviando mudanças para um repositório remoto
`git push origin master`

### Clonando repositórios remotos

`git clone git@github.com:marcelodss/git_github_course.git nomeRepositorioLocal`

sendo _nomeRepositorioLocal_, por exemplo, *git_github_course_clone*

### Usando Fork (Bifurcação)

veja: [contribuindo para um projeto](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)

[mais sobre trabalhar com controles remotos...](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)

## Ramificação (Branch)

uma ramificação no Git é simplesmente um ponteiro móvel leve para um desses commits. O nome do ramo padrão no Git é *master*. Quando você começa a fazer confirmações, você recebe um ramo master que aponta para o último commit que você fez. Toda vez que você faz um commit, o ponteiro master do ramo avança automaticamente.

o ramo *"master"* no Git não é um ramo especial. É exatamente como qualquer outro ramo. A única razão pela qual quase todo repositório tem um é que o comando `git init` o cria por padrão e a maioria das pessoas não se preocupa em alterá-lo.

o que acontece quando você cria uma nova ramificação? Isso cria um novo ponteiro para você se movimentar. Digamos que você queira criar um novo ramo chamado *testing*. Você faz isso com o comando `git branch`: `$ git branch testing`

isso cria um novo ponteiro para o mesmo commit em que você está atualmente.

por que usar?

* poder usar sem alterar o local principal ("*master*");
* facilmente "desligável", criando-os e apagando-os;
* permite várias pessoas trabalhando em diversos branches;
* evita conflitos em casos de muitos commits simultâneos;
* permite mesclar branchs "secundários" com o principal.

[veja mais sobre branchs...](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)

criando um branch: 
`git branch testing` ou 
`git checkout -b testing` para criar e acessar no mesmo comando

para visualizar o branch ativo, digite: `git branch`

movendo-se entre branchs: `git checkout <nomeDoBranch>`

deletando branchs locais: `git branch -D <nomeDoBranch>`

deletando branchs remotos: `git push origin :<nomeDoBranch>`

### Unindo branchs

#### Merge

supondo que você está em um branch chamado master e quiser mesclar outro branch chamado teste, digite: `git merge teste`

analise o resultado com `git log --graph`

prós:

* operação não destrutiva - não destrõe commits, pelo contrário junta todos em um novo commit

contras:

* necessidade de commits extras;
* histórico poluído

[mais sobre merge...](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

### Rebase

prós:

* evita commits extras;
* mantém um histórico linear

contras:

* perda da ordem cronológica

[mais sobre rebase...](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)

## Extras

### Esconder e limpar

para ocultar arquivos mofificados ou estagiados (add) e impedir um commit:

* `git stash` oculta alterações
* `git stash list` exibe todos os stashs
* para retorná-los aplicando as mudanças: `git stash apply`
* para limpar todos os stashs: `git stash clear`

[mais sobre stashs...](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)

### Aliases do Git

o Git não infere automaticamente seu comando se você o digitar parcialmente. Se você não quiser digitar o texto inteiro de cada um dos comandos do Git, poderá configurar facilmente um alias para cada comando usando git config. Aqui estão alguns exemplos que você pode querer configurar:

`git config --global alias.co checkout`
`git config --global alias.br branch`
`git config --global alias.ci commit`
`git config --global alias.st status`

[mais...](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)

### Marcação (Tag)
como a maioria dos VCSs, o Git tem a capacidade de marcar pontos específicos no histórico de um repositório como sendo importantes. Normalmente, as pessoas usar essa funcionalidade para pontos de liberação de marca ( *v1.0*, *v2.0* e assim por diante). Nesta seção, você aprenderá como listar tags existentes, como criar e excluir tags e quais são os diferentes tipos de tags.

listando suas tags: `git tag`

#### Criando Tags
o Git suporta dois tipos de tags: **leve** e **anotado** .

uma tag **leve** é ​​muito parecida com uma ramificação que não muda - é apenas um ponteiro para um commit específico.

tags **anotadas**, no entanto, são armazenadas como objetos completos no banco de dados Git. Eles estão somados; conter o nome, o email e a data do marcador; ter uma mensagem de marcação; e pode ser assinado e verificado com o GNU Privacy Guard (GPG). Geralmente, é recomendável que você crie tags anotadas para ter todas essas informações; mas se você deseja uma tag temporária ou, por algum motivo, não deseja manter as outras informações, também estão disponíveis tags leves. **Exemplo:** `git tag -a 1.0.0 -m "Readme Finalizado"`.

* subir as tags para o remoto: `git push origin master --tags`
* excluir a tag do git local: `git tag -d 1.0.0`
* excluir a tag do git remoto: `git push origin :1.0.0`, isso porque as **_tags remotas não são apagadas ao apagar as tags locais_**

[mais sobre tags...](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

$\Overrightarrow{AB}$
