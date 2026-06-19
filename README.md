# 6F_PROYECTO_FINAL_23310403_23310288
# Sistema de Detección de Equipo de Protección Personal (EPP) con YOLO

Integrantes
Manuel Alejandro Lucano Estrada 23310403

Instrucciones para correr el codigo
1. Clonar este repositorio o descargar el archivo .ipynb.
2. Instalar las dependencias ejecutando: `pip install -r requirements. txt*
3. Abrir el notebook en Google Colab
4. Cargar el modelo entrenado `best.pt de la carpeta de Codigo Fuente.
5. Ejecutar la celda de predicción subiendo una imagen de prueba en los archivos de colab.

E Caso de Estudio (Aplicación Práctica)

1. Problema a resolver
En las obras de construccion, la falta de uso del Equipo de Proteccion Personal (EPP), como cascos y chalecos reflectantes, es una de las
principales causas de accidentes graves o fatales. La supervision humana es insuficiente, propensa a descuidos y no puede cubrir todas las
areas simultaneamente. Ademas, las empresas constructoras enfrentan fuertes multas por incumplimiento de normativas de seguridad.

2. Descripcion del Hardware Propuesto
Para llevar este modelo a un entorno real, proponemos la siguiente infraestructura:
Camaras: Camaras IP de seguridad con vision nocturna e infrarroja (ej. Hikvision o Dahua 4K) instaladas estrategicamente en los
torniquetes de acceso, gruas y zonas de alto riesgo.
Procesamiento (Edge Computing): En lugar de enviar el video a la nube (lo cual causaria latencia), se utilizaran microcomputadoras
industriales NVIDIA Jetson Orin Nano instaladas en la caseta de control de la obra. Estos equipos procesaran el video en tiempo real
gracias a su GPU integrada.
Maquinaria de Accion: Torniquetes de control de acceso automatizados y sirenas/semaforos visuales (rojo/verde) conectados mediante
reles al sistema de procesamiento.

3. Flujo de Funcionamiento
Captura: Un trabajador se acerca al torniquete de entrada de la obra. La camara IP capta el video en tiempo real.
Inferencia:  El stream de video llega a la NVIDIA Jetson, donde nuestro modelo YOLO analiza cada *frame* en milisegundos buscando
las clases helmet y vest.

Toma de Decisiones:
Escenario A (Cumple): Si el modelo detecta casco y chaleco con un nivel de confianza alto, el sistema envía una señal digital al
torniquete para que se abra, permitiendo el paso.
Escenario B (No Cumple): Si el modelo detecta no-helmet o `no-vest`, el torniquete permanece bloqueado. Se enciende una luz roja
y suena una alerta de voz pregrabada: "Por favor, coloquese su equipo de seguridad".
Registro: El sistema guarda una captura de la incidencia y la envía automáticamente por Telegram o correo al supervisor de obra
para un reporte estadístico.
