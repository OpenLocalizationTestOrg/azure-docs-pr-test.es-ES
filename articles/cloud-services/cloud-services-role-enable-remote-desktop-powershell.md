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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Habilitación de la conexión a Escritorio remoto para un rol de Servicios en la nube de Azure mediante PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal de Azure clásico](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Escritorio remoto permite escritorio de hello tooaccess de una función que se ejecuta en Azure. Puede usar un tootroubleshoot de conexión de escritorio remoto y diagnosticar problemas con la aplicación mientras se está ejecutando.

Este artículo se describe cómo tooenable escritorio remoto en los Roles de servicio de nube mediante PowerShell. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) de requisitos previos de hello necesarios para este artículo. PowerShell utiliza Hola extensión de escritorio remoto, por lo que puede habilitar Escritorio remoto una vez implementada la aplicación hello.

## <a name="configure-remote-desktop-from-powershell"></a>Configuración de Escritorio remoto desde PowerShell
Hola [AzureServiceRemoteDesktopExtension conjunto](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet le permite tooenable escritorio remoto en los roles especificados o todos los roles de la implementación del servicio de nube. Hola cmdlet le permite especificar Hola nombre de usuario y la contraseña de usuario de escritorio remoto de Hola a través de hello *credencial* parámetro que acepta un objeto PSCredential.

Si usa PowerShell de forma interactiva, puede configurar fácilmente objeto de PSCredential Hola por llamada hello [obtener credenciales](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

Este comando muestra un cuadro de diálogo que permite tooenter Hola nombre de usuario y contraseña de usuario remoto hello de forma segura.

Puesto que PowerShell ayuda a los escenarios de automatización, también puede configurar hello **PSCredential** objeto de forma que no requiere la interacción del usuario. En primer lugar, debe tooset una contraseña segura. Empezar por la especificación de una contraseña de texto sin formato Convertir cadena segura tooa con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). A continuación debe tooconvert esta cadena segura en una cadena cifrada estándar utilizando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx). Ahora puede guardar este archivo de cadena estándar cifrada tooa mediante [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).

También puede crear un archivo de contraseña segura para que no tengan tootype contraseña Hola cada vez. Además, un archivo de contraseña segura es mejor que un archivo de texto sin formato. Usar hello después PowerShell toocreate un archivo de contraseña segura:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Al establecer la contraseña de hello, asegúrese de que cumplen hello [requisitos de complejidad](https://technet.microsoft.com/library/cc786468.aspx).
>
>

objeto de credencial de hello toocreate de archivo de contraseña segura de hello, debe leer el contenido del archivo hello y convertirlos tooa atrás seguras a través de la cadena [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Hola [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet también acepta un *caducidad* parámetro, que especifica un **DateTime** en qué usuario Hola la cuenta expira. Por ejemplo, podría establecer Hola cuenta tooexpire unos días de hello fecha y hora actuales.

Este ejemplo de PowerShell muestra cómo tooset Hola extensión de escritorio remoto en un servicio de nube:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Opcionalmente, también puede especificar ranura de implementación de Hola y roles que desee tooenable de escritorio remoto en. Si no se especifican estos parámetros, Hola habilita Escritorio remoto en todos los roles de hello **producción** ranura de implementación.

Hola extensión de escritorio remoto está asociado a una implementación. Si crea una nueva implementación para el servicio de hello, haya tooenable de escritorio remoto en esa implementación. Si desea que siempre toohave escritorio remoto habilitado, debe considerar la integración de scripts de PowerShell de hello en el flujo de trabajo de implementación.

## <a name="remote-desktop-into-a-role-instance"></a>Escritorio remoto en una instancia de rol
Hola [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet es escritorio tooremote usado en una instancia de rol específico de servicio en la nube. Puede usar hello *LocalPath* Hola de toodownload del parámetro RDP archivo localmente. O bien puede usar hello *iniciar* tooaccess de cuadro de diálogo de conexión a Escritorio remoto de parámetro toodirectly inicio Hola Hola instancia de rol de servicio de nube.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Comprobación de si la extensión de Escritorio remoto está habilitada en un servicio
Hola [AzureServiceRemoteDesktopExtension Get](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet muestra que Escritorio remoto está habilitado o deshabilitado en una implementación de servicio. Hola cmdlet devuelve el nombre de usuario de Hola de usuario de escritorio remoto de Hola y Hola roles extensión de escritorio remoto de hello está habilitada para. De forma predeterminada, esto se produce en la ranura de implementación de Hola y puede elegir hello toouse ranura de ensayo en su lugar.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Eliminación de la extensión de Escritorio remoto de un servicio
Si ya ha habilitado extensión de escritorio remoto de hello en una implementación, y necesita tooupdate Hola configuración de escritorio remoto, primero quite extensión Hola. Y vuelva a habilitarla con una nueva configuración de Hola. Por ejemplo, si desea que tooset una nueva contraseña para la cuenta de usuario remoto de Hola o cuenta de hello expirado. Esto es necesario en las implementaciones existentes que tienen la extensión de escritorio remoto de hello habilitado. Para nuevas implementaciones, puede simplemente aplicar extensión Hola directamente.

tooremove Hola remoto escritorio extensión de la implementación de hello, puede usar hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. Opcionalmente, también puede especificar ranura de implementación de Hola y el rol del que desea que la extensión de escritorio remoto tooremove Hola.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configuración de la extensión de Hola de toocompletely remove, debe llamar a hello *quitar* cmdlet con hello **UninstallConfiguration** parámetro.
>
> Hola **UninstallConfiguration** parámetro desinstala cualquier configuración de la extensión que es el servicio de toohello aplicado. Cada configuración de la extensión está asociado a la configuración del servicio Hola. Llamar a hello *quitar* cmdlet sin **UninstallConfiguration** desasocia hello <mark>implementación</mark> de configuración de la extensión de hello, lo que quitaría extensión de Hola. Sin embargo, la configuración de la extensión de hello permanece asociada con el servicio de Hola.
>
>

## <a name="additional-resources"></a>Recursos adicionales

[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)
