# 🧠 Segmentação de Vasos Sanguíneos na Retina usando **UNetMER**

Este repositório contém um código em **Python** que implementa um modelo de aprendizado profundo para segmentação de vasos sanguíneos em imagens da retina. O modelo é baseado na arquitetura **UNet**, com modificações para melhorar a eficiência e a precisão.

---

## 📑 Tabela de Conteúdo

- [📚 Descrição do Projeto](#-descrição-do-projeto)
- [📂 Dataset](#-dataset)
- [🧹 Pré-processamento](#-pré-processamento)
- [🏗️ Arquitetura do Modelo](#-arquitetura-do-modelo)
- [🎯 Treinamento](#-treinamento)
- [🏆 Resultados](#-resultados)
- [🚀 Como Usar](#-como-usar)
- [📦 Requisitos](#-requisitos)
- [🤝 Colaboradores](#-colaboradores)
- [⚠️ Observações](#️-observações)


---

## 📚 Descrição do Projeto

Este projeto tem como objetivo desenvolver um modelo capaz de segmentar automaticamente os vasos sanguíneos em imagens da retina. A segmentação precisa dos vasos é crucial para o diagnóstico e monitoramento de diversas doenças oculares, como **retinopatia diabética** e **glaucoma**.

✨ O modelo utilizado é chamado **UNetMER** (*UNet with Mobile Encoder and Refinement*), e incorpora:

- 🔹 **Encoder MobileNetV2:** Extração eficiente de características da imagem.
- 🔹 **Módulos de Refinamento:** Melhora da detecção de bordas dos vasos.
- 🔹 **Atenção Espacial:** Foco em áreas relevantes da imagem.

---

## 📂 Dataset

O dataset utilizado é o **"Retina Blood Vessel"** do Kaggle. Ele contém imagens da retina e suas respectivas máscaras de segmentação.

### 📁 Estrutura do Dataset:

```bash
dataset_retina/
├── Data/
│   ├── train/
│   │   ├── image/   # Imagens de treino
│   │   └── mask/    # Máscaras de treino
│   └── test/
│       ├── image/   # Imagens de teste
│       └── mask/    # Máscaras de teste
└── ...
```
---

### 🔧 Pré-processamento

As imagens do dataset passam pelas seguintes etapas antes do treinamento:

- 🖼️ **Redimensionamento:**  
  Todas as imagens são redimensionadas para **128x128 pixels**.

- ⚙️ **Normalização:**  
  Os valores dos pixels são normalizados para o intervalo **[0, 1]**.

- 🔄 **Aumento de Dados (Data Augmentation):**  
  Durante o treinamento, são aplicadas técnicas de aumento de dados para melhorar a robustez do modelo, incluindo:
  
  - Rotações aleatórias
  - Espelhamento horizontal e vertical
  - Zoom

---

## 🏗️ Arquitetura do Modelo

O modelo **UNetMER** é baseado na arquitetura UNet e é composto por:

- **Codificador:**  
  Extrai características hierárquicas usando blocos convolucionais seguidos de camadas de **Max Pooling**.

- **Decodificador:**  
  Reconstrói a segmentação utilizando:
  - Características extraídas no codificador
  - **Conexões de salto** (skip connections)
  - **Convoluções transpostas** (transposed convolutions) e **upsampling**

---

## 🎯 Treinamento

O modelo é treinado no conjunto de treinamento para aprender a mapear imagens para suas máscaras correspondentes.

### ⚡ Função de Perda:

- Combinação de **Binary Crossentropy** e **Dice Loss** para otimizar a segmentação.

### 📊 Métricas Avaliadas:

- **Dice Coefficient**
- **Accuracy**
- **Recall**
- **Precision**

---

## 🏆 Resultados

Após o treinamento, o modelo é avaliado no conjunto de teste do dataset. Os resultados obtidos demonstram que o modelo UNetMER é capaz de segmentar os vasos sanguíneos na retina com alta precisão.

---

## 🚀 Como Usar

Siga os passos abaixo para executar o projeto, seja localmente ou no Google Colab:

### 1. 📥 Baixe o Dataset

Primeiro, você precisa baixar o dataset **"Retina Blood Vessel"** do Kaggle. Você pode acessá-lo através deste [link do Kaggle](https://www.kaggle.com/datasets/abdallahwagih/retina-blood-vessel).

### 2. 🗂️ Organize o Dataset

Após o download, organize o dataset de acordo com a estrutura de diretórios esperada. A estrutura do dataset deve ser a seguinte:

```bash
dataset_retina/
├── Data/
│   ├── train/
│   │   ├── image/   # Imagens de treino
│   │   └── mask/    # Máscaras de treino
│   └── test/
│       ├── image/   # Imagens de teste
│       └── mask/    # Máscaras de teste
└── ...
```
### 3. 🖥️ Rodando Localmente
Se você optar por rodar o código localmente, você precisará alterar o caminho do dataset no código. O seguinte código mostra como definir o caminho para o dataset no seu computador:
```python
# Se você estiver rodando localmente, defina o caminho para o seu dataset
path = '/caminho/para/o/seu/dataset_retina'  # Substitua pelo caminho onde você armazenou o dataset

# Definição dos caminhos das pastas de treino e teste dentro do dataset
pasta_treinamento  = os.path.join(path, "Data", "train")  # Caminho para as imagens de treino
pasta_teste  = os.path.join(path, "Data", "test")  # Caminho para as imagens de teste
```

### 4. 🌐 Rodando no Google Colab com Google Drive
Caso você prefira rodar o código no Google Colab, você pode facilitar o gerenciamento e o manuseio das imagens ao armazenar o dataset no seu Google Drive.  
- **Passos:**
  * **1.** `Armazene o dataset no seu Google Drive:` Crie uma pasta chamada dataset_retina em seu Google Drive e faça o upload das pastas do dataset (como "Data", "train", "test", etc.) dentro dela.
  
  * **2.** `Monte seu Google Drive no Colab:` No Colab, você pode montar seu Google Drive para acessar o dataset diretamente.
    * Aqui está o código para montar o Google Drive e definir os caminhos para as imagens de treino e teste (como está no [notebook](https://github.com/gzerbone/CNN_Segmentacao_de_Retina/blob/main/CNN_Segmentação_de_Retina.ipynb)):
     ``` python
    # Montando o Google Drive no Colab para acessar o dataset
    from google.colab import drive
    drive.mount('/content/drive', force_remount=True)
    
    # Defina o caminho para o seu dataset armazenado no Google Drive
    path = '/content/drive/MyDrive/dataset_retina'  # Substitua pelo caminho correto se necessário
    
    # Definição dos caminhos das pastas de treino e teste dentro do dataset
    pasta_treinamento  = os.path.join(path, "Data", "train")  # Caminho para as imagens de treino
    pasta_teste  = os.path.join(path, "Data", "test")  # Caminho para as imagens de teste

      ```
### 5. 🎯 Execute o Código
Após configurar o caminho do dataset (seja local ou no Google Drive), execute o código Python para treinar e avaliar o modelo.

---

## 📦 Requisitos

Bibliotecas utilizadas:

### 📊 Bibliotecas de Data Science

- `numpy >= 1.19.0`
- `pandas >= 1.3.0`
- `scikit-learn >= 1.0.0`
- `matplotlib >= 3.4.0`
- `seaborn >= 0.11.0`

### 🧠 Deep Learning

- `tensorflow >= 2.8.0`
- `tensorflow-addons >= 0.16.0`

### 🖼️ Processamento de Imagem

- `pillow >= 9.0.0`
- `opencv-python >= 4.5.5`
- `scipy >= 1.8.0`

### ⚙️ MLOps

- `mlflow >= 1.20.0`

### 🛠️ Utilitários

- `jupyter >= 1.0.0`
- `python-dotenv >= 0.19.0`
- `tqdm >= 4.62.0`
- `ipykernel >= 6.0.0`
- `pyyaml >= 6.0`

### 📈 Visualização Avançada

- `plotly >= 5.5.0`

---

### 🚀 Instalação rápida

Para instalar todos os pacotes de uma vez:

```bash
pip install numpy>=1.19.0 pandas>=1.3.0 scikit-learn>=1.0.0 matplotlib>=3.4.0 seaborn>=0.11.0 tensorflow>=2.8.0 tensorflow-addons>=0.16.0 pillow>=9.0.0 opencv-python>=4.5.5 scipy>=1.8.0 mlflow>=1.20.0 jupyter>=1.0.0 python-dotenv>=0.19.0 tqdm>=4.62.0 ipykernel>=6.0.0 pyyaml>=6.0 plotly>=5.5.0
```

## ⚠️ Observações:

- Certifique-se de que as bibliotecas necessárias estão instaladas:  
  (`TensorFlow`, `Keras`, `OpenCV`, etc.)
- Ajuste o **caminho para o dataset** no código conforme necessário.
- Os **hiperparâmetros** podem ser modificados para melhorar o desempenho conforme o seu ambiente de execução.

---

## 🤝 Colaboradores

> Agradecimentos especiais a todos que contribuíram para este projeto 🌟:

| Nome  | GitHub |
| :--- | :--- |
| Gabriela Zerbone | [@gzerbone](https://github.com/gzerbone) |
| Hanna Câmara da Justa | [@HannaCJ ](https://github.com/HannaCJ ) |
| Catharina Carneiro | [@catharinapc](https://github.com/catharinapc) |
| Anderson Mendes | [@Andersonn-2000](https://github.com/Andersonn-2000) |

---

<p align="center">
  <a href="https://github.com/gzerbone/CNN_Segmentacao_de_Retina">
    <img alt="Python" src="https://img.shields.io/badge/Python-3.8%2B-blue">
  </a>
  <a href="#">
    <img alt="Status" src="https://img.shields.io/badge/Status-Em%20Desenvolvimento-orange">
  </a>
  <a href="#">
    <img alt="Made With" src="https://img.shields.io/badge/Made%20with-❤️-red">
  </a>
  <a href="#">
    <img alt="License" src="https://img.shields.io/badge/License-MIT-blue.svg">
  </a>
</p>

