### <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js

Cree un nuevo archivo JavaScript denominado `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Agregar paquete de retransmisión NPM Hola

Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.

### <a name="write-some-code-tooreceive-messages"></a>Escribir un cierto código tooreceive mensajes

1. Agregar Hola después de la parte superior de la constante toohello de hello `listener.js` archivo.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Agregar Hola siguientes constantes toohello `listener.js` en el archivo de conexión híbrida Hola. Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.
   
   1. `const ns`-Hola espacio de nombres de retransmisión. Ser nombre de espacio de nombres completo de hello toouse seguro; Por ejemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nombre de Hola de conexión híbrida de Hola.
   3. `const keyrule`-nombre de Hola de clave SAS de Hola.
   4. `const key`-Hola valor de clave de SAS.

3. Agregar Hola después código toohello `listener.js` archivo:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Este es el aspecto que debería tener el archivo listener.cs:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

