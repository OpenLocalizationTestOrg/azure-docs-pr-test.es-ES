<span data-ttu-id="cc561-101">Las aplicaciones .NET pueden usar el cliente de caché **StackExchange.Redis** , que se puede configurar en Visual Studio mediante un paquete NuGet que simplifica la configuración de aplicaciones de cliente de caché.</span><span class="sxs-lookup"><span data-stu-id="cc561-101">.NET applications can use the **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies the configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="cc561-102">Para obtener más información, consulte la página Github [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) y la [documentación del cliente de caché StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="cc561-102">For more information, see the [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  the [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="cc561-103">Para configurar una aplicación cliente en Visual Studio usando el paquete NuGet StackExchange.Redis, haga clic con el botón derecho en el proyecto en el **Explorador de soluciones** y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cc561-103">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, right-click the project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="cc561-105">Escriba **StackExchange.Redis** o **StackExchange.Redis.StrongName** en el cuadro de texto de búsqueda, seleccione la versión que desee en los resultados y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="cc561-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into the search text box, select the desired version from the results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="cc561-106">Si prefiere usar una versión con nombre seguro de la biblioteca de cliente **StackExchange.Redis**, elija **StackExchange.Redis.StrongName**; de lo contrario, elija **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="cc561-106">If you prefer to use a strong-named version of the **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="cc561-108">El paquete de NuGet se descarga y agrega las referencias de ensamblado requeridas para que la aplicación cliente acceda a Caché en Redis de Azure con el cliente de caché StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="cc561-108">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="cc561-109">Si anteriormente ha configurado el proyecto para usar StackExchange.Redis, puede buscar actualizaciones para el paquete desde el **Administrador de paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cc561-109">If you have previously configured your project to use StackExchange.Redis, you can check for updates to the package from the **NuGet Package Manager**.</span></span> <span data-ttu-id="cc561-110">Para buscar e instalar versiones actualizadas del paquete StackExchange.Redis NuGet, haga clic en **Actualizaciones** en la ventana del **Administrador de paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cc561-110">To check for and install updated versions of the StackExchange.Redis NuGet package, click **Updates** in the the **NuGet Package Manager** window.</span></span> <span data-ttu-id="cc561-111">Si existe una actualización para el paquete StackExchange.Redis de NuGet, puede actualizar el proyecto para usar la versión actualizada.</span><span class="sxs-lookup"><span data-stu-id="cc561-111">If an update to the StackExchange.Redis NuGet package is available, you can update your project to use the updated version.</span></span>
> 
> 

<span data-ttu-id="cc561-112">También puede instalar el paquete NuGet StackExchange.Redis haciendo clic en **Administrador de paquetes NuGet**, **Consola del Administrador de paquetes** desde el menú **Herramientas** y ejecutando el comando siguiente en la ventana **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="cc561-112">You can also install the StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu, and running the following command from the **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
