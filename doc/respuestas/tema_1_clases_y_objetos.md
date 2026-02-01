# TEMA 1. Clases y objetos
## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos?
## Se identifican cuatro pilares fundamentales: Abstracción, Encapsulamiento, Herencia y Polimorfismo. La abstracción permite representar las características esenciales de un objeto del mundo real en el código, descartando los detalles irrelevantes para el problema. Se define qué hace un objeto en lugar de cómo lo hace a nivel interno.

### El encapsulamiento consiste en agrupar los datos y los métodos que operan sobre esos datos en una sola unidad (la clase), ocultando los detalles de implementación al exterior. Por otro lado, la herencia permite crear nuevas clases a partir de otras ya existentes, favoreciendo la reutilización de código. Finalmente, el polimorfismo permite que una misma operación se comporte de manera distinta según el objeto que la ejecute.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos
## Existen diversos lenguajes que implementan este paradigma. Java es uno de los más extendidos, especialmente en entornos empresariales y educativos, debido a su portabilidad. C++, lenguaje que ya conoces en su faceta procedimental, permite también el uso de clases y objetos, siendo muy utilizado en sistemas de alto rendimiento y videojuegos.

### Otros dos ejemplos muy populares son Python, que destaca por su sintaxis sencilla y su gran flexibilidad, y C# (C-Sharp), desarrollado por Microsoft y muy vinculado al ecosistema .NET. Estos lenguajes comparten la mayoría de los conceptos de la POO, aunque varían en su gestión de memoria o sintaxis.

## 3. Paradigmas anteriores: Programación estructurada y modular
## La programación estructurada es un paradigma que organiza el código mediante el uso de estructuras de control (bucles, condicionales) y funciones, evitando el uso de saltos incondicionales (como el goto). Se basa en el teorema de la estructura, que afirma que cualquier programa puede escribirse usando solo secuencia, selección e iteración.

### La programación modular da un paso más allá al dividir el programa en partes más pequeñas e independientes denominadas módulos. Cada módulo suele agrupar funciones y datos relacionados, y se comunican entre sí mediante interfaces claras. En C, esto se asemeja a separar el código en distintos archivos .c y archivos de cabecera .h.

## 4. ¿Qué tres elementos definen a un objeto?
## Un objeto se define mediante su estado, comportamiento e identidad. El estado está determinado por los valores de sus atributos o variables en un momento dado. El comportamiento se define a través de sus métodos (funciones), que representan las acciones que el objeto puede realizar o las reacciones ante estímulos externos.

### La identidad es lo que distingue a un objeto de todos los demás, incluso si tienen el mismo estado (los mismos valores en sus variables). En memoria, dos objetos pueden ser idénticos en datos, pero ocupan posiciones distintas y, por tanto, poseen identidades únicas.

## 5. Clase, Objeto e Instancia
## Una clase se entiende como el plano, molde o plantilla que define las características y comportamientos comunes. Un objeto es la entidad concreta creada a partir de ese molde. El término instancia se refiere al proceso de "dar vida" a una clase; de modo que un objeto es una instancia de una clase específica.

### No todos los lenguajes orientados a objetos utilizan clases. Aunque la mayoría (Java, C++, Python) son "basados en clases", existen otros como JavaScript (en sus versiones originales) que utilizan prototipos, donde los objetos se crean clonando otros objetos en lugar de seguir un molde estático.

## 6. Memoria y Recolección de Basura
## En la mayoría de lenguajes como Java, los objetos se almacenan en una zona de memoria dinámica llamada Heap (montículo). A diferencia de las variables locales simples que van al Stack (pila), los objetos requieren una gestión más flexible del espacio. Esta organización varía ligeramente según el lenguaje y su implementación.

### La recolección de basura (Garbage Collection) es un proceso automático que libera la memoria ocupada por objetos que ya no tienen ninguna referencia apuntando a ellos. En C/C++ se debe usar free o delete manualmente, pero en lenguajes modernos como Java, un proceso en segundo plano se encarga de limpiar el "desorden" para evitar fugas de memoria.

## 7. Método y Sobrecarga
## Un método es una función que está definida dentro de una clase y que tiene acceso a sus atributos. Representa una acción que el objeto puede realizar. La principal diferencia con una función de C es que el método siempre actúa sobre una instancia específica de la clase.

### La sobrecarga de métodos permite definir varios métodos con el mismo nombre dentro de una misma clase, siempre que su lista de parámetros sea distinta (diferente número o tipo de argumentos). Esto permite realizar acciones similares con diferentes tipos de entrada, mejorando la legibilidad del código.

## 8. Ejemplo de clase Punto en Java
## A continuación se presenta la definición de la clase y su uso.

### public class Punto {
###     double x; // Visibilidad por defecto
###     double y;
### 
###     double calculaDistanciaAOrigen() {
###         return Math.sqrt(x * x + y * y);
###     }
### }

