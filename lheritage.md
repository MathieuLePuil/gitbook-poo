# L'héritage

L'héritage est un pilié essentiel de la programmation orientée objet. Elle nous permet de garder une organisation optimale de note code et nous permet d'avoir le moins de répétition possible. Pour cela, nous allons retourner à nos personnages du début.

Nous allons imaginer un personnage archer qui a moins de vie, mais lorsqu'il attaque, il fait deux fois les dégâts.

{% code title="index.php" %}
```php
<?php

require 'Personnage'; // Ici, l'ordre des classes est important selon les héritages
require 'Archer.php';

$legolas = new Archer();
```
{% endcode %}

{% code title="Archer.php" %}
```php
<?php

Class Archer {
    
}
```
{% endcode %}

Si nous voulons la faire fonctionne comme un personnage classique, nous sommes obligés de copier-coller les fonctions de `Personnage`. Si nous faisons une modification, nous devons la faire à deux endroits. Nous allons donc faire en sorte que notre classe `Archer` hérite de `Personnage`.

{% code title="Archer.php" %}
```php
Class Archer extends Personnage {
    public $arc = 3;
}
```
{% endcode %}

Ici, l'archer a toutes les propriétés de personnages (vie, atk, nom) et celle de archer (arc). Nous pouvons également modifier à la volée les propriétés de Personnage en faisant par exemple :&#x20;

{% code title="Archer.php" %}
```php
Class Archer extends Personnage {
    public $vie = 40;
}
```
{% endcode %}

Ce morceau de code ne fait que pour le moment rajouter une propriétés vie en plus de celle déjà présente. C'est parce que nous l'avons défini en private dans la classe `Personnage`. Si nous voulons l'utiliser, nous devons la passer en protected :&#x20;

{% code title="Personnage.php" %}
```php
class Personnage {
    protected $vie = 80;
    ...
}
```
{% endcode %}

Maintenant, la vie sera modifié et ne sera plus de 80 mais de 40.

<mark style="background-color:red;">Pour utiliser les fonctions de</mark> <mark style="background-color:red;"></mark><mark style="background-color:red;">`Personnage`</mark><mark style="background-color:red;">, nous devons passer toutes les variables en protected.\*</mark>

Nous allons donc refaire notre fonction `attaque` pour que notre archer mette deux fois les dégâts.

{% code title="Archer.php" %}
```php
Class Archer extends Personnage {
    protected $vie = 40;
    
    public function attaque($cible){
        $cible->vie -= 2 * $this->atk;
        $cible->empecher_negatif();
    }
}
```
{% endcode %}

Si un archer attaque un personnage, il perdra 40 de vie.

{% code title="index.php" %}
```php
$legolas->attaque($harry);
var_dump($harry);
```
{% endcode %}

Une autre solution existe pour attaquer deux fois. Attaquer une première fois dans la fonction `attaque` de `Archer` puis attaquer une deuxième fois d'affiler avec la fonction `attaque` de `Personnage`.

{% code title="Archer.php" %}
```php
public function attaque($cible){
        $cible->vie -= $this->atk;
        parent::attaque($cible);
    }
```
{% endcode %}

Si nous utilisons la même fonction que les parents (ici attaque par exemple), nous ne pouvons pas la modifier et y ajouter par exemple des paramètres.
