# Classificador de Comentários

Este é um projeto de classificação de comentários que utiliza modelos pré-treinados utilizando o algoritmo BERT. O modelo passou por um processo de fine-tunning utilizando o framework TensorFlow.

# TL;DR - Execução do projeto
Para executar este projeto é necessário ter o docker instalado na máquina.
1. Clonando o repositório
2. Navegue para o repositório clonado
3. Buildando e Executando a imagem Docker
```
docker build -t alan_soul . && docker run alan_soul
```

# Modelo Pré-Treinado
Neste projeto, utilizamos o modelo [BERTimbau Base](https://huggingface.co/neuralmind/bert-base-portuguese-cased). Ele foi refinado utilizando cerca de 10.000 comentários coletados do site Americanas.com. O arquivo original contém mais de 130 mil comentários e pode ser encontrado [aqui](https://www.kaggle.com/datasets/fredericods/ptbr-sentiment-analysis-datasets?resource=download).

A ideia foi associar as notas dos usuários com comentários. Os critérios foram os seguintes:
- Notas 1 e 2: "Negativo"
- Nota 3: "Neutro"
- Notas 4 e 5: "Positivo"

Os comentários então foram tokenizados em palavras-chave e associados a essas labels.

# Acurácia e Tempo de Treinamento
O modelo alcança uma acurácia de aproximadamente 84%. 

É importante pontuar que o treinamento foi realizado por apenas 2 horas e utilizando recursos limitados. Acredito que um resultado melhor pode ser alcançado utilizando mais comentários e alterando configurações do modelo.

# Descrição dos Arquivos do Projeto
- `download_model.py`: Como o arquivo do modelo é muito grande para ser colocado diretamente em um repositório do github, ele foi colocado em um bucket no Google Cloud Storage (GCS). Esse arquivo é responsável por baixá-lo.
- `gcp-key.json`: chave json para acessar o modelo.
- `clear_data.py`: Este arquivo realiza a limpeza dos dados utilizados no treinamento.
- `train_model.py`: Contém o código utilizado para treinar o algoritmo de classificação.
- `Dockerfile`: O arquivo Dockerfile está configurado para construir a imagem do projeto e baixar as dependências necessárias.
- `b2w.csv`: Arquivo com as reviews.
- `clear_b2w.csv`: Arquivo a ser lido pelo train_model.py.
- `start.py`: Carrega o modelo treinado e classifica o comentário associado à variável `test_sentence`.

Por padrão o modelo não será treinado novamente, porém o código foi incluído para avaliação.
#
