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

Práctica: 
Antes de todo tenemosqe preparar las maquinas, dos ubuntus limpios, uno le ponemos client y al otro server, esto para poder diferenciarlas.

Para preparar las maquinas ponemos una nat network enves de adaptador pont, això perquè? Perquè el adaptador pont cada vegada cambiaria la ip.

Comenzaremos por la maquina server.
Un domini server serveix per a tindre usuaris, grups, equips, recursos i unitats organizatives.
Aquí antes de empezar con la Instalación LDAP haremos algunos cambios:

al server: sudo su; apt update; ip a; en parametres cambiaos la ip y posem  10.0.2.4; 255.255.255.0; 10.0.2.1 y el DNS: 8.8.8.8, la primera ip es la que nos dona ip a, lo aplicamos y desconectamos y volvemos a connectar, hacemos ping para ver si funciona, de 8.8.8.8 y de www.google.es; luego nano /etc/hostname (y dentro de este ponemos server y borramos lo que haya); luego nano /etc/hosts, a la tercera linea 10.0.2.4 server.sari.cat server (poner lo que dice en la nuestra ip a)

<img width="731" height="430" alt="image" src="https://github.com/user-attachments/assets/4d77b409-7318-432e-99a6-24106ad17a83" />


Ara si instalamos LDAP: apt install slaps ldap-utils;

<img width="722" height="423" alt="image" src="https://github.com/user-attachments/assets/ebb94d05-8491-48ea-82b4-f12e23452db3" />

 despues si queremos ver todos los objetos dentro ponemos: slapcat; 

 <img width="468" height="264" alt="image" src="https://github.com/user-attachments/assets/802d4487-2e53-431f-a355-acec7f929f10" />


Ahora crearemos la estructura del Domini:
ponemos: cd Baixades/; ls; unzip arxius.zip; ls; dpkg-reconfigure slapd (esta comanda serveix per a no utilitzar el ldif); en la franja rosa ponemos el domini que hemos puesto: sari.cat, luego nos pide el nom osigue sari, la contraseña de el administrador

<img width="724" height="398" alt="image" src="https://github.com/user-attachments/assets/c50e7909-0fca-4323-9236-28a42d4f84f7" />

luego ls; nano uo.ldif:

<img width="724" height="398" alt="image" src="https://github.com/user-attachments/assets/3b8e8bd1-a727-4eb6-acc5-792e1a5f78af" />

luego ldapadd -c -x -D ‘’cn=admin,dc=sari,dc=cat’’ -W -f uo.ldif (ques esto significa que estamos modificando el nom del domini i els dominis components, -W significa que el comando pedirá la contraseña del usuario indicado con -D y no muestra la contraseña en pantalla; la solicita de forma interactiva.)



<img width="724" height="101" alt="image" src="https://github.com/user-attachments/assets/8fe04a6a-8ce3-4808-b812-7522b0a416ca" />


comanda:  nano usu.ldif aquí modificamos nd: uid=alu1,ou=users,cd=sari,dc=cat, luego  ldapadd -c -x -D ‘’cn=admin,dc=sari,dc=cat’’ -W -f usu.ldif; nano grup.ldif y aquí cambiamos el nombre por el nuestro que es sari;  ldapadd -c -x -D ‘’cn=admin,dc=sari,dc=cat’’ -W -f grup.ldif; slapcat (nos aparecerá lo que hemos creado; 


<img width="467" height="267" alt="image" src="https://github.com/user-attachments/assets/a73f0ed5-9810-4594-9e5c-de1162225b44" />


Ahora aunque no hemos acabado iremos a la maquina del client:

comanda principal: sudo su; ip a; ping a la anterior osigue la server 10.0.2.4; 


<img width="576" height="198" alt="image" src="https://github.com/user-attachments/assets/c67c3c86-b933-4c0d-956a-adeb5a9b7a2d" />

ahora validamos u client al domini: apt update; apt install libnss-ldap libpam-ldap nscd -y; nos sladrá la pantalla rosa, eliminamos la i y que solo tenga dos // y ponemos la ip del server osea  10.0.2.4 intro; dc=sari,dc=cat ningun espacio, intro; version 3; 


<img width="731" height="430" alt="image" src="https://github.com/user-attachments/assets/dcf2b543-d42e-469f-986a-fe6f53f4bd88" />


si; 


<img width="731" height="430" alt="image" src="https://github.com/user-attachments/assets/8a463a6a-5b96-44a2-9e38-7c2305f7b647" />

ahora ponemos esta comanda: cn=admin,dc=sari,dc=cat intro; password; cn=admin,dc=sari,dc=cat intro; dpkg-reconfigure ldap-auth-config; si, si; 3; si; si; password; si; d’acord; 


<img width="731" height="430" alt="image" src="https://github.com/user-attachments/assets/944d1b7b-74f8-4f96-bb8d-23b89d197c9e" />

y posem md5:

<img width="731" height="430" alt="image" src="https://github.com/user-attachments/assets/84febabb-8f5e-4ce3-b94e-18608cb47fa6" />




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
