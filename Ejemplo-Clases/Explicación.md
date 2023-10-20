# Configuracion Software 
**_HuskyLensLibrary("COM_PROTOCOL, "COM_PORT", channel, address)_**

Inicia el tipo de clase de HuskyLens y automaticamente se conectara a tu camara. Esto te permitira utilizar las funciones disponibles de la Husky.

- **_Argumentos_**:
  - `"COM_PROTOCOL"`: (String) También `"SERIAL"` para conexiones USB o `"I2C"` para Raspberry Pi.
  - `"COM_PORT"`: (String) COM Port de la HuskyLens, no es necesario para conexiones de `"I2C"`.

  **_Returns_**: Devuelve a un Object de `HuskyLens`

  
- **_Ejemplos_**:
  - `hl = HuskyLensLibrary("SERIAL", "/dev/ttyUSB0")`
  - `hl = HuskyLensLibrary("I2C","", address=0x32, channel=0)`

## Funciones

**_knock()_**
  - **Descripción**: Envia un _knock_ para asegurarse que la HuskyLens establecio una comunicación con el hub y se conecto correctamente.

    **Returns**: Devuelve a la consola un "Knock Received" si esta todo correcto.

**_frameNumber()_**
  - **Descripción**: Obtiene el numero de frames que la HuskyLens procesa.

    **Returns**: La cantidad de frames.

**_count()_**
  - **Descripción**: Obtiene el numero de objetos aprendidos o no aprendidos en la pantalla.

    **Returns**: Numero de objetos en la pantalla.

**_learnedObjCount()_**
  - **Descripción**: Obtiene el número total de objetos que corren el algoritmo continuo, no hace falta que los objetos se presenten en la pantalla.

    **Returns**: Numero de objetos aprendidos.

## Data Functions

> Data Fromat
> - Data corresponde a la información de un `block` con todos los algoritmos exceptuando el _Line Tracking_, que en vez de esto devolvera la informacion de `arrow`.
> - Esto directamente reflejara los blocks/arrows en el UI de la HuskyLens.
>```
> class  Block:
>   	Members:
>   		x => (Integer) x coordinate of the center of the square 
>   		y => (Integer) y coordinate of the center of the square 
>   		width  =>  (Integer) width of the square
>   		height =>  (Integer) height of the square
>   		ID => (Integer) Objects ID (if not learned, ID is 0)
>   		learned => (Boolean) True  if the object is learned
>   		type => "BLOCK"
>   class  Arrow:
>   	Members:
>   		xTail => (Integer) x coordinate of the tail of the arrow
>   		yTail => (Integer) y coordinate of the tail of the arrow
>   		xHead => (Integer) x coordinate of the head of the arrow
>   		yHead => (Integer) y coordinate of the head of the arrow
>   		ID => (Integer) Objects ID (if not learned, ID is 0)
>   		learned => (Boolean) True  if the object is learned
>   		type => "ARROW"
>```
>
> - Devuelve la información en un array de cada bloque o arrow:
> **`[block1, block2, ... blockN]` o `[arrow1, arrow2, ... arrowN]`**

**_requestAll()_**
  - **Descripción**: Hace un request de todos los bloques y arrows guardados en la HuskyLens. Esto devolvera un block/arrow de todos los que aprendio y los que no sera visibles en su pantalla.

    **Returns**: Devolvera un array `[block1, block2, ... blockN]` or `[arrow1, arrow2, ... arrowN]`

**_blocks()_**
  - **Descripción**: Pide la información de todos los bloques de la HuskyLens. Esto devolvera la información de cada bloque aprendido.

    **Returns**: Devuelve un array `[block1, block2, ... blockN]`


**_arrows()_**
  - **Descripción**: Hace un request de todas las arrow data que se encuentran dentro de la HuskyLens. Esto devolvera la información de los bloques aprendida y de objetos no aprendidos seran visibles en la pantalla.
    **Returns**: Devuelve un array `[arrow1, arrow2, ... arrowN]`


**_learned()_**
  - **Descripción**: Manda un request a toda la información que reconozcoa sobre arrows y bloques de la HuskyLenss. Esto devolvera el conocimiento aprendido que tenga sobre los objetos visibles en la pantalla. Los objetos no aprendidos seran ignorados.

    **Returns**¨: Returns data array `[block1, block2, ... blockN]` or `[arrow1, arrow2, ... arrowN]`

**_learnedBlocks()_**
  - **Descripción**: Solicita todos los datos de block que tiene la HuskyLens. Esto devolverá los datos del block para todos los objetos aprendidos que son visibiles en la pantalla, los objetos no aprendidos se ignoran.
    **Returns**: Devuelve un array `[block1, block2, ... blockN]`



**_learnedArrows()_**
  - **Descripción**:Solicitda todos los datos de las arrows que tiene la HuskyLens. Esto devolverá los datos de las arros para todos los objetos aprendidos seran visibles en las pantallas, pero los que no seran ignorados.

    **Returns**: Devuelve un array `[arrow1, arrow2, ... arrowN]`


**_getObjectByID( ID )_**
  - **Descripción**: Solicita todos los datos del block de la HuskyLens que tengan una ID designada y sean visibles en la pantalla.

    **Argumentos**: ID : (Entero) El ID del objeto.

    **Returns**: Devuelve un array `[block1, block2, ... blockN]`

**_getArrowsByID( ID )_**
  - **Descripción**: Solicita todos los datos de las arrows de la HuskyLens que tengan una ID designada y sean visibles en la pantalla.

    **Argumentos**: ID : (Entero) El ID del objeto.

    **Returns**: Devuelve un array `[arrow1, arrow2, ... arrowN]`

## Funciones mediante Algoritmos
**algorithm ( algorithmName )**
  - **Descripción**: Cambia a un algoritmo especifico de la HuskyLens.

    **Argumentos**:
    **_algorithmName_**: (String)
      > “ALGORITHM_OBJECT_TRACKING”
      > 
      > “ALGORITHM_FACE_RECOGNITION”
      > 
      > “ALGORITHM_OBJECT_RECOGNITION”
      > 
      > “ALGORITHM_LINE_TRACKING”
      > 
      > “ALGORITHM_COLOR_RECOGNITION”
      > 
      > “ALGORITHM_TAG_RECOGNITION”
      > 
      > “ALGORITHM_OBJECT_CLASSIFICATION”

    **Returns**: Si esta todo correcto devuelve un "Knock".

**_learn( ID )_**
  - **Descripción**: Aprende los objetos que son reconocidos en la pantalla por una ID.


    **Argumentos**:
      `ID`: (Integer) La id puede ser entre 1-1023.

    **Returns**: Devuelve un Knock si funciona.

**_forget()_** 
  - **Descripción**: Se olvida todos los objetos que estan corriendo ahora mismo en el algoritmo.

    **Returns**: Devuelve un Knock si es exitoso.


## UI Related Functions
**_setCustomName("Name_Value", objectID)_**

 **_Descripción_**: Poner un nombre customizado de un objeto aprendido con una ID especifica. Por ejemplo, si aprendio alguna ID, podes usar huskylens.setCustomName("Robert", 1) para renombrar la cara del objeto de "Robert".

 **_Argumentos_**: 
 `"Name_Value"`: (String) valor deseado.
 `objectID`: (Interger) valor de la ID del objeto aprendido que deseas cambiar.

 **Returns**: Devuelve un Knock si funciona.

**_customText("Text_Value", X, Y)_**

  - **Descripción**:
          Coloque una cadena de texto (menos de 20 caracteres) en la parte superior de la interfaz de usuario de     
          HuskyLens. La posición de la coordenada (X,Y) del texto es la parte superior izquierda del cuadro de texto.

          Puedes tener como máximo 10 textos personalizados en la IU a la vez, y si sigues añadiendo textos 
          reemplazarás los textos anteriores de forma circular. Por ejemplo, si introduce 10 textos llenará el búfer 
          de texto. Si luego insertas un nuevo objeto de texto, sobrescribirás la primera posición de texto 
          (textBuffer[0]). Si inserta otro objeto de texto nuevo, sobrescribirá la segunda posición de texto 
          (textBuffer[1]).

          Cada texto se identifica de forma única por su coordenada (X,Y), por lo que puedes reemplazar la cadena de 
          texto en una coordenada (X,Y) en lugar de añadir un nuevo objeto de texto. Por ejemplo, si insertas     
          "PRUEBA_1" en (120,120) y más tarde envías "PRUEBA_2" en (120,120), sustituirás la cadena "PRUEBA_1" por 
          "PRUEBA_2" y mantendrás un recuento total de texto de 1.


    **_Argumentos_**:
        `"Text_Value"`: (String) valor del texto mandado.

        `X`: (Integer) La coordinada X para el objeto UI (0-320)

        `Y`: (Integer) La coordenada Y para el objeto UI (0-240)

    **Returns**: Devuelve un Knock si todo esta correcto


**_clearText()_**

  - **Descripción**: Borra y elimina todas las customizaciones UI texto de la screen.


    **Returns**: Devuelve un Knock si todo esta correcto.


## Funciones de Utilidad
**_saveModelToSDCard( fileNum )_**
  - **Descripción**: Guarda todos los algoritmos en la carpeta(Los objetos aprendidos) en la tarjeta SD. La carpeta se guardara en el formato "AlgorithimName_Backup´_FileNum.conf".

    **Argumentos**:
      `fileNum`: (Integer) El numero de archivo especificado que se utilizará en el nombre del archivo.

    **Returns**: Devuelve "Golpe recibido" en caso de éxito. Si no hay ninguna tarjeta SD insertada o se produce un
error en la tarjeta SD, aparecerá una ventana emergente de la interfaz de usuario de HuskyLens indicando el problema.

**_loadModelFromSDCard( fileNum )_**
  - **Descripción**: Carga un archivo de modelo desde la tarjeta SD al algoritmo actual y actualiza el algoritmo. El
archivo cargado tendrá el siguiente formato "AlgorithimName_Backup_FileNum.conf"

    **Argumentos**:
      `fileNum`: (Integer) Especifica el numero de la carpeta que va a ser usado para el nombre.

    **Returns**: Devuelve "Golpe recibido" en caso de éxito. Si no hay ninguna tarjeta SD insertada o se produce un
error en la tarjeta SD, aparecerá una ventana emergente de la interfaz de usuario de HuskyLens indicando el problema.


**_savePictureToSDCard()_**:
  - **Descripción**: Guarda la foto en la HuskyLens dentro de la tarjeta SD.

    **Returns**: Devuelve "Golpe recibido" en caso de éxito. Si no hay ninguna tarjeta SD insertada o se produce un
error en la tarjeta SD, aparecerá una ventana emergente de la interfaz de usuario de HuskyLens indicando el problema.


**_saveScreenshotToSDCard()_**
  - **Descripción**: Guarda la Screenshot en la HuskyLens UI dentro de la tarjeta SD.

    **Returns**: Devuelve "Golpe recibido" en caso de éxito. Si no hay ninguna tarjeta SD insertada o se produce un
error en la tarjeta SD, aparecerá una ventana emergente de la interfaz de usuario de HuskyLens indicando el problema.
