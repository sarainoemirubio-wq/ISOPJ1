## Administració de Dominis i Seguretat

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/165783ed-76b1-4f2b-aeb8-a46cdf4c94dc" />


### Configurar i gestionar dominis, assegurant un correcte accés i explotació de recursos de xarxa.

<img width="3200" height="3000" alt="image" src="https://github.com/user-attachments/assets/b30ab4a1-066c-43d4-94dd-d765372d2f22" />

Para poder gestionar y configurar los dominios tenemos que tener algunos conceptos claros antes de hacer la práctica:

#### LDAP es un protocolo que permite almacenar y consultar información de usuarios y recursos en un directorio centralizado.

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

luego ls; nano uo.ldif:   que este se usa para:

añadir usuarios

crear grupos

modificar directorio

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

después vamos a : nano /etc/nsswitch.conf, aquí a todas ponemos ‘ldap compat’ antes de los primeros files; 

<img width="625" height="220" alt="image" src="https://github.com/user-attachments/assets/41226e49-4333-4c5b-a750-6e4b11f4176b" />

después: nano /etc/pam.d/common-password aquí ponemos en password de la cuarta fila cambiamos el use.authusl y que solo quede el try sin tocar el de atras .so;

<img width="833" height="81" alt="image" src="https://github.com/user-attachments/assets/eeb779f5-bf17-4d37-9395-f65419dba537" />

lugo ponemos:  nano /etc/pam.d/common-session aquí baix de tot el arxiu creamos una linea se: session optional pam_mkhomedir.so skel=/etc/skel umask=022 ( este es para que se cree la seva home y ejecute el modul de homedir); 

<img width="542" height="47" alt="image" src="https://github.com/user-attachments/assets/fd71061f-80df-4ee9-a772-791e7dd9b235" />

después: nano /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf: user-session=ubuntu intro greeter-show-manual-login=true; getent passwd | grep alu1 (aquí tenemos que ver los usuaris al local y al server osea alu1); reboot; 

<img width="290" height="70" alt="image" src="https://github.com/user-attachments/assets/8a0772b6-21d1-4d73-b1d4-b83f0689c8b0" />


siguiente a esto: si no funciona un: su alu1
després un rebbot


aquí hemos modificado common, user share, etc


<img width="622" height="296" alt="image" src="https://github.com/user-attachments/assets/41b36d81-8c22-4eca-8812-e16f552123b0" />


comprobacio de que ha funcionat:


<img width="338" height="51" alt="image" src="https://github.com/user-attachments/assets/5cde7eb8-a680-4979-9964-9907c620124f" />


### Configurar l'accés a recursos locals i remots, garantint la connectivitat i seguretat adequades.



<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/9f35bab0-b94d-47a6-9b39-c1e346a0b69c" />



#### Recursos Locals: 

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/792a0cce-30a7-4e3c-88c2-54b6249511ca" />



Són els recursos que es troben físicament dins de la mateixa màquina o servidor que està utilitzant l’usuari. Això significa que no depenen d’una xarxa per accedir-hi, ja que estan connectats directament a l’ordinador.

Exemples de recursos locals:

El disc dur o SSD de l’ordinador.

Carpetes i fitxers guardats al sistema.

Impressores connectades per USB.

Altres dispositius connectats directament com escàners o memòries USB.

Gestió:
La gestió d’aquests recursos es fa mitjançant el sistema de fitxers del sistema operatiu. El sistema de fitxers s’encarrega d’organitzar les dades, controlar l’espai d’emmagatzematge i permetre l’accés als fitxers.

En sistemes Windows s’utilitza principalment NTFS.

En sistemes Linux són habituals ext4 o XFS.

Seguretat:
La seguretat dels recursos locals es controla mitjançant permisos d’usuari i de grup configurats al sistema operatiu. Aquests permisos determinen qui pot llegir, escriure o executar un fitxer o utilitzar un dispositiu.
Per exemple, un administrador pot decidir quins usuaris poden accedir a determinades carpetes del disc o utilitzar una impressora connectada a l’ordinador.


