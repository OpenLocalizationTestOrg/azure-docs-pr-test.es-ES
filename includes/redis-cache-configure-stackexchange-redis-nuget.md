Las aplicaciones .NET pueden utilizar hello **StackExchange.Redis** cliente de caché, que se puede configurar en Visual Studio mediante un paquete de NuGet que simplifica la configuración de Hola de aplicaciones de cliente de caché. 

> [!NOTE]
> Para obtener más información, vea hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github hello y página [documentación del cliente de caché de StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure una aplicación cliente en Visual Studio mediante Hola paquete de StackExchange.Redis NuGet, haga clic en proyecto de hello en **el Explorador de soluciones** y elija **administrar paquetes de NuGet**. 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Tipo de **StackExchange.Redis** o **StackExchange.Redis.StrongName** en el cuadro de texto de búsqueda de hello, seleccione la versión que desee Hola de resultados de Hola y haga clic en **instalar**.

> [!NOTE]
> Si prefiere una versión con nombre seguro de hello toouse **StackExchange.Redis** biblioteca de cliente, elija **StackExchange.Redis.StrongName**; en caso contrario, elija **StackExchange.Redis**.
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado para su tooaccess de aplicación de cliente caché en Redis de Azure con el cliente de caché de StackExchange.Redis Hola.

> [!NOTE]
> Si previamente ha configurado su toouse proyecto StackExchange.Redis, puede comprobar para el paquete de actualizaciones toohello de hello **Administrador de paquetes de NuGet**. toocheck para y versiones de instalación actualizado de hello paquete de StackExchange.Redis NuGet, haga clic en **actualizaciones** Hola Hola **Administrador de paquetes de NuGet** ventana. Si un paquete de StackExchange.Redis NuGet toohello de actualización está disponible, puede actualizar la versión del proyecto toouse Hola actualizado.
> 
> 

También puede instalar Hola paquete de StackExchange.Redis NuGet, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** hello ejecución y menú siguiente comando de hello **Package Manager Console** ventana.
    
```
Install-Package StackExchange.Redis
```
