# Contrôleur d'Onglets

```dart
class HomeScreen extends StatefulWidget {
    @override
    _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> with SingleTickerProviderStateMixin {
    late TabController controller;  // pour le défilement des onglets

    @override
    void initState() {
        super.initState();
        controller = TabController(length: 3, vsync: this);
    }

    @override
    void dispose() {
        controller.dispose();
        super.dispose();
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text("Mon Application"),
                bottom: TabBar(
                    controller: controller,
                    tabs: [
                        Tab(text: "Accueil"),
                        Tab(text: "Paramètres"),
                        Tab(text: "Profil"),
                    ]
                )
            ),
            body: TabBarView(
                controller: controller,
                children: [
                    Center(child: Text("Page d'Accueil")),
                    Center(child: Text("Page des Paramètres")),
                    Center(child: Text("Page de Profil")),
                ]
            )
        );
    }
}
