---
title: roles de hello aaaConfigure para un Azure servicio con Visual Studio en la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset una copia de seguridad y configurar roles para servicios de nube de Azure mediante Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Configuración de los roles para un servicio de Azure con Visual Studio
Un servicio en la nube de Azure puede tener uno o más roles web o de trabajo. Para cada rol, es necesario toodefine cómo se configura ese rol y también configurar cómo se ejecuta ese rol. toolearn más información acerca de los roles de servicios en la nube, vea el vídeo de hello [Introducción tooAzure servicios en la nube](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

información de Hello para el servicio de nube se almacena en hello siguientes archivos:

- **ServiceDefinition.csdef** -archivo de definición de servicio de Hola define la configuración de tiempo de ejecución de hello para el servicio de nube incluido qué roles se requieren, los puntos de conexión y el tamaño de máquina virtual. Ninguno de los datos de hello almacenados en `ServiceDefinition.csdef` puede cambiarse cuando se ejecuta el rol.
- **ServiceConfiguration.cscfg** : archivo de configuración de servicio de hello configura el número de instancias de un rol se ejecuta y definen los valores de hello de configuración de Hola para un rol. Hola datos almacenados en `ServiceConfiguration.cscfg` se pueden cambiar mientras se ejecuta el rol.

toostore diferentes valores de configuración de Hola que controlan cómo se ejecuta un rol, puede definir varias configuraciones del servicio. Puede usar una configuración de servicio diferente para cada entorno de implementación. Por ejemplo, puede establecer el emulador de almacenamiento de Azure local de almacenamiento cuenta conexión cadena toouse hello en una configuración de servicio local y crear otro toouse de configuración de servicio almacenamiento de Azure en la nube de Hola.

Cuando se crea un servicio de nube de Azure en Visual Studio, dos configuraciones del servicio automáticamente se crean y agregan tooyour proyecto de Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Configurar un servicio en la nube de Azure
Puede configurar un servicio de nube de Azure desde el Explorador de soluciones en Visual Studio, como se muestra en hello pasos:

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.
   
    ![Menú contextual del proyecto en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. En la página de propiedades del proyecto de hello, seleccione hello **desarrollo** ficha. 

    ![Página de propiedades del proyecto: pestaña Desarrollo](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. Hola **configuración del servicio** lista, el nombre de select Hola de configuración del servicio de Hola que desea tooedit. (Si desea que toomake cambia configuraciones del servicio de hello tooall para este rol, seleccione **todas las configuraciones de**.)
   
    > [!IMPORTANT]
    > Si elige una configuración de servicio específica, algunas propiedades están deshabilitadas porque solo se pueden establecer para todas las configuraciones. tooedit estas propiedades, debe seleccionar **todas las configuraciones de**.
    > 
    > 
   
    ![Lista Configuración del servicio para un servicio en la nube de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Cambiar el número de Hola de instancias de rol
rendimiento de hello tooimprove de servicio en la nube, puede cambiar Hola número de instancias de un rol que se está ejecutando, según el número de Hola de usuarios o carga de hello esperada para un rol determinado. Cuando se ejecuta el servicio de nube de hello en Azure, se crea una máquina virtual independiente para cada instancia de un rol. Esto afecta a la facturación de hello para la implementación de Hola de este servicio de nube. Para más información sobre la facturación, consulte [Comprender la factura de Microsoft Azure](billing/billing-understand-your-bill.md).

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola. En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleccione hello **configuración** ficha.

    ![Pestaña Configuración](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.
   
    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. Hola **el número de instancias** texto cuadro, escriba el número de Hola de instancias que desee toostart para este rol. Cada instancia se ejecuta en una máquina virtual independiente al publicar tooAzure de servicio de nube de Hola.

    ![Actualizar Hola recuento de instancias](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Administrar cadenas de conexión para cuentas de almacenamiento
Puede agregar, quitar o modificar cadenas de conexión para sus configuraciones de servicio. Por ejemplo, es posible que quiera una cadena de conexión local para una configuración de servicio local que tiene un valor de `UseDevelopmentStorage=true`. Puede que le interese tooconfigure una configuración de servicio de nube que utiliza una cuenta de almacenamiento de Azure.

> [!WARNING]
> Al especificar información de clave de cuenta de almacenamiento de Azure y Hola de una cadena de conexión de la cuenta de almacenamiento, esta información se almacena localmente en el archivo de configuración de servicio de Hola. Sin embargo, esta información no se almacena actualmente como texto cifrado.
> 
> 

Mediante el uso de un valor diferente para cada configuración de servicio, no tiene toouse cadenas de conexión diferentes en el servicio de nube o modificar su código al publicar su tooAzure de servicio de nube. Puede usar Hola mismo nombre de cadena de conexión de hello en el valor de código y hello es diferente, en función de configuración del servicio Hola seleccionada al compilar su servicio en la nube o al publicarla.

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola. En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleccione hello **configuración** ficha.

    ![Pestaña Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.

    ![Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd una cadena de conexión, seleccione **Agregar configuración**.

    ![Agregar cadena de conexión](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Una vez que la nueva configuración de Hola se ha agregado toohello lista, actualizar la fila de hello en lista de hello con información necesaria de Hola.

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nombre de** -escriba nombre hello que quiere toouse de cadena de conexión de Hola.
    - **Tipo de** : seleccione esta opción **cadena de conexión** desde la lista desplegable de Hola.
    - **Valor** -desea, puede escribir la cadena de conexión de hello directamente en hello **valor** celda o seleccione hello toowork de puntos suspensivos (...) en hello **crear cadenas de conexión de almacenamiento** cuadro de diálogo.  

1. Hola **crear cadenas de conexión de almacenamiento** cuadro de diálogo, seleccione una opción para **conectarse mediante**. A continuación, siga las instrucciones de Hola de opción de Hola que seleccione:

    - **Emulador de almacenamiento de Microsoft Azure** : Si selecciona esta opción, se deshabilita configuración restante de hello en el cuadro de diálogo de hello cuando se aplica solo tooAzure. Seleccione **Aceptar**.
    - **Su suscripción** : si se selecciona esta opción, usar Hola lista desplegable lista tooeither seleccionar e inicie sesión en una cuenta de Microsoft o se agrega una cuenta de Microsoft. Seleccione una suscripción de Azure y una cuenta de almacenamiento. Seleccione **Aceptar**.
    - **Credenciales escritas manualmente** : escriba el nombre de cuenta de almacenamiento de hello y una clave principal o secundaria de Hola. Seleccione una opción en **Conexión** (se recomienda HTTPS en la mayoría de los escenarios). Seleccione **Aceptar**.

1. toodelete una cadena de conexión, seleccione la cadena de conexión de hello y, a continuación, seleccione **Quitar configuración**.

1. Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.

## <a name="programmatically-access-a-connection-string"></a>Acceso mediante programación a una cadena de conexión

Hello pasos siguientes muestran cómo tooprogrammatically tener acceso a una cadena de conexión con C#.

1. Agregue Hola siguiente mediante directivas tooa C# archivo donde se va configuración de Hola toouse:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello código siguiente muestra un ejemplo de cómo tooaccess una cadena de conexión. Reemplace hello &lt;ConnectionStringName > marcador de posición con el valor adecuado de Hola. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Agregar una configuración personalizada toouse en el servicio de nube de Azure
Configuración personalizada en el archivo de configuración de servicio de hello, podrá agregar un nombre y valor de una cadena para una configuración de servicio específico. Puede elegir toouse esta tooconfigure de configuración, una característica de servicio en la nube leyendo el valor de Hola de Hola establecer y usar esta lógica de hello toocontrol de valor en el código. Puede cambiar estos valores de configuración de servicio sin necesidad de toorebuild su paquete del servicio o cuando se está ejecutando el servicio de nube. Su código puede buscar las notificaciones de cuando cambia un valor. Vea [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Puede agregar, quitar o modificar valores personalizados para sus configuraciones de servicio. Es posible que quiera valores diferentes para estas cadenas para distintas configuraciones del servicio.

Mediante el uso de un valor diferente para cada configuración de servicio, no tiene toouse diferentes cadenas en el servicio de nube o modificar su código al publicar su tooAzure de servicio de nube. Puede usar Hola mismo nombre de cadena de hello en el valor de código y hello es diferente, en función de configuración del servicio Hola seleccionada al compilar su servicio en la nube o al publicarla.

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola. En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleccione hello **configuración** ficha.

    ![Pestaña Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.

    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Seleccione una configuración personalizada, tooadd **Agregar configuración**.

    ![Agregar configuración personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Una vez que la nueva configuración de Hola se ha agregado toohello lista, actualizar la fila de hello en lista de hello con información necesaria de Hola.

    ![Nueva configuración personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nombre de** -escriba nombre Hola de saludo.
    - **Tipo de** : seleccione esta opción **cadena** desde la lista desplegable de Hola.
    - **Valor** -escriba valor Hola de saludo. Puede escribir el valor de hello directamente en hello **valor** celda o valor de hello seleccione puntos suspensivos (...) tooenter Hola Hola **Editar cadena** cuadro de diálogo.  

1. toodelete una configuración personalizada, seleccione la configuración de hello y, a continuación, seleccione **Quitar configuración**.

1. Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.

## <a name="programmatically-access-a-custom-settings-value"></a>Acceso mediante programación al valor de una configuración personalizada
 
Hello pasos siguientes muestran cómo tooprogrammatically tener acceso a una configuración personalizada mediante C#.

1. Agregue Hola siguiente mediante directivas tooa C# archivo donde se va configuración de Hola toouse:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello código siguiente muestra un ejemplo de cómo tooaccess una configuración personalizada. Reemplace hello &lt;SettingName > marcador de posición con el valor adecuado de Hola. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Administrar el almacenamiento local para cada instancia de rol
Puede agregar almacenamiento del sistema de archivos local para cada instancia de un rol. Hola datos almacenados en almacenamiento no es accesible por otras instancias de rol de Hola para qué Hola se almacenan los datos, o por otras funciones.  

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola. En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleccione hello **almacenamiento Local** ficha.

    ![Pestaña Almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. Hola **configuración del servicio** lista, asegúrese de que **todas las configuraciones de** se selecciona como configuración de almacenamiento local de hello aplica configuraciones de servicio de tooall. Cualquier otro valor producirá todos los campos de entrada de hello en página de Hola que se va a deshabilitar. 

    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. Seleccione una entrada de almacenamiento local, tooadd **agregar almacenamiento Local**.

    ![Agregar almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Una vez que se ha agregado toohello lista a nueva entrada de almacenamiento local de hello, actualizar la fila de hello en lista de hello con información necesaria de Hola.

    ![Nueva entrada de almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nombre de** -escriba nombre de Hola que quiere toouse para el almacenamiento local de hello nueva.
    - **Tamaño (MB)** -especifique el tamaño de hello en MB que necesita para el almacenamiento local de hello nueva.
    - **Limpieza de reciclado de rol** -seleccionar estos datos de opción tooremove hello en almacenamiento local de hello nueva cuando se recicla la máquina virtual de hello para el rol de Hola.

1. toodelete una entrada de almacenamiento local, seleccione la entrada de hello y, a continuación, seleccione **quitar almacenamiento Local**.

1. Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.

## <a name="programmatically-accessing-local-storage"></a>Acceso mediante programación al almacenamiento local

Esta sección muestra cómo tooprogrammatically tener acceso a almacenamiento local utilizando C# mediante la escritura de un archivo de texto de prueba `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Escribir un almacenamiento de toolocal del archivo de texto

Hola siguiente código muestra un ejemplo de cómo toolocal almacenamiento de archivos en toowrite un texto. Reemplace hello &lt;LocalStorageName > marcador de posición con el valor adecuado de Hola. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Buscar un archivo escrito toolocal almacenamiento

archivo de hello tooview creado por código de hello en la sección anterior de hello, siga estos pasos:
    
1.  En Hola área de notificación de Windows, haga clic en el icono de Azure de hello y, en el menú contextual de hello, seleccione **Mostrar IU del emulador de proceso**. 

    ![Mostrar el emulador de proceso de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Seleccione el rol web de Hola.

    ![Emulador de proceso de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. En hello **emulador de proceso de Microsoft Azure** menú, seleccione **herramientas** > **Abrir almacén local**.

    ![Opción de menú Open local store (Abrir almacén local)](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Cuando se abre la ventana del explorador de Windows hello, escriba ' MyLocalStorageTest.txt'' en hello **búsqueda** cuadro de texto y seleccione **ENTRAR** búsqueda de hello toostart. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los proyectos de Azure en Visual Studio, consulte [Configurar un proyecto de Azure](vs-azure-tools-configuring-an-azure-project.md). Más información sobre el esquema del servicio de nube Hola leyendo [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).

