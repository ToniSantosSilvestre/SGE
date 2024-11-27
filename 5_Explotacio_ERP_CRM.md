---
title: UD05: Explotació de sistemes ERP-CRM
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
Odoo és un ERP-CRM de codi obert que es distribueix sota dos tipus de desplegament:

- On-premise en GNU/Linux o Windows amb dues versions (Community, gratuïta i Enterprise, de pagament).
- SaaS (Programari As A Service): l’empresa que desenvolupa Odoo també proporciona el seu servei en el núvol. 

D'aquesta manera, una empresa pot tenir el seu propi Odoo en un servidor local, en un núvol propi o en un núvol de tercers. També pot tenir accés a Odoo pel SaaS d'Odoo o d'altres terceres empreses que proporcionen Odoo com SaaS.

La llicència d'Odoo ha anat canviant al llarg del temps. La llicència actual, de la versió 18 'Community' és LGPLv3.

Odoo té una arquitectura “client-servidor” de 3 capes:

- La base de dades en un servidor PostgreSQL.
- El servidor Odoo, que engloba la lògica de negoci i el servidor web.
- La capa de client que és un SPA (Single Page Application). La capa client està dividida en almenys 3 interfícies molt diferenciades:
    - El “Backend” on s'administra la base de dades per part dels administradors i empleats de l'empresa.
    - El “Frontend” o pàgina web, on poden accedir els clients i empleats. Pot incloure una botiga i altres aplicacions.
    - El “TPV” per als terminals punt de venda que poden ser tàctils.

> 💬 **Atenció**: a més d'usar el seu propi client, Odoo admet que altres aplicacions interactuen amb el seu servidor usant XML-RPC. També es poden desenvolupar “web controllers” per a crear una API per a aplicacions web o mòbils, per exemple.

A part de l'arquitectura de 3 capes, Odoo és un sistema modular. Això vol dir que es pot ampliar amb mòduls de tercers (oficials o no) i mòduls desenvolupats per nosaltres mateixos.

De fet, en Odoo hi ha un mòdul “base” que conté el funcionament bàsic del servidor i a partir d'ací es carreguen tots els altres mòduls.

Quan instal·lem Odoo, abans d'instal·lar cap mòdul, tenim accés al “backend” on gestionar poc més que les opcions i usuaris. És necessari instal·lar els mòduls necessaris per a un funcionament mínim. Per exemple, el més típic és instal·lar almenys els mòduls de vendes, compres, CRM i comptabilitat.

Per a ampliar les funcionalitats o adaptar Odoo a les necessitats d'una empresa, no cal modificar el codi font d'Odoo. Tan sols necessitem crear un mòdul.

Els **mòduls d'Odoo** poden modificar el comportament del programa, l'estructura de la base de dades i/o la interfície d'usuari. En principi, un mòdul es pot instal·lar i desinstal·lar i els canvis que implicava el mòdul es reverteixen completament.
<imatge>
Odoo facilita el desenvolupament de mòduls perquè, a més d'un ERP, és un framework de programació. Odoo té el seu propi framework tipus **RAD (Rapid Application Development)**. Això significa que amb poc esforç es poden aconseguir aplicacions amb altes prestacions i segures.

>❕**Atenció**: el poc esforç és relatiu. Per a desenvolupar correctament en Odoo són necessaris amplis coneixements de Python, XML, HTML, Javascript i altres tecnologies associades com QWeb, JQuery, XML-RPC, etc. La corba d'aprenentatge és alta i la documentació és escassa. A més, els errors són més difícils d'interpretar perquè no sabem tot el que està passant per davall. La frustració inicial es veurà compensada amb una major agilitat i menys errors.

Aquest framework es basa en alguns dels principis generals dels RAD moderns:

- La capa **ORM (Object Relational Mapping)** entre els objectes i la base de dades.
    - La combinació **Classe Python ↔ ORM ↔ Tabla PostgreSQL** es coneix com a **Model**.
    - El programador no efectua el disseny de la base de dades, només de les classes i les seues relacions.
    - Tampoc és necessari fer consultes SQL, quasi tot es pot fer amb els mètodes d'ORM d'Odoo.
- L’arquitectura **MVC** (Modelo-Vista-Controlador).
    - El model es programa declarant classes de Python que hereten de “**models.Model**”. Aquesta herència provoca que actue l'ORM i és mapejen en la base de dades.
    - Les vistes es defineixen normalment en arxius XML i són llistes, formularis, calendaris, gràfics, menús, etc. Aquest XML serà enviat al client web on el framework Javascript d'Odoo ho transforma en HTML.
    - El controlador també es defineix en fitxers Python, normalment al costat del model. El controlador són els mètodes que proporcionen la lògica de negoci.
- Odoo té una arquitectura de **Tinença Múltiple**. De manera que un únic servidor pot proporcionar servei a molts clients de bases de dades diferents.
- Odoo proporciona un dissenyador d'informes.
- El framework facilita la traducció de l'aplicació a molts idiomes.

> 📖 **Important**: ja que Odoo facilita la traducció, és una bona pràctica programar tot en anglés, tant el nom de les variables com els textos que vam mostrar als usuaris. Posteriorment, podem afegir les traduccions necessàries.



## 2 La base de dades d'Odoo

Gràcies a l'ORM, no hi ha un disseny definit de la base de dades. La base de dades d'una empresa pot tenir algunes taules molt diferents d’altres en funció del mapatge que l'ORM haja fet amb les classes actives en aquesta empresa. Per tant, és difícil trobar un disseny “entitat-relació” o una cosa similar en la documentació d'Odoo.

Cal afegir que Odoo té alguns models ja creats i ben documentats com:
- “res.partner” (clients, proveïdors, etc.).
    - https://www.technaureus.com/odoo-partner-res-partner-concept/
- “sale.order” (Ordre de venda).

Aquests models existeixen de base pel fet que estan en quasi totes les empreses i versions d'Odoo.

Però ni tan sols aquests tenen en la base de dades les mateixes columnes o relacions que en altres empreses. Moltes vegades necessitem saber el nom del model, del camp o de la taula en la base de dades. Per a això, Odoo proporciona en el seu “backend” el “mode desenvolupador” per a saber el model i camp posant el ratolí damunt d'un camp dels formularis.

> 📖 **Important**: el nom de les classes de Python sempre ha de ser en minúscula i amb el  punt per a separar per jerarquia. El nom d'un model, per tant, serà  sempre: “modul.model”. Si el model té un nom compost, se separa per “_”.

> En la base de dades, el punt se substitueix per una barra baixa.



> 💬 **Interessant**: aconsellem dedicar uns minuts a conéixer la base de dades usant el “mode  desenvolupador” i el client de terminal de PostgreSQL. Per a això, podem repassar les consultes SQL traient, per exemple, el nom dels clients  que no han fet cap comanda.

## 3. Composició d'un mòdul

Odoo és un programa modular. Tant el servidor com el client es componen de mòduls que estenen al mòdul “base”. Qualsevol cosa que es vulga modificar en Odoo s'ha de fer creant un mòdul.