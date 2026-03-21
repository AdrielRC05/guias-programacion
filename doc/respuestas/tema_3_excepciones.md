1. Control de errores en C
En el lenguaje C, al no existir un mecanismo nativo de excepciones, se debe recurrir a señales mediante el valor de retorno o variables globales. Para una función de raíz cuadrada, el diseño debe ser explícito para que el llamador sepa que algo falló.

Opción A: Valor centinela. Se devuelve un valor que sea imposible en condiciones normales (como un número negativo) para indicar el error.

C
float raiz(float n) {
    if (n < 0) return -1.0; // Valor centinela
    return sqrt(n);
}
Opción B: Paso por referencia y código de error. Se reserva el retorno para un código de estado (0 éxito, 1 error) y se usa un puntero para devolver el resultado real.

C
int raiz(float n, float *resultado) {
    if (n < 0) return 1; // Código de error
    *resultado = sqrt(n);
    return 0; // Éxito
}
2. Definición de Excepción
Una excepción es un evento que ocurre durante la ejecución de un programa que interrumpe el flujo normal de las instrucciones. Técnicamente, es un objeto que encapsula información sobre un error o una situación inesperada, permitiendo separar el código de la lógica de negocio del código dedicado a la gestión de errores.

El objetivo del programador al implementar funciones es señalar que se ha alcanzado un estado inválido que la función no puede resolver por sí misma. Al llamarlas, el objetivo es centralizar la respuesta a esos errores en un solo lugar, evitando que el programa "aborte" de forma abrupta y permitiendo una recuperación controlada.

3. Ejemplo en Java
En Java, se utiliza la palabra clave throw para lanzar un objeto de tipo excepción. En este caso, usaremos IllegalArgumentException, que es estándar para argumentos inválidos.

Java
public class Calculadora {
    public double raiz(double n) {
        if (n < 0) {
            throw new IllegalArgumentException("No se puede calcular la raíz de un negativo");
        }
        return Math.sqrt(n);
    }

    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        try {
            System.out.println(calc.raiz(-5));
        } catch (IllegalArgumentException e) {
            System.out.println("Error detectado: " + e.getMessage());
        }
    }
}
4. Conceptos de Propagación
Lanzar es el acto de crear el objeto excepción y entregarlo al sistema de ejecución (throw). Controlar/Capturar es interceptar ese objeto mediante un bloque catch para decidir qué hacer. La propagación ocurre cuando una función no captura la excepción; entonces, el sistema busca un manejador en la función que llamó a la actual, y así sucesivamente hacia atrás en la pila.

A medida que la excepción se propaga, las funciones en la pila de llamadas finalizan su ejecución de forma repentina. No se ejecutan las líneas de código que seguían a la llamada problemática. Si una función no controla la excepción, no se reanuda; simplemente se "desapila" y desaparece de la memoria. En el ejemplo de la raíz, si raiz lanza la excepción y main no la captura, el programa termina ahí mismo.

5. Ventajas de la Propagación Natural
La principal ventaja frente a C es la limpieza del código. En C, tras cada llamada a una función, se debe escribir un if para comprobar el código de retorno. Si hay diez llamadas seguidas, hay diez bloques de comprobación que ensucian la lógica principal.

Con la propagación, se puede escribir un bloque de código extenso (el "camino feliz") y poner un único capturador al final. Esto reduce drásticamente la redundancia y asegura que los errores no pasen desapercibidos, ya que en C es muy fácil olvidar comprobar un valor de retorno, mientras que una excepción no capturada obliga a prestar atención al detener el programa.

6. Excepciones como Objetos
En los lenguajes orientados a objetos, las excepciones son efectivamente objetos que heredan de una clase base (en Java, Throwable). Esto permite aplicar la encapsulación: la excepción no es solo un número de error, sino un contenedor que puede llevar mensajes, estados internos y el estado de la pila en el momento del fallo.

Debido a esto, se pueden crear excepciones personalizadas mediante herencia. Al crear una clase que herede de Exception, se dota al sistema de errores con nombres significativos (ej. SaldoInsuficienteException), lo que hace el código mucho más legible y específico que manejar simples enteros.

7. Información Esencial del Objeto Excepción
A diferencia de C, donde un -1 no dice mucho, un objeto excepción lleva consigo el Stack Trace (traza de la pila). Esta es una lista de todos los métodos que estaban activos en el momento del error, indicando el archivo y la línea exacta donde ocurrió.

Además, incluye un mensaje descriptivo (String) que explica la causa humana del error. Esta combinación de "qué pasó" (mensaje), "dónde pasó" (traza) y "qué tipo de error es" (el nombre de la clase) es fundamental para que el manejador tome decisiones informadas o para que el desarrollador corrija el bug rápidamente.

8. El bloque Try-Catch
En Java, es perfectamente posible y común tener más de un bloque catch asociado a un mismo try. Esto se hace para dar un tratamiento diferente a distintos tipos de errores que pueden ocurrir en un mismo bloque de código.

