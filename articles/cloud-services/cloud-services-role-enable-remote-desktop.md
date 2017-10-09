---
title: aaaEnable escritorio remoto en un servicio de nube de Azure | Documentos de Microsoft
description: "¿Cómo tooconfigure la nube de azure conexiones de escritorio remoto de tooallow de aplicación de servicio"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="868a1-103">Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="868a1-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="868a1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="868a1-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="868a1-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="868a1-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="868a1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="868a1-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="868a1-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="868a1-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="868a1-108">Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de módulos de escritorio remoto de hello en la definición de servicio o puede elegir tooenable escritorio remoto a través de hello extensión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="868a1-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="868a1-109">Hello método preferido es extensión de escritorio remoto de hello toouse tal y como se puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello sin necesidad de tooredeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="868a1-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="868a1-110">Configurar Escritorio remoto desde el portal de Azure clásico Hola</span><span class="sxs-lookup"><span data-stu-id="868a1-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="868a1-111">Hola portal de Azure clásico utiliza el método de extensión de escritorio remoto de Hola por lo que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="868a1-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="868a1-112">Hola **configurar** página de servicio en la nube permite tooenable escritorio remoto, Hola cambiar cuenta de administrador local usa máquinas virtuales de tooconnect toohello, certificado Hola utilizada en la autenticación y establece Hola fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="868a1-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="868a1-113">Haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="868a1-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="868a1-114">Haga clic en hello **remoto** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Servicios en la nube remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="868a1-116">se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="868a1-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="868a1-117">tooprevent un reinicio, contraseña de Hola de hello certificado tooencrypt usado debe estar instalado en el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="868a1-118">tooprevent un reinicio, [cargar un certificado de servicio en la nube hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, a continuación, devolver toothis cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="868a1-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="868a1-119">En **Roles**, seleccione el rol de Hola que desee tooupdate o seleccione **todos los** para todos los roles.</span><span class="sxs-lookup"><span data-stu-id="868a1-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="868a1-120">Realice uno de hello siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="868a1-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="868a1-121">Escritorio remoto, seleccione hello tooenable **habilitar Escritorio remoto** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="868a1-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="868a1-122">toodisable escritorio remoto, Hola desactive casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="868a1-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="868a1-123">Crear una cuenta toouse en conexiones de escritorio remoto toohello instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="868a1-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="868a1-124">Actualice la contraseña de hello cuenta existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="868a1-125">Seleccione un toouse los certificados cargados para la autenticación (carga Hola certificado mediante **cargar** en hello **certificados** página) o crear un nuevo certificado.</span><span class="sxs-lookup"><span data-stu-id="868a1-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="868a1-126">Cambiar la fecha de expiración de hello para la configuración de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="868a1-127">Después terminar las actualizaciones de la configuración, haga clic en **Aceptar** (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="868a1-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="868a1-128">Acceso remoto en instancias de rol</span><span class="sxs-lookup"><span data-stu-id="868a1-128">Remote into role instances</span></span>
<span data-ttu-id="868a1-129">Una vez que Escritorio remoto está habilitado en los roles de hello puede remoto en una instancia de rol a través de varias herramientas.</span><span class="sxs-lookup"><span data-stu-id="868a1-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="868a1-130">instancia de rol tooconnect tooa de hello portal de Azure clásico:</span><span class="sxs-lookup"><span data-stu-id="868a1-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="868a1-131">Haga clic en **instancias** tooopen hello **instancias** página.</span><span class="sxs-lookup"><span data-stu-id="868a1-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="868a1-132">Seleccione una instancia de rol que tenga el Escritorio remoto configurado.</span><span class="sxs-lookup"><span data-stu-id="868a1-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="868a1-133">Haga clic en **conectar**y siga el escritorio de hello instrucciones tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="868a1-134">Haga clic en **abiertos** y, a continuación, **conectar** toostart Hola conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="868a1-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="868a1-135">Usar Visual Studio tooremote en una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="868a1-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="868a1-136">En el Explorador de servidores de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="868a1-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="868a1-137">Expanda hello **Azure** > **servicios en la nube** > **[nombre de servicio de nube]** nodo.</span><span class="sxs-lookup"><span data-stu-id="868a1-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="868a1-138">Expanda **Almacenamiento provisional** o **Producción**.</span><span class="sxs-lookup"><span data-stu-id="868a1-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="868a1-139">Expanda el rol individual Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="868a1-140">Haga clic en una de las instancias de rol de hello, haga clic en **conectar utilizando Escritorio remoto...** y, a continuación, escriba Hola nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="868a1-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Escritorio remoto del Explorador de servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="868a1-142">Usar el archivo RDP de PowerShell tooget Hola</span><span class="sxs-lookup"><span data-stu-id="868a1-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="868a1-143">Puede usar hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) archivo RDP de cmdlet tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="868a1-144">A continuación, puede usar archivo RDP de hello con servicio de nube de hello tooaccess de conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="868a1-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="868a1-145">Descargar mediante programación el archivo RDP de Hola a través de la API de REST de administración de servicios de Hola</span><span class="sxs-lookup"><span data-stu-id="868a1-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="868a1-146">Puede usar hello [Descargar archivo RDP](https://msdn.microsoft.com/library/jj157183.aspx) archivo RDP de REST operación toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="868a1-147">Escritorio remoto en el archivo de definición de servicio de hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="868a1-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="868a1-148">Este método permite tooenable escritorio remoto para la aplicación hello durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="868a1-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="868a1-149">Este enfoque requiere contraseñas cifradas se almacena en la configuración del servicio archivo y cualquier configuración de escritorio remoto de toohello de actualizaciones requeriría una nueva implementación de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="868a1-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="868a1-150">Si desea que tooavoid estas desventajas que debe usar la extensión de escritorio remoto de hello enfoque basado en que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="868a1-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="868a1-151">Puede usar Visual Studio demasiado[habilitar una conexión a escritorio remota](../vs-azure-tools-remote-desktop-roles.md) mediante el enfoque de archivo de definición de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="868a1-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="868a1-152">Hola pasos siguientes describe Hola cambios necesarios toohello servicio modelo archivos tooenable escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="868a1-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="868a1-153">Visual Studio realizará estos cambios automáticamente al publicar.</span><span class="sxs-lookup"><span data-stu-id="868a1-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="868a1-154">Configurar conexión de hello en el modelo de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="868a1-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="868a1-155">Hola de uso **importaciones** Hola de elemento tooimport **RemoteAccess** hello y módulo **RemoteForwarder** módulo toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) archivo.</span><span class="sxs-lookup"><span data-stu-id="868a1-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="868a1-156">Hello archivo de definición de servicio debe ser similar toohello siguiente ejemplo con hello `<Imports>` elemento agregado.</span><span class="sxs-lookup"><span data-stu-id="868a1-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="868a1-157">Hola [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) archivo debe ser similar toohello siguiente ejemplo, tenga en cuenta hello `<ConfigurationSettings>` y `<Certificates>` elementos.</span><span class="sxs-lookup"><span data-stu-id="868a1-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="868a1-158">Hola certificado especificado debe ser [cargado el servicio en la nube toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="868a1-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="868a1-159">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="868a1-159">Additional Resources</span></span>
<span data-ttu-id="868a1-160">[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="868a1-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
