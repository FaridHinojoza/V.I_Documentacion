# Reporte Consolidado: Evaluación del Costo Computacional y Rendimiento de Hardware en la Literatura de Merodeo y Detección de Anomalías Peatonales

**Proyecto:** Desarrollo de un sistema inteligente de videovigilancia para la detección de merodeo peatonal y trayectorias recurrentes mediante visión artificial y cercos virtuales dinámicos  
**Autores del Proyecto:** Denilson Celi y Raúl Hinojoza  
**Institución:** Universidad de las Fuerzas Armadas ESPE  
**Materia:** Lectura y Redacción de Textos Académicos  
**Fecha de Emisión:** 11 de noviembre de 2026  

---

## 1. Resumen Ejecutivo y Estadísticas Globales

El presente informe técnico proporciona una evaluación exhaustiva y cuantitativa del costo computacional, las especificaciones de hardware y el rendimiento temporal en el corpus cerrado de trece artículos científicos autorizados correspondientes a la sección de Trabajos Relacionados del proyecto. El análisis responde a la necesidad crítica de fundamentar con rigor metodológico el balance entre precisión de detección y velocidad de procesamiento en sistemas de videovigilancia inteligente para la detección de merodeo peatonal.

### 1.1. Panorama del Tratamiento del Costo Computacional en la Literatura

El examen detallado del corpus revela una notable heterogeneidad metodológica en el modo en que los investigadores abordan el costo computacional:

1. **Abordaje Formal Cuantitativo (4 de 13 artículos, 30.77%):** Li y Huang (2024), Vu et al. (2026), Lee y Park (2026) y Zhao et al. (2025) incorporan el costo computacional como un eje de investigación formal. Estos trabajos caracterizan experimentalmente la sobrecarga temporal mediante tasas de cuadros por segundo (FPS) reales, latencias desglosadas por etapa algorítmica, operaciones de punto flotante (GFLOPs) o estudios de ablación paramétrica, ejecutando sus modelos sobre plataformas de cómputo descritas con detalle de ingeniería.
2. **Abordaje Parcial o Basado en Tiempos de Ejecución (8 de 13 artículos, 61.54%):** Jiang et al. (2022), Shanmughapriya et al. (2022), Zhang et al. (2023), Waddenkery y Soma (2024), Yang et al. (2024), Thosar et al. (2025), Jeoung et al. (2026) y Jiménez-Frías et al. (2026) tratan el rendimiento temporal de forma segmentada. Algunos reportan tiempos de ejecución cronometrados para un módulo específico (Jiang et al. en AlphaPose y red recurrente, Jiménez-Frías et al. en estabilización de video), otros miden throughput global en video continuo sin desglosar componentes (Yang et al. entre 43.2 y 654.5 FPS), o bien exponen latencias esperadas de diseño sin validación empírica en hardware físico (Thosar et al.). En el caso de Jeoung et al. (2026), el hardware se describe exhaustivamente pero no se cuantifican los tiempos de inferencia de las redes neuronales.
3. **Abordaje Cualitativo-Teórico (1 de 13 artículos, 7.69%):** Fedosov et al. (2021) asumen teóricamente que su pipeline opera en tiempo real basándose de forma exclusiva en las credenciales de la familia YOLO, sin realizar ninguna medición cuantitativa propia ni reportar el hardware de experimentación.

### 1.2. Estadísticas de Hardware y Transparencia Experimental

- **Artículos que reportan hardware específico (6 de 13, 46.15%):**
  - Jiang et al. (2022): Tarjeta gráfica de escritorio NVIDIA GeForce RTX 2080 Ti (4,352 núcleos CUDA, 14 Gbps de velocidad de memoria).
  - Li y Huang (2024): Tarjeta gráfica NVIDIA GeForce RTX 3060 con 32 GB de memoria.
  - Jeoung et al. (2026): Procesador Intel Core i7-12700KF, 32 GB de memoria RAM y tarjeta gráfica NVIDIA GeForce RTX 3060.
  - Vu et al. (2026): Servidor con procesador Intel Xeon E5-2696 v3, tarjeta gráfica para estaciones de trabajo NVIDIA Quadro P5000 (16 GB VRAM) y 64 GB de memoria RAM.
  - Lee y Park (2026): Sistema embebido Intel NUC 11 Enthusiast con procesador Intel Core i7-1165G7, tarjeta gráfica NVIDIA GeForce RTX 2060 móvil (6 GB GDDR6) y 32 GB de memoria RAM, montado en el robot autónomo IVIS TARO.
  - Zhao et al. (2025): Plataforma de doble régimen compuesta por un servidor con procesador Intel Xeon Gold 6248R y tarjeta gráfica NVIDIA H800 para entrenamiento y benchmark sintético, y una computadora portátil con procesador Intel Core i9-13900HX, GPU NVIDIA GeForce RTX 4060 Laptop (8 GB VRAM), 32 GB de RAM y sensor LiDAR Hesai Pandar QT128 (864,000 puntos/segundo) para pruebas en vivo bajo ROS Noetic.
- **Artículos que omiten hardware ("No reporta", 7 de 13, 53.85%):**
  - Fedosov et al. (2021), Zhang et al. (2023), Waddenkery y Soma (2024) y Yang et al. (2024) no reportan procesador, acelerador gráfico ni memoria física.
  - Shanmughapriya et al. (2022) mencionan genéricamente una computadora portátil conectada a una tarjeta gráfica en la nube mediante Google Colab sin identificar el modelo de GPU ni CPU.
  - Thosar et al. (2025) aluden de forma abstracta a servidores y tarjetas gráficas sin especificar marcas ni arquitecturas.
  - Jiménez-Frías et al. (2026) agradecen el soporte del centro de supercómputo TOOLOK de CIMAT Mérida pero no detallan los nodos ni especificaciones utilizadas.

### 1.3. Dispersión y Espectro de Tasas de Procesamiento (FPS)

El rendimiento temporal exhibe una enorme dispersión en la literatura, evidenciando que la viabilidad en tiempo real depende directamente de la complejidad de los módulos complementarios integrados:

- **Cuellos de botella severos (< 5 FPS):** Shanmughapriya et al. (2022) obtienen entre 0.55 y 0.59 FPS (promedio de 0.563 FPS, con una latencia de 1.7 a 1.8 segundos por cuadro y hasta 3 segundos entre eventos) al ejecutar YOLOv3 y DeepSORT sobre cuadro completo en Google Colab. Jiménez-Frías et al. (2026) requieren 0.3056 segundos por homografía de estabilización en video 4K, equivalente a 3.27 FPS únicamente para estabilizar la imagen antes de aplicar detección.
- **Régimen de compromiso con re-identificación o datos volumétricos (7 a 18 FPS):** Zhao et al. (2025) caen a 7.30 FPS durante el despliegue físico bajo ROS con LiDAR QT128 debido a la deserialización de nubes de puntos en CPU. Li y Huang (2024) registran una caída desde los 29.6 FPS del rastreador base ByteTrack hasta 10.1 FPS al incorporar el extractor de marcha. Vu et al. (2026) alcanzan 10.6 FPS en su pipeline completo de YOLOv11n con DeepSORT bajo flujos concurrentes RTSP. Lee y Park (2026) operan a 17.2 FPS (58.11 ms por cuadro) integrando YOLOv12-m con DeepSORT y reglas deterministas sobre un robot móvil.
- **Tiempo real en detectores o benchmarks estandarizados (20 a 31 FPS):** Zhang et al. (2023) obtienen entre 10.8 y 20.5 FPS en MOT20 según la resolución, alcanzando al menos 24 FPS únicamente mediante TensorRT. Zhao et al. (2025) logran 28.56 FPS sobre el conjunto público KITTI ejecutado en una GPU NVIDIA H800. Jiang et al. (2022) reportan un throughput global de 30.16 FPS en una GPU de escritorio RTX 2080 Ti de 250 W.
- **Régimen condicional de alto throughput (43 a 654 FPS):** Yang et al. (2024) registran velocidades de 43.2 a 654.5 FPS gracias a una arquitectura en cascada donde un filtro ligero de color HSV en reposo omite la inferencia profunda de YOLOv4 y DeepSORT en los cuadros donde no hay trenes activos.

---

## 2. Tabla Comparativa Consolidada

A continuación se presenta la matriz comparativa que sintetiza las métricas de rendimiento, hardware y manejo espacial de los trece artículos analizados.

