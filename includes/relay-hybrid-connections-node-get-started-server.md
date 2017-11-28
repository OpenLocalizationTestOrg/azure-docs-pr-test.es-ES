### <a name="create-a-nodejs-application"></a><span data-ttu-id="c9ccc-101">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="c9ccc-101">Create a Node.js application</span></span>

<span data-ttu-id="c9ccc-102">Cree un nuevo archivo JavaScript denominado `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="c9ccc-103">Adición del paquete Relay NPM</span><span class="sxs-lookup"><span data-stu-id="c9ccc-103">Add the Relay NPM package</span></span>

<span data-ttu-id="c9ccc-104">Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="c9ccc-105">Escritura de código para recibir mensajes</span><span class="sxs-lookup"><span data-stu-id="c9ccc-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="c9ccc-106">Agregue la siguiente constante al principio del archivo `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="c9ccc-107">Agregue la siguientes constantes al archivo `listener.js` para los detalles de la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="c9ccc-108">Reemplace los marcadores de posición entre corchetes por los valores que obtuvo al crear la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="c9ccc-109">`const ns`: el espacio de nombres de Relay.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="c9ccc-110">Asegúrese de utilizar el nombre de espacio de nombres completo; por ejemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="c9ccc-111">`const path`: el nombre de la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="c9ccc-112">`const keyrule`: el nombre de la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="c9ccc-113">`const key`: el valor de la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="c9ccc-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="c9ccc-114">Agregue el siguiente código al archivo `listener.js`:</span><span class="sxs-lookup"><span data-stu-id="c9ccc-114">Add the following code to the `listener.js` file:</span></span>
   
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
    <span data-ttu-id="c9ccc-115">Este es el aspecto que debería tener el archivo listener.cs:</span><span class="sxs-lookup"><span data-stu-id="c9ccc-115">Here is what your listener.js file should look like:</span></span>
   
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

