# La visibilité public / private

Ce mot clé (public / private) désigne la visibilité de nos variables. À quel moment on peut y accéder ou pas ? Il existe 3 mots-clés :&#x20;

* public -> La variable est accessible au sein de la classe et en dehors
* private -> La variable est accessible uniquement au sein de la classe (sauf exemple ci-dessous)
* protected -> Aussi strict que le private mais on peut y accéder via des classes qui hérite du parent

Pour afficher tout de même une information qui est privé, nous pouvons utiliser une fonction public.

{% code title="Personnage.php" %}
```php
class Personnage {
    private $nom;
    
    public function getNom(){
        return $this->nom;
    }
}
```
{% endcode %}

{% code title="index.php" %}
```php
$merlin->getNom();
```
{% endcode %}

Pour avoir une API plus simple à comprendre, il est conseillé de mettre les variables en private et de créer des fonctions `getter` (ex: `getNom()`) et `setter` (ex: `setNom()`) afin de pouvoir les lires dans le fichier index.php.

{% code title="Personnage.php" %}
```php
public function setNom($nom){
    $this->nom = $nom;
}
```
{% endcode %}



Par exemple, faisons en sorte que la vie de notre personnage ne puisse pas descendre en dessous de 0. Pour cela, créons un fonction qui s'appelle `empecher_negatif` et qui sera défini sur private (nous n'en aurons besoin uniquement dans notre classe. Inutile qu'elle soit en publique).

{% code title="Personnage.php" %}
```php
private function empecher_negatif(){
    if($this->vie < 0){
        $this->vie = 0;
    }
}
```
{% endcode %}

Modifions maintenant notre fonctionne attaque pour que la cible ne descende pas en dessous de 0 point de vie.

{% code title="Personnage.php" %}
```php
public function attaque($cible){
    $cible->vie -= $this->atk;
    $cible->empecher_negatif();
}
```
{% endcode %}
