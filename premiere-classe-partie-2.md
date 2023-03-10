# Première Classe - Partie 2

Voici tout d'abord à quoi ressemble nos deux fichiers :&#x20;

{% code title="index.php" %}
```php
<?php

require 'Personnage.php';

$merlin = new Personnage();
$merlin->crier();
$merlin->regenerer();

var_dump($merlin);

$harry = new Personnage();

var_dump($harry);
```
{% endcode %}

{% code title="Personnage.php" %}
```php
<?php

class Personnage {
    public $vie = 80;
    public $attaque = 20;
    
    public function crier(){
        echo 'JE CRIIEEE';
    }
    
    public function regenerer(){
        $this->vie = 100;
    }
}
```
{% endcode %}



Nos personnages sont ici définis par `$merlin` et `$harry`. Ajoutons leur un vrai nom :&#x20;

{% code title="Personnage.php" %}
```php
    public $nom; // Ajout d'une variable 'nom' qui n'a pas de valeur par défaut
```
{% endcode %}

Nous définissons les noms dans le `index.php` :&#x20;

{% code title="index.php" %}
```parigp
$merlin->nom = 'Merlin';
var_dump($merlin);

$harry->nom = 'Harry';
var_dump($harry);
```
{% endcode %}

Il existe un autre moyen plus pratique et plus facile : mettre le nom directement quand nous créons un personnage. Pour cela, nous allons avoir besoin d'un constructeur qui va définir les paramètres de la classe.

{% code title="Personnage.php" %}
```php
public function __construct($nom){
    $this->nom = $nom;
}
```
{% endcode %}

{% code title="index.php" %}
```php
$merlin = new Personnage("Merlin");
var_dump($merlin);

$harry = new Personnage("Harry");
var_dump($harry);
```
{% endcode %}

Notre personnage peut régénérer sa vie après un combat mais malheureusement peut être mort aussi pendant celui-ci. Créons une fonction mort qui vérifie si il reste de la vie à mon personnage.

{% code title="Personnage.php" %}
```php
public function mort(){
    $this->vie <= 0; // Si la vie est inférieur ou égale à 0, notre personnage est mort
}
```
{% endcode %}

Créons maintenant notre fonction d'attaque afin que nos personnages puisse se battre entre eux.&#x20;

{% code title="Personnage.php" %}
```php
public function attaque($cible){
    $cible->vie -= $this->atk; // Nous enlevons la vie à la cible selon le nombre de points d'attaques du personnage ($this)
}
```
{% endcode %}

Merlin va attaquer Harry. Regardons ensemble si Harry est mort ou pas.

{% code title="index.php" %}
```php
$merlin->attaque($harry);

if($harry->mort()){
    echo 'Harry est mort !';
} else {
    echo 'Harry a survécu !'
}
```
{% endcode %}

Ici, Harry a 80 points de vie, Merlin a 20 points d'attaque. Il ne lui reste donc plus que 60 points de vie. Hors, si nous définissons le nombre de points de vie de Harry un 20 ou un nombre inférieur, la console nous indique qu'il est mort.



Faisons maintenant en sorte de regénérer nos personnages avec le nombre de vie que nous souhaitons (ici 50 points par exemple).

{% code title="Personnage.php" %}
```php
public function regenerer($vie = null){
    if(is_null($vie)){
        $this->vie = 100;
    } else {
        $this->vie += $vie;
    }
}
```
{% endcode %}

Si ici, le nombre de vie a ajouté n'est pas précisé, le personnage récupèrera ses 100 points de vie. Si nous spécifions comme ci-dessous, il récupèrera un nombre de points de vie personnalisé.

{% code title="index.php" %}
```php
$merlin->regenerer(); // Merlin revient à 100 points de vie
$merlin->regenerer(50); // Merlin gagne 50 points de vie de plus
```
{% endcode %}
