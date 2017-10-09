## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Crear una base de datos SQL en blanco con hello portal de Azure

Se crea una instancia de Azure SQL Database con un conjunto definido de [recursos de proceso y almacenamiento](../articles/sql-database/sql-database-service-tiers.md). base de datos de Hola se crea dentro de un [grupo de recursos de Azure](../articles/azure-resource-manager/resource-group-overview.md) y en un [servidor lógico de base de datos de SQL Azure](../articles/sql-database/sql-database-features.md). 

Siga estos toocreate pasos una base de datos SQL en blanco. 

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Seleccione **bases de datos** de hello **New** página y seleccione **base de datos SQL** de hello **bases de datos** página. 

   ![crear una base de datos en blanco](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Rellenar formulario de la base de datos SQL de Hola con hello después de obtener información, tal como se muestra en hello anterior imagen:   

   | Configuración | Valor sugerido | Descripción |
   | --------| --------------- | ----------- | 
   | **Nombre de la base de datos** | mySampleDatabase | Para conocer los nombres de base de datos válidos, consulte [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos). | 
   | **Suscripción** | Su suscripción  | Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions). |
   | **Grupos de recursos** | myResourceGroup | Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). |
   | **Seleccionar origen** | Base de datos en blanco | Especifica que se debe crear una base de datos en blanco. |
   ||||

4. Haga clic en **Server** toocreate y configurar un servidor nuevo para la nueva base de datos. Rellene hello **nuevo formulario server** con hello siguiente información: 

   | Configuración | Valor sugerido | Descripción |
   | --------| --------------- | ----------- | 
   | **Nombre del servidor** | Cualquier nombre globalmente único. | Para conocer cuáles son los nombres de servidor válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). | 
   | **Inicio de sesión del administrador del servidor** | Cualquier nombre válido. | Para conocer los nombres de inicio de sesión válidos, consulte [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos).|
   | **Password** | Cualquier contraseña válida. | La contraseña debe tener al menos ocho caracteres y debe contener caracteres de tres de las siguientes categorías de hello: caracteres en mayúsculas, caracteres en minúsculas, números y caracteres no alfanuméricos. |
   | **Ubicación** | Cualquier ubicación válida. | Para obtener información acerca de las regiones, consulte [Regiones de Azure](https://azure.microsoft.com/regions/). |
   ||||

   ![create database-server](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Haga clic en **Seleccionar**.

6. Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para la nueva base de datos. Para este tutorial, seleccione **20 DTU** y **250** GB de almacenamiento.

   ![create database-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Haga clic en **Apply**.  

8. Seleccione un **intercalación** de base de datos en blanco de hello (para este tutorial, el valor predeterminado de Hola de uso). Para más información sobre las intercalaciones, vea [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations) (Intercalaciones)

9. Haga clic en **crear** base de datos de tooprovision Hola. Aprovisionamiento dura aproximadamente un minuto y Media toocomplete. 

10. En la barra de herramientas de hello, haga clic en **notificaciones** toomonitor proceso de implementación de Hola.

   ![notificación](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Crear una regla de firewall de nivel de servidor mediante Hola portal de Azure

Hola servicio de base de datos SQL crea un servidor de seguridad en el nivel de servidor hello. Inicialmente firewall de hello impide aplicaciones conectarse toohello server o bases de datos de tooany en servidor hello y herramientas externas. Se permiten las conexiones después de que se crea una regla de firewall tooopen las direcciones IP concretas. Siga estos pasos toocreate una [regla de firewall de nivel de servidor de base de datos SQL](../articles/sql-database/sql-database-firewall-configure.md) para el cliente y dirección IP, tooenable conectividad externa a través de firewall de base de datos SQL de Hola para sólo la dirección IP. 


> [!NOTE]
> Azure SQL Database se comunica a través del puerto 1433. Puede conectarse tooSQL base de datos solo después de que firewall de saludo de la red permite el tráfico saliente a través del puerto 1433.


1. Una vez finalizada la implementación de hello, haga clic en **bases de datos SQL** del menú izquierdo de hello y, a continuación, haga clic en **mySampleDatabase** en hello **bases de datos SQL** página. página de información general para abrir el base de datos, que muestra que Hola totalmente Hello calificado nombre del servidor (como **mynewserver20170313.database.windows.net**) y proporciona opciones para otra configuración. Copie dicho nombre, ya que lo tendrá que usar más adelante,

   > [!IMPORTANT]
   > Necesitará este servidor de tooyour de tooconnect de nombre completo del servidor y sus bases de datos en las siguientes guías de inicio rápidos.
   > 

   ![nombre del servidor](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Haga clic en **Configurar firewall de servidor** de barra de herramientas de hello tal y como se muestra en la imagen anterior de Hola. Hola **configuración del Firewall** se abre la página servidor de base de datos de SQL de Hola. 

   ![regla de firewall del servidor](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Haga clic en **agregar dirección IP del cliente** en tooadd de barra de herramientas de hello tooa nueva regla de firewall de direcciones de la IP actual. La regla de firewall puede abrir el puerto 1433 para una única dirección IP o un intervalo de direcciones IP.

4. Haga clic en **Guardar**. Se crea una regla de firewall de nivel de servidor para la dirección IP actual abrir el puerto 1433 en el servidor lógico Hola.

   ![establecer regla de firewall del servidor](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Haga clic en **Aceptar** y, a continuación, cierre hello **configuración del Firewall** página.

Ahora puede conectarse toohello servidor de base de datos de SQL Azure y sus bases de datos mediante una herramienta como SQL Server Management Studio (SSMS). conexión de Hola se desde esta dirección IP, y utiliza la cuenta de administrador de servidor de hello creado anteriormente.


> [!IMPORTANT]
> De forma predeterminada, el acceso a través de firewall de base de datos SQL de hello está habilitado para todos los servicios de Azure. Haga clic en **OFF** en este toodisable de página para todos los servicios de Azure.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Obtener valores de cadena de conexión mediante Hola portal de Azure

Obtener nombre de servidor completo de hello para el servidor de base de datos de SQL Azure en hello portal de Azure. Usa Hola completo nombre tooconnect tooyour server utilizando SQL Server Management Studio.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 

3. Hola **Essentials** panel Hola página del portal Azure para la base de datos, busque y, a continuación, copie hello **nombre del servidor**.

   ![información sobre la conexión](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
