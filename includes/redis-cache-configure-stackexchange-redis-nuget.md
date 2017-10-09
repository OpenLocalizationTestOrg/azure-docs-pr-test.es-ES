<span data-ttu-id="6bab4-101">Las aplicaciones .NET pueden utilizar hello **StackExchange.Redis** cliente de caché, que se puede configurar en Visual Studio mediante un paquete de NuGet que simplifica la configuración de Hola de aplicaciones de cliente de caché.</span><span class="sxs-lookup"><span data-stu-id="6bab4-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="6bab4-102">Para obtener más información, vea hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github hello y página [documentación del cliente de caché de StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="6bab4-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="6bab4-103">tooconfigure una aplicación cliente en Visual Studio mediante Hola paquete de StackExchange.Redis NuGet, haga clic en proyecto de hello en **el Explorador de soluciones** y elija **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="6bab4-105">Tipo de **StackExchange.Redis** o **StackExchange.Redis.StrongName** en el cuadro de texto de búsqueda de hello, seleccione la versión que desee Hola de resultados de Hola y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="6bab4-106">Si prefiere una versión con nombre seguro de hello toouse **StackExchange.Redis** biblioteca de cliente, elija **StackExchange.Redis.StrongName**; en caso contrario, elija **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="6bab4-108">Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado para su tooaccess de aplicación de cliente caché en Redis de Azure con el cliente de caché de StackExchange.Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="6bab4-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="6bab4-109">Si previamente ha configurado su toouse proyecto StackExchange.Redis, puede comprobar para el paquete de actualizaciones toohello de hello **Administrador de paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="6bab4-110">toocheck para y versiones de instalación actualizado de hello paquete de StackExchange.Redis NuGet, haga clic en **actualizaciones** Hola Hola **Administrador de paquetes de NuGet** ventana.</span><span class="sxs-lookup"><span data-stu-id="6bab4-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="6bab4-111">Si un paquete de StackExchange.Redis NuGet toohello de actualización está disponible, puede actualizar la versión del proyecto toouse Hola actualizado.</span><span class="sxs-lookup"><span data-stu-id="6bab4-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="6bab4-112">También puede instalar Hola paquete de StackExchange.Redis NuGet, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** hello ejecución y menú siguiente comando de hello **Package Manager Console** ventana.</span><span class="sxs-lookup"><span data-stu-id="6bab4-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
