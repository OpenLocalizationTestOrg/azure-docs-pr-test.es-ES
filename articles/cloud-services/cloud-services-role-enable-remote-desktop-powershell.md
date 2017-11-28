---
title: "aaaEnable conexión a Escritorio remoto para un rol de servicios de nube de Azure mediante PowerShell"
description: "¿Cómo tooconfigure la nube de azure aplicación de servicio con PowerShell tooallow conexiones a Escritorio remoto"
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="e832d-103">Habilitación de la conexión a Escritorio remoto para un rol de Servicios en la nube de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e832d-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e832d-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e832d-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="e832d-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e832d-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="e832d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e832d-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="e832d-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e832d-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="e832d-108">Escritorio remoto permite escritorio de hello tooaccess de una función que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="e832d-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="e832d-109">Puede usar un tootroubleshoot de conexión de escritorio remoto y diagnosticar problemas con la aplicación mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="e832d-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="e832d-110">Este artículo se describe cómo tooenable escritorio remoto en los Roles de servicio de nube mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e832d-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="e832d-111">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo.</span><span class="sxs-lookup"><span data-stu-id="e832d-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="e832d-112">PowerShell utiliza Hola extensión de escritorio remoto, por lo que puede habilitar Escritorio remoto una vez implementada la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e832d-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="e832d-113">Configuración de Escritorio remoto desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="e832d-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="e832d-114">Hola [AzureServiceRemoteDesktopExtension conjunto](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet le permite tooenable escritorio remoto en los roles especificados o todos los roles de la implementación del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="e832d-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="e832d-115">Hola cmdlet le permite especificar Hola nombre de usuario y la contraseña de usuario de escritorio remoto de Hola a través de hello *credencial* parámetro que acepta un objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="e832d-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="e832d-116">Si usa PowerShell de forma interactiva, puede configurar fácilmente objeto de PSCredential Hola por llamada hello [obtener credenciales](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e832d-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="e832d-117">Este comando muestra un cuadro de diálogo que permite tooenter Hola nombre de usuario y contraseña de usuario remoto hello de forma segura.</span><span class="sxs-lookup"><span data-stu-id="e832d-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="e832d-118">Puesto que PowerShell ayuda a los escenarios de automatización, también puede configurar hello **PSCredential** objeto de forma que no requiere la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="e832d-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="e832d-119">En primer lugar, debe tooset una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="e832d-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="e832d-120">Empezar por la especificación de una contraseña de texto sin formato Convertir cadena segura tooa con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e832d-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="e832d-121">A continuación debe tooconvert esta cadena segura en una cadena cifrada estándar utilizando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="e832d-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="e832d-122">Ahora puede guardar este archivo de cadena estándar cifrada tooa mediante [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="e832d-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="e832d-123">También puede crear un archivo de contraseña segura para que no tengan tootype contraseña Hola cada vez.</span><span class="sxs-lookup"><span data-stu-id="e832d-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="e832d-124">Además, un archivo de contraseña segura es mejor que un archivo de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="e832d-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="e832d-125">Usar hello después PowerShell toocreate un archivo de contraseña segura:</span><span class="sxs-lookup"><span data-stu-id="e832d-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="e832d-126">Al establecer la contraseña de hello, asegúrese de que cumplen hello [requisitos de complejidad](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="e832d-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="e832d-127">objeto de credencial de hello toocreate de archivo de contraseña segura de hello, debe leer el contenido del archivo hello y convertirlos tooa atrás seguras a través de la cadena [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e832d-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="e832d-128">Hola [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet también acepta un *caducidad* parámetro, que especifica un **DateTime** en qué usuario Hola la cuenta expira.</span><span class="sxs-lookup"><span data-stu-id="e832d-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="e832d-129">Por ejemplo, podría establecer Hola cuenta tooexpire unos días de hello fecha y hora actuales.</span><span class="sxs-lookup"><span data-stu-id="e832d-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="e832d-130">Este ejemplo de PowerShell muestra cómo tooset Hola extensión de escritorio remoto en un servicio de nube:</span><span class="sxs-lookup"><span data-stu-id="e832d-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="e832d-131">Opcionalmente, también puede especificar ranura de implementación de Hola y roles que desee tooenable de escritorio remoto en.</span><span class="sxs-lookup"><span data-stu-id="e832d-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="e832d-132">Si no se especifican estos parámetros, Hola habilita Escritorio remoto en todos los roles de hello **producción** ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="e832d-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="e832d-133">Hola extensión de escritorio remoto está asociado a una implementación.</span><span class="sxs-lookup"><span data-stu-id="e832d-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="e832d-134">Si crea una nueva implementación para el servicio de hello, haya tooenable de escritorio remoto en esa implementación.</span><span class="sxs-lookup"><span data-stu-id="e832d-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="e832d-135">Si desea que siempre toohave escritorio remoto habilitado, debe considerar la integración de scripts de PowerShell de hello en el flujo de trabajo de implementación.</span><span class="sxs-lookup"><span data-stu-id="e832d-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="e832d-136">Escritorio remoto en una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="e832d-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="e832d-137">Hola [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet es escritorio tooremote usado en una instancia de rol específico de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="e832d-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="e832d-138">Puede usar hello *LocalPath* Hola de toodownload del parámetro RDP archivo localmente.</span><span class="sxs-lookup"><span data-stu-id="e832d-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="e832d-139">O bien puede usar hello *iniciar* tooaccess de cuadro de diálogo de conexión a Escritorio remoto de parámetro toodirectly inicio Hola Hola instancia de rol de servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="e832d-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="e832d-140">Comprobación de si la extensión de Escritorio remoto está habilitada en un servicio</span><span class="sxs-lookup"><span data-stu-id="e832d-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="e832d-141">Hola [AzureServiceRemoteDesktopExtension Get](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet muestra que Escritorio remoto está habilitado o deshabilitado en una implementación de servicio.</span><span class="sxs-lookup"><span data-stu-id="e832d-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="e832d-142">Hola cmdlet devuelve el nombre de usuario de Hola de usuario de escritorio remoto de Hola y Hola roles extensión de escritorio remoto de hello está habilitada para.</span><span class="sxs-lookup"><span data-stu-id="e832d-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="e832d-143">De forma predeterminada, esto se produce en la ranura de implementación de Hola y puede elegir hello toouse ranura de ensayo en su lugar.</span><span class="sxs-lookup"><span data-stu-id="e832d-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="e832d-144">Eliminación de la extensión de Escritorio remoto de un servicio</span><span class="sxs-lookup"><span data-stu-id="e832d-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="e832d-145">Si ya ha habilitado extensión de escritorio remoto de hello en una implementación, y necesita tooupdate Hola configuración de escritorio remoto, primero quite extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="e832d-146">Y vuelva a habilitarla con una nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="e832d-147">Por ejemplo, si desea que tooset una nueva contraseña para la cuenta de usuario remoto de Hola o cuenta de hello expirado.</span><span class="sxs-lookup"><span data-stu-id="e832d-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="e832d-148">Esto es necesario en las implementaciones existentes que tienen la extensión de escritorio remoto de hello habilitado.</span><span class="sxs-lookup"><span data-stu-id="e832d-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="e832d-149">Para nuevas implementaciones, puede simplemente aplicar extensión Hola directamente.</span><span class="sxs-lookup"><span data-stu-id="e832d-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="e832d-150">tooremove Hola remoto escritorio extensión de la implementación de hello, puede usar hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e832d-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="e832d-151">Opcionalmente, también puede especificar ranura de implementación de Hola y el rol del que desea que la extensión de escritorio remoto tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="e832d-152">configuración de la extensión de Hola de toocompletely remove, debe llamar a hello *quitar* cmdlet con hello **UninstallConfiguration** parámetro.</span><span class="sxs-lookup"><span data-stu-id="e832d-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="e832d-153">Hola **UninstallConfiguration** parámetro desinstala cualquier configuración de la extensión que es el servicio de toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="e832d-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="e832d-154">Cada configuración de la extensión está asociado a la configuración del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="e832d-155">Llamar a hello *quitar* cmdlet sin **UninstallConfiguration** desasocia hello <mark>implementación</mark> de configuración de la extensión de hello, lo que quitaría extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="e832d-156">Sin embargo, la configuración de la extensión de hello permanece asociada con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e832d-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="e832d-157">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e832d-157">Additional resources</span></span>

<span data-ttu-id="e832d-158">[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e832d-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
