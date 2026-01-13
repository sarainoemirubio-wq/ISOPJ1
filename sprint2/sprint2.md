---
layout: default
title: "Sprint 2: Instal·lació, Configuració de Programari de Base i Gestió de Fitxers "
Este se enfoca en entender y aplicar los conceptos esenciales de los Sistemas de Ficheros y la Gestión de Particiones, elementos cruciales para la organización y el rendimiento del almacenamiento en un sistema operativo.
---

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/3e40c2d5-00e8-423f-922e-4d252c7917c5" />


## Sistemes de fitxers i particions

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/0edf3341-bbf1-4f6e-a5d3-7f2b95ab0cc1" />


Un sistema de ficheros es la estructura que el sistema operativo utiliza para organizar los datos en un dispositivo de almacenamiento (por ejemplo: disco duro, SSD, USB, etc.). Las particiones son divisiones lógicas del disco físico, cada una de las cuales puede tener un sistema de ficheros diferente.

Comenzaremos por las Unidades de Almacenamiento Fundamentales:


### Mida sector
Es la unidad minima fisica de los discos on se guarden les dades i per defecte 512bytes no se pot cambiar.

Aquí hemos creado un nuevo archivo llamado hola y hemos escrito la cadena de texto "Bon dia" dentro de él para ver cuando puede ser su tamaño.
El tamaño exacto del contenido del archivo lo hemos visto con la comanda (du -b hola) y para cambiar su tamaño (du -sh hola ).
cat hola	Visualización	Muestra el contenido del archivo hola, confirmando que el texto es "Bon dia".

<img width="583" height="233" alt="image" src="https://github.com/user-attachments/assets/810f30f8-2203-4fdd-bdd6-78567157a082" />

Para obtener información detallada sobre el dispositivo de almacenamiento, incluyendo el tamaño de sus sectores, utilizaremos la herramienta ( sudo fdisk -l )

<img width="571" height="364" alt="image" src="https://github.com/user-attachments/assets/36453140-0d48-40bf-81c3-f685e961f1fa" />

Gràficament es veuria així:
<img width="3999" height="2283" alt="image" src="https://github.com/user-attachments/assets/2a137ecf-5e8b-452c-915e-4e13116ac23d" />

### Mida block
es la unidad minima logica on se guarden les dades a nivell de S.Operativo i per defecte 4096 i esta mida se pot cambiar cuan formatiem un disco

<img width="746" height="183" alt="image" src="https://github.com/user-attachments/assets/f90fb816-2efa-4224-88ad-81497da37146" />


Ahora iremos por LOS TIPUS DE FRAGMENTACIÓ: 

La fragmentación se refiere a cómo se distribuyen los datos en el disco y afecta el rendimiento.


### Fragmentació interna

Es produeix quan l’espai dins dels blocs d’emmagatzematge no s’aprofita completament, ja que els blocs són massa grans per a la informació que contenen.

Ejemplo: Si el tamaño del block es de 4 KB y guardas un archivo de 1 KB, se reservan 4 KB, y se desaprovechan 3 KB dentro de ese block.


### Fragmentació externa
Es produeix quan l’espai lliure al disc queda dispers en petits fragments separats, dificultant l’assignació de blocs contigus per a nous fitxers.

<img width="652" height="334" alt="image" src="https://github.com/user-attachments/assets/01253e02-24ef-4115-8dd4-9a9057dfff42" />

Aquí podemos comprobar para ver si desfragmentar

<img width="787" height="234" alt="image" src="https://github.com/user-attachments/assets/d8eb3bf6-e137-4f74-882c-450befdae2b0" />

Y en esta captura vemos como se desfragmentar


### Tipus de formateig

El formateo es el proceso de preparar un dispositivo de almacenamiento para un sistema de ficheros. Existen 3 tipos: 

<img width="711" height="504" alt="image" src="https://github.com/user-attachments/assets/7a2f1f82-7202-486b-a87a-0f0342f9abfe" />


#### Formateo de Bajo Nivel

Sus carácterísticas son que es un proceso de bajo nivel, ejecutado típicamente por el fabricante, que define la estructura física del disco (sectores, pistas).

Es el único que realmente elimina de forma irrecuperable los datos al reescribir la estructura física.

No se puede/debe hacer por el usuario en discos modernos (HDD/SSD), ya que puede dañar permanentemente el disco.

