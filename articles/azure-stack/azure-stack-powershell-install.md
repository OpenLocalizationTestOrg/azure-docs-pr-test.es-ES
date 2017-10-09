---
title: aaaInstall PowerShell para Azure pila | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall PowerShell para la pila de Azure."
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
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a>Instalación de PowerShell para Azure Stack  

Módulos de PowerShell de Azure compatibles de pila de Azure son necesario toowork con la pila de Azure. En esta guía, le guiaremos por hello pasos necesarios tooinstall PowerShell para la pila de Azure. Puede usar los pasos de hello descritos en este artículo desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN.

En este artículo, se detallaron instrucciones tooinstall PowerShell para la pila de Azure. Sin embargo, si lo desea tooquickly instalación y configuración de PowerShell, puede usar script de Hola que se proporciona en hello [ponerse a trabajar con PowerShell](azure-stack-powershell-configure-quickstart.md) tema. 

> [!NOTE]
> Hola pasos requiere PowerShell 5.0. toocheck su versión, ejecución de comparación e $PSVersionTable.PSVersion Hola "Principal" versión.

Comandos de PowerShell para Azure pila se instalan a través de la Galería de PowerShell de Hola. tooregiser Hola PSGallery repositorio, abra una sesión de PowerShell con privilegios elevados desde el kit de desarrollo de Hola o desde un cliente externo basado en Windows, si está conectado a través de VPN y ejecute el siguiente comando de hello:

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>Desinstalación de las versiones existentes de PowerShell

Antes de instalar la versión requerida de hello, asegúrese de que los desinstale los módulos de PowerShell de Azure existentes. Puede desinstalarlos mediante uno de hello siguiendo dos métodos:

* toouninstall Hola módulos de PowerShell existentes, inicie sesión en el kit de desarrollo de toohello o basados en Windows toohello los clientes externos si tiene previsto tooestablish una conexión VPN. Cierre todas las sesiones activas de PowerShell de Hola y Hola ejecución siguiente comando: 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* Inicie sesión en el kit de desarrollo de toohello o basados en Windows toohello los clientes externos si tiene previsto tooestablish una conexión VPN. Eliminar todas las carpetas de Hola que empiezan con "Azure" de hello `C:\Program Files (x86)\WindowsPowerShell\Modules` y `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` carpetas. Al eliminar estas carpetas, quitan los módulos de PowerShell existentes de Hola "AzureStackAdmin" y ámbitos de usuario "global". 

Hello siguientes secciones describen Hola pasos necesarios tooinstall PowerShell para la pila de Azure. PowerShell puede instalarse en Azure Stack que opere en un escenario conectado, parcialmente conectado o sin conexión. 

## <a name="install-powershell-in-a-connected-scenario"></a>Instalación de PowerShell en un escenario conectado 

Los módulos AzureRM compatibles con Azure Stack se instalan a través de perfiles de la versión de API. Pila de Azure requiere hello **2017-03-09-perfil** perfil de versión de API, que está disponible mediante la instalación de módulo de AzureRM.Bootstrapper Hola. toolearn sobre perfiles de la versión de API y cmdlets de hello proporcionada por ellos, consulte toohello [administrar perfiles de la versión de API](azure-stack-version-profiles.md). En los módulos de suma toohello AzureRM, también debe instalar los módulos de PowerShell de Azure específica de la pila de Hola. Ejecute hello después tooinstall de secuencia de comandos de PowerShell estos módulos en la estación de trabajo de desarrollo:

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

instalación de hello tooconfirm, ejecute el siguiente comando de hello:

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  Si se realiza correctamente la instalación de hello, hello AzureRM y AzureStack módulos se muestran en la salida de hello.

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a>Instalación de PowerShell en un escenario sin conexión o parcialmente conectado

En una situación sin conexión, debe descargar primero máquina tooa de módulos de PowerShell de Hola que tenga conectividad a internet y, a continuación, transferirlos toohello Kit de desarrollo de pila de Azure para la instalación.

1. Inicie sesión en el equipo de tooa donde tiene conectividad a internet y usar hello después hello de la secuencia de comandos toodownload AzureRM y AzureStack paquetes en el equipo local:

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. Hola copia los paquetes descargados en el dispositivo USB de tooa.

3. Inicie sesión en el kit de desarrollo de toohello y copiar paquetes de saludo de ubicación del tooa Hola para dispositivo USB en el kit de desarrollo de Hola. 

4. Ahora debe registrar esta ubicación como repositorio de hello predeterminado e instalar hello AzureRM y AzureStack módulos desde este repositorio:

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a>Pasos siguientes

* [Descarga de herramientas de Azure Stack desde GitHub](azure-stack-powershell-download.md)
* [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md)  
* [Configurar el entorno de PowerShell del operador de hello pila de Azure](azure-stack-powershell-configure-admin.md) 
* [Administración de perfiles de la versión de API en Azure Stack](azure-stack-version-profiles.md)  
