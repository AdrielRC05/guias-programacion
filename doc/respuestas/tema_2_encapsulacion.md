1. En Programación Orientada a Objetos (POO), ¿Qué buscan la encapsulación y la ocultación de información? Enumera brevemente algunas ventajas de la ocultación de información.
Respuesta
La encapsulación busca agrupar en una misma unidad (la clase) tanto los datos (atributos) como las funciones que operan sobre ellos (métodos). Por su parte, la ocultación de información es el mecanismo que restringe el acceso directo a los componentes internos de esa unidad, permitiendo que el objeto se comporte como una "caja negra" hacia el exterior.

Entre las ventajas principales se encuentran el aislamiento de errores, ya que si un dato es incorrecto, se sabe exactamente qué métodos de la clase pudieron modificarlo; la facilidad de mantenimiento, que permite cambiar la estructura interna sin romper el código que usa la clase; y la protección de la integridad, evitando que agentes externos pongan al objeto en un estado inconsistente.

2. ¿Qué se entiende por la interfaz pública de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.
Respuesta
La interfaz pública se define como el conjunto de métodos y constantes que una clase expone al exterior para que otros objetos puedan interactuar con ella. Es, esencialmente, el "contrato" o el manual de uso que especifica qué servicios ofrece la clase sin revelar cómo están implementados internamente.

La relación con la ocultación es de complementariedad: mientras la ocultación "esconde" los detalles técnicos y los datos sensibles, la interfaz pública "muestra" los puntos de entrada autorizados. Gracias a esta separación, se garantiza que los usuarios de la clase solo dependan de la firma de los métodos y no de la representación interna de los datos.

3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la interfaz pública de una clase? ¿Es fácil cambiarla?
Respuesta
El diseño de la interfaz pública es crítico porque representa el compromiso de la clase con el resto del sistema. Una vez que otros programadores o módulos empiezan a utilizar esos métodos públicos, cualquier cambio en ellos (como eliminar un método o cambiar sus parámetros) provocará errores de compilación en todo el código dependiente.

Por tanto, no es fácil cambiarla una vez publicada. Mientras que el interior de los métodos (la implementación privada) puede modificarse libremente para optimizar el rendimiento, la interfaz pública debe permanecer estable para asegurar la compatibilidad y evitar el efecto dominó de errores en el software.

4. ¿Qué son las invariantes de clase y por qué la ocultación de información nos ayuda?
Respuesta
Una invariante de clase es una condición o regla que debe cumplirse siempre para que un objeto se considere válido. Por ejemplo, en una clase Fecha, una invariante sería que el mes siempre esté en el rango de 1 a 12. Son reglas lógicas que definen la salud interna del objeto durante todo su ciclo de vida.

La ocultación de información es fundamental aquí porque, al hacer los atributos privados, se impide que un código externo asigne valores ilegales directamente (como mes = 99). Al centralizar el acceso a través de métodos controlados, la clase puede validar los datos antes de aceptarlos, garantizando que las invariantes nunca se rompan.

5. Pon un ejemplo de una clase Punto en Java... ¿Cuál es la interfaz pública de la clase Punto? ¿Qué significa public y private?
Respuesta
Java
public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
La interfaz pública de esta clase está compuesta por el constructor Punto(double, double) y el método calcularDistanciaAOrigen(). Estos son los únicos elementos accesibles desde fuera de la clase.

En Java, private indica que el miembro solo es accesible desde el código que reside dentro de la misma clase (similar a lo que se intenta simular en C con archivos fuente y cabeceras restringidas). Por el contrario, public indica que cualquier otra clase del programa puede acceder a dicho miembro.

6. En Java, ¿A quiénes se pueden aplicar los modificadores public o private?
Respuesta
Estos modificadores se pueden aplicar a los miembros de la clase, que incluyen tanto a las variables (atributos) como a las funciones (métodos) y constructores. Su uso determina qué partes del objeto son visibles para otros programadores y qué partes son de uso estrictamente interno.

Además, estos modificadores pueden aplicarse a la propia definición de la clase. Una clase pública es visible para todo el proyecto, mientras que una clase con visibilidad restringida (como las clases internas o las de nivel de paquete) limita quién puede instanciar objetos de ese tipo.

7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?
Respuesta
Sí, existen niveles intermedios. En Java, además de public y private, existe el modificador protected (relacionado con la herencia) y la visibilidad por defecto (package-private), que ocurre cuando no se escribe ningún modificador y permite el acceso solo a clases dentro del mismo paquete.

En otros lenguajes como C++, la estructura es similar con public, private y protected. Algunos lenguajes modernos incluyen conceptos como internal (visible solo dentro del mismo módulo o biblioteca), permitiendo un control más granular sobre cómo se comparte el código en proyectos de gran escala.

8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo...
Respuesta
La respuesta correcta es la (a). En Java, la visibilidad privada es a nivel de clase, no a nivel de objeto. Esto significa que una instancia de la clase Punto puede acceder a los atributos privados de otra instancia de la clase Punto.