| # | Artículo (Autor, Año) | ¿Aborda Costo Computacional? | Hardware Reportado (CPU, GPU, RAM) | Velocidad / FPS | Latencia / Tiempos de Ejecución | Memoria / VRAM / Parámetros | Manejo Espacial / Impacto Cuadro Completo vs ROI |
|---|---|---|---|---|---|---|---|
| 1 | **Fedosov et al. (2021)** | Parcial (Cualitativo-Teórico) | No reporta (0 CPU, 0 GPU local, 0 RAM; V100 en Fig. 1 citada de literatura ajena) | No reporta (0 FPS medidos en el texto) | No reporta (0 ms de latencia medida) | No reporta (sin FLOPs ni parámetros propios) | Cuadro completo continuo ($S \times S$ celdas en YOLOv3). Cruce peatonal segmentado una sola vez como configuración estática manual. Sobrecarga permanente. |
| 2 | **Jiang et al. (2022)** | Parcial (Tiempos de ejecución empíricos) | GPU: NVIDIA GeForce RTX 2080 Ti (4,352 CUDA cores, 14 Gbps memory speed). CPU y RAM: No reporta | 30.16 FPS global derivado (~1900 cuadros en 63 s). AlphaPose: 47.50 FPS (40 s). MPED-RNN: 82.61 FPS (23 s). Video nativo: 30 FPS | Latencia acumulada: 33.16 ms/cuadro. Entrenamiento: 3 h 35 min para 300 épocas (batch 32, >2000 trayectorias) | No reporta FLOPs, VRAM ni número de parámetros. Justifica decodificador único para reducir tiempo | Cuadro completo continuo en AlphaPose (VGG-SSD). Genera falsos positivos graves (basurero detectado como peatón) y ambigüedad espacial al no discernir vía férrea de acera. |
| 3 | **Shanmughapriya et al. / M et al. (2022)** | Parcial (Operativo) | GPU: "Google GPU" en Google Colab (modelo no especificado). Laptop física en cliente: No reporta. CPU y RAM: No reporta. Cámara web 8 MP, enlace subida 8 Mbps | 0.55 a 0.59 FPS (Fig. 7, promedio 0.563 FPS, ~1.7 a 1.8 s por cuadro) | Intervalo de seguimiento de hasta 3 segundos ("within 3 seconds interval", Sec. V). Umbral de merodeo $t_2 = 60\text{ s}$ | No reporta FLOPs, VRAM ni memoria RAM. Modifica YOLOv3 para filtrar una sola clase ("person") | Cuadro completo continuo a 3 escalas en YOLOv3 (cuello de botella de <1 FPS). Haar Cascade facial se aplica en ROI de caja delimitadora tras merodeo. Sin cercos virtuales. |
| 4 | **Zhang et al. (2023)** | Parcial (Diseño y FPS en benchmark) | No reporta (0 CPU, 0 GPU, 0 RAM). Menciona aceleración con TensorRT sin especificar dispositivo | JYTracker en MOT20: 20.5 FPS ($512\times928$), 19.4 FPS ($608\times1088$), 11.5 FPS ($736\times1280$), 10.8 FPS ($800\times1440$). JYLD con TensorRT: $\ge 24$ FPS | No reporta latencia desglosada por componente | Parámetros detector: 9.58 M (YOLOA-S) vs 8.97 M (YOLOX-S). No reporta FLOPs, VRAM ni RAM | Cuadro completo continuo en 4 escalas de submuestreo. Caída del 47.3% en FPS al aumentar resolución. Sin cercos virtuales ni ROI previo; requiere compresión para hardware limitado. |
| 5 | **Li & Huang (2024)** | Sí (Cuantitativo formal y estudio de limitaciones) | GPU: NVIDIA GeForce RTX 3060 con 32 GB de memoria. Software: Python 3.9, PyTorch 1.8.0, CUDA 11.6. CPU: No reporta | 10.1 FPS en MOT17 (Tracker con reevaluación de marcha). Baseline ByteTrack: 29.6 FPS. StrongSORT: 7.5 FPS. BoT-SORT: 4.5 FPS | No reportada en ms para la fase final en IITB-Corridor (ACC 87.4%, Recall 90.0%, Precision 95.4%) | Detector YOLOX: 25.3 M parámetros y 118.7 GFLOPs ($1088\times608$). Marcha ResNet-like: 4.72 M parámetros y 1.183 GFLOPs por silueta. Purga temporal de memoria activa | Cuadro completo continuo. La reevaluación de marcha penaliza la velocidad en 65.9% (de 29.6 a 10.1 FPS). No utiliza cercos virtuales dinámicos; la sustracción de siluetas se aplica en toda la imagen. |
| 6 | **Waddenkery & Soma (2024)** | Parcial (Complejidad analítica de optimizador y tiempo empírico) | No reporta (0 CPU, 0 GPU, 0 RAM, 0 SO). Única declaración: "The implementation is done in python." | No reporta FPS (0 menciones). Reporta tiempo de procesamiento de 1.78 s (frente a 2.97 s, 3.81 s, 3.96 s) | Tiempo de procesamiento: 1.78 s (unidad muestral no definida: cuadro, snippet o clip). Conclusiones admiten tiempo real como trabajo futuro | Complejidad analítica del optimizador BWADO ($\mathcal{C}(\text{BWADO})$, Ec. 15). Batch 8, 100 épocas, población 50. Parámetros de DCNN, FLOPs y VRAM: No reporta | Submuestreo temporal cada 10 cuadros y reescalado de imágenes a $64\times64$ píxeles de UCF Crime. No delimita cercos virtuales ni evalúa video continuo a 30 FPS. |
| 7 | **Yang et al. (2024)** | Parcial (Throughput empírico en 104 h de video) | No reporta (0 CPU, 0 GPU, 0 RAM, 0 plataforma de cómputo) | 43.2 a 654.5 FPS (26 sesiones de 4 horas en Tabla 1). Tasa de grabación de video: 30 FPS | No reportada en ms por componente | Cita teórica de 27.6 M de parámetros para backbone CSPDarknet53. FLOPs, VRAM y RAM: No reporta | Activación por etapas: Etapa 1 detecta luz intermitente con HSV saltando 15 cuadros; Etapa 2 activa YOLOv4 + DeepSORT sobre cuadro completo en 4 zonas poligonales estáticas fijas. |
| 8 | **Thosar et al. (2025)** | Parcial (Conceptual y latencias esperadas) | No reporta (0 CPU, 0 GPU específica, 0 RAM). Menciona genéricamente GPU de alta gama y servidores | No reporta FPS propios medidos. (65 FPS es una cita a literatura de YOLOv4 en COCO) | Latencia teórica esperada (Tabla 1): Detección intrusión: 45 ms; Rostro: 50 ms; Sabotaje: 40 ms; Comportamiento sospechoso: 55 ms; Total sistema: 48 ms | No reporta FLOPs, memoria RAM/VRAM ni parámetros. Discute alta demanda de GPU en YOLOv8 como limitación | Cuadro completo sin filtrado espacial previo ni cercos virtuales dinámicos. Marco puramente conceptual con implementación en progreso. |
| 9 | **Jeoung et al. (2026)** | Parcial (Hardware detallado y motivación cualitativa sin métricas de cómputo) | CPU: Intel Core i7-12700KF. RAM: 32 GB. GPU: NVIDIA GeForce RTX 3060. Software: Python 3.11.13, PyTorch, scikit-learn, scipy | No reporta FPS de procesamiento. (Los 23 fps citados corresponden a la tasa de captura de las cámaras CCTV del dataset AI-HUB) | No reporta latencia en ms. ("Minimal latency" en conclusiones describe la autocalibración tras acumular ~150 trayectorias) | 32 GB de RAM reportados. Consumo dinámico de VRAM, FLOPs y parámetros: No reporta | Descubrimiento automático de ROIs semánticos post-rastreo con GMM y Voronoi. Sin embargo, en Etapa 1 YOLO11m procesa cuadro completo a resolución 1080p sin cerco previo. |
| 10 | **Jiménez-Frías et al. (2026)** | Parcial (Tiempos de estabilización en 4K) | No reporta hardware específico (0 CPU, 0 GPU, 0 RAM). Menciona apoyo de supercómputo TOOLOK en agradecimientos | Tiempo medio de homografía CP: 0.3056 s (~3.27 FPS para estabilización). Video 0362 (9613 cuadros): 41 min 35 s (~3.85 FPS sobre lote). ECC V1: 1.71 s; ECC V2: 2.12 s | Latencia de estabilización: 0.3056 s por homografía en resolución 4K ($3840\times2160$). Tiempos de detección YOLOv4 y rastreo IoU: No reporta | No reporta FLOPs, VRAM ni RAM. Evalúa submuestreo temporal $j=1$ a $5$ (mejor precisión global en $j=4$) | Estabilización opera sobre cuadro completo en 4K compensando deriva del dron. El ROI se aplica únicamente al final para conteo vehicular, pero la detección analiza la escena entera. |
| 11 | **Vu et al. (2026)** | Sí (Cuantitativo formal en arquitectura multicámara) | CPU: Intel Xeon E5-2696 v3. GPU: NVIDIA Quadro P5000 (16 GB VRAM). RAM: 64 GB. SO: Windows 10. CUDA online batch 1, FP32 sin TensorRT | 10.6 FPS global promedio para YOLOv11n + DeepSORT (concurrencia de 3 a 6 flujos RTSP). ByteTrack: 19.7 FPS. OC-SORT: 16.9 FPS. YOLOv8: 18.9 FPS. SCRFD: 19.2 FPS | No reporta latencia desglosada en ms por componente aislado | 16 GB VRAM y 64 GB RAM físicas especificadas; consumo en MB, GFLOPs y parámetros: No reporta. Evalúa sobrecarga de concurrencia RTSP | Polígonos virtuales fijos configurados por usuario para presencia e intrusión. La inferencia visual corre sobre el cuadro completo de cada flujo RTSP y los polígonos filtran trayectorias post-tracking. |
| 12 | **Lee & Park (2026)** | Sí (Cuantitativo formal y desglose de módulos en robot móvil) | Sistema: Intel NUC 11 Enthusiast. CPU: Intel Core i7-1165G7. GPU: NVIDIA GeForce RTX 2060 móvil (6 GB GDDR6). RAM: 32 GB. Sensor: Intel RealSense ($640\times480$) | 17.2 FPS globales en 1570 cuadros evaluados (latencia promedio total: 58.11 ms/cuadro) | Desglose en Tabla 4: YOLOv12-m: 34.54 ms (59.4% del tiempo); DeepSORT: 11.14 ms (19.2%); Reglas: 12.43 ms (21.4%). Comparativa en Tabla 9 vs ResNet+LSTM (66.8 ms + 528 ms) | 32 GB de RAM físicas. VRAM consumida, GFLOPs y parámetros exactos de YOLOv12-m fine-tuneado: No reporta | Cuadro completo nativo a $640\times480$. Aplica delimitación espacial y reglas lógicas post-detección. El detector YOLOv12-m representa el cuello de botella principal de cómputo. |
| 13 | **Zhao et al. (2025)** | Sí (Cuantitativo formal en benchmark y despliegue real en patio) | Benchmark: Intel Xeon Gold 6248R, NVIDIA H800, Ubuntu 22.04. Despliegue en vivo: Intel Core i9-13900HX, NVIDIA RTX 4060 Laptop (8 GB VRAM), 32 GB RAM, ROS Noetic, LiDAR Hesai QT128 | Benchmark KITTI: 28.56 FPS (Baseline Voxel-RCNN: 55.87 FPS). Despliegue en vivo patio de carbón (Tabla 4): 7.30 FPS promedio (7.42, 7.13 y 7.36 FPS en escenarios A, B y C) | Formaliza $\text{FPS} = 1/(T_{\text{pre}} + T_{\text{inf}} + T_{\text{post}})$. Ablación de ablación (Tabla 2): EnhancedVFE (-21.39 FPS), FocalConv (-25.29 FPS), TeBEVPooling (-11.03 FPS) | 8 GB VRAM y 32 GB RAM en host. Consumo en MB de VRAM y FLOPs: No reporta. Propone downsampling y TensorRT para mitigar sobrecarga en CPU bajo ROS | Proyección ortogonal 3D a BEV 2D para simplificar el juicio de intrusión punto-polígono. No obstante, la red EFT-RCNN procesa la nube 3D completa de $360^\circ$ antes del análisis espacial. |

---

## 3. Desglose Individual por Artículo

A continuación se desarrolla el análisis técnico exhaustivo de cada uno de los trece artículos científicos autorizados.

```
+--------------------------------------------------------------------------------------------------+
| ÍNDICE DE ANÁLISIS INDIVIDUAL POR ARTÍCULO                                                       |
+--------------------------------------------------------------------------------------------------+
| 3.1. Fedosov et al. (2021) .............................................................. Pág. 8 |
| 3.2. Jiang et al. (2022) ................................................................ Pág. 9 |
| 3.3. Shanmughapriya et al. / M, S. et al. (2022) ........................................ Pág. 10 |
| 3.4. Zhang et al. (2023) ................................................................ Pág. 11 |
| 3.5. Li & Huang (2024) .................................................................. Pág. 12 |
| 3.6. Waddenkery & Soma (2024) ........................................................... Pág. 14 |
| 3.7. Yang et al. (2024) ................................................................. Pág. 15 |
| 3.8. Thosar et al. (2025) ............................................................... Pág. 17 |
| 3.9. Jeoung et al. (2026) ............................................................... Pág. 18 |
| 3.10. Jiménez-Frías et al. (2026) ....................................................... Pág. 19 |
| 3.11. Vu et al. (2026) .................................................................. Pág. 21 |
| 3.12. Lee & Park (2026) ................................................................. Pág. 22 |
| 3.13. Zhao et al. (2025) ................................................................ Pág. 24 |
+--------------------------------------------------------------------------------------------------+
```

---

### 3.1. Fedosov et al. (2021)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Fedosov, V. P., Ibadov, S. R., Kucheryavenko, S. V., & Ibadov, R. R. (2021). *Method For Detecting Violation at a Pedestrian Crossing Using a Convolutional Neuaral Network*. 2021 Radiation and Scattering of Electromagnetic Waves (RSEMW), Divnomorskoe, Russia, pp. 451–454. IEEE. DOI: [10.1109/RSEMW52378.2021.9494089](https://doi.org/10.1109/RSEMW52378.2021.9494089).
- **Arquitectura propuesta:** Detección de objetos mediante la red neuronal convolucional YOLOv3 combinada con segmentación interactiva del cruce peatonal basada en marcas de usuario y ecuaciones cinemáticas de estimación de distancias de frenado seguro para automóviles.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Cualitativo-Teórico).
- **Justificación textual:** Los autores discuten el costo computacional de forma discursiva para justificar la elección de YOLO frente a arquitecturas precedentes. En la página 451, columna 2, afirman que las propuestas basadas en regiones presentan la desventaja crítica de su lentitud y alta demanda de recursos:
  > *"These approaches have problems, but the most significant of them is that they are slow, require a lot of computing power, and the fact that they concentrate on individual regions, and not on the whole image."*
  En contraposición, argumentan que los modelos de la familia YOLO solventan dicha limitación:
  > *"The good thing about YOLO is that this architecture does not have these problems, and it has proven to be effective many times over. Models of the YOLO family are really fast, much faster than R-CNN and others. This means that it is suitable for real-time object recognition."*
  Asimismo, en la página 453 destacan la ventaja computacional del procesamiento en una sola pasada:
  > *"Since everything is done in one pass, the model runs at almost the same speed as classification."*

