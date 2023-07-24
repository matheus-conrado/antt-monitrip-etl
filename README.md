
# Coleta de dados do Monitriip - Sistema de Monitoramento do Transporte Rodoviário Interestadual e Internacional Coletivo de Passageiro

## Introdução
Este projeto pretende extrair os dados de bilhete de passagem coletados pelo Sistema de Monitoramento do Transporte Rodoviário Interestadual e Internacional Coletivo de Passageiros. O periodo de coleta fornecido pelo site é de Janeiro/2019 à Junho/2023.

## Diagrama de Arquitetura

![ETL_ANTT_Monitrip](https://github.com/matheus-conrado/etl-antt-monitrip/raw/master/etl-antt-monitrip.jpg?raw=true)

## Visão Geral

+ O objetivo principal deste projeto é demonstrar a criacao de um pipeline de coleta de dados usando os dados do sistema Monitrip fornecido pela ANTT via [Portal de dados abertos do Governo Federal](https://dados.gov.br/dados/conjuntos-dados/monitriip-bilhetes-de-passagem1).

+ Usaremos o Spark desde a extração, transformação e processamento dos dados. Neste projeto vamos realizar a configuração de uma imagem Docker que sera responsavel por processar os notebooks usando o papermil, uma ferramenta de parametrização e execução de jupyter notebooks.

## Arquivos do Projeto

+ ``monitrip_extract_files.ipynb``: Este arquivo tem como principal objetivo acessar o link da api do portal de dados abertos e coletar os arquivos brutos para posteriormente serem processados.
+ ``monitrip_transform_files.ipynb``: Este arquivo tem como principal objetivo extrair os arquivo que foram baixados no processo de extração, e aplicar uma modelagem prévia baseado nos schemas fornecidos na pasta ```schemas/``` que por sua vez foram basedados no [dicionário fornecido pela ANTT](https://dados.antt.gov.br/dataset/989414bc-6327-4a1c-be47-22ba31a9d271/resource/375d8963-d0e2-4cd3-bc5f-e532613646b3/download/venda_passagem_dicionario_dados.pdf), essa integração é feita afim de padronizar e manter a conformidade dos dados fornecidos.
+ ``monitrip_load_files.ipynb``: Este arquivo tem como objetivo carregar os dados que foram tratados no processo de transformação. Nesta etapa podemos escolher dois métodos de carga. O primeiro seria baseada no schema fornecido, já realizar o envio dos dados para o Kafka que posteriormente poderia replicar para uma base de dados, ou realizar a gravação destes registros em um sistema de armazenamento de objetos como o S3 da AWS por exemplo.

**Todos os notebooks serão convertidos para python e poderem ser utilizados no Lambda da AWS 
