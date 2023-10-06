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



