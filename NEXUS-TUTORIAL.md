# Instalando e configurando o Nexus

## Download
Os downloads do Sonatype Nexus Repository estão disponíveis em: [https://help.sonatype.com/en/download.html](https://help.sonatype.com/en/download.html).

- Windows
[https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip).

- Unix
[https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz).

Eles contêm todos os recursos necessários para instalar e executar o Sonatype Nexus Repository.

O arquivo zip pode ser descompactado usando o utilitário de compactação do Windows ou um utilitário de terceiros, como o 7zip.

## Configuração
De acordo com a documentação oficial, o *Nexus* não deve ser instalado no diretório *Program Files*  para evitar problemas com a virtualização do registro de arquivos do Windows.

É recomendado usar eg, C:\nexus ou algo semelhante, garantindo que o usuário que executa o aplicativo tenha acesso total.

As configurações básicas de execução do Nexus, como o número de porta dentre outras, está disponivel em:
```\nexus-3.74.0-05\etc```.


