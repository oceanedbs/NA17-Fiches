

# NA17 - Fiche


## Conception de bases de données en UML


**Attribut multi-évalués et taille max d'un attribut :** prenom[1...3]:string(15)
Un objet de cette relation peut avoir 1 à 3 prénoms de taille max 15 charactères.

**Attribut dérivé :** /Age : integer
Puis dans les méthodes on a Age = Maintenant() - dateNaiss

Ne marquer que les clés évidentes dans le MCD

**méthode :** fonction associée à une classe qui intéragit sur les objets et renvoie des valeurs. 

**Cardinalités :**
- 0,1 = optionel
- 1..1 OU 1 = obligatoirement 1
- 0...n = plusieurs
- 1 ..n = obligatoire

**Classe association :** classe liée à une association 

## Modélisation logique et relationelle

**clé artificielle :**
- minimiser l'ajout de clé artificielle (elles ne figurent pas dans l'UML)
- facilite la maintenance de la BDD
- plus performant car domaine plus optimisé pour une clé artificielle


**MLD :**
- Relation(#attribut1 : domaine1, attribut2 : domaine2 ....)
- clé étrangères : Relation (#attribut1 : domaine1, attribut2 => table(attribut) ...) // L'attribut est précisé dans la clé étrangère si clé de la relation table composée de 2 attribut et fait référence à un seul des 2
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

**LCT :** language de contrôle de transaction
*COMMIT, ROLLBACK**

**types du SQL** : char, varchar, integer, smallint, float, real, double precision, bit, numeric(15,2) *le nombre comporte au plus 15 chiffres significatifs DONT 2 décimales*, date (AAAA-MM-DD), time, timestamp, datetime (AAAA-MM-DD HH:MM:SS), interval (intervalle de date/temps)
ATTENTION : il vaut mieux utiliser décimal qui donne une valeur exacte que float qui donne une valeur approchée. 
ATTENTION : char = longueure fixe, complétée par des espaces, varchar = longueur variable.

**contraintes en SQL :** NOT NULL, PRIMARY KEY(..), UNIQUE(...), FOREIGN KEY (..) REFERENCES Tables(attribut), CHECK(conditions)
Une clé candiadate est donc UNIQUE AND NOT NULL.

**CREATE TABLE** 'nom table' (attribut1 : type1 PRIMARY KEY, attribut2 : type2, attribut3 : type3, ..., FOREIGN KEY (attribut3) REFERENCES table(attribut) );

**INSERT INTO** 'table' (attribut1, attribut2, attribut3, ...) VALUES ('chaine1', 10, 'chaine2' ....); 

**UPDATE** Table SET (attribut3="chaine4", attribut2=4) WHERE (condition);

**DELETE FROM** Table < WHERE condition >

**DROP**  type_de_l'objet  nom_de_l'objet;
**DROP TABLE** Table;
**DROP VIEW** vue;


**ALTER TABLE** table ADD condition attribut;
			DROP nom_attribut;
