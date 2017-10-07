---
title: aaaAdd una nueva cuenta de inquilino de pila de Azure en Azure Active Directory | Documentos de Microsoft
description: "Después de implementar el Kit de desarrollo de pila de Microsoft Azure, necesitará toocreate al menos una cuenta de usuario de inquilinos para que puedan explorar el portal del inquilino de Hola."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a>Adición de una nueva cuenta de inquilino de Azure Stack en Azure Active Directory
Después de [implementar Hola Kit de desarrollo de Azure pila](azure-stack-run-powershell-script.md), necesitará una cuenta de usuario inquilino para que pueda explorar el portal del inquilino de Hola y sus ofertas y planes de pruebas. Puede crear una cuenta de inquilino por [utilizando Hola portal de Azure](#create-an-azure-stack-tenant-account-using-the-azure-portal) o [con PowerShell](#create-an-azure-stack-tenant-account-using-powershell).

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a>Crear una cuenta de inquilino de Azure pila utilizando Hola portal de Azure
Debe tener un hello toouse de suscripción de Azure portal de Azure.

1. Inicie sesión demasiado[Azure](http://manage.windowsazure.com).
2. En la barra de navegación izquierda de Microsoft Azure, haga clic en **Active Directory**.
3. En la lista de directorios de hello, haga clic en directorio de Hola que desee toouse para la pila de Azure, o cree uno nuevo.
4. En este directorio, haga clic en **Usuarios**.
5. Haga clic en **Agregar usuario**.
6. Hola **para agregar un usuario** asistente, hello **tipo de usuario** elija **nuevo usuario de su organización**.
7. Hola **nombre de usuario** , escriba un nombre de usuario de Hola.
8. Hola  **@**  cuadro, seleccione la entrada adecuada de Hola.
9. Haga clic en la flecha siguiente Hola.
10. Hola **perfil de usuario** página del Asistente de hello, escriba un **nombre**, **apellidos**, y **nombre para mostrar**.
11. Hola **rol** elija **usuario**.
12. Haga clic en la flecha siguiente Hola.
13. En hello **obtener contraseña temporal** página, haga clic en **crear**.
14. Hola copia **nueva contraseña**.
15. Inicie sesión en tooMicrosoft Azure con la nueva cuenta de hello. Cambiar la contraseña de hello cuando se le solicite.
16. Inicie sesión demasiado`https://portal.local.azurestack.external` con hello nueva toosee Hola inquilino portal de la cuenta.

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a>Creación de una cuenta de inquilino de Azure Stack con PowerShell
Si no tiene una suscripción de Azure, no se puede usar hello tooadd portal Azure una cuenta de usuario de inquilino. En este caso, puede usar hello Azure módulo Active Directory para Windows PowerShell en su lugar.

> [!NOTE]
> Si usas Microsoft Account (Live ID) toodeploy Kit de desarrollo de pila de Azure, no puede usar la cuenta de inquilino de AAD PowerShell toocreate. 
> 
> 

1. Instalar hello [Microsoft Online Services Sign-In Assistant para profesionales de TI RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).
2. Instalar hello [Azure módulo Active Directory para Windows PowerShell (versión de 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) y ábralo.
3. Ejecute hello siguientes cmdlets:

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. Inicie sesión en tooMicrosoft Azure con la nueva cuenta de hello. Cambiar la contraseña de hello cuando se le solicite.
2. Inicie sesión en demasiado`https://portal.local.azurestack.external` con hello nueva toosee Hola inquilino portal de la cuenta.

