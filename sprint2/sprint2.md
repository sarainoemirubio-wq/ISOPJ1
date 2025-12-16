---
layout: default
title: "Sprint 2: Instal·lació, Configuració de Programari de Base i Gestió de Fitxers "
Este se enfoca en entender y aplicar los conceptos esenciales de los Sistemas de Ficheros y la Gestión de Particiones, elementos cruciales para la organización y el rendimiento del almacenamiento en un sistema operativo.
---

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/3e40c2d5-00e8-423f-922e-4d252c7917c5" />


## Sistemes de fitxers i particions
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

## Gestió d’usuaris i grups

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


Los permisos para los archivos y verlos en ls -l


<img width="699" height="239" alt="image" src="https://github.com/user-attachments/assets/51a7194c-1899-4681-8f4e-c20d19474666" />

Si quiero modificar el UMASK elpuc fer de nano /etc/login.defs


<img width="699" height="239" alt="image" src="https://github.com/user-attachments/assets/7ca7e8f1-1a7a-4adc-a7c8-796c4150db31" />


aquí cambiaria el UMASK solo para este usuario


<img width="528" height="55" alt="image" src="https://github.com/user-attachments/assets/a8d5a969-aee8-421d-bcf2-a673394f8a22" />

Aquí salimos del root para cambiar la mascara temporalmente.


<img width="633" height="325" alt="image" src="https://github.com/user-attachments/assets/4647782c-37ab-4a44-b3e4-a17e8f38b7f3" />


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
## Quotes d’usuaris

