### <a name="create-a-nodejs-application"></a><span data-ttu-id="57164-101">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="57164-101">Create a Node.js application</span></span>

<span data-ttu-id="57164-102">Cree un nuevo archivo JavaScript denominado `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="57164-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="57164-103">Adición del paquete Relay NPM</span><span class="sxs-lookup"><span data-stu-id="57164-103">Add the Relay NPM package</span></span>

<span data-ttu-id="57164-104">Ejecute `npm install hyco-ws` desde un símbolo del sistema del nodo en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="57164-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="57164-105">Escritura de código para enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="57164-105">Write some code to send messages</span></span>

1. <span data-ttu-id="57164-106">Agregue lo siguiente `constants` en la parte superior del archivo `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="57164-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="57164-107">Agregue la siguientes constantes al archivo `sender.js` para los detalles de la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="57164-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="57164-108">Reemplace los marcadores de posición entre corchetes por los valores que obtuvo al crear la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="57164-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="57164-109">`const ns`: el espacio de nombres de Relay.</span><span class="sxs-lookup"><span data-stu-id="57164-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="57164-110">Asegúrese de utilizar el nombre de espacio de nombres completo; por ejemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="57164-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="57164-111">`const path`: el nombre de la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="57164-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="57164-112">`const keyrule`: el nombre de la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="57164-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="57164-113">`const key`: el valor de la clave SAS.</span><span class="sxs-lookup"><span data-stu-id="57164-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="57164-114">Agregue el siguiente código al archivo `sender.js`:</span><span class="sxs-lookup"><span data-stu-id="57164-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="57164-115">Este es el aspecto que debería tener el archivo sender.js:</span><span class="sxs-lookup"><span data-stu-id="57164-115">Here is what your sender.js file should look like:</span></span>
   
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

