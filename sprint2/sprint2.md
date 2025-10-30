---
layout: default
title: "Sprint 2: Instal·lació, Configuració de Programari de Base i Gestió de Fitxers "
---
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/3e40c2d5-00e8-423f-922e-4d252c7917c5" />


## Sistemes de fitxers i particions
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

### Fragmentació interna

Es produeix quan l’espai dins dels blocs d’emmagatzematge no s’aprofita completament, ja que els blocs són massa grans per a la informació que contenen.


### Fragmentació externa
Es produeix quan l’espai lliure al disc queda dispers en petits fragments separats, dificultant l’assignació de blocs contigus per a nous fitxers.
<img width="652" height="334" alt="image" src="https://github.com/user-attachments/assets/01253e02-24ef-4115-8dd4-9a9057dfff42" />
<img width="787" height="234" alt="image" src="https://github.com/user-attachments/assets/d8eb3bf6-e137-4f74-882c-450befdae2b0" />

### Tipus de formateig

### Gestió de particions

#### GPARTED
#### Comandes


## Gestió de processos
## Gestió d’usuaris i grups
## Còpies de seguretat i automatització de tasques
## Quotes d’usuaris

