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
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="c3d8d-103">Configuración de los roles para un servicio de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3d8d-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="c3d8d-104">Un servicio en la nube de Azure puede tener uno o más roles web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="c3d8d-105">Para cada rol, es necesario toodefine cómo se configura ese rol y también configurar cómo se ejecuta ese rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="c3d8d-106">toolearn más información acerca de los roles de servicios en la nube, vea el vídeo de hello [Introducción tooAzure servicios en la nube](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="c3d8d-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="c3d8d-107">información de Hello para el servicio de nube se almacena en hello siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="c3d8d-108">**ServiceDefinition.csdef** -archivo de definición de servicio de Hola define la configuración de tiempo de ejecución de hello para el servicio de nube incluido qué roles se requieren, los puntos de conexión y el tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="c3d8d-109">Ninguno de los datos de hello almacenados en `ServiceDefinition.csdef` puede cambiarse cuando se ejecuta el rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="c3d8d-110">**ServiceConfiguration.cscfg** : archivo de configuración de servicio de hello configura el número de instancias de un rol se ejecuta y definen los valores de hello de configuración de Hola para un rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="c3d8d-111">Hola datos almacenados en `ServiceConfiguration.cscfg` se pueden cambiar mientras se ejecuta el rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="c3d8d-112">toostore diferentes valores de configuración de Hola que controlan cómo se ejecuta un rol, puede definir varias configuraciones del servicio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="c3d8d-113">Puede usar una configuración de servicio diferente para cada entorno de implementación.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="c3d8d-114">Por ejemplo, puede establecer el emulador de almacenamiento de Azure local de almacenamiento cuenta conexión cadena toouse hello en una configuración de servicio local y crear otro toouse de configuración de servicio almacenamiento de Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="c3d8d-115">Cuando se crea un servicio de nube de Azure en Visual Studio, dos configuraciones del servicio automáticamente se crean y agregan tooyour proyecto de Azure:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="c3d8d-116">Configurar un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="c3d8d-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="c3d8d-117">Puede configurar un servicio de nube de Azure desde el Explorador de soluciones en Visual Studio, como se muestra en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="c3d8d-118">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c3d8d-119">En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Menú contextual del proyecto en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="c3d8d-121">En la página de propiedades del proyecto de hello, seleccione hello **desarrollo** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Página de propiedades del proyecto: pestaña Desarrollo](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="c3d8d-123">Hola **configuración del servicio** lista, el nombre de select Hola de configuración del servicio de Hola que desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="c3d8d-124">(Si desea que toomake cambia configuraciones del servicio de hello tooall para este rol, seleccione **todas las configuraciones de**.)</span><span class="sxs-lookup"><span data-stu-id="c3d8d-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="c3d8d-125">Si elige una configuración de servicio específica, algunas propiedades están deshabilitadas porque solo se pueden establecer para todas las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="c3d8d-126">tooedit estas propiedades, debe seleccionar **todas las configuraciones de**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Lista Configuración del servicio para un servicio en la nube de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="c3d8d-128">Cambiar el número de Hola de instancias de rol</span><span class="sxs-lookup"><span data-stu-id="c3d8d-128">Change hello number of role instances</span></span>
<span data-ttu-id="c3d8d-129">rendimiento de hello tooimprove de servicio en la nube, puede cambiar Hola número de instancias de un rol que se está ejecutando, según el número de Hola de usuarios o carga de hello esperada para un rol determinado.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="c3d8d-130">Cuando se ejecuta el servicio de nube de hello en Azure, se crea una máquina virtual independiente para cada instancia de un rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="c3d8d-131">Esto afecta a la facturación de hello para la implementación de Hola de este servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="c3d8d-132">Para más información sobre la facturación, consulte [Comprender la factura de Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="c3d8d-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="c3d8d-133">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c3d8d-134">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="c3d8d-135">En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c3d8d-137">Seleccione hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-137">Select hello **Configuration** tab.</span></span>

    ![Pestaña Configuración](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="c3d8d-139">Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="c3d8d-141">Hola **el número de instancias** texto cuadro, escriba el número de Hola de instancias que desee toostart para este rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="c3d8d-142">Cada instancia se ejecuta en una máquina virtual independiente al publicar tooAzure de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Actualizar Hola recuento de instancias](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="c3d8d-144">Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="c3d8d-145">Administrar cadenas de conexión para cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c3d8d-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="c3d8d-146">Puede agregar, quitar o modificar cadenas de conexión para sus configuraciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="c3d8d-147">Por ejemplo, es posible que quiera una cadena de conexión local para una configuración de servicio local que tiene un valor de `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="c3d8d-148">Puede que le interese tooconfigure una configuración de servicio de nube que utiliza una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="c3d8d-149">Al especificar información de clave de cuenta de almacenamiento de Azure y Hola de una cadena de conexión de la cuenta de almacenamiento, esta información se almacena localmente en el archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="c3d8d-150">Sin embargo, esta información no se almacena actualmente como texto cifrado.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="c3d8d-151">Mediante el uso de un valor diferente para cada configuración de servicio, no tiene toouse cadenas de conexión diferentes en el servicio de nube o modificar su código al publicar su tooAzure de servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="c3d8d-152">Puede usar Hola mismo nombre de cadena de conexión de hello en el valor de código y hello es diferente, en función de configuración del servicio Hola seleccionada al compilar su servicio en la nube o al publicarla.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="c3d8d-153">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c3d8d-154">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="c3d8d-155">En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c3d8d-157">Seleccione hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-157">Select hello **Settings** tab.</span></span>

    ![Pestaña Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="c3d8d-159">Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="c3d8d-161">tooadd una cadena de conexión, seleccione **Agregar configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Agregar cadena de conexión](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="c3d8d-163">Una vez que la nueva configuración de Hola se ha agregado toohello lista, actualizar la fila de hello en lista de hello con información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="c3d8d-165">**Nombre de** -escriba nombre hello que quiere toouse de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="c3d8d-166">**Tipo de** : seleccione esta opción **cadena de conexión** desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="c3d8d-167">**Valor** -desea, puede escribir la cadena de conexión de hello directamente en hello **valor** celda o seleccione hello toowork de puntos suspensivos (...) en hello **crear cadenas de conexión de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="c3d8d-168">Hola **crear cadenas de conexión de almacenamiento** cuadro de diálogo, seleccione una opción para **conectarse mediante**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="c3d8d-169">A continuación, siga las instrucciones de Hola de opción de Hola que seleccione:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="c3d8d-170">**Emulador de almacenamiento de Microsoft Azure** : Si selecciona esta opción, se deshabilita configuración restante de hello en el cuadro de diálogo de hello cuando se aplica solo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="c3d8d-171">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-171">Select **OK**.</span></span>
    - <span data-ttu-id="c3d8d-172">**Su suscripción** : si se selecciona esta opción, usar Hola lista desplegable lista tooeither seleccionar e inicie sesión en una cuenta de Microsoft o se agrega una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="c3d8d-173">Seleccione una suscripción de Azure y una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="c3d8d-174">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-174">Select **OK**.</span></span>
    - <span data-ttu-id="c3d8d-175">**Credenciales escritas manualmente** : escriba el nombre de cuenta de almacenamiento de hello y una clave principal o secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="c3d8d-176">Seleccione una opción en **Conexión** (se recomienda HTTPS en la mayoría de los escenarios). Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="c3d8d-177">toodelete una cadena de conexión, seleccione la cadena de conexión de hello y, a continuación, seleccione **Quitar configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="c3d8d-178">Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="c3d8d-179">Acceso mediante programación a una cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="c3d8d-179">Programmatically access a connection string</span></span>

<span data-ttu-id="c3d8d-180">Hello pasos siguientes muestran cómo tooprogrammatically tener acceso a una cadena de conexión con C#.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="c3d8d-181">Agregue Hola siguiente mediante directivas tooa C# archivo donde se va configuración de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="c3d8d-182">Hello código siguiente muestra un ejemplo de cómo tooaccess una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="c3d8d-183">Reemplace hello &lt;ConnectionStringName > marcador de posición con el valor adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="c3d8d-184">Agregar una configuración personalizada toouse en el servicio de nube de Azure</span><span class="sxs-lookup"><span data-stu-id="c3d8d-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="c3d8d-185">Configuración personalizada en el archivo de configuración de servicio de hello, podrá agregar un nombre y valor de una cadena para una configuración de servicio específico.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="c3d8d-186">Puede elegir toouse esta tooconfigure de configuración, una característica de servicio en la nube leyendo el valor de Hola de Hola establecer y usar esta lógica de hello toocontrol de valor en el código.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="c3d8d-187">Puede cambiar estos valores de configuración de servicio sin necesidad de toorebuild su paquete del servicio o cuando se está ejecutando el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="c3d8d-188">Su código puede buscar las notificaciones de cuando cambia un valor.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="c3d8d-189">Vea [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3d8d-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="c3d8d-190">Puede agregar, quitar o modificar valores personalizados para sus configuraciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="c3d8d-191">Es posible que quiera valores diferentes para estas cadenas para distintas configuraciones del servicio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="c3d8d-192">Mediante el uso de un valor diferente para cada configuración de servicio, no tiene toouse diferentes cadenas en el servicio de nube o modificar su código al publicar su tooAzure de servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="c3d8d-193">Puede usar Hola mismo nombre de cadena de hello en el valor de código y hello es diferente, en función de configuración del servicio Hola seleccionada al compilar su servicio en la nube o al publicarla.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="c3d8d-194">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c3d8d-195">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="c3d8d-196">En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c3d8d-198">Seleccione hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-198">Select hello **Settings** tab.</span></span>

    ![Pestaña Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="c3d8d-200">Hola **configuración del servicio** lista, configuración de servicio de hello select que desea tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="c3d8d-202">Seleccione una configuración personalizada, tooadd **Agregar configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Agregar configuración personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="c3d8d-204">Una vez que la nueva configuración de Hola se ha agregado toohello lista, actualizar la fila de hello en lista de hello con información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nueva configuración personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="c3d8d-206">**Nombre de** -escriba nombre Hola de saludo.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="c3d8d-207">**Tipo de** : seleccione esta opción **cadena** desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="c3d8d-208">**Valor** -escriba valor Hola de saludo.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="c3d8d-209">Puede escribir el valor de hello directamente en hello **valor** celda o valor de hello seleccione puntos suspensivos (...) tooenter Hola Hola **Editar cadena** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="c3d8d-210">toodelete una configuración personalizada, seleccione la configuración de hello y, a continuación, seleccione **Quitar configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="c3d8d-211">Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="c3d8d-212">Acceso mediante programación al valor de una configuración personalizada</span><span class="sxs-lookup"><span data-stu-id="c3d8d-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="c3d8d-213">Hello pasos siguientes muestran cómo tooprogrammatically tener acceso a una configuración personalizada mediante C#.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="c3d8d-214">Agregue Hola siguiente mediante directivas tooa C# archivo donde se va configuración de Hola toouse:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="c3d8d-215">Hello código siguiente muestra un ejemplo de cómo tooaccess una configuración personalizada.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="c3d8d-216">Reemplace hello &lt;SettingName > marcador de posición con el valor adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="c3d8d-217">Administrar el almacenamiento local para cada instancia de rol</span><span class="sxs-lookup"><span data-stu-id="c3d8d-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="c3d8d-218">Puede agregar almacenamiento del sistema de archivos local para cada instancia de un rol.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="c3d8d-219">Hola datos almacenados en almacenamiento no es accesible por otras instancias de rol de Hola para qué Hola se almacenan los datos, o por otras funciones.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="c3d8d-220">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c3d8d-221">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="c3d8d-222">En hello **Roles** nodo, un rol Hola contextual desea tooupdate y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menú contextual del rol de Azure en el Explorador de soluciones](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="c3d8d-224">Seleccione hello **almacenamiento Local** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-224">Select hello **Local Storage** tab.</span></span>

    ![Pestaña Almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="c3d8d-226">Hola **configuración del servicio** lista, asegúrese de que **todas las configuraciones de** se selecciona como configuración de almacenamiento local de hello aplica configuraciones de servicio de tooall.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="c3d8d-227">Cualquier otro valor producirá todos los campos de entrada de hello en página de Hola que se va a deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Lista Configuración de servicio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="c3d8d-229">Seleccione una entrada de almacenamiento local, tooadd **agregar almacenamiento Local**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Agregar almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="c3d8d-231">Una vez que se ha agregado toohello lista a nueva entrada de almacenamiento local de hello, actualizar la fila de hello en lista de hello con información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nueva entrada de almacenamiento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="c3d8d-233">**Nombre de** -escriba nombre de Hola que quiere toouse para el almacenamiento local de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="c3d8d-234">**Tamaño (MB)** -especifique el tamaño de hello en MB que necesita para el almacenamiento local de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="c3d8d-235">**Limpieza de reciclado de rol** -seleccionar estos datos de opción tooremove hello en almacenamiento local de hello nueva cuando se recicla la máquina virtual de hello para el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="c3d8d-236">toodelete una entrada de almacenamiento local, seleccione la entrada de hello y, a continuación, seleccione **quitar almacenamiento Local**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="c3d8d-237">Desde Visual Studio, Hola barra de herramientas, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="c3d8d-238">Acceso mediante programación al almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="c3d8d-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="c3d8d-239">Esta sección muestra cómo tooprogrammatically tener acceso a almacenamiento local utilizando C# mediante la escritura de un archivo de texto de prueba `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="c3d8d-240">Escribir un almacenamiento de toolocal del archivo de texto</span><span class="sxs-lookup"><span data-stu-id="c3d8d-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="c3d8d-241">Hola siguiente código muestra un ejemplo de cómo toolocal almacenamiento de archivos en toowrite un texto.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="c3d8d-242">Reemplace hello &lt;LocalStorageName > marcador de posición con el valor adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

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

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="c3d8d-243">Buscar un archivo escrito toolocal almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c3d8d-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="c3d8d-244">archivo de hello tooview creado por código de hello en la sección anterior de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c3d8d-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="c3d8d-245">En Hola área de notificación de Windows, haga clic en el icono de Azure de hello y, en el menú contextual de hello, seleccione **Mostrar IU del emulador de proceso**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Mostrar el emulador de proceso de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="c3d8d-247">Seleccione el rol web de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-247">Select hello web role.</span></span>

    ![Emulador de proceso de Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="c3d8d-249">En hello **emulador de proceso de Microsoft Azure** menú, seleccione **herramientas** > **Abrir almacén local**.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Opción de menú Open local store (Abrir almacén local)](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="c3d8d-251">Cuando se abre la ventana del explorador de Windows hello, escriba ' MyLocalStorageTest.txt'' en hello **búsqueda** cuadro de texto y seleccione **ENTRAR** búsqueda de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="c3d8d-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3d8d-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3d8d-252">Next steps</span></span>
<span data-ttu-id="c3d8d-253">Para obtener más información sobre los proyectos de Azure en Visual Studio, consulte [Configurar un proyecto de Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="c3d8d-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="c3d8d-254">Más información sobre el esquema del servicio de nube Hola leyendo [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="c3d8d-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

