<div align="center">
  <a href="https://github.com/gamestdio/colyseus">
    <img src="https://github.com/gamestdio/colyseus/blob/master/media/header.png?raw=true" />
  </a>
  <br>
  <br>
  <a href="https://npmjs.com/package/colyseus">
    <img src="https://img.shields.io/npm/dm/colyseus.svg">
  </a>
  <a href="https://patreon.com/endel" title="Donate to this project using Patreon">
    <img src="https://img.shields.io/badge/patreon-donate-yellow.svg" alt="Patreon donate button" />
  </a>
  <a href="http://discuss.colyseus.io" title="Discuss on Forum">
    <img src="https://img.shields.io/badge/discuss-on%20forum-brightgreen.svg?style=flat&colorB=b400ff" alt="Discussion forum" />
  </a>
  <a href="https://gitter.im/gamestdio/colyseus">
    <img src="https://badges.gitter.im/gamestdio/colyseus.svg">
  </a>
  <h3>
     Multiplayer Game Client for Haxe <br /><a href="http://colyseus.io/docs/">View documentation</a>
  <h3>
</div>

## Usage

### Connecting to server:

```haxe
import io.colyseus.Client;
import io.colyseus.Room;

var client = new Client('ws://localhost:2657');
```

### Joining to a room:

```haxe
var room = client.join("room_name");
room.onJoin = function() {
    trace(client.id + " joined " + room.name);
}
```

### Listening to room state change:

Listening to entities being added/removed from the room:

```haxe
room.listen("entities/:id", function (change) {
    trace("new entity " +  change.path.id + " => " + change.value);
});
```

Listening to entity attributes being added/replaced/removed:

```haxe
room.listen("entities/:id/:attribute", function (change) {
    trace("entity " + change.path.id + " changed attribute " + change.path.attribute + " to " + change.value);
});
```

### Other room events

Room state has been updated:

```haxe
room.onStateChange = function(state) {
  // full new state avaialble on 'state' variable
}
```

Message broadcasted from server or directly to this client:

```haxe
room.onMessage = function (message) {
  trace(client.id + " received on " + room.name + ": " + message);
}
```

Server error occurred:

```haxe
room.onError = function() {
  trace(client.id + " couldn't join " + room.name);
}
```

The client left the room:

```haxe
room.onLeave = function() {
  trace(client.id + " left " + room.name);
}
```

## License

MIT