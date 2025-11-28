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


### Gestió de particions

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

Para hacer una segunda partición 
<img width="778" height="280" alt="image" src="https://github.com/user-attachments/assets/fff393d2-7858-48c9-a14e-309979352759" />


#### Comandes

Estas son las comandas de uso diario para interactuar con los ficheros y directorios dentro de un sistema de ficheros montado.

<img width="711" height="504" alt="Captura de pantalla de 2025-11-28 14-26-04" src="https://github.com/user-attachments/assets/172e0d22-8d59-4117-8f68-e5c7e1d7a7bd" />


## Gestió de processos
## Gestió d’usuaris i grups


## Còpies de seguretat i automatització de tasques
## Quotes d’usuaris

