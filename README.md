# fluro_web
flutter fluro 1.5.1 的 web 版本,
copy version from [fluro 1.5.1](https://github.com/theyakka/fluro) and modify it to web version

## Features

- Simple route navigation
- Function handlers (map to a function instead of a route)
- Wildcard parameter matching
- Querystring parameter parsing
- Common transitions built-in
- Simple custom transition creation

## Version compatability

See CHANGELOG for all breaking (and non-breaking) changes.

## Getting started

You should ensure that you add the router as a dependency in your flutter project.
```yaml
dependencies:
 fluro_web: "^1.5.1"
```

You can also reference the git repo directly if you want:
```yaml
dependencies:
 fluro_web:
   git: https://github.com/ryan730/fluro_web
```

You should then run `pub get` or update your packages in IntelliJ.

## Example Project

There is a pretty sweet example project in the `example` folder. Check it out. Otherwise, keep reading to get up and running.

## Setting up

First, you should define a new `Router` object by initializing it as such:
```dart
final router = Router();
```
It may be convenient for you to store the router globally/statically so that
you can access the router in other areas in your application.

After instantiating the router, you will need to define your routes and your route handlers:
```dart
var usersHandler = Handler(handlerFunc: (BuildContext context, Map<String, dynamic> params) {
  return UsersScreen(params["id"][0]);
});

void defineRoutes(Router router) {
  router.define("/users/:id", handler: usersHandler);

  // it is also possible to define the route transition to use
  // router.define("users/:id", handler: usersHandler, transitionType: TransitionType.inFromLeft);
}
```

In the above example, the router will intercept a route such as
`/users/1234` and route the application to the `UsersScreen` passing
the value `1234` as a parameter to that screen.

## Navigating

You can use the `Router` with the `MaterialApp.onGenerateRoute` parameter
via the `Router.generator` function. To do so, pass the function reference to
the `onGenerate` parameter like: `onGenerateRoute: router.generator`.

You can then use `Navigator.push` and the flutter routing mechanism will match the routes
for you.

You can also manually push to a route yourself. To do so:

```dart
router.navigateTo(context, "/users/1234", transition: TransitionType.fadeIn);
```