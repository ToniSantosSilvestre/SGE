---
title: UD06: Desenvolupament de mòduls d'Odoo: Controlador, Herència i Web Control.
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

## 1. Controlador
Odoo té una arquitectura MVC (Model-Vista-Controlador) que ens permet desenvolupar cadascuna d'aquestes parts per separat. No obstant això, és habitual que el controlador es desenvolupe en els mateixos fitxers Python en els quals es fa el model.

Per a aclarir, podríem dir que el controlador són els mètodes que hi ha en els models.

En la unitat anterior hem vist els “fields” computats i com funcionen les funcions en Python i Odoo. En aquest apartat veurem les facilitats que proporciona el framework d'Odoo per a manipular l'ORM (Object Relational Mapping).

> ❕ **Atenció**: llegats a aquest punt, se suposa que hi ha un nivell mínim de coneixements de programació i del llenguatge de programació Python. 



La capa ORM té uns mètodes per a manipular les dades sense necessitat de fer sentències SQL contra la base de dades.

> 💬 **Interessant**: Odoo té una eina per a accedir per terminal en comptes de per la web. Per a  això hem d'escriure en la terminal quan reiniciem el servidor: “odoo  shell”.
>

> L'accés a la terminal  ens permet provar les instruccions de l'ORM sense haver d'editar arxius i reiniciar el servidor. Quan en aquest capítol vegem exemples de codi de l'estil:
>

> **\>>> print(self)**

> Indica que s'han fet en la terminal d'Odoo i que seria interessant fer-ho per a provar el seu funcionament.
>



Per a Odoo, un conjunt de registres d'un model es diu “Recordset” i un  conjunt amb un sol registre d'un model és un “Singleton”. La interacció  amb l'ORM es basa a manipular “recordsets” o recórrer-los per a anar  manipulant els “singletons”. 

```python
def do_operation(self):
    print self # => a.model(1, 2, 3, 4, 5) (Recordset)    
    for record in self:      
        print record # => a.model(1), a.model(2), a.model(3), ... (Singletons)
```

Recordem que per a accedir a les dades, cal anar als “singletons” i no als “recordsets”.

```python
>>> a 
school.course(1, 2) 
>>> for i in a: 
...  i.name 
... 
'2DAM' 
'1DAM' 
>>> a.name ValueError: too many values to unpack
```

Si s'intenta accedir a les dades en un “recordset” dona error. Les dades  dels “fields” relacionals donen un “recordset”, fins i tot encara que  només tinguen un element:

```python
>>> a[0].students 
res.partner(14, 26, 33, 27, 10)
```

Els “recordsets” són iterables com una llista/array i tenen, a més,  operacions de conjunts que permeten facilitar el treball amb ells:

- **record in set**:  retorna True si “rècord” està en el conjunt (set).
- **set1 | set2**: unió de conjunts (sets). També funciona el signe +.
- **set1 & set2**: intersecció de conjunts (sets).
- **set1 - set2**:  diferència de conjunts (sets).

A més, compta amb funcions pròpies de la programació funcional:

**filtered()**

Retorna un “recordset” amb els elements del “recordset” que passen el filtre.  Per a passar el filtre, es necessita que retorne un True, siga una  funció Lambda o un “field” Booleà. Similar a “filter”.

```python
records.filtered(lambda r: r.company_id == user.company_id) 
records.filtered("partner_id.is_company")
```

**sorted()**

Retorna un “recordset” ordenat segons el resultat d'una funció Lambda aplicat a la seua “key function”  https://docs.python.org/3/howto/sorting.html#key-functions. Similar a  “sort”.

```python
# sort records by name 
records.sorted(key=lambda r: r.name) 
records.sorted(key=lambda r: r.name, reverse=True)
```

**mapped()**

Li aplica una funció a cada element del recordset i retorna un recordset amb els canvis demanats. Similar a “map”.

```python
# returns a list of summing two fields for each record in the set 
records.mapped(lambda r: r.field1 + r.field2) 
# returns a list of names 
records.mapped('name') 
# returns a recordset of partners 
record.mapped('partner_id') 
# returns the union of all partner banks, with duplicates removed record.mapped('partner_id.bank_ids')
```


