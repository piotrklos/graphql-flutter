# GraphQL Flutter
[![All Contributors](https://img.shields.io/badge/all_contributors-0-orange.svg?style=flat-square)](#contributors)

## Usage

In `main.dart`:

```dart
...

import 'package:graphql/graphql.dart';

void main() async {
  client = new Client(<YOUR_ENDPOINT>);
  client.apiToken = <YOUR_API_KEY>

  ...
}

...
```

Now create a quiry:

```dart
String readAllPeople = """
  query ReadAllPeople {
    allPeople(first: 4) {
      people {
        id
        name
      }
    }
  }
"""
  .replaceAll("\n", " ");
```

In your widget:

```dart
...

new Query(
  queries.readAllPeople,
  variables: {},
  polling: 10,
  builder: ({
    bool loading,
    var data,
    String error,
  }) {
    if (error != '') {
      return new Text(error);
    }

    if (loading) {
      return new Text('Loading');
    }

    // It can be either Map or List or Map
    List people = data['allPeople']['people'];

    return new ListView.builder(
      itemCount: people.length,
      itemBuilder: (context, index) {
        final item = people[index];

        return new Text(item['name']);
    });
  },
)

...
```

The StarWars API does not have mutations, but has the same syntax as a query where the first argument of the builder function is the mutation function. Just call it to trigger the mutations (Yeah we deliberetly stole this from react-apollo.)

```dart
...

new Mutation(
  <YOUR_MUTATION_STRING>,
  builder: (
    runMutation, {
    bool loading,
    var data,
    String error,
}) {
  return new FloatingActionButton(
    onPressed: () => runMutation({
      <YOUR_PARAMETERS>
    }),
    tooltip: 'Increment',
    child: new Icon(Icons.edit),
  );
}),

...
```

## Contributing

Feel free to open a PR with any suggetions! We'll be actively working on the library ourselfs.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!