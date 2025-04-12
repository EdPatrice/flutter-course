# Stockage

Dans le dossier `services`, **créer un nouveau fichier** appelé `storage.dart`.

```dart
class Storage {
    final _storage = FlutterSecureStorage();

    Future get(String key) async {
        return await _storage.read(key: key);
    }
    
    Future<void> delete(String key) async {        
        await _storage.delete(key: key);
    }

    Future<void> write(String key, dynamic data) async {
        await _storage.write(key: key, value: json.encode(data));
    }
    
    Future<void> update(String key, dynamic data) async {
        await _storage.delete(key: key);
        await _storage.write(key: key, value: json.encode(data));        
    }
}
```
<br>

## Utilisation
Essayez d'obtenir la réponse du serveur. Si l'utilisateur est hors ligne, obtenez la réponse du stockage.
```dart

final storageService = StorageService();

try {
    response = await ApiService.get("link");
    storageService.write('products', response);
} catch (e) {
    response = await storageService.get('products');
}

```

# Notifications
 - On peut utiliser `Firebase`.

 ```dart
import 'package:flutter_local_notification/flutter_local_notifications.dart';

class NotificationService {

    static final FlutterLocalNotificationsPlugin notif = FlutterLocalNotificationsPlugin();

    static Future pushNotification({ required String title, required Map<String, dynamic> data }) async {
        // Bonjour {username}, vous avez {nombre} d'articles dans votre panier. 
        // {'username': 'Ed', 'nombre': 14}
        
        await notif.show(
            0,
            title,
            'Bonjour ${data['username']}, vous avez ${data['nombre']} d\'articles dans votre panier.',
            NotificationDetails(),
        );
    }
}
 ```

## Utilisation 

```dart
NotificationService.pushNotification(
    title: 'Bienvenue',
    data: {
        'username': 'Ed',
        'nombre': 14
    }
);
```

<br>
# Boîte de dialogue d'alerte

```dart
onTap: () {
    showDialog(
        context: context, 
        builder: (ctx) {
            return AlertDialog(  // pour IPhone -> return CupertinoAlertDialog 
                title: Text('Titre de la notification'),
                content: Text('Contenu de la notification'),
                actions: [
                    TextButton(child: Text("Ok"), onPressed: () {}),
                    TextButton(child: Text("Annuler"), onPressed: () {
                        Navigator.of(context).pop();
                    })
                ]
            );
        }
    );
}
```


# Versionnage
'0.0.0' 
- Partie 1 -> Nouvelle version de l'application
- Partie 2 -> Indique l'ajout de fonctionnalités
- Partie 3 -> Indique la correction de bugs