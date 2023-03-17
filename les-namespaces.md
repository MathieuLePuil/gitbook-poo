# Les namespaces

Le problème de notre organisation de classe est que, si une autre personne reprend le projet ou que nous travaillons avec une librairie tierce, on risque d'avoir des conflits. Deux classes ne peuvent pas avoir le même nom.

Les namespaces sont disponibles dans la plupart des langages de programmation et permettent de ranger les classes dans des packages. Essaions de mettre la classe Form dans un namespace nommé HTML qui sera lui dans POO :&#x20;

{% code title="Form.php" %}
```php
<?php

namespace POO\HTML;

class Form {
    ...
}
```
{% endcode %}

Pour l'utiliser dans `BoostrapForm`, nous devons l'importer via son namespace :&#x20;

{% code title="BoostrapForm.php" %}
```php
class BoostrapForm extends POO\HTML\Form {
    ...
}
```
{% endcode %}

Notre classe `Form` est importé dans `BootstrapForm` mais nous avons toujours une erreur. Celle-ci est lié à l'autoloader. Il récupere le namespace au lieu du nom de la classe. Il suffit de supprimer le POO du namespace pour avoir le nom de la classe.

{% code title="Autoloader.php" %}
```php
static function autoload($class_name){
    $class_name = str_replace('POO\\', '', $class_name); // on remplace le POO\ par rien
    require 'class\' . $class . '.php';
}
```
{% endcode %}

Nous avons plus qu'a mettre notre classe `Form` dans un dossier nommé HTML. Nous pouvons ainsi ajouter des namespaces à toutes nos classes.

Reprenons notre classe `BoostrapForm` et importons un peu mieux notre classe parent `Form`.

{% code title="BoostrapForm.php" %}
```php
<?php

namespace POO\HTML;

class BoostrapForm extends Form {
    ...
}
```
{% endcode %}

Plus qu'à mettre la classe `BoostrapForm` dans le dossier HTML et le tour est joué.

Si par exemple, nous mettons notre `Autoloader` dans le namespace `POO`, nous devrons appelé notre fonction comme ceci :&#x20;

```php
\POO\Autoloader::register();
```

L'autre solution plus simple et plus facile et d'importer la classe en utilisant un `use`.

{% code title="index.php" %}
```php
<?php

use \POO\Autoloader;
use \POO\HTML\BoostrapForm;

require 'class/Autoloader.php';

Autoloader::register();
$form = new BoostrapForm($_POST);
```
{% endcode %}

Pour gagner encore plus en propreté, au lieu de mettre directement POO dans notre fonction `autoload`, nous pouvons directement mettre namespace comme nous l'avons fais pour classe.

{% code title="Autoloader.php" %}
```php
static function autoload($class_name){
    $class_name = str_replace(__NAMESPACE__ . '\\', '', $class_name);
    require 'class\' . $class . '.php';
}
```
{% endcode %}

Si nous voulons utiliser une fonction PHP par défaut (exemple : `DateTime`), nous devons préciser que celle-ci est dans le namespace de PHP de base. Sinon, il la cherchera dans `POO\HTML\` par exemple.

```php
public function date() {
    return new \DateTime(); // On utilise un \ pour préciser le namespace de base
}
```

Nous pouvons encore améliorer notre `Autoloader` en lui précisant quel namespace il peut charger. Ici, essaions avec POO.

{% code title="Autoloader.php" %}
```php
static function autoload($class_name){
    if(strpos($class, __NAMESPACE__ . '\\' === 0 {
        $class_name = str_replace(__NAMESPACE__ . '\\', '', $class_name);
        require 'class\' . $class . '.php';
    })  
}
```
{% endcode %}

