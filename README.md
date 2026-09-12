# CALCULO-AMBULATORIO-DEL-INDICE-PLETISMOGRAFICO-QUIRURGICO-SPI 
# Introducción

El dolor posoperatorio continúa siendo un problema clínico relevante, pues se estima que entre el 20 % y el 80 % de los pacientes que son sometidos a algún procedimiento quirúrgico experimentan dolor agudo de intensidad moderada a severa después de la cirugía [1]. Esta cifra  evidencia que buena parte del manejo analgésico durante y después de una intervención quirúrgica sigue siendo insuficiente, lo cual ha motivado el desarrollo de herramientas que permitan evaluar de forma objetiva y en tiempo real el nivel de nocicepción de un paciente mientras se encuentra bajo anestesia general. Contar con esta información permite al anestesiólogo ajustar la dosis de analgésicos de manera más precisa, en lugar de basarse únicamente en variables hemodinámicas indirectas como la frecuencia cardíaca o la presión arterial, que pueden verse afectadas por múltiples factores ajenos al dolor.

Entre las alternativas que se han propuesto para este propósito se encuentra el índice pletismográfico quirúrgico, conocido por sus siglas en inglés como SPI (Surgical Pleth Index), desarrollado originalmente por GE Healthcare. Este índice se calcula a partir de la señal fotopletismográfica (PPG), es decir, la onda de pulso que puede obtenerse de forma no invasiva mediante un sensor óptico ubicado, por ejemplo, en un dedo. El SPI combina dos características de esta señal, el intervalo entre pulsos consecutivos (HBI) y la amplitud de cada pulso (PPGA) en un único valor que va de 0 a 100, donde los valores más altos reflejan una mayor activación simpática asociada a una respuesta nociceptiva no controlada, mientras que valores entre 20 y 50 suelen asociarse con un nivel de analgesia adecuado durante la cirugía [2]. Su atractivo principal radica en que no requiere ningún dispositivo adicional al que ya usa un pulsioxímetro convencional, lo que lo convierte en una herramienta de monitorización accesible y de fácil implementación.

A pesar de que el SPI fue diseñado como una herramienta de uso intraoperatorio, su principio de cálculo puede reproducirse fuera de un quirófano utilizando sensores ópticos de bajo costo y un microcontrolador, lo que abre la posibilidad de construir un sistema ambulatorio capaz de estimar este índice sin depender del equipo comercial. Ahora bien, para verificar que un sistema construido de esta manera responde de forma coherente ante cambios reales en el estado del sistema nervioso autónomo, es necesario someterlo a un estímulo controlado que module la actividad simpática de manera predecible. El Cold Pressor Test (CPT), que consiste en la inmersión de una extremidad en agua fría durante un periodo breve, es uno de los modelos experimentales de dolor más utilizados con este fin, ya que se ha demostrado que induce una vasoconstricción periférica marcada con la consecuente caída de la PPGA y un aumento reproducible del SPI en voluntarios sanos [5].

En este orden de ideas, el presente laboratorio tiene como propósito diseñar, implementar y validar un sistema ambulatorio capaz de capturar la señal PPG de un sujeto, procesarla en tiempo real y calcular a partir de ella el SPI, para posteriormente evaluar su comportamiento ante la aplicación del Cold Pressor Test como estímulo nociceptivo controlado.

# Objetivos

Objetivo General:

Desarrollar un sistema de medición continua del índice pletismográfico quirúrgico (SPI) en condiciones ambulatorias.

Objetivos Específicos:

Reconocer las características fundamentales de la onda de pulso a partir de las cuales se obtiene el SPI.
Construir un sistema que calcule el SPI en tiempo real y bajo condiciones ambulatorias.
Validar el funcionamiento del sistema desarrollado mediante un método que induzca una respuesta fisiológica similar a la que produce el dolor agudo.

# Metodología
Parte A

Parte B

Parte C 

# Análisis y Discusión De Resultados
# Conclusión
# Referencias 
[1] J. L. Apfelbaum, C. Chen, S. S. Mehta, and T. J. Gan, "Postoperative pain experience: results from a national survey suggest postoperative pain continues to be undermanaged," Anesth. Analg., vol. 97, no. 2, pp. 534–540, 2003. doi: 10.1213/01.ANE.0000068822.10113.9E.

[2] S. K. Oh, Y. J. Won, and B. G. Lim, "Surgical pleth index monitoring in perioperative pain management: usefulness and limitations," Korean J. Anesthesiol., vol. 77, no. 1, pp. 31–45, 2024. doi: 10.4097/kja.23158.

[3] E. J. Argüello-Prada, M. A. Dávalos Cantín, and J. C. Victoria, "A photoplethysmography-based system for talking detection in bedridden patients," Biomed. Signal Process. Control, vol. 81, art. 104477, 2023. doi: 10.1016/j.bspc.2022.104477.

[4] P. H. Charlton, E. J. Argüello-Prada, J. Mant, and P. A. Kyriacou, "The MSPTDfast photoplethysmography beat detection algorithm: design, benchmarking, and open-source distribution," Physiol. Meas., vol. 46, art. 035002, 2025. doi: 10.1088/1361-6579/adb89e.

[5] K. Hamunen, V. Kontinen, E. Hakala, P. Talke, M. Paloheimo, and E. Kalso, "Effect of pain on autonomic nervous system indices derived from photoplethysmography in healthy volunteers," Br. J. Anaesth., vol. 108, no. 5, pp. 838–844, 2012. doi: 10.1093/bja/aes001.

[6] M. Vincenot, M. Roberge, C.-É. Giguère, and S. Potvin, "Conditioned pain modulation and pleasant pain relief as complementary processes reflecting individual differences in pain coping: a clustering approach," Eur. J. Pain, vol. 30, no. 8, art. e70366, 2026. doi: 10.1002/ejp.70366.

[7] M. Arevalillo-Herráez, Y. Wu, B. Tilbury, and N. Ramzan, "Motion-based confidence score to support the practical application of rPPG methods in health monitoring," J. Med. Syst., vol. 50, no. 1, 2026. doi: 10.1007/s10916-026-02412-2.

[8] M. Koriakina, M. Lukov, U. Nikishkina, A. Kirsanov, E. Dmitrieva, and E. Blagovechtchenski, "Social and physiological stress elicit divergent psycho-physiological dynamics and motor cortex activation," Front. Psychol., vol. 17, art. 1760772, 2026. doi: 10.3389/fpsyg.2026.1760772.
