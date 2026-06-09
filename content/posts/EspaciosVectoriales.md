+++
date = '2026-02-03T20:14:08-05:00'
draft = false
title = 'Espacios Vectoriales'
author = 'Ling Sequera'
+++


# La potencia de la abstracción: ¿Por qué nos importan los espacios vectoriales en física?

Hay ideas que son tan extraordinariamente buenas que terminan manifestándose en casi cualquier rincón de la ciencia y sus aplicaciones. En física, resulta casi natural formular la mayoría de las teorías en el lenguaje de los espacios vectoriales. De hecho, históricamente la intuición geométrica y física de los vectores se utilizó mucho antes de que la estructura matemática detrás de ellos fuera rigurosamente formalizada por matemáticos como Giuseppe Peano a finales del siglo XIX.

Desde el punto de vista de la formación en física, solemos abordar los problemas utilizando realizaciones muy concretas: los vectores de posición, velocidad o fuerza en $\mathbb{R}^2$ o $\mathbb{R}^3$, o el espacio-tiempo de Minkowski en $\mathbb{R}^4$. Si bien esto otorga una excelente intuición geométrica para la física clásica, a menudo nos juega una mala pasada. Nos acostumbra a pensar que un vector es únicamente "una flechita con magnitud, dirección y sentido", limitando nuestra comprensión de la estructura matemática general. Esta definición rigurosa y abstracta es la que verdaderamente desbloquea el entendimiento de teorías más profundas —como la mecánica cuántica o la relatividad general— y extiende su aplicación a campos que a primera vista parecerían ajenos a la física.

## El cimiento algebraico: El concepto de campo (o cuerpo)

Antes de hablar de un espacio vectorial, debemos entender sobre qué "suelo" estamos construyendo. Ese suelo es un **campo** (o *cuerpo*, en la terminología matemática en español, denotado usualmente por $\mathbb{K}$). Un campo es un conjunto dotado de dos operaciones (que llamamos suma y producto) que se comportan de manera tan amigable como los números reales: tienen elementos neutros, inversos (salvo para el cero) y cumplen la propiedad distributiva. Los campos más familiares para un físico son los números reales $\mathbb{R}$ y los complejos $\mathbb{C}$.

Sin embargo, para valorar la generalidad de la definición, vale la pena salir de la zona de confort y mirar los **campos finitos** (o campos de Galois, $\mathbb{F}_q$). A primera vista, un conjunto finito donde las operaciones "dan la vuelta" (como la aritmética modular) puede parecer un exotismo matemático sin aplicación física. Pero en computación y teoría de la información, donde el hardware impone límites estrictos y se busca exactitud numérica sin errores de redondeo, los campos finitos son fundamentales.

