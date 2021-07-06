# Mis notas de comandos frecuentes

### Hardware

###### Ficheros dentro de proc

*  [Documentacion de Linux sobre el directorio /proc](http://tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html)    

**cat /proc/cpuinfo** // Muestra informacion sobre la cpu  
**cat /proc/meninfo** // Uso de memoria en el sistema  
**cat /proc/partitions** // Particiones del sistema  
**cat /proc/interrupts** // Tabla de interrupciones en el sistema   
**cat /proc/ioports** // Ubicacion de los diversos dispositivos en el banco de memoria  
**cat /proc/dma** // Direcciones de acceso directo a memoria  

###### Dispositivos PCI

  Hay dos tipos de dispositivos en el sistema,  **“cold plug”** y  **“hot plug”**, la diferencia es la forma en la que pueden ser conectados y desconectados en el sistema, “cold plug”, cuando el dipositivo esta apagado, por ejemplo CPU, memoria RAM, disco duro, en cambio “hot plug”, se pueden desconectar y conectar con el sistema operativo en funcionamiento.  

![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/1.png?raw=true)

**lspci** // Listado de los dispositivos PCI del sistema  
**man lspci** // Manual del comando lspci  
**lspci -t** // Lista en arbol de buses PCI  
**lspci -nn** // Nombre del fabricante y dispositivo con codigo numero del dispositivo PCI  
**setpci** // Permite configurar el dispositivo, (Es necesario conocer a bajo nivel el hardware que estamos consultando)  

 
###### Modulos del Kernel  

  En un sistema Linux los modulos del Kernel representan lo que seria los controladores o drivers del hardware que tenemos en el sistema. En /lib/modules Linux almacena los drivers de los diversos elementos Hardware que tenemos en el sistema.    
  
  **lsmod** // Muestra los modulos cargados actualmente en la memoria RAM  
  **cd /lib/modules/4.19.0-8-amd64/** // Serie de ficheros que dan informacion de los modulos  
  **netlink_diag.ko** // Ficheros .ko son drivers en Linux, por estandar se guardan en /lib/modules  
  **modinfo nombreModulo** // Ofrece informacion a nivel detallado del modulo, por ejemplo donde esta ubicado ese driver  
  **insmod** // Para cargar un modulo en el sistema con el fichero.ko dentro de /lib/modules/ 
  **insmod /lib/modules/4.4.0-64-generic/kernel/net/netlink/netlink_diag.ko** // Carga ese driver en la memoria RAM  
  **lsmod |grep netlink** // Filtrar por netlink para ver que ya esta cargado (Se podra ver que ocupa un espacio en memoria RAM)  
  **rmmod netlink_diag** // Se descargaria el modulo netlink_diag, comando original pensado para esto
  
  **modprobe** // La ventaja que tiene sobre insmod y rmmod, es que realiza una gestion inteligente a la hora de anadir o eliminar modulos en el sistema, si con insmod inteamos cargar un modulo que tiene una dependencia sobre otro modulo nos daria un error, en cambio este detecta que tiene una dependencia y la carga automaticamente para poder cargar ese modulo, al igual para descargar, detectara las depencias.  
  
  **modprove -v netlink_diag** // -v es el verbose que nos muestra que ejecuta por debajo al utilizar el comando (Ejecuta por debajo insmod)  
  **modprove -vr netlink_diag** // -vr descargariamos un modulo (Ejecuta por debajo insmod y rmmod)  
  
  ###### Gestion de dispositivos USB  (Bus Universal en Serie)  
  
  **lsusb** // Nos muestra los diferentes buses que tienen la placa madre y los diferentes dispositivos en ese bus  
  **lsusb -v** // Version mas depurada de la informacion  
  **lsusb -t** // Muestra la vista en forma de arbol  
  
  ###### Arranque del sistema
  
  ![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/2.png?raw=true)
  
  **runlevel** // Nos muestra dos valores: nivel de estado anterior y nivel de estado actual  
  **init 3** // Nos cambia al nivel de ejecucion 3  
  **telinit 3** // Nos cambia al nivel de ejecucion 3  
  **cd /etc/systemd/** // Directorios de configuracion systemd  
  **cd /etc/systemd/system** // Funcionalidades de systemd  
  
  **wall** // Muestra un mensaje a la consola de todos los usuarios  
  **shutdown opciones tiempo mensaje**// Apagar servidor  
  **shutdown -r +30 Voy reiniciar la maquina en 30 minutos** // Ejemplo de reiniciar el servidor  
  **shutdown -c** // Se cancela el apagado    
  
![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/5.png)  
![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/6.png)  
![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/7.png)  
![](https://github.com/leandrocosmetomassini/Linux/blob/master/Capetas/101/Capturas/8.png) 
   
  
  
  
  
  

