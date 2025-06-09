# FEDformer_Time_Series
FEDformer es un modelo de Transformer especialmente diseñado para la predicción de series temporales de largo plazo. Parte de la motivación de este enfoque es que los Transformers clásicos suelen ser costosos (complejidad O(N²)) y tienden a no capturar bien la tendencia global de la serie (predicen cada instante de forma casi independiente)
Colab: https://colab.research.google.com/drive/1W9Qu6BDrHHFIxhY-Y6nf6ppmYpTpqwLx?usp=sharing
Articulo de Referencia: [[paper](https://arxiv.org/abs/2201.12740)]. 
## Frequency Enhanced Attention
|![Figure1](https://user-images.githubusercontent.com/44238026/171341166-5df0e915-d876-481b-9fbe-afdb2dc47507.png)|
|:--:| 
| *Figure 1. Overall structure of FEDformer* |

|![image](https://user-images.githubusercontent.com/44238026/171343471-7dd079f3-8e0e-442b-acc1-d406d4a3d86a.png) | ![image](https://user-images.githubusercontent.com/44238026/171343510-a203a1a1-db78-4084-8c36-62aa0c6c7ffe.png)
|:--:|:--:|
| *Figure 2. Frequency Enhanced Block (FEB)* | *Figure 3. Frequency Enhanced Attention (FEA)* |
