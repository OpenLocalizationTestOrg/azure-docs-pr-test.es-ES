<span data-ttu-id="45ff0-101">emulador de almacenamiento de Hello es compatible con una cuenta única fija y una clave de autenticación conocido para la autenticación de clave compartida.</span><span class="sxs-lookup"><span data-stu-id="45ff0-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="45ff0-102">Esta cuenta y clave son Hola solo Shared Key las credenciales de admiten para su uso con el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="45ff0-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="45ff0-103">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="45ff0-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="45ff0-104">clave de autenticación de Hello compatible con el emulador de almacenamiento de hello está pensado únicamente para la funcionalidad de Hola la prueba de su código de autenticación de cliente.</span><span class="sxs-lookup"><span data-stu-id="45ff0-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="45ff0-105">No responde a ningún propósito de seguridad.</span><span class="sxs-lookup"><span data-stu-id="45ff0-105">It does not serve any security purpose.</span></span> <span data-ttu-id="45ff0-106">No puede usar su cuenta de almacenamiento de producción y la clave con el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="45ff0-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="45ff0-107">No se debe usar cuenta de hello de desarrollo con datos de producción.</span><span class="sxs-lookup"><span data-stu-id="45ff0-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="45ff0-108">emulador de almacenamiento de Hello admite solo la conexión a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="45ff0-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="45ff0-109">Sin embargo, HTTPS es hello recomendada protocolo para tener acceso a recursos en una cuenta de almacenamiento de Azure de producción.</span><span class="sxs-lookup"><span data-stu-id="45ff0-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="45ff0-110">Conectar toohello cuenta del emulador mediante un acceso directo</span><span class="sxs-lookup"><span data-stu-id="45ff0-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="45ff0-111">Hola más fácil manera tooconnect toohello emulador de almacenamiento de la aplicación es tooconfigure una cadena de conexión en el archivo de configuración de la aplicación que hace referencia el acceso directo de hello `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="45ff0-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="45ff0-112">Este es un ejemplo de un emulador de almacenamiento de toohello de cadena de conexión en un *app.config* archivo:</span><span class="sxs-lookup"><span data-stu-id="45ff0-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="45ff0-113">Conectar toohello cuenta del emulador mediante la clave y el nombre de cuenta conocida de Hola</span><span class="sxs-lookup"><span data-stu-id="45ff0-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="45ff0-114">toocreate una cadena de conexión que referencias Hola nombre de la cuenta de emulador y clave, debe especificar los puntos de conexión de Hola para cada uno de hello de servicios le interese toouse desde el emulador de hello en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="45ff0-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="45ff0-115">Esto es necesario para que la cadena de conexión de hello hará referencia a los extremos de emulador de hello, que son diferentes de las de una cuenta de almacenamiento de producción.</span><span class="sxs-lookup"><span data-stu-id="45ff0-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="45ff0-116">Por ejemplo, valor de saludo de la cadena de conexión tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="45ff0-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="45ff0-117">Este valor es contextual toohello idénticos mostrado anteriormente, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="45ff0-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="45ff0-118">Especificación de un servidor proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="45ff0-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="45ff0-119">También puede especificar un toouse de proxy HTTP cuando se está probando su servicio con el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="45ff0-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="45ff0-120">Esto puede ser útil para observar solicitudes y respuestas HTTP mientras está depurando operaciones con los servicios de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="45ff0-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="45ff0-121">toospecify un proxy, agregar hello `DevelopmentStorageProxyUri` opción toohello cadena de conexión y establecer su URI del servidor de proxy toohello del valor.</span><span class="sxs-lookup"><span data-stu-id="45ff0-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="45ff0-122">Por ejemplo, aquí es una cadena de conexión que señala el emulador de almacenamiento de toohello y configura a un servidor proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="45ff0-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

