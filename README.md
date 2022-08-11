# Docker React Native 
[See in Português](README.md)

Rode qualquer projeto com react/react native ou Expo sem precisar instalar nenhuma integrated development environment (IDE) na sua máquina, simplesmente usando uma imagem do Docker. A única coisa que você precisará instalar é o Docker na sua máquina, disponível para **Windows, Linux, Mac**. Caso nunca tenha instalado Docker, veja aqui como instalar [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/). 

Caso queira saber um pouco mais antes de começar você pode acessar esse link [https://github.com/lexvieira/Docker-Init-Nodejs-React-React-Native-SQLServer](https://github.com/lexvieira/Docker-Init-Nodejs-React-React-Native-SQLServer)

## Mãos na Massa

Essa imagem está disponível no link abaixo, siga lendo para descobrir como utilizá-la.

[https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01](https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01)

Ou apenas faça um Pull 👇 (baixar) a imagem.

```docker pull lexvieira/docker_react_native_deploy_01:v01```

## Dockerfile

É possível também você criar sua própria imagem a partir do *Dockerfile* disponível neste repositório.

```docker build -t drn:v01 .```

* *docker build -t drn:v01 .* -> Docker executável no Windows ou Linux, onde o parametro *Build ⚙️🛠️* criará uma imagem com os seguintes parametros  

* *build -t* -> *-t* É o parâmetro para nome da *tag* ou nome da imagem que você está criado

* *drn:v01* -> Nesse caso o nome da imagem será: **drn:v01** (**drn** é uma abreviação para Docker React Native)

* *.* -> **.** significa que você está rodando o comando dentro da pasta onde está o **Dockerfile**

## Publique a sua própria imagem e deixe disponível online pública ou privada (caso queira)

1) - Crie o seu login no site: [https://hub.docker.com/](https://hub.docker.com/)

2) - Logue com sua conta na linha de comando do docker no Linux/Mac ou através da aplicação no Windows 

```
 docker login  
```

Insira o usuário e senha quando solicitado

3) Depois que você já fez o **Pull 👇** da imagem ou deu um **Build ⚙️🛠️**, faça um **Push 👆** da imagem para o reposítorio online

Exemplo no site [https://docs.docker.com/engine/reference/commandline/push/](https://docs.docker.com/engine/reference/commandline/push/) - Não se preocupem, vou mostrar de mode simples

```
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
```

Imagem que subi no [https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01](https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01)

```
docker tag drn:v01 lexvieira/docker_react_native_deploy_01:v01
docker push lexvieira/docker_react_native_deploy_01:v01
```

* *docker tag drn:v01* > O parametro **tag** é para identificar o nome da imagem que você criou ou baixou (Pull 👇)
* *lexvieira/docker_react_native_deploy_01:v01* > é para idenficar aonde você irá fazer um Push 👆 (Enviar) sua imagem 

## Commandos básicos para rodar seus projetos em React / ou React Native

Nesse link você tem alguns commandos básicos para conseguir rodar suas imagens de uma forma mais prática usando **Alias** por exemplo [https://github.com/lexvieira/Docker-Init-Nodejs-React-React-Native-SQLServer#usando-alias-veja-mais-em-github-semana-omnistack-10-alias-bonushttpsgithubcomlexvieirasemana-omnistack-10treerun_on_dockeralias-bonus-target_blank](Docker Alias)


* Nesse caso estou passando o comando que utilizo na minha máquina para docker meus projetos rodando um Linux Ubuntu.

### Usando um Alias (atalho), para diminuir o tamanho dos coomandos 

**Alias** é apenas um atalho que criamos para fazer com que digitemos menos comandos e nossa vida fique mais fácil. 

Abaixo 👇 existe um **Alias** que você tanto pode copiar e colar na linha de comando do terminal ou adicionar no seu arquivo de configuração do terminal **.bashrc | .zshrc** veja mais no link acima 👆.

**Comandos básico**
```
alias drn='docker run --network host -ti -v "$(pwd)":/opt/ui -p 8081:3000 --privileged -v /dev/bus/usb:/dev/bus/usb drn:v01' 
```

**Comando Avançado**, 
1) Para o Docker se já estiver rodando
2) Identifica o ip da sua máquina para você rodar no seu navegador (Browser) ou no seu App React Native.
3) Roda a Imagem do React por último.
```
alias drn='$([[ $(docker container ls | grep drn:v01 | cut -d" " -f 1) != "" ]] && $(docker stop $(docker container ls | grep drn:v01 | cut -d" " -f 1)) || echo "") && ifconfig | grep inet && docker run --network host -ti -v "$(pwd)":/opt/ui -p 8081:3000 --privileged -v /dev/bus/usb:/dev/bus/usb drn:v01' 
```

Não importa o atalho que você criou o resultado será o mesmo, a única coisa que você terá que digitar depois na linha de comando é **drn** seguido do comando que você quer executar.


### Na Prática

Primeiro crie uma **pasta/folder** para o projeto com react Native, por exemplo `mkdir MyApp` e depois rode o comando abaixo
```
drn npx react-native init MyApp --template react-native-template-typescript\
```

Primeira vez rodando um projeto do react-native no seu smartphone Android, para **Apple** é necessário um Mac Book para rodar o projeto.
No Android você deve  habilitar o **mode de desenvolvedor** (diferentes modelos diferentes modos de acessar), connectar o cabo **USB**, selectionar **File Transfer (Transferência de Arquivos)**, após rodar o comando abaixo 👇 fique atento para aceitar a **chave de segurança** quando solicitado, caso o contrário a compilação dará erro. Voalá, seu app está rodando no seu celular. Pode desconectar o **USB** e dá próxima vez é só rodar o próximo comando.
```
drn react-native run-android 
```

Última parte, executa o seu projeto do react native para rodar através do IP da sua máquina. Caso não saiba o IP, digite `ifconfig` no **Linux**, no **Windows** `ipconfig`, e no **Mac** não tenho nem ideia (A gente também não sabe de tudo 😁). Aparentemente é ifconfig também.
Localize o No seu App rodando no Smartphone Android, *sacuda o seu celular da direita para a esquerda*, em seguida, selecione *Settings ⚙️🛠️* e depois *Debug Server host & port for device*, digite o ip que recebeu após digitar *ifconfig*. Volte e clique em *Reload* você notará que tanto no celular quanto no terminal da sua máquina você verá um percentual de download. E pronto, sua aplicação está no Ar.
```
drn react-native start
```

* Para rodar o **Expo** existem alguns outros comandos para ser adicionado, enviarei na atualização 😉

O **Alias** 


## Atualizações vindo ;)

Chegando em breve mais, imagens e mais exemplos.

##That's all folks