---
title: aaaEnable multiempresa de pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosupport varios directorios de Azure Active Directory en la pila de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a>Habilitar los servicios multiinquilino en Azure Stack

Puede configurar usuarios de toosupport de pila de Azure de varios servicios de toouse de inquilinos de Azure Active Directory (Azure AD) en la pila de Azure. Por ejemplo, considere la posibilidad de hello siguiendo el escenario:

 - Son Hola Administrador de servicios de contoso.onmicrosoft.com, donde se instala la pila de Azure.
 - Mary es hello administrador del directorio de fabrikam.onmicrosoft.com, donde se encuentran los usuarios invitados. 
 - Compañía de Mary recibe servicios IaaS y PaaS de su empresa y necesita tooallow a los usuarios del directorio (fabrikam.onmicrosoft.com) toosign de invitado de hello en y usa recursos de la pila de Azure en contoso.onmicrosoft.com.

Esta guía proporciona pasos de hello necesarios, en el contexto de Hola de este escenario, tooconfigure multiempresa de pila de Azure.  En este escenario, se Mary debe completar los pasos que los usuarios tooenable de toosign de Fabrikam en y consumir servicios de implementación de pila de Azure en Contoso Hola.  

## <a name="before-you-begin"></a>Antes de empezar
Hay unos tooaccount de requisitos previos para antes de configurar la arquitectura multiempresa de pila de Azure:
  
 - Mary debe coordinar los procedimientos de administración a través de ambos directorios Hola pila de Azure se instala en (Contoso) y Hola directory invitado (Fabrikam).  
 - Asegúrese de que ha [instalado](azure-stack-powershell-install.md) y [configurado](azure-stack-powershell-configure-admin.md) PowerShell para Azure Stack.
 - [Descargar herramientas de pila de hello Azure](azure-stack-powershell-download.md)e importar módulos de conexión y la identidad de hello:

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - Mary requerirá [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) acceso tooAzure pila. 

## <a name="configure-azure-stack-directory"></a>Configurar el directorio de Azure Stack
En esta sección, configurará Azure pila tooallow inicios de sesión de inquilinos de directorio de Azure AD de Fabrikam.

### <a name="onboard-guest-directory-tenant"></a>Incorporar el inquilino del directorio de invitados
A continuación, incorporar Hola inquilino de directorio de invitado (Fabrikam) tooAzure pila.  Este paso configura Azure Resource Manager tooaccept usuarios y entidades de servicio de inquilino de directorio de hello invitado.

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a>Configurar el directorio de invitados
Después de completar los pasos en el directorio de la pila de Azure de hello, Mary debe especifique pila de tooAzure consentimiento al tener acceso al directorio de invitado hello y registrar pila de Azure con el directorio de invitado de Hola. 

### <a name="registering-azure-stack-with-hello-guest-directory"></a>El registro de pila de Azure con directorio de invitado de Hola
Una vez que el administrador del directorio de invitado de hello ha proporcionado consentimiento para el directorio de Azure pila tooaccess Fabrikam, deben registrarse pila de Azure con el inquilino de directorio de Fabrikam.

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a>Toosign de dirigir a los usuarios en
Ahora que usted y Mary termines de directorio de María hello pasos tooonboard, Mary puede dirigir toosign de los usuarios de Fabrikam en.  Los usuarios de Fabrikam (es decir, los usuarios con el sufijo de hello fabrikam.onmicrosoft.com) iniciar sesión en visitando https://portal.local.azurestack.external.  

Mary dirigirá cualquiera [las entidades de seguridad externas](../active-directory/active-directory-understanding-resource-access.md) en hello Fabrikam directorio (es decir, los usuarios de directorio de Fabrikam Hola sin sufijo Hola de fabrikam.onmicrosoft.com) toosign utilizando https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Si no utilizan esta dirección URL, que se envían el directorio predeterminado de tootheir (Fabrikam) y recibir un error que indique su administrador no ha dado su consentimiento.

## <a name="next-steps"></a>Pasos siguientes

- [Administrar proveedores delegados](azure-stack-delegated-provider.md)
- [Conceptos clave de Azure Stack](azure-stack-key-features.md)
