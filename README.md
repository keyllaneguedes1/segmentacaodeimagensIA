# 🛣️ Segmentação de Estradas com DeepLabV3+ e ResNet50 no Dataset KITTI Road

Este projeto implementa uma rede de segmentação semântica baseada em **DeepLabV3+ com backbone ResNet50** para identificar automaticamente **estradas em imagens urbanas**. Ele é comparado com uma versão anterior baseada em **U-Net**, com foco em melhorar a **precisão**, **robustez** e **capacidade de generalização**.

---

## 📦 Dataset Utilizado

- **KITTI Road Dataset**  
  Fonte: http://www.cvlibs.net/datasets/kitti/eval_road.php  
  Contém imagens reais de tráfego com rotulagem pixel a pixel para detecção de estrada.

---

## 📊 Comparativo: DeepLabV3+ vs U-Net

| Característica                  | DeepLabV3+ com ResNet50           | U-Net Clássica                         |
|--------------------------------|----------------------------------|----------------------------------------|
| **Backbone**                   | ResNet50 pré-treinada (ImageNet) | Arquitetura própria com convoluções    |
| **Módulo Especial**            | ASPP (Atrous Spatial Pyramid)    | Conexões de atalho (skip connections)  |
| **Capacidade de Generalização**| Alta (graças ao ResNet e ASPP)   | Boa, mas limitada em contextos complexos |
| **Precisão nas bordas**        | Melhor (captura multiescala)     | Pode suavizar bordas                   |
| **Métricas médias**            | IoU ≈ **0.84**, Dice ≈ **0.89**  | IoU ≈ **0.81**, Dice ≈ **0.88**        |
| **Tempo de Treinamento**       | Maior (modelo mais profundo)     | Mais leve e rápido para treinar        |
| **Aplicações**                 | Projetos robustos em produção    | Protótipos e aplicações educacionais   |

📌 *Conclusão*: A **DeepLabV3+ supera a U-Net** em precisão e detalhamento, especialmente em imagens urbanas complexas. A U-Net, no entanto, é mais leve e fácil de adaptar em dispositivos embarcados ou ambientes com menos recursos computacionais.

---

## 🧠 Arquitetura Utilizada

- **Entrada**: imagens RGB 512x512
- **Backbone**: `ResNet50` com pesos do ImageNet
- **Módulo ASPP**: convoluções dilatadas em paralelos
- **Decoder**: upsampling + skip connections
- **Saída**: Máscara binária (sigmoid) com um canal

---

## 🔧 Treinamento

- Função de perda: `binary_crossentropy`
- Otimizador: `Adam`
- Métricas: `Accuracy`, `Precision`, `Recall`, `MeanIoU`
- Técnicas de *augmentation* com `ImageDataGenerator`

---

## 🎯 Avaliação

- **IoU médio**: ~0.84  
- **Dice médio**: ~0.89  
- Visualizações detalhadas com sobreposição da predição na imagem original

---

## 📁 Comparação Visual (DeepLabV3+ vs U-Net)

### Exemplo: Máscara predita 

# DeepLabV3+ DeepLabV3+
<img width="1572" height="403" alt="image" src="https://github.com/user-attachments/assets/9b454974-d04f-4b3d-bb56-0b3e31430727" />

#UNet
<img width="1187" height="174" alt="image" src="https://github.com/user-attachments/assets/4354dfd0-1942-4adf-8d19-9acb063932e5" />


> DeepLabV3+ apresenta maior nitidez e aderência às bordas reais da estrada.

---

## 🔬 Código e Funções Relevantes

- `load_kitti_data(...)`: Carrega as imagens e máscaras com base em padrões do KITTI
- `ASPP`: Camada personalizada para extração multiescala
- `DeeplabV3Plus`: Criação do modelo completo
- `compute_iou(...)` e `compute_dice(...)`: Avaliação das máscaras

---
Código DeepLabV3+: https://colab.research.google.com/drive/15sHKMgnreo-UFKsIk65Tki3o-y_VyHDf  

Código UNet: https://colab.research.google.com/drive/12rGaXbZfIH59HmMcwf4i07u95nQ2c1eF

---

## 📜 Licença

Uso educacional e acadêmico. Dataset KITTI possui sua própria [licença de uso](http://www.cvlibs.net/datasets/kitti/index.php#license).
