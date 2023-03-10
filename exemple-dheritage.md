# Exemple d'héritage

Reprenons notre exemple de formulaire et imaginons que nous voulons utiliser bootstrap.

{% code title="index.php" %}
```php
<html>
  <head>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </head>
  <body>
    
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
    
  </body>
</html>
```
{% endcode %}

L'objectif est de modifier le html de notre formulaire pour le lié à Bootstrap. Nous allons reprendre la classe `Form` et y ajouter des fonctionnalités. Pour cela, créons la classe `BoostrapForm`.

{% code title="BoostrapForm.php" %}
```php
<?php

class BoostrapForm extends Form {
    
}
```
{% endcode %}

{% code title="index.php" %}
```php
<?php
    require 'BoostrapForm.php';
    $form = new BoostrapForm($_POST);
?>
```
{% endcode %}

Récupérons nos trois fonctions qui contiennent du HTML (ici `surrond`, `input` et `submit`) et ajoutons y nos classes Bootstrap.

{% code title="BoostrapForm.php" %}
```php
private function surrond($html){
    echo '<div class="form-group">{$html}</div>';
}

public function input($name){
    echo $this->surrond(
        '<label>' . $name . '</label><input type="text" name="' . $name . '" value="' . $this->getValue($name) . '" class="form-control"'
    );
}

public function submit(){
    echo $this->surrond('<button type="submit" class="btn btn-primary">Envoyer</button>');
}
```
{% endcode %}

N'oubliez pas lorsque vous utiliser une classe parent de vérifier la visibilité de vos éléments.