Java
public double calcularDistanciaAPunto(Punto otro) {
    // Es legal acceder a otro.x y otro.y aunque sean privados
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}
Esto se permite porque se asume que el programador de la clase conoce la implementación de la misma y no violará sus propias invariantes. El acceso está restringido para "extraños" (otras clases), pero no entre "compañeros" del mismo tipo.

9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?
Respuesta
Los getters y setters (también llamados accesores y mutadores) son métodos públicos diseñados para leer o modificar el valor de un atributo privado, respectivamente. El "getter" devuelve el valor del dato y el "setter" recibe un parámetro para actualizarlo.

Su propósito no es solo dar acceso, sino actuar como filtros. Un "setter" permite incluir lógica de validación (por ejemplo, impedir que una edad sea negativa), mientras que un "getter" podría devolver una copia del dato o un valor calculado, manteniendo siempre el control en manos de la propia clase.

10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?
Respuesta
No se refiere a seguridad contra ataques informáticos externos o encriptación, sino a la robustez y estabilidad del código. Es una seguridad de tipo "estructural" que evita errores accidentales causados por programadores que interactúan con la clase.

Se busca evitar que se manipule el estado interno de un objeto de forma imprevista, lo que podría corromper los datos o causar un cuelgue del sistema (como un puntero nulo o una división por cero). Es, en esencia, protección contra la mala manipulación del software durante su desarrollo.

11. ¿Qué diferencia hay entre miembro de instancia y miembro de clase? ¿Los miembros de clase también se pueden ocultar?
Respuesta
Un miembro de instancia pertenece a cada objeto individual; cada Punto tiene sus propias coordenadas x e y. Un miembro de clase (declarado con static) es compartido por todos los objetos de esa clase; solo existe una copia del dato para todas las instancias.

Los miembros de clase también se pueden ocultar. Un atributo static private puede ser utilizado para llevar una cuenta interna o configuración global de la clase que ningún agente externo debe modificar directamente, aplicando los mismos principios de encapsulación que en los miembros de instancia.

12. Brevemente: ¿Tiene sentido que los constructores sean privados?
Respuesta
Sí, tiene sentido en varios patrones de diseño. Un constructor privado impide que se creen objetos de esa clase usando el operador new desde el exterior. Esto es útil, por ejemplo, cuando se desea controlar estrictamente el número de instancias o cuando la creación del objeto es muy compleja.

En estos casos, la clase suele proporcionar un método público estático (método factoría) que invoca internamente al constructor privado después de realizar ciertas comprobaciones. También se usa en clases que solo contienen utilidades estáticas (como la clase Math de Java), donde no tiene sentido crear objetos.

13. ¿Cómo se indican los miembros de clase en Java? Pon un ejemplo... para saber cuáles son los valores x e y máximos...
Respuesta
Los miembros de clase se indican con la palabra reservada static.

Java
public class Punto {
    private double x, y;
    private static double xMax = Double.NEGATIVE_INFINITY;
    private static double yMax = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        if (x > xMax) xMax = x;
        if (y > yMax) yMax = y;
    }

    public static double getXMax() { return xMax; }
    public static double getYMax() { return yMax; }
}
En este ejemplo, xMax e yMax son compartidos. Cada vez que se crea un punto, se actualizan los valores globales si es necesario.

14. Como sería un método factoría dentro de la clase Punto para construir un Punto a partir de dos coordenadas, pero que las redondee al entero más cercano. ¿Has usado static?
Respuesta
Java
public static Punto crearPuntoRedondeado(double x, double y) {
    double xRedondeado = Math.round(x);
    double yRedondeado = Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}
Sí, se ha usado static. Es imprescindible porque un método factoría debe poder ejecutarse antes de que el objeto exista. Si no fuera estático, necesitaríamos un objeto Punto para poder llamar al método que crea un Punto, lo cual sería una contradicción lógica.

15. Cambia la implementación de Punto. En vez de dos double, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.
Respuesta
Java
public class Punto {
    private double[] coordenadas = new double[2];

    public Punto(double x, double y) {
        this.coordenadas[0] = x;
        this.coordenadas[1] = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coordenadas[0] * coordenadas[0] + 
                         coordenadas[1] * coordenadas[1]);
    }
}
A pesar de haber cambiado radicalmente cómo se guardan los datos (de variables sueltas a un array), cualquier código externo que usara new Punto(1.0, 2.0) y p.calcularDistanciaAOrigen() seguirá funcionando perfectamente sin necesidad de ser recompilado o modificado. Esta es la potencia de la ocultación.

16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos? ¿Tiene esto algo que ver con las "invariantes de clase"?
Respuesta
No es mejor declararlo público. La convención estándar en Java es que todos los atributos sean privados. Aunque existan getters y setters para todos ellos, mantener el atributo privado permite que en el futuro se pueda cambiar la lógica interna (como en el ejemplo del array) o añadir validaciones en el setter sin afectar a terceros.

Esto tiene todo que ver con las invariantes de clase. Si el atributo es público, la clase pierde el control y no puede garantizar que sus reglas se cumplan. Con un setter, la clase puede rechazar valores que rompan su lógica interna, manteniendo así la integridad del objeto en todo momento.

