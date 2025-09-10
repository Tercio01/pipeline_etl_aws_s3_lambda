# pipeline_etl_aws_s3_lambda
Pipeline de ETL serveless na AWS que processa dados JSON de pedidos, transforma com Python/Pandas e armazena em formato Parquet.
# Pipeline de ETL Serverless na AWS para Processamento de Pedidos

## 📖 Sobre o Projeto

Este projeto demonstra a construção de um pipeline de dados 100% serverless na nuvem AWS. O objetivo é simular um cenário real de e-commerce, onde dados de pedidos são gerados em formato JSON, processados em tempo real e armazenados em um formato analítico otimizado (Parquet) em um Data Lake.

Esta é uma solução robusta, escalável e de baixo custo, utilizando as melhores práticas de arquitetura orientada a eventos.

---

## 🏛️ Arquitetura da Solução

O fluxo de dados segue a seguinte arquitetura:

1. **Ingestão:** Arquivos JSON contendo dados de pedidos são enviados para um bucket S3, em uma pasta de dados brutos (`incoming`).
2. **Gatilho (Trigger):** O evento de criação de um novo objeto no S3 aciona automaticamente uma função AWS Lambda.
3. **Processamento (ETL):** A função Lambda, escrita em Python, executa as seguintes tarefas:
    * Lê o arquivo JSON do S3.
    * Utiliza a biblioteca **Pandas/AWS Data Wrangler** para achatar a estrutura aninhada do JSON e limpar os dados.
    * Converte o DataFrame processado para o formato **Apache Parquet**.
4. **Armazenamento:** O arquivo Parquet resultante é salvo em outra pasta no mesmo bucket S3, servindo como nosso Data Lake.

![Diagrama da Arquitetura](https://github.com/user-attachments/assets/34d6c5d2-5361-4379-9c5f-a5cb780df9a8)

---

## 🛠️ Tecnologias Utilizadas

As seguintes ferramentas e tecnologias foram utilizadas na construção do projeto:

* **Cloud Provider:** AWS (Amazon Web Services)
* **Armazenamento:** Amazon S3
* **Processamento Serverless:** AWS Lambda
* **Segurança e Permissões:** AWS IAM (Identity and Access Management)
* **Monitoramento e Logs:** AWS CloudWatch
* **Linguagem de Programação:** Python 3.9
* **Bibliotecas Principais:** Pandas, AWS Data Wrangler (para interação com serviços AWS)
* **Formato de Dados:** JSON (origem), Apache Parquet (destino)
* **Infraestrutura como Código (IaC):** Configuração realizada via Console da AWS.

---

## 챌 Desafios e Aprendizados

A construção deste projeto foi uma jornada de grande aprendizado. Um dos principais desafios foi a configuração correta das permissões no **IAM**, garantindo que a função Lambda tivesse acesso para ler do S3 e escrever logs no CloudWatch, seguindo o princípio do menor privilégio. Outro ponto crucial foi o gerenciamento de dependências externas (Pandas e AWS Wrangler) através das **AWS Lambda Layers**, um conceito fundamental para o desenvolvimento serverless. A depuração de erros utilizando os logs do CloudWatch foi essencial para o sucesso do pipeline.

---

## 🚀 Como Executar o Projeto

Para replicar este projeto, siga os seguintes passos:
1. Crie um bucket no S3 com duas pastas: `orders_json_incoming/` e `orders_parquet_datalake/`.
2. Crie uma função Lambda com o código disponível em `/src/lambda_function.py`.
3. Configure as permissões no IAM e as Lambda Layers necessárias.
4. Configure o gatilho do S3 na função Lambda para monitorar a pasta de entrada.
5. Faça o upload do arquivo `orders_etl.json` para a pasta `orders_json_incoming/` para iniciar o pipeline.
