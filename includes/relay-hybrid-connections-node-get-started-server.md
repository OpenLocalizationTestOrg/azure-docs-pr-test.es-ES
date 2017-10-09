### <a name="create-a-nodejs-application"></a><span data-ttu-id="29752-101">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="29752-101">Create a Node.js application</span></span>

<span data-ttu-id="29752-102">Cree un nuevo archivo JavaScript denominado `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="29752-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="29752-103">Agregar paquete de retransmisión NPM Hola</span><span class="sxs-lookup"><span data-stu-id="29752-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="29752-104">Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="29752-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="29752-105">Escribir un cierto código tooreceive mensajes</span><span class="sxs-lookup"><span data-stu-id="29752-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="29752-106">Agregar Hola después de la parte superior de la constante toohello de hello `listener.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="29752-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="29752-107">Agregar Hola siguientes constantes toohello `listener.js` en el archivo de conexión híbrida Hola.</span><span class="sxs-lookup"><span data-stu-id="29752-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="29752-108">Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="29752-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="29752-109">`const ns`-Hola espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="29752-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="29752-110">Ser nombre de espacio de nombres completo de hello toouse seguro; Por ejemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="29752-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="29752-111">`const path`-nombre de Hola de conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="29752-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="29752-112">`const keyrule`-nombre de Hola de clave SAS de Hola.</span><span class="sxs-lookup"><span data-stu-id="29752-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="29752-113">`const key`-Hola valor de clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="29752-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="29752-114">Agregar Hola después código toohello `listener.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="29752-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="29752-115">Este es el aspecto que debería tener el archivo listener.cs:</span><span class="sxs-lookup"><span data-stu-id="29752-115">Here is what your listener.js file should look like:</span></span>
   
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

