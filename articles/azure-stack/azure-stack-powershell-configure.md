---
title: aaaConfigure PowerShell para su uso con la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure PowerShell para la pila de Azure."
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
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a>Configurar PowerShell para su uso con la pila de Azure 

Este artículo describe instancia de hello pasos necesarios tooconnect tooan Kit de desarrollo de pila de Azure mediante PowerShell. Después de conectarse, puede tener acceso a portal de hello e implementar recursos a través de PowerShell. Puede usar los pasos de hello descritos en este artículo del kit de desarrollo de hello, o desde un cliente externo basado en Windows, si está conectado a través de VPN.

En este artículo, se detallaron instrucciones tooconfigure PowerShell para la pila de Azure. Sin embargo, si lo desea tooquickly instalación y configuración de PowerShell, puede usar script de Hola proporcionado en hello [ponerse a trabajar con PowerShell](azure-stack-powershell-configure-quickstart.md) tema. 

## <a name="prerequisites"></a>Requisitos previos
* Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  
* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).  

## <a name="import-hello-connect-powershell-module"></a>Módulo de importación Hola Connect PowerShell

Después de descargar Hola requiere herramientas, desplazarse por las carpetas de toohello descargar e importar hello **conectar** módulo de PowerShell. módulo tooimport Hola Connect, ejecute el siguiente comando en una sesión de PowerShell con privilegios elevados de hello:

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a>Configurar el entorno de PowerShell de Hola

tooconfigure el entorno de la pila de Azure, Hola siguientes:

1. Registrar un entorno de AzureRM destinado a la instancia de la pila de Azure mediante uno de los siguientes cmdlets de hello:

   * **Entorno administrativo en la nube**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * **Entorno de usuario**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   Después de que ha registrado el entorno de AzureRM hello, puede usar todos los cmdlets de AzureRM hello en su entorno de pila de Azure. se muestra el resultado de Hello del cmdlet anterior Hola Hola siguiente captura de pantalla:

   ![Obtener detalles del entorno](media/azure-stack-powershell-configure/getenvdetails.png)

2. Establezca el valor de GraphEndpointResourceId de hello mediante uno de los siguientes cmdlets de hello:
   
   * **Azure Active Directory (Azure AD)**
   
      * Para hello **entorno administrativo en la nube**, use:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * Para hello **entorno del usuario**, use:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * **Servicios de federación de Active Directory**
   
      * Para hello **entorno administrativo en la nube**, use:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * Para hello **entorno del usuario**, use:
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. Obtener valor GUID de Hola Hola inquilino de Active Directory que es usado toodeploy pila de Azure. Si su entorno de pila de Azure se implementa mediante el uso de:  

   * **Azure Active Directory (Azure AD)**
   
      * Hola tooaccess **entorno administrativo en la nube**, use:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * Hola tooaccess **entorno del usuario**, use:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * **Servicios de federación de Active Directory**
   
      * Hola tooaccess **entorno administrativo en la nube**, use:
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * Hola tooaccess **entorno del usuario**, use:
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a>Inicie sesión en tooAzure pila

Inicie sesión en toohello entorno de pila de Azure mediante uno de hello después de dos cmdlets:

   * toosign en toohello **portal administrativa**, use:
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * toosign en toohello **portal de usuarios**, use:

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a>Registro de proveedores de recursos

Después de iniciar sesión en el portal de administrador o usuario toohello, puede emitir las operaciones en proveedores de recursos de hello registrado. De forma predeterminada, se registran todos los proveedores de recursos fundamentales de hello en Hola suscripción predeterminada de proveedor (suscripción del Administrador de la nube de Hola).

Cuando trabaje en una suscripción de usuario recién creado, que no tiene los recursos que se implementan a través del portal de hello, proveedores de recursos de hello no se registran automáticamente. Explícitamente, debe registrar proveedores de recursos de Hola mediante Hola siguiente secuencia de comandos:

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a>Pasos siguientes
* [Desarrollo de plantillas para Azure Stack](azure-stack-develop-templates.md)
* [Implementación de plantillas con PowerShell](azure-stack-deploy-template-powershell.md)
