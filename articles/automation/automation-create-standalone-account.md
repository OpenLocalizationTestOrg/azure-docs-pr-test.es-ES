---
title: "aaaCreate independiente cuenta de automatización de Azure | Documentos de Microsoft"
description: "Tutorial le guía a través del uso de creación, las pruebas y ejemplo de Hola principal de autenticación de seguridad en la automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Creación de una cuenta independiente de Azure Automation
Este tema muestra cómo toocreate una cuenta de automatización de hello portal de Azure si desea tooevaluate y obtenga información acerca de automatización de Azure sin incluir las soluciones de administración adicional de Hola o integración con análisis de registros de OMS tooprovide supervisión avanzadas de trabajos de runbook.  Puede agregar estas soluciones de administración o integrar con análisis de registros en cualquier momento Hola futuras.  Con Hola cuenta de automatización son runbooks tooauthenticate capaz de administrar los recursos en el Administrador de recursos de Azure o implementación clásico de Azure.

Cuando se crea una cuenta de automatización en hello portal de Azure, se crean automáticamente:

* Cuenta de ejecución, que crea una nueva entidad de servicio en Azure Active Directory, un certificado, y asigna Hola control de acceso basado en roles de colaborador (RBAC), que es recursos del Administrador de recursos de toomanage uso de runbooks que se utilizan.   
* Clásico cuenta de ejecución mediante la carga de un certificado de administración, que se usan los recursos clásicos toomanage uso de runbooks.  

Esto simplifica el proceso de Hola para usted y le ayuda a comenzar rápidamente a construir e implementar runbooks toosupport necesita de la automatización.  

## <a name="permissions-required-toocreate-automation-account"></a>Permisos necesario toocreate cuenta de automatización
toocreate o una cuenta de automatización de la actualización, debe tener Hola después determinados privilegios y permisos necesarios toocomplete en este tema.   
 
* En orden toocreate una cuenta de automatización, su cuenta de usuario de AD necesita toobe tooa agregado rol con el rol de propietario de toohello equivalente de permisos para los recursos de Microsoft.Automation tal como se describe en el artículo [control de acceso basado en roles en automatización de Azure ](automation-role-based-access-control.md).  
* Si los registros de aplicación Hola configuración se establece demasiado**Sí**, los usuarios sin derechos administrativos en el inquilino de Azure AD pueden [registrar aplicaciones AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Si los registros de aplicación Hola configuración se establece demasiado**n**, usuario Hola realizar esta acción debe ser un administrador global de Azure AD. 

Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello global administrador o coadministrator-administrator roles de suscripción de hello, se agregan tooActive directorio como invitado. En este caso, recibirá un "no tiene permisos toocreate..." Advertencia de hello **agregar una cuenta de automatización** hoja. Los usuarios que se agregaron toohello administrador o coadministrator-administrator función global en primer lugar se puede quitar de la instancia de Active Directory de la suscripción de Hola y añadir toomake a un usuario en Active Directory completo. tooverify esta situación, hello **Azure Active Directory** panel Hola portal de Azure, seleccione **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar Hola un usuario específico, seleccione **perfil**. Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Crear una nueva cuenta de automatización de hello portal de Azure
En esta sección, realizar Hola siguiendo los pasos toocreate una cuenta de automatización de Azure en hello portal de Azure.    

1. Inicie sesión en toohello portal de Azure con una cuenta que sea miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.
2. Haga clic en **Nuevo**.<br><br> ![Seleccione la opción Nuevo en Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Busque **automatización** y, a continuación, en hello resultados de la búsqueda seleccione **Control y automatización***.<br><br> ![Busque y seleccione Automation en Marketplace](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. En la hoja de cuentas de automatización de hello, haga clic en **agregar**.<br><br>![Agregar cuenta de Automatización](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Si ve Hola después de advertencia en hello **agregar una cuenta de automatización** hoja, es porque la cuenta no es miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.<br><br>![Advertencia para agregar cuenta de Automatización](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. Hola **agregar una cuenta de automatización** hoja en hello **nombre** cuadro, escriba un nombre para la nueva cuenta de automatización.
5. Si tiene más de una suscripción, uno para la nueva cuenta de hello, especifique un nuevo o existente **grupo de recursos** y un centro de datos Azure **ubicación**.
6. Comprobar el valor de hello **Sí** está seleccionada para hello **crear Azure cuenta de ejecución** opción y haga clic en hello **crear** botón.  
   
   > [!NOTE]
   > Si elige toonot crear cuenta de identificación de hello seleccionando la opción de hello **No**, se le presentará un mensaje de advertencia en hello **agregar una cuenta de automatización** hoja.  Mientras se crea la cuenta de hello en hello portal de Azure, no tiene una identidad de autenticación correspondiente en el clásico o servicio de directorio de suscripción de administrador de recursos y por lo tanto, no tooresources de acceso en su suscripción.  Esto evita que los runbooks que hacen referencia a esta cuenta se pueda tooauthenticate y realizar tareas con los recursos en los modelos de implementación.
   > 
   > ![Advertencia para agregar cuenta de Automatización](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Cuando no se crea la entidad de servicio de hello no está asignado el rol de colaborador de Hola.
   > 

7. Mientras Azure crea la cuenta de automatización de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

### <a name="resources-included"></a>Recursos incluidos
Cuando se crea correctamente la cuenta de automatización de hello, varios recursos se crean automáticamente para usted.  Hello en la tabla siguiente resume los recursos para hello cuenta de ejecución.<br>

| Recurso | Descripción |
| --- | --- |
| Runbook AzureAutomationTutorial |Un runbook gráfico de ejemplo que muestra cómo usar tooauthenticate Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola. |
| Runbook AzureAutomationTutorialScript |Un runbook de PowerShell de ejemplo que muestra cómo usar tooauthenticate Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola. |
| AzureRunAsCertificate |Activo de certificado automáticamente creado durante la creación de cuentas de automatización o con el siguiente script de PowerShell de Hola de una cuenta existente.  Permite tooauthenticate con Azure para que pueda administrar recursos de Azure Resource Manager desde los runbooks.  Este certificado tiene una duración de un año. |
| AzureRunAsConnection |Activo de conexión automática creado durante la creación de cuentas de automatización o con el siguiente script de PowerShell de Hola de una cuenta existente. |

Hello en la tabla siguiente resume los recursos para hello clásico cuenta de ejecución.<br>

| Recurso | Descripción |
| --- | --- |
| Runbook AzureClassicAutomationTutorial |Gráfica runbook de ejemplo, que obtiene todas las máquinas virtuales de clásico de hello en una suscripción utilizando Hola clásico como cuenta de ejecución (certificado) y a continuación, muestra el nombre de la máquina virtual de Hola y el estado. |
| Runbook AzureClassicAutomationTutorial Script |Un runbook de PowerShell de ejemplo, que obtiene todas las máquinas virtuales de clásico de hello en una suscripción utilizando Hola clásico como cuenta de ejecución (certificado) y a continuación, muestra el nombre de la máquina virtual de Hola y el estado. |
| AzureClassicRunAsCertificate |Activo de certificado creado automáticamente que utiliza tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks.  Este certificado tiene una duración de un año. |
| AzureClassicRunAsConnection |Activo de conexión creado automáticamente que utiliza tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks. |


## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la creación de gráficos, consulte [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).
* tooget a trabajar con runbooks de PowerShell, consulte [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md).