#### Formateo de Medio Nivel

Este es el menos común, sus características son refierentes a un proceso intermedio. En el contexto de los errores de sector, se asemeja a las funciones de diagnóstico que borran el sistema de ficheros y pueden marcar los sectores defectuosos (errores de sector) para que el sistema no guarde datos en ellos, pero no intenta repararlos físicamente.

#### Formateo de Alto Nivel

Es el formato que se realiza habitualmente (por ejemplo, en un USB).

Crea la estructura del sistema de ficheros (tabla de asignación de archivos, directorios raíz) en la partición.

Normalmente, solo borra los contenidos de los ficheros (los "oculta") al reescribir la tabla de contenidos, pero los datos son recuperables hasta que son sobrescritos.

<img width="828" height="291" alt="image" src="https://github.com/user-attachments/assets/88bfa03d-81c1-4712-ab3b-3d9c4fa5cc3c" />


A quí podemos se ha completado la preparación lógica de la primera partición (/dev/sdb1) que vemos la aprtición más adelante. Se le ha aplicado un Formateo de Alto Nivel para crear un sistema de ficheros Ext4, especificando un tamaño de bloque de 2 KB.

### Gestió de particions

<img width="687" height="630" alt="image" src="https://github.com/user-attachments/assets/b74e68f2-9a71-4b9a-a28a-69ff104ce349" />


La gestión de particiones es el proceso de crear, modificar, eliminar y formatear las divisiones del disco.

#### GPARTED

GParted es una de las herramientas gráficas más populares para la gestión de particiones en entornos Linux.

Permite visualizar gráficamente las particiones de todos los discos conectados.

Facilita la creación, eliminación, redimensión y copia de particiones de manera segura y visual.

Soporta una gran variedad de sistemas de ficheros (ext4, NTFS, FAT32, etc.).

En este no se puede cambiar la medida

<img width="769" height="337" alt="image" src="https://github.com/user-attachments/assets/7f45a276-8a86-42c8-97d5-8bd90267bcf7" />


Aquí estamos en el proceso de inicializar y particionar un disco duro nuevo (/dev/sdb). Específicamente, ha creado la primera partición primaria (/dev/sdb1) y le ha asignado un tamaño de 12.4 GB.

<img width="813" height="420" alt="image" src="https://github.com/user-attachments/assets/6e50166a-73d2-4b7f-bdb9-09e44e21859e" />

Luego de esto guardamis los cambios (w) y luego formatear la nueva partición usando mkfs para poder montarla y usarla.

Para hacer una segunda partición hemos continuado el proceso y creado una segunda partición primaria (/dev/sdb2) en el mismo disco (/dev/sdb). Esta segunda partición ocupa el resto del espacio disponible en el disco y tiene un tamaño de 12.6 GB

<img width="778" height="280" alt="image" src="https://github.com/user-attachments/assets/fff393d2-7858-48c9-a14e-309979352759" />

He aquí vemos el resultado de las dos particiones

<img width="582" height="226" alt="image" src="https://github.com/user-attachments/assets/b7d88357-84f1-4e50-9e8b-237dd1e526cb" />


Ahora veremos como se ve lo que hemos hecho pero en GPARTED

<img width="785" height="262" alt="image" src="https://github.com/user-attachments/assets/18dce9e9-87b9-4dcb-b386-bbc33543872f" />


GParted confirma que las dos particiones (/dev/sdb1 y /dev/sdb2) se crearon correctamente en términos de tamaño y ubicación. Sin embargo, muestra un problema o desactualización al no reconocer el Sistema de Ficheros en ninguna de las dos (incluso en la que ya fue formateada), lo cual se indica con la etiqueta desconegut y el símbolo de advertencia.


<img width="707" height="215" alt="image" src="https://github.com/user-attachments/assets/c8d93f73-15b7-4ad2-b12b-c831071d6ef9" />

aquí muestro la edición del archivo de configuración fundamental de Linux, /etc/fstab, para asegurar que la partición montada siga accesible después de cada reinicio.

<img width="478" height="111" alt="image" src="https://github.com/user-attachments/assets/6e60849b-255e-4c39-bd25-552ff5ab81db" />


Esta imagen nos dice que el montaje es exitoso, la partición /dev/sdb1 ahora está montada y accesible en /mnt/particio1/.

