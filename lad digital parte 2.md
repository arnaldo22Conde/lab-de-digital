# Generación y control de tiempos (temporización):

## Estudie el oscilador astable basado en trasistores e implemente un oscilador que genere una salida entre 0 a 3.3 voltios o entre 0 a 5 voltios a una frecuencia de 1 KHz, puede usar una tecnología mosfet o bjt.
## Estudie el LM555 en sus tres modos de operación (monoestable, bistable, astable.) y realice la implementación de un oscilador astable con las mismas características con las que implementó el oscilador basado en transistores (frecuencia y voltaje de salida).
## Compare los resultados obtenidos y realice una comparativa de ambas implementaciones indicando las diferentes aplicaciones.

# Desarrollo.
## Estudie el oscilador astable basado en trasistores e implemente un oscilador que genere una salida entre 0 a 3.3 voltios o entre 0 a 5 voltios a una frecuencia de 1 KHz, puede usar una tecnología mosfet o bjt.
 
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

Verificación de la frecuencia en la simulación (LTspice)

Para verificar la frecuencia en la simulación se mide el tiempo que tarda en repetirse la señal. Si se observan N ciclos dentro de un intervalo de tiempo $\Delta t$, la frecuencia se calcula como:

$f = \frac{N}{\Delta t}$

Ejemplo de verificación

Si en la simulación se observan 2 ciclos entre 6.5 ms y 9 ms:

$\Delta t = 9,ms - 6.5,ms = 2.5,ms$

Entonces la frecuencia es:

$f = \frac{2}{0.0025} = 800,Hz$

Esto confirma el valor obtenido en la simulación.
