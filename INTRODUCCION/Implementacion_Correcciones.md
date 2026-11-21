# Desarrollo de un sistema inteligente de videovigilancia para la detección de merodeo peatonal y trayectorias recurrentes mediante visión artificial y cercos virtuales dinámicos

## Evaluación de cercos virtuales dinámicos para la detección de merodeo peatonal y trayectorias recurrentes mediante visión artificial en videovigilancia inteligente

**Denilson Celi1\[0009-0009-4480-2770\] y Raúl Hinojoza1\[0009-0009-9635-3292\]**


*Universidad de las Fuerzas Armadas ESPE, Sangolquí 171103, Ecuador*


{dsceli, rfhinojoza}@espe.edu.ec

### 1 Introducción

Los Sistemas Inteligentes de Vigilancia (ISS) han experimentado una adopción global masiva producto del rápido avance en infraestructura tecnológica y la creciente demanda de seguridad en espacios públicos \[1, 6\].


Mehmood \[3\] explica cómo, tradicionalmente, la vigilancia era ejercida por operadores humanos encargados de observar y analizar las transmisiones de video en pantallas, pero dado que los eventos anómalos eran poco frecuentes por naturaleza, esta labor se tornaba lenta, laboriosa e ineficiente, sobre todo en periodos prolongados de tiempo. Es en este contexto que surge la necesidad de contar con sistemas para la detección automática de anomalías. Los ISS nacen con el fin de suplir esta necesidad, introduciendo técnicas de visión por computador para el análisis de las imágenes generadas por las cámaras y con ello identificar sucesos anómalos, y todo este proceso con una intervención humana mínima \[6\].


**\[Corrección: Delimitar el merodeo como un patrón observable de permanencia o trayectoria; su detección, por sí sola, no demuestra intención delictiva ni permite concluir que una persona constituye una amenaza.\]** 

Entre los comportamientos que estos sistemas buscan detectar se encuentra el merodeo, el cual, aplicado al escenario peatonal, se define como un patrón observable de permanencia prolongada o desplazamiento continuo de un individuo en un área específica, sin una trayectoria o propósito evidentes, siendo normalmente asociada con actividades predelictivas como el robo  \[3, 6, 16\]. En la identificación de esta anomalía resulta igual de fundamental el análisis de las trayectorias recurrentes, es decir, los patrones latentes que se obtienen de los puntos iniciales y finales de las rutas donde los individuos aparecen, pasan o se detienen reiteradamente en el espacio de la imagen \[9\]. Al capturar y clasificar estas trayectorias repetitivas, el sistema tiene la capacidad de determinar áreas de transición funcional y analizar el desplazamiento del individuo en su dominio espacial (posición del sujeto) y en su dominio temporal (tiempo que dura el evento) para discernir si su conducta constituye una amenaza \[9, 6\]. 


Para tratar los comportamientos anómalos mencionados previamente, las primeras versiones de analítica usaron algoritmos de visión por computadora que se basan en características creadas manualmente: el empleo de histogramas de gradientes orientados y descriptores para examinar las trayectorias en términos espaciales y temporales; la separación del fondo estático de los objetos en movimiento mediante modelos gaussianos mixtos \[3, 6, 16\]; y la categorización de los eventos a través de modelos logísticos y lineales. La inflexibilidad del sistema ante factores externos, como las oclusiones, los cambios de la iluminación o los ángulos de cámara, y la necesidad de numerosas calibraciones complejas eran las principales desventajas de este enfoque original \[1\].


**\[Corrección: Eliminar la fórmula 'estas limitaciones se solventaron', precisar temporalmente 'en un principio' (¿principio de qué?) y moderar expresiones como 'siendo solucionado'.\]**

