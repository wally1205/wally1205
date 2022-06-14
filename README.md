### Hi there 👋
 
Hola mi nombre es Walter Tutzauer.
Curso la carrera de Ingenieria en computacion, en la UNRN (Universidad Nacional de Rio Negro)
## *Estas son pruebas que estoy realizando*
Esto esta muy bueno .... jo jo jo

**********************************************************************************************
# Control de Versiones - Una breve historia de Git
### *Una breve historia de Git*
Como muchas de las grandes cosas en esta vida, Git comenzó con un poco de destrucción creativa y una gran polémica.

El kernel de Linux es un proyecto de software de código abierto con un alcance bastante amplio. Durante la mayor parte del mantenimiento del kernel de Linux (1991-2002), los cambios en el software se realizaban a través de parches y archivos. En el 2002, el proyecto del kernel de Linux empezó a usar un DVCS propietario llamado BitKeeper.

En el 2005, la relación entre la comunidad que desarrollaba el kernel de Linux y la compañía que desarrollaba BitKeeper se vino abajo y la herramienta dejó de ser ofrecida de manera gratuita. Esto impulsó a la comunidad de desarrollo de Linux (y en particular a Linus Torvalds, el creador de Linux) a desarrollar su propia herramienta basada en algunas de las lecciones que aprendieron mientras usaban BitKeeper. Algunos de los objetivos del nuevo sistema fueron los siguientes:

    * Velocidad
    * Diseño sencillo
    * Gran soporte para desarrollo no lineal (miles de ramas paralelas)
    * Completamente distribuido
    * Capaz de manejar grandes proyectos (como el kernel de Linux) eficientemente (velocidad y tamaño de los datos)

Desde su nacimiento en el 2005, Git ha evolucionado y madurado para ser fácil de usar y conservar sus características iniciales. Es tremendamente rápido, muy eficiente con grandes proyectos y tiene un increíble sistema de ramificación (branching) para desarrollo no lineal (véase [ch03-git-branching])

### *Fundamentos de Git*
Entonces, ¿qué es Git en pocas palabras? Es muy importante entender bien esta sección, porque si entiendes lo que es Git y los fundamentos de cómo funciona, probablemente te será mucho más fácil usar Git efectivamente. A medida que aprendas Git, intenta olvidar todo lo que posiblemente conoces acerca de otros VCS como Subversion y Perforce. Hacer esto te ayudará a evitar confusiones sutiles a la hora de utilizar la herramienta. Git almacena y maneja la información de forma muy diferente a esos otros sistemas, a pesar de que su interfaz de usuario es bastante similar. Comprender esas diferencias evitará que te confundas a la hora de usarlo.

### *Otros softwares de controles de versiones (Top 5)*
* Git: es una de las mejores herramientas de control de versiones disponible en el mercado actual. Es un modelo de repositorio distribuido compatible con sistemas y protocolos existentes como HTTP, FTP, SSH y es capaz de manejar eficientemente proyectos pequeños a grandes.
* CVS: es otro sistema de control de versiones muy popular. Es un modelo de repositorio cliente-servidor donde varios desarrolladores pueden trabajar en el mismo proyecto en paralelo. El cliente CVS mantendrá actualizada la copia de trabajo del archivo y requiere intervención manual sólo cuando ocurre un conflicto de edición.
* Apache Subversion (SVN): abreviado como SVN, apunta a ser el sucesor más adecuado. Es un modelo de repositorio cliente-servidor donde los directorios están versionados junto con las operaciones de copia, eliminación, movimiento y cambio de nombre.
* Mercurial: es una herramienta distribuida de control de versiones que está escrita en Python y destinada a desarrolladores de software. Los sistemas operativos que admite son similares a Unix, Windows y macOS. Tiene un alto rendimiento y escalabilidad con capacidades avanzadas de ramificación y fusión y un desarrollo colaborativo totalmente distribuido. Además, posee una interfaz web integrada.
* Monotone: está escrito en C ++ y es una herramienta para el control de versiones distribuido. El sistema operativo que admite incluye Unix, Linux, BSD, Mac OS X y Windows. Brinda un buen apoyo para la internacionalización y localización. Además, utiliza un protocolo personalizado muy eficiente y robusto llamado Netsync.
-----------------------------------------------------------------------------
### *Grep y Sed*
En esta entrada vamos a ver parte de las páginas man de los comandos grep y sed, así como algunos ejemplos para entrar en contacto con estas potentes herramientas de búsqueda y flujo de texto.
grep : Busca en archivos cadenas de texto y nos devuelve el nombre del archivo y si además es un archivo de texto nos devolverá la línea que contiene dicho patrón.  La sintaxis de grep es:
grep [opciones] exp_regular [archivos]

Opciones:
* Si no queremos que nos muestre la línea que contiene el patrón pero si un número que indica cuantas líneas lo contienen: -c, –count
* Si no queremos hacer distinción entre mayúsculas y minúsculas: -i, –ignore-case
* Buscar de forma recursiva: -r, –recursive
* Si en vez de una exp_regular/patrón queremos pasar un archivo con un texto como patrón: -f, –file <archivo> .
* Para usar expresiones regulares extendidas (que contienen metacaracteres como ?, +, |, {},()) :-E, –extended-regexp . Esto es igual a egrep
* Si queremos hacer una búsqueda de varias cadenas de texto (opciones diferentes): -F

*Nota:* grep -F es igual a fgrep. No se permite el uso de expresiones regulares. Las opciones a buscar deben de ir en líneas separadas. El siguiente ejemplo busca trastero o garaje en un archivo de texto

fgrep trastero
garaje archivo.txt

