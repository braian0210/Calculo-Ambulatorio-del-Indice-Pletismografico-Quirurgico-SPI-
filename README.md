# CALCULO-AMBULATORIO-DEL-INDICE-PLETISMOGRAFICO-QUIRURGICO-SPI 
# Introducción

El dolor posoperatorio continúa siendo un problema clínico relevante, pues se estima que entre el 20 % y el 80 % de los pacientes que son sometidos a algún procedimiento quirúrgico experimentan dolor agudo de intensidad moderada a severa después de la cirugía [1]. Esta cifra  evidencia que buena parte del manejo analgésico durante y después de una intervención quirúrgica sigue siendo insuficiente, lo cual ha motivado el desarrollo de herramientas que permitan evaluar de forma objetiva y en tiempo real el nivel de nocicepción de un paciente mientras se encuentra bajo anestesia general. Contar con esta información permite al anestesiólogo ajustar la dosis de analgésicos de manera más precisa, en lugar de basarse únicamente en variables hemodinámicas indirectas como la frecuencia cardíaca o la presión arterial, que pueden verse afectadas por múltiples factores ajenos al dolor.

Entre las alternativas que se han propuesto para este propósito se encuentra el índice pletismográfico quirúrgico, conocido por sus siglas en inglés como SPI (Surgical Pleth Index), desarrollado originalmente por GE Healthcare. Este índice se calcula a partir de la señal fotopletismográfica (PPG), es decir, la onda de pulso que puede obtenerse de forma no invasiva mediante un sensor óptico ubicado, por ejemplo, en un dedo. El SPI combina dos características de esta señal, el intervalo entre pulsos consecutivos (HBI) y la amplitud de cada pulso (PPGA) en un único valor que va de 0 a 100, donde los valores más altos reflejan una mayor activación simpática asociada a una respuesta nociceptiva no controlada, mientras que valores entre 20 y 50 suelen asociarse con un nivel de analgesia adecuado durante la cirugía [2]. Su atractivo principal radica en que no requiere ningún dispositivo adicional al que ya usa un pulsioxímetro convencional, lo que lo convierte en una herramienta de monitorización accesible y de fácil implementación.

A pesar de que el SPI fue diseñado como una herramienta de uso intraoperatorio, su principio de cálculo puede reproducirse fuera de un quirófano utilizando sensores ópticos de bajo costo y un microcontrolador, lo que abre la posibilidad de construir un sistema ambulatorio capaz de estimar este índice sin depender del equipo comercial. Ahora bien, para verificar que un sistema construido de esta manera responde de forma coherente ante cambios reales en el estado del sistema nervioso autónomo, es necesario someterlo a un estímulo controlado que module la actividad simpática de manera predecible. El Cold Pressor Test (CPT), que consiste en la inmersión de una extremidad en agua fría durante un periodo breve, es uno de los modelos experimentales de dolor más utilizados con este fin, ya que se ha demostrado que induce una vasoconstricción periférica marcada con la consecuente caída de la PPGA y un aumento reproducible del SPI en voluntarios sanos [5].

En este orden de ideas, el presente laboratorio tiene como propósito diseñar, implementar y validar un sistema ambulatorio capaz de capturar la señal PPG de un sujeto, procesarla en tiempo real y calcular a partir de ella el SPI, para posteriormente evaluar su comportamiento ante la aplicación del Cold Pressor Test como estímulo nociceptivo controlado.

# Objetivos

Objetivo General:

- Desarrollar un sistema de medición continua del índice pletismográfico quirúrgico (SPI) en condiciones ambulatorias.

Objetivos Específicos:

- Reconocer las características fundamentales de la onda de pulso a partir de las cuales se obtiene el SPI.
  
- Construir un sistema que calcule el SPI en tiempo real y bajo condiciones ambulatorias.

- Validar el funcionamiento del sistema desarrollado mediante un método que induzca una respuesta fisiológica similar a la que produce el dolor agudo.

# Metodología
Parte A

1. Construir en Proto-Board el circuito que se muestra en la Figura 1:

<img width="526" height="290" alt="image" src="https://github.com/user-attachments/assets/19da24e1-a340-4678-ab0b-9d898597f093" />

 <b>Figura 1.</b> Circuito para capturar las variaciones del volumen sanguíneo periférico.
</p>

Se construyó en una protoboard el circuito propuesto en la Figura 1 de la guía, orientado a capturar las variaciones del volumen sanguíneo periférico a partir de un sensor óptico. El circuito está compuesto por un sensor óptico de reflectancia, un transistor 2N3904 que actúa como etapa de conmutación/amplificación inicial de la señal del fototransistor, y un amplificador operacional dual LM358 configurado para acondicionar dicha señal, apoyado en resistencias de distintos valores, un condensador cerámico de 100 nF, un condensador electrolítico de 4.7 µF y dos potenciómetros para ajustar la ganancia y el offset de la etapa analógica.

Como sensor óptico se utilizó el TCST1103 en lugar del TCST110 sugerido por la guía, dado que este último no se consiguió comercialmente al momento de construir el circuito. Ambos son optoacopladores con un principio de funcionamiento equivalente (emisor infrarrojo y fototransistor receptor enfrentados), por lo que su uso no alteró la estructura del circuito construido. La Figura 2 muestra el resultado de este montaje, incluyendo el sensor alojado en una carcasa de cartón para aislarlo de la luz ambiente durante la medición.

