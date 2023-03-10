# Les objets

## Qu'est ce qu'un objet ?

Un objet peut être un type de variables :&#x20;

* Chiffres
* Chaines de caractères
* Tableaux
* ...

### Exemple : Les dates

Ajouter 3 mois à une date et l'afficher dans un autre format ?&#x20;

```
date_default_timezone_set('Europe/Paris')

$date = '2023-03-10';
$new_date = date('Y-m-d', strtotime($date . '+ 3 months +2 day'));

echo date('d/m/Y', strtotime($new_date)); // 12/06/2023
```

Ce code est difficile à comprendre. Mais nous pouvons l'améliorer grâce à des fonctions.

```
$date = '2023-03-10';

$date = add_days($date, 2);
$date = add_months($date, 3);

echo format_date($date, 'd/m/Y'); // 12/06/2023
```

## Les objets

Maintenant, nous allons refaire le même code que ci-dessus mais avec des objets.

```
$date = new MaDate('2023-03-10');

$date->addDays(2);
$date->addMonths(3);

$date->format('d/m/Y');
```

Ici, notre date n'est pas créée à base d'une chaîne de caractères, elle est créée en utilisant la class `MaDate()`_._ La date n'est donc ni une chaîne de caractères, ni un entier, c'est un nouveau type de variable qui est un objet : `MaDate`.&#x20;

Nous pouvons à cette date, faire des modification, actions particulières. Ici, nous lui ajoutons 2 jours grâce à `addDays` puis 3 mois grâce à `addMonths`.

### Instanciation

```
$date1 = new MaDate('2023-03-10');
$date2 = new MaDate();
```

Ici, `$date1` et `$date2` sont deux instances (deux variables du même type : `MaDate`). Mais chaque variable sera indépendante.

**MaDate :** Classe

**new MaDate(), $date1, $date2 :** Objets / Instances

### Propriétés et Méthode

Sur nos objets, nous allons avoir des propriétés :&#x20;

```
$date->days
$date->months
$date->years
```

Nous allons pouvoir ensuite appliquer des méthodes :&#x20;

```
$date->days()
$date->months()
$date->addDays(2)
$date->format('d/m/Y')
```

Les méthodes sont comme les fonctions sauf qu'elle s'applique directement sur un objet, donc un instance.
