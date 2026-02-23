# Generación y control de tiempos (temporización):

## 1. Estudie el oscilador astable basado en trasistores e implemente un oscilador que genere una salida entre 0 a 3.3 voltios o entre 0 a 5 voltios a una frecuencia de 1 KHz, puede usar una tecnología mosfet o bjt.
## 2. Estudie el LM555 en sus tres modos de operación (monoestable, bistable, astable.) y realice la implementación de un oscilador astable con las mismas características con las que implementó el oscilador basado en transistores (frecuencia y voltaje de salida).
## 3. Compare los resultados obtenidos y realice una comparativa de ambas implementaciones indicando las diferentes aplicaciones.

# Desarrollo.
## 1. Estudie el oscilador astable basado en trasistores e implemente un oscilador que genere una salida entre 0 a 3.3 voltios o entre 0 a 5 voltios a una frecuencia de 1 KHz, puede usar una tecnología mosfet o bjt.
 
### Multivibrador astable con transistores (BJT)
- Ecuaciones del circuito (caso general)
El funcionamiento del multivibrador astable se basa en la carga y descarga de los capacitores a través de las resistencias de base. El tiempo de cada semiciclo se aproxima por:

$t_1 = \ln(2),R_2C_1 \approx 0.693,R_2C_1$

$t_2 = \ln(2),R_3C_2 \approx 0.693,R_3C_2$

El período total de oscilación es la suma de ambos tiempos:

$T = t_1 + t_2 = \ln(2),(R_2C_1 + R_3C_2)$

Por lo tanto, la frecuencia de oscilación queda:

$f = \frac{1}{T} = \frac{1}{\ln(2),(R_2C_1 + R_3C_2)}$

Caso simétrico (más usado en el laboratorio)

Cuando el circuito es simétrico:

$R_2 = R_3 = R$
$C_1 = C_2 = C$

donde $R_2 = R_3 = R$ son resistencias de carga y por lo geneneral son 100 veces mas grande que $R_1 = R_4 = R$ ya que esto granatiza el perfento funcionamiento de los bjt. 

El período se simplifica a:

$T = 2\ln(2),RC$

Y la frecuencia queda:

$f = \frac{1}{2\ln(2),RC}$

Como $2\ln(2) \approx 1.386$, se usa comúnmente:

$f = \frac{1}{1.386,RC}$


Selección de la resistencia R1 (resistencia del LED / colector)

La resistencia R1 se elige para limitar la corriente del LED y asegurar la saturación del transistor. Se calcula mediante:

$R_1 = \frac{V_{CC} - V_{LED} - V_{CE(sat)}}{I_{LED}}$

Donde típicamente:

$V_{CE(sat)} \approx 0.2,V$

$V_{LED} \approx 3.2,V$ (LED azul)

$I_{LED}$ suele elegirse entre 2 mA y 10 mA.

Selección del capacitor a partir de la frecuencia requerida

Si se desea diseñar el circuito para una frecuencia específica, se despeja el capacitor a partir de la ecuación de frecuencia del caso simétrico:

$f = \frac{1}{1.386,RC}$

Despejando C:

$C = \frac{1}{1.386,R,f}$

Ejemplo de diseño

Si se requiere una frecuencia de $f = 1,kHz$ y se elige $R = 47,k\Omega$:

$C = \frac{1}{1.386 \times 47000 \times 1000}$

$C \approx 15,nF$

Por lo tanto, se selecciona un capacitor comercial cercano, como 15 nF.
hola


