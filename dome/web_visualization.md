# Overview

Web visualization supports rendering and interacting with running Ignition
Gazebo simulations. You may find web visualization useful
when interacting with remote or headless Ignition Gazebo simulations. No
additionally dependencies, other than a browser and internet connection, are
required.

## How to use web visualization

The following steps will guide you through the process of running Ignition
Gazebo with a websocket server and connecting to the websocket for
visualization. 

1. Start an Ignition Gazebo instance as usual. We will use the `fuel.sdf`
   world and run it headless.
```
ign gazebo -v 4 -s -r fuel.sdf
```

1. Create an Ignition Launch file with the websocket server plugin.
```
echo "<?xml version='1.0'?>
<ignition version='1.0'>
  <plugin name='ignition::launch::WebsocketServer'
          filename='ignition-launch-websocket-server'>
    <port>9002</port>
  </plugin>
</ignition>" > websocket.ign
```

1. Run the websocket server using
```
ign launch -v 4 websocket.ign
```

1. Visualize the simulation by going to
   [https://app.ignitionrobotics.org/visualization](https://app.ignitionrobotics.org/visualization) and pressing the Connect button.

1. It may take a few seconds for the scene to load. Your browser needs to
   fetch all of the models in the world.

## Websocket server customization

The following parameters are available in the websocket server plugin.

  * `<admin_authorization_key>` : If this is set, then a connection must provide the matching key using an "auth" call on the websocket. If the `<authorization_key>` is set, then the connection can provide that key.
  * `<authorization_key>` : If this is set, then a connection must provide the
matching key using an "auth" call on the websocket. If the `<admin_authorization_key>` is set, then the connection can provide that key.
  * `<max_connections>` : An integer that is the maximum number of simultaneous connections.
  * `<port>` : An integer that is websocket port.
  * `<publication_hz>` : An integer that is the maximum publication hertz rate.