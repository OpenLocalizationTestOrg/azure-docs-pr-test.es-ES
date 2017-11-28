<span data-ttu-id="29ea4-101">El emulador de almacenamiento es compatible con una sola cuenta fija y una clave de autenticación ya conocida para autenticación de clave compartida.</span><span class="sxs-lookup"><span data-stu-id="29ea4-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="29ea4-102">Esta cuenta y clave son las únicas credenciales de clave compartida que se admiten para su uso con el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="29ea4-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span></span> <span data-ttu-id="29ea4-103">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="29ea4-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="29ea4-104">La clave de autenticación admitida por el emulador de almacenamiento está pensada para comprobar únicamente la funcionalidad de su código de autenticación de cliente.</span><span class="sxs-lookup"><span data-stu-id="29ea4-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span></span> <span data-ttu-id="29ea4-105">No responde a ningún propósito de seguridad.</span><span class="sxs-lookup"><span data-stu-id="29ea4-105">It does not serve any security purpose.</span></span> <span data-ttu-id="29ea4-106">A parte, no puede utilizar la cuenta de almacenamiento y la clave de producción con el emulador.</span><span class="sxs-lookup"><span data-stu-id="29ea4-106">You cannot use your production storage account and key with the storage emulator.</span></span> <span data-ttu-id="29ea4-107">Se debe tener en cuenta que no se puede utilizar la cuenta de desarrollo con datos de producción.</span><span class="sxs-lookup"><span data-stu-id="29ea4-107">You should not use the development account with production data.</span></span>
> 
> <span data-ttu-id="29ea4-108">El emulador de almacenamiento admite solo la conexión a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="29ea4-108">The storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="29ea4-109">Sin embargo, HTTPS es el protocolo recomendado para obtener acceso a recursos en una cuenta de producción de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="29ea4-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-to-the-emulator-account-using-a-shortcut"></a><span data-ttu-id="29ea4-110">Conexión a la cuenta del emulador mediante un acceso directo</span><span class="sxs-lookup"><span data-stu-id="29ea4-110">Connect to the emulator account using a shortcut</span></span>
<span data-ttu-id="29ea4-111">La manera más fácil de conectarse al emulador de almacenamiento desde su aplicación consiste en configurar, dentro del archivo de configuración de la aplicación, una cadena de conexión que haga referencia al método abreviado `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="29ea4-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="29ea4-112">Este es un ejemplo de una cadena de conexión al emulador de almacenamiento en un archivo *app.config*:</span><span class="sxs-lookup"><span data-stu-id="29ea4-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-to-the-emulator-account-using-the-well-known-account-name-and-key"></a><span data-ttu-id="29ea4-113">Conexión a la cuenta del emulador con el nombre de cuenta y la clave conocidos</span><span class="sxs-lookup"><span data-stu-id="29ea4-113">Connect to the emulator account using the well-known account name and key</span></span>
<span data-ttu-id="29ea4-114">Para crear una cadena de conexión que hace referencia al nombre de la cuenta del emulador y la clave, debe especificar los puntos de conexión para cada uno de los servicios que desea usar desde el emulador en la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="29ea4-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span></span> <span data-ttu-id="29ea4-115">Esto es necesario para que la cadena de conexión haga referencia a los extremos del emulador, que son diferentes de los de una cuenta de almacenamiento de producción.</span><span class="sxs-lookup"><span data-stu-id="29ea4-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="29ea4-116">Por ejemplo, el valor de la cadena de conexión será similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="29ea4-116">For example, the value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="29ea4-117">Este valor es idéntico al acceso directo mostrado anteriormente, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="29ea4-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="29ea4-118">Especificación de un servidor proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="29ea4-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="29ea4-119">También puede especificar que se use un proxy HTTP cuando se está probando el servicio con el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="29ea4-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span></span> <span data-ttu-id="29ea4-120">Esto puede ser útil para observar solicitudes y respuestas HTTP mientras está depurando operaciones con los servicios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="29ea4-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span></span> <span data-ttu-id="29ea4-121">Para especificar un proxy, agregue la opción `DevelopmentStorageProxyUri` a la cadena de conexión y establezca su valor en el URI del proxy.</span><span class="sxs-lookup"><span data-stu-id="29ea4-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span></span> <span data-ttu-id="29ea4-122">Por ejemplo, esta es una cadena de conexión que apunta al emulador de almacenamiento y configura un proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="29ea4-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