Por ejemplo, el estándar de cifrado simétrico **AES** (Advanced Encryption Standard), que protege nuestras comunicaciones diarias en la web, realiza todas sus operaciones algebraicas dentro del campo finito $\mathbb{F}_{2^8}$ (el campo de Galois con 256 elementos). Esto demuestra que las reglas del álgebra abstracta funcionan de manera idéntica sin importar si el campo de escalares contiene infinitos elementos continuos o un puñado finito de bits. Si se quiere profundizar en el funcionamiento del cifrado AES sugiero altamente ver este par de videos de Numberphile [AESexplained](https://youtu.be/O4xNJsjtN6E) [AES2](https://youtu.be/-fpVv_T4xwA). Como dato curioso, solo quiero mencionar que este estandar ya está implementado directamente en el hardware de nuestros computadores y celulares, dentro del conjunto de instrucciones del procesador ahi unas cuantas que se encargan del cifrado y descifrado AES, ver [AES instruction set](https://en.wikipedia.org/wiki/AES_instruction_set)

## La estructura de Espacio Vectorial

Con el campo $\mathbb{K}$ definido, podemos formalizar qué es un **espacio vectorial** $V$. No es simplemente un conjunto de objetos; es una estructura algebraica que involucra la interacción de dos conjuntos no vacíos:
1. Un conjunto de **vectores** $V$ (con una operación interna de adición: $+: V \times V \to V$).
2. Un conjunto de **escalares** pertenecientes al campo $\mathbb{K}$.

Ambos conjuntos se vinculan mediante una operación externa llamada multiplicación por un escalar: $\cdot: \mathbb{K} \times V \to V$. Para que esta estructura sea considerada un espacio vectorial, estas operaciones deben cumplir con ocho axiomas clásicos (asociatividad, conmutatividad del grupo aditivo, distributividad respecto a suma de vectores y escalares, etc. [Ver detalles en Axler, *Linear Algebra Done Right*](https://linear.axler.net/)).

Si nos ponemos meticulosos, la adición dentro del campo $\mathbb{K}$ (sumar dos escalares) y la adición dentro del espacio $V$ (sumar dos vectores) son operaciones matemáticamente distintas que actúan sobre conjuntos diferentes. Sin embargo, la notación matemática universal utiliza el mismo símbolo $+$ para ambas. Esta sutil sobrecarga de operadores no genera confusión precisamente gracias a los axiomas de compatibilidad que entrelazan a los vectores con los escalares.

## El poder de la base: Reduciendo lo infinito a lo contable

En lugar de recitar una lista de teoremas típicos de libro de texto, vale la pena detenerse en uno de los resultados más profundos y elegantes del álgebra lineal: **todo espacio vectorial posee una base**. 

Para apreciar esto, solo necesitamos tener claros dos conceptos fundamentales estrechamente vinculados:
*   **Combinación lineal**: La capacidad de construir nuevos vectores sumando vectores escalados, de la forma $\sum_{i} c_i v_i$ con $c_i \in \mathbb{K}$ y $v_i \in V$.
*   **Independencia lineal**: Un conjunto de vectores es independiente si ninguno de ellos puede expresarse como combinación lineal de los demás.

Una **base** de $V$ es un conjunto de vectores linealmente independientes que genera a todo el espacio. El teorema que asegura que *cualquier* espacio vectorial tiene una base ([cuya demostración para el caso general requiere el Lema de Zorn y, por ende, el Axioma de Elección](https://en.wikipedia.org/wiki/Basis_(linear_algebra)#Proof_that_every_vector_space_has_a_basis)) tiene implicaciones prácticas gigantescas. 

Lo verdaderamente relevante de tener una base es la **simplificación**. En lugar de tener que estudiar y operar directamente con los infinitos elementos abstractos de un espacio vectorial, nos basta con estudiar lo que ocurre en los elementos de la base. Cualquier vector del espacio puede escribirse de forma única como una combinación lineal de los elementos de la base. Así, representar un vector se reduce simplemente a dar una lista de números (sus coordenadas).

## El salto al infinito: Espacios de funciones y la necesidad de la Topología

La **dimensión** de un espacio vectorial se define como el cardinal (el número de elementos) de cualquiera de sus bases. Pero qué pasa por ejemplo si consideramos las secuencias infinitas de números reales $x = (x_1, x_2, ...)$, definimos la suma $(x_1+y_1, x_2+y_2, ...)$ y el producto por un escalar $\alpha\in\mathbb{R}$ como $(\alpha x_1, \alpha x_2, ...)$, podemos decir que los elementos $e_i = (0, 0, ..., 1, ...)$ con un 1 en la i-ésima posición y 0 en el resto son linealmente independientes y que cualquier secuencia $x = (x_1, x_2, ...)$ se puede escribir como $x = \sum_{i=1}^{\infty} x_i e_i$. Esta es una base de este espacio vectorial, pero no es una base numerable. Una pregunta que surge es qué significa que un vector sea representable como una suma infinita. Me gusta mencionar este ejemplo porque es como una extensión de $\mathbb{R}^n$ a "$\mathbb{R}^{\infty}$".

En general, en los ejemplos clasicos de **espacios vectoriales de dimensión infinita** los "vectores" suelen ser funciones. Surge una pregunta matemática crucial: si sumamos infinitos vectores (una serie), ¿cómo nos aseguramos de que el resultado de esa suma infinita siga perteneciendo al espacio vectorial? El álgebra pura ya no es suficiente. Para dar sentido a la convergencia y al límite de sumas infinitas, necesitamos dotar al espacio vectorial de una **topología** (una noción de cercanía o vecindad).

Aunque un espacio vectorial de dimensión infinita pueda parecer una abstracción puramente matemática, en la física real es nuestro pan de cada día:

1.  **Electromagnetismo y Ecuaciones Diferenciales**: Al resolver la ecuación de Laplace $\nabla^2 \Phi = 0$ en electrostática, el principio de superposición nos dice que el conjunto de soluciones forma un espacio vectorial. Para satisfacer condiciones de frontera complejas, expresamos la solución general como una suma infinita de funciones de una base ortogonal (como los polinomios de Legendre o los armónicos esféricos).
2.  **Mecánica Cuántica**: Aquí el uso de espacios de dimensión infinita es explícito y fundacional. Los estados físicos de un sistema cuántico viven en un **espacio de Hilbert** $\mathcal{H}$ (un espacio vectorial complejo dotado de un producto interno que, además, es métricamente *completo*). La completitud significa que toda sucesión de Cauchy de vectores converge a un elemento que también pertenece al espacio, lo cual garantiza que las probabilidades sumen 1 y que los estados físicos resultantes de procesos límite sigan siendo físicamente válidos.
3.  **Procesamiento de Señales (Física Aplicada / Ingeniería)**: El análisis de Fourier descompone una señal (función) en una suma infinita (serie de Fourier) de componentes sinusoidales. Cada seno y coseno actúa como un vector de una base ortogonal. Filtrar una señal no es más que proyectar dicho vector sobre un subespacio vectorial específico para eliminar ciertas frecuencias.
4. **Econometría e Inteligencia Artificial**: En la econometría y el aprendizaje automático, se utilizan **espacios vectoriales de dimensión infinita** para modelar distribuciones de probabilidad. Aunque a menudo trabajamos con muestras finitas, los modelos teóricos se basan en espacios de funciones donde los "vectores" son distribuciones de probabilidad. Por ejemplo, el espacio de funciones medibles con valor real en un espacio de probabilidad es un espacio vectorial. 

## Lo que un espacio vectorial NO es: La separación de estructuras

Es crucial que un estudiante note algo que a menudo se pasa por alto: **en su definición pura, un espacio vectorial no tiene noción de distancia, ángulo, tamaño o cercanía**. 

Conceptos como la longitud de un vector o el ángulo entre dos vectores no son intrínsecos al espacio vectorial. Para tenerlos, debemos añadir estructuras algebraicas adicionales:
*   Un **producto interno** (o producto escalar), que nos permite definir ángulos y proyecciones.
*   Una **norma**, que nos da la noción de "tamaño" o longitud.
*   Una **métrica**, que define la distancia entre elementos.

Un espacio vectorial desnudo es puramente algebraico. Al dotarlo paulatinamente de estas capas (espacio vectorial $\to$ espacio prehilbertiano $\to$ espacio normado $\to$ espacio métrico), multiplicamos su utilidad, pero es vital mantener la distinción conceptual para no asumir propiedades que el espacio podría no tener.

## Geometría vs. Álgebra: El espacio físico frente al espacio vectorial

En física, conviene hacer una precisión sutil pero sumamente importante. En mecánica clásica, el espacio donde se mueve una partícula (el espacio físico o *espacio de configuraciones*) no es, en general, un espacio vectorial. Es una estructura geométrica llamada **variedad diferenciable** (como una esfera $S^2$ o una superficie curva). 

¿Por qué importa esto? Porque en una superficie curva no tiene sentido sumar dos "posiciones" ni multiplicar una posición por un número. Sin embargo, en cada punto $p$ de esa variedad, podemos "adjuntar" un espacio vectorial llamado **espacio tangente** $T_p M$. Es en este espacio vectorial donde viven entidades físicas como la velocidad $\vec{v}$, la aceleración o las fuerzas aplicadas en ese instante.

Al estudiar una partícula en un plano llano, solemos usar $\mathbb{R}^2$ tanto para describir las posiciones (como variedad) como para describir las velocidades (como espacio vectorial). Esta feliz coincidencia nos hace olvidar la distinción. Pero al dar el salto a la relatividad general o a sistemas con restricciones, comprender que las posiciones pertenecen a una variedad y las velocidades físicas viven en espacios vectoriales tangentes independientes es la clave para no perder el rumbo.

Cuando comence a escribir este texto mi intención era solo resaltar ciertos aspectos que son muy elementales una vez los conoces, pero que me hubiera gustado saber cuando estudiaba física porque creo por podría haber ententido mejor. Quería que fuera un pequeño preambulo para describir la implentación física de vectores matrices y operaciones dentro de una GPU, me he dado cuenta en este punto que hay mucho por decir y ya está suficientemente extenso, asi que lo reservaré para sus propios espacios y dejaré este hasta este punto.