# Control de Versiones - Una breve historia de Git
### *Una breve historia de Git*
Como muchas de las grandes cosas en esta vida, Git comenz� con un poco de destrucci�n creativa y una gran pol�mica.

El kernel de Linux es un proyecto de software de c�digo abierto con un alcance bastante amplio. Durante la mayor parte del mantenimiento del kernel de Linux (1991-2002), los cambios en el software se realizaban a trav�s de parches y archivos. En el 2002, el proyecto del kernel de Linux empez� a usar un DVCS propietario llamado BitKeeper.

En el 2005, la relaci�n entre la comunidad que desarrollaba el kernel de Linux y la compa��a que desarrollaba BitKeeper se vino abajo y la herramienta dej� de ser ofrecida de manera gratuita. Esto impuls� a la comunidad de desarrollo de Linux (y en particular a Linus Torvalds, el creador de Linux) a desarrollar su propia herramienta basada en algunas de las lecciones que aprendieron mientras usaban BitKeeper. Algunos de los objetivos del nuevo sistema fueron los siguientes:

    * Velocidad
    * Dise�o sencillo
    * Gran soporte para desarrollo no lineal (miles de ramas paralelas)
    * Completamente distribuido
    * Capaz de manejar grandes proyectos (como el kernel de Linux) eficientemente (velocidad y tama�o de los datos)

Desde su nacimiento en el 2005, Git ha evolucionado y madurado para ser f�cil de usar y conservar sus caracter�sticas iniciales. Es tremendamente r�pido, muy eficiente con grandes proyectos y tiene un incre�ble sistema de ramificaci�n (branching) para desarrollo no lineal (v�ase [ch03-git-branching])

### *Fundamentos de Git*
Entonces, �qu� es Git en pocas palabras? Es muy importante entender bien esta secci�n, porque si entiendes lo que es Git y los fundamentos de c�mo funciona, probablemente te ser� mucho m�s f�cil usar Git efectivamente. A medida que aprendas Git, intenta olvidar todo lo que posiblemente conoces acerca de otros VCS como Subversion y Perforce. Hacer esto te ayudar� a evitar confusiones sutiles a la hora de utilizar la herramienta. Git almacena y maneja la informaci�n de forma muy diferente a esos otros sistemas, a pesar de que su interfaz de usuario es bastante similar. Comprender esas diferencias evitar� que te confundas a la hora de usarlo.

### *Otros softwares de controles de versiones (Top 5)*
* Git: es una de las mejores herramientas de control de versiones disponible en el mercado actual. Es un modelo de repositorio distribuido compatible con sistemas y protocolos existentes como HTTP, FTP, SSH y es capaz de manejar eficientemente proyectos peque�os a grandes.
* CVS: es otro sistema de control de versiones muy popular. Es un modelo de repositorio cliente-servidor donde varios desarrolladores pueden trabajar en el mismo proyecto en paralelo. El cliente CVS mantendr� actualizada la copia de trabajo del archivo y requiere intervenci�n manual s�lo cuando ocurre un conflicto de edici�n.
* Apache Subversion (SVN): abreviado como SVN, apunta a ser el sucesor m�s adecuado. Es un modelo de repositorio cliente-servidor donde los directorios est�n versionados junto con las operaciones de copia, eliminaci�n, movimiento y cambio de nombre.
* Mercurial: es una herramienta distribuida de control de versiones que est� escrita en Python y destinada a desarrolladores de software. Los sistemas operativos que admite son similares a Unix, Windows y macOS. Tiene un alto rendimiento y escalabilidad con capacidades avanzadas de ramificaci�n y fusi�n y un desarrollo colaborativo totalmente distribuido. Adem�s, posee una interfaz web integrada.
* Monotone: est� escrito en C ++ y es una herramienta para el control de versiones distribuido. El sistema operativo que admite incluye Unix, Linux, BSD, Mac OS X y Windows. Brinda un buen apoyo para la internacionalizaci�n y localizaci�n. Adem�s, utiliza un protocolo personalizado muy eficiente y robusto llamado Netsync.
-----------------------------------------------------------------------------
### *Grep y Sed*
En esta entrada vamos a ver parte de las p�ginas man de los comandos grep y sed, as� como algunos ejemplos para entrar en contacto con estas potentes herramientas de b�squeda y flujo de texto.
grep : Busca en archivos cadenas de texto y nos devuelve el nombre del archivo y si adem�s es un archivo de texto nos devolver� la l�nea que contiene dicho patr�n.  La sintaxis de grep es:
grep [opciones] exp_regular [archivos]

Opciones:
* Si no queremos que nos muestre la l�nea que contiene el patr�n pero si un n�mero que indica cuantas l�neas lo contienen: -c, �count
* Si no queremos hacer distinci�n entre may�sculas y min�sculas: -i, �ignore-case
* Buscar de forma recursiva: -r, �recursive
* Si en vez de una exp_regular/patr�n queremos pasar un archivo con un texto como patr�n: -f, �file <archivo> .
* Para usar expresiones regulares extendidas (que contienen metacaracteres como ?, +, |, {},()) :-E, �extended-regexp . Esto es igual a egrep
* Si queremos hacer una b�squeda de varias cadenas de texto (opciones diferentes): -F

*Nota:* grep -F es igual a fgrep. No se permite el uso de expresiones regulares. Las opciones a buscar deben de ir en l�neas separadas. El siguiente ejemplo busca trastero o garaje en un archivo de texto

fgrep trastero
garaje archivo.txt

