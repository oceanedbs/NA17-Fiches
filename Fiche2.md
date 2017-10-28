
# NA17 - Fiche : CONCEPTION DE DONNEES RELATIONELLES

## L'héritage

**héritage :** transmission des propriété d'une classe à l'autre, permet de factoriser les classes. N'a pas de verbe associé à l'association, oralement on peut dire "est un"

**classe abstraite** classe non instanciable, n'a de sens que si une autre classe en hérite. Elle correspond à un groupe général de classes (*ex : mamifères*)

**héritage complet :** les classes filles n'ont aucunes caractéristiques qui leurs sont propres. Elles ont les même attributs

**héritage presque complet :** les classes filles ont le même nombre d'attributs et aucune autre association leur est lié. 

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
Si _l'héritage est complet_ : transformation par la classe mère
- Si la classe mère est abstraite :
    Classe1(#a,b,t:{2,3})
- Si la classe mère n'est pas abstraite :
    Classe1(#a,b,t:{1,2,3}) 
Si _l'héritage est non compet, que la classe mère est abstraite_ et sans associations, héritage par les classes filles :
Classe2(#a,b,c,d) avec c KEY
Classe3(#a,b,e,f) avec e KEY

Si _l'héritage est non complet et que la classe mère est non abstraite_ et sans associations héritage par référence : 
Classe1(#a,b)
Classe2(#a,b,c,d) avec c KEY
Classe3(#a,b,e,f,fka=>Classe2) avec e KEY 

Si _l'héritage est presque complet_ on peut transformer par la classe mère :
Classe1(#a,b,c,d,e,f,t:{1,2,3})

**Cas problématiques**
- association sur la classe mère et héritage par les classes filles :
Classe2(#a,b,c,d) avec c KEY
Classe3(#a,b,e,f) avec e KEY
Classe4(#g,h,fka=>Classe2, fkb=>Classe3)
Contrainte : fka OR fkb
- héritage non complet par la classe mère (association M:N ou 1:N sur une classe fille)
Classe1(#a,b,c,d,e,f,t:{1,2,3})
Classe4(#g,h,fka=>Classe1)
Contraintes : Classe4.fka ne référence que des enregistrements tels que Classe1.t=3

-héritage non complet par la classe mère (et association entre les classes filles)
Classe1(#a,b,c,d,e,f,fka=>Classe1,t:{1,2,3})
Contraintes : fka ne référence que des enregistrements tels que t=2 ; si fka alors t=3


ATTENTION : un héritage non exclusif ne doit jamais être traité par les classes filles. 


## Implémentation d'une base de donnée dans Postgres

=> voir feuille papier

## Algèbre relationelle


