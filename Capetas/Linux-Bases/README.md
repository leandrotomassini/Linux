## Bases de Linux  
GNU/Linux permite muchas formas de poder acceder al sistema operativo, a través de interfaces gráficas, consolas virtuales e incluso a través de la red.  

En este curso vamos a explicar, gracias a nuestra máquina virtual, el método de acceso local (interfaz gráfica y consola virtual) y el método de acceso en remoto a través del servicio ssh.  

***Método local:***  
Interfaz gráfica: Esta interfaz es la que nos aparece por defecto en el arranque del sistema operativo Ubuntu. Nos permite ejecutar una terminal en modo gráfico
Terminal virtual: Este tipo de terminales se pueden visualizar en el sistema pulsando la combinación de teclas Alt + Ctrl + F1-F6. Linux crea por defecto 6 terminales virtuales para poder usar y dos displays gráficos, ubicados en Ctrl + Alt + F7-F8.  
***Método remoto:***  
SSH: Ssh es el acrónimo de Secure SHell y permite el acceso a una terminal de nuestro sistema a través de la red con la característica de aportar seguridad gracias a la encriptación de sus comunicaciones. Es un servicio de estructura cliente-servidor, donde el servidor abre el puerto 22 para admitir conexiones y el cliente utiliza la aplicación para conectarse a dicho puerto.  

* Para instalar ssh: sudo apt-get install openssh-server  
* Para conectarse medianse ssh: ssh osboxes@localhost // Me conectaria a si mismo  

## Estructura de directorios: 

Para comprender la estructura de directorios de Linux hay que analizar y conocer previamente el estándar FHS (Filesystem Hierarchy Standard). Esta norma determina como se definen los directorios principales y los contenidos del sistema operativo GNU/Linux, llegando a completarse en 1995.  

Para entender cómo funciona Linux y su relación con los elementos físicos de almacenamiento, primero vamos a verlo desde el lado del software y a partir de ahí desarrollaremos la relación entre esto y los componentes físicos (particiones).  

Esta es la composición del árbol de directorios de un sistema Linux:  