Sin embargo, solo se ejecuta un único bloque catch: el primero que coincida con el tipo de excepción lanzada (o con una superclase de esta). Una vez que un catch termina su ejecución, el control pasa al código que haya después de toda la estructura try-catch, ignorando los demás bloques de captura.

9. Garantía de Ejecución con Finally
Para asegurar que recursos como ficheros se cierren pase lo que pase, se utiliza el bloque finally. Este bloque se ejecuta siempre, tanto si la ejecución del try fue exitosa como si se produjo una excepción y fue capturada.

Java
// Ejemplo con catch
try {
    abrirArchivo();
} catch (IOException e) {
    System.out.println("Error de lectura");
} finally {
    cerrarArchivo(); // Se ejecuta siempre
}

// Ejemplo sin catch (solo para asegurar limpieza y propagar el error)
try {
    procesarDatos();
} finally {
    liberarRecursos(); // Se ejecuta y luego la excepción sigue subiendo
}
10. Comportamiento de Finally
El bloque finally puede ir sin catch, siempre que haya un try. Su característica fundamental es la inevitabilidad: se ejecuta incluso si hay una instrucción return, break o continue dentro del bloque try.

Si el programa encuentra un return en el try, el sistema "hace una pausa", ejecuta el contenido del finally y solo entonces efectúa el retorno físico de la función. La única forma de que un finally no se ejecute es que la máquina virtual se detenga bruscamente (un apagón o un System.exit(0)).

11. Excepciones Controladas vs. No Controladas
Las controladas (Checked) son aquellas que el compilador te obliga a gestionar o declarar (heredan de Exception). Las no controladas (Unchecked) son errores de programación que pueden ocurrir en cualquier momento y no obligan a su captura (heredan de RuntimeException).

Uso de Controladas (Obligatorias):

Acceso a archivos (FileNotFoundException).

Conexiones de red.

Consultas a bases de datos.

Uso de No Controladas (Opcionales):

Argumentos nulos (NullPointerException).

Índices fuera de rango en arrays.

Cálculos matemáticos imposibles (división por cero).

12. El uso de Throws
La cláusula throws se coloca en la firma de un método para indicar que dicho método puede lanzar ciertas excepciones y no tiene intención de capturarlas. Es una forma de delegar la responsabilidad al programador que llame a ese método.

Es la alternativa a capturar la excepción porque permite que la función se mantenga simple, dejando que el error se propague hacia arriba en la pila hasta un nivel donde tenga más sentido decidir cómo informar al usuario o registrar el fallo.

13. Ejemplo de Throws y Finally
Java
import java.io.*;

public class GestorArchivos {
    public void leerConfiguracion() throws FileNotFoundException {
        FileReader fr = null;
        try {
            fr = new FileReader("config.txt");
            // procesar...
        } finally {
            System.out.println("Limpiando recursos de apertura...");
            // Aquí iría el cierre si fr no es null
        }
    }
}
14. Throws con RuntimeException
Es técnicamente posible poner excepciones no controladas en el throws, pero es redundante y poco común. El compilador no lo exige, por lo que el llamador no estará obligado a poner un try-catch.

El único sentido que tendría es meramente documentativo, para advertir explícitamente a otros programadores que esa función es propensa a un error específico (como un fallo de validación), aunque el lenguaje no les obligue a tratarlo.

15. Cuándo usar cada tipo
Se recomienda usar controladas para condiciones de las que el programa razonablemente podría recuperarse (un archivo que no está pero el usuario puede elegir otro). Se usan no controladas para errores de lógica del programador que no deberían suceder si el código estuviera bien escrito.

No todos los lenguajes tienen ambos tipos. C++, C# o Python solo tienen excepciones "no controladas" (en el sentido de que el compilador no te obliga a nada). Java es el lenguaje más famoso por imponer esta distinción, aunque la tendencia moderna en nuevos lenguajes es evitar las excepciones controladas por considerarlas demasiado rígidas.

16. Lanzar desde un Catch
Tiene mucho sentido lanzar una excepción dentro de un catch. Se puede relanzar la misma excepción si se desea que un error se registre en un log local pero que también siga subiendo para que el usuario sea notificado.

También se puede lanzar una excepción diferente para traducir un error técnico a uno de negocio.

Java
try {
    conectarBD();
} catch (SQLException e) {
    log.error("Fallo técnico", e);
    throw e; // Relanzar la misma
    // o... throw new ServiceException("El servicio no está disponible");
}
17. Excepciones con Causa (Chaining)
Que una excepción sea la causa de otra significa que el error original se "envuelve" dentro de una nueva excepción. Esto permite mantener el contexto técnico original sin exponerlo directamente a las capas superiores de la aplicación.

Java
try {
    Integer.parseInt("no_soy_un_numero");
} catch (NumberFormatException e) {
    // La original (e) se pasa como causa de la nueva
    throw new DatosInvalidosException("Error en el formulario", e);
}
Cuando una excepción con causa sale por pantalla, Java muestra la traza de la excepción principal y debajo añade una sección "Caused by:" con los detalles de la excepción original. Esto permite rastrear el error hasta su raíz más profunda.