#### Hardware Reportado
- **Dictamen:** No reporta.
- **Detalle de la inspección:** El texto carece de especificaciones sobre procesador (CPU), tarjeta gráfica (GPU), memoria RAM o estación de trabajo local. La única mención de hardware figura en el eje horizontal de la Figura 1 (página 451), donde aparece la etiqueta "FPS (V100)". Sin embargo, los propios autores declaran en el texto que se trata del gráfico presentado por los creadores originales de YOLO (*"the graph presented by the creators of YOLO"*), correspondiente a la curva AP frente a FPS en GPU Tesla V100 del artículo de YOLOv4 publicado por Bochkovskiy et al. (2020), constituyendo una cita externa y no un experimento propio.

#### Métricas Cuantitativas Verbatim
- **Tasa de fotogramas (FPS):** No reporta mediciones experimentales propias (0 FPS medidos).
- **Latencia y tiempos de ejecución:** No reporta (0 milisegundos).
- **Operaciones de punto flotante y parámetros:** No reporta FLOPs, GFLOPs ni conteo de parámetros entrenables.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
Fedosov et al. (2021) aplican la red YOLOv3 sobre la totalidad del cuadro de video ($S \times S$ celdas de rejilla). En la Sección III (página 453), los autores establecen que el paso de cebra es un elemento estático y que, por tanto, no requiere ser detectado en cada instante:
> *"And since, unlike cars and people who move, a pedestrian crossing (zebra crossing) is a static object in the video. Therefore, we do not need to detect a pedestrian crossing in real time, it is enough to do it once. This step can be considered a setting for this method."*
Aunque esta delimitación manual inicial alivia la necesidad de segmentar el cruce en cada fotograma, el detector neuronal YOLOv3 continúa procesando el encuadre visual completo de manera ininterrumpida. No existe un mecanismo de cerco virtual dinámico que inactive el detector o restrinja la inferencia neuronal a la zona crítica cuando no hay peatones en proximidad, incurriendo en una sobrecarga computacional permanente sobre regiones de la escena sin relevancia operativa.

---

### 3.2. Jiang et al. (2022)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Jiang, Z., Song, G., Qian, Y., & Wang, Y. (2022). *A deep learning framework for detecting and localizing abnormal pedestrian behaviors at grade crossings*. Neural Computing and Applications, 35(12), 8967–8981. https://doi.org/10.1007/s00521-022-07660-0
- **Arquitectura propuesta:** Extracción de esqueletos corporales (17 coordenadas articulares) y seguimiento mediante AlphaPose (detector VGG-SSD, módulo SSTN con ResNet-18 y red de 4-stack hourglass), seguido de un codificador-decodificador recurrente bidireccional GRU denominado MPED-RNN para reconstrucción de trayectorias y detección de comportamientos anómalos (merodeo, caídas y cruces no autorizados).

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Cuantitativo en tiempos de ejecución).
- **Justificación textual:** Jiang et al. (2022) miden y desglosan experimentalmente los tiempos de procesamiento cronometrados para las dos etapas principales del pipeline, además de reportar el tiempo de entrenamiento y justificar decisiones estructurales para reducir el costo computacional. En la página 8, columna 2, explican la simplificación de su arquitectura de red:
  > *"Note that the prediction decoder and the reconstruction decoder can be combined to form a single encoder-dual decoder structure [24]. However, our work only contains the reconstruction decoder as we intend to detect and localize the anomaly through the reconstruction error of trajectories. In addition, using the reconstruction decoder only also reduces computational time."*
  Asimismo, en la página 3, columna 1, advierten sobre la limitación computacional de modelos que requieren reentrenamiento continuo:
  > *"The current research that requires retraining the model to accommodate different crossing scenes and spots may be too computationally demanding in the field."*

#### Hardware Reportado
- **Ubicación:** Página 9, Sección 4 (*Results and discussion*), columna 2, líneas 60–63.
- **Cita verbatim:**
  > *"All the experiments are conducted on an NVIDIA GeForce RTX 2080 Ti GPU computing workstation with 4,352 CUDA cores and 14 Gbps memory speed."*
- **Especificaciones:** Tarjeta gráfica para estaciones de trabajo NVIDIA GeForce RTX 2080 Ti (arquitectura Turing, 4,352 núcleos CUDA, 14 Gbps de velocidad de memoria, 11 GB GDDR6). Procesador (CPU) y memoria RAM principal: No reportan.

#### Métricas Cuantitativas Verbatim
- **Tiempo de entrenamiento (Página 9, Sección 4):**
  > *"The training of the proposed anomaly detection model takes about 3 h and 35 min for a total of 300 epochs with a batch size of 32."* (Evaluado sobre más de 2000 trayectorias normales extraídas de 50 horas de video).
- **Tiempos de inferencia por etapas en Caso de Estudio 1 (Página 11, Sección 4.1):**
  > *"The computational time of the proposed framework includes two parts: (1) generating the skeleton trajectories of pedestrians using Alphapose and (2) detecting/localizing the anomalies of the trajectories... Correspondingly, taking Case study 1 in this work as an example, it costs 40 s to process nearly 1900 frames using Alphapose. For anomaly detection, the proposed method takes 23 s to detect and localize the anomalies in all these frames."*
- **Valores derivados exactos:**
  - Etapa 1 (AlphaPose sobre ~1900 cuadros): 40 segundos, equivalente a **47.50 FPS** (21.05 ms por cuadro), consumiendo el **63.49%** del presupuesto temporal.
  - Etapa 2 (MPED-RNN GRU sobre ~1900 cuadros): 23 segundos, equivalente a **82.61 FPS** (12.11 ms por cuadro), consumiendo el **36.51%** del presupuesto temporal.
  - Tubería completa acumulada: 63 segundos para ~1900 cuadros, equivalente a **30.16 FPS** (33.16 ms por cuadro global).
  - Tasa de captura del video de prueba: **30 FPS** (*"The video used in testing has 30 frames per second"*, pág. 9).
- **Métricas no reportadas:** No reportan latencia de transmisión, FLOPs o GFLOPs, conteo de parámetros de los modelos, consumo dinámico de VRAM ni potencia eléctrica en Watts.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
AlphaPose procesa la totalidad del cuadro de video sin un filtrado espacial por región de interés. Este procesamiento indiscriminado generó dos deficiencias graves documentadas por los autores:
1. **Falsos positivos por objetos estáticos en el fondo:** En la página 6, Sección 3.1, los autores documentan que un basurero municipal fue detectado y rastreado como peatón:
   > *"Figure 4 illustrates one of these examples, in which a trash can (enlarged in the dashed red box) is detected as a pedestrian by mistake... In this work, since the wrong detection issue was only observed at one grade crossing location, the false data are manually removed."*
2. **Ambigüedad espacial en merodeo:** En el Caso de Estudio 2 (página 12), el sistema no pudo clasificar con certeza si la permanencia prolongada constituía peligro debido a la falta de cercos virtuales:
   > *"...because it is difficult to define whether the lingering behavior happens on the rail or on the road."*
Un cerco virtual dinámico habría evitado el cómputo del 63.5% del tiempo en áreas desiertas y suprimido por completo las detecciones espurias de mobiliario urbano.

---

### 3.3. Shanmughapriya et al. / M, S. et al. (2022)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Shanmughapriya M, Gunasundari S, S Bharathy. (2022). *Loitering Detection in Home Surveillance System*. 2022 10th IEEE International Conference on Emerging Trends in Engineering & Technology - Signal and Information Processing (ICETET-SIP-22), IEEE, pp. 1–6. DOI: [10.1109/ICETET-SIP-2254415.2022.9791651](https://doi.org/10.1109/ICETET-SIP-2254415.2022.9791651).
- **Arquitectura propuesta:** Detección de personas mediante YOLOv3 preentrenado en MS COCO y adaptado a una sola clase, seguimiento multiobjetivo con DeepSORT y filtro de Kalman para cálculo de tiempo de permanencia (*dwell time*), y activación condicional de un clasificador Haar Cascade para reconocimiento facial al superar el umbral temporal.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Operativo).
- **Justificación textual:** En la página 1, columna 2, los autores identifican conceptualmente la pesadez de los flujos de video:
  > *"Video is a heavy weight data, contains both image and time information, raw video data cannot be used for automatic analysis and processing... The RGB video input provides overhead of Alignment, Movement and Illumination variations."*
  Para atenuar esta sobrecarga, modifican el detector YOLOv3 reduciendo los filtros convolucionales a la clase exclusiva de peatones (página 3, columna 1):
  > *"The YOLOv3 is modified in such a way that it detects only one class that is persons... in the convolution step the number of filters is changed to filter a single class of detection."*
  Asimismo, formalizan matemáticamente la relación de velocidad en la Ecuación 3 (página 4):
  $$\text{FPS} = \frac{1}{\text{Processing time of the frame}}$$

#### Hardware Reportado
- **Dictamen:** Incompleto / No reporta especificaciones de cómputo.
- **Detalle verbatim:**
  - GPU: Mencionan genéricamente **"Google GPU"** en la nube mediante Google Colab, sin especificar el modelo (K80, T4, P100 o V100):
    > *"Google colab is used for implementation of the proposed system. The colab is set up in such a way that the tensor flow model and the GPU are enabled."* (Pág. 4, Sec. IV-A).
    > *"The Google GPU used provides tracking within 3 seconds interval..."* (Pág. 5, Sec. V).
  - CPU y memoria RAM: No reportan.
  - Dispositivo cliente: Mencionan una computadora portátil (*laptop*) conectada a una cámara web USB de 8 megapíxeles (Figura 6, pág. 3), sin reportar marca, procesador ni memoria.
  - Conexión de red: Requiere una velocidad de subida mínima de **8 Mbps** hacia los servidores de Google Colab.

#### Métricas Cuantitativas Verbatim
- **Tasa de fotogramas (FPS):** En la consola de ejecución mostrada en la Figura 7 (página 4, columna 2), se observan las siguientes mediciones directas:
  - Cuadro 136: **0.55 FPS**
  - Cuadro 137: **0.55 FPS**
  - Cuadro 138: **0.56 FPS**
  - Cuadro 139: **0.59 FPS**
  *(Promedio registrado: 0.563 FPS, equivalente a una latencia de 1.69 a 1.82 segundos por cuadro).*
- **Intervalo de respuesta y umbral de permanencia:**
  - Latencia de actualización: Hasta **3 segundos** entre eventos de seguimiento (*"within 3 seconds interval"*, pág. 5).
  - Umbral de merodeo ($t_2$): **1 minuto (60 segundos)** de seguimiento ininterrumpido (*"if loiterer is tracked for more than one minute... $t_2$ is set to one minute"*, pág. 3).
- **Métricas no reportadas:** No reportan FLOPs, GFLOPs, parámetros ni consumo de memoria RAM o VRAM.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El sistema aplica YOLOv3 sobre la totalidad de la imagen a 3 escalas diferentes, lo cual explica el grave estrangulamiento de velocidad (<0.6 FPS). Como estrategia de ahorro, el clasificador Haar Cascade para reconocimiento facial no opera de forma continua sobre todo el fotograma, sino que se restringe estrictamente a la región delimitada por la caja delimitadora (*bounding box*) del sujeto una vez que este ha superado el minuto de permanencia. No obstante, el sistema carece de cercos virtuales o zonas de exclusión espacial, generando alertas de merodeo sobre cualquier transeúnte estacionario en la vía pública frente al domicilio vigilado.

---

