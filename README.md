# GL_Projet1_Groupe5_Fabio_VANDEWAETER

Explication des dossiers et fichiers du dépôt du Projet1 :
- `bac_a_sable` contient l'archive du dépôt `gson` analysé ainsi qu'un main Java pour pouvoir expérimenter (lancer avec la commande `make main`)
- `README.md` sert de compte rendu à ce Projet 1

## 1 Présentation globale du projet

Il s'agit du logiciel GSon qui a été forké :
https://github.com/fabiovandewaeter/gson

### 1.1 Utilité du projet
#### Fonctionnement du projet
Ce programme permet, en Java, de convertir des objets Java en JSON, et inversement, avec des méthodes fonctionnant comme un `toString()`

Par exemple, on peut convertir du Java en Json grâce à la méthode `gson.toJson()` en passant en paramètre l'objet Java à convertir :

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

public class Main{
    public static void main(String[] args){
        GsonBuilder builder = new GsonBuilder();
        Gson gson = builder.create();

        // Convertion d'éléments simples
        System.out.println("1 => " + gson.toJson(1));
        System.out.println("test => " + gson.toJson("test"));
        final int[] list = { 1, 2, 3 };
        System.out.println("{1,2,3} => " + gson.toJson(list));
        
        // Convertion d'objets complets
        Cube cube = new Cube("red", 10, 50);
        System.out.println("Cube(\"red\", 10, 10) => " + gson.toJson(cube));
    }
    
    public static class Cube{
        private String color;
        private int height;
        private int width;

        public Cube(String color, int height, int width){
            this.color = color;
            this.height = height;
            this.width = width;
        }
    }
}
```

Ce qui affiche :

```
1 => 1
test => "test"
{1,2,3} => [1,2,3]
Cube("red", 10, 10) => {"color":"red","height":10,"width":50}
```

Dans l'autre sens, il est possible de convertir du Json, sous forme de chaîne des caractères, en un objet Java, grâce à la méthode `gson.fromJson()` en passant en paramètre la chaine de caractère Json à convertir ainsi que la classe de l'objet à retourner :

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

public class Main{
    public static void main(String[] args){
        GsonBuilder builder = new GsonBuilder();
        Gson gson = builder.create();

        // Convertion à partir du Json
        Cube cube = new Cube("red", 10, 50);
        String convertedCube = gson.toJson(cube);
        System.out.println("Cube(\"red\", 10, 10) => " + convertedCube);
        Cube cube2 = gson.fromJson(convertedCube, Cube.class);
        System.out.println("Cube(\"red\", 10, 10) => " + gson.toJson(cube2));
        System.out.println("Même objet ? " + cube.equals(cube2));
    }
    
    public static class Cube{
        private String color;
        private int height;
        private int width;

        public Cube(String color, int height, int width){
            this.color = color;
            this.height = height;
            this.width = width;
        }
    }
}
```

Ce qui nous donne bien un nouvel objet avec les mêmes valeurs en attributs que l'ancien, même après convertion en Json : 

```
Cube("red", 10, 10) => {"color":"red","height":10,"width":50}
Cube("red", 10, 10) => {"color":"red","height":10,"width":50}
Même objet ? false
```

#### Créer l'archive du programme
##### > Sans Maven ou Gradle
A la racine du projet, faire `mvn clean verify` pour obtenir l'archive dans le dossier `gson/gson/target/gson-2.10.2-SNAPSHOT.jar`

Le dépôt contient divers dossiers, par exemple `gson/extras` qui contient des fonctionnalités non fournies par défaut ou `gson/metrics` qui permet aux développeurs de faire des benchmarks de leur côté, mais le dossier le plus important, avec plus de 200 classes, est le dossier `gson/gson`, qui permet d'obtenir l'archive

##### > Avec Gradle/Android

D'après le Readme, il suffit d'ajouter cette dépendance :

```gradle
dependencies {
    implementation 'com.google.code.gson:gson:2.10.1'
}
```

##### > Avec Maven2/3
Toujours d'après le Readme, il faut ajouter ceci :

```xml
<dependencies>
    <!--  Gson: Java to JSON conversion -->
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.10.1</version>
      <scope>compile</scope>
    </dependency>
</dependencies>
```

Dans le dépôt de ce compte rendu, il y a un dossier `bac_a_sable` dans lequel se trouve un main Java permettant d'essayer gson avec la commande `make main`

### 1.2) Description du projet

#### Readme

