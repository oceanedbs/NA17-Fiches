

# NA17 - Fiche : INTRODUCTIONS AUX BASES DE DONNEES RELATIONELLES


## Conception de bases de données en UML

**Clé candidate :** ensemble d’attributs permettant d’identifier un tuple de manière unique

**Attribut multi-évalués et taille max d'un attribut :** prénom[1...3]:string(15)
Un objet de cette relation peut avoir 1 à 3 prénoms de taille max 15 caractère.

**Attribut dérivé :** /Age : integer
Puis dans les méthodes on a Age = Maintenant() - dateNaiss

Ne marquer que les clés évidentes dans le MCD

**méthode :** fonction associée à une classe qui intéragit sur les objets et renvoie des valeurs.
*Rouler (in km:integer) : interger*

**Cardinalités :**
- 0,1 = optionel
- 1..1 OU 1 = obligatoirement 1
- 0...n = plusieurs
- 1 ..n = obligatoire

**Classe association :** classe liée à une association

**Clé étrangère :** `AttributN => Relation2.attr`
```
Personne (#Numero:Entier, Nom:Chaîne, Prénom:Chaîne, LieuNaissance=>Ville)
Pays (#Nom:Chaîne, Population:Entier, Superficie:Réel, Dirigeant=>Personne)
Région (#Pays=>Pays, #Nom:Chaîne, Superficie, Dirigeant=>Personne)
Ville (#CodePostal:CP, Nom:Chaîne, Pays=>Région.Pays, Région=>Région.Nom,
Dirigeant=>Personne)
```


## Modélisation logique et relationelle

**clé artificielle :**
- minimiser l'ajout de clé artificielle (elles ne figurent pas dans l'UML)
- facilite la maintenance de la BDD
- plus performant car domaine plus optimisé pour une clé artificielle

