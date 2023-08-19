# Dockerfile para criar uma imagem python com alpine e pip

Este Dockerfile cria uma container com o shell bash como padrão, junto com uma versão do python e o pip instalado usando pyenv.

## Como usar

### Criando a imagem

Para construir a imagem Docker, certifique-se de estar no diretório onde o Dockerfile está localizado e execute o seguinte comando:

```bash
docker image build -t nome_da_imagem:latest .
```

### Executando o container

Para executar o container, execute o seguinte comando:

```bash
docker container run -ti --name nome_do_container --rm nome_da_imagem:latest
```

### Personalizando a imagen com argumentos

Para personalizar o container, você pode passar argumentos para o comando `docker run`. Por exemplo, para alterar o nome do usuário padrão, execute o seguinte comando:

USER: Define o nome do usuário dentro do container. Default do nome e `app`.

```bash
docker image build -t nome_da_imagem:latest --build-arg USER=nome_do_usuario .
```

PY_VERSION: Define a versão do python a ser instalada. Default da versão e `3.11.4`.

```bash
docker image build -t nome_da_imagem:latest --build-arg PY_VERSION=3.8.0 .
```

Lembre-se de que você pode ajustar os valores de `USER` e `PY_VERSION` conforme suas necessidades.

```bash
docker image build -t nome_da_imagem:latest --build-arg USER=nome_do_usuario --build-arg PY_VERSION=3.8.0 .
```

### Acessando o container

Para acessar o container, execute o seguinte comando:

```bash
docker container exec -ti nome_do_container bash
```

### Removendo o container

Para remover o container, execute o seguinte comando:

```bash
docker container rm nome_do_container
```

### Removendo a imagem

Para remover a imagem, execute o seguinte comando:

```bash
docker image rm nome_da_imagem:latest
```

### Removendo todas as imagens

Para remover todas as imagens, execute o seguinte comando:

```bash
docker image rm $(docker image ls -a -q)
```

### Removendo todos os containers

Para remover todos os containers, execute o seguinte comando:

```bash
docker container rm $(docker container ls -a -q)
```

## Licença

MIT [LICENSE](../../LICENSE) &copy; [Walber Vaz](https://github.com/walber-vaz)
