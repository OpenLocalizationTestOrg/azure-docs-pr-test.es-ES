### <a name="create-a-nodejs-application"></a><span data-ttu-id="9d8e8-101">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="9d8e8-101">Create a Node.js application</span></span>

<span data-ttu-id="9d8e8-102">Cree un nuevo archivo JavaScript denominado `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="9d8e8-103">Agregar paquete de retransmisión NPM Hola</span><span class="sxs-lookup"><span data-stu-id="9d8e8-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="9d8e8-104">Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="9d8e8-105">Escribir un cierto código toosend mensajes</span><span class="sxs-lookup"><span data-stu-id="9d8e8-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="9d8e8-106">Agregue los siguiente hello `constants` toohello arriba del programa Hola a `sender.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="9d8e8-107">Agregar Hola siguientes constantes toohello `sender.js` en el archivo de conexión híbrida Hola.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="9d8e8-108">Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="9d8e8-109">`const ns`-Hola espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="9d8e8-110">Ser nombre de espacio de nombres completo de hello toouse seguro; Por ejemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="9d8e8-111">`const path`-nombre de Hola de conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="9d8e8-112">`const keyrule`-nombre de Hola de clave SAS de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="9d8e8-113">`const key`-Hola valor de clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="9d8e8-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="9d8e8-114">Agregar Hola después código toohello `sender.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="9d8e8-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="9d8e8-115">Este es el aspecto que debería tener el archivo sender.js:</span><span class="sxs-lookup"><span data-stu-id="9d8e8-115">Here is what your sender.js file should look like:</span></span>
   
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

