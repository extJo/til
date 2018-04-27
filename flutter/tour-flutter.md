# Flutter 둘러보기

android studio를 통해서 매우 편하게 Flutter를 개발할 수 있습니다.

Flutter 프로젝트를 생성하게 되면, `<project_dir>/lib/main.dart`가 생기게 되는데, `main.dart`가 start point 입니다.

main.dart를 천천히 둘러보겠습니다.

``` dart
// package import 부분
import 'package:flutter/material.dart';

// app의 메인 function 호출.
// react native에서 AppRegistry 컴포넌트를 통해서 앱 시작지점을 등록하는것과 비슷함.
void main() => runApp(new MyApp());

// Dart의 문법은 Java like 하므로, Java에 익숙하면 읽는데에는 부담이없다.
// parameter를 key-value 형식으로 넘겨줄 수도 있음.
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      theme: new ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: new MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

// widget의 경우에는 stateless한 것과 stateful한 것으로 나뉜다.
// state는 react, react-native의 state와 유사한 개념이다.
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => new _MyHomePageState();
}

// StatefuilWidget을 위해서, 새로운 class를 생성하여, state를 관리하게 만든다.
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  // Scaffold는 기초적인 material design을 구현한 visual layout structure이다.
  // 굉장히 material design에 대한 구현이 잘 되어있어서
  // 안드로이드는 금방금방 레이아웃을 만들 수 있겠다고 생각이 든다.
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
      body: new Center(
        child: new Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            new Text(
              'You have pushed the button this many times:',
            ),
            new Text(
              '$_counter',
              style: Theme.of(context).textTheme.display1,
            ),
          ],
        ),
      ),
      floatingActionButton: new FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: new Icon(Icons.add),
      ),
    );
  }
}
```

# 총평

* 전반적인 dart의 느낌은 Java + Javascript의 느낌이 강하게 든다.
* flutter에 들어가는 dart의 metarial 컴포넌트(?)들은 ios, android 똑같이 적용되기때문에, 각각의 플랫폼에 디자인 가이드를 맞추려면.. 음... 애를 좀 먹을수도 있겠다는 생각이든다.
* state로 컴포넌트의 상태변화를 보고, react, react-native의 영향을 많이 받았다고 느낄 수 있었음. ~~[(공식문서에서도 react-native 개발자를 위한 문서를 제공하고있다.)][flutter_for_rn]~~
* Dart를 충분히 익힐 수 있을지 걱정이 된다... ~~물론 react 모르고 react-native를 시작했던 나에겐.. 헤딩하면서 충분히 익힐 수 있을지도...~~
* state가 컴포넌트들에게 관여하므로, 프로젝트가 커지면서 state관리를 위해서 redux 또는 mobx같은 state관리를 위한 다른 라이브러리를 익혀야 하는 부분들이 생길 수 있다고 생각이 듦.



[flutter_for_rn]: https://flutter.io/flutter-for-react-native/