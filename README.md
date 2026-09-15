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

<b>Figura 3.</b> Sensor óptico de reflectancia basado en el optoacoplador TCST110.
</p>


Como se mencionó anteriormente se usó el sensor TCST1103 el cual sí fue modificado físicamente para convertirlo de su configuración original transmisiva a una configuración de reflectancia, tal como se ilustra en la Figura 3, el emisor y el receptor infrarrojo, que originalmente están enfrentados a través de la ranura del optoacoplador, se separaron y reorientaron para quedar dispuestos lado a lado, apuntando ambos hacia la misma dirección. De esta manera, en lugar de que la luz emitida atraviese el dedo para ser captada al otro lado, la luz incide sobre el dedo y es la porción reflejada por el tejido la que llega al fototransistor receptor.

Este sensor ya modificado se montó dentro de una carcasa de cartón construida a la medida (Figura 4), con el TCST1103 fijo en la base y una abertura superior por la cual el voluntario introduce el dedo, apoyándolo sobre el sensor. La carcasa cumple dos funciones ya que mantiene el dedo en una posición fija y constante sobre el par emisor-receptor, evitando que el movimiento degrade la señal reflejada, y bloquea la entrada de luz ambiente, la cual de otro modo se sumaría como interferencia a la señal óptica de interés, dado que el fototransistor no distingue entre la luz infrarroja reflejada por el dedo y cualquier otra fuente de luz externa.

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

El paso siguiente consistía en conectar la salida analógica  del circuito a una entrada analógica del microcontrolador y verificar mediante el Monitor y Graficador Serial de Arduino IDE, que se obtuviera una señal pletismográfica reconocible, ajustando los potenciómetros del amplificador para lograr la forma de onda más limpia posible.

Al realizar esta conexión, no se logró observar ninguna señal en el Graficador Serial, lo cual no se debía a que el sensor estuviera apagado o mal alimentado ya que se confirmó, usando la cámara de un celular que el diodo emisor efectivamente estaba encendido, deduciendo así que la etapa óptica del sensor funcionaba correctamente, pero la señal no llegaba de forma utilizable hasta la entrada analógica del ESP32, lo que indicaba un problema en la etapa de acondicionamiento  o en su acople con el rango de lectura del ADC del microcontrolador. Ante esta dificultad, se optó por reemplazar la adquisición basada en el circuito por el módulo integrado MAX30102, el cual es es un sensor de pulsioximetría que integra en un solo chip el LED emisor (rojo e infrarrojo), el fotodetector y todo el front-end analógico (amplificación, filtrado y conversión analógico-digital), entregando directamente por comunicación digital un valor numérico proporcional a la luz reflejada por el tejido [2]. Esto elimina la necesidad de construir y calibrar manualmente las etapas de amplificación y filtrado del circuito discreto, ya que el propio módulo resuelve internamente esa parte del acondicionamiento de la señal.

El MAX30102 se conectó por  I2C a la ESP32-S3-N16R8, usando SDA = GPIO8 y SCL = GPIO9, y se manejó mediante la librería SparkFun MAX30105. La configuración utilizada en Arduino IDE fue la siguiente:

<img width="1600" height="1204" alt="image" src="https://github.com/user-attachments/assets/3177ff6e-2eac-41ee-8d02-9091cf82f592" />

<b>Figura 5.</b> Circuito de Adquisición con MAX30102.
</p>


```
#include <Wire.h>
#include "MAX30105.h"

MAX30105 particleSensor;

#define SDA_PIN 8
#define SCL_PIN 9

void setup() {
  Serial.begin(115200);
  Wire.begin(SDA_PIN, SCL_PIN);      // SDA=8, SCL=9

  if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
    Serial.println("MAX30102 no detectado. Revisa el cableado.");
    while (1);
  }

  particleSensor.setup(0x1F, 4, 2, 100, 411, 4096);
  // ledBrightness, sampleAverage, ledMode(2=Red+IR), sampleRate, pulseWidth, adcRange
}

void loop() {
  long irValue = particleSensor.getIR();
  Serial.println(irValue);
}
```


<img width="1917" height="1020" alt="RESPUESTA_EN_ARDUINO" src="https://github.com/user-attachments/assets/b9ffedf7-4620-4543-aada-edc7b0082871" />

<b>Figura 6.</b> Respuesta en el Serial Plotter .
</p>

