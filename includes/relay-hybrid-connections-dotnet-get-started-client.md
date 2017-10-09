### <a name="create-a-console-application"></a><span data-ttu-id="db492-101">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="db492-101">Create a console application</span></span>

<span data-ttu-id="db492-102">En primer lugar, inicie Visual Studio y cree un proyecto **Console app (.NET Framework)** nuevo.</span><span class="sxs-lookup"><span data-stu-id="db492-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="db492-103">Agregar paquete de NuGet de retransmisión de Hola</span><span class="sxs-lookup"><span data-stu-id="db492-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="db492-104">Haga clic en proyecto de hello recién creado y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="db492-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="db492-105">Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.Relay" y seleccione hello **Microsoft Azure retransmisión** elemento.</span><span class="sxs-lookup"><span data-stu-id="db492-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="db492-106">Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db492-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="db492-107">Escribir un cierto código toosend mensajes</span><span class="sxs-lookup"><span data-stu-id="db492-107">Write some code toosend messages</span></span>

1. <span data-ttu-id="db492-108">Reemplazar existente hello `using` instrucciones en parte superior de hello del archivo Program.cs de hello con siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="db492-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="db492-109">Agregar constantes toohello `Program` clase para obtener detalles de conexión de hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="db492-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="db492-110">Reemplace los marcadores de posición de hello corchetes con valores de hello que obtuvo al crear conexión híbrida de Hola.</span><span class="sxs-lookup"><span data-stu-id="db492-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="db492-111">Ser nombre de espacio de nombres completo de hello toouse seguro:</span><span class="sxs-lookup"><span data-stu-id="db492-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="db492-112">Agregar Hola siguiendo el método toohello `Program` clase:</span><span class="sxs-lookup"><span data-stu-id="db492-112">Add hello following method toohello `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
        // Create a new hybrid connection client
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Initiate hello connection
        var relayConnection = await client.CreateConnectionAsync();
   
        // We run two concurrent loops on hello connection. One 
        // reads input from hello console and writes it toohello connection 
        // with a stream writer. hello other reads lines of input from hello 
        // connection with a stream reader and writes them toohello console. 
        // Entering a blank line will shut down hello write task after 
        // sending it toohello server. hello server will then cleanly shut down
        // hello connection which will terminate hello read task.
   
        var reads = Task.Run(async () => {
            // Initialize hello stream reader over hello connection
            var reader = new StreamReader(relayConnection);
            var writer = Console.Out;
            do
            {
                // Read a full line of UTF-8 text up toonewline
                string line = await reader.ReadLineAsync();
                // if hello string is empty or null, we are done.
                if (String.IsNullOrEmpty(line))
                    break;
                // Write toohello console
                await writer.WriteLineAsync(line);
            }
            while (true);
        });
   
        // Read from hello console and write toohello hybrid connection
        var writes = Task.Run(async () => {
            var reader = Console.In;
            var writer = new StreamWriter(relayConnection) { AutoFlush = true };
            do
            {
                // Read a line form hello console
                string line = await reader.ReadLineAsync();
                // Write hello line out, also when it's empty
                await writer.WriteLineAsync(line);
                // Quit when hello line was empty
                if (String.IsNullOrEmpty(line))
                    break;
            }
            while (true);
        });
   
        // Wait for both tasks toocomplete
        await Task.WhenAll(reads, writes);
        await relayConnection.CloseAsync(CancellationToken.None);
    }
    ```
4. <span data-ttu-id="db492-113">Agregar Hola después de la línea de código toohello `Main` método Hola `Program` clase.</span><span class="sxs-lookup"><span data-stu-id="db492-113">Add hello following line of code toohello `Main` method in hello `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="db492-114">Este es el aspecto que debería tener Program.cs.</span><span class="sxs-lookup"><span data-stu-id="db492-114">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
                // Create a new hybrid connection client
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Initiate hello connection
                var relayConnection = await client.CreateConnectionAsync();
   
                // We run two conucrrent loops on hello connection. One 
                // reads input from hello console and writes it toohello connection 
                // with a stream writer. hello other reads lines of input from hello 
                // connection with a stream reader and writes them toohello console. 
                // Entering a blank line will shut down hello write task after 
                // sending it toohello server. hello server will then cleanly shut down
                // hello connection which will terminate hello read task.
   
                var reads = Task.Run(async () => {
                    // Initialize hello stream reader over hello connection
                    var reader = new StreamReader(relayConnection);
                    var writer = Console.Out;
                    do
                    {
                        // Read a full line of UTF-8 text up toonewline
                        string line = await reader.ReadLineAsync();
                        // If hello string is empty or null, we are done.
                        if (String.IsNullOrEmpty(line))
                            break;
                        // Write toohello console
                        await writer.WriteLineAsync(line);
                    }
                    while (true);
                });
   
                // Read from hello console and write toohello hybrid connection
                var writes = Task.Run(async () => {
                    var reader = Console.In;
                    var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                    do
                    {
                        // Read a line form hello console
                        string line = await reader.ReadLineAsync();
                        // Write hello line out, also when it's empty
                        await writer.WriteLineAsync(line);
                        // Quit when hello line was empty
                        if (String.IsNullOrEmpty(line))
                            break;
                    }
                    while (true);
                });
   
                // Wait for both tasks toocomplete
                await Task.WhenAll(reads, writes);
                await relayConnection.CloseAsync(CancellationToken.None);
            }
        }
    }
    ```

