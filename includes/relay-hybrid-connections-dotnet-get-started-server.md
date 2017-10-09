### <a name="create-a-console-application"></a><span data-ttu-id="b25f8-101">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="b25f8-101">Create a console application</span></span>

<span data-ttu-id="b25f8-102">En primer lugar, inicie Visual Studio y cree un proyecto **Console app (.NET Framework)** nuevo.</span><span class="sxs-lookup"><span data-stu-id="b25f8-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="b25f8-103">Agregar paquete de NuGet de retransmisión de Hola</span><span class="sxs-lookup"><span data-stu-id="b25f8-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="b25f8-104">Haga clic en proyecto de hello recién creado y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b25f8-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b25f8-105">Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.Relay" y seleccione hello **Microsoft Azure retransmisión** elemento.</span><span class="sxs-lookup"><span data-stu-id="b25f8-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="b25f8-106">Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b25f8-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="b25f8-107">Escribir un cierto código tooreceive mensajes</span><span class="sxs-lookup"><span data-stu-id="b25f8-107">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="b25f8-108">Reemplazar existente hello `using` instrucciones en parte superior de hello del archivo Program.cs de hello con siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b25f8-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="b25f8-109">Agregar constantes toohello `Program` clase para obtener detalles de conexión de hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="b25f8-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="b25f8-110">Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="b25f8-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="b25f8-111">Ser nombre de espacio de nombres completo de hello toouse seguro:</span><span class="sxs-lookup"><span data-stu-id="b25f8-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="b25f8-112">Agregar Hola siguiendo el método llamado `ProcessMessagesOnConnection` toohello `Program` clase:</span><span class="sxs-lookup"><span data-stu-id="b25f8-112">Add hello following method called `ProcessMessagesOnConnection` toohello `Program` class:</span></span>
   
    ```csharp
    // Method is used tooinitiate connection
    private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
    {
        Console.WriteLine("New session");
   
        // hello connection is a fully bidrectional stream. 
        // We put a stream reader and a stream writer over it 
        // which allows us tooread UTF-8 text that comes from 
        // hello sender and toowrite text replies back.
        var reader = new StreamReader(relayConnection);
        var writer = new StreamWriter(relayConnection) { AutoFlush = true };
        while (!cts.IsCancellationRequested)
        {
            try
            {
                // Read a line of input until a newline is encountered
                var line = await reader.ReadLineAsync();
   
                if (string.IsNullOrEmpty(line))
                {
                    // If there's no input data, we will signal that 
                    // we will no longer send data on this connection
                    // and then break out of hello processing loop.
                    await relayConnection.ShutdownAsync(cts.Token);
                    break;
                }
   
                // Output hello line on hello console
                Console.WriteLine(line);
   
                // Write hello line back toohello client, prepending "Echo:"
                await writer.WriteLineAsync($"Echo: {line}");
            }
            catch (IOException)
            {
                // Catch an IO exception that is likely caused because
                // hello client disconnected.
                Console.WriteLine("Client closed connection");
                break;
            }
        }
   
        Console.WriteLine("End session");
   
        // Closing hello connection
        await relayConnection.CloseAsync(cts.Token);
    }
    ```
4. <span data-ttu-id="b25f8-113">Agregue otro método llamado `RunAsync` toohello `Program` de la clase, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b25f8-113">Add another method called `RunAsync` toohello `Program` class, as follows:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe toohello status events
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
        // Opening hello listener will establish hello control channel to
        // hello Azure Relay service. hello control channel will be continuously 
        // maintained and reestablished when connectivity is disrupted.
        await listener.OpenAsync(cts.Token);
        Console.WriteLine("Server listening");
   
        // Providing callback for cancellation token that will close hello listener.
        cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
        // Start a new thread that will continuously read hello console.
        new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
        // Accept hello next available, pending connection request. 
        // Shutting down hello listener will allow a clean exit with 
        // this method returning null
        while (true)
        {
            var relayConnection = await listener.AcceptConnectionAsync();
            if (relayConnection == null)
            {
                break;
            }
   
            ProcessMessagesOnConnection(relayConnection, cts);
        }
   
        // Close hello listener after we exit hello processing loop
        await listener.CloseAsync(cts.Token);
    }
    ```
5. <span data-ttu-id="b25f8-114">Agregar Hola después de la línea de código toohello `Main` método Hola `Program` clase:</span><span class="sxs-lookup"><span data-stu-id="b25f8-114">Add hello following line of code toohello `Main` method in hello `Program` class:</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="b25f8-115">Este es el aspecto que debería tener el archivo Program.cs completado:</span><span class="sxs-lookup"><span data-stu-id="b25f8-115">Here is what your completed Program.cs file should look like:</span></span>
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var cts = new CancellationTokenSource();
   
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Subscribe toohello status events
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
                // Opening hello listener will establish hello control channel to
                // hello Azure Relay service. hello control channel will be continuously 
                // maintained and reestablished when connectivity is disrupted.
                await listener.OpenAsync(cts.Token);
                Console.WriteLine("Server listening");
   
                // Providing callback for cancellation token that will close hello listener.
                cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
                // Start a new thread that will continuously read hello console.
                new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
                // Accept hello next available, pending connection request. 
                // Shutting down hello listener will allow a clean exit with 
                // this method returning null
                while (true)
                {
                    var relayConnection = await listener.AcceptConnectionAsync();
                    if (relayConnection == null)
                    {
                        break;
                    }
   
                    ProcessMessagesOnConnection(relayConnection, cts);
                }
   
                // Close hello listener after we exit hello processing loop
                await listener.CloseAsync(cts.Token);
            }
   
            private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
            {
                Console.WriteLine("New session");
   
                // hello connection is a fully bidrectional stream. 
                // We put a stream reader and a stream writer over it 
                // which allows us tooread UTF-8 text that comes from 
                // hello sender and toowrite text replies back.
                var reader = new StreamReader(relayConnection);
                var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                while (!cts.IsCancellationRequested)
                {
                    try
                    {
                        // Read a line of input until a newline is encountered
                        var line = await reader.ReadLineAsync();
   
                        if (string.IsNullOrEmpty(line))
                        {
                            // If there's no input data, we will signal that 
                            // we will no longer send data on this connection
                            // and then break out of hello processing loop.
                            await relayConnection.ShutdownAsync(cts.Token);
                            break;
                        }
   
                        // Output hello line on hello console
                        Console.WriteLine(line);
   
                        // Write hello line back toohello client, prepending "Echo:"
                        await writer.WriteLineAsync($"Echo: {line}");
                    }
                    catch (IOException)
                    {
                        // Catch an IO exception that is likely caused because
                        // hello client disconnected.
                        Console.WriteLine("Client closed connection");
                        break;
                    }
                }
   
                Console.WriteLine("End session");
   
                // Closing hello connection
                await relayConnection.CloseAsync(cts.Token);
            }
        }
    }
    ```

