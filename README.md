# GL_Projet1_Groupe5_Fabio_VANDEWAETER

Dépôt du Projet1

## Outils utilisés

### Intellij
Les plugins :
- Code Metrics
- Metrics Reloaded
- Statistic
- Statistic View

## Présentation globale du projet

Il s'agit du logiciel GSon qui a été forké :
https://github.com/fabiovandewaeter/gson

### Utilité du projet
#### Fonctionnement du projet
Ce programme permet, en Java, de convertir des objets Java en JSON, et inversement, avec des méthodes fonctionnant comme un `toString()`

Par exemple, on peut convertir du Java en Json :

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

Dans l'autre sens, il est possible de convertir du Json, sous forme de chaîne des caractères, en un objet Java :

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

Ce qui nous redonne bien un objet (différent) avec les mêmes valeurs en attributs : 

```
Cube("red", 10, 10) => {"color":"red","height":10,"width":50}
Cube("red", 10, 10) => {"color":"red","height":10,"width":50}
Même objet ? false
```

#### Créer l'archive du programme

A la racine du projet, faire `mvn package` pour obtenir l'archive dans le dossier `gson/gson/target/gson-2.10.2-SNAPSHOT.jar`

#### Analyse du code
https://github.com/fabiovandewaeter/gson/blob/main/GsonDesignDocument.md

https://www.javadoc.io/doc/com.google.code.gson/gson/latest/com.google.gson/module-summary.html

https://github.com/fabiovandewaeter/gson/blob/main/UserGuide.md