#### Recursos Remots


<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/cd7cf6b9-23de-41e0-b771-1bc1b5c62f0f" />




Són recursos que no es troben dins de l’ordinador de l’usuari, sinó que estan allotjats en altres servidors dins de la xarxa o a Internet. Per poder accedir-hi és necessari utilitzar una connexió de xarxa.

Aquests recursos permeten compartir informació i serveis entre diversos usuaris o ordinadors sense que les dades estiguin guardades localment.

Exemples de recursos remots:

NAS (Network Attached Storage) per guardar fitxers compartits.

Servidors de fitxers dins d’una empresa.

Bases de dades allotjades en un servidor.

Serveis al núvol com sistemes d’emmagatzematge o aplicacions remotes.

Protocols de connectivitat:
Són els protocols de xarxa que permeten accedir als recursos remots.

SMB/CIFS: Protocol utilitzat principalment en entorns Windows per compartir carpetes i impressores a través de la xarxa.

NFS: Protocol molt utilitzat en sistemes Linux i Unix per compartir directoris entre equips dins d’una xarxa.

SSH/SFTP: Protocols segurs que permeten transferir fitxers i executar ordres de manera remota amb connexions xifrades.

Seguretat:
L’accés als recursos remots requereix mesures de seguretat addicionals perquè les dades es transmeten per la xarxa.

Autenticació: procés per verificar la identitat de l’usuari (usuari i contrasenya, claus SSH, etc.).

Autorització: determina quins recursos pot utilitzar l’usuari i quines accions pot realitzar (llegir, escriure, modificar o executar).

En molts sistemes també s’utilitzen xifratge de dades, tallafocs i control d’accés per protegir la informació que es comparteix a través de la xarxa.



#### El binomi: Connectivitat + Seguretat



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/617e0e19-81b3-4c26-8cd2-6d934a7e0d86" />





Perquè un recurs remot funcioni correctament en una xarxa, és necessari combinar connectivitat i seguretat.
La connectivitat permet que els equips puguin trobar i accedir al recurs, mentre que la seguretat controla qui pot entrar i què pot fer una vegada dins.

Perquè la configuració sigui correcta, s’han de complir tres condicions principals:

1. Visibilitat
El recurs ha de ser visible i accessible dins de la xarxa. Això significa que el servidor ha d’estar connectat i que els ports necessaris estiguin oberts al tallafoc perquè altres equips puguin comunicar-se amb ell.
Per exemple:

Port 445 per a compartir fitxers amb SMB.

Port 22 per a connexions remotes amb SSH.

Si aquests ports estan bloquejats o el servidor no és accessible, els usuaris no podran ni intentar accedir al recurs.

2. Permisos de compartició
Aquests permisos determinen qui pot accedir al recurs a través de la xarxa, és a dir, qui té permís per connectar-se al servidor o a la carpeta compartida.
Es pot limitar l’accés només a determinats usuaris o grups perquè no tothom de la xarxa pugui entrar.

3. Permisos de sistema (ACL – Access Control List)
Una vegada que l’usuari ha accedit al recurs, entren en joc els permisos del sistema de fitxers.
Les ACL (Access Control List) permeten definir permisos detallats sobre fitxers i carpetes, com ara:

Llegir el contingut.

Escriure o modificar fitxers.

Executar programes.

Això significa que un usuari pot tenir accés a la carpeta compartida però només amb permisos de lectura, sense poder modificar els fitxers.

Exemple:
Un usuari pot veure una carpeta compartida en la xarxa (visibilitat), tenir permís per accedir-hi (permisos de compartició), però només poder llegir els fitxers sense modificar-los gràcies als permisos ACL.




### Assignar i gestionar drets d'usuari i directives de seguretat per protegir els recursos i el sistema.




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/15f0de44-fa61-45d5-a116-dadc8f65ff23" />






