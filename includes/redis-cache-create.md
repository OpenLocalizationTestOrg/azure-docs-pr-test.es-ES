toocreate una memoria caché, en primer lugar, inicie sesión en toohello [portal de Azure](https://portal.azure.com)y haga clic en **New** > **bases de datos** > **caché en Redis**.

> [!NOTE]
> Si no tiene una cuenta de Azure, puede [abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en tan solo un par de minutos.
> 
> 

![New cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Además de las memorias caché toocreating de hello portal de Azure, también puede crear paquetes con el Administrador de recursos plantillas, PowerShell o CLI de Azure.
> 
> * toocreate una caché con plantillas de administrador de recursos, consulte [crear una caché en Redis mediante una plantilla de](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate una caché con Azure PowerShell, consulte [administrar Azure Redis Cache con Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate una memoria caché mediante la CLI de Azure, consulte [cómo toocreate y administrar caché en Redis de Azure con hello Azure interfaz de línea de comandos (CLI de Azure)](../articles/redis-cache/cache-manage-cli.md).
> 
> 

Hola **nueva caché en Redis** hoja, especifican la configuración deseada de Hola para caché de Hola.

![Create cache](media/redis-cache-create/redis-cache-cache-create.png) 

* En **nombre Dns**, escriba un toouse de nombre de la memoria caché única para el extremo de la caché de Hola. nombre de la memoria caché de Hello debe ser una cadena comprendida entre 1 y 63 caracteres y contener solo números, letras y hello `-` caracteres. Hello nombre de la caché no puede empezar ni terminar con hello `-` caracteres y consecutivos `-` caracteres no son válidos.
* Para **suscripción**, seleccione Hola suscripción de Azure que quiere toouse de caché de Hola. Si la cuenta tiene solo una suscripción, se seleccionará automáticamente y Hola **suscripción** no se mostrará la lista desplegable.
* En **Grupo de recursos**, seleccione o cree un grupo de recursos para su caché. Para obtener más información, consulte [grupos de recursos utilizando toomanage los recursos de Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Use **ubicación** toospecify Hola ubicación geográfica en la que se hospeda la caché. Para obtener el mejor rendimiento de hello, Microsoft recomienda encarecidamente que cree caché Hola Hola misma región que la aplicación de cliente de caché de Hola.
* Use **tarifa** tooselect Hola deseado tamaño de caché y las características.
* **Redis clúster** permite toocreate cachés mayores que los datos de 53 GB y tooshard en varios nodos de Redis. Para obtener más información, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Redis persistencia** ofrece Hola capacidad toopersist su tooan caché cuenta de almacenamiento de Azure. Para obtener instrucciones acerca de cómo configurar la persistencia, consulte [cómo persistencia tooconfigure para una caché de Redis de Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Red virtual** proporciona seguridad mejorada y aislamiento restringiendo el acceso tooyour caché tooonly esos clientes dentro de hello especificadas red Virtual de Azure. Puede usar todas las características de Hola de red virtual, como subredes, las directivas de control de acceso y otra características toofurther restringen acceso tooRedis. Para obtener más información, consulte [cómo son compatibles con tooconfigure red Virtual para una caché de Redis de Azure Premium](../articles/redis-cache/cache-how-to-premium-vnet.md).
* El acceso no SSL está deshabilitado de forma predeterminada para las nuevas cachés. puerto de tooenable hello no SSL, verificación **desbloquear el puerto 6379 (no cifradas con SSL)**.

Después de configuran opciones de caché de hello nueva, haga clic en **crear**. Puede tardar unos minutos para hello caché toobe creado. estado de hello toocheck, puede supervisar el progreso de hello en el panel de inicio de Hola. Una vez creada la memoria caché de hello, la nueva caché tiene un **ejecutando** estado y está listo para su uso con [configuración predeterminada](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache created](media/redis-cache-create/redis-cache-cache-created.png)

