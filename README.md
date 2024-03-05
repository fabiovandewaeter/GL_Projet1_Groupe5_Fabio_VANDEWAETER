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
Le projet comporte 252 classes au total dont 203 dans `gson/gson`, avec 84 classes dans `gson/gson/src/main` et 119 classes de test dans `gson/gson/src/test`

La majorité des classes se trouvent uniquement dans le packetage `com.google.gson` mais le le package `com.google.gson.reflect` ne contient qu'une classe, ce qui montre que ce choix de répartition en package est pertinent

### 3.4) Organisation des classes
(PAS FAIT)

## 4) Analyse approfondie
### 4.1) Tests













#### Documentation
https://github.com/fabiovandewaeter/gson/blob/main/GsonDesignDocument.md
https://www.javadoc.io/doc/com.google.code.gson/gson/latest/com.google.gson/module-summary.html
https://github.com/fabiovandewaeter/gson/blob/main/UserGuide.md