### 3.4. Zhang et al. (2023)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Zhang, Y., Wang, J., Wang, X., Wang, Y., & Yu, S. (2023). *Research and Application of Loitering Detection Based on Deep Learning*. 2023 9th International Conference on Dependable Systems and Their Applications (DSA), IEEE, pp. 340–346. DOI: [10.1109/DSA59317.2023.00052](https://doi.org/10.1109/DSA59317.2023.00052).
- **Arquitectura propuesta:** Sistema JYLD estructurado sobre el detector YOLOA-S (backbone CSPDarkNeXt con convoluciones agrupadas $7 \times 7$ tipo ConvNeXt, módulo Focus y atención espacial/canal SAM y CAM), el rastreador JYTracker basado en la arquitectura Joint Detection and Embedding (JDE) con asociación de datos en cascada, y un módulo cinemático de reglas para detección de merodeo (tiempo de permanencia > 300 s, dispersión espacial y conteo de cambios angulares).

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Diseño arquitectónico y FPS en benchmark).
- **Justificación textual:** El costo computacional constituye el núcleo motivacional del artículo. En el resumen (página 340, columna 1), los autores advierten sobre la inviabilidad de los modelos profundos convencionales en entornos concurridos:
  > *"At present, the model of deep learning-based wandering detection algorithm is too complex and requires the support of devices with high computing power, otherwise it is difficult to be applied to scenes with dense pedestrians, so in-depth research on this problem is needed."*
  Para mitigar esta carga, introducen optimizaciones estructurales (página 341, columna 1):
  > *"ConvNeXt improves the training speed through fewer activation functions and normalization layers, and uses 7x7 convolution kernels to convolve in groups, reducing the amount of calculation."*
  > *"...replaces CSPDarkNet's subsampling through convolution with subsampling through Focus, and then uses 1x1 convolution to increase and decrease the dimension of the channel, which can reduce network parameters and increase inference speed."*
  En la Sección 3.6 (página 345), reconocen la necesidad de recurrir a técnicas de compresión para posibilitar el despliegue en hardware restringido:
  > *"In future research, JYLD can be popularized by means of a series of compression models such as knowledge distillation, making it smaller in size and able to be deployed on equipment with limited resources."*

#### Hardware Reportado
- **Dictamen:** No reporta.
- **Detalle:** El artículo no menciona CPU, GPU, memoria RAM ni servidor. La única mención técnica de aceleración corresponde al framework por software TensorRT en la página 345, columna 1:
  > *"JYLD operates in real time, processing at least 24 frames per second with the help of TensorRT."*
  No se especifican la versión de TensorRT, la precisión numérica empleada (FP32, FP16 o INT8) ni el hardware físico subyacente.

#### Métricas Cuantitativas Verbatim
- **Conteo de parámetros del detector (Tablas 1 a 4, página 342, resolución 640):**
  - `YOLOX-S` (línea base): 8.97 M
  - `YOLOA-S` (propuesto): **9.58 M**
- **Velocidad de procesamiento (FPS) de JYTracker en MOT20 (Tabla 6, página 345):**
  - Entrada $512 \times 928$: **20.5 FPS**
  - Entrada $608 \times 1088$: **19.4 FPS**
  - Entrada $736 \times 1280$: **11.5 FPS**
  - Entrada $800 \times 1440$: **10.8 FPS**
  *(Al pasar de resolución media a alta, la velocidad de procesamiento sufre una degradación del **47.32%**, cayendo a ~11 FPS).*
- **Rendimiento con TensorRT:** Al menos **24 FPS** (*"at least 24 frames per second with the help of TensorRT"*, pág. 345).
- **Métricas no reportadas:** No reportan latencias individuales por cuadro en milisegundos, operaciones FLOPs o GFLOPs, consumo de memoria VRAM ni tiempos de entrenamiento.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El flujo de video se transmite hacia la red troncal dividiéndose en cuatro escalas espaciales de submuestreo ($32\times$, $16\times$, $8\times$ y $4\times$, pág. 343). El sistema no cuenta con cercos virtuales dinámicos ni regiones de interés que acoten la inferencia visual. Como consecuencia directa, la carga computacional escala cuadráticamente con la resolución del sensor, obligando a los autores a recurrir a TensorRT para alcanzar el umbral de tiempo real y postulando la destilación de conocimiento como trabajo futuro.

---

### 3.5. Li & Huang (2024)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Li, H., & Huang, X. (2024). *Spatiotemporal heterogeneous information fusion model for loitering anomaly detection*. Signal, Image and Video Processing, 18(6), 5733–5742. https://doi.org/10.1007/s11760-024-03267-1
- **Arquitectura propuesta (Línea Base Principal del Proyecto ESPE):** Sistema de fusión de información heterogénea estructurado en: detector YOLOX, rastreador basado en ByteTrack con asociación en tres etapas mediante métrica HIoU, módulo de reevaluación de marcha (*gait reassessment module*) alimentado por siluetas monocanal de $64 \times 44$ píxeles procesadas por un backbone convolucional liviano tipo ResNet, y módulo cinemático de merodeo evaluado en el conjunto IITB-Corridor mediante dispersión espacial de coordenadas y ángulo de desviación de trayectoria $\le 135^\circ$.

#### Abordaje de Costo Computacional
- **Clasificación:** SÍ (Exhaustivo, cuantitativo y crítico).
- **Justificación textual:** Li y Huang (2024) abordan el balance entre precisión de seguimiento y costo computacional como un eje transversal. En la página 5738, justifican la selección del backbone de marcha comparando directamente su demanda de operaciones:
  > *"For the reassessment module, when the input silhouette size is 64 × 44, referring to Gaitbase [8], given the overall speed and computational cost of running the model (3.939 vs. 1.183 GFLOPs per silhouette image), we use a ResNet-like backbone network instead of the standard ResNet50 backbone, which requires 4.72M parameters."*
  En la Sección 4.3 (página 5739), analizan con rigor la penalización en FPS que introduce el módulo de marcha:
  > *"As for the running speed (FPS) of the model, Bytetrack, which is the baseline model of the tracker in this paper, obtains the fastest running speed due to its exclusion of the re-identification module. Although, in exchange for higher tracking accuracy, the model runs much slower after the introduction of the gait feature reassessment module. However, compared with BoT-SORT and StrongSORT... the running speed of the model in this paper is still more considerable... Firstly, the input to the gait feature network is a single-channel grey-scale image, which is less data-intensive than a traditional three-channel RGB image; Secondly, the ResNet-like backbone network used in the gait feature reassessment module is more lightweight..."*
  En la Sección 4.6 (página 5740), describen la gestión de sobrecarga en memoria activa:
  > *"Considering the computational cost and the overall running speed of the model, the gait feature information of the pedestrian’s previous track is retained for a certain period of time and then deleted."*
  Finalmente, en la Sección 4.8 (*Limitations*, página 5741), admiten de forma autocrítica:
  > *"Secondly, as the gait feature reassessment module is essentially a deep learning network-based re-identification task, as a typical two-stage tracker. It is computationally expensive when large images need to be processed, and has high hardware requirements on the running devices. As a result, it operates at relatively low speeds compared to joint trackers and several appearance-free trackers..."*

#### Hardware Reportado
- **Ubicación:** Página 5738, Sección 4.1 (*Datasets and parameter settings*), columna 1.
- **Cita verbatim:**
  > *"In this experiment, our GPU is NVIDIA GeForce RTX 3060 with 32GB memory. The software configuration includes Python 3.9, PyTorch 1.8.0, and CUDA 11.6."*
- **Especificaciones:** Tarjeta gráfica NVIDIA GeForce RTX 3060 con 32 GB de memoria (descripción que engloba la GPU y la memoria RAM principal del host). Procesador (CPU) no reportado por separado.

#### Métricas Cuantitativas Verbatim
- **Complejidad y parámetros del detector YOLOX (Página 5738):**
  - Parámetros: **25.3 M**
  - GFLOPs: **118.7 GFLOPs** (con resolución de entrada $1088 \times 608$).
- **Complejidad y parámetros del módulo de marcha (Página 5738):**
  - Parámetros: **4.72 M**
  - GFLOPs por silueta: **1.183 GFLOPs** (frente a 3.939 GFLOPs de ResNet50 GaitBase, reduciendo un 70.0% el cómputo).
- **Velocidad de procesamiento (FPS) en MOT17 (Tabla 1, página 5739):**
  - `Bytetrack` (baseline sin Re-ID): **29.6 FPS** (MOTA 76.7%, IDF1 79.3%)
  - `StrongSORT` (con ResNeSt50): **7.5 FPS** (MOTA 77.1%, IDF1 82.3%)
  - `BoT-SORT` (con ResNet50 y compensación de cámara): **4.5 FPS** (MOTA 78.5%, IDF1 82.1%)
  - **Ours (Propuesto)**: **10.1 FPS** (MOTA **78.0%**, IDF1 **83.2%**)
  *(La reevaluación de marcha incrementa la persistencia de identidad IDF1 en +3.9%, a costa de reducir la velocidad de procesamiento en un **65.88%**, pasando de 29.6 a 10.1 FPS).*
- **Exactitud en detección de merodeo en IITB-Corridor (Tabla 4, página 5741):**
  - Exactitud (ACC): **87.4%**; Recall: **90.0%**; Precision: **95.4%**. No reportan FPS ni latencia en ms en esta fase final.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
Li y Huang (2024) evalúan su sistema procesando la escena visual completa tanto en MOT17 como en el corredor de IITB. La segmentación de siluetas de marcha y la sustracción de fondo se aplican de manera global. Al carecer de cercos virtuales dinámicos que restrinjan la activación de la red de marcha únicamente a trayectorias que penetran zonas restringidas, el sistema debe extraer siluetas y recalcular descriptores para cada transeúnte en el encuadre, provocando la severa caída de rendimiento temporal hasta 10.1 FPS.

---

### 3.6. Waddenkery & Soma (2024)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Waddenkery, N., & Soma, S. (2024). *Loitering Based Human Crime Detection in Video Surveillance using Beluga Whale Adam Dingo Optimizer and Deep Convolutional Neural Network*. The International Arab Journal of Information Technology (IAJIT), 21(3), 351–368. DOI: [10.34028/iajit/21/3/1](https://doi.org/10.34028/iajit/21/3/1).
- **Arquitectura propuesta:** Extracción de fotogramas del conjunto de datos UCF Crime submuestreados cada 10 cuadros y reescalados a $64 \times 64$ píxeles, seguimiento de personas mediante Deep SORT con alineación cuadrática espacial (SQA), y clasificación de delitos asociados al merodeo mediante una red neuronal convolucional profunda (DCNN) optimizada por el algoritmo bioinspirado híbrido Beluga Whale Adam Dingo Optimizer (BWADO).

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Complejidad teórica de la metaheurística y tiempo empírico aislado).
- **Justificación textual:** En la Sección 3.4 (página 360), los autores deducen analíticamente la complejidad computacional del algoritmo de optimización BWADO en función del número de ballenas ($n$) y las iteraciones máximas ($t_{\max}$):
  $$\mathcal{C}\left(n \times 0.1 \times t_{\max\text{-BWOA}} + f(t_{\max\text{-ADOA}})\right)$$
  Posteriormente, en la Tabla 5 y Figura 13 (página 364), reportan una métrica de tiempo de procesamiento de 1.78 segundos para comparar su eficiencia frente a tres métodos de la literatura:
  > *"The assessment of processing times for various techniques, as depicted in Figure 13 and Table 5, sheds light on the efficiency disparities among these methods. Notably, the introduced technique emerges as the most time-efficient, completing the task in a mere 1.78 seconds. Comparatively, ASGCM, NIQMC and BIQME exhibit processing times of 3.96 seconds, 3.81 seconds and 3.81 seconds, respectively..."*
  No obstante, los autores no aclaran a qué unidad muestral corresponde dicho tiempo (si es por imagen de $64 \times 64$, por lote de 10 cuadros o por clip de video). Asimismo, en las conclusiones (página 366), admiten explícitamente que la operación en tiempo real no fue alcanzada:
  > *"The future scope of this research entails real-time optimization of the LHCD module for swift response in live surveillance scenarios..."*