Con esta configuración, el Monitor y Graficador Serial mostró de inmediato una señal de gran amplitud y claramente periódica superior en estabilidad a lo que se había obtenido con el circuito. Se verificó, sin embargo, que en esta señal cruda los picos sistólicos aparecían como valles (mínimos locales) en lugar de máximos, por lo que  se decidió invertir la señal  antes de cualquier procesamiento posterior en MATLAB, de modo que los picos sistólicos quedaran representados como máximos y pudieran procesarse con el algoritmo de detección de picos.

4. Investigue sobre la técnica “Cold Pressor Test” (CPT), en qué consiste y cómo
aplicarla en el laboratorio.

El Cold Pressor Test (CPT) es una maniobra experimental clásica para inducir dolor y estrés fisiológico de forma controlada en el laboratorio. Fue descrita originalmente en la década de 1930 por Hines y Brown como un método para estudiar la reactividad vasomotora y predecir el desarrollo de hipertensión, y desde entonces se ha adoptado ampliamente tanto en investigación del dolor como en estudios de estrés fisiológico [3]. Consiste en sumergir una extremidad típicamente la mano o el antebrazo en agua fría durante un tiempo determinado. Aunque no existe un protocolo único y universal , la revisión de Fanninger et al. encontró que la temperatura más comúnmente reportada en la literatura es de 1 °C, con tiempos de inmersión que suelen oscilar entre 60 y 180 segundos [3]. Otros estudios que emplean la técnica con fines distintos usan parámetros diferentes; por ejemplo, en un estudio sobre modulación condicionada del dolor se sumergió el antebrazo en agua a 10 °C durante 120 s [7], lo que confirma que la temperatura exacta es un parámetro ajustable según el propósito del experimento, siempre que se mantenga fija y se documente.

Desde el punto de vista fisiológico, la inmersión en agua fría activa los nociceptores de la piel, que transmiten señales de dolor agudo a través de fibras A-δ y C hacia la corteza somatosensorial. De forma simultánea, el estímulo frío activa el sistema nervioso simpático (SNS), lo que produce un aumento de la frecuencia cardíaca, la presión arterial y la frecuencia respiratoria; de hecho, el incremento de presión arterial que caracteriza esta respuesta la "respuesta presora" es precisamente el origen del nombre de la prueba [3]. A diferencia de otros protocolos de estrés como el Trier Social Stress Test (TSST), que involucra principalmente un componente psicológico evaluativo y activa con fuerza el eje hipotálamo-hipófisis-adrenal, el CPT es ante todo un estresor físico directo que actúa sobre todo por la vía simpático-adrenal, con una activación del eje HPA comparativamente menor [5].

Para el sistema de adquisición basado en PPG que se construyó en esta práctica, el efecto más relevante del CPT es el que produce sobre la circulación periférica, ya que  el frío desencadena vasoconstricción, lo que reduce el diámetro de los vasos sanguíneos y aumenta su tono, disminuyendo el flujo sanguíneo cutáneo y el volumen sistólico. Como la amplitud de la onda PPG depende directamente de las variaciones de volumen sanguíneo en el tejido, esta vasoconstricción se traduce en una reducción de la amplitud de pulso (PPGA), e incluso puede llegar a degradar considerablemente la relación señal-ruido de la señal PPG durante la maniobra [4]. Este mecanismo es exactamente el que permite calcular el SPI como indicador indirecto de la respuesta autonómica, de hecho Hamunen et al. demostraron experimentalmente que, de varios estímulos dolorosos comparados (calor a 43 °C, calor a 48 °C y CPT), fue precisamente la intensidad del dolor inducido por el CPT la que correlacionó de forma significativa con los cambios en PPGA, frecuencia cardíaca y SPI derivados de la fotopletismografía, validando el uso de esta maniobra junto con parámetros derivados del PPG como los que se calculan en este laboratorio [6].

En el contexto de esta práctica, la aplicación del CPT consistió en sumergir la mano del voluntario en agua fría durante los 40 segundos centrales de la captura de 2 minutos, inmediatamente después de un período de reposo inicial que sirvió como línea base, y seguida de un período de recuperación de igual duración. Este diseño permite observar tanto la respuesta aguda durante la inmersión como la fase de recuperación posterior, en la que la literatura reporta fenómenos adicionales como la hiperemia reactiva.

Parte B

