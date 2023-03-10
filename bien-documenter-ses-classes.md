# Bien documenter ses classes

Lorsque l'on utilise un IDE, nous avons une auto-complétion du code. Si les classes sont organisées comme nous l'avons fait, lorsque quelqu'un va le reprendre, cela va être dur de comprendre de quoi il s'agit.

Ce que l'on peut faire, c'est mettre des documentations dans le code. C'est ce qu'on appelle PHPdoc. Voyons par exemple comment documenter notre classe `Form`.

{% code title="form.php" %}
```php
/**
* Class Form
* Permet de rédiger un formulaire rapidement et simplement
*/

class Form{
    ...
}
```
{% endcode %}

Nous pouvons également documenter nos variables en mettant `@var` et le type de variable :&#x20;

{% code title="form.php" %}
```php
class Form{
    /**
    * @var array Données utilisées par le formulaire
    */
    private $data;
    
    /**
    * @var string Tag utilisé pour entourer les champs
    */
    private $surrond;
    
}
```
{% endcode %}

Il nous reste plus qu'a documenter nos fonctions en utilisant @param pour chaque paramètre de celle-ci et @return si la fonction renvoie une information :&#x20;

{% code title="form.php" %}
```php
class Form{
    ...
    /**
    * @param $index string Index de la valeur à récupérer
    * @return string
    */
    private function getValue($index){
        return isset($this->data[$index])  ? $this->data[$index] : null;
    }   
}
```
{% endcode %}
