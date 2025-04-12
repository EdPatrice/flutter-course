# Images
Pour ajouter des images, ajouter d'abord le dossier dans le fichier de configuration `pubspec.yaml`.

## 1. Si l'image est ajoutée au projet (assets/images/):
```dart
Image.assets("assets/images/your_image.png")
```

## 2. Si l'image est sur internet: 
```dart
final String imageUrl = "https://link_to_image"
Image.Network(
    imageUrl,
    height: 50.0,

    // pour afficher une icône de chargement quand l'image n'apparaît pas encore
    loadingBuilder: (ctx, child, progress) {
        if(progess == null) {
            return child;
        }
        else {
            return CircularProgressIndicator(); // cercle de chargement
        }
    }
)
```