1. Revise la literatura relacionada para encontrar la definición matemática del
índice pletismográfico quirúrgico (SPI) y asegúrese de incluirla al documentar
la práctica. En caso de utilizar modelos de IA generativa (e.g., ChatGPT) debe
verificar la información contra una fuente confiable (e.g., libros, manuales,
informes técnicos).

El índice pletismográfico quirúrgico (Surgical Pleth Index, SPI) es una herramienta de monitoreo desarrollada originalmente por GE Healthcare para estimar, de forma objetiva y no invasiva, el balance entre la nocicepción y la analgesia durante cirugías bajo anestesia general, a partir de la señal fotopletismográfica obtenida en la arteriola del dedo [8]. Según la definición reportada en la literatura, el SPI se calcula mediante la siguiente expresión:

$$
SPI = 100 - (0.33 \times HBI_{norm} + 0.67 \times PPGA_{norm})                [8].
$$

donde HBI (heartbeat interval) es el intervalo entre latidos consecutivos y PPGA (photoplethysmographic waveform amplitude) es la amplitud pico-valle de la onda de pulso fotopletismográfica, ambos normalizados a una escala de 0 a 100 antes de aplicarse en la fórmula [8]. El resultado es un índice que también varía entre 0 y 100, donde valores más altos indican una mayor respuesta nociceptiva; en el contexto clínico original, se considera que un rango adecuado de analgesia intraoperatoria corresponde a valores de SPI entre 20 y 50, y se recomienda evitar incrementos abruptos superiores a 10 unidades [8].

El mecanismo fisiológico detrás de esta fórmula se basa es que un estímulo nociceptivo (por ejemplo, un estímulo quirúrgico, o en nuestro caso el Cold Pressor Test) incrementa el tono simpático, lo cual produce simultáneamente un aumento de la frecuencia cardíaca y por tanto una disminución del HBI y un aumento del tono vascular por vasoconstricción periférica lo que reduce la PPGA. Como ambos términos disminuyen y se restan de 100, el efecto neto es un incremento del valor del SPI [8]. Esta es precisamente la relación que se buscó reproducir con el sistema de adquisición propio construido, y la que permite interpretar fisiológicamente los resultados obtenidos con el Cold Pressor Test.


2. Diseñe y elabore un breve código en MATLAB que capture la señal resultante
del circuito construido en la parte A y calcule el SPI con cada pulsación o
latido. Utilice para ello un algoritmo de detección de máximos y mínimos. El
resultado deberá mostrarse en la ventana de comandos de MATLAB y la
captura se hará durante un tiempo finito, a elección del usuario.

