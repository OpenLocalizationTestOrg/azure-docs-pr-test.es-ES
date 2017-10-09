1. Inicie sesión en hello [Portal de Azure].
2. Haga clic en **+NUEVO** > **Web y móvil** > **Aplicación móvil** y, después, proporcione un nombre para el back-end de la aplicación móvil.
3. Para hello **grupo de recursos**, seleccione un grupo de recursos existente o crear uno nuevo (usando Hola el mismo nombre que la aplicación). 
   
    Puede seleccionar un plan de Servicio de aplicaciones ya existente o crear uno nuevo. Para obtener más información sobre los planes de servicios de aplicaciones y cómo toocreate un nuevo plan de precios de diferentes capas y en la ubicación deseada, consulte [información general detallada de planes de servicio de aplicaciones de Azure](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para hello **plan de servicio de aplicaciones**, plan de hello predeterminado (Hola [nivel estándar](https://azure.microsoft.com/pricing/details/app-service/)) está seleccionado. También puede seleccionar otro plan o [crear uno](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). la configuración del plan del servicio de aplicación Hello determina hello [ubicación, características, costo y recursos de proceso](https://azure.microsoft.com/pricing/details/app-service/) asociados a su aplicación. 
   
    Después de decidir plan hello, haga clic en **crear**. Esto crea la aplicación móvil de hello back-end. 
5. Hola **configuración** hoja para hello nueva aplicación móvil back-end, haga clic en **inicio rápido** > su plataforma de aplicaciones de cliente > **conectar una base de datos**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. Hola **Agregar conexión de datos** hoja, haga clic en **base de datos SQL** > **crear una nueva base de datos**, base de datos de tipo hello **nombre**, Elija un nivel de precios, a continuación, haga clic en **Server**.  Puede reutilizar esta nueva base de datos. Si ya tiene una base de datos en hello misma ubicación, puede elegir en su lugar **usar una base de datos**. no recomienda el uso de Hola de una base de datos en una ubicación diferente debido a los costos de toobandwidth y una latencia mayor.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. Hola **nuevo servidor** hoja, escriba un nombre de servidor único en hello **nombre del servidor** campo, proporcione un inicio de sesión y una contraseña, compruebe **server tooaccess de permitir que los servicios de azure**y haga clic en **Aceptar**. Esto crea Hola base de datos.
8. Nuevo en hello **Agregar conexión de datos** hoja, haga clic en **cadena de conexión**, escriba los valores de inicio de sesión y la contraseña de hello de la base de datos y haga clic en **Aceptar**. Espere unos minutos para toobe de base de datos de hello implementado correctamente antes de continuar.

<!-- URLs. -->
[Portal de Azure]: https://portal.azure.com/