Le dépôt contient un Readme à jour malgré le fait que le projet soit en "maintenance mode" (d'après le Readme), donc qu'il ne soit plus prévu d'ajouter de fonctionnalités

#### Documentation

En plus du fichier `README.md`, le fichier `GsonDesignDocument.md` donne des détails sur les choix faits lors de la conception du programme

Le fichier `Troubleshooting.md`, quant à lui, détaille le fonctionnement des exceptions

Le fichier `UserGuide.md` vient compléter le Readme dans tous ses aspects

Ces informations sont suffisantes pour permettre d'utiliser le programme

## 2) Historique du logiciel
### 2.1) Analyse du git

#### Composition de l'équipe
Le projet compte 145 contributeurs mais les 6 plus gros contributeurs ont participé significativement plus que les autres

La grande majorité des contributions ont eu lieu entre 2008 et 2015

#### Activité du projet
Le projet a été crée en 2008 et étant en "maintenance mode" depuis 2014 (ce qui signifie ici qu'il n'y aura pas de nouvelles fonctionnalités ajoutées), il est donc normal de voir que pratiquement aucun commit n'a eu lieu depuis 2014

![commits-history](https://github.com/fabiovandewaeter/GL_Projet1_Groupe5_Fabio_VANDEWAETER/assets/134401954/4c5c4a66-0f8a-4a1b-b864-ce8c29b59207)


#### Branches

Il y a eu 18 branches au total et 8 branches sont encore actives dont :
- la branche `main`
- 6 branches gérée par `dependabot`, un programme qui met automatiquement à jour les dépendances du projet Github
- une branche gérée par `OSSF Scorecard` qui gère la sécurité du projet

#### Pull requests

Les pulls requests sont utilisées depuis 2015 sur le dépôt, avec des labels en fonction du type de modifications à apporter ; il y a actuellement 105 pulls requests ouvertes, notamment pour mettre à jour des dépendances, et 874 fermées

## 3) Architecture logicielle
### 3.1) Utilisation de bibliothèques extérieures
(PAS FAIT)
### 3.2) Organisation en paquetages
Le projet `gson/gson` est composé de 9 packages, qui se trouvent dans le dossier `gson/gson/src/main/java` :
> `com.google.gson` contient tous les autres packages
>> `com.google.gson.annotations` qui fournit des annotations qui peuvent être utilisées avec le projet

>> `com.google.gson.internal` qui permet au projet de fonctionner mais ne doit pas être accédé directement
>>> `com.google.gson.internal.bind`
>>> `com.google.gson.internal.bind.util`
>>> `com.google.gson.internal.reflect`
>>> `com.google.gson.internal.sql`

>> `com.google.gson.reflect` qui donne des informations sur les types
>> `com.google.gson.stream` qui fournit des classes pour traiter le JSON de manière efficace

Dans le dossier `gson/gson/src/test/java` on retrouve globalement la même structure avec quelques changements :
1) `com.google.gson.annotations` n'est pas testé
2) `com.google.gson.common` est un nouveau package qui ajoute des méthodes pour les autres tests
2) `com.google.gson.functional` est un nouveau package qui test le projet de façon plus globale avec des tests fonctionnels
3) `com.google.gson.metrics` est un nouveau package qui test les performances
4) `com.google.gson.regression` est un nouveau package

Globalement, les packages ont des noms pertinents et séparent les fonctions du projet de façon pertinente, en plus de rester cohérent avec la structure des test

### 3.3) Répartition des classes dans les paquetages
Le projet comporte 252 classes au total dont 202 dans `gson/gson`, avec 83 classes dans `gson/gson/src/main` et 119 classes de test dans `gson/gson/src/test`

La majorité des classes se trouvent uniquement dans le packetage `com.google.gson` mais le le package `com.google.gson.reflect` ne contient qu'une classe, ce qui montre que ce choix de répartition en package est pertinent

### 3.4) Organisation des classes
(PAS FAIT)

## 4) Analyse approfondie
### 4.1) Tests
On lance les tests dans le dossier `gson/gson` grâce à la commande `mvn test`

#### Metrics
![JUnit metrics](./assets/JUnit-metrics-gson.png)

Le tableau ci-dessus présente des statistiques sur les tests JUnit du dossier `gson/gson/src/test` avec le nombre d'assertions de test (JTA), le nombre de classes de test (JTC) et le nombre de méthodes de test (JTM)

