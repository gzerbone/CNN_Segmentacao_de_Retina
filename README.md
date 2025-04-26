#Descrição do Código de Segmentação de Retina
Este código implementa um modelo de aprendizado profundo para segmentação de vasos sanguíneos na retina. Ele usa uma arquitetura UNet modificada chamada UNetMER (UNet with Mobile Encoder and Refinement), que incorpora codificadores MobileNetV2 para eficiência e módulos de refinamento para melhor detecção de bordas. O código abrange as seguintes etapas:

## **1. Exploração e Pré-processamento de Dados:**

* Importa bibliotecas necessárias como TensorFlow, Keras, OpenCV, etc.
* Define o caminho do dataset, que é carregado a partir do Google Drive.
* Realiza uma exploração inicial do dataset para verificar o formato, tamanho, modo de cor das imagens e a distribuição das classes.
* Verifica se há imagens corrompidas ou duplicadas.
* Normaliza as imagens (valores de pixel entre 0 e 1) e as redimensiona para um tamanho consistente.
* Divide o dataset em conjuntos de treinamento e teste.
* Cria geradores de dados com aumento de dados (rotações, espelhamento, zoom) para o conjunto de treinamento, a fim de aumentar a robustez do modelo.

## **2. Arquitetura do Modelo:**

  * Define a arquitetura UNetMER usando blocos codificadores MobileNetV2, módulos de refinamento e atenção espacial.
  * O codificador extrai características hierárquicas da imagem.
  * O decodificador reconstrói a segmentação usando as características extraídas e conexões de salto do codificador.
  * Os módulos de refinamento aprimoram a detecção de bordas.
  * A atenção espacial foca em áreas relevantes da imagem.

## **3. Treinamento e Avaliação:**

* Compila o modelo com uma função de perda combinada (Binary Crossentropy e Dice Loss) e métricas relevantes (Dice Coefficient, Accuracy, Recall, Precision).
* Treina o modelo usando os geradores de dados e callbacks para otimizar o processo de treinamento (redução da taxa de aprendizado, parada antecipada).
* Avalia o modelo no conjunto de teste para medir seu desempenho.
* Visualiza as previsões do modelo em imagens de teste para análise qualitativa.

## **4. Funções Auxiliares:**

* Inclui funções para carregar e pré-processar dados, criar geradores de dados, definir a arquitetura do modelo, compilar o modelo, definir callbacks e visualizar resultados.

# `Objetivo:`
  O objetivo deste código é treinar um modelo de aprendizado profundo capaz de segmentar com precisão os vasos sanguíneos em imagens da retina. Isso tem aplicações importantes na área médica, como auxiliar no diagnóstico e monitoramento de doenças oculares, como retinopatia diabética e glaucoma.
