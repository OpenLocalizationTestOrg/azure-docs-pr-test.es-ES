### <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js

Cree un nuevo archivo JavaScript denominado `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Agregar paquete de retransmisión NPM Hola

Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.

### <a name="write-some-code-toosend-messages"></a>Escribir un cierto código toosend mensajes

1. Agregue los siguiente hello `constants` toohello arriba del programa Hola a `sender.js` archivo.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Agregar Hola siguientes constantes toohello `sender.js` en el archivo de conexión híbrida Hola. Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.
   
   1. `const ns`-Hola espacio de nombres de retransmisión. Ser nombre de espacio de nombres completo de hello toouse seguro; Por ejemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nombre de Hola de conexión híbrida de Hola.
   3. `const keyrule`-nombre de Hola de clave SAS de Hola.
   4. `const key`-Hola valor de clave de SAS.

3. Agregar Hola después código toohello `sender.js` archivo:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Este es el aspecto que debería tener el archivo sender.js:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

