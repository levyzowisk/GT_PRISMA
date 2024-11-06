# Que É um ORM?

## Definição Simples:
ORM (Object-Relational Mapping) é uma técnica que permite que você interaja com bancos de dados relacionais usando objetos no seu código, ao invés de escrever comandos SQL manualmente.

Em termos simples:

O ORM ele tenta abstrair a complexibilidade de consultas sql no código, para um paradigma de programação que é muito usado no mercado, que é o de Orientação a objeto.

O ORM ajuda a converter dados do banco (relacional) em objetos para que você possa usar de forma mais fácil no seu código. Ele também converte objetos de volta para o formato que o banco entende.

## Por Que Usar um ORM?
### Desvantagens de Usar SQL Manualmente:
SQL Manual pode ser difícil e demorado de escrever, especialmente se o banco de dados tiver muitas tabelas e relacionamentos.
Manter o código SQL separado da lógica de programação pode gerar dificuldades de manutenção.

### Vantagens do ORM:
Simplicidade: Usar o ORM é como trabalhar com objetos no seu código.
Segurança: O ORM evita erros como SQL Injection, tornando a aplicação mais segura.
Rapidez no Desenvolvimento: Reduz a quantidade de código repetitivo, acelerando o desenvolvimento.


# Passo 1: Instalação do prisma
## Instalação do Prisma

````
    1º mkdir meu-projeto-prisma
    2º cd meu-projeto-prisma
    3º npm init -y
````
 

## Instalação do Prisma CLI e as dependências necessárias.

### Prisma (CLI): Ferramenta de linha de comando para configurar, migrar e gerenciar o banco de dados com Prisma. Usada no desenvolvimento para criar migrações e atualizar o esquema do banco.

### @Prisma/client: Biblioteca que permite ao código interagir com o banco de dados. Fornece uma API com métodos para criar, ler, atualizar e deletar dados de acordo com os modelos definidos.

````
   1º npm install prisma --save-dev
   2º npm install @prisma/client

````

# Passo 2: Inicilizar o prisma

### Inicie o Prisma no projeto. Isso criará uma pasta prisma e um arquivo de esquema chamado schema.prisma.

```` 
   1º npx prisma init
   
````

### O arquivo schema.prisma conterá a configuração inicial para conectar o Prisma ao seu banco de dados. Localize a variável DATABASE_URL e insira a string de conexão do seu banco de dados. Ela define onde o Prisma vai se conectar.

``` ex
generator client {
  provider = "prisma-client-js"
}

# O provider define qual ferramenta o Prisma vai usar para gerar o cliente. Nesse caso, o valor "prisma-client-js" indica que o Prisma deve gerar um Prisma Client em JavaScript (ou TypeScript, que é compatível).
# O Prisma Client é a biblioteca que você vai importar no seu código para interagir com o banco de dados. Ao usar "prisma-client-js", você está dizendo ao Prisma para gerar esse client em JavaScript.

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

```

```
mysql://USER:PASSWORD@HOST:PORT/DATABASE
```


# Passo 3 : Definindo Modelos no prisma

### No arquivo schema.prisma, você define os modelos (modelos são tabelas no banco de dados). Exemplo de um modelo de usuário simples:

```
model User {

  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  createdAt DateTime @default(now())
}
```

# Passo 4: Migrar o Banco de Dados

### Crie uma migração:

```
    npx prisma migrate dev --name inicial
```