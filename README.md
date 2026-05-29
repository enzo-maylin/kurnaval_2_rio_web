# API + Flutter

Voici la procédure pour générer un client Flutter à partir de l’API Symfony.

## 1. Générer la spec OpenAPI depuis Symfony

Dans votre projet Symfony, exécutez :

```bash
php bin/console api:openapi:export -o var/openapi.yaml --yaml
```

C’est ce fichier qui servira de base au générateur Flutter.

## 2. Générer le client Flutter

Dans votre projet Flutter, installez l’outil de génération :

```bash
npm install @openapitools/openapi-generator-cli -g
```

Puis générez le client :

```bash
openapi-generator-cli generate \
  -i C:\xampp\htdocs\kurnaval_2_rio_web\var\openapi.yaml \
  -g dart-dio \
  -o C:\Users\enzom\project\kurnaval_2_rio\lib\api_client \
  --additional-properties=pubName=kurnaval_2_rio_api
```

Si vous voulez un nom de package plus propre, vous pouvez aussi utiliser :

```bash
--additional-properties=pubName=event_api,packageName=event_api
```

## 3. Installer les dépendances Flutter

Dans le dossier de votre application Flutter :

```bash
flutter pub get
```

## 4. Utiliser le client généré

Exemple d’utilisation :

```dart
import 'package:dio/dio.dart';
import 'package:kurnaval_2_rio/api_client/api.dart';

Future<void> main() async {
  final api = DefaultApi(Dio(BaseOptions(
    baseUrl: 'http://localhost:8000',
  )));

  final events = await api.getCollection();
  print(events);
}
```
