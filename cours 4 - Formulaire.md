# Fonctions Dart avec paramètres nommés
```dart
void main() {
    relem("Bonjour", "Ed");
    relem2(msg: "Bonjour", name: "Ed");
}

void relem(String msg, String name) {
    print(msg);
    print(name);
}

// définir des paramètres nommés avec des {}
void relem2({String? msg, String? name}) {
    print(msg);
    print(name);
}
```

`super.key` <br>
La clé est unique et permet d'identifier un écran pour que Flutter puisse facilement l'identifier. 


# Formulaire

```dart
class _MyHomePageState extends State<MyHomePage> {

    final = formKey = GlobalKey<>();
    
    TextEditingController passwordInput = TextEditingController();
    TextEditingController fullNameInput = TextEditingController();

    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text("Mon Application"),
                body: Container (
                    padding: EdgeInsets.all(20.0),
                    child: Form(
                        key: formKey,
                        child: Column(
                            children: [
                                TextFromField(
                                    controller: emailInput,
                                    style: TextStyle(
                                        fontSize: 14.0,
                                        color: Colors.black,
                                    ),
                                    decoration: InputDecoration(
                                        hintText: "Entrez votre email",
                                    ),
                                    validator: (value) {
                                        if(value == null || value.isEmpty) {
                                            return "Ce champ est obligatoire"
                                        }
                                        else if(value.length < 6) {
                                            return "Email invalide";
                                        }
                                        else if(!value.endsWith('esih.edu')) {
                                            print("Seulement le domaine de l'ESIH est autorisé");
                                        }
                                        return null;
                                    },
                                ),
                                SizedBox(height: 20.0),
                                TextFromField(
                                    controller: passwordInput,
                                    decoration: InputDecoration(
                                        hintText: "Entrez votre mot de passe",
                                    ),
                                    obscureText: true,      // pour cacher le mot de passe durant l'insertion
                                    validator: (value) {
                                        if(value == null || value.isEmpty) {
                                            return "Ce champ est obligatoire"
                                        }
                                        return null;
                                    },
                                ),
                                SizedBox(height: 20.0),
                                SizedBox(
                                    width: double.infinity, 
                                    child: ElevatedButton(
                                        child: Text("Envoyer"),
                                        onPressed: () {
                                            print("Envoyé...");
                                            if(fromKey.currentState!.validate()) {
                                                // pour récupérer les données du formulaire
                                                Map data = {
                                                    'email': emailInput.text, 
                                                    'password': passwordInput.text,
                                                };
                                            }
                                            else {
                                                print("Le formulaire n'est pas valide")
                                            }

                                            // pour afficher un message "toast" sur flutter
                                            ScaffoldMessenger.of(context).showSnackBar(
                                                const SnackBar(
                                                    content: Text("Le formulaire n'est pas valide")
                                                )
                                            );

                                            print(data);
                                        },
                                    ),
                                )
                            ]
                        )
                    ),
                ),
            ),
        );
    }
}
```


## Pour contrôler les valeurs insérées par l'utilisateur dans les champs: 
`TextEditingController();`

# API Factice
Créez le fichier `lib/services/api.dart`
À l'intérieur : 

```dart
Map data = {
    'users': [
        {
            'id': 1,
            'first_name': 'Ed Patrice',
            'last_name': 'Pavelus',
            'email': 'paveluspatrice@esih.edu',
            'password': '1234',
            'photo': 'chemin_vers_la_photo'
        },
        {
            'id': 2,
            'first_name': 'Brian',
            'last_name': 'Pavelus',
            'email': 'pavelusbrian@esih.edu',
            'password': '5678',
            'photo': 'chemin_vers_la_photo'
        },
    ],
}
```

<br>

# Exemple d'utilisation des expressions régulières

```dart
// Si vous voulez utiliser des expressions régulières
RegExp phoneNumberPattern = RegExp(r'^(?:\+?509\s?)?(?:\d{2}\s?){3}\d{2}$');

if(!phoneNumberPattern.hasMatch(_variableToMatchPattern)) {
    // code ...
}
    
```