Comme on pouvait s'y attendre les packages `com.google.gson.regression` et `com.google.gson.metrics` et `com.google.gson.common` comportent peu de tests car ils sont là pour compléter les autres tests ou n'ont pas besoin d'être testés

#### Coverage

![Test coverage](./assets/coverage.png)

Sonarqube indique 89.6% du code de `gson/gson/src/main` est testé, ce qui est satisfaisant car les classes essentielles sont bien testées

#### Type de tests
Les tests sont des tests unitaires sauf dans le package `com.google.gson.functional` qui contient des test fonctionnel, ce qui permet de tests les méthodes mais aussi de vérifier qu'elles intéragissent bien entre-elles du début à la fin

#### Resultat des tests
![Test success](./assets/test_success.png)

Les tests 1360 tests passent sans erreurs et même si 19 ne sont pas exécutés, cela est très satisfaisant

#### Améliorations possibles

On pourrait ajouter des tests aux classes `com.google.gson.JsonParser` et `com.google.gson.JsonElement` qui ont environ 50% de coverage, puis compléter certaines classes de tests pour tester des cas relativements simples qui ne sont pas encore testés

### 4.2) Commentaires
#### Nombre de lignes de commentaire
![Javadoc coverage](./assets/javadoc_coverage.png)
Le tableau ci-dessus présente différentes statistiques sur la javadoc de `gson/gson`, avec le coverage des classes (Jc), le coverage des attributs (Jf), le nombre de lignes de javadoc (JLOC) ainsi que le coverage des méthodes


#### Type de commentaire
Le code est largement commenté dans le format de la Javadoc, avec les licences en début de fichier

#### Parties sans commentaires

Le code est donc largement commenté en dehors des packages `com.google.gson.internal`, car ces derniers ne sont pas censé être accédés directement lors de l'utilisation de l'API ; cela peut poser problème pour les développeurs eux-mêmes qui pourraient ne pas s'y retrouver par manque de documentation, et il serait pertinent d'ajouter des commentaires à certaines méthodes, notamment pour expliquer dans quel contexte elles sont utilisées dans le projet

### 4.3) Dépréciation
(PAS FAIT)

### 4.4) Duplication de code
Il n'y a pratiquement pas de duplication de code, mais on peut trouver du code dupliqué dans le fichier `gson/gson/src/main.java/com/google/gson/internal/bind/TypeAdapters.java`, de façon très légère, par exemple pour les lignes 197-209 et 232-244, mais cela se répère dans les méthodes de type `public statis final TypeAdapter<T>` :
```java
  public static final TypeAdapter<Number> SHORT =
      new TypeAdapter<Number>() {
        @Override
        public Number read(JsonReader in) throws IOException {
          if (in.peek() == JsonToken.NULL) {
            in.nextNull();
            return null;
          }

          int intValue;
          try {
            intValue = in.nextInt();
          } catch (NumberFormatException e) {
            throw new JsonSyntaxException(e);
          }
```
```java
  public static final TypeAdapter<Number> BYTE =
      new TypeAdapter<Number>() {
        @Override
        public Number read(JsonReader in) throws IOException {
          if (in.peek() == JsonToken.NULL) {
            in.nextNull();
            return null;
          }

          int intValue;
          try {
            intValue = in.nextInt();
          } catch (NumberFormatException e) {
            throw new JsonSyntaxException(e);
          }
```


Il semble donc possible d'améliorer cela en créant de petites fonctions qui gèrent les différentes parties communes à ces méthodes

### 4.5) God Classes
Même si la majorité des classes sont peu complexes, quelques-unes sont particuliérement imposantes ; par exemple ces méthodes on une complexité (WMC) particuliérement élevée :

![God Classes](./assets/god_class.png)

Il en va de même pour les fichiers de tests de ces classes, mais cela est moins impactant

#### Améliorations possibles
Avec beaucoup de temps il serait possible de séparer ces classes en sous-classes plus spécialisées et simples à maintenir, même si cela demenderai beacoups de temps


Nombre magique dans `gson/gson/src/main/java/com/google/gson/internal/bind/TypeAdapters.java` dans tous les trucs du stype TypeAdapter<T>





#### Documentation
https://github.com/fabiovandewaeter/gson/blob/main/GsonDesignDocument.md
https://www.javadoc.io/doc/com.google.code.gson/gson/latest/com.google.gson/module-summary.html
https://github.com/fabiovandewaeter/gson/blob/main/UserGuide.md