![](https://openwebinars.net/media/django-summernote/2015-09-14/b4f21c23-8e43-4800-9c0f-5f8f11555003.png)

Cada directorio que cuelga directamente del raíz (/) tiene un propósito concreto en el sistema. Según el estándar FHS, cada directorio tiene el siguiente cometido:  
### Directorios Importantes y sus Contenidos  

FHS define algunos directorios con mucha precisión. Los más comunes definidos por FHS o utilizados por convención, son los siguientes:  

***/ :*** Los sistemas de ficheros Linux tienen su raíz en un mismo directorio conocido como sistema de ficheros raíz o directorio raíz. Todos los demás directorios se ramifican desde éste. Linux no utiliza letras de unidad sino que las particiones o discos extraíbles se montan en un punto dentro del sistema de ficheros raíz. Algunos directorios críticos deben residir siempre en la partición raíz pero otros pueden encontrarse en particiones independientes. No se debe confundir el directorio /root con el directorio raíz.  

***/boot :*** Contiene ficheros estáticos y no compartibles relacionados con el arranque del ordenador. Algunos sistemas imponen limites particulares a /boot , por ejemplo, en BIOS antiguas y versiones antiguas del LILO pueden requerir que /boot se encuentre por debajo del cilindro 1024 del disco duro. También puede que se requiera que /boot sea una partición independiente.
  
***/bin :*** Contiene algunos ficheros ejecutables que son accesibles para todos los usuarios y constituyen los comandos más importantes que pueden ejecutar los usuarios normales. Contiene ficheros estáticos. Sus ficheros son compartibles pero son tan importantes para el funcionamiento básico del ordenador que este directorio casi nunca se comparte. Cada cliente debe tener su directorio /bin en local.  

***/sbin :*** Es similar a /bin pero contiene programas que sólo ejecuta el administrador. Es estático y en teoría compartible. En la práctica sin embargo, no tiene sentido compartirlo.  

***/lib :*** Contiene bibliotecas de programa que son código compartido por muchos programas y que se almacenan en ficheros independientes, para ahorrar RAM y espacio en disco. /lib/modules contiene módulos o drivers que se pueden cargar y descargar según necesitemos. Es estático y teóricamente compartible aunque en la práctica no se comparten.  

***/usr :*** Aloja el grueso de los programas de un ordenador Linux. Tiene un contenido compartible y estático lo que permite montarlo en modo sólo lectura. Se puede compartir con otros sistemas Linux; muchos administradores separan /usr en una partición independiente aunque no es necesario. Contiene algunos subdirectorios similares a los del directorio raíz como /usr/bin y /usr/lib , que contienen programas y bibliotecas que no son totalmente críticos para el funcionamiento del ordenador.  

***/usr/local :*** Contiene subdirectorios que reflejan la organización de /usr . Aloja los ficheros que instala localmente el administrador y es un área a salvo de las actualizaciones automáticas de todo el SO. Después de la instalación de Linux debería estar vacío, excepto para determinados subdirectorios stub. Se suele separar en una partición para protegerlo de las reinstalaciones del SO.  

***/usr/X11R6 :*** Alberga los ficheros relacionados con el sistema X Window (entorno GUI). Contiene subdirectorios similares a los de /usr, como /usr/X11R6/bin y /usr/X11R6/lib.  

***/opt :*** Es similar a /usr/local pero está pensado para los paquetes que no vienen con el SO como los procesadores de texto o juegos comerciales, que se guardan es sus propios subdirectorios. El contenido de /opt es estático y compartible. Se suele separar en su propia partición para convertirlo en un enlace simbólico a un subdirectorio de /usr/local.  

***/home :*** contiene los datos de los usuarios y es compartible y variable. Se considera opcional en FHS, pero, en la práctica lo opcional es el nombre. El directorio /home con mucha frecuencia reside en su propia partición.  

***/etc:*** Contiene archivos de configuración del sistema específicos del Host de todo el sistema.  

***/root :*** Es el directorio home del usuario root. Como la cuenta de root es tan crítica y específica del sistema, este directorio variable no es realmente compartible.  

***/var :*** Contiene ficheros efímeros de varios tipos, de registro del sistema, de cola de impresión, de correo y news, etc. El contenido del directorio es variable pues algunos subdirectorios son compartibles y otros no. Se suele colocar /var en su propia partición, sobre todo si el sistema registra una gran actividad en /var.  

***/tmp :*** Es donde se crean los archivos temporales y variables que necesitan los programas. La mayoría de las distribuciones limpian este directorio periódicamente en el inicio. Este directorio raramente se comparte pero se suele poner en una partición independiente para que los procesos no controlados no provoquen problemas en el sistema de ficheros al ocupar demasiado.  

***/mnt :*** La finalidad de este directorio es albergar el montaje de los dispositivos. En la estructura de directorios, algunas distribuciones crean subdirectorios dentro de /mnt para que hagan de puntos de montado; otras utilizan directamente /mnt o incluso puntos de montado independientes de /mnt, como /floppy o /cdrom . FHS sólo menciona /mnt y no especifica cómo se ha de utilizar. Los medios montados en esta partición pueden ser estáticos o variables y, por norma general son compartibles.  

***/media :*** Es una parte opcional del FHS como /mnt , pero que podría contener subdirectorios para tipos de medio específicos. Muchas distribuciones modernas utilizan subdirectorios /media como punto de montado para los discos extraíbles.          

***/dev:*** Linux trata la mayoría de los dispositivos de hardware como si fueran ficheros y el SO debe tener un lugar para estos en su sistema de ficheros. Ese lugar es el directorio /dev que contiene un gran número de ficheros que hacen de interfaces de hardware. Con los permisos apropiados se accede al hardware del dispositivo leyendo y escribiendo en el fichero de dispositivo asociado. El kernel permite que /dev sea un sistema de ficheros virtual creado automáticamente. El kernel y las herramientas de soporte crean sobre la marcha entradas en /dev para adaptarse a las necesidades de los drivers específicos. La mayoría de las distribuciones emplean este recurso.  

***/proc :*** Es un directorio inusual ya que no corresponde a un directorio o partición normal sino que se trata de un sistema de ficheros virtual que proporciona acceso a ciertos tipos de información del hardware dinámicamente. Esta información no se encuentra accesible a través de /dev.  

En la administración de Linux conocer la finalidad de los directorios resulta tremendamente útil ya que si instalamos por ejemplo un programa en una ubicación equivocada, un binario colocado en /bin c u ando debería estar en /usr/local/bin puede que se sobrescriba o elimine al realizar una actualización del sistema.  

Ref: https://es.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#Especificando_los_directorios_definidos_por_FHS  

Tras este estudio del sistema de ficheros a nivel software, a continuación vamos a ilustrar con un ejemplo gráfico cómo se distribuyen los discos y particiones dentro del sistema de ficheros. El ejemplo consta de un disco SATA que tiene 5 particiones, y cada una de ellas albergará un directorio (o punto de montaje) de la estructura de directorios visto anteriormente:  

![](https://openwebinars.net/media/django-summernote/2015-09-14/1aea0fc2-aa94-4377-af24-690b8ee7e383.png)

Como se puede apreciar en la imagen, cada partición del disco duro está asociado a un directorio de la estructura de directorios única del sistema operativo, a diferencia de windows que cada partición del disco duro se le asigna una letra de unidad (C:, D:, etc) y en ella se contiene su propia estructura de directorios.  

Esta forma de componer la estructura de directorios tiene una serie de ventajas en cuanto a la integridad y seguridad del sistema operativo que son:
  
* Soporte multi-operativo: Permite alojar varios sistemas operativos.    
* Elección del sistema de ficheros: Cada sistema de ficheros ofrece diferentes características eligiéndolas según las necesidades que se tengan para esa partición.    
* Control y administración del espacio en disco: Se puede controlar el acceso de los usuarios a las diferentes particiones.    
* Protección de errores en el disco: Al estar dividida la partición un error físico del disco probablemente afectará a una parte del sistema operativo, dejando la posibilidad de que se pueda seguir trabajando con él e intentar recuperar el sector dañado.    
* Seguridad: Puedes asegurar un sector de tu sistema de datos críticos montándolo en solo lectura. La ventaja de agregar esta característica a la partición y no a los ficheros es por cuestiones de redundancia.    
* Backup: Las herramientas de copias de seguridad trabajan mejor en sistemas pequeños y aislados de tareas de escritura.    

### Que es una shell  

El shell es el entorno que hace de intermediario entre el usuario y los recursos del ordenador, como si fuera un entorno de programación en tiempo real para ejecutar tareas. La shell aparece cuando nos logueamos en el sistema en modo consola, o bien cuando en el entorno gráfico abrimos una terminal.  
  
La shell se compone de un prompt, que es un texto inicial que normalmente nos ofrece información útil como el usuario que está utilizando la shell, el hostname de la máquina o incluso el directorio sobre el que estamos posicionados en cada momento, y el cursor que recibe las ordenes de teclado.
  
### Diferentes shells en Linux  
  
Existen multitud de shells diferentes para poder interactuar con nuestro sistema operativo, aunque la más conocida y habitual en la mayoría de distribuciones es la shell bash. Cada shell cuenta con sus propias características de uso, contando con atajos de teclado, visualización en vivo de ficheros, y atajos durante la navegación entre directorios. A continuación vamos a citar las shells mas famosas y una pequeña descripción de su procedencia:  

***bash*** (Bourne Again Shell): Se basa en los principios de shell Bourne de Unix pero se ha extendido en varios aspectos. Es la shell por defecto para la mayoria de las cuentas de usuario y es la que se tratará con más detalle en este curso.  
***bsh:*** El shell Bourne es la shell sobre la que está basada bash. Se conoce con el nombre de BSH. Su uso no es frecuente en Linux aunque el comando bsh suele ser un enlace simbólico a bash.  
***tcsh*** Este shell tcsh se basa en el anterior shell C (csh). Es una shell bastante popular en algunos círculos pero no hay distribuciones de Linux que lo traigan por defecto. Aunque es similar a bash en muchos aspectos difiere en algunos aspectos de operación. Por ejemplo, no se asignan variables de entorno de la misma manera que en bash.  
***csh:*** El original csh shell C no es muy utilizado en Linux pero si un usuario está familiarizado con csh, tcsh es un buen sustituto.  
***ksh:*** El shell Korn (ksh) fue diseñado cogiendo las mejores opciones de la shell Bourne y el C shell. Tiene un pequeño pero dedicado numero de seguidores.
***zsh:*** El shell zsh Z (zsh) es la evolución de la shell Korn e incorpora características de esta última además de agregar otras.  
 

