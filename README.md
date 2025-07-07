import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  MyApp({Key? key}) : super(key: key);

  @override
  State createState() => _MyAppState();
}

class _MyAppState extends State<MyApp>{
  var num1 = TextEditingController();
  List contentadd = [];
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'TODO App',
      color: Colors.amber,
      home: Scaffold(
        appBar: AppBar(
          centerTitle: true,

          title: const Text(
            'TODO',
            style: TextStyle(
              fontSize: 23,
              fontWeight: FontWeight.bold,
              color: Colors.black,
              backgroundColor: Colors.blue,
            ),
          ),
        ),
        body: SingleChildScrollView(
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              SizedBox(height: 12),
              Container(
                padding: EdgeInsets.symmetric(horizontal: 9, vertical: 6),
                child: TextField(
                  controller: num1,
                  decoration: InputDecoration(
                    border: OutlineInputBorder(),
                    prefixIcon: Icon(Icons.text_fields),
                    labelText: 'Enter the text',
                  ),
                  keyboardType: TextInputType.text,
                ),
              ),
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: [
                  ElevatedButton(
                    onPressed: () {
                      setState(() {
                        var text = num1.text;
                        contentadd.add(text);
                        num1.clear();
                      });
                    },
                    child: Text('Add', style: TextStyle(fontSize: 20)),
                  ),
                  ElevatedButton(
                    onPressed: () {
                      setState(() {
                        contentadd = [];
                        num1.clear();
                      });
                    },
                    child: Text('Clear', style: TextStyle(fontSize: 20)),
                  ),
                ],
              ),
              SizedBox(height: 30),
              Text(
                'Today Task is',
                style: TextStyle(
                  fontSize: 24,
                  fontFamily: 'Ubuntu',
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(height: 20),
              ListView.builder(
                shrinkWrap: true,
                physics: NeverScrollableScrollPhysics(),
                itemCount: contentadd.length,
                itemBuilder: (context, index) {
                  return Padding(
                    padding: EdgeInsetsGeometry.only(bottom: 20),
                    child: Container(
                      margin: EdgeInsets.only(left: 12, right: 12),
                      padding: EdgeInsets.all(9),
                      decoration: BoxDecoration(
                        color: Color(0xFFF0F8FF),
                        borderRadius: BorderRadius.circular(8),
                        boxShadow: [
                          BoxShadow(
                            color: Colors.black,
                            blurRadius: 3,
                            spreadRadius: 2,
                          ),
                        ],
                      ),
                      child: Row(
                        children: [
                          Text(
                            '=> ',
                            style: TextStyle(
                              fontSize: 18,
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          Flexible(
                            child: Text(
                              contentadd[index],
                              style: TextStyle(
                                fontSize: 18,
                                fontWeight: FontWeight.w600,
                              ),
                            ),
                          ),
                        ],
                      ),
                    ),
                  );
                },
              ),
              SizedBox(height: MediaQuery.of(context).padding.bottom),
            ],
          ),
        ),
      ),
    );
  }
}
