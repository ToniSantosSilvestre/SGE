---
title: UD04: Adequació de sistemes ERP-CRM
language: VAL
author: Toni Santos Silvestre [https://github.com/ToniSantosSilvestre]
subject: Sistemes de Gestió Empresarial
keywords: [SGE, 2024, Sistemes de Gestió Empresarial,Python]
IES: CIPFP Batoi (Alcoi) [https://portal.edu.gva.es/cipfpbatoi/]
header: ${title} - ${subject} (ver: ${today})
footer:${currentFileName}.pdf - ${author} - ${IES} - ${pageNo}/${pageCount}
typora-root-url:${filename}/../
typora-copy-images-to:${filename}/../assets
---

[TOC]

## 1. INTRODUCCIÓ
En les situacions d'aprenentatge anteriors s'explica com instal·lar Odoo, tant amb una configuració pensada per a un entorn de producció com una configuració pensada per a un entorn de desenvolupament. En aquesta unitat insistirem un poc més en la configuració de l'entorn de desenvolupament, incloent-hi tant el mateix Odoo, com l'IDE de desenvolupament amb els seus respectius “plugins”. Amb tot això llest, farem els nostres primers mòduls d’Odoo

### 1.1 Com orientarem aquesta unitat?
En primer lloc, prepararem tot l'entorn de desenvolupament. Amb un sistema ERP Odoo instal·lat, es poden desenvolupar mòduls que amplien la seua funcionalitat sense una gran preparació de l'entorn. Tan sols una terminal i un editor de text són suficients per a poder desenvolupar amb Odoo.

No obstant això, es recomana realitzar una configuració prèvia tant del mateix sistema ERP Odoo com de les eines de desenvolupament associades per fer la feina més fàcil i augmentar la productivitat.

Una vegada configurat l'entorn de desenvolupament, començarem a introduir els primers mòduls d’Odoo. Començarem amb un senzill mòdul "que no fa res", però que ja es pot instal·lar. Aquest mòdul ens ajudarà a validar si tenim una configuració correcta del nostre entorn de desenvolupament.

A continuació ampliarem el mòdul base anterior, afegint coses per augmentar la seua funcionalitat. Aquesta serà la metodologia que seguirem en aquesta unitat d'introducció al desenvolupament de mòduls.

El desenvolupament de mòduls d’Odoo pot arribar a ser molt complex i només els programadors experts són capaços d'aprofundir des del principi sense veure com va funcionant. En la següent unitat ja aprofundirem en major detall en la programació de mòduls per Odoo.



## 2. Creant un directori per a mòduls

Com ja vam veure en les unitats anteriors, és important tenir un directori per incloure i desenvolupar mòduls en Odoo. En aquest apartat comentarem com posar en marxa aquest directori tant en una instal·lació manual com utilitzant Docker.

### 2.1 Instal·lació manual
Si hem fet una instal·lació manual tal com es va explicar en les unitats anteriors, un script per aconseguir crear aquest directori a la carpeta "/var/lib/Odoo/modules" és:

>// Estant situat en /var/lib/odoo:
// Creem directori “modules”
mkdir modules
// Creem un módul anomenat “prova” amb la utilitat “odoo scaffold”
odoo scaffold prova ./modules
// Modifiquem el path dels “addons”.
odoo --addons-path="/var/lib/odoo/modules,/usr/lib/python3/dist-packages/odoo/addons" --save
// Llancem el servidor Odoo i actualitzem el módul “prova” en la bd “empresa”
odoo -u prova -d empresa

Amb aquesta acció, el que aconseguim és afegir el nostre directori "modules" al PATH d’Odoo (emmagatzemat a l'arxiu de configuració "**.odoorc**", situat al “home” de l'usuari Odoo). Amb l'últim comandament hem arrancat Odoo actualitzant aquest mòdul ( "prova") a la base de dades "empresa".

Els mòduls han de poder ser almenys llegits per l'usuari "Odoo", que és el que llança el servei:
- En un entorn de producció, els permisos dels mòduls solen configurar-se de manera que només l'usuari "Odoo" puga llegir-los i cap altre usuari puga llegir ni escriure.
- En un entorn de desenvolupament, és recomanable que el propietari siga el mateix "Odoo" i tinga permisos d'escriptura per fer els canvis necessaris.

### 2.2 Instal·lació mitjançant Docker i Docker Compose

Si poseu en marxa Odoo en mode desenvolupament amb Docker i Docker  Compose, tal com era suggerit a les unitats anteriors, simplement tindreu el  vostre directori de mòduls llest per treballar. Aquest directori és  l'anomenat **volumesOdoo/addons**", que tindreu mapejat en la vostra màquina amfitriona.

## 3 Entorn de desenvolupament

Hi ha diversos entorns de desenvolupament que permeten desenvolupar mòduls per Odoo. Els més utilitzats són "Visual Studio Code" i "PyCharm". A més és important fer servir algunes eines addicionals. Recomanem en el desenvolupament usar un sistema de control de versions "git" juntament amb plataformes com [https://github.com](https://github.com) o [https://gitlab.com](https://gitlab.com).

### 3.1 Visual Studio Code

Recomanem l'ús de Visual Studio Code. És molt potent i posseeix un gran ecosistema de “plugins” per ampliar la seua funcionalitat [https://code.visualstudio.com/](https://code.visualstudio.com/) 

Ací alguns manuals lliures d'ús de Visual Studio Code en castellà:
[http://www.mclibre.org/consultar/informatica/lecciones/](http://www.mclibre.org/consultar/informatica/lecciones/)

[http://www.mclibre.org/consultar/informatica/lecciones/vsc-instalacion.htmlVSC-personalizacion.html](http://www.mclibre.org/consultar/informatica/lecciones/vsc-instalacion.htmlVSC-personalizacion.html) 

Per al desenvolupament amb Odoo, es recomanen els següents
- Python: [https://marketplace.visualstudio.com/items?itemName=ms-python.python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- Odoo-snippets: [https://marketplace.visualstudio.com/items?itemName=jeffery9.odoo-snippets](https://marketplace.visualstudio.com/items?itemName=jeffery9.odoo-snippets) 

### 3.2 Control de versions usant Git + Visual Studio Code
Git és un sistema de control de versions. El seu ús en l'entorn professional està molt estés i és
utilitzat en tota mena de desenvolupaments. Durant el curs, s'utilitzaran repositoris Git tant per al lliurament de pràctiques com per facilitar disposar d'un repositori amb control de versions.

Per instal·lar Git:

- Ubuntu:
    sudo apt-get update    
    sudo apt-get install git
- Windows: https://git-for-windows.github.io/ 

Per facilitar la tasca de l'ús de Git és recomanable instal·lar alguna extensió o entorn que us facilite el seu ús. Per fer servir Git en Visual Studio Code recomanem el següent connector  [https://marketplace.visualstudio.com/items?itemName=donjayamanne.git-extension-pack](https://marketplace.visualstudio.com/items?itemName=donjayamanne.git-extension-pack).

Pots trobar més informació de com fer servir Git amb Visual Studio Code a:
- [https://code.visualstudio.com/docs/editor/versioncontrol](https://code.visualstudio.com/docs/editor/versioncontrol)
- [http://www.mclibre.org/consultar/informatica/lecciones/vsc-git-repositorio.html](http://www.mclibre.org/consultar/informatica/lecciones/vsc-git-repositorio.html) 

### 3.3 PyCharm

Un altre editor molt recomanat en Pycharm [https://www.jetbrains.com/es-es/pycharm/](https://www.jetbrains.com/es-es/pycharm/ ) 
Per defecte no reconeix els elements del framework Odoo, però sí els del llenguatge Python. 
Si volem facilitar el desenvolupament podem instal·lar l'extensió d’Odoo Pycharm Templates [https://github.com/mohamedmagdy/odoo-pycharm-templates](https://github.com/mohamedmagdy/odoo-pycharm-templates) .

### 3.4 Control de versions usant Git + PyCharm

PyCharm també permet l'ús d'un sistema de control de versions Git des del seu entorn. Podeu trobar informació de com utilitzar Git amb Pycharm a:
- [https://programmerclick.com/article/169045515/](https://programmerclick.com/article/169045515/)
- [https://www.jetbrains.com/help/pycharm/set-up-a-git-repository.html](https://www.jetbrains.com/help/pycharm/set-up-a-git-repository.html)

## 4 Activant el mode “desenvolupador” en Odoo 17

En aquest URL de la guia de Odoo 17 s'expliquen les diferents vies existents per activar el mode desenvolupador. Aquesta manera ens permet depurar els nostres mòduls Odoo gràficament.

[https://www.odoo.com/documentation/17.0/es/applications/general/developer_mode.html](https://www.odoo.com/documentation/17.0/es/applications/general/developer_mode.html)

Qualsevol de les explicades (interfície Odoo, url, extensió navegador) és igualment vàlida per a aquest fi, encara que si feu un desenvolupament exhaustiu és possible que la més còmoda siga l'activació mitjançant una extensió de navegador.

Podeu trobar l'extensió per:
- Firefox: [https://addons.mozilla.org/es/firefox/addon/odoo-debug/](https://addons.mozilla.org/es/firefox/addon/odoo-debug/)
- Chrome:[ https://chrome.google.com/webstore/detail/odoo-debug/hmdmhilocobgohohpdpolmibjklfgkbi?hl=es_PR](https://chrome.google.com/webstore/detail/odoo-debug/hmdmhilocobgohohpdpolmibjklfgkbi?hl=es_PR)
