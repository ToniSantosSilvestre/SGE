---
title: Projecte d'SGE.
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

## 1. DESENVOLUPAMENT DEL REPTE

### 1.1 Plantejar i identificar repte:

**Explicació del repte**:

L'Associació de Sant Jordi ens ha contractat perquè li resolguem la següent problemàtica referent a les filaes:

**Problemàtica**:

Cada vegada hi ha més complexitat a l'hora de gestionar les filaes i es vol oferir un paraigües unificat que gestione els llistats oficials i les aportacions a compte (montepios) que realitzen els festers al llarg de l'any.

El vostre treball és resoldre aquesta problemàtica mitjançant software a mida (aplicació mòbil i mòduls per a ERP) de forma que no només solucionen la problemàtica proposada, sinó que també siga usable i útil per agilitzar aquest procediment a l'Associació.
Els fitxers generats hauran de treballar i emmagatzemar la informació en un repositori de GitHub privat d’un dels membres de l’equip creat especialment per al repte.

Necessitem crear una classe "**Sòcies**" que herete de **res.partner** i que incloga els següents camps si no estan ja:

- Data_Naixement: Data

Al mateix temps tindrem, d'una classe "**Filaes**" que també hereten de **res.partner** amb els següents camps:

- Any Fundació: Data
- Nombre components: camp calculat amb el sumatori de tots els actius, jovenils, honoraris i socials que es guarden al model d'històric

Per altra banda, cal disposar d'una classe "**Històric**" que gestione les altes i baixes a les diferents filaes. Cal tindre en compte que una persona pot ser sòcia de diferents filaes al mateix temps. Dins dels seus camps, podem trobar:

- DNI_Soci_ids: camp relacionat amb "socies"

- Nom_Fila_ids: camp relacionat amb "filaes"

- Acció: Alta o Baixa

- Data_Acció_Alta_Baixa

- Certificat_minusvalidesa: de tipus Image amb la captura del document acreditatiu si és procedent

- Condició: Camp calculat que es guardar en taula i és un camp calculat que ha de disposar de les següents ítems:

  - Jovenil: Persona activa menor de 18 anys
  - Actiu: Persona activa major de 18 anys
  - Baixa: Persona no sòcia
  - Honorari: Persona activa major de 70 anys i estada de més de 30 anys en la filà en còmput global
  - Social: Si disposa de Certificat_minusvalidesa

- Antiguitat: Camp calculat guardat al model on es suma el temps total d'eixa persona quan ha estat activa a la filà.

  Cal disposar d'un mètode que controle que no es pot donar d'alta a una filà un soci ja actiu i que no es pot donar de baixa un soci que ja no pertany a la filà.

En últim terme, hi haurà un model "**montepios**" amb les següents dades:

- DNI_Soci: camp relacionat amb "socies"
- Nom_Fila: camp relacionat amb "filaes"
- Aportació: Flotant
- Data_Aportació: Data

Caldrà validar que el soci no està de baixa abans de fer qualsevol tipus d'aportació.

Les vistes de "Socies" i "Filaes" inclouran les vistes Tree, Kanban i Form mentre que la d'Històric inclourà les vistes Tree i Form. A banda, la vista de Filaes, mostrarà una vista Graph comparativa del nombre de components de les files.

Caldrà mostrar un **informe** amb el llistat ordenat de cada filà i el sumatori de montepios que han realitzat. El camp primari d'ordenació serà la data d'inscripció i el secundari la data de naixement en format ascendent i es lliurarà amb un títol amb el nom de la filà i el nom dels diferents membres ordenats per números.

A més a més, hi haurà **dos controladors web**: un que filtrarà els socis per filaes i condició passant estos paràmetres per JSON i després un altre que passat per paràmetre un DNI, una filà i un any, retorne el conjunt de montepios realitzats en eixe any. 

### 1.2 Crear i activar equip:

**Creació d'equip:**
Es realitzarà per parelles identificant les tasques que cadascun dels membres ha realitzat dins del projecte.

