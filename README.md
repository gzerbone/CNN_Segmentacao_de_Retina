# 🧠 Segmentação de Vasos Sanguíneos na Retina usando **UNetMER**

Este repositório contém um código em **Python** que implementa um modelo de aprendizado profundo para segmentação de vasos sanguíneos em imagens da retina. O modelo é baseado na arquitetura **UNet**, com modificações para melhorar a eficiência e a precisão.

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

Siga estes passos:

1. 📥 Baixe o dataset **"Retina Blood Vessel"** do Kaggle.
2. 🗂️ Organize o dataset conforme a estrutura abaixo:

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

3. 🖥️ Execute o código Python para treinar e avaliar o modelo.

### ⚠️ Observações:

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
| Catharina | [@catharinapc](https://github.com/catharinapc) |
| Anderson Mendes | [@Andersonn-2000](https://github.com/Andersonn-2000) |

---
