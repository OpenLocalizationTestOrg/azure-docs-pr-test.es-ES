---
title: "Habilitación de la conexión a Escritorio remoto para un rol de Servicios en la nube de Azure mediante PowerShell"
description: "Configuración de la aplicación de servicios en la nube de Azure con PowerShell para permitir conexiones a Escritorio remoto"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="3dac8-103">Habilitación de la conexión a Escritorio remoto para un rol de Servicios en la nube de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dac8-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3dac8-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3dac8-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="3dac8-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="3dac8-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="3dac8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dac8-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="3dac8-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3dac8-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="3dac8-108">Escritorio remoto le permite tener acceso al escritorio de un rol que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="3dac8-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="3dac8-109">Puede usar la conexión de Escritorio remoto para solucionar y diagnosticar problemas con su aplicación mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="3dac8-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="3dac8-110">En este artículo se describe cómo habilitar Escritorio remoto en los roles del servicio en la nube con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dac8-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="3dac8-111">Para conocer los requisitos previos necesarios para este artículo, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3dac8-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="3dac8-112">PowerShell usa la extensión de Escritorio remoto, por lo que Escritorio remoto se puede habilitar después de la implementación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dac8-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="3dac8-113">Configuración de Escritorio remoto desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dac8-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="3dac8-114">El cmdlet [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) permite habilitar Escritorio remoto en los roles especificados o en todos los roles de la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3dac8-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="3dac8-115">Este cmdlet permite especificar el nombre de usuario y la contraseña del usuario de Escritorio remoto a través del parámetro *Credential* , que acepta un objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="3dac8-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="3dac8-116">Si PowerShell se usa de forma interactiva, el objeto PSCredential se puede establecer fácilmente mediante una llamada al cmdlet [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3dac8-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="3dac8-117">Este comando muestra un cuadro de diálogo que permite especificar el nombre de usuario y la contraseña del usuario remoto de forma segura.</span><span class="sxs-lookup"><span data-stu-id="3dac8-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="3dac8-118">Dado que PowerShell sirve de ayuda en los escenarios de automatización, también es posible configurar el objeto **PSCredential** de manera que no requiera la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="3dac8-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="3dac8-119">En primer lugar es preciso configurar una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="3dac8-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="3dac8-120">Para empezar, es preciso especificar una contraseña de texto sin formato y convertirla en una cadena segura con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="3dac8-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="3dac8-121">Seguidamente, hay que convertir esta cadena segura en una cadena estándar cifrada, para lo que se usa [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="3dac8-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="3dac8-122">Ya se puede guardar la cadena estándar cifrada en un archivo con [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="3dac8-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="3dac8-123">También puede crear un archivo de contraseña segura para que no tenga que escribir la contraseña cada vez.</span><span class="sxs-lookup"><span data-stu-id="3dac8-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="3dac8-124">Además, un archivo de contraseña segura es mejor que un archivo de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="3dac8-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="3dac8-125">Use la siguiente instrucción de PowerShell para crear un archivo de contraseña seguro:</span><span class="sxs-lookup"><span data-stu-id="3dac8-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="3dac8-126">Al establecer la contraseña asegúrese de cumplir los [requisitos de complejidad](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="3dac8-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="3dac8-127">Para crear el objeto de credencial desde el archivo de contraseña seguro debe leer el contenido del archivo y convertirlo en una cadena segura con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="3dac8-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="3dac8-128">El cmdlet [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) también acepta un parámetro *Expiration* que especifica un valor **DateTime** en que la cuenta de usuario caducará.</span><span class="sxs-lookup"><span data-stu-id="3dac8-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="3dac8-129">Por ejemplo, puede establecer que la cuenta caduque unos días después de la fecha y hora actuales.</span><span class="sxs-lookup"><span data-stu-id="3dac8-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="3dac8-130">En este ejemplo de PowerShell se muestra cómo establecer la extensión de Escritorio remoto en un servicio en la nube:</span><span class="sxs-lookup"><span data-stu-id="3dac8-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="3dac8-131">Opcionalmente, también puede especificar la ranura de implementación y los roles en que desea habilitar Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="3dac8-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="3dac8-132">Si no se especifican estos parámetros, el cmdlet habilita el Escritorio remoto en todos los roles de la ranura de implementación de **producción** .</span><span class="sxs-lookup"><span data-stu-id="3dac8-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="3dac8-133">La extensión de Escritorio remoto se asocia con una implementación.</span><span class="sxs-lookup"><span data-stu-id="3dac8-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="3dac8-134">Si crea una nueva implementación para el servicio, tendrá que habilitar el Escritorio remoto en la nueva implementación.</span><span class="sxs-lookup"><span data-stu-id="3dac8-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="3dac8-135">Si desea que Escritorio remoto esté siempre habilitado, debe considerar la integración de scripts de PowerShell en el flujo de trabajo de implementación.</span><span class="sxs-lookup"><span data-stu-id="3dac8-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="3dac8-136">Escritorio remoto en una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="3dac8-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="3dac8-137">El cmdlet [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) se usa para introducir Escritorio remoto en una instancia de rol específica del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3dac8-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="3dac8-138">Puede usar el parámetro *LocalPath* para descargar el archivo RDP localmente.</span><span class="sxs-lookup"><span data-stu-id="3dac8-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="3dac8-139">O bien puede usar el parámetro *Launch* para iniciar directamente el cuadro de diálogo Conexión a Escritorio remoto para tener acceso a la instancia de rol del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="3dac8-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="3dac8-140">Comprobación de si la extensión de Escritorio remoto está habilitada en un servicio</span><span class="sxs-lookup"><span data-stu-id="3dac8-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="3dac8-141">El cmdlet [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) muestra si Escritorio remoto está habilitado o no en una implementación de servicio.</span><span class="sxs-lookup"><span data-stu-id="3dac8-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="3dac8-142">El cmdlet devuelve el nombre de usuario del usuario de Escritorio remoto y los roles en la que está habilitada la extensión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="3dac8-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="3dac8-143">De forma predeterminada, esto se realiza en la ranura de implementación y se puede utilizar la ranura de ensayo en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3dac8-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="3dac8-144">Eliminación de la extensión de Escritorio remoto de un servicio</span><span class="sxs-lookup"><span data-stu-id="3dac8-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="3dac8-145">Si ya habilitó la extensión de Escritorio remoto en una implementación y necesita actualizar la configuración de Escritorio remota, primero debe quitar la extensión.</span><span class="sxs-lookup"><span data-stu-id="3dac8-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="3dac8-146">Y, después, volver a habilitarla con la nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="3dac8-146">And enable it again with the new settings.</span></span> <span data-ttu-id="3dac8-147">Por ejemplo, si quiere establecer una nueva contraseña para la cuenta de usuario remoto o porque la cuenta ha caducado.</span><span class="sxs-lookup"><span data-stu-id="3dac8-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="3dac8-148">Esto solo se requiere en las implementaciones existentes que tienen la extensión de Escritorio remoto habilitada.</span><span class="sxs-lookup"><span data-stu-id="3dac8-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="3dac8-149">En las nuevas implementaciones, simplemente aplique la extensión directamente.</span><span class="sxs-lookup"><span data-stu-id="3dac8-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="3dac8-150">Para quitar la extensión de Escritorio remoto de la implementación, puede usar el cmdlet [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="3dac8-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="3dac8-151">Opcionalmente, también puede especificar la ranura de implementación y los roles de los que desea habilitar la extensión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="3dac8-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="3dac8-152">Para quitar completamente la configuración de la extensión se debe llamar al cmdlet *remove* con el parámetro **UninstallConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="3dac8-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="3dac8-153">El parámetro **UninstallConfiguration** desinstala cualquier configuración de la extensión que se aplica al servicio.</span><span class="sxs-lookup"><span data-stu-id="3dac8-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="3dac8-154">Cada configuración de la extensión se asocia a la configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="3dac8-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="3dac8-155">Si se llama al cmdlet *remove* sin **UninstallConfiguration**, se desasocia la <mark>implementación</mark> de la configuración de la extensión, con lo que se quitará eficazmente la extensión.</span><span class="sxs-lookup"><span data-stu-id="3dac8-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="3dac8-156">Sin embargo, la configuración de la extensión sigue estando asociada al servicio.</span><span class="sxs-lookup"><span data-stu-id="3dac8-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="3dac8-157">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3dac8-157">Additional resources</span></span>

<span data-ttu-id="3dac8-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md) (Configuración de Cloud Services)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md) (Preguntas frecuentes sobre Cloud Services > Escritorio remoto)</span><span class="sxs-lookup"><span data-stu-id="3dac8-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