En las fases iniciales de aplicación del aprendizaje profundo en analítica de video, propiciadas por una mayor capacidad computacional y la disponibilidad de conjuntos de datos más extensos, se implementaron arquitecturas convolucionales complementadas con algoritmos para rastrear vehículos y personas cuadro a cuadro \[5, 4\]. Para analizar secuencias temporales en video, se incorporaron redes convolucionales 3D, consistentes en dos ramas que combinan datos espaciales e información temporal, además de integrar redes recurrentes para captar las dependencias a través del tiempo \[3, 1\]. Dado que el refinamiento de estos sistemas resultaba complejo y costoso por el procesamiento y etiquetado masivo de horas de video, tecnologías como los autoencoders y las redes generativas antagónicas ofrecieron una alternativa viable, modelando patrones de conducta normal para emitir alertas únicamente cuando ocurre alguna desviación o anomalía \[1\]. Sin embargo, aunque estas arquitecturas reducen la dependencia de datos completamente anotados, continúan operando sobre la totalidad de la escena visual. Este procesamiento integral obliga al algoritmo a evaluar ruido de fondo y áreas carentes de interés, sosteniendo una carga computacional ineficiente reflejada principalmente en el consumo de CPU, GPU, memoria y energía \[5\].


**\[Corrección : 2.1 fuera de contexto, se debe eliminar / 2.3 esto no es antecedentes, son trabajos relacionados. Diferenciar antecedentes (introducción) de trabajos relacionados. Párrafo eliminado de la Introducción y reubicado en la sección de Trabajos Relacionados.\]**


A pesar de la evolución en las arquitecturas predictivas, la literatura evidencia un dilema de compensación algorítmica definido por dos limitaciones operativas críticas. Por un lado, se presenta una severa degradación de la precisión frente a variables de confusión espaciales; Wahyono et al. \[6\] reportan fallas de clasificación ante oclusiones y variaciones de iluminación que restringen su modelo a escenarios de una sola persona, sumado a las inconsistencias en la discriminación de trayectorias advertidas por Mehmood \[3\]. Por otro lado, existe una ineficiencia computacional insostenible al intentar mitigar dichos errores; el propio Mehmood \[3\] señala que sostener la exactitud exige cálculos de flujo óptico altamente demandantes, mientras que Choudhry et al. \[1\] confirman que la sobrecarga de operaciones en redes neuronales recurrentes imposibilita el procesamiento de videovigilancia a gran escala.


**\[Corrección: 2.4 no hay análisis, hay introducción. Pág. 3, objetivo de la investigación: definan qué hace dinámico al cerco virtual: actualización automática de límites, adaptación a trayectorias, frecuencia de actualización u otro mecanismo.\]**

Estas limitaciones en los sistemas de videovigilancia inteligente evidencian que el procesamiento integral de la escena de video satura los recursos del sistema al obligarlo a evaluar ruido de fondo continuo y áreas irrelevantes. Con el propósito de reducir esta demanda computacional, se plantea la delimitación algorítmica del análisis visual mediante cercos virtuales dinámicos, los cuales permiten al usuario definir y reajustar manualmente los límites del área de interés según los requerimientos de vigilancia de la escena. Por consiguiente, el objetivo de esta investigación es evaluar el impacto de los cercos virtuales dinámicos sobre la precisión de clasificación y el costo computacional frente al procesamiento de escena completa en modelos de detección orientados al merodeo peatonal, para determinar su viabilidad algorítmica en tiempo real.

### 2 Trabajos relacionados

**\[Corrección: 3.1 eliminar (narrativa de conteo de registros).\]** 

La literatura reciente sobre videovigilancia inteligente, seleccionada bajo la metodología PRISMA 2020 de Page et al. \[19\] a partir de Web of Science, IEEE Xplore y Scopus como se resume en la Figura 1, se centra en la identificación de merodeo o trayectorias peatonales repetitivas y anómalas, la localización y el seguimiento continuo de peatones en cámaras fijas mediante visión artificial o aprendizaje profundo, y la delimitación geométrica o semántica del espacio con líneas de cruce, regiones de interés o zonas restringidas configurables.



**Figura 1. Diagrama de flujo de selección bibliográfica según la metodología PRISMA 2020.**