Per mantenir la seguretat d’un sistema informàtic és necessari controlar què poden fer els usuaris. Això es fa mitjançant permisos i drets d’usuari, que permeten limitar l’accés als recursos i evitar accions que podrien comprometre el sistema.

Aquests mecanismes formen part de les directives de seguretat, que estableixen les normes d’accés i ús dels recursos del sistema.

És important entendre la diferència entre aquests dos conceptes:

Permisos
Els permisos s’apliquen a objectes concrets del sistema, com ara fitxers, carpetes, impressores o altres recursos compartits. Serveixen per determinar què pot fer un usuari amb aquell recurs específic.

Alguns exemples de permisos són:

Llegir un fitxer.

Escriure o modificar un document.

Executar un programa.

Eliminar fitxers o carpetes.

Per exemple:
Un usuari pot tenir permís per llegir un document, però no per modificar-lo o eliminar-lo.

Drets d’usuari
Els drets d’usuari s’apliquen al sistema operatiu en general, no a un objecte concret. Defineixen quines accions administratives o del sistema pot realitzar un usuari.

Alguns exemples de drets d’usuari són:

Canviar l’hora del sistema.

Apagar o reiniciar el servidor.

Instal·lar programes.

Iniciar sessió remotament.

Fer còpies de seguretat del sistema.

Per exemple:
Un administrador pot tenir dret a apagar el servidor, mentre que un usuari normal no tindrà aquest dret.

En resum:

Permisos → controlen l’accés a recursos concrets (fitxers, carpetes, impressores).

Drets d’usuari → controlen accions que afecten el sistema operatiu.




#### Directives de Seguretat



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/bc04b004-499c-4371-8246-91dba5543488" />





Les directives de seguretat són un conjunt de normes i configuracions definides pels administradors del sistema per protegir els recursos, les dades i els usuaris. Aquestes directives permeten automatitzar la seguretat, de manera que totes les màquines i usuaris segueixin les mateixes regles sense haver de configurar-ho manualment cada vegada.

L’objectiu principal és reduir riscos de seguretat, evitar accessos no autoritzats i garantir un ús correcte dels sistemes informàtics dins d’una organització.

Alguns exemples comuns de directives de seguretat són:

Complexitat de contrasenyes
Aquesta directiva obliga els usuaris a crear contrasenyes segures. Normalment exigeix que la contrasenya tingui:

Un nombre mínim de caràcters.

Majúscules i minúscules.

Números.

Símbols especials.

Això ajuda a evitar que les contrasenyes siguin fàcils d’endevinar o vulnerables a atacs.

Bloqueig de compte
Aquesta directiva protegeix el sistema contra intents repetits d’accés no autoritzat.
Si un usuari introdueix la contrasenya incorrecta diverses vegades (per exemple, 3 o 5 intents), el sistema bloqueja temporalment el compte.

Això evita atacs de força bruta, en què un atacant prova moltes contrasenyes fins trobar la correcta.

Restriccions de programari
Aquestes directives impedeixen que els usuaris instal·lin o executin aplicacions no autoritzades.
Això ajuda a prevenir:

Instal·lació de malware o virus.

Ús de programari no aprovat per l’empresa.

Problemes de seguretat o compatibilitat en el sistema.

Per exemple, només els administradors poden instal·lar nous programes al sistema.

En resum:
Les directives de seguretat permeten establir normes automàtiques que tots els usuaris han de seguir, millorant la protecció del sistema, de les dades i de la xarxa.




### Implementar i gestionar servidors de fitxers, servidors d'impressió i servidors d'aplicacions per cobrir les necessitats de l'entorn.




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/7078990c-2dec-4585-9a91-b8447fcebd50" />






En un entorn informàtic, els servidors són equips que proporcionen serveis i recursos a altres ordinadors o usuaris dins de la xarxa. Implementar i gestionar correctament els servidors és clau perquè els usuaris puguin treballar de manera eficient i segura.