El archivo adeu que se creó antes del montaje ha desaparecido del listado porque ha sido "ocultado" por el contenido de la partición /dev/sdb1. Si el usuario desmontara la partición (umount /mnt/particio1/), el archivo adeu volvería a aparecer.

La partición /dev/sdb1 está ahora totalmente operativa para guardar datos del sistema.


<img width="731" height="282" alt="image" src="https://github.com/user-attachments/assets/8ac90bf7-8d21-461c-9aca-3a9f271d968b" />

aquí vemos cómo el usuario prueba que tiene permisos de escritura y que el sistema de ficheros está funcionando correctamente en la partición recién montada.


<img width="434" height="68" alt="image" src="https://github.com/user-attachments/assets/58558e1f-ce21-4a02-bb11-cec6ccf6714d" />


y este es el resultado final

#### Comandes

Estas son las comandas de uso diario para interactuar con los ficheros y directorios dentro de un sistema de ficheros montado.

<img width="711" height="504" alt="Captura de pantalla de 2025-11-28 14-26-04" src="https://github.com/user-attachments/assets/172e0d22-8d59-4117-8f68-e5c7e1d7a7bd" />


## Gestió de processos


<img width="710" height="709" alt="image" src="https://github.com/user-attachments/assets/fe30be21-bd3a-4838-9fd8-1d517b38c0fb" />


Un Gestor de procesos es una herramienta fundamental del sistema operativo. Su función principal es monitorear y controlar la actividad de los programas y servicios que se están ejecutando en el equipo en un momento dado. Este piensa en un programa como un archivo inactivo guardado en el disco duro (por ejemplo, el archivo de Word). Cuando haces doble clic en ese archivo para abrirlo y empieza a funcionar, se convierte en un proceso vivo.

El objectiu de las comandas en los processos es identificar el gdip

<img width="745" height="660" alt="image" src="https://github.com/user-attachments/assets/33dcc109-745b-46af-9234-39eb097d2866" />

El comando pstree es la forma en que un usuario puede visualizar la información que el Gestor de Procesos está manteniendo.

Esta imagen muestra que cada proceso tiene un proceso "padre" que lo inició (por ejemplo, systemd es el proceso padre de casi todos los demás). Esta jerarquía es fundamental en la gestión de procesos, ya que:

Muestra cómo se inicia la actividad en el sistema (generalmente a partir de systemd, que es el primer proceso al arrancar).

Cuando un proceso padre muere, el sistema operativo (a través del Gestor de Procesos) debe decidir qué hacer con sus procesos hijos.


<img width="777" height="862" alt="image" src="https://github.com/user-attachments/assets/01c7d9bf-c76f-4ee9-8922-1c4c5b97e36d" />


El proceso que he realizado aquí es la ejecución del comando de Linux pstree -p -h mirela.

Este comando es una variante más detallada del anterior pstree. Se utiliza para mostrar los procesos activos en el sistema en una estructura de árbol, pero con opciones adicionales:

-p: Muestra el ID de Proceso (PID) junto al nombre de cada programa. Por ejemplo, systemd(1807) significa que el proceso systemd tiene el PID 1807.

-h: Resalta el proceso actual y su ascendencia (no visible directamente en la imagen, pero es la función del comando).

mirela: Filtra la salida para mostrar solo los procesos que pertenecen al usuario "mirela".

<img width="701" height="459" alt="image" src="https://github.com/user-attachments/assets/1b44e1f2-5a73-4404-aec6-81a52e86f708" />


identificador de processos en el contenido (-h):  identificar processos per al usuari
en la misma comanda vemos la terminar ( en este caso de mireia porque es el usuari)

También podemos despues de esta comanda ponerle un | grep gnome-terminal
Al combinar ambos (pstree -p -h mirela | grep gnome-terminal):

El comando pstree genera cientos de líneas que describen el estado de todos los procesos de tu sesión.

La tubería envía todas esas líneas a grep.

grep lee esas líneas y solo muestra aquellas líneas que contienen la cadena de texto gnome-terminal.


kill: señar
-9: señal per a matar

<img width="894" height="784" alt="image" src="https://github.com/user-attachments/assets/48592d52-01fe-4d96-b1cd-b9a05fd6c748" />


ps aux: es una de las herramientas más potentes en Linux para monitorizar el sistema.

