# Workshop Jinja2

![](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fgblobscdn.gitbook.com%2Fassets%252F-MYVW6MKCi9iujNc3SK_%252F-M_e-oreKDASc0S58clo%252F-M_e1dkHEZGBPJA4S5Uq%252Fjinja-banner.jpg%3Falt%3Dmedia%26token%3Dbfe1fadd-0c7f-4fe2-9f0f-7517c3a0ed52&f=1&nofb=1&ipt=012bfb044e2ab69544304394d6125e4eb597ff85216395552f2d0a660e664bf3&ipo=images)

Bienvenue dans cette activité Workshop où vous allez apprendre à utiliser Jinja, un moteur de template.

L'outil permet de générer à partir de template des documents en y injectant des données grâce à une syntaxe dans le style de Python. On peut notamment l'utiliser pour générer plusieurs sortes de document dont des documents HTML pour créer des pages WEB.

# Démarrage

Pour débuter le workshop vous pouvez choisir d'installer par vous-même `Jinja2` dans votre propre projet python en utilisant la [documentation officielle](https://jinja.palletsprojects.com/en/3.1.x/intro/), où choisir d'utiliser le contenu proposé dans ce dépôt.

## Initialisation du projet

### Création de l'environnement
Nous allons utiliser Jinja en tandem avec le langage Python qui nous propose une façon d'isoler les paquets de développement de vos paquets système. Pour ceux qui ont déjà fait du développement avec `npm` voyez ça comme un équivalent à votre dossier `node_modules`.

```console
$ python -m venv .venv
```

Cette commande permet l'initialisation de l'environnement virtuel de python dans un dossier `.venv` (le nom du dossier peut-être modifié à votre préférence, assurez vous le modifier en accord avec le nouveau nom les commandes suivantes) dans lequel nous allons installer nos dépendances Python.

### Activation

#### POSIX Shell (bash, zsh, fish)
```console
$ source .venv/bin/activate
```

#### Windows (CMD, Powershell)

**CMD**
```cmd
C:\> .venv\Scripts\activate.bat
```
**Powershell**
```ps
PS C:\> .venv\Scripts\Activate.ps1
```

Ces commandes nous permettent d'activer l'environnement, cela nous permet de rentrer dans un "sous-shell" qui ajoute à son `$PATH` les paquets installés dans l'environnement.

### Installation des dépendances

```console
$ pip install Jinja2
```
`pip` est le gestionnaire de paquet de Python, l'équivalent à `npm` pour les projets `nodejs`. On installe Jinja dans notre environnement.

## Créer des templates

Dans un dossier `templates/`, créez un fichier HTML simple. C'est dans ce fichier HTML que l'on va placer des **balises** Jinja.

### Print
Pour insérer la valeur d'une variable dans le document vous pouvez utiliser les balises `{{ }}`.

```html
<body>
    <h1>Bonjour {{name}}</h1>
</body>
```

`{{name}}` sera remplacé dans le document par le contenu de `name`.


### Logique

Pour insérer de la logique dans le document vous pouvez utiliser les balises `{% %}`.

```html
<body>
    <h1>Bonjour
        {% if gender == "male" %} M. {% elif gender == "female" %} Mme. {% endif %}
        {{name}}
    </h1>
    Liste de vos agents:
    <ul>
        {% for agent in agents %}
        <li>{{ agent.name }}</li>
        {% endfor %}
    </ul>
</body>
```

Le bloc `{% if %}` affichera "M." ou "Mme." selon la variable `gender`.
Une liste avec le nom de chaque agent sera afficher grâce au block `{% for %}` qui parcours la liste contenue dans `agents`.

## Générer la template

Vous pouvez générez une template en utilisant le module Python `Jinja2`.

**Exercice**
En Python, créez une template de votre choix (HTML ou non) et générez un fichier correspondant dans un dossier `output/`.
Vous devrez suivre ces étapes:

- importez Jinja,
- chargez vos template dans votre programme,
- créez un jeu de donnée de votre choix (`dict`, `list`, `class`, `str`...),
- ouvrez un fichier en utilisant la librarie `os` de Python (pensez à l'`import`),
- générez le fichier en donnant à la template votre jeu de donnée.

**Note:** ouverture et création de fichier en python
```python
import os

with open("/path/to/output_file", "w") as f:
    f.write(output)
```
Remplacez `output` par une string contenant le contenu du fichier.

## Aller plus loin

Vous pouvez utiliser Jinja pour générer n'importe quel type de fichier: HTML, XML, CSV... L'imagination est votre limite.

### Mise en situation
Vous avez à votre disposition une petite base de donnée sqlite `userbase.sqlite`. Cette base contient une table `users` et 6 utilisateurs.

Utilisez le module `sqlite3` de python pour accéder aux données puis injectez les dans une template HTML pour afficher la liste des utilisateurs et leurs informations.

**Note:** utilisation de `sqlite3`
```python
import sqlite3
db = sqlite3.connect("todo.db")
users = db.execute("SELECT * FROM users").fetchall()
```

## Merci d'avoir participé
Dans un futur Workshop FastAPI nous utiliserons Jinja pour créer un site web présentant une page de Todos.