Hi ha diferents tipus de servidors segons el servei que ofereixen:

1. Servidors de fitxers

Funció: Permeten emmagatzemar, organitzar i compartir fitxers dins de la xarxa.

Exemple: Una carpeta compartida en un servidor on diversos usuaris poden guardar documents, fulls de càlcul o presentacions.

Beneficis: Centralitza l’emmagatzematge, facilita còpies de seguretat i permet controlar permisos d’accés.

2. Servidors d’impressió

Funció: Gestionen les impressores connectades a la xarxa i controlen les cues d’impressió.

Exemple: Una impressora d’oficina que és compartida per tots els equips mitjançant un servidor d’impressió.

Beneficis: Evita que cada ordinador necessiti configurar la impressora per separat i permet controlar qui pot imprimir i quantes pàgines.

3. Servidors d’aplicacions

Funció: Allotgen i executen aplicacions centralitzades que poden utilitzar diversos usuaris a través de la xarxa.

Exemple: Sistemes ERP, CRM, aplicacions de gestió de bases de dades o eines de disseny col·laboratiu.

Beneficis: Centralitza la instal·lació i actualització de programari, redueix els requisits de hardware dels equips clients i facilita el manteniment.

Gestió i bones pràctiques:

Configuració correcta: assegurant que els serveis funcionen i que els usuaris poden accedir-hi segons els permisos establerts.

Seguretat: aplicar autenticació, permisos i backups per protegir les dades i els serveis.

Monitorització: vigilar el rendiment i disponibilitat dels servidors per evitar interrupcions.

Resum:
Implementar i gestionar aquests servidors permet que l’entorn informàtic sigui eficient, segur i fàcil de mantenir, assegurant que els recursos estiguin disponibles quan els usuaris els necessiten.



#### Tipus de Servidors i la seva funció:




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/08b73d1f-40f9-4317-a3fb-c1f0766f228b" />






1. Servidors de Fitxers (File Servers)
Són el magatzem central de dades dins d’una organització. La seva funció és guardar fitxers i documents de manera estructurada i segura, permetent que diversos usuaris puguin accedir-hi segons els permisos assignats.

Quota de disc: Limita l’espai que cada usuari pot utilitzar, evitant que algú consumeixi tot l’emmagatzematge del servidor.

Auditoria: Permet saber qui ha creat, modificat o esborrat un fitxer, útil per seguretat i control de la informació.

Benefici principal: Centralitza les dades, facilita còpies de seguretat i garanteix un control d’accés consistent.

2. Servidors d’Impressió (Print Servers)
Gestionen les impressores de l’oficina i les cues d’impressió, evitant que cada ordinador hagi de connectar-se directament a cada impressora.

Centralització: Només cal instal·lar el controlador (driver) una vegada al servidor i automàticament es posa a disposició de tots els usuaris.

Gestió: Permet cancel·lar treballs encallats, prioritzar impressions importants o controlar qui pot imprimir.

Benefici principal: Estalvia temps i recursos, i facilita la gestió de múltiples impressores.

3. Servidors d’Aplicacions (App Servers)
Executen programari centralitzat que pot ser accedit per diversos usuaris des dels seus ordinadors clients.

Recursos: L’aplicació s’executa utilitzant el processador i la memòria del servidor, no del PC de l’usuari.

Exemples: ERP, bases de dades corporatives, aplicacions de gestió d’inventari o eines col·laboratives.

Benefici principal: Permet que els usuaris treballin amb aplicacions potents sense necessitat que els seus equips siguin molt potents, i facilita el manteniment i actualitzacions del programari.

En resum:
Cada tipus de servidor té una funció específica que cobreix necessitats diferents dins de l’entorn informàtic:

Fitxers → emmagatzematge i control de dades.

Impressió → gestió de recursos físics com impressores.

Aplicacions → execució centralitzada de programari per usuaris múltiples.




### Accedir i gestionar els servidors mitjançant tècniques de connexió remota segures.




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/2d37f4c9-dfe5-4255-81de-279899a62a3e" />