### 1.3 Execució d'accions

En aquesta fase es desenvoluparan les accions necessàries per a resoldre el repte i generar els fitxers i manuals necessaris. El professorat ja haurà proporcionat la rúbrica tècnica.

● A lliurar:

Solució al repte plantejat. Hauran de lliurar-se tant els fitxers generats, els
documents generats i tot el necessari als repositoris de Docker Hub i GitHub per
tal que el professor puga replica la solució proposada.

### 1.4 Exposició de resultats

Amb l'objectiu de compartir i valorar l'experiència, cada equip prepararà un vídeo amb
presentació en format PechaKucha (20 diapositives per 20 segons) on han d'intervenir tots els membres de l'equip i que ha de recollir:

- Com s'ha implementat la solució tècnica per resoldre el repte:
- Què tecnologies s'han utilitzat.
- Quins passos s'han seguit per implantar la solució tècnica.
- Quines dificultats han aparegut.
- Idees per utilitzar l'aprés en altres mòduls.
- Propostes de millora futures.
- Com ha estat l'experiència de treball en equip:
- Han sorgit dificultats?
- Com s'ha solucionat?
- Ha resultat satisfactòria per a tots i totes les components de l'equip?
- Què destacaries en positiu?
- Què destacaries en negatiu?

S'exposarà el resultat i el professorat i altres alumnes realitzaran aportacions.
La data màxima de lliurament codi, documents i vídeo serà el **dijous 13 de febrer a les 17:40 hores.**
A lliurar: material creat per al repte i entrega de la presentació i vídeo explicatiu.

## 2. AVALUACIÓ DE RESULTATS

### 2.1. Qualificació obtinguda

L'avaluació dels resultats es realitzarà tant a nivell d'equip com individual. L'avaluació tindrà un repartiment de pesos igual o semblant al següent:

- AVALUACIÓ A NIVELL D'EQUIP

  - Resultats tècnics de l'equip (70%)
    - El professorat avalua la presentació final del repte (5%)
    - El professorat avalua la part tècnica final del repte (65%)

- AVALUACIÓ A NIVELL INDIVIDUAL

  - Competències transversals (30%)
    - Cada membre és avaluat pel company de grup (10%)
    - el professorat avalua a cada alumne (20%)

  **Consideracions finals:**

● Cada alumne ha d'aprovar tant l’avaluació grupal com l’avaluació individual per aprovar el repte. Si no s'aprova alguna part, no podrà obtenir una nota superior a 3.
● L'alumnat que tinga un 15% o més de faltes injustificades durant el repte, no podrà
obtenir una nota superior a 3.
● L'alumnat que incompleix greument normes referides a la feina en equip (bon clima,
còpia, etc.) podrà perdre el dret a avaluació contínua.
NOTA: L'avaluació que el professorat realitzarà respecte de les competències transversals serà realitzada a partir de les evidències recollides en relació amb: faltes d’assistència, conductes inadequades, bones pràctiques, puntualitat, treball en equip, implicació i compromís.

### 2.2. Prova de validació

Per a tota la gent que haja aconseguit una nota superior a 3 amb les indicacions de l'apartat 2.1, el professorat podria indicar la possibilitat de passar a una prova de validació del repte, per tal de valorar la transmissió de continguts.
El professorat planteja una prova escrita per a comprovar que cada individu ha obtingut els
coneixements esperats en el repte. La prova tindrà una valoració d'APTE/NO APTE.
Una vegada obtinguda aquesta qualificació:
● **APTE**: en el cas de superar aquesta prova, es validarà la nota del repte.
● **NO APTE**: en aquest cas, l'alumne tindrà una última oportunitat de validar la nota del
repte, demostrant els seus coneixements del repte en una entrevista personal amb el
professorat. Si supera aquesta entrevista personal, validarà la nota del repte. En cas
contrari, no podrà obtenir una nota superior a 3.
