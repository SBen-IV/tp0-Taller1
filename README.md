# TP0

Nombre completo: Sebastian Bento Inneo Veiga

Padron: 100998

Link: https://github.com/SBen-IV/tp0

## Paso 0: Entorno de Trabajo

**a.** Capturas de pantalla de la ejecución del aplicativo (con y sin Valgrind).

![Imagen Paso 0](imagen_paso_0.png)

**b.** ¿Para qué sirve Valgrind? ¿Cuáles son sus opciones más comunes?

Valgrind es usado para detectar mal uso de memoria en un programa, por ejemplo, al hacer uso de `malloc()` sin haber hecho `free()`.

**c.** ¿Qué representa sizeof()? ¿Cuál sería el valor de salida de sizeof(char) y sizeof(int)?

`sizeof()` es una función que devuelve el tamaño en bytes del tipo de dato de la variable que se le pasa por parámetro. El valor que devuelva va a depender de la arquitectura en la que se encuentre el programa, por ejemplo, en 32 bits el tamaño de un `short` será de 2 bytes mientras que en 64 bits será de 4 bytes.

**d.** ¿El sizeof() de una struct de C es igual a la suma del sizeof() de cada uno sus elementos?
Justifique mediante un ejemplo.

En la mayoría de los casos esto no es cierto, por ejemplo, si se tiene la estructura (en 32 bits):

```c
typedef struct Ejemplo{
	short a;
	int b;
};
```
`sizeof(short)` + `sizeof(int)` = 2 + 4 = 6, pero si hacemos `sizeof(Ejemplo)` = 8 =! 6.

Esto ocurre porque se agrega un *padding* a la estructura de modo que sus miembros queden en direcciones de memoria múltiplos de 4. En este caso queda así:

0 | 1 | 2 | 3
------|-------|----|----
short | short | x | x
int | int | int | int 

(x = padding)

**e.** Investigar la existencia de los archivos estándar: STDIN, STDOUT, STDERR. Explicar
brevemente su uso y cómo redirigirlos en caso de ser necesario (caracteres > y <) y como
conectar la salida estándar de un proceso a la entrada estándar de otro con un pipe (carácter
| ).

STDIN: Se usa para almacenar lo que se ingresa por teclado. Se puede redirigir con `porgrama1 < programa2`.

STDOUT: Se usa para almacenar lo que se imprime por pantalla en la terminal. Se puede redirigir con `programa1 > programa2` o `programa1 1> programa2`. 

STDERR: Se usa para almacenar la salida sobre errores de los programas. Se puede redirigir con `programa1 2> programa2`.

Para conectar la salida estándar con la entrada estándar de 2 procesos se puede usar un pipe de la siguiente manera:

`programa_con_salida_estandar | programa_con_entrada_estandar`


## Paso 1: SERCOM - Errores de generación y normas de programación

**a.** Captura de pantalla mostrando los problemas de estilo detectados. Explicar cada uno.

```
/task/student//source_unsafe/paso1_wordscounter.c:27:  Missing space before ( in while(  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:41:  Mismatching spaces inside () in if  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:41:  Should have zero or one spaces inside ( and ) in if  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:47:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
/task/student//source_unsafe/paso1_wordscounter.c:47:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
/task/student//source_unsafe/paso1_wordscounter.c:48:  Missing space before ( in if(  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:53:  Extra space before last semicolon. If this should be an empty statement, use {} instead.  [whitespace/semicolon] [5]
/task/student//source_unsafe/paso1_wordscounter.h:5:  Lines should be <= 80 characters long  [whitespace/line_length] [2]
/task/student//source_unsafe/paso1_main.c:12:  Almost always, snprintf is better than strcpy  [runtime/printf] [4]
/task/student//source_unsafe/paso1_main.c:15:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
/task/student//source_unsafe/paso1_main.c:15:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
Done processing /task/student//source_unsafe/paso1_wordscounter.c
Done processing /task/student//source_unsafe/paso1_wordscounter.h
Done processing /task/student//source_unsafe/paso1_main.c
Total errors found: 11
```


**b.** Captura de pantalla indicando los errores de generación del ejecutable. Explicar cada uno e indicar si se trata de errores del compilador o del linker.



**c.** ¿El sistema reportó algún WARNING? ¿Por qué?