#### Hardware Reportado
- **Dictamen:** No reporta.
- **Detalle verbatim:** El artículo omite cualquier referencia a CPU, GPU, núcleos CUDA, memoria RAM o sistema operativo. La única mención al entorno figura en la Sección 4 (página 360, columna 1):
  > *"The implementation is done in python."*
  No se especifican bibliotecas de Deep Learning (sin menciones a PyTorch ni TensorFlow).

#### Métricas Cuantitativas Verbatim
- **Tiempo de procesamiento (Tabla 5, página 364):**
  - ASGCM: 3.96 s
  - NIQMC y BIQME: 3.81 s
  - AD-Graph: 2.97 s
  - **Introduced (Propuesto): 1.78 s**
- **Hiperparámetros de entrenamiento (Tablas 2 y 3, página 360):**
  - Batch size = 8; Épocas = 100; Tasa de aprendizaje = 0.001; Tamaño de población = 50; Iteraciones totales = 1000.
- **Métricas no reportadas:** Cero menciones de FPS (Frames Per Second), latencia por cuadro en milisegundos, FLOPs o GFLOPs, conteo de parámetros de la DCNN y uso de memoria RAM o VRAM.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El método se entrena y valida sobre recortes de imágenes estáticas de $64 \times 64$ píxeles extraídas a saltos de 10 fotogramas. No opera sobre secuencias de video continuas ni implementa cercos virtuales dinámicos. Su altísima exactitud reportada (99.76% de exactitud y 99.89% de F1-score) carece de viabilidad para vigilancia en vivo, como los propios autores reconocen al postergar la optimización en tiempo real para trabajos futuros.

---

### 3.7. Yang et al. (2024)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Yang, X., Li, J. Q., Zhan, Y., & Yu, W. (2024). *Real-time automated deep learning based railroad trespassing violation detection and tracking at highway-rail grade crossing*. Intelligent Transportation Infrastructure, 2024, liae003, pp. 1–10. DOI: [10.1093/iti/liae003](https://doi.org/10.1093/iti/liae003).
- **Arquitectura propuesta:** Marco de detección y seguimiento de intrusiones en cruces de ferrocarril estructurado en dos etapas: Etapa 1 mediante filtrado de color HSV ligero con salto de 15 fotogramas para detectar la activación de la luz intermitente de advertencia; Etapa 2 mediante YOLOv4 (backbone CSPDarknet53) y Deep SORT con filtro de baja confianza para seguimiento cuadro a cuadro de peatones dentro de cuatro zonas poligonales estáticas predefinidas.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Throughput empírico en video de campo).
- **Justificación textual:** Yang et al. (2024) no realizan un estudio formal de complejidad teórica, consumo de memoria ni FLOPs. En su lugar, evalúan exhaustivamente la velocidad de procesamiento en cuadros por segundo (FPS) en un conjunto de prueba masivo de 104 horas de video continuo (26 sesiones de observación de 4 horas cada una). En el resumen (página 1) y Sección 6 (página 6) destacan:
  > *"The automated trespassing violation detection speed ranged from 43.2 to 654.5 frames per second (FPS), exceeding the field video data recording rate at 30 FPS."*
  La enorme fluctuación de velocidad (desde 43.2 hasta 654.5 FPS) se debe al diseño en cascada explicado en la Sección 5.1 (páginas 2–3):
  > *"Firstly, the flashing light signal should be checked with a video feed. If a flashing light signal is detected, the algorithm will enter Stage 2 to perform a frame-by-frame trespassing violation detection and tracking using YOLOv4 and Deep SORT... If the flashing light signal is not detected, the algorithm will remain in Stage 1... In other words, if the flashing light signal is off, the methodology will not perform the trespassing detection and tracking task for that video frame, which will significantly reduce the amount of time required..."*
  Además, en la Etapa 1 implementan salto de cuadros (página 4):
  > *"Skip 15 frames and repeat Steps 1 to 5 for a second round of signal light detection..."*

#### Hardware Reportado
- **Dictamen:** No reporta.
- **Detalle:** Ausencia absoluta de información sobre procesador (CPU), tarjeta gráfica (GPU), memoria RAM, servidor o framework (sin menciones de PyTorch, TensorFlow o CUDA). Se desconoce la máquina sobre la cual se registraron las velocidades de 43 a 654 FPS.

#### Métricas Cuantitativas Verbatim
- **Rango global de velocidad (FPS):** **43.2 a 654.5 FPS** (frente a los 30 FPS de la tasa de grabación del video en campo).
- **Detalle de las 26 sesiones evaluadas en la Tabla 1 (página 7, Columna 5):**
  - Mínimo registrado: **43.2 FPS** (31 de enero de 2023, 12:00 pm–4:00 pm, con 13 señales activas, 12 trenes y 48 violaciones simultáneas).
  - Máximo registrado: **654.5 FPS** (31 de enero de 2023, 8:00 am–12:00 pm, con solo 2 señales y 4 violaciones, dominada por la Etapa 1 en reposo).
  - Sesiones representativas intermedias: 57.6, 67.9, 70.6, 72.0, 77.4, 83.7, 96.0, 120.0, 141.2, 171.4, 205.0 FPS.
- **Parámetros del detector (Página 4, Sección 5.3.1):** Citan la cifra teórica de **27.6 millones de parámetros** para el backbone CSPDarknet53.
- **Métricas no reportadas:** No reportan latencia en milisegundos desglosada por componente, FLOPs o GFLOPs, ni uso de memoria RAM o VRAM.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El sistema delimita cuatro zonas poligonales estáticas fijadas sobre la calzada ferroviaria (Figura 6, pág. 5). Sin embargo, una vez que la luz de advertencia se activa, YOLOv4 procesa el fotograma completo de manera continua. La tasa de 43.2 FPS observada en periodos de congestión demuestra el costo de ejecutar YOLOv4 y Deep SORT sobre todo el cuadro. Las zonas poligonales son estáticas y rígidas; no permiten al usuario reajustar dinámicamente los límites del área durante la operación ni acotan la inferencia neuronal a la región de interés antes de la detección.

---

### 3.8. Thosar et al. (2025)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Thosar, D., Thosar, R., Sharma, L., Chanore, M., Belkhede, P., & Pohanerkar, S. (2025). *SmartSurveil: AI-based Intrusion and Suspicious Behavior Detection in CCTV*. 2025 3rd DMIHER International Conference on Artificial Intelligence in Healthcare, Education and Industry (IDICAIHEI), IEEE. DOI: [10.1109/IDICAIHEI65991.2025.11379088](https://doi.org/10.1109/IDICAIHEI65991.2025.11379088).
- **Arquitectura propuesta:** Marco conceptual inteligente denominado SmartSurveil estructurado en cuatro módulos: detección de intrusión mediante YOLOv8, detección de rostros cubiertos, detección de sabotaje de cámara, y análisis de comportamiento sospechoso (merodeo y aceleración repentina) mediante flujo óptico y movimiento.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Conceptual y latencias esperadas de diseño).
- **Justificación textual:** En la Sección VI (*Limitations*, página 5), los autores identifican cualitativamente la sobrecarga computacional de las redes profundas como una limitación crítica:
  > *"Deep getting to know fashions like YOLOv8 and facial evaluation frameworks demand excessive GPU processing power, making real-time analysis challenging on low-cease or part gadgets."*
  Asimismo, en la Sección VII (*Future Scope*, página 5), proponen la migración a dispositivos de borde:
  > *"Edge AI Deployment: Implementing lightweight models for real-time inference on edge devices, reducing dependency on high-end servers."*
  Sin embargo, en la Sección VI (*Result & Discussions*, página 4), declaran explícitamente que el sistema se encuentra en fase de desarrollo y que los resultados presentados no son mediciones físicas reales:
  > *"Although implementation is in progress, the system is expected to achieve the following outcomes:"*

#### Hardware Reportado
- **Dictamen:** No reporta.
- **Detalle:** El artículo no describe CPU, modelo de GPU, memoria RAM ni dispositivos de borde. Únicamente alude a servidores de alta gama (*high-end servers*) y cámaras genéricas de CCTV o webcams sin especificación técnica.

#### Métricas Cuantitativas Verbatim
- **Latencias de procesamiento esperadas (Tabla 1 y Figura 2, página 4):**
  - Módulo de detección de intrusión (YOLOv8): **45 ms** (Accuracy: 94.5%)
  - Módulo de detección de ocultación facial: **50 ms** (Accuracy: 92.1%)
  - Módulo de detección de sabotaje de cámara: **40 ms** (Accuracy: 90.3%)
  - **Módulo de análisis de comportamiento sospechoso (merodeo): 55 ms** (Accuracy: 88.4%)
  - **Sistema completo integrado (Overall System): 48 ms** (Accuracy: 91.3%)
- **Tasa de fotogramas (FPS):** No reporta mediciones de FPS para SmartSurveil. La cifra de **65 FPS** mencionada en la Sección II (página 2) corresponde a una cita textual del artículo de YOLOv4 publicado por Bochkovskiy et al. (2020) sobre el conjunto de datos COCO.
- **Métricas no reportadas:** No reportan FLOPs, consumo de VRAM en megabytes, uso de CPU ni tiempos empíricos de entrenamiento.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
SmartSurveil está planteado como un sistema que procesa el flujo de video completo sin acotación espacial adaptativa. Al no contar con cercos virtuales dinámicos definidos por el operador, todas las ramas analíticas (YOLOv8, rostro, flujo óptico) se proyectan sobre el encuadre global, lo cual justifica la preocupación de los autores sobre la excesiva demanda de procesamiento en GPU y la necesidad de servidores robustos.

---

### 3.9. Jeoung et al. (2026)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Jeoung, J., Lee, S., & Hong, T. (2026). *Automatic discovery of semantic ROIs for vision-based occupancy analysis in corridors*. Building and Environment, 298, 114656. https://doi.org/10.1016/j.buildenv.2026.114656
- **Arquitectura propuesta:** Marco no supervisado de tres etapas para la autocalibración espacial en edificios inteligentes: Etapa 1 con detección de peatones mediante YOLO11m y seguimiento con BoT-SORT y descriptores OSNet; Etapa 2 con extracción y filtrado de anomalías cinemáticas de trayectorias mediante Isolation Forest; Etapa 3 con descubrimiento automático de regiones de interés semánticas mediante modelos de mixturas gaussianas (GMM), polígonos envolventes convexos (Quickhull) y teselación de Voronoi.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Hardware detallado y motivación cualitativa sin métricas de cómputo).
- **Justificación textual:** Los autores justifican la selección de la arquitectura neuronal en función del rendimiento y velocidad en la Sección 3.1 (página 5, columna 1):
  > *"In this study, a YOLO-based object detector was adopted considering the optimal balance between real-time processing speed and detection accuracy [34]. In particular, YOLO11m, with a medium-sized architecture, was selected to ensure high throughput and robust detection performance."*
  Asimismo, en la Sección 7 (*Conclusion*, página 15), aluden a la convergencia operativa:
  > *"...converging to operational-level accuracy with only approximately 150 trajectories. This implies that the system can rapidly self-calibrate in new environments with minimal latency."*
  No obstante, esta "latencia mínima" se refiere al tiempo requerido para acumular unas 150 trayectorias de transeúntes y autocalibrar el sistema sin intervención humana, y no a la latencia computacional por cuadro. Los autores no midieron el tiempo de inferencia ni los FPS del pipeline.

#### Hardware Reportado
- **Ubicación:** Página 8, Sección 4.3 (*Implementation details*), columna izquierda, líneas 1–7.
- **Cita verbatim:**
  > *"All experiments were conducted on a computing system equipped with an Intel Core i7–12700KF CPU, 32 GB RAM, and an NVIDIA GeForce RTX 3060 GPU. For the software environment, Python 3.11.13 was utilized, with the PyTorch library employed for deep learning operations."*
- **Especificaciones:** Procesador Intel Core i7-12700KF, 32 GB de memoria RAM, tarjeta gráfica NVIDIA GeForce RTX 3060, entorno Python 3.11.13, PyTorch, scikit-learn y scipy.

