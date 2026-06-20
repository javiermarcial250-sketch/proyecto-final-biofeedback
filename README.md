# Sistema de Biofeedback para el Control del Estrés (ECG + EEG)

Proyecto final de la materia [nombre de la materia] — Procesamiento de señales biomédicas y análisis en tiempo real.

Sistema que adquiere (a partir de un archivo de datos real grabado con BIOPAC), procesa y fusiona una señal de ECG y una señal de EEG para clasificar el estado de relajación/estrés del usuario en tiempo real, mostrando el resultado mediante un "Semáforo de Relajación" en una interfaz gráfica (GUI).

## Descripción general

- **Señal ECG** (derivación II): se detectan los picos R y se calcula la Variabilidad de la Frecuencia Cardíaca (HRV) mediante las métricas RMSSD y LF/HF.
- **Señal EEG** (derivación frontal Fz/Cz): se aísla la banda Alfa (8–13 Hz) y se calcula su potencia espectral mediante la Densidad Espectral de Potencia (PSD, método de Welch).
- **Lógica del semáforo**: si la potencia Alfa es alta y el LF/HF es bajo (respecto a una línea base personal calibrada), el indicador pasa a verde (relajación). Si la Alfa es baja y el LF/HF es alto, pasa a rojo (estrés). En estados mixtos, queda en amarillo.

El procesamiento se realiza sobre una ventana deslizante de 2 segundos, actualizando la interfaz 5 veces por segundo.

## Requisitos

- Python 3.9 o superior
- Librerías necesarias:

```bash
pip install numpy scipy matplotlib
```

> `tkinter` viene incluido por defecto en la mayoría de instalaciones de Python. Si no lo tienes (común en algunas instalaciones de Linux), instálalo con:
> ```bash
> sudo apt-get install python3-tk
> ```

## Estructura del repositorio

```
/Hardware   → Diagramas de colocación de electrodos y fotos del montaje BIOPAC
/Software   → Código fuente (codigo_de_interfaz.py) y archivo de datos
/Reporte    → Reporte técnico en formato IEEE (PDF y .docx)
README.md   → Este archivo
```

## Cómo ejecutar el programa

1. Clona o descarga este repositorio.
2. Asegúrate de que el archivo de datos (`.txt` exportado de BIOPAC) esté en la misma carpeta que el script, o ajusta la ruta en la variable `ARCHIVO_DATOS` dentro del código.
3. Desde la terminal, ubicado en la carpeta `/Software`, ejecuta:

```bash
python codigo_de_interfaz.py
```

4. Se abrirá la ventana de la interfaz. Pasos para usarla:
   - Presiona **"▶ Iniciar Adquisición"** para comenzar a leer y procesar la señal.
   - Presiona **"⚙ Calibrar Línea Base (5 s)"** y mantente en reposo durante esos 5 segundos. Esto establece tus valores personales de referencia (α₀ y LF/HF₀).
   - Una vez calibrado, el semáforo comenzará a reflejar tu estado de relajación/estrés en tiempo real.

## Capturas de pantalla

![Semáforo en estado verde (relajación)]("C:\Users\Javie\Downloads\interfaz de codigo en estado relajado.jpeg")
![Semáforo en estado rojo (estrés)]("C:\Users\Javie\Downloads\interfaz en estado de estres .jpeg")
![Vista general de la GUI con gráficas ECG, EEG y PSD]("C:\Users\Javie\Downloads\Interfaz en estado de transicion .jpeg")

## Limitaciones conocidas

- El cálculo de LF/HF usa una aproximación de muestreo uniforme sobre la serie de intervalos R-R, en vez de interpolación a un eje de tiempo verdaderamente uniforme.
- La ventana de calibración (5 s) y el historial de HRV (~20-30 s) son más cortos que los recomendados por la literatura estándar (varios minutos) para un cálculo riguroso de LF/HF.
- El detector de picos R no fue validado contra una base de datos anotada (gold standard).

## Integrantes del equipo

- [Javier Marcial Luis Sanjuan]
- [Verónica Iveth Alarcón Hernández]