**Attributs**
Attribut | MCD (UML) | $\to$ MLD |
| -------- | --------- | --------- |
| Attribut Composite | ![](https://stph.scenari-community.org/bdd/rel2/res/03attc.png) | `Classe1(#a,b_b1,b_b2)` |
| Attribut Multivalué | ![](https://stph.scenari-community.org/bdd/rel2/res/04attmv.png) | `Classe1(#a)` et `RB(#b,#a=>Classe1)` <br> ou bien `Classe1(#a,b1,b2,b3)`|
| Attribut Composé Multivalué | ![](https://stph.scenari-community.org/bdd/rel2/res/04attmvc.png) | `Classe1(#a)` et `RB(#b_b1,#b_b2,#a=>Classe1)` |
| Attribut dérivés | ![](https://stph.scenari-community.org/bdd/rel2/res/05attd.png) | Pas représenté en MLD

Associations : Compositions
| Composition | MCD (UML) | $\to$ MLD |
| ----------- | --------- | --------- |
| Composition | ![](https://stph.scenari-community.org/bdd/rel2/res/13comp.png) | `Classe1(#a,b)` `Classe2(#c,#a=>Classe1,d)`<br>{local key} est la clé de de la composée |
| Composition et Attribut Composé Multivalué| ![](https://stph.scenari-community.org/bdd/rel2/res/13compAttmvc.png) | `Classe1(#a)` `RB(#b_b1,#b_b2,#a=>Classe1)`  |
| Composition et Attribut Multivalué | ![](https://stph.scenari-community.org/bdd/rel2/res/13compAttmv.png) | `Classe1(#a)` `RB(#b,#a=>Classe1)` |

#### Associations
| Association | MCD (UML) | $\to$ MLD |
| ----------- | --------- | --------- |
| 1:N | ![](https://stph.scenari-community.org/bdd/rel2/res/06a0n.png) | `Classe1(#a,b)` `Classe2(#c,d,a=>Classe1)`|
| N:M | ![](https://stph.scenari-community.org/bdd/rel2/res/07anm0.png) | `Classe1(#a,b)` ,  `Classe2(#c,d)` `Assoc(#a=>Classe1,#c=>Classe2)` |
| 1:1 | ![](https://stph.scenari-community.org/bdd/rel2/res/08a11.png) | `Classe1(#a,b,c=>Classe2) avec c UNIQUE` et `Classe2(#c,d)` ou inverse |
| Classe d'association N:M | ![](https://stph.scenari-community.org/bdd/rel2/res/11cla_ass20-nolocalkey.png) | `Classe1(#a,b)` , `Classe2(#c,d)` `Assoc(#a=>Classe1,#c=>Classe2,e,f)`<br>Peut avoir une `#g {local key}` en plus|
Classe d'association 1:N ou 1:1 : ajouter les attributs à une classe


**MLD :**
- Relation(#attribut1 : domaine1, attribut2 : domaine2 ....)
- clé étrangères : Relation (#attribut1 : domaine1, attribut2 => table(attribut) ...) // L'attribut est précisé dans la clé étrangère si clé de la relation table composée de 2 attribut et fait référence à un seul des 2
Proj(relation, attribut2) est inclus dans Proj(table, attribut)
- clé candiate : Relation(#attribut1 : domaine1, attribut2 : domaine2 ....) avec attribut2 KEY

**Produit carthésien :** Toutes les lignes de R1 sont associés 1 fois à chaque ligne de R2


## Passage UML relationel : associations

**relations 1 : N :** on ajoute la clé étrangère du coté de la cardialité n

**relations n:m :** on créé une nouvelle classe association
*ex : assoc(#a=>classe1, #b=>classe2)*

**relation 1:1 :** on les traite comme des relations 1:N en ajoutant UNIQUE AND NOT NULL (ou directement KEY) sur la clé étrangère (qui devient donc une clé candidate.
Parfois on peut aussi fusionner les 2 relations plutôt que d'introduire une clé étrangère.

**contraintes :**
- *intégrité reférentielle :* on insert dans un attribut faisant référence à une autre classe une valeur non présente dans cette même classe
- *contrainte sur une clé candidate :* on viole l'unicité d'une clé candiadate
- *contraitede non nullité :* attribut ne peut pas être nul et on l'initialise à NULL

## Création et Alimentation de bases de données en SQL

**LDD :** language de définition de données
*CREATE, DROP, ALTER*

**LMD :** language de manipulation de données
*GRANT, REVOKE*

**LCD :** language de contrôle de transaction
*COMMIT, ROLLBACK**

**types du SQL** : char, varchar, integer, smallint, float, real, double precision, bit, numeric(15,2) *le nombre comporte au plus 15 chiffres significatifs DONT 2 décimales*, date (AAAA-MM-DD), time, timestamp, datetime (AAAA-MM-DD HH:MM:SS), interval (intervalle de date/temps)
ATTENTION : il vaut mieux utiliser décimal qui donne une valeur exacte que float qui donne une valeur approchée.
ATTENTION : char = longueure fixe, complétée par des espaces, varchar = longueur variable.

**contraintes en SQL :** NOT NULL, PRIMARY KEY(..), UNIQUE(...), FOREIGN KEY (..) REFERENCES Tables(attribut), CHECK(conditions)
Une clé candiadate est donc UNIQUE AND NOT NULL.

!! Pour une énumération faire nom CHAR(1) CHECK (nom IN {'H', 'G', 'L'})

**CREATE TABLE** 'nom table' (attribut1 : type1 PRIMARY KEY, attribut2 : type2, attribut3 : type3, ..., FOREIGN KEY (attribut3) REFERENCES table(attribut) );

**INSERT INTO** 'table' (attribut1, attribut2, attribut3, ...) VALUES ('chaine1', 10, 'chaine2' ....);

**UPDATE** Table SET (attribut3="chaine4", attribut2=4) WHERE (condition);

**DELETE FROM** Table < WHERE condition >

**DROP**  type_de_l'objet  nom_de_l'objet;
**DROP TABLE** Table;
**DROP VIEW** vue;


**ALTER TABLE** table ADD attribut type; //permet d'ajouter un attribut à une table
			DROP nom_attribut;//supprime un attribut d'une table
			CHANGE attribut nv_nom type;
			MODIFY attribut nv_type;


	**CREATE TYPE** nom_type AS OBJECT (
		  nom_attribut1 type_attribut1,
		  ...
		);

## Exemple

CREATE TABLE Personne (
    N°SS CHAR(13) PRIMARY KEY,
    Nom VARCHAR(25) NOT NULL,
    Prenom VARCHAR(25) NOT NULL,
    Age INTEGER(3) CHECK (Age BETWEEN 18 AND 65),
    Mariage CHAR(13) REFERENCES Personne(N°SS),
    Codepostal INTEGER(5),
    Pays VARCHAR(50),
    UNIQUE (Nom, Prenom),
    FOREIGN KEY (Codepostal, Pays) REFERENCES Adresse (CP, Pays)
);
CREATE TABLE Adresse (
    CP INTEGER(5) NOT NULL,
    Pays VARCHAR(50) NOT NULL,
    Initiale CHAR(1) CHECK (Initiale = LEFT(Pays, 1)),
    PRIMARY KEY (CP, Pays)
);
