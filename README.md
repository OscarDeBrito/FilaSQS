Projeto: Integração com Amazon SQS usando LocalStack

Funcionalidades

    Produzir Mensagens: Enviar mensagens para uma fila SQS simulada no LocalStack.
    Consumir Mensagens: Receber e processar mensagens da fila SQS.
    Ambiente Local: Uso do LocalStack para simular o ambiente da AWS localmente, sem necessidade de uma conta real da AWS.

Tecnologias Utilizadas

    Java 21
    AWS SDK para Java v2
    LocalStack
    Docker
    AWS CLI

Requisitos

Antes de começar, certifique-se de que você tenha as seguintes ferramentas instaladas:

    Java 11
    Docker
    AWS CLI
    IntelliJ IDEA ou outro IDE para Java

Configuração do Projeto


1. Instalar Dependências

Certifique-se de que o Maven ou Gradle está configurado no seu projeto Java. Adicione a dependência do AWS SDK para SQS no arquivo pom.xml (se estiver usando Maven):

![image](https://github.com/user-attachments/assets/833446e0-ce50-41d7-82f1-4512976d7dea)


2. Configurar o LocalStack
   
Passo 1: Iniciar o LocalStack usando Docker

Execute o seguinte comando para iniciar o LocalStack:

#### docker run --rm -it -p 4566:4566 -p 4510-4559:4510-4559 localstack/localstack

Isso iniciará o LocalStack e permitirá que os serviços da AWS sejam acessados localmente através da porta 4566.

Passo 2: Criar uma Fila SQS no LocalStack

Após iniciar o LocalStack, crie uma fila SQS simulada:


#### aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name filaSQS

3. Configurar Credenciais da AWS

O LocalStack não requer credenciais reais da AWS, mas você precisará configurá-las com valores fictícios:

bash

#### aws configure

Exemplo:

    AWS Access Key ID: AccessKeyId
    AWS Secret Access Key: SecretAccessKey
    Default region name: sa-east-1
    Default output format: json
    

4. Rodar o Projeto
Produzir Mensagens (SqsProducer)

A classe SqsProducer é usada para enviar uma mensagem para a fila SQS. Execute a classe no IntelliJ ou use o Maven/Gradle.
Consumir Mensagens (SqsConsumer)

A classe SqsConsumer é usada para receber e processar mensagens da fila SQS. Assim que a classe SqsProducer enviar a mensagem, rode esta classe para consumi-la.
5. Testar via AWS CLI

Além das classes Java, você pode testar o envio e recebimento de mensagens usando a AWS CLI.

    Enviar uma mensagem:



#### aws --endpoint-url=http://localhost:4566 sqs send-message --queue-url http://localhost:4566/000000000000/filaSQS --message-body "Mensagem de teste"

    Receber uma mensagem:



#### aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/000000000000/filaSQS

Estrutura do Projeto

bash

src/
 └── main/
     └── java/
         └── com.exemplo.sqs/
                 ├── SqsProducer.java  # Produz mensagens na fila SQS
                 └── SqsConsumer.java  # Consome mensagens da fila SQS



Referências

    Documentação do AWS SDK para Java v2
    LocalStack
    Docker





Prints:


![image](https://github.com/user-attachments/assets/a16cb375-305b-4188-b4d6-f92afa4b1111)

![image](https://github.com/user-attachments/assets/2e64cd4a-4800-4e5e-ba29-b3be71acd500)

![image](https://github.com/user-attachments/assets/c4b2a7db-d003-4597-bd41-53b4f21ddc86)

![image](https://github.com/user-attachments/assets/d9668bd6-156e-4cfa-930e-49bd6814903e)