![Model de classe d'Odoo](/assets/imatges/05_02_classe_model.png)

Sobre el codi anterior, vegem detalladament tot el que passa:

- Es defineix una classe de Python que hereta de “**models.Model**”
- Es defineixen dos atributs “**_name**” i “**_description**”. El “**_name**” és obligatori en els models i és el nom del model. Ací s'observa l'abstracció, ja no s'accedirà a la classe “**Amodel**”, sinó al model “**a.model**”.
- Després està la definició d'un altre atribut tipus “**field**” que serà mapatge per l'ORM en la base de dades. Com es pot observar, crida al constructor de la classe “**fields.Char**” amb uns arguments. Tots els arguments són opcionals en el cas de “**Char**”. Hi ha constructors per a tots els tipus de dades.

> 💬 **Interessant**: és molt probable que a hores d'ara no entengues el perquè de la majoria  del codi anterior. Els frameworks requereixen entendre moltes coses  abans de poder començar. No obstant això, amb aquest fragment de codi ja tenim solucionat l'emmagatzematge en la base de dades, la integritat de les dades i part de la interacció amb l'usuari.

> 💬 **Interessant**: Odoo està pensat perquè siga fàcilment modificable per la web. Sense  necessitat d'entrar al codi. Això és molt útil per a prototipar les  vistes, per exemple.
> Una de les  funcionalitats és la manera desenvolupador, que permet, entre moltes  altres coses, explorar els models que té en aquest moment el servidor. 

Els models tenen alguns atributs del model, com “**_name**” o “**_description**”. Un altre atribut de model important és “**_rec_name**” que indica que atribut pren nom el registre i que per defecte apunta a l'atribut “name” (no confondre amb “_name”).

- En les vistes (que veurem més endavant), en alguns camps es basa en l'atribut marcat per “**_rec_name**”, que per defecte és “**name**”. Si no tenim un atribut “name” o volem que siga un altre atribut el que de nom, podem modificar-ho amb “**_rec_name=’nomatribut**’”.



 ### 4.2 Atributs tipus “field” simples

Els models tenen altres atributs tipus “field”, que es mapejen en la base  de dades i als quals l'usuari té accés i mètodes que conformen el  controlador. A continuació detallarem tots els tipus de “field” que hi  ha i les seues possibilitats:

En primer lloc, definim els “fields” de dades més habituals:

- **Integer**
- **Char**
- **Text**
- **Date**
- **Datetime**
- **Float**
- **Boolean**
- **Html**
- **Binary**: arxius binaris que guarda en format base64. Poden guardar-se imatges o  altres elements. Abans d'Odoo 13 en aquest tipus de “fields” es  guardaven les imatges.

Dins dels “fields” de dades, hi ha alguns una mica més complexos:

- **Image**: a partir de la versió 13 d'Odoo es poden guardar imatges en aquest  “field”. Cal definir el “max_width” o “max_height” i es redimensionarà  en guardar. 
- **Selection**: guarda una dada, però cal dir-li amb una llista de tuples les opcions que té.

Ací un exemple de “Selection”:

```python
type = fields.Selection([('1','Basic'),('2','Intermediate'),('3','Completed')]) 

aselection = fields.Selection(selection='a_function_name') # se puede definir su contenido en una función.
```

Tots els “fields” esmentats tenen un constructor que funciona de la mateixa  manera que en l'exemple anterior. Poden tenir un nom, un valor per  defecte, o fins i tot pot definir-se el seu contingut mitjançant una  funció.

Al llarg d'aquest text es veuran exemples de com s'han definit “fields” segons les necessitats.

### 4.3 Atributs “fields” relacionals

A continuació, observarem els “fields” relacionals. Atés que l'ORM evita  que hàgem de crear les taules i les seues relacions en la base de dades, quan existeixen relacions entre models es necessiten uns camps que  definisquen aquelles relacions.



**Exemple**: una comanda de venda té un client i un client pot fer moltes comandes de  venda. Al seu torn, aquesta comanda té moltes línies de comanda, que són només d’aquesta comanda i tenen un producte, que pot estar en moltes  línies de venda.



En situacions com la de l'exemple, aquestes relacions acaben estant en la  base de dades amb claus alienes. Però amb els frameworks que implementen ORM, tot això és molt més senzill.

Per a això utilitzarem els “fields” relacionals d'Odoo:

- **Many2one**: és el més simple. Indica que el model en el qual està té una relació  molts a un amb un altre model. Això significa que un registre té relació amb un únic registre de l'altre model, mentre que l'altre registre pot  tenir relació amb molts registres del model que té el “Many2one”. En la  taula de la base de dades, això es traduirà en una clau aliena a l'altra taula.
    - Exemple on es pretén que cada ciutat emmagatzeme el seu país.
    ![Exemple de relació Many2One](/assets/imatges/05_03_relacio_many2one.png)



## 7. Mòduls d'exemple amb comentaris

Es poden trobar exemples de mòduls d'Odoo comentats amb els conceptes tractats durant la unitat en [https://github.com/sergarb1/OdooModulosEjemplos](https://www.google.com/url?q=https://github.com/sergarb1/OdooModulosEjemplos&sa=D&source=editors&ust=1726775625798493&usg=AOvVaw3lgNw3WtiorbJh5MAKaG5t)



## 8. Activitats

### Activitat 01

Modifica l’exemple més senzill de la llista de tasques de forma que:

- Tinga una nova vista per veure les tasques en format “Kanban”.
- Modifica les tasques per tindre una data assignada i crea una nova vista per veure en una vista “Calendar” la data assignada.

### Activitat 02

Amplia el mòdul de l’exemple de biblioteca de còmics de forma que:

- Incloure la possibilitat de gestionar socis, emmagatzemar nom, cognom e identificador.
- Introduïu la possibilitat que hi haja exemplars de còmics per prestar.

- El model de còmic actual ha de servir com a referència de la informació  del còmic. A banda d’aquest model, jaureu de plantejar un nou model per a indicar exemplars de préstec d’eixe còmic. 
- Aquests exemplars de préstec hauran de controlar només a qui estan prestats i  la data d’inici i data de final del préstec. No cal tindre un històric  de préstecs, només qui té el còmic en cada moment, quan se l’ha prestat i la data prevista de tornada.

- La data de préstec no pot ser posterior al dia de hui.
- La data prevista de tornada no pot ser anterior al dia de hui.

### Activitat 03

Crea un mòdul per a gestionar pacients i metges d’un hospital.

Per cada pacient, tindrem un model amb les següents dades:

- Nom i cognoms del pacient.
- Símptomes.

Per cada metge, tindrem un model amb les següents dades:

- Nom i cognoms del metge.
- Número de col·legiat.

Per cada vegada que un metge ha atés un pacient, tindrem un model indicant el diagnòstic.

Un pacient pot haver sigut atés per diversos metges i un metge pot haver atés diversos pacients.

Implementa els models i les vistes que cregues adequades per als 3 models.

### Activitat 04

Fes un mòdul d’Odoo que represente els nostres estudis de cicles formatius a un institut:

- Model Cicle formatiu. Cada instància representa a un cicle formatiu en un institut. Un cicle té un o més mòduls associats-
- Model Mòdul. Cada “mòdul” estarà relacionat amb cicles formatius (al qual  pertany), alumnes matriculats i professor que ho imparteix.
- Model Alumne. Relacionat amb els mòduls que té matriculat.
- Model Professor. Relacionat amb els mòduls que imparteix.

Implementa els models, les relacions necessàries i les vistes que cregues adequades per als 4 models.

Una vegada en funcionament l’aplicació, volem que implementes la següent configuració de seguretat:

- Els usuaris amb el rol “Director” podran modificar els registres dels models anteriors.
- A més del director, els únics usuaris que podran veure les dades dels  professors (en mode lectura) seran els usuaris amb rol “Professor”. 