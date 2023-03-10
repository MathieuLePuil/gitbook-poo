# Exemple concert : formulaire

L'idée ici est de créer une classe permettant de créer un formulaire comme ceci :&#x20;

{% code title="index.php" %}
```php
<?php

require 'form.php';

$form = new Form();
echo $form->input('username');
echo $form->input('password');
echo $form->submit();
```
{% endcode %}

Nous pouvons également faire passer des paramètres par défaut dans les variables de la classe.

{% code title="index.php" %}
```php
$form = new Form(array(
    'username' => 'Mathieu'
));
echo $form->input('username');
echo $form->input('password');
echo $form->submit();
```
{% endcode %}

Comme nous l'avons dit précédemment, séparons nos classes dans différents fichiers. Créons donc le fichier `Form.php`.

Ajoutons la fonction et son constructeur :&#x20;

{% code title="Form.php" %}
```php
<?php

class Form{
    private $data;

    public function __construct($data = array()){ // on définit les paramètres vide par défaut
        $this->data = $data;
    }
}
```
{% endcode %}

Nous avons besoin maintenant des fonctions `input` et `submit` pour notre formulaire. Nous les ajouterons comme ceci dans la classe `Form`.

{% code title="Form.php" %}
```php
public function input($name){
    echo '<input type="text" name="' . $name . '">';
}

public function submit(){
    echo '<button type="submit">Envoyer</button>';
}
```
{% endcode %}

Pour améliorer le html, nous allons ajouter des paragraphes autour du `input` et du `submit`. Pour cela, nous allons créer une nouvelle fonction private.

{% code title="Form.php" %}
```php
public $surrond = 'p';

private function surrond($html){
    echo '<{$this->surrond}>{$html}</{$this->surrond}>';
}

public function input($name){
    echo $this->surrond('<input type="text" name="' . $name . '"');
}

public function submit(){
    echo $this->surrond('<button type="submit">Envoyer</button>');
}
```
{% endcode %}

Le formulaire fonctionne mais dans le `input` de username, aucune valeur n'est rentré par défaut alors que nous le souhaitons. Pour cela, nous allons créer un nouvelle fonction privé qui permet de récupérer la valeur par défaut de la classe `Form`.

{% code title="Form.php" %}
```php
private function getValue($index){
    return isset($this->data[$index])  ? $this->data[$index] : null;
}

public function input($name){
    echo $this->surrond(
        '<input type="text" name="' . $name . '" value="' . $this->getValue($name) . '"'
    );
}
```
{% endcode %}

### Le formulaire final

{% code title="index.php" %}
```php
<?php
    require 'form.php';
    $form = new Form($_POST);
?>

<form action="#" method="post">
    <?php
        echo $form->input('username');
        echo $form->input('password');
        echo $form->submit();
    ?>
</form>
```
{% endcode %}