Detectar programas bloqueados: Si un programa no responde, usas ps aux para buscar su PID y luego lo cierras a la fuerza.




<img width="901" height="230" alt="image" src="https://github.com/user-attachments/assets/ede37675-2581-496c-b5c2-0272589d3961" />



Aquí estamos comprobando quién está conectado, qué programas están abiertos y cómo controlar el acceso a través de las contraseñas. Es el flujo típico de un administrador que busca un error o un proceso "colgado" para cerrarlo.



<img width="902" height="146" alt="image" src="https://github.com/user-attachments/assets/c78b95e2-40b9-4027-8f0a-ba4c21aed50d" />


btop es un monitor de recursos del sistema basado en terminal (TUI) que permite visualizar en tiempo real el rendimiento del hardware y la actividad de los procesos.


<img width="893" height="871" alt="image" src="https://github.com/user-attachments/assets/f1a27f57-f534-43e1-acc7-04d7460afa8f" />


Aquí utilizamos una consola de alto rendimiento (btop) para ver qué impacto tienen esos procesos en la RAM, el disco y el procesador del equipo.



<img width="769" height="582" alt="image" src="https://github.com/user-attachments/assets/62318e0d-14db-4b9d-a230-19f8b2cb94e1" />



top actualiza la información cada pocos segundos, permitiéndote ver qué procesos están consumiendo más recursos en este instante.


<img width="924" height="791" alt="image" src="https://github.com/user-attachments/assets/3747440f-766f-477f-85cb-353b8d229c33" />


el numero negatiu de nite, si lo aumentamos disminuimos la prioridad



<img width="917" height="91" alt="image" src="https://github.com/user-attachments/assets/4b94bb79-b16c-4c11-a8f0-4ff484d4897d" />


cambia la prioridad e un procés que se esta executant


## Gestió d’usuaris i grups

Es la parte del sistema operativo encargada de administrar las identidades. Básicamente, define quién eres (Usuario) y a qué colectivo perteneces (Grupo) para determinar qué acciones tienes permitido realizar.

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/469bb666-3fcc-4af3-b4d4-46f86784d688" />


Linux es un sistema operativo multiusuario. Esto significa que puede ser utilizado por múltiples personas al mismo tiempo, cada una con su propia cuenta y sus propios permisos.

El Grupo Principal (Primary Group) es el grupo al que pertenece un usuario por defecto y el más importante en términos de permisos de acceso.

Cuando un usuario crea un nuevo archivo o directorio, el grupo asignado a ese nuevo elemento será, automáticamente, su grupo principal.

¿Cómo se crea? (Modelo User Private Group - UPG)
En la mayoría de las distribuciones modernas de Linux (como Red Hat, Fedora, Ubuntu, etc.), se utiliza un modelo llamado User Private Group (UPG).



<img width="693" height="550" alt="image" src="https://github.com/user-attachments/assets/1c03b903-b60a-4b9a-9db6-ecb10a0acfe5" />

<img width="702" height="409" alt="image" src="https://github.com/user-attachments/assets/b1132751-935c-4286-a5d5-b65ce3f8bfad" />


Aquí vemos las comandas que necessitamos


<img width="937" height="680" alt="image" src="https://github.com/user-attachments/assets/26dced85-5fdc-411c-9e3e-1bd5d48156a2" />

Aquí observamos UID 0 y GID 0 (el grupo root), su directorio de inicio es /root y su shell es /bin/bash (el shell predeterminado para comandos).

La mayoría de las entradas (como daemon, bin, lp, news) tienen un UID bajo y su shell está establecido a /usr/sbin/nologin. Esto confirma que son cuentas del sistema que no pueden ser utilizadas para iniciar sesión.

También podemos ver la cuenta nobody con UID 65534. Es una cuenta especial con muy pocos privilegios, utilizada por el sistema para ejecutar programas que necesitan acceso limitado al sistema.


<img width="349" height="680" alt="image" src="https://github.com/user-attachments/assets/9aadd493-596b-40b7-806e-21f8ffbb31a9" />


Aquí muestra el contenido del archivo /etc/shadow: Pueden cambiar la contraseña inmediatamente (0).

La contraseña nunca expira (99999). El aviso de expiración es 7 días antes (aunque nunca expira, es el valor por defecto).

La cuenta no tiene políticas de inactividad o caducidad total.


