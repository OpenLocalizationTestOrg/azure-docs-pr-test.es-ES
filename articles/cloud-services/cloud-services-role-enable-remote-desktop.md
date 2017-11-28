---
title: "Habilitación de Escritorio remoto para un servicio Azure Cloud Services | Microsoft Docs"
description: "Configuración de la aplicación de servicios en la nube de Azure para permitir conexiones a Escritorio remoto"
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
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="01e55-103">Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="01e55-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01e55-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="01e55-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="01e55-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="01e55-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="01e55-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01e55-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="01e55-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01e55-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="01e55-108">Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de los módulos de Escritorio remoto en la definición de servicio, o puede habilitar Escritorio remoto a través de la extensión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="01e55-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="01e55-109">El método preferido es usar la extensión de Escritorio remoto dado que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación sin tener que volver a implementarla.</span><span class="sxs-lookup"><span data-stu-id="01e55-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="01e55-110">Configuración de Escritorio remoto desde el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="01e55-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="01e55-111">El Portal de Azure clásico usa el método de extensión de Escritorio remoto, por lo que puede habilitar Escritorio remoto incluso después de que se implemente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01e55-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="01e55-112">En la pagina **Configurar** de su servicio en la nube, puede habilitar Escritorio remoto, cambiar la cuenta de Administrador local usada para conectarse a las máquinas virtuales o el certificado que se usa en la autenticación y definir la fecha de caducidad.</span><span class="sxs-lookup"><span data-stu-id="01e55-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="01e55-113">Haga clic en **Cloud Services**, en el nombre del servicio en la nube y, a continuación, en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="01e55-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="01e55-114">Haga clic en el botón **Remoto** situado en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="01e55-114">Click the **Remote** button at the bottom.</span></span>

    ![Servicios en la nube remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="01e55-116">se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="01e55-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="01e55-117">Para evitar un reinicio, el certificado que se usó para cifrar la contraseña debe instalarse en el rol.</span><span class="sxs-lookup"><span data-stu-id="01e55-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="01e55-118">Para evitar un reinicio, [cargue un certificado para el servicio en la nube](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, luego, vuelva a este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01e55-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="01e55-119">En **Roles**, seleccione el rol de servicio que desea actualizar o seleccione **Todos** para todos los roles.</span><span class="sxs-lookup"><span data-stu-id="01e55-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="01e55-120">Realice alguno de los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="01e55-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="01e55-121">Para habilitar Escritorio remoto, seleccione la casilla **Habilitar Escritorio remoto** .</span><span class="sxs-lookup"><span data-stu-id="01e55-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="01e55-122">Para deshabilitar el Escritorio remoto, desmarque la casilla.</span><span class="sxs-lookup"><span data-stu-id="01e55-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="01e55-123">Cree una cuenta para usarla en las conexiones de Escritorio remoto con las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="01e55-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="01e55-124">Actualice la contraseña de la cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="01e55-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="01e55-125">Seleccione un certificado cargado para usar en la autenticación (cargue el certificado usando **Cargar** en la página **Certificados**) o cree un certificado nuevo.</span><span class="sxs-lookup"><span data-stu-id="01e55-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="01e55-126">Cambie la fecha de caducidad para la configuración de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="01e55-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="01e55-127">Después terminar las actualizaciones de la configuración, haga clic en **Aceptar** (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="01e55-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="01e55-128">Acceso remoto en instancias de rol</span><span class="sxs-lookup"><span data-stu-id="01e55-128">Remote into role instances</span></span>
<span data-ttu-id="01e55-129">Una vez que Escritorio remoto está habilitado en los roles, puede conectarse de forma remota a una instancia de rol a través de varias herramientas.</span><span class="sxs-lookup"><span data-stu-id="01e55-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="01e55-130">Para conectarse a una instancia de rol desde el Portal de Azure clásico:</span><span class="sxs-lookup"><span data-stu-id="01e55-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="01e55-131">Haga clic en **Instancias** para abrir la página **Instancias**.</span><span class="sxs-lookup"><span data-stu-id="01e55-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="01e55-132">Seleccione una instancia de rol que tenga el Escritorio remoto configurado.</span><span class="sxs-lookup"><span data-stu-id="01e55-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="01e55-133">Haga clic en **Conectar**y siga las instrucciones para abrir el escritorio.</span><span class="sxs-lookup"><span data-stu-id="01e55-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="01e55-134">Haga clic en **Abrir** y, a continuación, en **Conectar** para iniciar la conexión del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="01e55-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="01e55-135">Uso de Visual Studio para conectarse de forma remota a una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="01e55-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="01e55-136">En el Explorador de servidores de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="01e55-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="01e55-137">Expanda el nodo **Azure** > **Cloud Services** > **[nombre del servicio en la nube]**.</span><span class="sxs-lookup"><span data-stu-id="01e55-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="01e55-138">Expanda **Almacenamiento provisional** o **Producción**.</span><span class="sxs-lookup"><span data-stu-id="01e55-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="01e55-139">Expanda el rol individual.</span><span class="sxs-lookup"><span data-stu-id="01e55-139">Expand the individual role.</span></span>
4. <span data-ttu-id="01e55-140">Haga clic con el botón derecho en una de las instancias de rol, haga clic en **Conectar con Escritorio remoto...**y, luego, escriba el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="01e55-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![Escritorio remoto del Explorador de servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="01e55-142">Uso de PowerShell para obtener el archivo RDP</span><span class="sxs-lookup"><span data-stu-id="01e55-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="01e55-143">Puede usar el cmdlet [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) para recuperar el archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="01e55-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="01e55-144">Luego, puede usar este archivo con Conexión a Escritorio remoto para tener acceso al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="01e55-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="01e55-145">Descarga del archivo RDP mediante programación a través de la API de REST de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="01e55-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="01e55-146">Puede usar la operación de REST [Descargar archivo RDP](https://msdn.microsoft.com/library/jj157183.aspx) para descargar el archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="01e55-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="01e55-147">Para configurar Escritorio remoto en el archivo de definición de servicio</span><span class="sxs-lookup"><span data-stu-id="01e55-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="01e55-148">Este método permite habilitar Escritorio remoto para la aplicación durante el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="01e55-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="01e55-149">Este enfoque requiere el almacenamiento de contraseñas cifradas en el archivo de configuración de servicio y cualquier actualización a la configuración de Escritorio remoto requeriría que se volviera a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01e55-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="01e55-150">Si desea evitar estas desventajas, debe usar el enfoque de extensión de Escritorio remoto descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01e55-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="01e55-151">Puede usar Visual Studio para [habilitar una conexión a Escritorio remoto](../vs-azure-tools-remote-desktop-roles.md) mediante el enfoque de archivo de definición de servicio.</span><span class="sxs-lookup"><span data-stu-id="01e55-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="01e55-152">Los pasos siguientes describen los cambios necesarios en los archivos de modelo de servicio para habilitar Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="01e55-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="01e55-153">Visual Studio realizará estos cambios automáticamente al publicar.</span><span class="sxs-lookup"><span data-stu-id="01e55-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="01e55-154">Configuración de la conexión en el modelo de servicio</span><span class="sxs-lookup"><span data-stu-id="01e55-154">Set up the connection in the service model</span></span>
<span data-ttu-id="01e55-155">Use el elemento **Importaciones** para importar el módulo **RemoteAccess** y el módulo **RemoteForwarder** para el archivo [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef).</span><span class="sxs-lookup"><span data-stu-id="01e55-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="01e55-156">El archivo de definición de servicio debe parecerse al ejemplo siguiente con el elemento `<Imports>` agregado.</span><span class="sxs-lookup"><span data-stu-id="01e55-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

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
<span data-ttu-id="01e55-157">El archivo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) debe parecerse al ejemplo siguiente; observe los elementos `<ConfigurationSettings>` y `<Certificates>`.</span><span class="sxs-lookup"><span data-stu-id="01e55-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="01e55-158">El certificado especificado debe [cargarse en el servicio en la nube](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="01e55-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="01e55-159">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="01e55-159">Additional Resources</span></span>
<span data-ttu-id="01e55-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md) (Configuración de Cloud Services)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md) (Preguntas frecuentes sobre Cloud Services > Escritorio remoto)</span><span class="sxs-lookup"><span data-stu-id="01e55-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
