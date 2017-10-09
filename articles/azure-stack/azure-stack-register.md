---
title: aaaRegister pila de Azure | Documentos de Microsoft
description: "Registre Azure Stack con su suscripción de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a>Registro de Azure Stack con una suscripción de Azure

Para las implementaciones de Azure Active Directory, puede registrar pila de Azure con elementos de toodownload Azure marketplace de Azure y tooset los datos de comercio posterior comunicación tooMicrosoft. 

> [!NOTE]
>El registro se recomienda porque permite tootest importante funcionalidad de pila de Azure, como informes de uso y distribución de marketplace. Después de registrar la pila de Azure, uso es notificado tooAzure commerce. Puede verlo en la suscripción de hello usada para el registro. No se cobrará a los usuarios de Azure Stack Development Kit por ningún uso que comuniquen.
>


## <a name="get-azure-subscription"></a>Obtención de la suscripción a Azure

Antes de registrar Azure Stack con Azure, debe tener:

- Hola Id. de suscripción para una suscripción de Azure. Hola tooget ID, inicio de sesión tooAzure, haga clic en **más servicios** > **suscripciones**, haga clic en la suscripción de Hola que desea toouse y en **Essentials** puede Buscar hello **Id. de suscripción**. Las suscripciones en la nube en los gobiernos de China, Alemania y EE. UU. no se admiten actualmente.
- Hola, nombre de usuario y la contraseña de una cuenta que sea propietario de la suscripción de hello (se admiten cuentas MSA/2FA)
- Hello Azure Active Directory para hello suscripción de Azure. Puede encontrar este directorio en Azure manteniendo el mouse sobre su avatar en hello superior derecho de hello portal de Azure. 
- Proveedor de recursos de Azure pila Hola registrados (vea hello **registrar un proveedor de recursos de pila de Azure** sección para obtener más información)

Si no tiene una suscripción de Azure que cumpla estos requisitos, puede [crear una cuenta gratuita de Azure aquí](https://azure.microsoft.com/en-us/free/?b=17.06). El registro de Azure Stack no supone ningún costo en su suscripción de Azure.



## <a name="register-azure-stack-resource-provider-in-azure"></a>Registro del proveedor de recursos de Azure Stack en Azure
> [!NOTE] 
> Este paso solo debe toobe una vez completado en un entorno de pila de Azure.
>

1. Inicie PowerShell ISE como administrador.
2. Inicie sesión en toohello cuenta de Azure es un propietario de hello suscripción de Azure con el parámetro - EnvironmentName establecido demasiado "Nube de Azure".
3. Registrar el proveedor de recursos de Azure Hola "Microsoft.AzureStack".

Ejemplo: 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a>Registro de Azure Stack con Azure

> [!NOTE]
>Todos estos pasos deben realizarse en el equipo de host de Hola.
>

1. [Instale PowerShell para Azure Stack](azure-stack-powershell-install.md). 
2. Hola copia [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa carpeta (como C:\Temp).
3. Inicie PowerShell ISE como administrador.    
4. Ejecutar secuencia de comandos de RegisterWithAzure.ps1 de hello, reemplazando Hola siguiendo los marcadores de posición:
    - *YourAccountName* es propietario de Hola de hello suscripción de Azure
    - *YourID* es Hola Id. de suscripción de Azure que desea toouse tooregister pila de Azure
    - *YourDirectory* es Hola nombre de su inquilino de Azure Active Directory que forma parte de su suscripción de Azure.

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    Por ejemplo:
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. En dos peticiones de hello, presione ENTRAR.
6. En la ventana emergente de inicio de sesión de hello, escriba sus credenciales de suscripción de Azure.

## <a name="verify-hello-registration"></a>Comprobar el registro de hello

1. Inicie sesión en el portal de administración de toohello (https://adminportal.local.azurestack.external).
2. Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace)  > **Add from Azure** (Agregar desde Azure).
3. Si aparece una lista de elementos disponibles de Azure (como WordPress), la activación fue correcta.

## <a name="next-steps"></a>Pasos siguientes

[Conectar tooAzure pila](azure-stack-connect-azure-stack.md)