Dentro de los estudios orientados a la detección de merodeo mediante seguimiento peatonal continuo, una primera línea metodológica combina modelos de detección de objetos y algoritmos de rastreo con reglas basadas en umbrales de tiempo o trayectoria definidos de antemano. En esta línea, Shanmughapriya et al. \[13\] integraron YOLOv3, DeepSORT y clasificadores Haar Cascade en un entorno residencial para declarar el merodeo cuando un mismo peatón rastreado supera los 60 segundos de permanencia, mientras que Zhang et al. \[18\] ampliaron dicho criterio en el sistema JYLD mediante YOLOA-S y JYTracker al combinar el tiempo de estancia con umbrales de distancia acumulada en píxeles y giros superiores a 90° y 160°. Pese a que el segundo trabajo incorpora restricciones geométricas para describir mejor el desplazamiento, ambos estudios coinciden en no reportar métricas de exactitud ni tasas de falsas alarmas sobre conjuntos de datos anotados, limitando sus pruebas a medir el tiempo de respuesta durante fotogramas consecutivos en vivo \[13\] o a una inspección visual cualitativa \[18\]. Esto dificulta conocer su precisión real al evaluar toda la escena sin delimitar zonas de interés.


**\[Corrección docente: 3.2 Aporta si se va a tomar como referencia de evaluación más adelante.\]**

 A diferencia de las pruebas meramente cualitativas, otros estudios incorporan evaluaciones estadísticas del merodeo sobre conjuntos de datos anotados. Li y Huang \[12\] midieron esta conducta al integrar YOLOX con un rastreador de reevaluación por siluetas de marcha y un detector de desplazamiento angular, reportando una exactitud de 87.4 %, sobre el conjunto IITB-Corridor tras calibrar manualmente el ángulo de desvío de la trayectoria peatonal en 135°. Al contrastar este método con arquitecturas basadas en esqueletos y predicción recurrente como MPED-RNN \[10, 12\], que alcanzó 80.2 % de exactitud en el mismo conjunto y presentó fallos ante desplazamientos en sentido opuesto en cruces peatonales \[10\], o frente a modelos como FFP con 78.5 % y SVADA con 86.2 %, se observa que los umbrales de decisión se ajustaron sobre las propias secuencias de prueba, sugiriendo la dependencia de su desempeño en el ajuste manual de parámetros en cada escena. Waddenkery y Soma \[16\] aplican validación cruzada de 10 pliegues sobre el conjunto UCF Crime, registrando las métricas individuales por cada pliegue, mientras que Mehmood \[3\] las calcula de forma estrictamente individualizada por clase sobre el conjunto UFLV-DS. Las metodologías manejadas en ambos casos proponen una evaluación desacoplada de la arquitectura sobre el conjunto de datos, entregando resultados más fiables 

A diferencia de las pruebas meramente cualitativas, otros estudios incorporan evaluaciones estadísticas del merodeo sobre conjuntos de datos anotados. Li y Huang \[12\] midieron esta conducta al integrar YOLOX con un rastreador de siluetas de marcha y un criterio de desvío angular, reportando una exactitud de 87.4 % en el conjunto IITB-Corridor frente a métodos basados en esqueletos como MPED-RNN, que alcanzó 80.2 % en el mismo conjunto y presentó fallos ante desplazamientos en sentido opuesto \[10, 12\]. Sin embargo, en esta comparación los umbrales angulares se calibraron directamente sobre las secuencias de prueba, lo que introduce un sesgo de ajuste manual ligado a cada escena. En contraste, Waddenkery y Soma \[16\] emplearon validación cruzada de 10 pliegues sobre el conjunto UCF-Crime alcanzando 99.76 % de exactitud, mientras que Mehmood \[3\] evaluó las métricas de forma desglosada por clase mediante redes convolucionales 3D logrando 98.5 % de exactitud. Estos dos últimos esquemas separan el entrenamiento de la validación para ofrecer estimaciones más fiables y constituyen una referencia metodológica más sólida para futuras pruebas, aunque continúan procesando la totalidad del fotograma.



**\[Corrección: Pág. 4, párrafo 2: Se presenta una explicación causal como si estuviera demostrada; la caída de FPS no puede atribuirse específicamente a inspeccionar regiones periféricas sin aislar esa variable. Revisar la escritura que expone una lectura compleja y desordenada; hacer una tabla de características con la información indicada.\]** 

