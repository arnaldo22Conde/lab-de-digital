% ==============================
% Multivibrador Astable con BJT
% Ecuaciones + Diseño + Verificación (LTspice)
% ==============================

\section{Multivibrador astable con transistores (BJT)}

\subsection{Ecuaciones (caso general)}
Para un multivibrador astable no simétrico, los tiempos de cada semiciclo se aproximan por:
\begin{equation}
t_1=\ln(2)\,R_2C_1 \approx 0.693\,R_2C_1
\end{equation}
\begin{equation}
t_2=\ln(2)\,R_3C_2 \approx 0.693\,R_3C_2
\end{equation}

El período total es la suma:
\begin{equation}
T=t_1+t_2=\ln(2)\,(R_2C_1+R_3C_2)
\end{equation}

Por lo tanto, la frecuencia resulta:
\begin{equation}
\boxed{
f=\frac{1}{T}=\frac{1}{\ln(2)\,(R_2C_1+R_3C_2)}
}
\end{equation}

\subsection{Ecuaciones (caso simétrico)}
Si el circuito es simétrico:
\[
R_2=R_3=R,\qquad C_1=C_2=C
\]
entonces:
\begin{equation}
T=\ln(2)\,(RC+RC)=2\ln(2)\,RC
\end{equation}
\begin{equation}
\boxed{
f=\frac{1}{2\ln(2)\,RC}\approx\frac{1}{1.386\,RC}
}
\end{equation}

\section{Selección de $R_1$ (resistencia del colector / LED)}
La resistencia $R_1$ se elige para limitar la corriente del LED (o de colector) cuando el transistor satura.
\begin{equation}
\boxed{
R_1=\frac{V_{CC}-V_{LED}-V_{CE(sat)}}{I_{LED}}
}
\end{equation}

Donde típicamente:
\[
V_{CE(sat)}\approx 0.2\,\text{V},\quad
V_{LED}\approx 3.0\text{--}3.3\,\text{V (azul)},\quad
V_{LED}\approx 1.8\text{--}2.0\,\text{V (rojo)}
\]
y $I_{LED}$ suele elegirse entre $2$ mA y $10$ mA para LEDs indicadores.

\section{Selección del capacitor a partir de la frecuencia requerida}
\subsection{Despeje de $C$ (caso simétrico)}
Partiendo de:
\[
f=\frac{1}{2\ln(2)\,RC}
\]
se despeja $C$ como:
\begin{equation}
\boxed{
C=\frac{1}{2\ln(2)\,R\,f}
}
\end{equation}
o usando $2\ln(2)\approx 1.386$:
\begin{equation}
\boxed{
C=\frac{1}{1.386\,R\,f}
}
\end{equation}

\subsection{Despeje de $C_2$ (caso no simétrico, opcional)}
Si se conoce $R_2,R_3,C_1$ y se desea despejar $C_2$ desde:
\[
f=\frac{1}{\ln(2)\,(R_2C_1+R_3C_2)}
\]
entonces:
\begin{equation}
\boxed{
C_2=\frac{\frac{1}{f\ln(2)}-R_2C_1}{R_3}
}
\end{equation}

\section{Verificación de frecuencia en LTspice mediante $N$ ciclos}
En la simulación transitoria, si entre dos instantes $t_a$ y $t_b$ se observan $N$ ciclos completos, entonces:
\begin{equation}
\Delta t=t_b-t_a
\end{equation}
\begin{equation}
T=\frac{\Delta t}{N}
\end{equation}
\begin{equation}
\boxed{
f=\frac{1}{T}=\frac{N}{\Delta t}
}
\end{equation}

\subsection{Ejemplo de verificación (2 ciclos)}
Si entre $6.5$ ms y $9$ ms se observan $2$ ciclos:
\[
\Delta t = 9\,\text{ms}-6.5\,\text{ms}=2.5\,\text{ms}=0.0025\,\text{s}
\]
\begin{equation}
f=\frac{N}{\Delta t}=\frac{2}{0.0025}=800\,\text{Hz}
\end{equation}

\section{Nota para el informe}
La frecuencia teórica se obtiene a partir de las expresiones anteriores (según el caso simétrico o no simétrico) y se contrasta con la medición en LTspice usando la relación $f=N/\Delta t$ a partir de los cursores en la forma de onda.