En molts entorns, els administradors o usuaris necessiten gestionar servidors sense estar físicament davant del maquinari. Això es fa mitjançant connexió remota, que permet controlar el servidor des d’un ordinador diferent a través de la xarxa.

Per què és important fer-ho de manera segura?
Accedir a un servidor sense protecció pot permetre que persones no autoritzades manipulin dades, programes o configuracions del sistema, provocant problemes de seguretat, pèrdues de dades o interrupcions del servei.

Tècniques de connexió remota segures:

SSH (Secure Shell)

Permet accedir a servidors Linux o Unix de manera xifrada.

Exemple: Administrar un servidor de fitxers des de casa sense que les dades viatgin en text pla.

SFTP (Secure File Transfer Protocol)

Permet transferir fitxers entre el client i el servidor de manera segura.

Exemple: Pujar actualitzacions de software al servidor sense exposar les contrasenyes.

RDP (Remote Desktop Protocol)

Permet veure i controlar l’escriptori d’un servidor Windows com si estiguessis davant del PC.

S’ha d’utilitzar amb connexions segures, com VPN, per evitar accessos no autoritzats.

VPN (Virtual Private Network)

Proporciona un túnel segur per connectar-se a la xarxa de l’empresa abans d’accedir al servidor.

Protegeix les dades mentre viatgen per Internet.

Bones pràctiques addicionals:

Utilitzar autenticació de dos factors sempre que sigui possible.

Canviar ports per defecte dels serveis remots per dificultar atacs.

Monitoritzar els accessos i registrar les connexions per auditoria.

En resum:
Accedir i gestionar els servidors de manera remota estalvia temps i recursos, però cal aplicar tècniques i mesures de seguretat per garantir la protecció de dades i del sistema.




### Identificar la necessitat de protegir el sistema i aplicar mesures preventives.




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/a8d5e73a-12cf-4898-9550-e4adfb0c00b8" />





Protegir un sistema informàtic és essencial per evitar pèrdues de dades, accessos no autoritzats o falles en el funcionament dels serveis. Abans d’aplicar mesures, cal identificar quins recursos i dades són crítics i quins riscos poden afectar-los.

Per què és necessari protegir el sistema?

Evitar que usuaris no autoritzats accedeixin a fitxers sensibles.

Prevenir atacs de malware o virus que poden corrompre informació.

Garantir que els serveis com servidors de fitxers, impressió i aplicacions estiguin sempre disponibles.

Complir normatives legals sobre protecció de dades.

Mesures preventives principals:

Control d’usuaris i permisos

Assignar drets d’usuari i permisos sobre fitxers i carpetes segons les funcions de cada persona.

Exemple: Un empleat de comptabilitat pot llegir factures però no modificar-les.

Ús de contrasenyes fortes i polítiques de seguretat

Aplicar directives com complexitat de contrasenyes, caducitat i bloqueig de comptes.

Exemple: Obligar a que les contrasenyes tinguin números, majúscules i símbols.

Protecció de la xarxa i connexions remotes

Utilitzar firewalls, VPNs i protocols segurs com SSH o SFTP.

Exemple: L’administrador accedeix al servidor de manera remota amb SSH xifrat.

Còpies de seguretat (backups)

Guardar còpies de dades importants en llocs segurs i diferents del servidor principal.

Exemple: Copiar fitxers crítics a un NAS o núvol diàriament.

Actualitzacions i manteniment

Aplicar actualitzacions de sistema i programari per tancar vulnerabilitats conegudes.

Exemple: Instal·lar pegats de seguretat de Windows o Linux regularment.

En resum:
Identificar la necessitat de protecció consisteix a conèixer què cal protegir i quins riscos existeixen, mentre que aplicar mesures preventives garanteix que les dades, aplicacions i serveis siguin segurs i fiables.




