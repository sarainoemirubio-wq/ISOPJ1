## Administració de Dominis i Seguretat

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/165783ed-76b1-4f2b-aeb8-a46cdf4c94dc" />


### Configurar i gestionar dominis, assegurant un correcte accés i explotació de recursos de xarxa.

<img width="3200" height="3000" alt="image" src="https://github.com/user-attachments/assets/b30ab4a1-066c-43d4-94dd-d765372d2f22" />

Para poder gestionar y configurar los dominios tenemos que tener algunos conceptos claros antes de hacer la práctica:

#### El Controlador de Domini (DC): El servidor "cap" que guarda la base de dades de tots els usuaris i màquines.

#### DNS (El cor de tot): Sense un servei de noms perfecte, el domini caurà. El domini necessita saber que servidor01 és la IP 192.168.1.10.

#### Recursos de Xarxa: Carpetes compartides, impressores i aplicacions que només els usuaris autoritzats podran veure.

#### Explotació de recursos: Es tracta d'optimitzar qui fa servir què, evitant que la xarxa se saturi o que hi hagi buits de seguretat.

Para la configuración :

#### Promoció del Servidor: Instal·lar els rols necessaris per convertir un servidor base en un "Administrador" de la xarxa.

#### Unió de Clients: Configurar les estacions de treball perquè "escoltin" al controlador de domini.

#### Estructura Organitzativa (OU): Crear "carpetes" dins del domini per separar departaments (Vendes, IT, RRHH).



### Configurar l'accés a recursos locals i remots, garantint la connectivitat i seguretat adequades.



<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/9f35bab0-b94d-47a6-9b39-c1e346a0b69c" />



#### Recursos Locals: 
Són els que resideixen físicament en la mateixa màquina o servidor on l'usuari està treballant.

Gestió: Es basa en sistemes de fitxers (NTFS en Windows, ext4/XFS en Linux).

Seguretat: Es controla mitjançant permisos d'usuari directes sobre el maquinari (discos, impressores connectades per USB).


#### Recursos Remots
Són recursos que estan en un altre servidor o al núvol (NAS, servidors de fitxers, bases de dades).

Protocols de connectivitat: * SMB/CIFS: Per a carpetes compartides en Windows.

NFS: Molt comú en entorns Linux.

SSH/SFTP: Per a transferència segura de fitxers i execució remota.

Seguretat: Requereix autenticació (qui ets) i autorització (què pots fer).

#### El binomi: Connectivitat + Seguretat
Perquè la configuració sigui correcta, has de complir tres condicions:

Visibilitat: Que el recurs sigui accessible a través de la xarxa (ports oberts com el 445 per a SMB o el 22 per a SSH).

Permisos de Compartició: Qui pot "trucar a la porta" del recurs des de la xarxa.

Permisos de Sistema (ACL): Una vegada dins, què pot fer l'usuari amb el fitxer (llegir, escriure, executar).





### Assignar i gestionar drets d'usuari i directives de seguretat per protegir els recursos i el sistema.


És vital aquests dos conceptes:

Permisos: S'apliquen a objectes (fitxers, carpetes, impressores). Ex: "Pots llegir aquest document".

Drets d'usuari: S'apliquen al sistema. Ex: "Pots canviar l'hora del servidor", "Pots apagar el sistema" o "Pots iniciar sessió remotament".



#### Directives de Seguretat
Són les regles del joc. Serveixen per automatitzar la seguretat en tot el sistema:

Complexitat de contrasenyes: Obligar a fer servir majúscules, números i símbols.

Bloqueig de compte: Si algú s'equivoca 3 cops, el compte es bloqueja.

Restriccions de programari: Impedir que els usuaris instal·lin aplicacions no autoritzades.




### Implementar i gestionar servidors de fitxers, servidors d'impressió i servidors d'aplicacions per cobrir les necessitats de l'entorn.


#### Tipus de Servidors i la seva funció:
Servidors de Fitxers (File Servers)
És el magatzem central. La seva feina és guardar les dades de manera estructurada i segura.

Quota de disc: Limitar quant espai pot fer servir cada usuari.

Auditoria: Saber qui ha esborrat o modificat un fitxer.

Servidors d'Impressió (Print Servers)
En lloc de connectar cada ordinador a cada impressora, el servidor gestiona les cues d'impressió.

Centralització: Instal·les el controlador (driver) una vegada al servidor i el reparteixes a tothom.

Gestió: Pots cancel·lar treballs encallats o prioritzar la impressió del director.

Servidors d'Aplicacions (App Servers)
Executen programari específic (ERP, bases de dades, eines de gestió) al qual els usuaris accedeixen des dels seus clients.

Recursos: L'aplicació corre amb el processador del servidor, no del PC de l'usuari.


### Accedir i gestionar els servidors mitjançant tècniques de connexió remota segures.


### Identificar la necessitat de protegir el sistema i aplicar mesures preventives.


### Instal·lar i configurar utilitats de seguretat bàsiques per protegir el sistema contra amenaces externes.


### Configurar i gestionar comptes d'usuaris locals i grups per assegurar un control adequat de l'accés al sistema.


### Establir polítiques de seguretat per comptes d'usuaris i contrasenyes, assegurant el compliment de les bones pràctiques de seguretat.


### Protegir l'accés a la informació mitjançant permisos locals i llistes de control d'accés (ACLs), garantint la privacitat i seguretat de les dades.