La velocidad de procesamiento en el seguimiento peatonal se ve afectada tanto por la complejidad del algoritmo de rastreo como por la resolución de entrada, según se resume en la Tabla 1. En las pruebas de Li y Huang \[12\] sobre el conjunto MOT17 manteniendo fijo el detector YOLOX, el rastreador ligero ByteTrack sostuvo una alta tasa de cuadros por segundo, mientras que incorporar extracción de apariencia con StrongSORT, BoT-SORT o siluetas de marcha incrementó ligeramente la precisión de seguimiento, pero redujo de forma pronunciada la velocidad. Por su parte, Zhang et al. \[18\] evaluaron el sistema JYLD sobre el conjunto MOT20 y registraron una caída cercana a la mitad en los cuadros por segundo al elevar la resolución de entrada con el mismo rastreador. Como estas pruebas cambian de rastreador o aumentan la resolución, la disminución de FPS se debe a esos factores y no puede atribuirse solo a procesar zonas periféricas, por lo que aún se requiere medir por separado el efecto de acotar el área vigilada.


**Tabla 1. Características de rendimiento y velocidad de procesamiento según el rastreador y la resolución de entrada.**

| **Estudio** | **Conjunto** | **Detector** | **Rastreador** | **Resolución** | **MOTA** | **Velocidad** |
| --- | --- | --- | --- | --- | --- | --- |
| **Li y Huang \[12\]** | **MOT17** | **YOLOX** | **ByteTrack** | **1088 × 608 px** | **76.7 %** | **29.6 FPS** |
| **Li y Huang \[12\]** | **MOT17** | **YOLOX** | **StrongSORT** | **1088 × 608 px** | **77.1 %** | **7.5 FPS** |
| **Li y Huang \[12\]** | **MOT17** | **YOLOX** | **BoT-SORT** | **1088 × 608 px** | **78.5 %** | **4.5 FPS** |
| **Li y Huang \[12\]** | **MOT17** | **YOLOX** | **Siluetas de marcha** | **1088 × 608 px** | **78.0 %** | **10.1 FPS** |
| **Zhang et al. \[18\]** | **MOT20** | **YOLOA-S** | **JYTracker** | **512 × 928 px** | **86.7 %** | **20.5 FPS** |
| **Zhang et al. \[18\]** | **MOT20** | **YOLOA-S** | **JYTracker** | **800 × 1440 px** | **89.3 %** | **10.8 FPS** |



**\[Corrección: Reubicación de Lee y Park \[2\] y Zhao et al. \[7\] desde la Introducción hacia Trabajos Relacionados.\]** 

Con el fin de focalizar el monitoreo peatonal dentro de la escena, otra línea de estudios emplea regiones de interés, segmentos de cruce o polígonos virtuales, cuyas características se comparan en la Tabla 2. Mientras Fedosov et al. \[8\] trazaron manualmente un paso peatonal sin reportar pruebas en secuencias reales, Vu et al. \[15\] definieron polígonos fijos de conteo que evitaron falsas alarmas en zonas vacías, pero omitieron eventos ante cruces simultáneos, oclusiones y cambios de luz. Por su parte, Lee y Park \[2\] calibraron una región de interés para detectar peatones a distancia con alta precisión, en tanto que Zhao et al. \[7\] delimitaron áreas de peligro tridimensionales mediante sensores LiDAR. Pese a sus avances, durante la inferencia en tiempo real los métodos basados en cámaras verifican estas zonas solo después de analizar el fotograma completo \[2, 8, 15\] o dependen de sensores LiDAR \[7\], por lo que no reducen el área procesada por el detector en operación.