#### Métricas Cuantitativas Verbatim
- **Rendimiento de detección y seguimiento (Tablas 2 y 3, página 10):**
  - YOLO11m: Precision = 0.981, Recall = 0.935, F1-score = 0.956 (promedios macro sobre 14 escenas de prueba).
  - BoT-SORT: IDF1 = 0.919, MOTA = 0.943.
- **Exactitud de asignación de eventos GMM (Páginas 11–12 y Tabla 4):** Exactitud superior al 93% (Camera A = 0.946, Camera B = 0.938), superando el promedio de anotadores humanos (0.633 a 0.744). Convergencia alcanzada tras acumular ~150 trayectorias (Figura 12).
- **Aclaración sobre la sigla "fps" (Página 7, Sección 4.1):** El valor de **23 fps** que figura en el texto (*"recorded for 320 s at 23 frames per second (fps), resulting in a total of 7360 frames"*) corresponde estrictamente a la tasa de grabación del video original del conjunto AI-HUB a resolución $1920 \times 1080$, y no a la velocidad de inferencia de los algoritmos.
- **Métricas computacionales no reportadas:** No reportan FPS de inferencia, latencia por cuadro en milisegundos, tiempo de cómputo del agrupamiento GMM/Voronoi, FLOPs ni consumo dinámico de VRAM.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
La propuesta de Jeoung et al. (2026) aporta una contribución geométrica fundamental al automatizar el descubrimiento de ROIs mediante agrupamiento no supervisado, resolviendo el problema de la dependencia de configuraciones humanas arbitrarias. Sin embargo, en la fase operativa de detección (Etapa 1), YOLO11m procesa la totalidad del cuadro de alta definición ($1920 \times 1080$). La delimitación espacial ocurre de forma diferida post-rastreo, por lo que el sistema no explota los ROIs descubiertos como cercos de activación temprana para reducir la carga de inferencia profunda.

---

### 3.10. Jiménez-Frías et al. (2026)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Jiménez-Frías, P., Salcedo-Delgado, C., & Carlos-Hernández, S. (2026). *Improving the Automatic Counting in a Region of Interest in Videos of Urban Traffic Taken by Drones Using Video Stabilization*. Computación y Sistemas, 30(1), 131–142. DOI: [10.13053/CyS-30-1-6328](https://doi.org/10.13053/CyS-30-1-6328).
- **Arquitectura propuesta:** Tubería de visión artificial para conteo vehicular y peatonal en intersecciones urbanas mediante drones en vuelo estacionario a resolución 4K ($3840 \times 2160$ píxeles), integrada por cuatro módulos: Módulo 1 de estabilización de video basado en puntos característicos Shi-Tomasi, flujo óptico piramidal Lucas-Kanade y estimación de homografías mediante RANSAC y Levenberg-Marquardt (método CP); Módulo 2 de detección con YOLOv4; Módulo 3 de rastreo temporal basado en métrica de asociación IoU; y Módulo 4 de conteo en una región de interés fija.

#### Abordaje de Costo Computacional
- **Clasificación:** Parcial (Evaluación exhaustiva de tiempos en el módulo de estabilización).
- **Justificación textual:** Jiménez-Frías et al. (2026) dedican la Sección 4.1.1 y la Tabla 1 (página 137) a comparar experimentalmente los tiempos de ejecución cronometrados de tres métodos de estabilización sobre un video de 9,613 fotogramas a resolución 4K. En la Sección 4.1.3, justifican la selección del método CP en función de su eficiencia temporal frente a métodos iterativos globales:
  > *"Indeed, while CP provides slightly better visual results than ECC (Version 1), its execution time is much shorter. The latter may be due to: (i) ECC requires all the points of the image, whereas CP only requires a subset of them. (ii) ECC relies on an optimization problem whose solution is obtained from an iterative scheme. Hence, we have chosen the CP method as the stabilization module of our counting system."*
  No obstante, el estudio omite los tiempos de inferencia del detector YOLOv4, del rastreador IoU y la latencia global de extremo a extremo.

#### Hardware Reportado
- **Dictamen:** No reporta hardware específico.
- **Detalle verbatim:** El cuerpo del texto no especifica CPU, GPU, memoria RAM ni modelo de dron. En los agradecimientos (página 141), se menciona:
  > *"The authors acknowledge support from the Supercomputing Center of CIMAT-Mérida “TOOLOK”. The second author acknowledges the “Investigadoras e Investigadores por Mexico” SECIHTI program."*
  No se especifican los nodos, aceleradores ni configuración de ejecución en TOOLOK.

#### Métricas Cuantitativas Verbatim
- **Estadísticas de tiempo de ejecución por homografía en video 0362 (Tabla 1, página 137):**
  - Método CP (Puntos Característicos): Media = **0.3056 s** (Desviación: 0.0873 s; Mínimo: 0.0899 s; Mediana: 0.3194 s; Máximo: 0.3889 s).
  - Método ECC Versión 1: Media = **1.7127 s** (Desviación: 0.5776 s; Máximo: 5.4331 s).
  - Método ECC Versión 2: Media = **2.1237 s** (Desviación: 0.4205 s; Máximo: 3.3213 s).
- **Tiempo total acumulado para estabilizar el video 0362 (9,613 cuadros a 4K, pág. 137):**
  - CP: **41 minutos y 35 segundos** ($\approx 2495\text{ s}$).
  - ECC Versión 1: **3 horas, 30 minutos y 2 segundos**.
  - ECC Versión 2: **4 horas, 1 minuto y 32 segundos**.
- **Tasa de fotogramas derivada:**
  - Tasa instantánea de estabilización: $\frac{1}{0.3056\text{ s}} \approx \mathbf{3.27\text{ FPS}}$.
  - Throughput de estabilización sobre el lote completo: $\frac{9613\text{ cuadros}}{2495\text{ s}} \approx \mathbf{3.85\text{ FPS}}$.
- **Estrategia de submuestreo temporal ($j$):** En las Tablas 3 y 4 (páginas 138–139), evalúan factores de salto de cuadros $j=1, 2, 3, 4, 5$. El mejor rendimiento se logra con $j=4$ (precisión de 76.76% con estabilización frente a 74.37% sin ella), reduciendo la carga de cómputo en un 75% al procesar únicamente 1 de cada 4 fotogramas.
- **Métricas no reportadas:** No reportan tiempos de inferencia de YOLOv4, latencia end-to-end, FLOPs ni consumo de memoria VRAM.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El módulo de estabilización debe procesar el cuadro completo a resolución 4K ($3840 \times 2160$) para rastrear los 1000 puntos Shi-Tomasi y compensar la deriva espacial provocada por el viento. Aunque el conteo final se realiza dentro de un ROI delimitado en la intersección, el detector YOLOv4 opera sobre la imagen completa estabilizada. La estabilización por sí sola introduce un cuello de botella de ~3.27 FPS, confirmando que el procesamiento en ultra alta definición sin filtrado espacial temprano es prohibitivo para aplicaciones en tiempo real estricto.

---

### 3.11. Vu et al. (2026)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Vu, T. C., Nguyen, D. T., Dinh, L. Q., Nguyen, M. D., Setiadi, D. R. I. M., & Nguyen, M. T. (2026). *Deep-Learning-Based Multi-Camera Framework for Indoor Human Detection and Presence Management*. Future Internet, 18(8), 435. MDPI. https://doi.org/10.3390/fi18080435
- **Arquitectura propuesta:** Framework centralizado multicámara para interiores estructurado en tres componentes: detección de personas con YOLOv11n y seguimiento temporal con DeepSORT; detección facial con SCRFD 2.5G y re-identificación biométrica mediante ArcFace R100 (imágenes normalizadas a $112 \times 112$ píxeles); y gestión de eventos espacio-temporales mediante polígonos virtuales y límites configurables para conteo y detección de intrusiones en áreas restringidas.

#### Abordaje de Costo Computacional
- **Clasificación:** SÍ (Exhaustivo, cuantitativo y con análisis de concurrencia).
- **Justificación textual:** El artículo dedica tablas comparativas y extensas secciones al análisis de sobrecarga computacional bajo escenarios de múltiples flujos de video RTSP concurrentes. En el resumen (página 1) reportan:
  > *"YOLOv11n is integrated with DeepSORT to detect and continuously track individuals within the monitored area. Experimental results showed the system achieving an average processing performance of 10.6 FPS, demonstrating the feasibility of the proposed architecture for small- to medium-scale indoor surveillance applications."*
  En la Tabla 2 (página 7), contrastan las ventajas y limitaciones de arquitecturas centralizadas frente a dispositivos de borde. En la Sección 4.5 (página 19), analizan los límites de escalabilidad:
  > *"Regarding the limitations of the proposed system framework, the centralized processing of multiple RTSP streams creates significant computational and storage demands, especially for long-term video storage and simultaneous multi-camera analysis. Therefore, runtime performance depends on the available hardware resources, especially the CPU, GPU, and memory capacity. As the number of cameras processed simultaneously increases, the trade-offs between inference throughput, tracking consistency, and processing latency become more apparent, especially under high-resolution multi-stream conditions."*

#### Hardware Reportado
- **Ubicación:** Página 12, Sección 4 (*Experimental Setup and Evaluation*), líneas del primer párrafo.
- **Cita verbatim:**
  > *"Experiments were conducted on a hardware platform equipped with an Intel Xeon E5-2696 v3 CPU, NVIDIA Quadro P5000 GPU (16 GB VRAM), 64 GB RAM, and running Windows 10. The system used the YOLOv11n, SCRFD 2.5G, and ArcFace R100 pre-training models. The DeepSORT module used the default parameters of the original implementation. The input images for the face recognition module were normalized to 112 × 112 pixels. Inference was performed online in CUDA mode with a batch size of 1. TensorRT and the FP16 inference method were not used, so the reported performance reflects the proposed framework under a standard deployment configuration. In the experiments, the number of concurrent RTSP threads was configured from 3 to 6 depending on the evaluation scenario."*

#### Métricas Cuantitativas Verbatim
- **Rendimiento global del sistema propuesto (`YOLOv11n + DeepSORT`):** **10.6 FPS** promedio end-to-end (incluyendo captura de video, detección, rastreo, asociación de identidad, eventos y registro concurrente).
- **Comparativa de detección y rastreo de personas (Tabla 7 y Sección 4.3, páginas 16–17):**
  - `YOLOv11n + ByteTrack`: **19.7 Avg FPS** (Recomendado para alta velocidad y monitoreo multiflujo).
  - `YOLOv11n + OC-SORT`: **16.9 Avg FPS** (Balance entre velocidad y estabilidad).
  - `YOLOv11n + DeepSORT` (propuesto): **10.6 Avg FPS** (mAP@0.5 de 0.66, estabilidad ante oclusiones a cambio de menor velocidad).
  - `YOLOv8 + DeepSORT`: **18.9 Avg FPS** (mAP@0.5 de 0.61).
- **Comparativa de módulos de detección facial (Tabla 5, página 15):**
  - `RetinaFace + ArcFace`: **11.8 Avg FPS**
  - `SCRFD 2.5G + ArcFace` (propuesto): **19.2 Avg FPS** (Balance óptimo de eficiencia y exactitud).
- **Concurrencia evaluada:** 3 a 6 flujos RTSP simultáneos en el servidor central.
- **Métricas no reportadas:** No desglosan latencias individuales por módulo en milisegundos, no reportan GFLOPs ni conteo de parámetros, ni consumo de VRAM en megabytes.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
Vu et al. (2026) introducen polígonos virtuales poligonales configurables por el usuario para detectar eventos de entrada/salida y merodeo en áreas restringidas (pág. 16, Figura 9 y 10). Sin embargo, el procesamiento visual de YOLOv11n y DeepSORT se ejecuta de forma ininterrumpida sobre el fotograma completo de cada cámara. Los polígonos actúan únicamente como un filtro de validación cinemática *post-tracking*. La sobrecarga de procesar cuadros completos concurrentes limita el throughput a 10.6 FPS, obligando a los autores a postular estrategias de balanceo de carga distribuida en sus conclusiones.

