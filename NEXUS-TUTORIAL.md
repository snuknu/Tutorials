# Instalação, configuração e execução do Sonatype Nexus Repository.

## Download
Os downloads do Sonatype Nexus Repository estão disponíveis em: [https://help.sonatype.com/en/download.html](https://help.sonatype.com/en/download.html).

- Windows: [https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-java17-win64.zip).

- Unix: [https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz](https://download.sonatype.com/nexus/3/nexus-3.74.0-05-unix.tar.gz).

## Configuração
De acordo com a documentação oficial, o *Nexus* não deve ser instalado no diretório ``Arquivos de Programas``  para evitar problemas com a virtualização do registro de arquivos do Windows.

É recomendado usar eg, ``C:\nexus`` ou algo semelhante, garantindo que o usuário que executa o aplicativo tenha acesso total.

As configurações básicas de execução do Nexus, como o número de porta dentre outras, podem ser editadas no arquivo ``nexus-default.properties``.
- Diretório de configuração: ``..\nexus-3.74.0-05\etc``

Obs: Por padrão, o nexus vem configurado para executar na porta *8081*.

## Execução
O executável ``nexus.exe`` do Nexus pode ser encontrado dentro do diretório bin e pode ser executado como aplicativo ou como serviço.

Diretório de execução: ``..\nexus-3.74.0-05\bin``

### Executar como *aplicativo*
- CMD: ``nexus.exe /run``
- SHELL: ``./nexus.exe /run``

Iniciar o gerenciador de repositório com o comando run o deixará em execução no shell atual e exibirá a saída do log. Você pode acessar o aplicativo assim que o log mostrar a mensagem "Started Sonatype Nexus". O aplicativo em execução pode ser parado usando CTRL+Co console apropriado.

### Executar como *serviço*
- ```./nexus.exe /start```
- ```./nexus.exe /stop```
- ```./nexus.exe /restart```
- ```./nexus.exe /force-reload```
- ```./nexus.exe /status```

O executável ``nexus.exe`` pode ser usado para gerenciar o Nexus como um serviço com os comandos listados acima.

## Acesso
Uma vez instalado, o Nexus fica acessível localmente pela url http://localhost:8081.

![image](https://github.com/user-attachments/assets/98e7c9b1-987e-43d5-84eb-7489cd930c81)

A senha de usuario administrador padrão pode ser configurada no arquivo ``admin.password`` encontrado no ``<diretorio-de-insalacao>\sonatype-work\nexus3\admin.password``.

![image](https://github.com/user-attachments/assets/9720efc6-df5b-4425-81aa-3c1a6b3964aa)

Obs: Após o login, o Nexus exigirá que a senha de adminstrador seja modificada imediatamente.

## Repositórios
Após logar no Nexus é possível ver a lista de reposiórios criados por padrão como demonstrado abaixo.

![image](https://github.com/user-attachments/assets/28b0e993-715f-4491-a5f7-d3d33ffcab6a)

## Deploy no Nexus com Maven.
Existem várias formas de realizar o deploy de artefatos no Nexus, por meio da UI do nexus, ou por meio da execução dos goals do maven.

### Configurando o Maven para deploy no Nexus.
Para realizar o deploy de projetos maven em um repositório Nexus, os seguintes passos devem ser seguidos:
1. No arquivo ``settings.xml`` de sua configuração local do maven crie um novo ``profile`` com as configurações do repositório Nexus. 
```xml
</profiles>

  ...

  <profile>
    <id>identificador-do-perfil</id>
    <repositories>
      <repository>
        <id>identificador-do-repositorio</id>
        <name>Nome do Repositorio</name>
        <url>http://localhost:8081/repository/maven-public/</url>
        <releases><enabled>true</enabled><updatePolicy>always</updatePolicy></releases>
        <snapshots><enabled>true</enabled><updatePolicy>always</updatePolicy></snapshots>
      </repository>
    </repositories>
  </profile>

</profiles>
```

2. Ainda no arquivo ``settings.xml`` indique quais repositórios dos perfis configurados deseja utilizar.
```xml
<servers>

  ...

  <server>
    <id>identificador-do-repositorio</id>
    <username>nome-do-usuario</username>
    <password>senha-do-usuario</password>
  </server>

</servers>
```

3. Por fim, indique no mesmo arquivo, qual perfil de configuração você deseja utilizar. Essa configuração, se feita no ``settings.xml``, aplíca-se à todos os projetos que o apontam. Se preferir, você pode informar diretamente no ``pom.xml`` dos seus projetos, quais perfis deseja usar.
```xml
</settings>

  ...

  <activeProfiles>
    <activeProfile>identificador-do-repositorio</activeProfile>
  </activeProfiles>

</settings>
```

### Realizando o deploy de um projeto.
Um vez com o ``settings.xml`` do maven configurado, na raiz do seu projeto java, onde encontra-se o arquivo ``pom.xml``, execute o seguinte comando para fazer o upload para o Nexus:
```shell
mvn deploy -DaltDeploymentRepository=id-do-repositorio::default::http://localhost:8081/repository/maven-releases/
```
Você também pode executar esse goal a partir dos ciclos de vida configurados em sua IDE.

### Realizando o deploy de um artefato isolado.
É possivel fazer o upload de artefatos isolados no nexus a partir do maven, para isso basta executar o seguinte comando:
```shell
mvn deploy:deploy-file `
"-Durl=http://localhost:9091/repository/maven-releases/" `
"-Dfile=nome-do-arquivo.jar" `
"-DgeneratePom=true" `
"-DgroupId=com.exemplo" `
"-Dclassifier=classificacao-opcional" `
"-DartifactId=meu-artefato" `
"-Dpackaging=jar" `
"-Dversion=1.0" `
"-DrepositoryId=identificador-do-repositorio"
```
Obs: Use ``[espaço] + ` `` para comandos multi-linha no shell, e ``[espaço] + /`` para comandos multi-linha no linux.
