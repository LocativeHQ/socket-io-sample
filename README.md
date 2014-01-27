# Geofancy-Socket.io-Sample

This Sample demonstrates the use of Geofancy's Socket.io API in your Browser.

Of course you may you the Socket.io API with whatever infrastructure you'd like to.

Just point against https://my.geofancy.com:443 just like

```
var socket = io.connect('https://my.geofancy.com:443');
```

and authenticate by emitting the **session** event

```
socket.emit('session', {username: 'YOUR_USERNAME', password:'YOU_PASSWORD'});

socket.on('session', function (data) {
	console.log(data);
});
```

you'll get an **session_id** in case the authentication was successful

```
{session_id: "966f3e37aa1cf6ad634bc8912d7e8386e28e70b4"} 
```

or an error in case it was invalid

```
{error: "invalid credentials"} 
```

Nothing to do with that **session_id** as long as your session persists you'll receive events like e.g.

```
socket.on('fencelog', function (data) {
	if (data.event === 'add') {
		var fencelog = data.fencelog;
		// Your fencelog and you
	} else if (data.event === 'list') {
		var fencelogs = data.fencelogs;
		for (var i = fencelogs.length - 1; i >= 0; i--) {
			var fencelog = fencelogs[i];
			// Do whatever you want with the fencelog
		};
	}
});
```

Current the **list** event can be emitted manually by using the **https://my.geofancy.com/api/socket.io/fencelogs**  (authentication needed) endpoint which will just emit all your current Fencelogs for testing purpose.

As soon as a Fencelogs is added the **add** event is emitted providing the Fecenlogs's data to you.