### Instal·lar i configurar utilitats de seguretat bàsiques per protegir el sistema contra amenaces externes.



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/7575c8e1-85d0-4888-a1cf-2629450ebf62" />





Els sistemes informàtics poden estar exposats a malware, virus, atacs externs i intrusions no autoritzades. Per això és fonamental instal·lar i configurar eines de seguretat que detectin i bloquegin aquestes amenaces abans que puguin causar problemes.

Tipus d’utilitats de seguretat bàsiques:

Antivirus i antimalware

Detecten i eliminen programari maliciós com virus, troians o ransomware.

Exemple: Windows Defender, Avast o Malwarebytes.

Bona pràctica: Configurar escaneigs automàtics i actualitzacions periòdiques.

Tallafocs (firewalls)

Controlen el trànsit de xarxa entrant i sortint, permetent només connexions segures.

Exemple: Activar el tallafocs de Windows o configurar un firewall de xarxa corporativa.

Bona pràctica: Bloquejar ports no necessaris i permetre només els serveis autoritzats.

Gestors de contrasenyes

Permeten generar i guardar contrasenyes fortes i úniques per a cada servei.

Exemple: LastPass, Bitwarden o 1Password.

Bona pràctica: No reutilitzar contrasenyes i activar autenticació de dos factors quan sigui possible.

Actualitzacions automàtiques del sistema i del programari

Asseguren que el sistema i les aplicacions tinguin els últims pegats de seguretat.

Exemple: Actualitzacions de Windows Update o apt/yum en Linux.

Beneficis principals:

Redueixen el risc de pèrdua de dades o accés no autoritzat.

Manté els sistemes disponibles i fiables per als usuaris.

Faciliten la gestió i monitorització de seguretat en entorns corporatius.

En resum:
Instal·lar i configurar aquestes utilitats és una mesura preventiva essencial, ja que protegeix el sistema contra les amenaces externes i garanteix que els recursos i dades estiguin segurs i disponibles.




### Configurar i gestionar comptes d'usuaris locals i grups per assegurar un control adequat de l'accés al sistema.




<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/b3bf2d14-221d-4ddb-9873-5fcdd6046e3e" />





En un sistema informàtic, cada usuari necessita un compte propi per accedir a recursos com fitxers, aplicacions o impressores. Gestionar aquests comptes de manera correcta és clau per controlar qui pot fer què i garantir la seguretat del sistema.

1. Comptes d’usuaris locals

Són comptes creats directament en l’ordinador o servidor.

Permeten identificar cada usuari i aplicar permisos personalitzats.

Exemple: Un empleat té un compte local amb nom d’usuari i contrasenya per accedir a l’ordinador i els fitxers de l’empresa.

2. Grups d’usuaris

Un grup és una col·lecció d’usuaris amb permisos similars.

Facilita la gestió d’accés: en comptes d’assignar permisos a cada usuari individualment, s’assignen al grup.

Exemple: Un grup “Comptabilitat” amb permisos per accedir a les carpetes de finances, i un grup “Recursos Humans” amb accés a fitxers de personal.

3. Configuració i gestió

Assignar contrasenyes segures i polítiques de caducitat.

Determinar nivells d’accés segons la responsabilitat de cada usuari.

Crear, modificar o eliminar comptes segons les necessitats de l’organització.

Supervisar l’ús dels comptes per detectar accessos no autoritzats.

Avantatges de gestionar correctament usuaris i grups:

Augmenta la seguretat: només els usuaris autoritzats poden accedir als recursos.

Simplifica la administració: canviar permisos d’un grup afecta tots els membres automàticament.

Permet auditar i controlar l’activitat dels usuaris per complir normatives de seguretat.

En resum:
Configurar i gestionar comptes d’usuaris i grups permet controlar l’accés de manera precisa, reduir riscos de seguretat i organitzar millor l’ús dels recursos del sistema.




### Establir polítiques de seguretat per comptes d'usuaris i contrasenyes, assegurant el compliment de les bones pràctiques de seguretat.



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/6f93ea97-5480-4433-9b33-90d384c289d6" />





