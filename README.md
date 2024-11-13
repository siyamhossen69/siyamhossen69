import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  HomePageState createState() => HomePageState();
}

class HomePageState extends State<HomePage> {
  String display = "0";
  int firstOperand = 0;
  int secondOperand = 0;
  String operator = "";

  void onButtonPressed(String value) {
    setState(() {
      if (value == 'C') {
        display = "0";
        firstOperand = 0;
        secondOperand = 0;
        operator = "";
      } else if (value == '+' || value == '-' || value == '*' || value == '/') {
        firstOperand = int.parse(display);
        operator = value;
        display = "0";
      } else if (value == '=') {
        secondOperand = int.parse(display);
        switch (operator) {
          case '+':
            display = (firstOperand + secondOperand).toString();
            break;
          case '-':
            display = (firstOperand - secondOperand).toString();
            break;
          case '*':
            display = (firstOperand * secondOperand).toString();
            break;
          case '/':
            display = secondOperand != 0
                ? (firstOperand / secondOperand).toString()
                : "Error";
            break;
        }
        firstOperand = 0;
        secondOperand = 0;
        operator = "";
      } else {
        display = display == "0" ? value : display + value;
      }
    });
  }

  Widget buildButton(String value) {
    return Expanded(
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: ElevatedButton(
          onPressed: () => onButtonPressed(value),
          style: ElevatedButton.styleFrom(
            padding: const EdgeInsets.all(24),
          ),
          child: Text(
            value,
            style: const TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Calculator"),
        backgroundColor: Colors.black54,
      ),
      body: Column(
        children: <Widget>[
          Expanded(
            child: Container(
              alignment: Alignment.bottomRight,
              padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 36),
              child: Text(
                display,
                style: const TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
              ),
            ),
          ),
          Row(
            children: <Widget>[
              buildButton("7"),
              buildButton("8"),
              buildButton("9"),
              buildButton("+"),
            ],
          ),
          Row(
            children: <Widget>[
              buildButton("4"),
              buildButton("5"),
              buildButton("6"),
              buildButton("-"),
            ],
          ),
          Row(
            children: <Widget>[
              buildButton("1"),
              buildButton("2"),
              buildButton("3"),
              buildButton("*"),
            ],
          ),
          Row(
            children: <Widget>[
              buildButton("C"),
              buildButton("0"),
              buildButton("="),
              buildButton("/"),
            ],
          ),
        ],
      ),
    );
  }
}
