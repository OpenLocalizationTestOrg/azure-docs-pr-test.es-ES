1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **publicar**. Elija **Crear nuevo** y, después, haga clic en **Publicar**. 

    ![Publicar para crear una nueva aplicación de función](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Si aún no está conectado tooyour cuenta de Azure de Visual Studio, haga clic en **agregar una cuenta...** .  

3. Hola **crear servicio en la aplicación** cuadro de diálogo, utilice hello **hospedaje** configuración como Hola especificado en la tabla siguiente: 

    ![Runtime local de Azure](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Configuración      | Valor sugerido  | Descripción                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nombre de aplicación** | Nombre único globalmente | Nombre que identifica de forma única la nueva aplicación de función. |
    | **Suscripción** | Elija una suscripción | Hola toouse de suscripción de Azure. |
    | **[Grupo de recursos](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nombre del recurso de hello agrupar en qué toocreate la aplicación de la función. |
    | **[Plan de App Service](../articles/azure-functions/functions-scale.md)** | Plan de consumo | Realizar seguro hello toochoose **consumo** en **tamaño** cuando se crea un nuevo plan.  |
    | **[Cuenta de almacenamiento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nombre único globalmente | Use una cuenta de almacenamiento existente o crear una nueva.   |

4. Haga clic en **crear** toocreate una aplicación de función en Azure con esta configuración. Tras completar el aprovisionamiento de hello, tome nota de hello **dirección URL del sitio** valor, que es la dirección de saludo de la aplicación de la función en Azure. 

    ![Runtime local de Azure](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
