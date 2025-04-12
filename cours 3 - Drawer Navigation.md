# Widgets avec État (Stateful)

~~~dart
class HomeScreen extends StatefulWidget {
    @override
    createState() {
        return HomeScreenState(); // la classe qui va representer le state de l'application
    }
}

class HomeScreenState extends State<HomeScreen> {
    // Toutes les manipulations se feront ici
}
~~~

`State<HomeScreen>` Permet de savoir à quel écran appartient l'état. 

Pour indiquer à Flutter quelle valeur rafraîchir lorsque vous changez quelque chose dans le widget avec état, vous devez utiliser la fonction `setState()`. Assurez-vous simplement d'être dans le contexte de l'**état**: `State<HomeScreen>`.

```dart
setState(() {
    // uniquement les éléments que vous souhaitez rafraîchir à l'écran
})
```

<br>

# Liste Vue 

```dart
Widget build(BuildContext context) {
    return Scaffold(
        //code...
        body: ListView(
            children: [
                ListTitle(
                    title: Text('Pain'),
                    subtitle: Text('Seulement 1 paquet restant'),
                ),
                ListTitle(
                    title: Text('Eau'),
                    subtitle: Text('Achetez-en 1, obtenez-en 1 gratuit'),
                ),
                ListTitle(
                    title: Text('Sucre'),
                    subtitle: Text('En rupture de stock'),
                ),
            ]
        )
    )
}
```

<br>

# Liste Dynamique

```dart
List<Map> data = [
    {"name": "Pain", 'price': 10},
    
];

Widget build(BuildContext context) {
    return Scaffold(
        //code...
        body: ListView.builder(
            itemCount: data.length,
            itemBuilder: (BuildContext ctx, int index){
                Map prod = products[index];

                return ListTile(
                    title: Text(prod['name']),
                    subtitle: Text('Prix: ${prod['price']}')
                    onTap: () {

                    }
                ); //ListTile
            }
        ); //ListView
    )
}
```

`index` représente l'indice de l'élément dans la liste.

Pour ajouter un séparateur entre les éléments d'une liste: `return separator();`

Si la liste est plus longue que l'écran de l'utilisateur, elle va créer automatiquement une barre de défilement, ce qui est super! 😉✅

<br>

# Menu Latéral (Drawer)

```dart
//inside the scaffold
drawer: Drawer (
    child: ListView(
        children: [
            DrawerHeader(
                child: Icon(Icons.person),
                decoration: BoxDecoration(
                    color: Colors.lightblue,
                )
            ), // DrawerHeader
            ListTitle(
                title: Text('Profil'),
                onTap: () {}
            ), //ListTile
            ListTitle(
                title: Text('Paramètres'),
                onTap: () {}
            ), //ListTile
            ListTitle(
                title: Text('Aide'),
                onTap: () {}
            ), //ListTile
            ListTitle(
                title: Text('Contact'),
                onTap: () {}
            ), //ListTile
        ]
    )
)
```

<br>

# Navigation entre écrans

Pour organiser votre code et vous assurer qu'il soit lisible, il est important de ne pas tout mettre dans le fichier **main.dart**. Au lieu de cela, vous pouvez créer différents fichiers, un pour chaque écran.

Créez un dossier appelé **screens** dans le dossier **lib**.
Nous pouvons créer deux fichiers :
- home_screen.dart
- profile_screen.dart

Dans le fichier **main**, importez les fichiers nouvellement créés : 
```dart
import 'screens/home_screen.dart'
import 'screens/profile_screen.dart'
```

Dans la page **Home Screen**, vous pouvez également importer l'écran de profil.

<br>

## Navigateur
Widget qui vous permet de passer d'une page à une autre.

```dart
Navigator.push(context, route)
```
La route doit être créée à partir d'un écran.

```dart
route = MaterialPageRoute(
    builder: (ctx) {
        return Screen();
    } // builder
)
```

<br>

## Utilisation
```dart
//inside the scaffold
drawer: Drawer (
    child: ListView(
        children: [
            DrawerHeader(
                child: Icon(Icons.person),
                decoration: BoxDecoration(
                    color: Colors.lightblue,
                )
            ), // DrawerHeader
            ListTitle(
                title: Text('Profil'),
                onTap: () {
                    // fermer l'écran actuel, dans ce cas, le drawer
                    Navigator.pop(context);
                    // Naviguer vers l'écran de profil
                    Navigator.push(context, MaterialPageRoute(
                        builder: (ctx) {
                            return ProfileScreen();
                        }
                    )); //MaterialPageRoute
                }
            ) // ListTitle
        ] // children
    )
)
```

