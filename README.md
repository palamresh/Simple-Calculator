# Simple-Calculator


import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int first = 0;
  int second = 0;
  String todisplay = "";
  String operatortoperform = "";
  String res = "";

  void buttonClick(String botton) {
    if (botton == "C") {
      first = 0;
      second = 0;
      todisplay = "";
      //   operatortoperform = "";
      res = "";
    } else if (botton == "+" ||
        botton == "-" ||
        botton == "*" ||
        botton == "/") {
      first = int.parse(todisplay.toString());
      res = "";
      operatortoperform = botton;
    } else if (botton == "=") {
      second = int.parse(todisplay.toString());
      if (operatortoperform == "+") {
        res = (first + second).toString();
      }
      if (operatortoperform == "-") {
        res = (first - second).toString();
      }
      if (operatortoperform == "*") {
        res = (first * second).toString();
      }
      if (operatortoperform == "/") {
        res = (first / second).toString();
      }
    } else {
      res = int.parse(todisplay + botton).toString();
    }
    setState(() {
      todisplay = res;
    });
  }

  Widget cost(String botton) {
    return Expanded(
      child: SizedBox(
        height: 60.0,
        width: 80,
        child: OutlinedButton(
          onPressed: () => buttonClick(botton),
          child: Text(
            botton,
            style: TextStyle(fontSize: 20.0),
          ),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Center(
        //
        child: Container(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.end,
            children: <Widget>[
              Expanded(
                  child: Container(
                padding: EdgeInsets.all(10.0),
                alignment: Alignment.bottomRight,
                child: Text(
                  "$todisplay",
                  style: TextStyle(fontSize: 30.0),
                ),
              )),
              Row(
                children: [
                  cost("9"),
                  cost("8"),
                  cost("7"),
                  cost("+"),
                ],
              ),
              Row(
                children: [
                  cost("6"),
                  cost("5"),
                  cost("4"),
                  cost("-"),
                ],
              ),
              Row(
                children: [
                  cost("3"),
                  cost("2"),
                  cost("1"),
                  cost("*"),
                ],
              ),
              Row(
                children: [
                  cost("C"),
                  cost("0"),
                  cost("="),
                  cost("/"),
                ],
              )
            ],
          ),
        ),
      ),
    );
  }
}