El algoritmo de detección de picos: MMPD (Mountaineer's Method for Peak Detection)

Para este laboratorio se investigó en la literatura un algoritmo de detección de máximos y mínimos adecuado para señales fotopletismográficas, encontrando el método MMPD, propuesto originalmente por Argüello-Prada en un artículo dedicado a describir esta técnica [9]. A diferencia de los algoritmos clásicos de detección de picos que dependen de un umbral de amplitud. el MMPD identifica los pulsos sistólicos a partir de la forma temporal del frente de subida de cada pulso ya que  se cuenta el número de muestras consecutivas en las que la señal presenta pendiente positiva, y cuando la señal deja de subir, esa duración se compara contra la duración de la subida que dio origen al pico confirmado inmediatamente anterior. Un nuevo máximo se acepta como pico sistólico válido únicamente si la duración de su subida es igual o mayor al 60 % de la duración de la subida anterior, en caso contrario se descarta como un evento a lo que se se considera como ruido o artefacto [9].

Esta lógica  de evaluar cada ciclo contra el historial reciente de ciclos ya confirmados, en lugar de contra un umbral absoluto es consistente con el nombre de la técnica, de la misma forma en que un montañista evalúa cada nuevo tramo de ascenso en relación con el esfuerzo del tramo anterior, el algoritmo evalúa cada subida sistólica en relación con la inmediatamente precedente. Esta característica resultó especialmente relevante para el diseño experimental de este laboratorio debido a que durante el Cold Pressor Test, la amplitud del pulso (PPGA) cambia deliberadamente como parte del fenómeno fisiológico que se busca medir (la vasoconstricción reduce la PPGA), por lo que un criterio de detección basado en un umbral de amplitud fija habría fallado  justo en el tramo más importante de la captura. Al depender únicamente de la forma temporal del frente de subida una característica que se conserva incluso cuando la amplitud del pulso disminuye, el MMPD permite seguir detectando los pulsos de forma confiable durante toda la maniobra.

La validez y utilidad práctica de este algoritmo cuentan con respaldo adicional en la literatura reciente. Por un lado, ha sido empleado exitosamente en sistemas de monitoreo continuo basados en PPG para tareas distintas a la detección de latidos, como la detección de habla en pacientes encamados a partir de las variaciones inducidas en la señal de pulso [10]. Por otro lado, su desempeño fue evaluado formalmente y comparado de manera cuantitativa contra otros algoritmos de referencia para la detección de latidos en señales PPG  incluyendo el propio MSPTD/MSPTDfast en un estudio de benchmarking publicado en Physiological Measurement [11]. Este último trabajo confirma que el MMPD se encuentra entre los algoritmos con menor tiempo de ejecución dentro de los evaluados, lo cual es coherente con su uso en este laboratorio dentro de un ciclo de procesamiento en tiempo real (muestra por muestra) sobre un microcontrolador de bajo costo.

Una vez identificado cada pico sistólico, la amplitud pico-valle (PPGA) del candidato debe superar el 25 % de la mediana de los PPGA ya confirmados como válidos recientemente. Este criterio complementario, calculado sobre el propio historial de pulsos confirmados y no sobre un umbral absoluto de la señal cruda, sigue la misma condición adaptativa del MMPD y permite filtrar artefactos de baja amplitud sin comprometer la sensibilidad del algoritmo ante los cambios reales de PPGA inducidos por el CPT.


```
clear; clc; close all;


puerto     = "COM3";
baudrate   = 115200;
t_captura  = 120;   
t_fase1    = 40;     
t_fase2    = 80;     
t_baseline = 15;    
t_warmup   = 2;      
ruta_salida = 'C:\Users\brafe\septimo_semestre\laboratorio_instrumentacion\lab3\toma_v2';
if ~exist(ruta_salida, 'dir'); mkdir(ruta_salida); end

beta_baseline    = 0.03;
gamma_suavizado  = 0.4;
frac_prominencia = 0.25;
n_min_bootstrap  = 3;

s = serialport(puerto, baudrate);
s.Timeout = 5;
flush(s);


N_seed = 15;
IR_MIN_PLAUSIBLE = 1e3;   
IR_MAX_PLAUSIBLE = 3e5;  
seed_vals = [];
while numel(seed_vals) < N_seed
    raw = readline(s);
    ir  = str2double(raw);
    if isnan(ir) || abs(ir) < IR_MIN_PLAUSIBLE || abs(ir) > IR_MAX_PLAUSIBLE
        continue;  
    end
    seed_vals(end+1) = -ir; %#ok<AGROW>
end
baseline = median(seed_vals);
suave    = 0;


fig = figure('Name','Captura en vivo - Protocolo CPT','NumberTitle','off');
ax1 = subplot(2,1,1);
hRaw  = animatedline(ax1, 'Color', [0.6 0.6 0.6]);
hFilt = animatedline(ax1, 'Color', [0 0.45 0.74], 'LineWidth', 1.3);
ylabel(ax1, 'Amplitud (u.a.)'); grid(ax1,'on'); xlim(ax1, [0 t_captura]);
title(ax1, 'Cruda (gris) vs. filtrada (azul) en tiempo real');
legend(ax1, {'Cruda invertida','Filtrada (pulsátil)'}, 'Location','best');
xline(ax1, t_fase1, '--m', 'Inicio CPT');
xline(ax1, t_fase2, '--m', 'Fin CPT');

ax2 = subplot(2,1,2);
hSPI = animatedline(ax2, 'Color', [0.85 0.1 0.1], 'Marker', 'o', 'LineStyle', '-');
ylim(ax2, [0 100]); xlim(ax2, [0 t_captura]);
ylabel(ax2, 'SPI'); xlabel(ax2, 'Tiempo (s)'); grid(ax2,'on');
title(ax2, 'SPI por pulso (líneas rosadas = ventana del CPT)');
xline(ax2, t_fase1, '--m', 'Inicio CPT');
xline(ax2, t_fase2, '--m', 'Fin CPT');


contador_subida = 0;
umbral_subida   = 8;
ultimo_pico_t   = NaN;
valor_minimo    = Inf;
t_valor_minimo  = NaN;

t_hist = []; raw_hist = []; filt_hist = [];
pico_t = []; pico_v = [];  valle_t = []; valle_v = [];

HBI_hist = []; PPGA_hist = [];
spi_vals = []; spi_t = [];

base_HBI_rango = []; base_PPGA_rango = [];
calibrado = false;

n_candidatos          = 0;
n_rechazo_prominencia = 0;
n_rechazo_hbi         = 0;

aviso_fase1_dado = false;
aviso_fase2_dado = false;

fprintf('Iniciando captura de %d s (protocolo CPT: 0-%d reposo | %d-%d CPT | %d-%d reposo)...\n', ...
    t_captura, t_fase1, t_fase1, t_fase2, t_fase2, t_captura);
tRef = tic;
suave_ant = NaN;

while toc(tRef) < t_captura
    raw = readline(s);
    ir  = str2double(raw);
    if isnan(ir); continue; end

    t_actual = toc(tRef);
    muestra  = -ir;

  
    if ~aviso_fase1_dado && t_actual >= t_fase1
        aviso_fase1_dado = true;
        beep;
        fprintf('\n*** t = %.1f s: APLIQUE EL COLD PRESSOR TEST AHORA (40 s) ***\n\n', t_actual);
    end
    if ~aviso_fase2_dado && t_actual >= t_fase2
        aviso_fase2_dado = true;
        beep;
        fprintf('\n*** t = %.1f s: FIN DEL CPT — VUELVA A LA CONDICIÓN DE REPOSO (40 s) ***\n\n', t_actual);
    end

    baseline = baseline + beta_baseline*(muestra - baseline);
    hp       = muestra - baseline;
    suave    = suave + gamma_suavizado*(hp - suave);

    t_hist(end+1)    = t_actual;
    raw_hist(end+1)  = muestra;
    filt_hist(end+1) = suave;
    addpoints(hRaw,  t_actual, muestra);
    addpoints(hFilt, t_actual, suave);

    dt_prom = t_actual / numel(t_hist);

    if suave < valor_minimo
        valor_minimo   = suave;
        t_valor_minimo = t_actual;
    end

    if ~isnan(suave_ant)
        if suave > suave_ant
            contador_subida = contador_subida + 1;
        else
            if contador_subida >= umbral_subida && t_actual >= t_warmup
                n_candidatos = n_candidatos + 1;

                idx_pico = numel(filt_hist) - 1;
                t_pico   = t_hist(idx_pico);
                v_pico   = filt_hist(idx_pico);
                PPGA_filt = v_pico - valor_minimo;

                if numel(PPGA_hist) >= n_min_bootstrap
                    prominencia_min = frac_prominencia * median(PPGA_hist(max(1,end-9):end));
                else
                    prominencia_min = 0;
                end

                if PPGA_filt > prominencia_min
                    pico_t(end+1)  = t_pico;  pico_v(end+1)  = v_pico; %#ok<AGROW>
                    valle_t(end+1) = t_valor_minimo; valle_v(end+1) = valor_minimo; %#ok<AGROW>

                    if ~isnan(ultimo_pico_t)
                        HBI  = t_pico - ultimo_pico_t;
                        PPGA = PPGA_filt;

                        salto_amplitud_ok = isempty(PPGA_hist) || ...
                            PPGA < 5*median(PPGA_hist(max(1,end-9):end));

                        if HBI > 0.3 && HBI < 2 && salto_amplitud_ok
                            HBI_hist(end+1)  = HBI;  %#ok<AGROW>
                            PPGA_hist(end+1) = PPGA; %#ok<AGROW>

                            if ~calibrado && t_pico >= t_baseline && numel(HBI_hist) >= 5
                                base_HBI_rango  = [min(HBI_hist),  max(HBI_hist)];
                                base_PPGA_rango = [min(PPGA_hist), max(PPGA_hist)];
                                calibrado = true;
                                fprintf('--- Línea base calibrada en t = %.1f s ---\n', t_pico);
                            end

                            if calibrado
                                HBI_norm  = max(0,min(100, 100*(HBI -base_HBI_rango(1)) /(diff(base_HBI_rango) +eps)));
                                PPGA_norm = max(0,min(100, 100*(PPGA-base_PPGA_rango(1))/(diff(base_PPGA_rango)+eps)));
                                SPI = 100 - (0.33*HBI_norm + 0.67*PPGA_norm);

                                spi_vals(end+1) = SPI; spi_t(end+1) = t_pico; %#ok<AGROW>
                                addpoints(hSPI, t_pico, SPI);
                                fprintf('t = %5.1f s | HBI = %.3f s | PPGA = %.1f | SPI = %.1f\n', t_pico, HBI, PPGA, SPI);
                            else
                                fprintf('t = %5.1f s | HBI = %.3f s | PPGA = %.1f | (calibrando línea base...)\n', t_pico, HBI, PPGA);
                            end
                        else
                            n_rechazo_hbi = n_rechazo_hbi + 1;
                        end
                    end
                    ultimo_pico_t = t_pico;

                    umbral_min = max(3, round(0.06/dt_prom));
                    umbral_max = max(umbral_min+2, round(0.6/dt_prom));
                    umbral_subida = min(umbral_max, max(umbral_min, round(0.6*contador_subida)));
                else
                    n_rechazo_prominencia = n_rechazo_prominencia + 1;
                end
                valor_minimo   = Inf;
                t_valor_minimo = NaN;
            end
            contador_subida = 0;
        end
    end

    suave_ant = suave;
    drawnow limitrate;
end

clear s
fprintf('\nCaptura finalizada. Duración real: %.1f s | Pulsos válidos: %d\n', toc(tRef), numel(spi_vals));
fprintf('Diagnóstico -> candidatos: %d | rechazados por prominencia: %d | rechazados por HBI/salto: %d\n', ...
    n_candidatos, n_rechazo_prominencia, n_rechazo_hbi);


seg_reposo1 = spi_vals(spi_t <  t_fase1);
seg_cpt     = spi_vals(spi_t >= t_fase1 & spi_t < t_fase2);
seg_reposo2 = spi_vals(spi_t >= t_fase2);

fprintf('\n--- RESUMEN POR FASE ---\n');
fprintf('Reposo inicial (0-%ds):   SPI medio = %6.1f | mín = %5.1f | máx = %5.1f | n = %d\n', ...
    t_fase1, mean(seg_reposo1), min(seg_reposo1), max(seg_reposo1), numel(seg_reposo1));
fprintf('Cold Pressor Test (%d-%ds): SPI medio = %6.1f | mín = %5.1f | máx = %5.1f | n = %d\n', ...
    t_fase1, t_fase2, mean(seg_cpt), min(seg_cpt), max(seg_cpt), numel(seg_cpt));
fprintf('Reposo final (%d-%ds):    SPI medio = %6.1f | mín = %5.1f | máx = %5.1f | n = %d\n', ...
    t_fase2, t_captura, mean(seg_reposo2), min(seg_reposo2), max(seg_reposo2), numel(seg_reposo2));
fprintf('Delta SPI (CPT - reposo inicial) = %.1f\n', mean(seg_cpt) - mean(seg_reposo1));
fprintf('Delta SPI (reposo final - CPT)   = %.1f\n', mean(seg_reposo2) - mean(seg_cpt));


figFinal = figure('Name','Captura completa - Protocolo CPT','NumberTitle','off','Position',[100 100 900 750]);

subplot(3,1,1);
plot(t_hist, raw_hist, 'Color', [0.6 0.6 0.6]); hold on;
xline(t_fase1, '--m', 'Inicio CPT'); xline(t_fase2, '--m', 'Fin CPT');
xlabel('Tiempo (s)'); ylabel('u.a.'); title('Señal cruda invertida'); grid on;

subplot(3,1,2);
plot(t_hist, filt_hist, 'Color', [0 0.45 0.74]); hold on;
plot(pico_t, pico_v, 'g^', 'MarkerFaceColor','g');
plot(valle_t, valle_v, 'rv', 'MarkerFaceColor','r');
xline(t_fase1, '--m', 'Inicio CPT'); xline(t_fase2, '--m', 'Fin CPT');
legend('Señal filtrada','Picos sistólicos','Valles','Location','best');
xlabel('Tiempo (s)'); ylabel('u.a.'); title('Señal filtrada con picos/valles detectados'); grid on;

if ~isempty(pico_v)
    ylim_filt = [min([valle_v, pico_v]), max([valle_v, pico_v])];
    margen = 0.2 * max(range(ylim_filt), 1);
    ylim(ylim_filt + [-margen, margen]);
end

subplot(3,1,3);
plot(spi_t, spi_vals, '-o', 'Color', [0.85 0.1 0.1], 'MarkerFaceColor', [0.85 0.1 0.1]); hold on;
yline(50, '--k', 'SPI = 50');
xline(t_fase1, '--m', 'Inicio CPT'); xline(t_fase2, '--m', 'Fin CPT');
ylim([0 100]);
xlabel('Tiempo (s)'); ylabel('SPI'); title('Evolución del SPI (reposo | CPT | reposo)'); grid on;


nombre_base = fullfile(ruta_salida, ['captura_CPT_' datestr(now,'yyyymmdd_HHMMSS')]);
exportgraphics(figFinal, [nombre_base '.png'], 'Resolution', 300);
save([nombre_base '.mat'], 't_hist','raw_hist','filt_hist','pico_t','pico_v', ...
     'valle_t','valle_v','spi_t','spi_vals','HBI_hist','PPGA_hist', ...
     'seg_reposo1','seg_cpt','seg_reposo2','t_fase1','t_fase2');
fprintf('\nGráfica guardada en: %s.png\nDatos guardados en:  %s.mat\n', nombre_base, nombre_base);

```


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

[2] J. Simões, R. Oliveira, F. M. Costa, A. Teixeira, C. Leitão, P. Correia, and A. L. M. Silva, "Non-Intrusive Monitoring of Vital Signs in the Lower Limbs Using Optical Sensors," Sensors (Basel), vol. 25, no. 2, art. 305, 2025. doi: 10.3390/s25020305.

[3] S. Fanninger, P. L. Plener, M. J. M. Fischer, O. D. Kothgassner, and A. Goreis, "Water temperature during the cold pressor test: A scoping review," Physiol. Behav., vol. 271, art. 114354, 2023. doi: 10.1016/j.physbeh.2023.114354.

[4] J. Herranz Olazabal, I. Lorato, J. Kling, M. Verhoeven, F. Wieringa, C. Van Hoof, W. Verkruijsse, and E. Hermeling, "Comparison between speckle plethysmography and photoplethysmography during cold pressor test referenced to finger arterial pressure," Sensors, vol. 23, no. 11, art. 5016, 2023. doi: 10.3390/s23115016.

[5] M. Koriakina, M. Lukov, U. Nikishkina, A. Kirsanov, E. Dmitrieva, and E. Blagovechtchenski, "Social and physiological stress elicit divergent psycho-physiological dynamics and motor cortex activation," Front. Psychol., vol. 17, art. 1760772, 2026. doi: 10.3389/fpsyg.2026.1760772.

[6] K. Hamunen, V. Kontinen, E. Hakala, P. Talke, M. Paloheimo, and E. Kalso, "Effect of pain on autonomic nervous system indices derived from photoplethysmography in healthy volunteers," Br. J. Anaesth., vol. 108, no. 5, pp. 838–844, 2012. doi: 10.1093/bja/aes001.

[7] M. Vincenot, M. Roberge, C.-É. Giguère, and S. Potvin, "Conditioned pain modulation and pleasant pain relief as complementary processes reflecting individual differences in pain coping: a clustering approach," Eur. J. Pain, vol. 30, no. 8, art. e70366, 2026. doi: 10.1002/ejp.70366.

[8] S. K. Oh, Y. J. Won, and B. G. Lim, "Surgical pleth index monitoring in perioperative pain management: usefulness and limitations," Korean J. Anesthesiol., vol. 77, no. 1, pp. 31–45, 2024. doi: 10.4097/kja.23158.

[9] E. J. Argüello-Prada, M. A. Dávalos Cantín, and J. C. Victoria, "A photoplethysmography-based system for talking detection in bedridden patients," Biomed. Signal Process. Control, vol. 81, art. 104477, 2023. doi: 10.1016/j.bspc.2022.104477.

[10] P. H. Charlton, E. J. Argüello-Prada, J. Mant, and P. A. Kyriacou, "The MSPTDfast photoplethysmography beat detection algorithm: design, benchmarking, and open-source distribution," Physiol. Meas., vol. 46, art. 035002, 2025. doi: 10.1088/1361-6579/adb89e.

[11] M. Arevalillo-Herráez, Y. Wu, B. Tilbury, and N. Ramzan, "Motion-based confidence score to support the practical application of rPPG methods in health monitoring," J. Med. Syst., vol. 50, no. 1, 2026. doi: 10.1007/s10916-026-02412-2.