17. ¿Qué significa que una clase sea inmutable? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?
Respuesta
Una clase es inmutable cuando sus objetos no pueden cambiar su estado una vez creados. Un método modificador es aquel que altera el estado interno del objeto. Un modificador no siempre es un "setter" tradicional (como setX); puede ser un método como trasladar(double dx, double dy) que cambia las coordenadas.

Las clases inmutables tienen grandes ventajas: son intrínsecamente seguras para hilos (multithreading), son más fáciles de entender y depurar, y pueden compartirse libremente sin miedo a que alguien las modifique por error. En una clase inmutable, los métodos que parecen "modificar" el objeto en realidad devuelven una instancia nueva con los cambios.

18. ¿Es recomendable incluir métodos "setter" siempre y como convención?
Respuesta
No es recomendable. Incluir setters de forma automática para todos los atributos es una práctica que a menudo debilita la encapsulación. Si un objeto no necesita cambiar sus datos después de ser creado, es preferible no proporcionar setters y mantenerlo inmutable o parcialmente inmutable.

El diseño debe guiarse por la necesidad: solo se deben añadir setters si el dominio del problema requiere que ese dato específico cambie durante la vida del objeto. De lo contrario, se exponen innecesariamente las tripas de la clase y se aumenta el riesgo de que el objeto termine en un estado inconsistente.

19. ¿La clase String en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a concatenar muchas veces...?
Respuesta
La clase String es inmutable. Cuando se concatenan dos cadenas (por ejemplo, con el operador +), no se modifica la cadena original, sino que se crea un objeto String completamente nuevo que contiene el resultado de la unión.

Si se requiere concatenar muchas veces en un bucle, crear miles de objetos temporales es muy ineficiente. En esos casos, se debe utilizar la clase StringBuilder, que está diseñada específicamente para ser mutable y permite construir cadenas largas de forma eficiente antes de convertirlas finalmente a un String.

20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Cómo se deben comparar dos cadenas en Java?
Respuesta
Los objetos se pueden comparar por identidad (si son el mismo objeto en memoria, usando ==) o por contenido (si sus atributos valen lo mismo). En Java, el método equals está diseñado para comparar el contenido de los objetos.

Por defecto, equals se comporta igual que ==, pero las clases suelen "sobrescribirlo" para comparar atributo por atributo. Para comparar dos cadenas de texto (String), siempre se debe usar .equals(), ya que == solo nos diría si son la misma instancia, lo cual suele fallar aunque el texto sea idéntico.

21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos...?
Respuesta
Las clases wrapper (envoltorios) son clases que representan a los tipos primitivos (como int, double, char) como si fueran objetos (Integer, Double, Character). Esto es necesario porque muchas herramientas de Java solo trabajan con objetos y no aceptan primitivos.

En Java, el proceso de convertir un primitivo a su wrapper se llama autoboxing y es automático. No todos los lenguajes tienen tipos primitivos; algunos, como Ruby o Smalltalk, son "puros" y todo es un objeto. Java los mantiene por una cuestión de rendimiento, ya que los primitivos son mucho más rápidos de procesar.

22. ¿En POO qué es un tipo de dato enumerado? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen...?
Respuesta
Un tipo enumerado (enum) es un tipo de dato que permite definir un conjunto fijo de constantes con nombre, como los días de la semana o los meses. En Java, los enumerados son mucho más que simples listas de enteros (como en C); son clases especiales.

Al ser clases, los enum en Java pueden tener atributos, métodos y constructores. Esto mejora la encapsulación porque permite asociar lógica a cada constante. Además, proporcionan seguridad de tipos: el compilador impide que se asigne un valor que no pertenezca a la lista definida, algo que no ocurre si se usan simples enteros o strings.

23. Crea un tipo enumerado en Java que se llame Mes...
Respuesta
Java
public enum Mes {
    ENERO(31, 1), FEBRERO(28, 2), MARZO(31, 3), ABRIL(30, 4),
    MAYO(31, 5), JUNIO(30, 6), JULIO(31, 7), AGOSTO(31, 8),
    SEPTIEMBRE(30, 9), OCTUBRE(31, 10), NOVIEMBRE(30, 11), DICIEMBRE(31, 12);

    private final int dias;
    private final int ordinal;

    private Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }

    public int getDias() { return dias; }
    public int getOrdinal() { return ordinal; }
}
24. Añade a la clase Mes del ejercicio anterior cuatro métodos...
Respuesta
Java
public boolean esDePrimavera(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == MARZO || this == ABRIL || this == MAYO;
    } else {
        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
    }
}

public boolean esDeVerano(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == JUNIO || this == JULIO || this == AGOSTO;
    } else {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    }
}

public boolean esDeOtoño(boolean enHemisferioNorte) {
    return !esDePrimavera(enHemisferioNorte) && !esDeVerano(enHemisferioNorte) && !esDeInvierno(enHemisferioNorte);
}

public boolean esDeInvierno(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    } else {
        return this == JUNIO || this == JULIO || this == AGOSTO;
    }
}