La restricción espacial del área vigilada constituye otra estrategia para acotar el seguimiento peatonal a zonas de interés específicas, cuyas propuestas se resumen en la Tabla 2. En sistemas basados en cámaras convencionales, la estrategia predominante consiste en definir líneas de cruce o polígonos virtuales fijos \[8, 15\]. Sin embargo, estos filtros estáticos son vulnerables a las condiciones cambiantes del entorno, omitiendo eventos ante cruces simultáneos, sombras y oclusiones \[15\], limitación que otros autores mitigan mediante la calibración geométrica de la región de interés para estimar distancias y detectar peatones lejanos con alta precisión \[2\]. Por otra parte, la delimitación espacial puede trasladarse al dominio tridimensional mediante sensores LiDAR para aislar zonas de riesgo a partir de nubes de puntos \[7\], prescindiendo de las variaciones de iluminación aunque con un costo de implementación restrictivo. Pese a estas alternativas, los métodos ópticos verifican las zonas delimitadas recién después de analizar el fotograma completo \[2, 8, 15\], mientras que las soluciones tridimensionales demandan equipamiento especializado ajeno a las cámaras estándar \[7\], dejando pendiente reducir la superficie evaluada por el detector durante la videovigilancia.


**Tabla 2. Comparación de enfoques basados en regiones de interés y delimitación espacial.**

| **Estudio** | **Pipeline o arquitectura** | **Delimitación espacial** | **Métrica de rendimiento reportada** | **Velocidad (FPS)** |
| --- | --- | --- | --- | --- |
| **Fedosov et al. \[8\]** | **YOLOv3** | **Cruce peatonal manual fijo** | **No reporta** | **No reporta** |
| **Vu et al. \[15\]** | **YOLOv11n + DeepSORT** | **Polígonos virtuales fijos** | **66.0 % mAP@0.5 (detección)** | **10.6** |
| **Lee y Park \[2\]** | **YOLOv12-m + DeepSORT** | **Región de interés calibrada** | **96.6 % Precisión (clasificación)** | **17.2** |
| **Zhao et al. \[7\]** | **EFT-RCNN (LiDAR 3D)** | **Área de peligro punto-región** | **92.9 % Exactitud (detección)** | **28.6** |




**\[Corrección: No hay el párrafo resumen con las características técnicas que se podrían tomar en el desarrollo, en su lugar se indica que** ***"el presente trabajo evalúa modelos ....*****"--> Fuera de contexto, ya que no se ha evaluado nada aún. \]** 


A partir de la evidencia expuesta y de los resultados sintetizados en las Tablas 1 y 2, se observa que equilibrar la precisión en la detección del merodeo con el costo computacional requiere articular componentes específicos en cada fase del análisis visual. En el seguimiento peatonal, resulta conveniente emplear detectores de una sola etapa de la familia YOLO junto con algoritmos de rastreo livianos como ByteTrack o DeepSORT \[2, 12, 15, 18\], evitando extractores pesados de apariencia en toda la escena que reducen de forma pronunciada los cuadros por segundo \[12\]. Para superar la limitación de las zonas fijas que solo filtran resultados después de procesar toda la imagen \[2, 8, 15\], se plantea evaluar cercos virtuales dinámicos que permitan al usuario definir y reajustar manualmente los límites del área de interés según los requerimientos de vigilancia de la escena, acotando la detección únicamente a dicha región activa. Finalmente, dentro del área delimitada se pueden integrar criterios de tiempo de permanencia y cambios de dirección para identificar el merodeo \[10, 12, 13, 18\], tomando las métricas reportadas por Li y Huang \[12\] como línea base de referencia sobre conjuntos de datos como IITB-Corridor, MOT17 o MOT20 \[12, 18\] para futuras pruebas de precisión y costo computacional. 

A partir de la evidencia expuesta y de los resultados sintetizados en las Tablas 1 y 2, sostener una alta precisión en la detección del merodeo sin degradar la tasa de cuadros por segundo ni elevar el tiempo de respuesta del sistema requiere articular componentes específicos en las etapas de detección y rastreo peatonal. En esta tarea, resulta conveniente emplear detectores de una sola etapa de la familia YOLO junto con algoritmos de rastreo livianos como ByteTrack o DeepSORT \[2, 12, 15, 18\], evitando extractores pesados de apariencia en toda la escena que reducen de forma drástica los cuadros por segundo \[12\]. Para superar la limitación de las zonas fijas que solo descartan detecciones después de examinar el fotograma completo durante el monitoreo \[2, 8, 15\], se plantea evaluar cercos virtuales dinámicos que permitan al usuario definir y reajustar manualmente los límites del área de interés según los requerimientos de vigilancia de la escena, concentrando el análisis exclusivamente en dicha región activa. Finalmente, dentro del área delimitada se pueden integrar criterios de tiempo de permanencia y cambios de dirección para identificar el merodeo \[10, 12, 13, 18\], tomando como referencia los esquemas de validación de Waddenkery y Soma \[16\] y Mehmood \[3\] para la exactitud, junto con los registros de Li y Huang \[12\], Zhang et al. \[18\] y Lee y Park \[2\] sobre conjuntos de datos como UCF-Crime, IITB-Corridor o MOT20 para evaluar el costo computacional a partir de la tasa de cuadros por segundo y la latencia de procesamiento.