---

### 3.12. Lee & Park (2026)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Lee, Y. H., & Park, M. (2026). *A Real-Time Pedestrian Situation Detection Method Using CNN and DeepSORT with Rule-Based Analysis for Autonomous Mobility*. Electronics, 15(3), 532. https://doi.org/10.3390/electronics15030532
- **Arquitectura propuesta:** Sistema modular montado en robot móvil autónomo estructurado en: detector YOLOv12-m fine-tuneado para extracción de personas y posturas; rastreador temporal DeepSORT con filtro de Kalman para asociación entre cuadros; y motor determinista de reglas lógicas para clasificación de situaciones peatonales individuales (caminar, correr, merodeo) y colectivas (cruce, agrupamiento).

#### Abordaje de Costo Computacional
- **Clasificación:** SÍ (Exhaustivo, cuantitativo y validado en plataforma móvil).
- **Justificación textual:** Lee y Park (2026) justifican su diseño criticando explícitamente la inviabilidad de los modelos profundos de extremo a extremo para plataformas con recursos limitados (página 2):
  > *"Moreover, learning-based behavior recognition models typically incur high computational complexity, which limits their suitability for real-time deployment on resource-constrained mobile platforms. These limitations highlight the need for a lightweight and efficient pedestrian situation awareness framework capable of operating in real time."*
  Para demostrarlo, miden empíricamente la latencia por componente en la Tabla 4 (página 14):
  > *"The proposed system achieves an average execution time of 58.11 ms, enabling a real-time operational speed of 17.2 fps. The detailed breakdown of processing times for individual modules is summarized in Table 4. A dataset comprising 1570 frames was utilized to rigorously evaluate the overall runtime efficiency."*
  En la Sección 4.2 (página 18), contrastan su motor de reglas frente a una red recurrente profunda (ResNet + LSTM):
  > *"In contrast, the proposed rule-based analysis achieves an execution time of only 12.43 ms, demonstrating its suitability for real-time applications. These results indicate that, while the rule-based approach is highly efficient for real-time deployment, the ResNet + LSTM-based method is less practical for time-critical scenarios due to its substantial initial delay and computational overhead."*

#### Hardware Reportado
- **Ubicación:** Página 13, Sección 4.1 (*Experimental Environment*), líneas 10–16.
- **Cita verbatim:**
  > *"To conduct the experiments, an environment was established using an autonomous multi-purpose mobility robot, the IVIS TARO (IVIS Corp., Suwon-si, Republic of Korea), to facilitate data acquisition. The robot was equipped with a forward-facing Intel RealSense camera (Intel Corporation, Santa Clara, CA, USA), capturing video at a resolution of 640 × 480 pixels. Computational tasks were performed on an NUC 11 Enthusiast system (Intel Corporation, Santa Clara, CA, USA), featuring an Intel i7-1165G7 processor, an NVIDIA GeForce RTX 2060 GPU, and 32 GB of RAM."*
- **Especificaciones:** Sistema compacto Intel NUC 11 Enthusiast, CPU Intel Core i7-1165G7 (4 núcleos / 8 hilos), GPU NVIDIA GeForce RTX 2060 móvil (6 GB GDDR6), 32 GB RAM, sensor Intel RealSense ($640 \times 480$), resolución de entrada a la red de $640 \times 640$ píxeles.

#### Métricas Cuantitativas Verbatim
- **Rendimiento temporal global:** **58.11 ms por cuadro**, equivalente a **17.2 FPS** (evaluado en 1570 cuadros continuos).
- **Desglose de latencia por módulo (Tabla 4, página 14):**
  - Módulo de Detección y Clasificación (YOLOv12-m): **34.54 ms** (**59.44%** del tiempo total). Cuello de botella principal.
  - Módulo de Rastreo Temporal (DeepSORT): **11.14 ms** (**19.17%** del tiempo total).
  - Módulo de Detección de Situaciones (Reglas lógicas): **12.43 ms** (**21.39%** del tiempo total).
  - **Latencia total acumulada:** **58.11 ms**.
- **Comparativa contra red profunda temporal (Tabla 9, página 18):**
  - Módulo de reglas propuesto: **12.43 ms** de inferencia, 0 ms de retraso de búfer inicial.
  - Alternativa ResNet + LSTM: **66.8 ms** de inferencia por cuadro (+437% más lento), requiriendo acumular una ventana de 16 cuadros que introduce un retraso inicial de **528 ms**.
- **Métricas no reportadas:** No cuantifican operaciones FLOPs o GFLOPs, conteo exacto de parámetros de YOLOv12-m, consumo dinámico de VRAM en megabytes ni consumo eléctrico en Watts.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
El sistema procesa la totalidad del cuadro capturado por la cámara RealSense ($640 \times 480$) en cada fotograma. Aunque el módulo de situaciones define un ROI post-detección para evaluar la proximidad de los peatones respecto a la trayectoria del robot, la inferencia profunda de YOLOv12-m se ejecuta de manera ininterrumpida sobre todo el campo visual. Los autores identifican a YOLOv12-m como el cuello de botella computacional dominante (consumiendo el 59.4% del presupuesto temporal con 34.54 ms), evidenciando que acotar espacialmente la detección neuronal mediante un cerco virtual previo reduciría drásticamente la latencia en plataformas autónomas.

---

### 3.13. Zhao et al. (2025)

