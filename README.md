# HuskyLens-Spike
Una camara de inteligencia artificial con diversos modos de funcionamientos.
1. Reconocimiento de caras
2. Reconocimiento de objetos
3. Seguimiento de líneas
4. Seguimiento de objetos
5. Reconocimiento de colores

**Utiliza un procesador IA Kendryte K210 y dispone de conexiones _I2C_ y _UART_ para interactuar con arduino, micro_bit, Raspberry Pi y Lego Spike Prime. Cuenta con una tensión de alimentación de _3.3~5.0V_**
- HuskyLens admite tres velocidades de transmisión UART(9600, 115200, 1000000) y el protocolo I2C.
- Además, admite la detección automática de los protocolos, es decir, Huskylens cambiará automaticamentre entre UART e I2C.
- Para usar **_Lego Spike Prime_** debes seguir una serie de pasos para instalarlo en el hub.

## Instalador de paquetes python
- Formatear el Lego spike para evitar problemas en la instalación.
- En el centro de comandos de windows haz lo siguiente:
```
pip3 install pyserial pypng
  ```

## Configuración de HuskyLens
- Debes hacer una conexión mediante pines para conectar la Huskylens a SpikePrime. Hay dos opciones sin un convertidor dc-dc y otro con un convertidor. La Husky 3v3 en su fuente de alimentación y los cables RX y TX conectados. La camara es resistente a 5 volteos, pero la comunicación se encuentra obstaculizada. Ya que no tenia un regulador fijo 3v3, asi que puedes usar un convertir más grande pero sintonizable.

  ### Opcion 1: Version sin dc-dc converter![dc-dc](https://www.antonsmindstorms.com/wp-content/uploads/2021/10/Paper.Sketchbook.97.png#main)
  - Suelde los cables de HuskyLens incluidos a un conector Wedo2plug de respuesto 5 y 6(líneas ID1/ID2) a través de UART a los pines 2 y 1 de HuskyLens(RX/TX)

  ### Opcion 2: Poder con un 100% pwm ![dc-dc](https://www.antonsmindstorms.com/wp-content/uploads/2021/10/Paper.Sketchbook.98.png#main)
  - La alimentación de la Huskylens se realiza con una batería USB o LPF mediante la conexión a un convertidor reductor 3V3. Sin configura el puerto al 100% PWM, M+ será aproximadamente 8V y M- será 0V(GND).
  - **_Cuidado_** al usar LPF-Motor(lineas M1/M2), si el firmware de HuskyLens es 0.5+, se bloqueará aleatoriamente durante el uso, a menos que lo encienda a través de un USB. Cambie al [firmware 0.4.7]()
 
  ### Opciones 3: ![img1](https://i0.wp.com/www.antonsmindstorms.com/wp-content/uploads/2021/11/IMG_2030-scaled.jpeg?resize=1024%2C768&ssl=1)
  - Si no quieres cortar y soldar algunos cables, tambien puedes usar el **_Distance Sensor Breakout Board_**. Simplemente utiliza cuatro cables hacia los pines establecidos. Tiene algunas desventajas, desde mi punto de vista para una perfomance más estable puedes utilizar el **_Convertidor 3v3_**, la opción 2.

## Instalación en Lego Spike
- **De momento HuskyLens solo es compatible en la versión _2.0.8_ de Lego Spike Prime, si quieres volver a esa versión descarga el archivo [Instalador Spike 2.0.8]().**
1. Crea un proyecto en Lego llamado SPIKEInstaller.
2. Pega el script de [SPIKEInstaller](https://github.com/IITADiegoCABJ/HuskyLens-Spike/blob/main/Libreria/SpikeInstaller.py)
3. Una vez que lo ejecutes y se instale correctamente en el hub, borra ese proyecto.
4. Crea uno nuevo con el nombre que más te guste.
5. Pega el codigo de [SPIKE-Example](https://github.com/IITADiegoCABJ/HuskyLens-Spike/blob/main/Libreria/Spike-Example.py).
