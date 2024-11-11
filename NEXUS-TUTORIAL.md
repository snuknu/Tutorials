# Instalação, configuração e execução do Sonatype Nexus Repository.

## Download
Os downloads do Sonatype Nexus Repository estão disponíveis em: [https://help.sonatype.com/en/download.html](https://help.sonatype.com/en/download.html).

- Windows
[https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip).

- Unix
[https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz).

## Configuração
De acordo com a documentação oficial, o *Nexus* não deve ser instalado no diretório ``Arquivos de Programas``  para evitar problemas com a virtualização do registro de arquivos do Windows.

É recomendado usar eg, ``C:\nexus`` ou algo semelhante, garantindo que o usuário que executa o aplicativo tenha acesso total.

As configurações básicas de execução do Nexus, como o número de porta dentre outras, podem ser editadas no arquivo ``nexus-default.properties``.
- Diretório de configuração: ``..\nexus-3.74.0-05\etc``

## Execução
O executável ``nexus.exe`` do Nexus pode ser encontrado dentro do diretório bin e pode ser executado como aplicativo ou como serviço.
Diretório de execução: ``..\nexus-3.74.0-05\bin``

### Executar como *aplicativo*
- CMD: ``nexus.exe /run``
- SHELL: ``./nexus.exe /run``

Iniciar o gerenciador de repositório com o comando run o deixará em execução no shell atual e exibirá a saída do log. Você pode acessar o aplicativo assim que o log mostrar a mensagem "Started Sonatype Nexus". O aplicativo em execução pode ser parado usando CTRL+Co console apropriado.

### Executar como *serviço*
- ```/start```
- ```/stop```
- ```/restart```
- ```/force-reload```
- ```/status```

O executável ``nexus.exe`` pode ser usado para gerenciar o Nexus como um serviço com os comandos listados acima.

