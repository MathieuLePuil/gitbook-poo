# Propriétés et méthodes statiques

Les propriétés et méthodes statiques n'ont pas besoin d'instance pour les appeler. Elles sont directement liées à notre classe. Nous allons donc voir comment ça marche en créant une fonction qui ajoute des zéros initiaux si la valeur est inférieure à 10. Nous allons créer la classe `Text` qui permet de les modifier.

{% code title="Text.php" %}
```php
<?php

class Text{
    public static function withZero($chiffre){
        if($chiffre < 10){
            return '0' . $chiffre;
        } else {
            return $chiffre;
        }
    }
}
```
{% endcode %}

Nous pouvons maintenant appelé plus facilement la fonction car elle est statique.&#x20;

{% code title="index.php" %}
```php
<?php

require 'Text.php';

$withZero = Text::withZero(4);
var_dump($withZero);
```
{% endcode %}

De la même façon, nous pouvons mettre la fonction en privé pour l'utiliser dans une autre fonction de la classe. Exemple :&#x20;

{% code title="Text.php" %}
```php
class Text{
    public static function publicWithZero($chiffre){
        return self::withZero($chiffre); // self fait référence au nom de la classe dans le cas où le nom soit modifié
    }

    private static function withZero($chiffre){
        ...
    }
}
```
{% endcode %}

{% code title="index.php" %}
```php
$withZero = Text::publicWithZero(4);
var_dump($withZero);
```
{% endcode %}

En plus des fonctions statiques, nous pouvons créer des variables statiques. Si nous souhaitons par exemple mettre un suffixe derrière notre chiffre, nous pouvons faire comme ceci :&#x20;

{% code title="Text.php" %}
```php
class Text{
    private static $suffix = ' €';

    public static function withZero($chiffre){
        if($chiffre < 10){
            return '0' . $chiffre . self::$suffix;
        } else {
            return $chiffre . self::$suffix;
        }
    }
}
```
{% endcode %}