Para negar, o buscar todo lo que no coincida: -v
Mostrar el n�mero de l�nea en la cual se ha encontrado el patr�n (v�lido para grep, egrep y fgrep): -n
Para mostrar l�neas donde el patr�n no es parte de una palabra si no una palabra completa: -w
Devolver el nombre del archivo en el que se ha encontrado el patr�n y no sus l�neas: -l

**Ejemplos:**
Busca de forma recursiva en /etc/ todos los archivos que contienen la palabra eth0 o eth1
$grep -r eth[01] /etc/*
El uso de * implica que pueda haber 0 o mas �i� en palabras que contengan como m�nimo �da�.
$grep dai* archivo.txt
Usamos la salida de ps como entrada de grep
$ps ax | grep inetd

En este ejemplo recalcaremos varias cosas, como por ejemplo, podr�amos haber usado el comando �egrep� que es igual que usar �grep -E�, el entrecomillado de la expresi�n regular es vital, de lo contrario el shell podr�a hacer una mala interpretaci�n de los metacaracteres, y para terminar la explicaci�n de que hace en este caso grep: busca en /etc/ archivos que contengan o bien el nombre de host de alberto o de paula y que adem�s contenga el n�mero 15
$grep -E "(alberto\.nebul4ck\.com|paula\.nebul4ck\.es).*15" /etc/*

**SED:** Es un �Stream EDitor� o editor de flujo que no modifica el contenido del archivo original si no una copia e imprime por pantalla las l�neas procesadas o aquellas que han sufrido cambios (esto depende de la opci�n que le pasemos). La sintaxis de sed es:
sed [-n] [-e comando] [-f archivo-comandos] archivo [> guardar_cambios]

**Explicaci�n de la sintaxis:**
* -n : Esta opci�n hace que no se impriman por pantalla las l�neas procesadas. Podemos imprimir solo las que han experimentado modificaciones siempre y cuando utilicemos la bandera �flag� p (print) que veremos a continuaci�n.
* -e : Con esta opci�n indicamos que estamos pasando comandos por la l�nea de comandos y no a trav�s de un archivo. Se puede omitir. Los comandos pueden ir acompa�ados de banderas que modifican su comportamiento
* -f archivo-comandos : Podemos indicar comandos desde un archivo (1 por l�nea)

Comandos sed:
    d : Elimina las filas
    p : Imprime las l�neas que ha experimentado cambios.
    q : quit. Recorrer un archivo e imprimir una l�nea y sale.

*Nota:* p y q unidos es mas efectivo, ya que no se recorre todo el archivo $ sed -n �3{p;q}� archivo.txt
    s : sustituci�n.
    a\ : Agregar texto
    i\ : Insertar texto
    c\ : Cambiar texto
    r : Leer archivo
    = : Muestra el n�mero de l�nea donde se encontr� el patr�n.

Podemos pasar varios comandos separados por �;� :
$sed -n 's/antiguos/MODIFICADO/g;p;=' archivo.txt
    O agrupados por �{}� cuyo uso es mas habitual en archivos de comandos sed :
$sed -n '{ s/antiguos/MODIFICADO/g; {p; {=; }}}' archivo.txt

Pasar varios comandos desde un script sed:
$cat script.sed
s/antiguos/MODIFICADO/g
p
=
$ sed -n -f script.sed archivo.txt
Vamos a ver el uso de los comandos sed:

    Sustituir patron1 por patron2. Por defecto sed solo sustituir� la primera coincidencia de cada l�nea. Si a�adimos una g final sustituir� todas las coincidencias de todas las l�neas.

sed s/patr�n1/patr�n2/g archivo.txtx
    Si queremos solo sustituir la tercera coincidencia de una linea:
sed s3/patron1/patr�n2 archivo.txt
    Si por el contrario queremos sustituir la primera coincidencia de patr�n1 en la tercera l�nea:
sed 3s/patr�n1/patr�n2 archivo.txt
    Podemos sustituir todas las coincidencias de patr�n 1 que ocurran desde la l�nea 5 a la l�nea 9:
sed 5-9s/patron1/patron2/g archivo.txt

------------------------------------------------------------------------------------------
### *Expresiones Regulares*
Las expresiones regulares son un medio para describir patrones de texto. Imaginemos que no s�lo queremos buscar en un texto todas las l�neas que contienen una palabra, como por ejemplo Barcelona, sino que s�lo nos interesan las l�neas que empiezan por la palabra Barcelona, pero no las que contengan la palabra en cualquier otra posici�n. Describir el patr�n �Barcelona� es trivial, tan s�lo hay que escribir �Barcelona�, pero �c�mo podemos describir �La l�nea comienza por la palabra Barcelona�. Las expresiones regulares permiten describir este tipo de patrones de texto y muchos m�s por lo que nos ser�n de una gran utilidad. Adem�s en Unix las expresiones regulares tienen un amplio soporte, tanto en las herramientas de procesamiento de ficheros de texto (grep), o en los editores de texto (vi, emacs) como en los lenguajes de programaci�n (Perl, Python). El �nico inconveniente de las expresiones regulares es que su sintaxis no es trivial y que adem�s var�a ligeramente entre distintas herramientas.


### *Referencias Bibliogr�ficas*
Drauta (11 febrero 2020) *5-softwares-de-control-de-versiones* https://www.drauta.com
Sobre el Control de Versiones - *Una breve historia de Git* https://git-scm.com 
Nebul4ck (30 agosto 2018) *GREP & SED* https://nebul4ck.wordpress.com/2015/02/19/uso-de-grep-y-sed/
*Expresiones Regulares* https://bioinf.comav.upv.es/courses/unix/expresiones_regulares.html

#### Walter Tutzauer 
#### wally1205@gmail.com
#### Ingenieria en computacion 2022