#### Metadatos Bibliográficos y Arquitectura
- **Referencia formal:** Zhao, A., Zhao, Y., & Zheng, Q. (2025). *Robust Pedestrian Detection and Intrusion Judgment in Coal Yard Hazard Areas via 3D LiDAR-Based Deep Learning*. Sensors, 25(18), 5908. https://doi.org/10.3390/s25185908
- **Arquitectura propuesta:** Red neuronal EFT-RCNN para detección de peatones en nubes de puntos 3D de LiDAR (integrando codificador EnhancedVFE, backbone 3D FocalConv y capa TeBEVPooling sobre la línea base Voxel-RCNN), combinada con un algoritmo jerárquico de juicio de intrusión punto-polígono en proyección cenital 2D (Bird's Eye View, BEV) mediante ray-casting y distancias euclidianas para zonas de peligro en patios de carbón.

#### Abordaje de Costo Computacional
- **Clasificación:** SÍ (Exhaustivo, con benchmark sintético, despliegue físico y estudio de ablación).
- **Justificación textual:** Zhao et al. (2025) formalizan matemáticamente la velocidad de procesamiento en la Ecuación 18 (página 13):
  $$\text{FPS} = \frac{1}{T_{\text{pre}} + T_{\text{inf}} + T_{\text{post}}}$$
  Donde descomponen el tiempo de preprocesamiento ($T_{\text{pre}}$), inferencia neuronal ($T_{\text{inf}}$) y postprocesamiento ($T_{\text{post}}$). Asimismo, en la Tabla 2 (página 14), realizan un estudio de ablación para cuantificar el costo en FPS de cada innovación propuesta:
  > *"However, while improving the detection accuracy, all three improvements have a negative impact on the computational efficiency, especially Improvement 2, which is caused by the complex network structure of FocalConv."*
  En la Sección 3.2.2 (página 18), evalúan la degradación temporal provocada por el middleware en despliegue real:
  > *"This efficiency difference stems primarily from the fact that the actual deployed system needs to receive the original point cloud data stream from the LiDAR in real-time through the CPU, and execute the complete early-warning workflow simultaneously."*
  Finalmente, en la Sección 4 (página 21), proponen soluciones de optimización industrial:
  > *"Downsampling the input point cloud data stream and using tools such as TensorRT to accelerate model inference can be adopted. Finally, the algorithm can be deployed on the NVIDIA Jetson series to evaluate its real-time performance under resource-constrained conditions..."*

#### Hardware Reportado
- **Doble plataforma de cómputo especificada:**
  1. **Plataforma de entrenamiento y benchmark sintético (Página 12, Sección 3.1.2):** Sistema Linux de 64 bits (Ubuntu 22.04), procesador Intel Xeon Gold 6248R, tarjeta gráfica NVIDIA H800 (single GPU), CUDA 11.8, PyTorch 2.1 y spconv 2.3.6.
  2. **Plataforma de despliegue en campo y pruebas en vivo (Páginas 16–17, Sección 3.2.1):** Computadora portátil con procesador 13th Gen Intel Core i9-13900HX (2.20 GHz), tarjeta gráfica NVIDIA GeForce RTX 4060 Laptop GPU (8 GB VRAM), 32 GB de memoria RAM, ejecutando ROS Noetic bajo Ubuntu 20.04.
  3. **Sensor físico de captura:** Sensor LiDAR mecánico Hesai Pandar QT128 (128 canales, 864,000 puntos/segundo, campo de visión $360^\circ \times 105^\circ$, resolución angular $0.4^\circ \times 0.4^\circ$, alcance de 20 m).

#### Métricas Cuantitativas Verbatim
- **Rendimiento en el benchmark público KITTI en GPU NVIDIA H800 (Tabla 1, página 14):**
  - `PointPillars`: 58.14 FPS (3D AP: 55.58%)
  - `Voxel-RCNN` (línea base): 55.87 FPS (3D AP: 60.54%)
  - `PillarNet`: 55.56 FPS (3D AP: 57.29%)
  - `SECOND`: 36.10 FPS (3D AP: 57.87%)
  - `Part-A2`: 35.46 FPS (3D AP: 62.67%)
  - `PV-RCNN`: 29.24 FPS (3D AP: 61.50%)
  - **EFT-RCNN (Propuesto)**: **28.56 FPS** (3D AP: **64.93%**, BEV AP: **66.87%**)
  - `HINTED`: 18.05 FPS (3D AP: 62.10%)
  - `PDV`: 16.18 FPS (3D AP: 64.59%)
- **Estudio de ablación de sobrecarga temporal en KITTI (Tabla 2, página 14):**
  - Línea base Voxel-RCNN: **55.87 FPS**
  - Con EnhancedVFE: **34.48 FPS** (Penalización de -21.39 FPS, -38.3%)
  - Con 3D FocalConv: **30.58 FPS** (Penalización de -25.29 FPS, -45.3%)
  - Con TeBEVPooling: **44.84 FPS** (Penalización de -11.03 FPS, -19.7%)
  - **EFT-RCNN Completo**: **28.56 FPS** (Penalización acumulada de **-27.31 FPS**, **-48.9%** respecto a la línea base).
- **Rendimiento en despliegue físico real bajo ROS en patio de carbón (Tabla 4, página 18):**
  - Escenario A (1 persona): **7.42 FPS** (Precisión: 97.0%)
  - Escenario B (2 personas, oclusión leve): **7.13 FPS** (Precisión: 92.1%)
  - Escenario C (3 personas, oclusión severa): **7.36 FPS** (Precisión: 89.6%)
  - **Promedio en despliegue real**: **7.30 FPS** (Precisión global: **92.9%**).
  *(En despliegue físico sobre la RTX 4060 con ROS y sensor QT128 en vivo, la velocidad se desploma desde los 28.56 FPS de laboratorio hasta 7.30 FPS).*
- **Métricas no reportadas:** No reportan latencias individuales en milisegundos para $T_{\text{pre}}$, $T_{\text{inf}}$ y $T_{\text{post}}$, conteo de parámetros ni consumo de VRAM en megabytes.

#### Manejo Espacial: Cuadro Completo frente a Regiones de Interés
Zhao et al. (2025) logran una notable simplificación algorítmica al proyectar ortogonalmente las coordenadas 3D a un plano BEV 2D para evaluar las relaciones topológicas punto-polígono (pág. 10). No obstante, la red neuronal EFT-RCNN debe procesar la nube volumétrica tridimensional completa ($360^\circ$ alrededor del sensor QT128 con 864,000 puntos/s) antes de realizar el juicio espacial. La sobrecarga generada al recibir y deserializar esta nube masiva en la CPU bajo ROS reduce la tasa efectiva a 7.30 FPS, demostrando la necesidad de incorporar un filtrado espacial o cerco virtual que acote el procesamiento previo a la inferencia.

---

## 4. Síntesis Crítica y Conclusiones Metodológicas para el Proyecto ESPE

El análisis comparativo de los trece artículos científicos permite extraer lecciones técnicas fundamentales para el diseño y validación del proyecto de titulación en la Universidad de las Fuerzas Armadas ESPE:

### 4.1. Análisis Transversal de Cuellos de Botella Computacionales

1. **La penalización de los módulos de re-identificación de apariencia (Re-ID):**  
   Los resultados cuantitativos demuestran que la mayor degradación en las tasas de procesamiento no proviene del detector de objetos, sino de los módulos de extracción y asociación de características de identidad profunda. En Li y Huang (2024), la adición del módulo de marcha provoca una caída del 65.9% en la velocidad del rastreador (de 29.6 FPS a 10.1 FPS). En Vu et al. (2026), la transición de un rastreador basado puramente en movimiento como ByteTrack (19.7 FPS) a DeepSORT con descriptores de apariencia reduce la velocidad a 10.6 FPS (-46.2%). De forma similar, Jiang et al. (2022) dedican el 63.5% de su tiempo total a la extracción de posturas en AlphaPose.  
   *Conclusión para el proyecto:* El sistema debe priorizar detectores de una sola etapa de última generación combinados con rastreadores cinemáticos ligeros, reservando descriptores profundos únicamente para momentos críticos de oclusión prolongada.

2. **El impacto crítico de la resolución espacial del sensor:**  
   La evidencia de Zhang et al. (2023) demuestra que un aumento en la resolución de entrada desde $512 \times 928$ hasta $800 \times 1440$ provoca una reducción de la tasa de procesamiento del 47.32% (de 20.5 a 10.8 FPS). De manera aún más contundente, Jiménez-Frías et al. (2026) constatan que procesar secuencias en ultra alta definición (4K, $3840 \times 2160$) introduce un tiempo de 0.3056 s únicamente para estabilizar la imagen (~3.27 FPS), haciendo imposible el tiempo real estricto sin submuestreo.  
   *Conclusión para el proyecto:* Para mantener tasas de operación superiores a 25 FPS en hardware convencional, la resolución de entrada debe estandarizarse en dimensiones intermedias ($640 \times 640$ o $1088 \times 608$) o acotarse espacialmente antes de alimentar las capas convolucionales.

3. **La brecha entre el benchmark de laboratorio y el despliegue físico:**  
   El estudio de Zhao et al. (2025) ilustra la brecha de rendimiento entre la evaluación sintética y la ejecución física en tiempo real. Mientras que en un servidor con GPU NVIDIA H800 el modelo alcanza 28.56 FPS sobre el benchmark KITTI, durante la captura en vivo con ROS en una computadora portátil la velocidad cae drásticamente a 7.30 FPS debido a la sobrecarga de la CPU en la gestión de flujos de datos. Un fenómeno análogo se evidencia en Shanmughapriya et al. (2022), donde la latencia de red y la ejecución no optimizada en la nube reducen el sistema a 0.56 FPS.  
   *Conclusión para el proyecto:* La evaluación computacional debe considerar los tiempos de extremo a extremo, incluyendo captura, preprocesamiento y renderizado en pantalla.

### 4.2. El Procesamiento en Escena Completa frente a los Cercos Virtuales Dinámicos

La totalidad de los trece estudios analizados adolece de una limitación estructural común: **la inferencia neuronal profunda se ejecuta sobre la escena completa de manera ininterrumpida**. 

- En Fedosov et al. (2021), Vu et al. (2026) y Yang et al. (2024), las regiones de interés o polígonos virtuales son zonas rígidas y fijas que actúan únicamente como un filtro cinemático posterior al rastreo (*post-tracking*). El detector neuronal procesa cada píxel del cuadro, independientemente de que se encuentre en áreas seguras donde la detección de merodeo carece de sentido.
- En Jiang et al. (2022), esta ausencia de acotación espacial genera falsos positivos graves al detectar mobiliario inanimado (un basurero) como peatón, obligando a los investigadores a depurar manualmente los datos.
- En Zhang et al. (2023) y Li y Huang (2024), la inferencia sobre toda la escena satura la memoria y exige recurrir a técnicas de purga temporal o aceleradores propietarios.

Frente a este paradigma de escena completa, el proyecto desarrollado en la ESPE introduce como propuesta metodológica central el concepto de **cerco virtual dinámico**, definido formalmente como:
> **Aquel cerco virtual que permite al usuario definir y reajustar manualmente los límites del área de interés según los requerimientos de vigilancia de la escena.**

La justificación de este enfoque se fundamenta en los hallazgos computacionales de este reporte:
1. **Reducción del costo computacional:** Al permitir al operador delimitar manualmente la zona crítica, la inferencia de alta densidad puede restringirse a la región de interés activa o activarse de forma condicional, emulando la eficiencia exhibida por Yang et al. (2024) en su primera etapa de reposo.
2. **Supresión de falsas alarmas:** Se eliminan de raíz los errores por detección en mobiliario urbano o transeúntes legítimos fuera del área vigilada (solventando las deficiencias de Jiang et al. y Shanmughapriya et al.).
3. **Flexibilidad operativa:** A diferencia de las zonas fijas de cruce ferroviario o peatonal estático, el cerco virtual dinámico se adapta interactivamente a los cambios en la disposición de los espacios vigilados sin requerir reentrenamiento del modelo neuronal.

### 4.3. Recomendaciones Algorítmicas Finales para la Investigación

Con base en la evidencia empírica consolidada, se establecen los siguientes lineamientos técnicos para el sistema de videovigilancia de la ESPE:
1. **Detector:** Adoptar un modelo YOLO de una sola etapa (preferentemente YOLOv8, YOLO11 o YOLOv12 en variantes compactas Nano o Medium), garantizando una latencia de detección inferior a 35 ms por cuadro, en concordancia con las mediciones de Lee y Park (2026) y Vu et al. (2026).
2. **Rastreador:** Seleccionar ByteTrack o DeepSORT con extractor de características liviano, evitando descriptores pesados de apariencia continua para prevenir caídas de velocidad como la documentada por Li y Huang (2024).
3. **Criterio de Merodeo:** Emplear reglas deterministas basadas en tiempo de permanencia acumulado (*dwell time*) y cambios angulares de dirección, las cuales consumen apenas ~12 ms de cómputo frente a los 66.8 ms más 528 ms de retraso inicial de las redes neuronales temporales recurrentes (Lee y Park, 2026).
4. **Manejo Espacial:** Acotar la inferencia mediante el cerco virtual dinámico reajustado por el usuario, evitando la sobrecarga permanente del procesamiento en cuadro completo.

---

## 5. Referencias Bibliográficas del Corpus Autorizado

1. **Fedosov, V. P., Ibadov, S. R., Kucheryavenko, S. V., & Ibadov, R. R. (2021).** *Method For Detecting Violation at a Pedestrian Crossing Using a Convolutional Neuaral Network*. 2021 Radiation and Scattering of Electromagnetic Waves (RSEMW), Divnomorskoe, Russia, pp. 451–454. IEEE. DOI: [10.1109/RSEMW52378.2021.9494089](https://doi.org/10.1109/RSEMW52378.2021.9494089).
2. **Jiang, Z., Song, G., Qian, Y., & Wang, Y. (2022).** *A deep learning framework for detecting and localizing abnormal pedestrian behaviors at grade crossings*. Neural Computing and Applications, 35(12), 8967–8981. DOI: [10.1007/s00521-022-07660-0](https://doi.org/10.1007/s00521-022-07660-0).
3. **Shanmughapriya M, Gunasundari S, & Bharathy, S. (2022).** *Loitering Detection in Home Surveillance System*. 2022 10th IEEE International Conference on Emerging Trends in Engineering & Technology - Signal and Information Processing (ICETET-SIP-22), IEEE, pp. 1–6. DOI: [10.1109/ICETET-SIP-2254415.2022.9791651](https://doi.org/10.1109/ICETET-SIP-2254415.2022.9791651).
4. **Zhang, Y., Wang, J., Wang, X., Wang, Y., & Yu, S. (2023).** *Research and Application of Loitering Detection Based on Deep Learning*. 2023 9th International Conference on Dependable Systems and Their Applications (DSA), IEEE, pp. 340–346. DOI: [10.1109/DSA59317.2023.00052](https://doi.org/10.1109/DSA59317.2023.00052).
5. **Li, H., & Huang, X. (2024).** *Spatiotemporal heterogeneous information fusion model for loitering anomaly detection*. Signal, Image and Video Processing, 18(6), 5733–5742. DOI: [10.1007/s11760-024-03267-1](https://doi.org/10.1007/s11760-024-03267-1).
6. **Waddenkery, N., & Soma, S. (2024).** *Loitering Based Human Crime Detection in Video Surveillance using Beluga Whale Adam Dingo Optimizer and Deep Convolutional Neural Network*. The International Arab Journal of Information Technology (IAJIT), 21(3), 351–368. DOI: [10.34028/iajit/21/3/1](https://doi.org/10.34028/iajit/21/3/1).
7. **Yang, X., Li, J. Q., Zhan, Y., & Yu, W. (2024).** *Real-time automated deep learning based railroad trespassing violation detection and tracking at highway-rail grade crossing*. Intelligent Transportation Infrastructure, 2024, liae003, pp. 1–10. DOI: [10.1093/iti/liae003](https://doi.org/10.1093/iti/liae003).
8. **Thosar, D., Thosar, R., Sharma, L., Chanore, M., Belkhede, P., & Pohanerkar, S. (2025).** *SmartSurveil: AI-based Intrusion and Suspicious Behavior Detection in CCTV*. 2025 3rd DMIHER International Conference on Artificial Intelligence in Healthcare, Education and Industry (IDICAIHEI), IEEE. DOI: [10.1109/IDICAIHEI65991.2025.11379088](https://doi.org/10.1109/IDICAIHEI65991.2025.11379088).
9. **Jeoung, J., Lee, S., & Hong, T. (2026).** *Automatic discovery of semantic ROIs for vision-based occupancy analysis in corridors*. Building and Environment, 298, 114656. DOI: [10.1016/j.buildenv.2026.114656](https://doi.org/10.1016/j.buildenv.2026.114656).
10. **Jiménez-Frías, P., Salcedo-Delgado, C., & Carlos-Hernández, S. (2026).** *Improving the Automatic Counting in a Region of Interest in Videos of Urban Traffic Taken by Drones Using Video Stabilization*. Computación y Sistemas, 30(1), 131–142. DOI: [10.13053/CyS-30-1-6328](https://doi.org/10.13053/CyS-30-1-6328).
11. **Vu, T. C., Nguyen, D. T., Dinh, L. Q., Nguyen, M. D., Setiadi, D. R. I. M., & Nguyen, M. T. (2026).** *Deep-Learning-Based Multi-Camera Framework for Indoor Human Detection and Presence Management*. Future Internet, 18(8), 435. MDPI. DOI: [10.3390/fi18080435](https://doi.org/10.3390/fi18080435).
12. **Lee, Y. H., & Park, M. (2026).** *A Real-Time Pedestrian Situation Detection Method Using CNN and DeepSORT with Rule-Based Analysis for Autonomous Mobility*. Electronics, 15(3), 532. DOI: [10.3390/electronics15030532](https://doi.org/10.3390/electronics15030532).
13. **Zhao, A., Zhao, Y., & Zheng, Q. (2025).** *Robust Pedestrian Detection and Intrusion Judgment in Coal Yard Hazard Areas via 3D LiDAR-Based Deep Learning*. Sensors, 25(18), 5908. DOI: [10.3390/s25185908](https://doi.org/10.3390/s25185908).