### Referencias

1. Choudhry, N., Abawajy, J., Huda, S., Rao, I.: A Comprehensive Survey of Machine Learning Methods for Surveillance Videos Anomaly Detection. IEEE Access 11, 114680–114713 (2023). [https://doi.org/10.1109/ACCESS.2023.3321800](https://doi.org/10.1109/ACCESS.2023.3321800)


1. Lee, Y.H., Park, M.: A Real-Time Pedestrian Situation Detection Method Using CNN and DeepSORT with Rule-Based Analysis for Autonomous Mobility. Electronics 15(3), 532 (2026). [https://doi.org/10.3390/electronics15030532](https://doi.org/10.3390/electronics15030532)


1. Mehmood, A.: Abnormal Behavior Detection in Uncrowded Videos with Two-Stream 3D Convolutional Neural Networks. Applied Sciences 11(8), 3523 (2021). [https://doi.org/10.3390/app11083523](https://doi.org/10.3390/app11083523)


1. Nayak, R., Behera, M.M., Girish, V., Pati, U.C., Das, S.K.: Deep Learning Based Loitering Detection System Using Multi-Camera Video Surveillance Network. In: 2019 IEEE International Symposium on Smart Electronic Systems (iSES) (Formerly iNiS), pp. 215–220 (2019). [https://doi.org/10.1109/iSES47678.2019.00055](https://doi.org/10.1109/iSES47678.2019.00055)


1. Vinod, J., T M, D., Rajesh, R.: Interactive YOLO-based Object Detection using a Polygonal Region of Interest for Airborne Surveillance Applications. In: 2024 IEEE Space, Aerospace and Defence Conference (SPACE), pp. 901–905 (2024). [https://doi.org/10.1109/SPACE63117.2024.10668012](https://doi.org/10.1109/SPACE63117.2024.10668012)


1. Wahyono, Harjoko, A., Dharmawan, A., Adhinata, F.D., Kosala, G., Jo, K.-H.: Loitering Detection Using Spatial-Temporal Information for Intelligent Surveillance Systems on a Vision Sensor. Journal of Sensor and Actuator Networks 12(1), 9 (2023). [https://doi.org/10.3390/jsan12010009](https://doi.org/10.3390/jsan12010009)


1. Zhao, A., Zhao, Y., Zheng, Q.: Robust Pedestrian Detection and Intrusion Judgment in Coal Yard Hazard Areas via 3D LiDAR-Based Deep Learning. Sensors 25(18), 5908 (2025). [https://doi.org/10.3390/s25185908](https://doi.org/10.3390/s25185908)


1. Fedosov, V.P., Ibadov, S.R., Ibadov, R.R., Kucheryavenko, S.V.: Method For Detecting Violation at a Pedestrian Crossing Using a Convolutional Neural Network. In: 2021 Radiation and Scattering of Electromagnetic Waves (RSEMW), pp. 451–454 (2021). [https://doi.org/10.1109/RSEMW52378.2021.9494089](https://doi.org/10.1109/RSEMW52378.2021.9494089)


1. Jeoung, J., Hong, T., Park, J., Jeong, K.: Automatic discovery of semantic ROIs for vision-based occupancy analysis in corridors. Building and Environment 298, 114656 (2026). [https://doi.org/10.1016/j.buildenv.2026.114656](https://doi.org/10.1016/j.buildenv.2026.114656)


1. Jiang, Z., Song, G., Qian, Y., Wang, Y.: A deep learning framework for detecting and localizing abnormal pedestrian behaviors at grade crossings. Neural Computing and Applications 34(24), 22099–22113 (2022). [https://doi.org/10.1007/s00521-022-07660-0](https://doi.org/10.1007/s00521-022-07660-0)


1. Jiménez-Frías, G.A., Hernandez-Lopez, F.J., Batard, T., Múniz-Sánchez, V., Hayet, J.-B., Forti-Sosa, S., Pérez-Pech, E.: Improving the Automatic Counting in a Region of Interest in Videos of Urban Traffic Taken by Drones Using Video Stabilization. Computación y Sistemas 30(1) (2026).


1. Li, H., Huang, X.: Spatiotemporal heterogeneous information fusion model for loitering anomaly detection. Signal, Image and Video Processing 18(8–9), 5733–5742 (2024). [https://doi.org/10.1007/s11760-024-03267-1](https://doi.org/10.1007/s11760-024-03267-1)


1. M, S., S, G., Bharathy, S.: Loitering Detection in Home Surveillance System. In: 2022 10th International Conference on Emerging Trends in Engineering and Technology - Signal and Information Processing (ICETET-SIP-22), pp. 1–6 (2022). [https://doi.org/10.1109/ICETET-SIP-2254415.2022.9791651](https://doi.org/10.1109/ICETET-SIP-2254415.2022.9791651)


1. Thosar, D., Thosar, R., Sharma, L., Chanore, M., Belkhede, P., Pohanerkar, S.: SmartSurveil: AI-based Intrusion and Suspicious Behavior Detection in CCTV. In: 2025 3rd DMIHER International Conference on Artificial Intelligence in Healthcare, Education and Industry (IDICAIHEI), pp. 1–6 (2025). [https://doi.org/10.1109/IDICAIHEI65991.2025.11379088](https://doi.org/10.1109/IDICAIHEI65991.2025.11379088)


1. Vu, T.C., Nguyen, D.T., Dinh, L.Q., Nguyen, M.D., Setiadi, D.R.I.M., Nguyen, M.T.: Deep-Learning-Based Multi-Camera Framework for Indoor Human Detection and Presence Management. Future Internet 18(8), 435 (2026). [https://doi.org/10.3390/fi18080435](https://doi.org/10.3390/fi18080435)


1. Waddenkery, N., Soma, S.: Loitering Based Human Crime Detection in Video Surveillance using Beluga Whale Adam Dingo Optimizer and Deep Convolutional Neural Network. The International Arab Journal of Information Technology 21(3) (2024). [https://doi.org/10.34028/iajit/21/3/1](https://doi.org/10.34028/iajit/21/3/1)


1. Yang, X., Li, J.Q., Zhan, Y., Yu, W.: Real-time automated deep learning based railroad trespassing violation detection and tracking at highway-rail grade crossing. Intelligent Transportation Infrastructure 3, liae003 (2024). [https://doi.org/10.1093/iti/liae003](https://doi.org/10.1093/iti/liae003)


1. Zhang, Y., Wang, J., Wang, X., Wang, Y., Yu, S.: Research and Application of Loitering Detection Based on Deep Learning. In: 2023 10th International Conference on Dependable Systems and Their Applications (DSA), pp. 339–346 (2023). [https://doi.org/10.1109/DSA59317.2023.00048](https://doi.org/10.1109/DSA59317.2023.00048)


1. Page, M.J., McKenzie, J.E., Bossuyt, P.M., Boutron, I., Hoffmann, T.C., Mulrow, C.D., et al.: The PRISMA 2020 statement: an updated guideline for reporting systematic reviews. BMJ 372, n71 (2021). [https://doi.org/10.1136/bmj.n71](https://doi.org/10.1136/bmj.n71)
1. Cho, J., Kang, Y.: Context-Aware Anomaly Detection of Pedestrian Trajectories in Urban Back Streets Using a Variational Autoencoder. ISPRS International Journal of Geo-Information 14(11), 438 (2025). [https://doi.org/10.3390/ijgi14110438](https://doi.org/10.3390/ijgi14110438) 

