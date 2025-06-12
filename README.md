# FEDformer_Time_Series Frequency Enhanced Decomposed Transformer para series temporales
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

## Fundamentos teóricos y arquitectura del modelo
- **Decomposición espectral**: separa la serie en componentes de baja frecuencia (tendencia) y alta frecuencia (estacionalidad) usando FFT o wavelets.  
- **Bloques FEB / FEA**: realizan atención en el dominio de frecuencia seleccionando un número fijo de modos, lo que reduce la complejidad a O(N).  
- **MOEDecomp**: “Mixture of Experts Decomposition” aplica filtros de media móvil de distintos anchos para extraer explícitamente patrones de tendencia de largo plazo.  
- **Encoder–Decoder**: cada capa de encoder/decoder alterna FEB/FEA, bloques feed-forward y MOEDecomp, combinando las salidas de frecuencia y tendencia para modelar series largas.

## Funcionamiento interno y mecanismo de predicción
- **Entrada**: vector de embedding de la serie de tiempo (posicional + características).  
- **Descomposición**: cada capa extrae componentes de frecuencia y tendencia de forma iterativa.  
- **Atención cruzada en frecuencia**: el decoder refina la parte estacional mediante atención entre la salida del encoder y el token de inicio.  
- **Recomposición**: suma de la predicción estacional (proyectada) y la tendencia final para generar el pronóstico.

## Comparación con otros modelos
- **Transformers clásicos**: O(N²) en atención; no garantizan captura de tendencia global.  
- **Informer / Autoformer**: atención ProbSparse y autocorrelación usan O(N log N), pero siguen siendo más costosos y menos explícitos en tendencia.  
- **FEDformer**: complejidad O(N), mejor captura de patrones de largo plazo y estacionalidades gracias a la descomposición y atención en frecuencia.

## Ventajas técnicas y computacionales
- **Eficiencia**: complejidad lineal en la longitud de la secuencia, adecuada para series muy largas.  
- **Interpretabilidad**: descomposición explícita de tendencia y estacionalidad facilita análisis de componentes.  
- **Robustez**: evita sobreajuste al procesar solo los modos frecuenciales más informativos.  
- **Flexibilidad**: dos variantes de frecuencia (Fourier y Wavelet) permiten adaptarse a diferentes características de series.

## Aplicaciones reales
- **Energía**: pronóstico de carga eléctrica a largo plazo con fuertes componentes estacionales.  
- **Salud pública**: predicción de incidencia de enfermedades estacionales (ej. influenza).  
- **Transporte**: forecasting de flujo vehicular o de pasajeros en redes de tráfico.  
- **Finanzas / Commodities**: modelado de precios de carbono, petróleo, metales, donde tendencia y ruido de alta frecuencia coexisten.

## Ejemplos y casos de uso publicados
- **Mercado de carbono en China**: DA-FEDformer para predicción de precios de emisiones, combinando FEDformer con ICEEMDAN y corrección de errores (Hong et al., 2024).  
- **Benchmarks públicos**: mejor desempeño en datasets ETTh1/ETTm1 (energía), ECL (electricity), Weather, Traffic, ILI (salud).  
- **Repositorios**: implementación oficial en PyTorch disponible en [github.com/MAZiqing/FEDformer](https://github.com/MAZiqing/FEDformer), con scripts que reproducen los experimentos del artículo.
