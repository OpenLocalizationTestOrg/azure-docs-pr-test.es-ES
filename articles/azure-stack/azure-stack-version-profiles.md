---
title: "perfiles de la versión de aaaUsing API en la pila de Azure | Documentos de Microsoft"
description: "Aprenda los perfiles de la versión de API en Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a>Administre los perfiles de la versión de API en Azure Stack

Perfiles de la versión de API proporcionan una manera toomanage diferencias de versión entre Azure y la pila de Azure. Un perfil de la versión de la API es un conjunto de módulos de PowerShell AzureRM con versiones específicas de la API. Cada plataforma de la nube tiene un conjunto de perfiles de versión de API compatibles. Por ejemplo, pila de Azure es compatible con una versión de perfil con fecha específico como **2017-03-09-perfil**, Azure es compatible con hello y **más reciente** perfil de la versión de API. Cuando se instala un perfil, hello módulos AzureRM PowerShell correspondientes toohello especificadas perfil están instaladas.

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a>Instalar perfiles de la versión de Hola PowerShell los módulos necesarios toouse API

Hola **AzureRM.Bootstrapper** módulo que está disponible a través de hello Galería de PowerShell proporciona cmdlets de PowerShell que son necesario toowork con perfiles de la versión de API. Usar hello después de módulo de cmdlets tooinstall Hola AzureRM.Bootstrapper:

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
módulo de Hello AzureRM.Bootstrapper está en vista previa; detalles y las funcionalidades están toochange de asunto. toodownload e instalar Hola versión más reciente de este módulo de hello Galería de PowerShell, ejecute hello siguiente cmdlet:

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>Instalar un perfil

Hola de uso **Install-AzureRmProfile** cmdlet con hello **2017-03-09-perfil** API versión perfil tooinstall hello AzureRM módulos requeridos por la pila de Azure. Tenga en cuenta que no se instalan módulos de administrador de hello pila de Azure en la nube con este perfil de la versión de API, y deben instalarse por separado según lo especificado en hello paso 3 de hello [instale PowerShell para Azure pila](azure-stack-powershell-install.md) artículo.

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>Instalar e importar módulos en un perfil

Hola de uso **AzureRmProfile Use** módulos tooinstall e importación de cmdlets que están asociados a un perfil de la versión de API. Puede importar un solo perfil de la versión de la API en una sesión de PowerShell. perfil de la versión de tooimport una API diferente, debe abrir una nueva sesión de PowerShell. Hola siguiente las tareas ejecuta el cmdlet de Hello AzureRMProfile de uso:  
1. Comprueba si el perfil de versión de API especificado de módulos de PowerShell de hello asociados con hello se instala en el ámbito actual de Hola.  
2. Descarga e instala los módulos de hello si ya no están instalados.   
3. Importaciones Hola módulos en la sesión actual de PowerShell de Hola. 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

tooinstall e importación seleccionan AzureRM módulos de un perfil de versión de API, ejecute el cmdlet hello AzureRMProfile de uso con hello **módulo** parámetro:

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a>Obtener perfiles Hola instalado

Hola de uso **AzureRmProfile Get** lista de cmdlets tooget Hola de perfiles de versión de API disponibles: 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>Administrar perfiles

Hola de uso **AzureRmProfile actualización** módulos de cmdlet tooupdate hello en una versión perfil toohello última versión de API de módulos que están disponibles en Hola PSGallery. Se recomienda tooalways ejecute hello **AzureRmProfile actualización** cmdlet en una nueva tooavoid de sesión de PowerShell entra en conflicto al importar módulos. Hola siguiente las tareas ejecuta el cmdlet de Hello AzureRmProfile de actualización:

1. Comprueba si las últimas versiones de Hola de módulos se instalan en hello dado el perfil de la versión de API para el ámbito actual de Hola.  
2. Le pide que tooinstall si no están ya instalados.  
3. Instala e importa módulos Hola actualizado en la sesión actual de PowerShell de Hola.  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

versiones de hello previamente instalado tooremove de módulos de hello antes de actualizar toohello última versión disponible, usar el cmdlet de hello AzureRmProfile actualización junto con hello **- RemovePreviousVersions** parámetro:

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

Este cmdlet ejecuta Hola siguientes tareas:  

1. Comprueba si las últimas versiones de Hola de módulos se instalan en hello dado el perfil de la versión de API para el ámbito actual de Hola.  
2. Quita las versiones anteriores de Hola de módulos de perfil de versión de API actual de Hola y en la sesión actual de PowerShell de Hola.  
4. le versión más reciente de tooinstall Hola.  
5. Instala e importa módulos Hola actualizado en la sesión actual de PowerShell de Hola.  
 
## <a name="uninstall-profiles"></a>Desinstalar perfiles

Hola de uso **AzureRmProfile desinstalar** cmdlet toouninstall Hola especifica el perfil de la versión de API.

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>Pasos siguientes
* [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Instalación de PowerShell para Azure Stack)
* [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md)  
