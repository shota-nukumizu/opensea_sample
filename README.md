# opensea_sample

Opensea APIを叩くためだけのFlutterプロジェクト。

# セットアップ

```powershell
# パッケージをインストール
flutter create opensea_sample

# 必要なパッケージをインストール
flutter pub add opensea_dart
```

あとは`ios`、`windows`や`mac`などのパッケージを削除して(使わないので)、以下のコードを`lib/main.dart`にコピペする

```dart
import 'package:opensea_dart/enums/enums.dart';
import 'package:opensea_dart/opensea_dart.dart';

void main() async {
  String? apiKey = "Put you api key here, or pass null to use without apikey";
  final openSea = OpenSea(apiKey);

  ///getOrders (requires apiKey to be set)
  openSea
      .getOrders(side: OrderSide.buy, limit: "1")
      .then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getEvents (requires apiKey to be set)
  openSea.getEvents(limit: "1").then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getCollectionStats
  openSea
      .getCollectionStats(slug: "copypasteearth")
      .then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getContract
  openSea
      .getContract(
          assetContractAddress: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb")
      .then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getAsset
  openSea
      .getAsset(
          assetContractAddress: "0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb",
          tokenId: "1",
          accountAddress: "0xb88f61e6fbda83fbfffabe364112137480398018")
      .then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getBundles
  openSea.getBundles(
      tokenIds: ["1", "209"], limit: "1").then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getCollections
  openSea.getCollections(limit: "1", offset: "5").then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getCollection
  openSea.getCollection("copypasteearth").then((value) => print(value));
  await Future.delayed(const Duration(seconds: 5));

  ///getAssets
  openSea
      .getAssets(
          orderBy: OrderBy.saleDate,
          orderDirection: OrderDirection.asc,
          limit: "1",
          offset: "0",
          collection: "doodles-official")
      .then((value) => print(value));
}
```

これを以下のコマンドで実行するとエラー発生。

```
flutter run
```

▼出力エラー

```
Error: FormatException: SyntaxError: Unexpected token I in JSON at position 0
    at Object.throw_ [as throw] (http://localhost:60638/dart_sdk.js:5148:11)
    at Object._parseJson (http://localhost:60638/dart_sdk.js:51299:19)
    at JsonDecoder.convert (http://localhost:60638/dart_sdk.js:49116:22)
    at JsonCodec.decode (http://localhost:60638/dart_sdk.js:48809:48)
    at Object.jsonDecode (http://localhost:60638/dart_sdk.js:51289:25)
    at opensea_dart.OpenSea.new.getCollectionStats
    (http://localhost:60638/packages/opensea_dart/opensea_dart.dart.lib.js:310:38)
    at getCollectionStats.next (<anonymous>)
    at http://localhost:60638/dart_sdk.js:40719:33
    at _RootZone.runUnary (http://localhost:60638/dart_sdk.js:40589:59)
    at _FutureListener.thenAwait.handleValue (http://localhost:60638/dart_sdk.js:35516:29)
    at handleValueCallback (http://localhost:60638/dart_sdk.js:36077:49)
    at _Future._propagateToListeners (http://localhost:60638/dart_sdk.js:36115:17)
    at [_completeWithValue] (http://localhost:60638/dart_sdk.js:35950:23)
    at async._AsyncCallbackEntry.new.callback (http://localhost:60638/dart_sdk.js:35984:35)
    at Object._microtaskLoop (http://localhost:60638/dart_sdk.js:40856:13)
    at _startMicrotaskLoop (http://localhost:60638/dart_sdk.js:40862:13)
    at http://localhost:60638/dart_sdk.js:36339:9
```

公式のexampleにかかれてある`token`がエラーで出力されたということ。

# 使用技術

* Windows 11
* Flutter 3
* Visual Studio Code 1.69
* opensea_dart 0.0.2

# 補足

APIを取得するにはOpensea公式からのGoogle Formに回答する必要があるため開発は断念。(**しかも開発目的やGitHubを共有しなければならず、即時に使えるわけではない**)

しばらくはWeb3の領域には着手しないかも...。