<img width="1600" height="1204" alt="image" src="https://github.com/user-attachments/assets/ef1114fd-e94b-4803-b850-259881ed89d5" />

 <b>Figura 2.</b> Construcción del circuito para capturar las variaciones del volumen sanguíneo periférico.
</p>

2. Si está usando un acoplador óptico TCST110, modifíquelo tal y como se ilustra
en la Figura 2 para convertirlo en un sensor de reflectancia:

<img width="503" height="252" alt="image" src="https://github.com/user-attachments/assets/11ed73ae-2e98-48e7-b07f-c1402458d6ab" />


Como se mencionó anteriormente se usó el sensor TCST1103 el cual sí fue modificado físicamente para convertirlo de su configuración original transmisiva a una configuración de reflectancia, tal como se ilustra en la Figura 3, el emisor y el receptor infrarrojo, que originalmente están enfrentados a través de la ranura del optoacoplador, se separaron y reorientaron para quedar dispuestos lado a lado, apuntando ambos hacia la misma dirección. De esta manera, en lugar de que la luz emitida atraviese el dedo para ser captada al otro lado, la luz incide sobre el dedo y es la porción reflejada por el tejido la que llega al fototransistor receptor.

Este sensor ya modificado se montó dentro de una carcasa de cartón construida a la medida (Figura 4), con el TCST1103 fijo en la base y una abertura superior por la cual el voluntario introduce el dedo, apoyándolo sobre el sensor. La carcasa cumple dos funciones ya que mantiene el dedo en una posición fija y constante sobre el par emisor-receptor, evitando que el movimiento degrade la señal reflejada, y bloquea la entrada de luz ambiente, la cual de otro modo se sumaría como interferencia a la señal óptica de interés, dado que el fototransistor no distingue entre la luz infrarroja reflejada por el dedo y cualquier otra fuente de luz externa.

<img width="1204" height="1600" alt="WhatsApp Image 2026-09-12 at 12 25 17 PM" src="https://github.com/user-attachments/assets/6e5da210-62c8-4a47-abd9-b9b8aa78dc25" />

<b>Figura 3.</b> Sensor óptico de reflectancia basado en el optoacoplador TCST110.
</p>

Como ya se mencionó anteriormente,no se empleó el TCST110 sino el TCST1103, sensor que se utilizó en su configuración como interruptor óptico en donde el dedo del voluntario se introduce en la ranura del sensor  quedando entre el emisor y el receptor infrarrojo, en lugar de reflejar la luz desde un mismo lado como ocurriría en una configuración de reflectancia. Por esta razón, la modificación descrita en este punto no fue necesaria ni aplicable en la implementación realizada.

<img width="1204" height="1600" alt="WhatsApp Image 2026-09-12 at 12 25 17 PM" src="https://github.com/user-attachments/assets/f13a3991-070e-48c4-88b9-df14ae9c1b64" />
<b>Figura 4.</b> Modifucación TCST1103 .
</p>

3. Conecte la salida del circuito a una de las entradas analógicas de una placa
Arduino UNO o Nano y verifique empleado el “Serial Plotter” que aquel es
capaz de registrar las variaciones del volumen sanguíneo periférico. Realice
los ajustes necesarios mediante los potenciómetros para obtener una señal
con la menor interferencia posible. NOTA: Puede que sea necesario emplear
una fuente negativa para controlar el offset de la señal, en cuyo caso, se
recomienda usar VEE = -3 VDC para alimentar a los operacionales.


4. Investigue sobre la técnica “Cold Pressor Test” (CPT), en qué consiste y cómo
aplicarla en el laboratorio.


Parte B

1. Revise la literatura relacionada para encontrar la definición matemática del
índice pletismográfico quirúrgico (SPI) y asegúrese de incluirla al documentar
la práctica. En caso de utilizar modelos de IA generativa (e.g., ChatGPT) debe
verificar la información contra una fuente confiable (e.g., libros, manuales,
informes técnicos).



2. Diseñe y elabore un breve código en MATLAB que capture la señal resultante
del circuito construido en la parte A y calcule el SPI con cada pulsación o
latido. Utilice para ello un algoritmo de detección de máximos y mínimos. El
resultado deberá mostrarse en la ventana de comandos de MATLAB y la
captura se hará durante un tiempo finito, a elección del usuario.



3. Pídale a uno de los integrantes del grupo que coloque su dedo sobre el sensor
óptico y configure el código para una captura de 2 minutos. Cuando transcurran 40 segundos, el voluntario deberá ejecutar la maniobra “Cold
Pressor Test” (CPT) durante otros 40 segundos. Tome nota de los valores que
alcanza el SPI antes y durante la maniobra. Transcurrido este tiempo, el
voluntario volverá a las condiciones iniciales hasta completarse los 2 minutos.
Recuerde tomar nota también del valor SPI durante los últimos 40 segundos.



4. Modifique el código para, mediante una gráfica y al final de la captura, se
pueda visualizar la evolución del SPI en función del tiempo.


Parte C 

• Pregunta 1: ¿Cómo se relacionan las variaciones del volumen sanguíneo
periférico con el balance autonómico?

• Pregunta 2: ¿Cómo se compara el SPI con otros índices comúnmente
empleados en cirugía, como el índice nocicepción-analgesia (ANI) y el
índice de perfusión?

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