Para negar, o buscar todo lo que no coincida: -v
Mostrar el número de línea en la cual se ha encontrado el patrón (válido para grep, egrep y fgrep): -n
Para mostrar líneas donde el patrón no es parte de una palabra si no una palabra completa: -w
Devolver el nombre del archivo en el que se ha encontrado el patrón y no sus líneas: -l

**Ejemplos:**
Busca de forma recursiva en /etc/ todos los archivos que contienen la palabra eth0 o eth1
$grep -r eth[01] /etc/*
El uso de * implica que pueda haber 0 o mas ‘i’ en palabras que contengan como mínimo ‘da’.
$grep dai* archivo.txt
Usamos la salida de ps como entrada de grep
$ps ax | grep inetd

En este ejemplo recalcaremos varias cosas, como por ejemplo, podríamos haber usado el comando «egrep» que es igual que usar «grep -E», el entrecomillado de la expresión regular es vital, de lo contrario el shell podría hacer una mala interpretación de los metacaracteres, y para terminar la explicación de que hace en este caso grep: busca en /etc/ archivos que contengan o bien el nombre de host de alberto o de paula y que además contenga el número 15
$grep -E "(alberto\.nebul4ck\.com|paula\.nebul4ck\.es).*15" /etc/*

**SED:** Es un ‘Stream EDitor’ o editor de flujo que no modifica el contenido del archivo original si no una copia e imprime por pantalla las líneas procesadas o aquellas que han sufrido cambios (esto depende de la opción que le pasemos). La sintaxis de sed es:
sed [-n] [-e comando] [-f archivo-comandos] archivo [> guardar_cambios]

**Explicación de la sintaxis:**
* -n : Esta opción hace que no se impriman por pantalla las líneas procesadas. Podemos imprimir solo las que han experimentado modificaciones siempre y cuando utilicemos la bandera ‘flag’ p (print) que veremos a continuación.
* -e : Con esta opción indicamos que estamos pasando comandos por la línea de comandos y no a través de un archivo. Se puede omitir. Los comandos pueden ir acompañados de banderas que modifican su comportamiento
* -f archivo-comandos : Podemos indicar comandos desde un archivo (1 por línea)

Comandos sed:
    d : Elimina las filas
    p : Imprime las líneas que ha experimentado cambios.
    q : quit. Recorrer un archivo e imprimir una línea y sale.

*Nota:* p y q unidos es mas efectivo, ya que no se recorre todo el archivo $ sed -n ‘3{p;q}’ archivo.txt
    s : sustitución.
    a\ : Agregar texto
    i\ : Insertar texto
    c\ : Cambiar texto
    r : Leer archivo
    = : Muestra el número de línea donde se encontró el patrón.

Podemos pasar varios comandos separados por ‘;‘ :
$sed -n 's/antiguos/MODIFICADO/g;p;=' archivo.txt
    O agrupados por ‘{}‘ cuyo uso es mas habitual en archivos de comandos sed :
$sed -n '{ s/antiguos/MODIFICADO/g; {p; {=; }}}' archivo.txt

Pasar varios comandos desde un script sed:
$cat script.sed
s/antiguos/MODIFICADO/g
p
=
$ sed -n -f script.sed archivo.txt
Vamos a ver el uso de los comandos sed:

    Sustituir patron1 por patron2. Por defecto sed solo sustituirá la primera coincidencia de cada línea. Si añadimos una g final sustituirá todas las coincidencias de todas las líneas.

sed s/patrón1/patrón2/g archivo.txtx
    Si queremos solo sustituir la tercera coincidencia de una linea:
sed s3/patron1/patrón2 archivo.txt
    Si por el contrario queremos sustituir la primera coincidencia de patrón1 en la tercera línea:
sed 3s/patrón1/patrón2 archivo.txt
    Podemos sustituir todas las coincidencias de patrón 1 que ocurran desde la línea 5 a la línea 9:
sed 5-9s/patron1/patron2/g archivo.txt

------------------------------------------------------------------------------------------
### *Expresiones Regulares*
Las expresiones regulares son un medio para describir patrones de texto. Imaginemos que no sólo queremos buscar en un texto todas las líneas que contienen una palabra, como por ejemplo Barcelona, sino que sólo nos interesan las líneas que empiezan por la palabra Barcelona, pero no las que contengan la palabra en cualquier otra posición. Describir el patrón “Barcelona” es trivial, tan sólo hay que escribir “Barcelona”, pero ¿cómo podemos describir “La línea comienza por la palabra Barcelona”. Las expresiones regulares permiten describir este tipo de patrones de texto y muchos más por lo que nos serán de una gran utilidad. Además en Unix las expresiones regulares tienen un amplio soporte, tanto en las herramientas de procesamiento de ficheros de texto (grep), o en los editores de texto (vi, emacs) como en los lenguajes de programación (Perl, Python). El único inconveniente de las expresiones regulares es que su sintaxis no es trivial y que además varía ligeramente entre distintas herramientas.


### *Referencias Bibliográficas*
Drauta (11 febrero 2020) *5-softwares-de-control-de-versiones* https://www.drauta.com
Sobre el Control de Versiones - *Una breve historia de Git* https://git-scm.com 
Nebul4ck (30 agosto 2018) *GREP & SED* https://nebul4ck.wordpress.com/2015/02/19/uso-de-grep-y-sed/
*Expresiones Regulares* https://bioinf.comav.upv.es/courses/unix/expresiones_regulares.html

#### Walter Tutzauer 
#### wally1205@gmail.com
#### Ingenieria en computacion 2022

**********************************************************************************************

<!--
**wally1205/wally1205** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

** Here are some ideas to get you started: **

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