Les polítiques de seguretat són un conjunt de regles i recomanacions que defineixen com han de crear-se, gestionar-se i utilitzar-se els comptes d’usuaris i les contrasenyes dins d’un sistema. L’objectiu és garantir la protecció de les dades i els recursos i minimitzar riscos de seguretat.

1. Per què són importants?

Eviten que persones no autoritzades accedeixin a recursos sensibles.

Redueixen el risc de robatori d’identitat o accés indegut.

Faciliten el compliment de normatives legals o corporatives sobre seguretat.

2. Elements clau d’una política de seguretat de comptes i contrasenyes:

Complexitat de contrasenyes: Obligar a utilitzar majúscules, minúscules, números i símbols.

Longitud mínima: Contrasenyes amb un mínim de caràcters (per exemple, 8 o 12).

Caducitat de contrasenyes: Forçar el canvi de contrasenya cada període determinat (p. ex., cada 90 dies).

Bloqueig de comptes: Desactivar temporalment el compte després de diversos intents fallits (per exemple, 3-5).

Reutilització prohibida: No permetre utilitzar contrasenyes antigues.

3. Bones pràctiques addicionals:

Activar autenticació de dos factors (2FA) quan sigui possible.

Fer auditoria periòdica dels comptes i permisos d’usuari.

Educar els usuaris sobre com crear contrasenyes segures i protegir-les.

4. Beneficis d’aplicar aquestes polítiques:

Augmenta la seguretat global del sistema.

Evita accessos no autoritzats o filtracions de dades.

Simplifica la gestió de comptes i permisos per als administradors.

Facilita el compliment normatiu en entorns corporatius o regulats.

En resum:
Establir polítiques de seguretat assegura que tots els comptes i contrasenyes segueixin bones pràctiques, reduint els riscos i mantenint el sistema segur i controlat.




### Protegir l'accés a la informació mitjançant permisos locals i llistes de control d'accés (ACLs), garantint la privacitat i seguretat de les dades.



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/bd3b1864-4741-45ce-bde5-f1440874b6e5" />






Quan múltiples usuaris comparteixen un sistema o recursos (fitxers, carpetes, impressores), és essencial controlar qui pot veure, modificar o executar cada recurs. Això s’aconsegueix amb permisos locals i ACLs, que garanteixen la privacitat i seguretat de les dades.

1. Permisos locals

S’apliquen directament a fitxers i carpetes d’un ordinador o servidor.

Permeten definir qui pot llegir, escriure o executar un recurs.

Exemple: Un usuari pot tenir accés a llegir un document però no modificar-lo ni esborrar-lo.

2. Llistes de control d’accés (ACLs)

Són una extensió avançada dels permisos locals, que permet assignar permisos més detallats a múltiples usuaris i grups.

Permeten especificar quins usuaris poden realitzar accions concretes (llegir, escriure, executar, eliminar) sobre cada recurs.

Exemple:

Grup “Comptabilitat” → pot llegir i modificar fitxers financers.

Usuari “Visitant” → només pot llegir informes generals.

3. Avantatges d’utilitzar permisos i ACLs:

Seguretat: Només els usuaris autoritzats poden accedir o modificar la informació.

Privacitat: Es protegeixen dades sensibles i confidencials.

Flexibilitat: Permet configurar accés diferent segons grups o rols dins de l’organització.

Auditoria: Facilita el seguiment de qui ha accedit o modificat un fitxer.

4. Bones pràctiques:

Revisar periòdicament els permisos i ACLs.

Evitar permisos excessius (“accés total” sense necessitat).

Assignar permisos segons el principi del mínim privilegi, només el que és necessari per treballar.

En resum:
Els permisos locals i les ACLs permeten controlar amb precisió l’accés a cada recurs, garantint que les dades es mantinguin segures i privades dins del sistema, i que només els usuaris amb autorització puguin realitzar accions concretes.



