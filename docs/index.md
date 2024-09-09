# Executando o Tutorial do MDSPlus

O objetivo deste tutorial é conseguir executar os primeiros passos da ferramenta MDSPlus: *A Quick Tour over MDSplus Basic Concepts*. Para isso, será seguido o tutorial disponível no site oficial do [MDSPlus](https://www.mdsplus.org/index.php?title=Documentation:Tutorial:QuickOverview&open=1624466399993193889855&page=Tutorials%2FQuick+Tour).


## Pré Requisitos

Antes de começar o tutorial é muito importante cumprir com estes requisitos:

- Ambiente Linux:
    - [Ubuntu 24.04](https://ubuntu.com/download/desktop);
    - [Ubuntu 22.04](https://ubuntu.com/download/alternative-downloads#past-releases-and-other-flavours);
    - [Ubuntu 20.04](https://ubuntu.com/download/alternative-downloads#past-releases-and-other-flavours).
- Biblioteca `build-essential`.

```bash
sudo apt install build-essential
```
- Biblioteca `cURL`.

```bash
sudo apt install curl
```
## Preparando o Ambiente Local

Para começar a baixar as dependências do projeto é necessário entender um conceito: **Release Levels**

| Release Level| Descriçao                                                            	|
|--------|----------------------------------------------------------------------	|
| Alpha  | Atualiza a versão com toda atualização no repositório do GitHub   |
| Stable | Atuliza menos frequentmente. Novas features são muito bem testadas.|
 
Para fins de tutoriais será utilizado a versão **Alpha**.

### Importando a Signing Key

Para garantir a seguraça dos pacotes que serão baixados, é necessário armaenar a chave de assinatura do MDSPlus. Para isso, execute o comando abaixo:
```bash
curl -fsSL http://www.mdsplus.org/dist/mdsplus.gpg.key | sudo tee /usr/share/keyrings/mdsplus.asc > /dev/null
```

O objetivo deste comando é armazenar a chave de assinatura do MDSPlus no diretório `/usr/share/keyrings/` com o nome `mdsplus.asc` de forma silenciosa.

Para verificar se a chave foi armazenada corretamente, execute o comando abaixo:
```bash
ls /usr/share/keyrings/ | grep mdsplus.asc
```
Se o output for `mdsplus.asc`, a chave foi armazenada corretamente.

### Habilitando o Repositório

Para a próxima etapa será necessário habilitar o repositório do MDSPlus. Só que antes, é fundamental entender qual distribuição do linux está sendo usada. Para isso, execute o comando abaixo:

```bash
lsb_release -a
```

Por fim, basta executar o comando abaixo de acordo com a distribuição do linux:
#### Ubuntu 24.04
```bash
sudo sh -c "echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/mdsplus.asc] http://www.mdsplus.org/dist/Ubuntu24/repo MDSplus alpha' > /etc/apt/sources.list.d/mdsplus.list"
```
#### Ubuntu 22.04
```bash
sudo sh -c "echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/mdsplus.asc] http://www.mdsplus.org/dist/Ubuntu22/repo MDSplus alpha' > /etc/apt/sources.list.d/mdsplus.list"
```
#### Ubuntu 20.04
```bash
sudo sh -c "echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/mdsplus.asc] http://www.mdsplus.org/dist/Ubuntu20/repo MDSplus alpha' > /etc/apt/sources.list.d/mdsplus.list"
```

### Atualizando local cache

> **NOTA**: Esta etapa exige uma conexão com a internet estável e pode gastar um tempo considerável.

Com toda essa informação, é necessário atualizar o cache local para que o sistema operacional possa reconhecer as novas informações. Para isso, execute o comando abaixo:
```bash
sudo apt update && sudo apt upgrade -y
```
Este comando atualizará o cache local e instalará as atualizações disponíveis.


### Extra

Aqui estão alguns links com mais informações sobre o MDSPlus:

- Lista de pacotes de MDSplus: [MDSplus Packages](https://www.mdsplus.org/index.php/Latest_Ubuntu/Debian_Packages#MDSplus_Packaging)
- Lista de outros sistemas operacionais para adicioar o repostiório: [Lista](https://www.mdsplus.org/index.php/Latest_Ubuntu/Debian_Packages#Enabling_MDSplus_Debian_Repository)
- Nomenclatura dos pacotes: [Nomenclatura](https://www.mdsplus.org/index.php/Latest_Ubuntu/Debian_Packages#Performing_the_installation)

## Executando o Tutorial

Com o ambiente pronto será necssário baixar os pacotes para executar o tutorial. 

### Instalando o MDSPlus

Para instalar o MDSPlus, execute o comando abaixo:
```bash
sudo apt install mdsplus-alpha mdsplus-alpha-rfxdevices
```

### Atualizando o .bashrc

Para não ocorrer erros durante a execução do tutorial, é necessário atualizar o arquivo `.bashrc` com o caminho do MDSPlus. Para isso, execute os comandos abaixo:

#### Atualizando o .bashrc
```bash
echo '# Adding MDSplus path to any directory' >> ~/.bashrc
echo 'export PATH=$PATH:/usr/local/mdsplus/bin' >> ~/.bashrc
```

#### Verificando
```bash
cat ~/.bashrc | grep 'mdsplus'
```
A saída deve conter as duas linhas adicionadas pelo commando `echo`.

#### Atualizando o bash
```bash
source ~/.bashrc
```

#### Reiniciar o computaodr
Para garantir que todas as mudanças foram aplicadas corretamente, é necessário **reiniciar o computador**.
```bash
sudo reboot
```

### Baixando o Tutorial
Para baixar o tutorial, é recomendável criar uma pasta para armazenar o tutorial. Para isso, execute o comando abaixo:
```bash
mkdir ~/tutorial-mdsplus; cd ~/tutorial-mdsplus
```

Após isso, execute o comando abaixo para baixar o tutorial e entrar na pasta:
```bash
wget -O - https://github.com/MDSplus/MDSplusTutorial/archive/master.tar.gz | tar zxf -; cd MDSplusTutorial-master
```
Por fim, execute o tutorial:
```bash
./start_tutorial_1
```

## Conclusão
A partir de agora, basta seguir o passo a passo do próprio site por este [link](https://www.mdsplus.org/index.php?title=Documentation:Tutorial:QuickOverview&open=1624466399993193889855&page=Tutorials%2FQuick+Tour#Tutorial_1:_MDSPlus_Experiment_Model_and_pulse_file_and_their_interfaces).