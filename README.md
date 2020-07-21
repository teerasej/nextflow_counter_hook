# nextflow_counter_hook

A counter application that use flutter_hook package to demonstrate how its power. 

## What I did with this app?

I modified the counter template which created whenever you start a new project. 

### 1. Change the extended one

To use flutter_hook. I changed `MyHomePage` class to extend `HookWidget` instead of `StatefulWidget` 


#### original 

```dart
class MyHomePage extends StatefulWidget 
```

#### modified 

```dart
class MyHomePage extends HookWidget 
```

### 2. Use Flutter hook in `build()` method

with this change, we have no need to implement `MyHomePageState` anymore. 

The `HookWidget` itself has build method, where you can use hook.

```dart
class MyHomePage extends HookWidget {
  @override
  Widget build(BuildContext context) {
    
    // useState is one of popular hook, it created a state object, and stay for a lifetime. 
    // Please be noticed that we have to use hook inside build() method, or you will got error.ß 
    var _counter = useState(0);

    return Scaffold(
      appBar: AppBar(
        title: Text('Nextflow React Hook 1'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '${_counter.value}',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
            // just make change to the state object, leave the rest for Hook widget! 
          _counter.value = _counter.value + 1;
        },
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ), 
    );
  }
}
```