<img width="604" height="675" alt="image" src="https://github.com/user-attachments/assets/e1ec2182-9620-4c28-8ed4-dfb61609cea4" />


Ahora estamos viendo el tercer archivo clave para la gestión de usuarios y grupos: /etc/group.

Este archivo define todos los grupos que existen en el sistema y qué usuarios pertenecen a cada grupo como miembros suplementarios (secundarios).

<img width="604" height="675" alt="image" src="https://github.com/user-attachments/assets/f81e9905-0e48-4425-9db7-900b3c104942" />


La comanda /etc/gshadow, es el espejo seguro del archivo /etc/group. Este es fundamentalmente un archivo de seguridad que garantiza que las contraseñas de grupo estén protegidas (aunque rara vez se usen) y que el sistema sepa qué usuarios pueden administrar las membresías de los grupos sin necesidad de ser el usuario root.


<img width="603" height="406" alt="image" src="https://github.com/user-attachments/assets/a61c3895-8ed0-47e4-943d-65ccbfdcd0c1" />

Aquí podemos ver la creación de un usuario nuevo-


<img width="772" height="578" alt="image" src="https://github.com/user-attachments/assets/13ab937e-c14c-4189-a693-e0ab40cc35dd" />

<img width="607" height="553" alt="image" src="https://github.com/user-attachments/assets/6be4eda7-3e5b-41e0-a34c-721b1b1eab56" />

Estos son dos ejemplos de cración de usuarios

<img width="918" height="134" alt="image" src="https://github.com/user-attachments/assets/dfb0d64f-8675-4780-a589-5d19e7546be9" />


