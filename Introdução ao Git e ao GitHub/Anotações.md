# Anotações do Curso de Introdução ao Git e ao GitHub 

## O que é Git?
O Git é um sistema de controle de versão distribuído, foi desenvolvido por Linus Torvalds, e é muito utilizado no desenvolvimento de software.

## O que é GitHub?
GitHub é uma plataforma onde você pode armazenar seus projetos e criar um ambiente de colaboração, utilizando o Git como sistema de controle.

## Comandos Windows

>Comandos importantes do terminal Windows - Por ser o sistema operacional que eu utilizo, irei colocar inicialmente apenas os comandos dele. 

 - **dir**
   - Exibe uma lista de arquivos e subdiretórios de um diretório (diretórios = pastas).
   
 - **cd**
    - Comando usado para navegar entre diretórios - entrar em uma pasta.
    - Para ser levado para o diretório raiz (como o diretório `C:\` , por exemplo), basta digitar **`cd/`**
    - Para entrar em uma pasta, basta digitar o comando: **`cd NomeDaPasta`** - Por exemplo **`cd windows`**
    - Para voltar um nivel, ou seja, para a pasta anterior a que você está, usar o comando: **`cd . .`**
   
 - **cls**
    - Comando para limpar o terminal - Limpa a janela prompt de comando.
   
 - **mkdir**
    - Comando para criar um diretório ou subdiretório - Digite **`mkdir NomeDaPasta`** 
 
 - **del**
    - Comando utilizado para excluir arquivos

 - **rmdir**
    - Para excluir um diretório, use o comando **`rmdir NomeDaPasta /s /q`** -  sendo que **/s** é um parâmetro para excluir o diretório especificado e todos os seus subdiretórios, incluindo todos os arquivos, e o parâmetro **/q** especifica o modo silencioso, sendo assim ele não solicita confirmação ao excluir. O parâmetro **/q** só funcionará se **/s** também for especificado e se quiser _confirmar_ antes de excluir, basta digitar apenas o parâmetro **/s** sem o **/q**.

## Alguns Comandos do Git Bash 

- **ls**
    - Comando utilizado para listar arquivos e subdiretórios do diretório de trabalho atual.

- **ctrl + l**
    - Atalho para limpar a tela do terminal

## Conectando a Máquina ao GitHub

Na sua página do GitHub, clicando no canto superior direito, na setinha para baixo, irá abrir um menu, clicando em **"settings"** nesse menu você irá para outra página, no lado esquerdo terá uma lista, nessa lista, clicar em **"SSH and GPG keys"**.

Agora clique em **"new SSH keys"**, em **"Title"** dê um título, como por exemplo, _Minha Máquina Windows Principal_., deixe aí por enquanto, não feche a página.

Abra o git Bash na sua máquina, e vamos á alguns comandos: 

 - Vamos gerar o par de chaves (pública e privada): 
    - use o seguinte comando: 
    - `ssh-keygen -t ed25519 -c EscreverEmailUsadoNoGitHub` + `Enter`
    - irá pedir para adicionar uma senha (passphrase), então adicione

 - Vá até a pasta onde foi salvo esse SSH, por exemplo: 
    - `cd /c/Users/isis-oliver/.ssh/`
    -  Digite `ls` para listar os itens da pasta e ter certeza de que está na pasta correta. 

 - Após confirmar que está na pasta correta, usar o seguinte comando para visualizar o conteúdo das chaves:
    - `cat id_ed25519.pub`
    - No caso `.pub` é de chave pública, usaremos a chave pública para o GitHub.
    - Copiar a sequência de caracteres até o final, incluindo o email, que irá aparecer no terminal, voltar para o GitHub e naquela pagina que deixamos aberta anteriormente, colar essa chave, em **"key"**, e por fim clicar em **"Add SSH key"**. 

 - Após salvar a chave no GitHub, é preciso inicializar o SSH agent em sua máquina (O SSH agent salva você de precisar digitar sua senha toda vez que você quiser se conectar ao GitHub.) 
    - Digite: `eval $(ssh-agent -s)`
    - Isso irá gerar um **"agent pid nº"** sendo que esse número vária.  (PID = identificação de processo particular). 
 
 - Agora vamos "entregar" as chaves para esse "Agent"
    - Digite: `ssh-add id_ed25519` 
    - Agora estamos usando a **chave privada** (sem o `.pub`).
    - Digite a senha criada...

 >**Importante**: Quando futuramente for **clonar** um repositório, é necessário utilizar o código ssh do repositório e não o HTTPS, pois esse não irá funcionar.  

## Iniciando o Git e criando um Commit
> A partir daqui irei fazer uma sequência, como um passo a passo, todos os tópicos são sequenciais, e são um exemplo para facilitar o entendimento de como trabalhar no Git.

 - Abra o Git Bash (preferencialmente já na pasta que você irá salvar esse repositório - para isso basta criar a pasta (vamos criar nesse exemplo a pasta "livro de receitas", dentro da pasta, clicar com o botão direito do mouse e clicar em Git Bash)
    - Digite: `git init`
 
 - Quando for a primeira vez usando o Git na máquina, é necessário configurar da seguinte forma: 
    - `git config --global user.email "ColocarEmailGitHub@qui"`
    - `git config --global user.name UserNameDoGitHubAqui`

## Adicionando um Arquivo

 - Vamos criar um **README . md** - Para criar um Readme, a dica é usar Markdown, mesmo se estiver editando na sua máquina, existem programas de edição, como o "Typora" para facilitar isso, e poder ver na hora como ficará no final, o VS Code também abre arquivos do tipo `.md` e dá para editar nele mesmo esses arquivos. 
 
 - Pesquise externamente para saber mais sobre o MarkDown, use o site: https://www.markdownguide.org/basic-syntax/ para poder entender melhor como utilizá-lo.  
 
 - Crie o Readme direto na pasta, usando um bloco de Notas por exemplo, nomeie como "strogonoff.md", basta mudar a extensão de **.txt** para **.md** (MarkDown).
 
 - Voltando para o Git Bash digite: 
    - `git add *` 
    - O git add irá adicionar as alterações no diretório ativo à área de staging - como uma "sala de espera", as atualizações ainda não foram "salvas", mas estão prontas para o commit. 
    - Agora digite: `git commit -m "Escreva aqui algo que descreva esse commit como por exemplo - git inicial"`
    - Digite agora `git status` para verificar o status do seu commit

## Enviando para o GitHub

 - Para enviar do Git para o GitHub, primeiro crie o repositório no GitHub: 
    - Vá na área de repositórios do seu GitHub e crie um repositório clicando em **"New"**, de um nome ao repositório, uma descrição, se quiser, escolha se irá ser um repositório público ou privado, marque se quer que crie um README, depois de selecionar tudo o que precisar, clique em **"Create repository"**.
    - Agora copie o **link SSH** do repositório criado, e vamos seguir os passos para fazer o **push**, ou seja, enviar o que está na máquina para o GitHub, no próprio GitHub, na página atual, já temos o passo a passo, mas iremos fazer aqui também. 
    
 - No Git Bash vamos adicionar o link do repositório criado, digite: 
    - `git remote add origin LinkDoGitHub`
    - e em seguida:
    - `git push origin master`
    - Pronto, agora atualizando a página do GitHub, seu repositório estará lá, com os arquivos que estavam em sua máquina.

## Outros comandos do Git

 - Alterar nome de usuário e/ou email do Git:
    - `git config --global --unset user.email` - Para alterar o email.
    - `git config --global --unset user.name` - Para alterar a senha.
    - Agora basta seguir os passos já citados anteriormente para criar o Email e/ou a Senha. 

 - Para **"puxar"** o repositório do GitHub para a máquina, bastante usado quando há alterações nos arquivos que estão no GitHub diferentes do último push feito da máquina, quando há conflito:
    - `git pull origin master`

 - Para **clonar** um repositório do GitHub: 
    - No repositório que quer clonar, vá em "code" e copie o link do repositório.
    - No Git Bash Digitar: `git clone LinkCopiado`

### Fim!