### // Ejemplo de uso
### public class Principal {
###     public static void main(String[] args) {
###         Punto miPunto = new Punto();
###         miPunto.x = 3.0;
###         miPunto.y = 4.0;
###         System.out.println("Distancia: " + miPunto.calculaDistanciaAOrigen());
###     }
### }

## 9. Punto de entrada, static y final
## El punto de entrada en Java es el método public static void main(String[] args). La palabra clave static indica que el método pertenece a la clase y no a una instancia específica; por tanto, no hace falta crear un objeto para ejecutarlo. No se usa solo en el main, sino también para crear constantes o métodos de utilidad que no dependen de datos individuales del objeto.

### Cuando static se combina con final, se utiliza para crear constantes de clase. El valor se vuelve inmutable y es compartido por todos los objetos de esa clase, lo que resulta muy eficiente para valores que nunca cambian, como el número PI o configuraciones globales.

## 10. Compilación, Máquina Virtual y Bytecode
## Java no se compila a código máquina directo como C. En su lugar, el comando javac genera un código intermedio llamado Bytecode (archivos .class). Para ejecutarlo, se usa el comando java, que inicia la Máquina Virtual de Java (JVM). La JVM es el software que interpreta o traduce ese Bytecode al lenguaje del procesador real.

### Este sistema permite que Java sea "portátil": el mismo archivo .class funciona en Windows, Mac o Linux, siempre que tengan instalada la JVM correspondiente. Se dice que Java es un lenguaje compilado (a bytecode) e interpretado (por la máquina virtual).

## 11. El operador new y el Constructor
## El operador new se utiliza para solicitar memoria en el heap y crear una nueva instancia de la clase. Por su parte, el constructor es un método especial que se ejecuta automáticamente al usar new. Su función principal es inicializar los atributos del objeto recién creado.

### public class Empleado {
###     String dni;
###     String nombre;
###     String apellidos;
### 
###     // Constructor
###     public Empleado(String dni, String nombre, String apellidos) {
###         this.dni = dni;
###         this.nombre = nombre;
###         this.apellidos = apellidos;
###     }
### }

## 12. La referencia this
## La palabra clave this es una referencia que apunta al objeto actual que está ejecutando el código. Se utiliza frecuentemente para diferenciar los atributos de la clase de los parámetros que recibe un método si ambos tienen el mismo nombre. En otros lenguajes como Python se llama self, pero el concepto es idéntico.

### public void setCoordenadas(double x, double y) {
###     this.x = x; // "this.x" es el atributo, "x" es el parámetro
###     this.y = y;
### }

## 13. Método distanciaA
## Este método recibe otro objeto de tipo Punto y calcula la distancia entre ambos.

### double distanciaA(Punto otroPunto) {
###     double dx = this.x - otroPunto.x;
###     double dy = this.y - otroPunto.y;
###     return Math.sqrt(dx * dx + dy * dy);
### }

## 14. Paso de parámetros: ¿Copia o Referencia?
## En Java, los objetos se pasan por valor, pero ese valor es la referencia (la dirección de memoria). Esto significa que si se modifica un atributo del objeto dentro del método, el cambio sí afecta al objeto original fuera del método, ya que ambos apuntan al mismo sitio.

### Sin embargo, los tipos primitivos (como int, double) se pasan por copia pura. Si se recibe un int y se modifica dentro de la función, el valor original fuera de ella permanece intacto. Es una distinción crítica que en C se gestionaba explícitamente con punteros.

## 15. Método toString()
## El método toString() se utiliza para obtener una representación en texto del objeto. Se hereda de una clase base común en Java y es muy útil para depuración o para imprimir información del objeto de forma rápida. En lenguajes como Python, existe el método equivalente __str__.

### public String toString() {
###     return "Punto(x=" + x + ", y=" + y + ")";
### }

## 16. Reflexión: ¿Es una clase como un struct en C?
## Una clase se parece a un struct en que ambos permiten agrupar datos de distintos tipos. Sin embargo, al struct le falta la capacidad de contener comportamiento (métodos) y el control de acceso (privacidad de los datos).

### Para que un struct fuera como una clase, debería permitir guardar funciones dentro de su definición y gestionar automáticamente la memoria mediante constructores y destructores. Además, en POO las instancias no son solo datos, sino entidades activas.

## 17. Emular una clase con struct en C
## Para "emular" una clase en C, se definen los datos en un struct y las funciones por separado, pasando siempre un puntero a la estructura como primer argumento. Este puntero manual es lo que en POO se convierte en el this automático.

### struct Punto {
###     double x;
###     double y;
### };

### double calculaDistanciaAOrigen(struct Punto* p) {
###     return sqrt(p->x * p->x + p->y * p->y);
### }

### En este caso, la "magia" de this desaparece porque el programador debe pasar explícitamente la dirección de la estructura (p) para que la función sepa sobre qué datos operar.