Montaje del circuito (LTspaice)
![Montaje del circuito (LTspice)](https://github.com/user-attachments/assets/5150c396-04e1-4fb4-8bd4-ee002d188c77)

Verificación de la frecuencia en la simulación (LTspice)
![Verificación de la frecuencia en la simulación (LTspice)](https://github.com/user-attachments/assets/38d214b8-32e4-4855-a63c-3b0e03cd9d50)



Para verificar la frecuencia en la simulación se mide el tiempo que tarda en repetirse la señal. Si se observan N ciclos dentro de un intervalo de tiempo $\Delta t$, la frecuencia se calcula como:

$f = \frac{N}{\Delta t}$

Ejemplo de verificación

Si en la simulación se observan 2 ciclos entre 6.5 ms y 9 ms:

$\Delta t = 9,ms - 6.5,ms = 2.5,ms$

Entonces la frecuencia es:

$f = \frac{2}{0.0025} = 800,Hz$


https://www.youtube.com/watch?v=_n8JR62jyOw

Esto confirma el valor obtenido en la simulación.

## 2. Estudie el LM555 en sus tres modos de operación (monoestable, bistable, astable.) y realice la implementación de un oscilador astable con las mismas características con las que implementó el oscilador basado en transistores (frecuencia y voltaje de salida).
Tiempo de activación del pulso

### A. Modo Monoestable con Temporizador 555
-El tiempo durante el cual la salida permanece activa está determinado por la constante de tiempo RC del circuito. Para el temporizador 555 en modo monoestable, el tiempo del pulso de salida se calcula mediante la expresión:

$T = 1.1 R C$

Donde:

$T$ es el tiempo de activación del pulso

$R$ es la resistencia de temporización

$C$ es el capacitor de temporización

Selección de valores de resistencia y capacitor

Para el montaje realizado se utilizaron los siguientes valores:

$R = 1 , k\Omega$

$C = 1 , \mu F$

Sustituyendo en la ecuación del tiempo:

$T = 1.1 (1000)(1 \times 10^{-6})$

$T = 1.1 \times 10^{-3}$

$T = 1.1 , ms$

Por lo tanto, la salida permanece activa durante aproximadamente 1.1 milisegundos después de recibir el pulso de disparo.

Resultado obtenido según la simulación

Al simular el circuito en LTspice se observó que, al aplicar un pulso de disparo en la entrada TRIG, la salida del temporizador cambia a estado alto y se mantiene activa durante aproximadamente 1.1 ms, lo cual coincide con el valor calculado teóricamente.

Esto confirma que el tiempo de activación del modo monoestable depende únicamente de los valores de la resistencia y el capacitor utilizados en el circuito.



![Modo monoestable](https://github.com/user-attachments/assets/86eefa70-a8c9-473d-bc64-1d2d19b52d30)
link https://www.build-electronic-circuits.com/circuit-calculator-conversion/555-timer-calculator/

### B. Modo Biestable con Temporizador 555
Introducción

En este montaje se implementó el temporizador 555 en modo biestable. Este modo se caracteriza porque el circuito tiene dos estados estables: un estado alto y un estado bajo. La salida permanece en uno de estos estados hasta que una señal externa la cambie.

Por esta razón se dice que el modo biestable permite almacenar información, ya que el circuito puede “recordar” si estaba encendido o apagado.

-Por qué el circuito almacena información

El temporizador 555 tiene internamente un flip-flop RS. Este elemento es el que permite guardar el estado de la salida.

Cuando se presiona el pulsador S1, el pin TRIG recibe un nivel bajo y el flip-flop se activa, haciendo que la salida pase a nivel alto y el LED se encienda.

Cuando se presiona el pulsador S2, el pin RESET recibe un nivel bajo, lo que desactiva el flip-flop y la salida pasa a nivel bajo, apagando el LED.

Lo importante es que, cuando se sueltan los pulsadores, el circuito mantiene su estado, ya que el flip-flop interno conserva la última condición aplicada.

Por qué se usan resistencias pull-up

Las resistencias R1 y R2 mantienen los pines del 555 en estado alto cuando los pulsadores no están presionados. Esto evita que el circuito cambie de estado por ruido eléctrico o señales indeseadas.

-Funcionamiento general

El comportamiento del circuito es el siguiente:

Presionar S1 → el LED se enciende y permanece encendido.

Presionar S2 → el LED se apaga y permanece apagado.

Si no se presiona ningún pulsador, el circuito mantiene su último estado.

Esto demuestra que el temporizador 555 en modo biestable funciona como un sistema de memoria simple, capaz de almacenar un bit de información.

![Modo monoestable](https://github.com/user-attachments/assets/95d075a0-c790-41c2-a150-649f574ab60c)


### C. Modo Astable con LM555 (1 kHz, 0–5 V)
-Introducción al montaje

En esta parte se implementó el temporizador LM555 en modo astable, el cual no tiene estados estables: la salida conmuta continuamente entre alto y bajo, generando una onda cuadrada. La frecuencia depende principalmente de los valores de dos resistencias y un capacitor.

-Ecuaciones de frecuencia (LM555 astable)

Para el LM555 en modo astable, el período total se define como la suma del tiempo alto y el tiempo bajo:

$T = t_{H} + t_{L}$

Donde:

$t_H = 0.693 (R_A + R_B) C$

$t_L = 0.693 (R_B) C$

Entonces:

$T = 0.693 (R_A + 2R_B) C$

La frecuencia se calcula como:

$f = \frac{1}{T}$

Por lo tanto:

$f = \frac{1}{0.693 (R_A + 2R_B) C}$

-Una forma equivalente (muy usada) es:

$f \approx \frac{1.44}{(R_A + 2R_B) C}$

Selección del capacitor a partir de la frecuencia deseada (despeje de C)

Si se requiere una frecuencia de $f = 1,kHz$, se despeja el capacitor desde:

$f = \frac{1}{0.693 (R_A + 2R_B) C}$

-Despejando:

$C = \frac{1}{0.693 (R_A + 2R_B) f}$

Consideración sobre el ciclo útil (duty cycle)

El ciclo útil en el 555 depende de:

$D = \frac{t_H}{T} = \frac{R_A + R_B}{R_A + 2R_B}$

Para acercarse a $50%$ se busca que $R_A$ sea muy pequeño comparado con $R_B$. Una forma práctica es elegir:

$R_B \approx 100 R_A$

Esto hace que $R_A$ influya muy poco y el duty se acerque a $50%$ (aunque en un 555 típico sin diodo nunca queda exactamente 50%).

-Ejemplo de diseño (1 kHz con 5 V)

Se toma un ejemplo con:

$R_A = 1,k\Omega$

$R_B = 100,k\Omega$

$f = 1000,Hz$

-Se calcula:

$C = \frac{1}{0.693 (R_A + 2R_B) f}$

$C = \frac{1}{0.693 (1k + 2\cdot 100k)\cdot 1000}$

$C = \frac{1}{0.693 (201000)\cdot 1000}$

$C \approx 7.2,nF$

Por lo tanto, se selecciona un valor comercial cercano (por ejemplo 6.8 nF o 8.2 nF) y luego se ajusta en simulación si se requiere más precisión.

Verificación de la frecuencia en LTspice (método con N ciclos)

Para verificar la frecuencia en la simulación se mide el tiempo que tarda en repetirse la señal. Si se observan $N$ ciclos dentro de un intervalo de tiempo $\Delta t$, la frecuencia se calcula como:

$f = \frac{N}{\Delta t}$

Ejemplo de verificación

-Si en la gráfica de LTspice se observan 2 ciclos entre 6.5 ms y 9 ms:

$\Delta t = 9,ms - 6.5,ms = 2.5,ms$

Pasando a segundos:

$\Delta t = 0.0025,s$

Entonces la frecuencia es:

$f = \frac{2}{0.0025} = 800,Hz$

Este valor se compara con el valor teórico calculado y, si es necesario, se ajustan $R_A$, $R_B$ o $C$ para aproximarse a $1,kHz$.
![Modo Astable](https://github.com/user-attachments/assets/15e50a47-47a8-42ef-b6c9-695ea032a3bc)


# 3. Comparación de resultados: Astable con transistores vs Astable con LM555
-1) Diferencia en ecuaciones (modelo teórico)
Astable con transistores (multivibrador)

En el caso simétrico ($R_2=R_3=R$ y $C_1=C_2=C$):

$f \approx \frac{1}{1.386RC}$

En caso general:

$f = \frac{1}{0.693(R_2C_1 + R_3C_2)}$

Interpretación: la frecuencia depende de dos ramas RC (una por cada semiciclo). El duty se acerca a 50% si el circuito es simétrico.

LM555 en modo astable

Con resistencias $R_A$, $R_B$ y capacitor $C$:

$f = \frac{1}{0.693(R_A + 2R_B)C} ;;; \approx \frac{1.44}{(R_A+2R_B)C}$

Tiempos:

$t_H = 0.693(R_A + R_B)C$

$t_L = 0.693(R_B)C$

Duty:

$D = \frac{R_A + R_B}{R_A + 2R_B}$

Interpretación: la frecuencia depende de una sola red RC, pero el duty queda condicionado por $R_A$ y $R_B$ (no queda exactamente 50% sin usar diodo u otra modificación).

-2) Señal de salida (amplitud y forma de onda)
Transistores

Salidas típicas en colectores: 0 a $V_{CC}$ (aprox).

Se observan picos/transitorios por el intercambio de carga en capacitores (normal).

Se obtienen dos salidas complementarias (una alta cuando la otra está baja).

LM555

Salida en pin 3: onda cuadrada más “limpia” y estable.

La amplitud se aproxima a 0–$V_{CC}$ dependiendo del tipo de 555 y la carga (bajo cargas fuertes puede no llegar perfecto a los extremos).

En general es más fácil obtener una salida útil directa.

-3) Estabilidad y precisión de frecuencia
Transistores

La frecuencia puede variar más por:

variación de $\beta$ del transistor

temperatura

tolerancia de capacitores

saturación y $V_{BE}$

Resultado: más dispersión entre cálculo teórico y simulación/real.

LM555

La frecuencia suele ser más repetible porque el 555 tiene:

comparadores internos con umbrales definidos (aprox $1/3V_{CC}$ y $2/3V_{CC}$)

descarga controlada por el transistor interno del pin 7

Resultado: más estabilidad y facilidad para ajustar a un valor objetivo.

-4) Velocidad de reacción / conmutación
Transistores

La conmutación puede ser rápida, pero si el transistor entra en saturación profunda aparecen tiempos de almacenamiento de carga (puede ralentizar el apagado).

A frecuencias moderadas como 1 kHz funciona sin problema.

LM555

Tiene etapas internas optimizadas para conmutar y descargar el capacitor.

La conmutación es consistente y generalmente más rápida/estable que un montaje discreto básico.

Conclusión práctica: para 1 kHz ambos funcionan bien, pero el 555 suele dar una respuesta más “controlada” y menos dependiente del transistor.

-5) Complejidad del circuito y facilidad de diseño
Transistores

Más componentes: 2 transistores + 2 capacitores + varias resistencias.

Muy útil para aprender realimentación y temporización RC.

Ajustar frecuencia a veces requiere ensayo porque el modelo ideal no siempre coincide.

LM555

Menos componentes: 1 CI + 2 resistencias + 1 capacitor (astable típico).

Diseño directo con fórmulas claras.

Fácil de ajustar.

-6) Consumo y eficiencia
Transistores

Dependiendo del diseño, puede consumir más (corrientes por ramas y saturación).

Buen desempeño si se diseña con corrientes pequeñas.

LM555

Depende del tipo:

555 bipolar consume más que CMOS

555 CMOS consume mucho menos

En general, para un montaje práctico el 555 es conveniente.


modos biestable https://www.youtube.com/watch?v=4EfFQS2afb0
modo monoestabl y astable https://www.youtube.com/watch?v=n15R_n_TshA
