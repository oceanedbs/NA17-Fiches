
# NA17 - Fiche : CONCEPTION DE DONNEES RELATIONELLES

## L'héritage

**héritage :** transmission des propriété d'une classe à l'autre, permet de factoriser les classes. N'a pas de verbe associé à l'association, oralement on peut dire "est un"

**classe abstraite** classe non instanciable, n'a de sens que si une autre classe en hérite. Elle correspond à un groupe général de classes (*ex : mamifères*)

**héritage complet :** les classes filles n'ont aucunes caractéristiques qui leurs sont propres. 

**héritage exclusif :** l'objet instancié appartiet à une seule des classes hérités.

**héritage non exclusif :** un objet peut appartenir aux 2 clases héritées. 

**héritage multiple :** une classe fille peut ériter de plusieurs de plusieurs classes mères 
ATTENTION : toujours justifier l'utilisation de l'héritage multiple

On peut transformer un héritage en associations : 1:1 --- 0:1 ou 1:1 --- 1:1

## Transformation de l'héritage en relationel

**Transformation de l'héritage**
- référence entre la classe mère et la classe fille
*Classe1(#a,b), Classe2(#a=>Classe1,c,d) avec c KEY, Classe3(#a=>Classe1,e,f) avec e KEY*
- héritage par les classes filles
*Classe2(#a,b,c,d) avec c KEY, Classe3(#a,b,e,f) avec e KEY*
- héritage par la classe mère
*Classe1(#a,b,c,d,e,f,t:{1,2,3}) avec c UNIQUE et e UNIQUE*
<img src="heritage.png" width="200" height="200" />
[drawing](heritage.png)

**Comment choisir le type de transformation de l'héritage**
Si l'héritage est complet : transformation par la classe mère
    Si la classe mère est abstraite :
    Classe1(#a,b,t:{2,3})
    Si la classe mère n'est pas abstraite :
    Classe1(#a,b,t:{1,2,3}) 




