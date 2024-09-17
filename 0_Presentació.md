---
title: SA0: Presentació del mòdul SGE
language: VA
author: Toni Santos Silvestre [https://github.com/ToniSantosSilvestre]
subject: Sistemes de Gestió Empresarial
keywords: [ERP-CRM, 2024, SGE, Python]
IES: CIPFP Batoi [portal.edu.gva.es/cipfpbatoi/]
header: ${title} - ${subject} (ver: ${today})
footer:${currentFileName}.pdf - ${author} - ${IES} - ${pageNo}/${pageCount}
typora-root-url:${filename}/../
typora-copy-images-to:${filename}/../assets
---

# 0. Presentació del mòdul d'SGE

Hui en dia, molta part de la competitivitat d’una empresa demana tindre optimitzats i integrats els seus fluxos/processos interns i les seues relacions comercials externes, per aconseguir objectius bàsics com són les millores de la productivitat, la qualitat, el servei al client i la reducció de costos. Les organitzacions necessiten integració interna i col·laboració externa per augmentar les oportunitats de sobreviure en un mercat global, cada vegada més competitiu.

Aquesta és la raó de la cerca d’un sistema que permeta assolir totes les necessitats del negoci, des del control de les operacions financeres i la generació d’informes, les relacions i vendes amb els clients, la planificació i programació de la producció, fins al control d’inventari i costos. En l’actualitat, les organitzacions busquen implementar sistemes que els permeten controlar totes les àrees del negoci, de forma integral. Així, amb un sistema integrat, tota l’empresa, els seus sistemes i processos, es centralitzen i integren per al benefici de tota l’organització.

A conseqüència de tot aquest sistema integrat, l’organització ha de veure com es generaren millors resultats, sempre que s’implante el programari adequadament, oferint com a benefici el control i el monitoratge de les operacions, l’eficiència administrativa, una productivitat més adequada, un servei al client més eficient, estalvi de costos i suport més fiable per a la presa de decisions.

En aquest sentit, els sistemes ERP, de l’anglès *Enterprise Resource Planning*, coneguts àmpliament com a sistemes de planificació de recursos empresarials o sistemes de gestió empresarial, són sistemes que integren o pretenen integrar totes les dades i processos d’una organització en un sistema unificat.

Aquest mòdul té com a finalitat inicial l’aproximació conceptual al món dels sistemes de gestió empresarial i la seua implantació a l’empresa.

Al començament de la situació d'aprenentatge **“ Identificació de sistemes ERP-CRM i solucions BI”**, i des d’un punt de vista teòric, s’examinen els diferents tipus de llicenciament de programaris ERP-CRM i els diferents tipus de desplegament de programari. També es veurà què són els sistemes ERP-CRM i les solucions BI i s’identifiquen els principals productes existents en l’actualitat. D’altra banda, s’identifiquen els punts a tindre en compte en la implantació tècnica d’un sistema ERP-CRM. A continuació es fa la instal·lació i configuració d’un ERP-CRM, en concret el programari Odoo en la situació d'aprenentatge **" Implantant un ERP-CRM a un negoci "**.

L’altra gran finalitat d’aquest mòdul és l’explotació i adequació dels sistemes de gestió empresarial desenvolupant components específics segons les necessitats i requeriments plantejats.

Primerament, a la situació **"Gestió de campanya amb ERP-CRM"** s'avalua l'ajust de l'aplicació a casos reals com puguen ser els de una campanya de llançament de productes o serveis, valorant el grau de flexibilitat que oferix. 

En les unitats **“Sistemes ERP. Explotació i adequació (I i II)“**, s’estudia el desenvolupament de nous mòduls que es puguen integrar al sistema, amb el programari i llenguatges específics. A continuació, en la segona part, aprendrem a ampliar i modificar mòduls existents, traduccions idiomàtiques, aspectes relatius a la seguretat, dissenyar i modificar informes.

Els continguts d’aquest mòdul tenen una orientació bàsicament professionalitzadora, es proposa una formació pràctica i aplicable amb l’objectiu que l’alumnat aprenga a saber fer. Una vegada llegits detingudament els continguts de cada apartat, cal realitzar les activitats i els exercicis d’autoavaluació per tal de posar en pràctica i comprovar l’assoliment dels coneixements adquirits. I, sobretot en les unitats referides a l’explotació i adequació dels sistemes ERP, és molt important la pràctica, en els pmateixos ordinadors, dels exemples que es descriuen en el material docent. 



### Resultats d'aprenentatge

En finalitzar aquest mòdul l’alumne/a:

- Sistemes ERP-CRM. Implantació:
  - Identifica sistemes de planificació de recursos empresarials i de gestió de relacions amb clients (ERP-CRM) reconeixent les seues característiques i verificant la configuració del sistema informàtic.
  - Implanta sistemes ERP-CRM interpretant la documentació tècnica i identificant les diferents opcions i mòduls.
- Sistemes ERP-CRM. Explotació i adequació
  - Realitza operacions de gestió i consulta de la informació seguint les especificacions de disseny i utilitzant les eines proporcionades pels sistemes ERP-CRM i solucions d’intel·ligència de negocis (BI).
  - Adapta sistemes ERP-CRM identificant els requeriments d’un supòsit empresarial i utilitzant les eines proporcionades pels mateixos.
  - Desenvolupa components per a un sistema ERP-CRM analitzant i utilitzant el llenguatge de programació incorporat.

### Glossari

-**\_\_init\_\_.py** *n* Fitxer d’existència obligada en qualsevol mòdul Python per indicar els arxius Python que s’han importar. 

-**\_\_manifest\_\_.py** *n* Fitxer descriptiu d’un mòdul d’OpenObject. En versions anteriors s’anomenava \_\_openerp\_\_.py. - 

-**\_\_openerp\_\_.py** *n* Vegeu *\_\_manifest\_\_.py.* 

-**arquitectura MVC** *f* Patró de disseny d’aplicacions que distingix tres capes: model (que  contempla la definició de les dades), vista (que contempla la definició  dels formularis i menús) i controlador (que contempla la lògica de  negoci).

-**cloud computing** *n* Vegeu *informàtica en el núvol*. 

 -**CRM** *n* Acrònim de *Customer RelationShip Management*. Vegeu *sistema CRM*. 

-**cub multidimensional** *m* Representació matricial (N dimensions) de les dades planes representades via *files* i columnes en una taula relacional, utilitzat en l’anàlisi OLAP. 

-**cub OLAP** *m* Vegeu *cub multidimensional*. 

-**dashboard** *n* Vegeu *quadre de comandament*. 

 -**data warehouse** *n* Magatzem de dades. Base de dades del repositori d’una solució BI,  destinada a contindre una col·lecció de dades orientada a un determinat  àmbit (empresa, organització, matèria…), integrada, no volàtil i  variable en el temps, que ha de servir de base per a l’aplicació d’eines analítiques amb l’objectiu d’obtenir informació útil per a la presa de  decisions. 

 -**datamart** *n* Aparador de dades. Subconjunt de dades del *data warehouse*, corresponents a una unitat de negoci (àrea) de l’organització, amb  l’objectiu de solucionar la problemàtica d’anàlisi de l’àrea  corresponent. 

 -**desplegament IaaS** *m* Acrònim d’*Infraestructure as a service*. L’organització contracta la infraestructura tecnològica (capacitat de  procés, d’emmagatzematge i/o de comunicacions) sobre les quals instal·la les seues plataformes (sistemes operatius) i aplicacions. L’organització té el control total sobre les plataformes i aplicacions,  però no té cap control sobre les infraestructures. 

 -**desplegament \"on-premise\"** *m* Programari de l’organització instal·lat a les seves dependències i sota la seva responsabilitat. 

 -**desplegament PaaS** *m* Acrònim de *Platform as a service*. L’organització contracta un servei que li permet allotjar i  desenvolupar les seues pròpies aplicacions (siguen desenvolupaments  propis o llicències adquirides) en una plataforma que disposa d’eines de desenvolupament perquè l’organització puga elaborar i/o adequar la  solució. L’organització no té cap control sobre la plataforma ni sobre  la infraestructura, però manté el control total sobre les seues  aplicacions. 

 -**desplegament SaaS** *m* Acrònim de *Software as a service*. L’organització contracta la utilització d’unes determinades  aplicacions, sobre les quals únicament pot exercir accions de  configuració i parametrització permeses pel proveïdor. L’organització no té cap control sobre l’aplicació ni sobre la plataforma, ni sobre la  infraestructura. 

 -**dia** *f* Eina de diagramació de propòsit general. OpenObject facilita un connector  per generar mòduls a partir de diagrames dissenyats amb aquesta eina. 

 -**eina \"data mining\" en BI** *f* Eina d’alt nivell que intenta obtenir informació no trivial que  resideix de manera implícita en les dades, que era prèviament  desconeguda i que pot resultar útil per a algun procés. 

 -**eina \"query&reporting\" en BI** *f* Tradicionals eines que permeten dissenyar i executar consultes sobre  una base de dades i formatar el resultat en informes. Acostuma a  aplicar-se sobre bases de dades dels sistemes OLTP i sobre el *data warehouse* i els *datamart*. 

 -**ERP** *n* Acrònim d’*Enterprise Resource Planning*. Vegeu *sistema ERP*. 

 -**ETL** *n* Acrònim d’*Extract, Transform and Load*. Procés de filtrat, reestructuració de dades i eliminació  d’inconsistències, en els processos de càrrega del *data warehouse* a partir de diversos orígens. 

 -**fitxer mestre** *m* Conjunt de registres corresponent a un aspecte important dins d’una  aplicació. El terme prové de l’època en què les aplicacions utilitzaven  sistemes gestors de fitxers; avui dia aquests registres s’emmagatzemen  en bases de dades. 

 -**free software** *n* Vegeu *programari lliure*. 

 -**freeware software** *n* Mot anglès per fer referència al programari gratuït, sigui o no lliure. 

 -**function** *n* Tipus d’atribut que s’utilitza en la definició de classes d’OpenObject, per definir un camp calculat a través d’una funció Python. 

 -**herència de classe** *f* Tipus d’herència facilitat per OpenObject consistent en evolucionar una classe (classe base de la qual es deriva) per ampliar-ne la  funcionalitat (atributs i/o mètodes). La nova classe ha de tenir el  mateix nom que la classe base i substitueix la classe original. 

 -**herència per delegació** *f* Tipus d’herència facilitat per OpenObject que consisteix a obtenir una  nova classe, la qual “delega” certs funcionaments a altres classes que  incorpora en el seu interior. Aquest tipus d’herència permet herència  múltiple. 

 -**herència per prototipus** *f* Tipus d’herència facilitat per OpenObject que consisteix a obtenir una  nova classe a partir de la classe base (“prototipus”), ampliant la  funcionalitat (atributs i/o mètodes). La nova classe ha de tenir un nom  diferent del de la classe base. La classe base continua existint. 

 -**HRM** *n* Acrònim de *Human Resource Management*. Vegeu *sistema HRM*. 

 -**informàtica en el núvol** *f* Programari de l’organització instal·lat en ubicacions remotes, propietat de tercers, als quals se’ls lloga el servei. 

 -**informe JRXML** *m* Tipus d’informe inserible en OpenObject, generat amb el motor  d’informes JasperReports a partir d’una plantilla que pot ser generada  manualment (si es coneix el llenguatge JRXML) o amb l’aplicació iReport  Designer. 

 -**informe RML** *m* Tipus d’informe inserible en OpenObject, generat amb el motor  d’informes RLTK a partir d’una plantilla que pot ser generada manualment (si es coneix el llenguatge RML) o amb l’aplicació Writer de  LibreOffice / OpenOffice. 

 -**in-house** *n* Vegeu *desplegament on-premise*. 

 -**interlocutor comercial** *m* Vegeu *tercer*. 

 -**iReport Designer** *n* Eina gràfica de disseny de plantilles JRXML per generar informes amb el motor d’informes JasperReport. 

 -**JasperReport** *n* Motor d’informes que genera informes a partir d’una plantilla Jasper obtinguda amb la compilació d’una plantilla JRXML. 

 -**JasperReport Server** *n* Servidor d’informes que permet allotjar informes Jasper i fer-los  accessibles de forma centralitzada a tots els usuaris d’una  organització. Hi ha una versió *Community* i una versió *Professional* (permet quadres de comandament). 

 -**KPI** *n* Acrònim de *Key Performance Indicator* (indicador clau d’acompliment). Fa referència a mètriques utilitzades  per quantificar els objectius que reflecteixen el rendiment d’una  organització, i que generalment es recullen en el seu pla estratègic. 

 -**llenguatge JRXML** *m* Vegeu *informe JRXML*. 

 -**llenguatge RML** *m* Vegeu *informe RML*. 

 -**llicència de programari** *f* Autorització o permís concedit pels autors del programari per poder-lo utilitzar, sota uns drets i deures. 

 -**m** *n* Acrònim de *Business Intelligence*. Vegeu *solució BI*. 

 -**many2many** *n* Tipus d’atribut relacional que s’utilitza en la definició de classes  d’OpenObject per definir una relació de molts a molts entre dues  classes. 

 -**many2one** *n* Tipus d’atribut relacional que s’utilitza en la definició de classes  d’OpenObject per definir una relació de molts a un entre dues classes.  La seua definició obliga a l’existència de l’atribut relacional one2many complementari. 

 -**mètode \"browse\"** *m* Mètode de la capa ORM d’OpenObject que permet recuperar els recursos  d’un objecte com a llista d’objectes sobre els quals és possible aplicar la notació de punt per accedir a qualsevol dels seus camps i, en el cas de camps relacionals, navegar cap als objectes apuntats. 

 -**mètode \"create\"** *m* Mètode de la capa ORM d’OpenObject que permet crear un nou registre amb els valors facilitats al mètode. 

 -**mètode \"name_get\"** *m* Mètode de la capa ORM d’OpenObject que permet dissenyar la forma  d’obtenir la representació textual (_name) dels recursos d’un objecte. 

 -**mètode \"on_change\"** *m* Mètode dissenyat en el model d’una classe (arxiu Python) que pot ser invocat des d’atributs editables en les vistes *form* per aconseguir modificar el valor d’altres camps quan l’usuari modifica el camp que invoca el mètode *on_change*. 

 -**mètode \"read\"** *m* Mètode de la capa ORM d’OpenObject que permet la lectura de camps per a un conjunt de recursos d’un mateix objecte. 

 -**mètode \"search\"** *m* Mètode de la capa ORM d’OpenObject que permet obtenir la llista  d’identificadors dels recursos d’un objecte que verifiquen els criteris  de cerca facilitats al mètode. 

 -**mètode \"self.pool.get\"** *m* Mètode especial de la capa ORM d’OpenObject que permet obtenir  l’objecte Python que gestiona els recursos del model associat a  qualsevol classe. 

 -**mètode \"unlink\"** *m* Mètode de la capa ORM d’OpenObject que permet eliminar els registres indicats al mètode. 

 -**mètode \"write\"** *m* Mètode de la capa ORM d’OpenObject que permet modificar els registres indicats al mètode amb els valors també assenyalats. 

 -**mineria de dades** *f* Vegeu *eina data mining*. 

 -**MVC** *m* Acrònim de model-vista-controlador. Vegeu *arquitectura MVC*. 

 -**Odoo** *n* ERP de codi obert baix llicència LGPL-3.

 -**OLAP** *n* Acrònim d’*On Line Analytical Processing* (procés analític en línia). Vegeu *sistema OLAP*. 

 -**OLTP** *n* Acrònim d’*On Line Transaction Processing* (procés de transaccions en línia). Vegeu *sistema OLTP*. 

 -**one2many** *n* Tipus d’atribut relacional que s’utilitza en la definició de classes  d’OpenObject, per definir una relació d’un a molts entre dues classes. 

 -**on-premise** *n* Vegeu *desplegament on-premise*. 

 -**open source** *n* Vegeu *programari de codi obert*. 

 -**OpenERP** *n* ERP de codi obert sota llicència AGPL. A partir de la servió 8 va agafar el nom Odoo

 -**OpenObject** *n* *Framework* de tipus RAD en el qual s’ha desenvolupat Odoo. 

 -**ORM** *n* Acrònim d’*Object Relational Mapping*. Capa de programari encarregada de facilitar la persistència de les  classes d’una aplicació orientada a objectes en un sistema gestor de  bases de dades relacionals. 

 -**pgAdmin** *n* Eina gràfica per interactuar amb servidors PostgreSQL. 

 -**PostgreSQL** *n* Sistema gestor de bases de dades relacionals utilitzat per Odoo. 

 -**programari de codi obert** *m* Programari menys restrictiu quant a llibertats que ha de garantir, que  verifica el decàleg definit per l’Open Source Initiative. 

 -**Python** *n* Llenguatge de programació orientat a objectes. 

 -**RAD** *n* Acrònim de *Rapid Applications Development*. Entorn de desenvolupament molt simple per al programador, que permet obtenir aplicacions d’altes prestacions amb poc esforç. 

 -**related** *n* Tipus d’atribut que s’utilitza en la definició de classes d’OpenObject  per definir un camp que accedisca a un camp d’un altre objecte,  relacionat des del mateix objecte. 

 -**vista \"calendar\" d’un objecte** *f* Vista que facilita la ubicació dels recursos de l’objecte en un  interval de temps, sempre que l’objecte continga camps de tipus  temporal, que en permeten la ubicació en un calendari. 

 -**vista \"form\" d’un objecte** *f* Vista formulari que distribueix en la pantalla els camps de l’objecte  amb l’objectiu de facilitar la visualització i/o l’edició d’un recurs de l’objecte. 

 -**vista \"graph\" d’un objecte** *f* Vista que permet la visualització de gràfics construïts a partir de les dades contingudes en els recursos de l’objecte. 

 -**vista \"search\" d’un objecte** *f* Vista pensada per personalitzar les opcions de cerca de recursos sobre l’objecte. 

 -**vista \"tree\" d’un objecte** *f* Vista arbre/llista que distribueix la pantalla en línies amb l’objectiu de facilitar la visualització i/o l’edició d’un conjunt de recursos de  l’objecte. La majoria de les vistes arbre/llista són només de  visualització, però OpenObject permet fer-les editables. La vista arbre  mostra els recursos de l’objecte seguint una estructura jeràrquica,  mentre que la vista llista mostra els recursos en seqüència, sense cap  jerarquia. 