Aquí si nosotros queremos bloquear a un usuario sería como la imagen que está arriba con la comanda: usermod -L (nombre del usuario que quiere bloquear) y después el cat/etc/shadow | grep (y otra vez ponemos el nombre del usuario que queremos bloquear. 


<img width="889" height="85" alt="image" src="https://github.com/user-attachments/assets/b7e5c206-4359-4a06-974c-a07750aa8fab" />


Y aquí tenemos el ejemplo para poderlo desbloquear, ponemos casi las mismas comandas que utilizamos al bloquear el usuario   pero esta vez envéz de -L ponemos -U.


El Ciclo de Vida de una Cuenta
No basta con crear un usuario; hay que gestionarlo a lo largo del tiempo. Aquí es donde entra la seguridad preventiva.

El comando chage 


<img width="725" height="424" alt="image" src="https://github.com/user-attachments/assets/6f62decf-5e59-4e4e-8975-4402ef3b43a0" />



Como vemos en la imagen, este comando sirve para administrar cuándo caduca una contraseña o una cuenta entera. Es vital en empresas para obligar a los empleados a cambiar su clave periódicamente.


Comprobación:

<img width="793" height="169" alt="image" src="https://github.com/user-attachments/assets/028fd681-37aa-4975-ae08-1ad68a62524e" />


ls /var/m

Opciones clave:

-l (list): La más usada. Te muestra el estado actual (cuándo cambió la clave por última vez, cuándo caduca, etc.).

-M (maxdays): Define cada cuántos días es obligatorio cambiar la contraseña (ej. cada 90 días).

-E (expiredate): Pone una fecha de "muerte" a la cuenta. Útil para becarios o trabajadores temporales.

-W (warndays): Define cuántos días antes de que caduque la clave el sistema empezará a avisar al usuario.

Deficnició=


<img width="687" height="503" alt="image" src="https://github.com/user-attachments/assets/28f14abc-49c4-4b3a-a44c-cec3b41ba433" />



.bash logout: Es un script oculto (por eso empieza con un punto) que se encuentra en el directorio personal del usuario (/home/usuario).

Se ejecuta automáticamente cada vez que un usuario cierra la sesión de un terminal de inicio (login shell).

Se utiliza principalmente para realizar tareas de limpieza.

Ejemplos: Borrar archivos temporales creados durante la sesión, limpiar la pantalla del terminal por seguridad o registrar la hora de desconexión en un archivo de log.



.bashrc: Es probablemente el archivo de configuración más importante para el usuario en el día a día. También es un archivo oculto en el home.

Se ejecuta cada vez que abres una nueva terminal o ejecutas un terminal interactivo que no es de inicio de sesión.

Define el entorno de trabajo del usuario.

   Aliases: Crear atajos de comandos (ej: que ll ejecute ls -la).

   Variables de entorno: Configurar rutas personalizadas.

   Personalización: Cambiar los colores y la apariencia del "prompt" (el texto que sale antes de escribir un comando).

   

.connexio_ssh: SSH (Secure Shell) es un protocolo que permite acceder y controlar un ordenador de forma remota a través de una red.

Permite gestionar un servidor que está en otra ubicación (o una máquina virtual) como si estuvieras sentado físicamente delante de él.

Características clave:

   Seguridad: Toda la información (incluyendo tu contraseña) viaja encriptada, a diferencia de protocolos antiguos como Telnet.

   Puerto por defecto: Utiliza normalmente el puerto 22.

   Sintaxis básica: ```bash ssh usuario@direccion_ip_del_servidor




Los permisos para los archivos y verlos en ls -l


<img width="699" height="239" alt="image" src="https://github.com/user-attachments/assets/51a7194c-1899-4681-8f4e-c20d19474666" />

Si quiero modificar el UMASK elpuc fer de nano /etc/login.defs


<img width="699" height="239" alt="image" src="https://github.com/user-attachments/assets/7ca7e8f1-1a7a-4adc-a7c8-796c4150db31" />


aquí cambiaria el UMASK solo para este usuario


<img width="528" height="55" alt="image" src="https://github.com/user-attachments/assets/a8d5a969-aee8-421d-bcf2-a673394f8a22" />

Aquí salimos del root para cambiar la mascara temporalmente.


<img width="633" height="325" alt="image" src="https://github.com/user-attachments/assets/4647782c-37ab-4a44-b3e4-a17e8f38b7f3" />


El Sistema de Permisos

Todo el sentido de tener usuarios y grupos reside en los permisos. En sistemas tipo Linux, cada archivo o carpeta tiene tres niveles de permisos:


<img width="531" height="188" alt="image" src="https://github.com/user-attachments/assets/a56db70a-3357-4d73-8fda-24c1795828b0" />

Los permisos suelen ser: R (Lectura/Read), W (Escritura/Write) y X (Ejecución/Execute).


aquí podemos ver como cambiar algunos permisos


<img width="665" height="268" alt="image" src="https://github.com/user-attachments/assets/4782e85a-6467-4b95-9183-062e426db411" />

Aquí lo podemos cambiar definitivamente, s+osea que si apagamos la computadora las modificaciones se guarden

<img width="726" height="439" alt="image" src="https://github.com/user-attachments/assets/e3916c24-6c31-4eab-a034-4dcd7d6668a6" />

Este sería el resultado de los cambios

<img width="557" height="225" alt="image" src="https://github.com/user-attachments/assets/36606269-6ed6-450e-b504-1d34df54863a" />


En mkdir creamos una carperta llamada numeros

setfacl -m user: segon--- numeros

si quiero llevar todas las accesiones que he puesto hago: setfacl -b numeros

setfacl (establir)

getfacl (mirar)     


## Còpies de seguretat i automatització de tasques

1. Còpies de Seguretat (Backups)
    Una còpia de seguretat és una duplicació de dades en un suport diferent a l'original per poder recuperar-les en cas de pèrdua, robatori o fallida del sistema.

<img width="804" height="222" alt="image" src="https://github.com/user-attachments/assets/b66f73b8-d8b7-4407-89db-5c1ecbc57be9" />

Para tener una mejor referencia de cuantas copias tengo que hacer:

La Regla d'Or: El Mètode 3-2-1
Aquest és l'estàndard de la indústria per evitar perdre informació:

3 còpies de les teves dades: L'original i dues còpies.

2 suports diferents: Per exemple, un disc dur extern i el núvol.

1 còpia fora de lloc: Una de les còpies ha d'estar físicament en un lloc diferent (un altre edifici o un servidor remot).

Què necessites per a la restauració?
1. Còpia Completa (Full Backup)
És la més senzilla de totes, però la que més espai ocupa.

Què necessites: Només el fitxer (o suport) de l'última còpia completa realitzada.

Com es fa: Simplement selecciones el fitxer de seguretat i el restaures. No depèn de cap altre fitxer anterior ni posterior.

Temps de recuperació: Molt ràpid, ja que només has de bolcar les dades un cop.

2. Còpia Incremental
És la més complexa de restaurar perquè depèn d'una "cadena" de fitxers.

Què necessites: 1. L'última còpia completa. 2. Tots i cadascun dels fitxers incrementals creats des d'aquella còpia completa fins al moment de la pèrdua.

Com es fa: Primer es restaura la còpia completa, i després el programari va aplicant els canvis de la còpia 1, després de la 2, de la 3... així successivament.

Risc: Si un dels fitxers de la cadena està danyat o es perd, no podràs recuperar el que hi havia a partir d'aquell punt.

3. Còpia Diferencial
És un punt mitjà entre les dues anteriors.

Què necessites:

L'última còpia completa.

Només l'última còpia diferencial realitzada.

Com es fa: Primer es restaura la completa i després s'aplica l'últim fitxer diferencial (que ja conté tots els canvis acumulats des de la completa).

Temps de recuperació: Més ràpid que l'incremental, ja que només s'han de processar dos fitxers.


2. Teoria comandes Backups
Hay muchos programas però en linux se neccesitan estas comandas:

	1. cp : es una copia simpkle no inteligente, només transfiera localmente, no optimitza(copiar y pegar) 
	2. rsync : es una eina inteligente que només copia els fitxer modificats y la sincronizacion puede ser local o en remot via ssh
	3. dd: no es propiamente una copia de seguretat, es una eina para recuperar discos o particion y no es inteligente, copia todos los sectores
3. Pràctica comandes Backups

crear dos discos de 1gb

<img width="851" height="639" alt="image" src="https://github.com/user-attachments/assets/9aaf4b72-bcc6-4080-b810-feb253393f8f" />

asi se ve:

<img width="739" height="442" alt="image" src="https://github.com/user-attachments/assets/f08c3000-52b6-4443-b70f-3682175b0664" />

1. cp
2. rsync
3. dd (clona discos o particions)creo un fixer clonacio en sdc1 y luego
4. 
<img width="854" height="843" alt="image" src="https://github.com/user-attachments/assets/085066fa-1591-45a4-9e65-79702b179b85" />

4. Pràctica programes Backups (ya lo haremso norotros)

	1. Deja-Dup
      És conegut a moltes distribucions simplement com "Còpies de seguretat". És ideal per a usuaris que volen una solució de "configurar i oblidar".

Passos per a la pràctica:
Instal·lació: Obre el terminal i instal·la'l (si no el tens ja): sudo apt install deja-dup

Configuració:

Busca l'aplicació "Còpies de seguretat" al teu menú d'inici.

Carpetes a desar: Tria una carpeta de prova (per exemple, Documents/Projecte).

Carpetes a ignorar: Pots deixar-ho per defecte (normalment la Papelera i Baixades).

Ubicació de l'emmagatzematge: Tria on vols la còpia (un disc dur extern, una carpeta local diferent o el núvol com Google Drive).

Execució i Automatització:

Fes clic a "Crea una còpia de seguretat ara" per a la primera vegada.

Activa l'interruptor de "Còpia de seguretat automàtica" i tria la freqüència (diària o setmanal).

Restauració:

Prem el botó "Restaura" i veuràs com pots triar la data de la còpia que vols recuperar.

  2. Duplicity
    Duplicity utilitza el mètode incremental, encripta les dades amb GPG i és extremadament potent per a servidors.

  Passos per a la pràctica:
  Instal·lació: sudo apt install duplicity

  Fer la primera còpia de seguretat: Imagina que vols copiar la carpeta /home/usuari/dades a una carpeta de backup /home/usuari/backup_dir.

  queda així: duplicity /home/usuari/dades file:///home/usuari/backup_dir

  (Et demanarà una contrasenya per encriptar la còpia. No l'oblidis!)

  3. Llistar els fitxers de la còpia: Per veure què hi ha dins del backup sense restaurar-lo:

  queda així: duplicity list-current-files file:///home/usuari/backup_dir

  4. Restaurar les dades: Per recuperar els fitxers en una carpeta nova anomenada recuperat:

      queda així: duplicity file:///home/usuari/backup_dir /home/usuari/recuperat

  5. Teoria Automatització scripts, cron i anacron
teoria: 

  6  . Pràctica automatització
  son dos eines de automatitzacio que ocupen tasques periodiques
	1. cron . Executa tasques programades en una data i hora especifiques, si el sistema 	esta apagado la tasca es perd, es ideal per a tasques en dates i hores concretes, i per 	accions especifiques de un usuari.

Archius o direcctoris importants:

<img width="1058" height="476" alt="image" src="https://github.com/user-attachments/assets/0cea7641-ed66-4362-b7e0-52ae3932ca21" />

todo lo de aquí afecta todos los uduaris


para una especifica: 

<img width="1058" height="476" alt="image" src="https://github.com/user-attachments/assets/9b747b73-229a-46fc-9bc4-e2f4cf2bf266" />


<img width="721" height="118" alt="image" src="https://github.com/user-attachments/assets/f72d0caf-b3e0-4cf4-9171-69ca934eb026" />



permisos:
<img width="922" height="550" alt="image" src="https://github.com/user-attachments/assets/23b35e23-c296-44fa-870f-f1ff78d169a4" />


<img width="922" height="550" alt="image" src="https://github.com/user-attachments/assets/475d8609-ba4e-486c-b75b-96fcc9e1da82" />

he cambiado el 35



2. anacron . Es ideal per a executar tasques periodiques on no cal una data i una hora 	especific, normalment s’utilitza per a tasques de manteniments de sistemes i no requireix 	que el sistema estigue obert perquè quan s’obrigue ja es executara, no es com una tasca així 	com el cron (general, guarda tasques)


el 1 al lado del 1 es el temps que tarda en fer un replace:


<img width="1126" height="567" alt="image" src="https://github.com/user-attachments/assets/681d2335-70df-4bf7-8449-2bf6fb6f8d18" />


<img width="785" height="187" alt="image" src="https://github.com/user-attachments/assets/b79baaa4-a7c5-4df5-a16f-dd40fc823a5f" />


Aquí he programado el tiempo que quiere que se ejecute y he intentado mover el script a /etc/cron.daily/, que es donde el sistema busca scripts para ejecutar una vez al día de forma automática.

En el comando cp copies.sh /etc/cron.daily/copies, intendo renombrar el archivo a copies dentro de ese directorio.



<img width="558" height="45" alt="image" src="https://github.com/user-attachments/assets/19a92a8e-d1f2-432d-a20b-3a3730987a2c" />

quota: se utiliza para visualizar el uso de disco y los límites de espacio asignados a un usuario o a un grupo.


<img width="789" height="312" alt="image" src="https://github.com/user-attachments/assets/8c278d38-322a-49ac-b29d-41b4cdd9bc91" />


Aquí montamos automáticamente las particiones del disco al arrancar el sistema.



<img width="903" height="489" alt="image" src="https://github.com/user-attachments/assets/ac94d294-90e8-44dc-8593-5bbab6daca4d" />


En esta segunda imagen se observa un intento de activar las cuotas de disco que configuraste en el archivo /etc/fstab



<img width="1046" height="684" alt="image" src="https://github.com/user-attachments/assets/630355a0-5136-4813-988a-b47885269530" />



<img width="903" height="489" alt="image" src="https://github.com/user-attachments/assets/bff7e463-20b6-4e83-a0af-b4a3c80ad0e6" />


he fet apartir de adduser gina


<img width="564" height="80" alt="image" src="https://github.com/user-attachments/assets/c8fd45a0-0de8-4674-8813-93252397f4ac" />


aquí comprobo en ls que mire si he fet esta comanda


<img width="694" height="27" alt="image" src="https://github.com/user-attachments/assets/3b3d252e-ff61-4184-aebc-be9e5ef29e7c" />


dentro del sudo su de gina si ponemos esta comanda comprovaremos lo que el almacenamiento de la misma

repquota /dev/sdc1 veremos los periodes de gracia y ahí si lo podemos programar


<img width="493" height="25" alt="image" src="https://github.com/user-attachments/assets/4f6b7663-9ff3-45ea-9d4f-3aa57e3df874" />



<img width="746" height="275" alt="image" src="https://github.com/user-attachments/assets/cab9f0c6-b55b-49dd-a318-3cdd01c7f0c9" />


Tienes la configuración escrita en el archivo, pero el servicio de cuotas no está operativo porque falta montar la partición (mount /mnt/dades) e inicializar los archivos de control.


<img width="1033" height="511" alt="image" src="https://github.com/user-attachments/assets/f685f964-dc2a-4718-96a5-e52957dfee75" />


     
     
## Quotes d’usuaris

