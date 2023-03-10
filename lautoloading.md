# L'autoloading

L'autoloading est un système qui va permettre de charger automatiquement nos classes afin de remplacer nos require. Pour mieux nous organiser, gardons notre `index.php` dans notre dossier principal et nous allons en créer un pour les classes.&#x20;

Les classes seront donc chargée directement lorsque nous l'appellerons ainsi que ses parents si elle en a. Pour cela, utilisons la fonction nommée `spl_autoload_register` qui prend en paramètre la fonction que l'on souhaite appelée.

{% code title="index.php" %}
```php
<?php

spl_autoload_register('mon_auto_loader');
```
{% endcode %}

{% code title="AutoLoader.php" %}
```php
<?php

class AutoLoader {
    static function autoload($class_name){
        require 'class/' . $class_name . '.php';
    }
}
```
{% endcode %}

Nous avons appelé la fonction `"mon_auto_loader"` dans `index.php` mais le problème est que maintenant, la fonction est dans une classe. Il va donc falloir mettre un tableau en paramètre.

{% code title="index.php" %}
```php
require 'class/Autoloader.php';
spl_autoload_register(array('AutoLoader', 'autoload')); // = AutoLoader::autoload
```
{% endcode %}

Nous pouvons encore réduire le nombre de ligne du `index.php` en mettant notre autoloader dans une fonction de notre classe.

{% code title="AutoLoader.php" %}
```php
class AutoLoader {
    static function register(){
        spl_autoload_register(array(__CLASS__, 'autoload'));
    }

    ...
}
```
{% endcode %}

Nous pouvons maintenant l'importer plus facilement dans le `index.php` :&#x20;

{% code title="index.php" %}
```php
require 'class/Autoloader.php';
AutoLoader::register();
```
{% endcode %}

Les classes sont maintenant chargées automatiquement lorsque nous les appellons.
