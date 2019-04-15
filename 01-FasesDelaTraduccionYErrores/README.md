## Autor de la resolución
  + Usuario: fjaraoz   
  + Legajo: 162789-2   
  + Apellido: Araoz   
  + Nombre: Francisco Javier 

-------------------

#### 1. Escribir hello2.c , que es una variante de hello.c
#### 2. Preprocesar hello2.c , no compilar, y generar hello2.i . Analizar su contenido.
>***Comando ejecutado**: -gcc -std=c11 -E hello2.c -o hello2.i  
**Resultado**: Se generó el archivo hello2.i  
**Análisis**: Los comentarios fueron borrados, y la linea \#include fue reemplazada por definiciones de funciones, directorios y tipos de datos referentes a la Biblioteca estándar de C.*
    
#### 3. Escribir hello3.c , una nueva variante.
#### 4. Investigar la semántica de la primera línea.
>***Análisis**: El sentido de la primera línea es definir el prototipo de la función printf para que el compilador compruebe si printf se invocó correctamente cada vez que se usa la misma.*

#### 5. Preprocesar hello3.c , no compilar, y generar hello3.i . Buscar diferencias entre hello3.c y hello3.i
>***Comando ejecutado**: -gcc -std=c11 -E hello3.c -o hello3.i  
**Resultado**: Se generó el archivo hello3.i  
**Análisis**: Con respecto a hello3.c, el preprocesador agregó el nombre del archivo y algunas referencias. Con respecto al hello2.i, se agregaron muchas menos líneas de código ya que no se incluyeron las referencias a la Biblioteca estándar.*
    
#### 6. Compilar el resultado y generar hello3.s , no ensamblar.
>***Comando ejecutado**: -gcc -std=c11 -S hello3.i -o hello3.s  
**Resultado**: ERROR  
                hello3.c: In function ‘main’:  
                hello3.c:6:5: warning: implicit declaration of function ‘prontf’ [-Wimplicit-function-declaration]  
                    prontf("La respuesta es %d\n");  
                    ^  
                hello3.c:6:5: error: expected declaration or statement at end of input    
**Análisis**: El warning nos advierte que estamos usando una función que no fue declarada (ya que la que declaramos fue printf y no prontf). Además el error surge de que al final del código de la funcion main falta la llave de cierre.*
    
#### 7. Corregir en el nuevo archivo hello4.c y empezar de nuevo, generar hello4.s , no ensamblar.
>***Corrección**: Se agregó la llave de cierre.  
**1° Comando ejecutado**: -gcc -std=c11 -E hello4.c -o hello4.i  
**Resultado**: se generó hello4.i  
**2°Comando ejecutado**: -gcc -std=c11 -S hello4.i -o hello4.s  
**Resultado**: se generó hello4.s. Además, gcc arrojó el mismo warning que en el paso anterior.*  
    
#### 8. Investigar hello4.s .
#### 9. Ensamblar hello4.s en hello4.o , no vincular.
>***Comando ejecutado**: -gcc -C hello4.s -o hello4.o  
**Resultado**: se generó hello4.o*

#### 10.Vincular hello4.o con la biblioteca estándar y generar el ejecutable.
>***Comando ejecutado**: -gcc hello4.o -o hello4  
    **Resultado**: ERROR  
                hello4.o: En la función main':  
                hello4.c:(.text+0x1a): referencia a `prontf' sin definir  
                collect2: error: ld returned 1 exit status    
**Análisis**: El linker ld no pudo resolver la referencia a prontf ya que no fue definida previamente.*

#### 11.Corregir en hello5.c y generar el ejecutable.
>***Corrección**: se cambió prontf por printf  
**1°Comando ejecutado**: -gcc -E -std=c11 hello5.c -o hello5.i  
**Resultado**: se generó hello5.i sin errores  
**2°Comando ejecutado**: -gcc -S -std=c11 hello5.i -o hello5.s  
**Resultado**: se generó hello5.s con un warning que nos advierte que la función espera un int como segundo argumento (actualmente estamos pasando un solo parámetro)  
**3°Comando ejecutado**: -gcc -c hello5.s -o hello5.o  
**Resultado**: se generó hello5.o sin errores  
**4°Comando ejecutado**: -gcc hello5.o -o hello5  
**Resultado**: se generó el ejecutable hello5 sin errores*

#### 12.Ejecutar y analizar el resultado.
>***Comando ejecutado**: ./hello5  
**Análisis**: El resultado esperado era que se imprima en pantalla la cadena "La respusta es 42". Esto no sucede, se debe a que al no haber definido como segundo parámetro de printf a la variable que queríamos imprimir, imprime valores aleatorios.*

#### 13.Corregir en hello6.c y empezar de nuevo.
>***Corrección**: se agregó como segundo parámetro de printf a la variable i  
**1°Comando ejecutado**: -gcc -E -std=c11 hello6.c -o hello6.i  
**Resultado**: se generó hello6.i sin errores  
**2°Comando ejecutado**: -gcc -S -std=c11 hello6.i -o hello6.s  
**Resultado**: se generó hello6.s sin errores   
**3°Comando ejecutado**: -gcc -c hello6.s -o hello6.o   
**Resultado**: se generó hello5.o sin errores  
**4°Comando ejecutado**: -gcc hello6.o -o hello6  
**Resultado**: se generó el ejecutable hello5 sin errores. Se ejecutó e imprime el resultado esperado.*

#### 14.Escribir hello7.c , una nueva variante.
>***Comando ejecutado**: -gcc hello7.c -o hello7  
**Resultado**: se generó hello7 con un warning que advierte que se está usando la función printf que no fue declarada previamente. Al abrir el ejecutable hello7, funciona correctamente.*

#### 15.Explicar porqué funciona.
>***Análisis**: Si bien la biblioteca estándar no fue referenciada, al ser printf una función de uso común, el sistema operativo (en este caso Ubuntu 16.04 LTS) sabe dónde buscarla y cómo usarla.*
