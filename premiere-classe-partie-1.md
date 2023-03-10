# Première Classe - Partie 1

Ici, nous allons utiliser l'exemple d'un personnage qui attaque des monstres.

Créons tout d'abord notre fichier `index.php`. Pour de meilleures pratiques, nous allons ensuite séparer nos classes dans des fichiers différents. Créons donc maintenant le fichier de notre première classe nommée `Personnage` et définissons celle-ci.

{% code title="personnage.php" %}
```php
class Personnage {}
```
{% endcode %}

Importons notre fichier dans notre `index.php` :&#x20;

{% code title="index.php" %}
```php
<?php

require 'Personnage.php';
```
{% endcode %}

Ajoutons maintenant un nouveau personnage nommé _Merlin_ et affichons le dans la console :&#x20;

{% code title="index.php" %}
```php
<?php

require 'Personnage.php';

$merlin = new Personnage();
var_dump($merlin);
```
{% endcode %}

Le résultat dans la console doit être celui-ci :&#x20;

```javascript
object(Personnage)[1]
```

Nous voulons voir la vie de notre personnage. Pour cela, créons une variable dans laquelle nous enregistrerons ses points de vie. Pour le moment, la variable est définie en public. Nous verrons plus tard les autres possibilités.

<pre class="language-php" data-title="Personnage.php"><code class="lang-php"><strong>class Personnage {
</strong>    public $vie = 100; // Notre personne a 100 points de vie au départ
}
</code></pre>

Actualisez la console et vous pouvez voir son nombre de vie s'afficher.

Maintenant, faisons de même pour ses points d'attaque :&#x20;

{% code title="Personnage.php" %}
```php
class Personnage {
    public $vie = 100;
    public $attaque = 20; // Ici, notre personnage a 20 points d'attaque
}
```
{% endcode %}

Ajoutons une action que peut faire notre personnage (exemple : crier).&#x20;

{% code title="Personnage.php" %}
```php
class Personnage {
    public $vie = 100;
    public $attaque = 20;
    
    public function crier(){
        echo 'JE CRIIEEE';
    }
}
```
{% endcode %}

Tout ça est bien mais c'est juste une fonction, notre personnage ne crie pas pour le moment. Modifions le `var_dump` du `index.php` pour : afficher sa vie, afficher ses points d'attaque puis faisons le crier.

{% code title="index.php" %}
```php
var_dump($merlin->vie);
var_dump($merlin->attaque);
var_dump($merlin->crier());
```
{% endcode %}

Imaginons maintenant que notre personnage n'a pas ses 100 points de vie mais plus que 80. Nous allons vouloir lui régénérer. Pour cela, créons une fonction :&#x20;

{% code title="Personnage.php" %}
```php
class Personnage {
    public $vie = 80;
    
    public function regenerer(){
        $this->vie = 100;
    }
}
```
{% endcode %}

`$this` est le personnage que nous voulons regénerer. Regénérons donc notre Merlin :&#x20;

{% code title="index.php" %}
```php
$merlin->regenerer();
var_dump($merlin->vie);
```
{% endcode %}

Nous pouvons voir maintenant que Merlin a récupéré ses 100 points de vie. Si nous créons un nouveau personnage, celui-ci aura 80 de vie au départ. Exemple :&#x20;

{% code title="index.php" %}
```php
$harry = new Personnage();
var_dump($harry->vie);
```
{% endcode %}

Le résultat affiché dans la console sera : 80.
