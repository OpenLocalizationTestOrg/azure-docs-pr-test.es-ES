---
title: aaaCreate cuenta de usuario de AD de Azure | Documentos de Microsoft
description: "Este artículo describe cómo toocreate una cuenta de usuario de AD de Azure de credencial de runbooks en automatización de Azure tooauthenticate en Azure y Azure clásico."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "usuario de azure active directory, administración de servicios de azure, cuenta de usuario de azure ad"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Autenticación de runbooks con la implementación clásica de Azure y Resource Manager
Este artículo describen los pasos de Hola que debe seguir tooconfigure una cuenta de usuario de AD de Azure para runbooks de automatización de Azure que se ejecutan en el modelo de implementación clásica Azure o recursos de Azure Resource Manager.  Aunque este proceso continúa toobe una identidad de autenticación admitidos para el Administrador de recursos de Azure en función de runbooks, Hola recomienda método es utilizar una cuenta de identificación de Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Creación de un usuario de Azure Active Directory nuevo
1. Inicie sesión en el portal de Azure clásico de toohello como administrador del servicio de suscripción de Azure que desee toomanage Hola.
2. Seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de su organización.
3. Seleccione hello **usuarios** ficha y, a continuación, en el área de comandos de hello, seleccione **Agregar usuario**.
4. En hello **envíenos comentarios acerca de este usuario** página, en **tipo de usuario**, seleccione **nuevo usuario de su organización**.
5. Escriba un nombre de usuario.  
6. Seleccione el nombre de directorio de Hola que está asociado a su suscripción de Azure en la página de Active Directory Hola.
7. En hello **perfil de usuario** , proporcione un primer y último nombre, un nombre descriptivo y usuario de hello **Roles** lista.  No seleccione **Habilitar Multi-Factor Authentication**.
8. Observe el nombre completo del usuario de Hola y la contraseña temporal.
9. Seleccione **Configuración > Administradores > Agregar**.
10. Escriba el nombre de usuario completa de Hola Hola del usuario de que ha creado.
11. Seleccione la suscripción de Hola que desee Hola toomanage de usuario.
12. Cerrar sesión en Azure y, a continuación, iniciar sesión con cuentas de Hola que acaba de crear. Es posible que la contraseña del usuario de hello toochange solicitadas.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Creación de una cuenta de Automation en el Portal de Azure clásico
En esta sección, realizar Hola siguientes pasos toocreate una cuenta de automatización de Azure en hello portal de Azure para su uso con sus runbooks administrar recursos de implementación clásico de Azure.  

> [!NOTE]
> Las cuentas de automatización creadas con el portal de Azure clásico de hello pueden administrarse mediante Hola clásico de Azure y portal de Azure y una conjunto de cmdlets. Una vez creada la cuenta de hello, no produce ninguna diferencia cómo crear y administrar los recursos dentro de la cuenta de hello. Si tiene previsto portal de Azure clásico de toocontinue toouse hello, a continuación, sólo debería utilizarlo en lugar de Hola toocreate portal Azure ninguna cuenta de automatización.
> 
> 

1. Inicie sesión en el portal de Azure clásico de toohello como administrador del servicio de suscripción de Azure que desee toomanage Hola.
2. Seleccione **Automation**.
3. En hello **automatización** página, seleccione **crear una cuenta de automatización**.
4. Hola **crear una cuenta de automatización** cuadro, escriba un nombre para la nueva cuenta de automatización y seleccione un **región** desde la lista desplegable de Hola.  
5. Haga clic en **Aceptar** tooaccept la configuración y crear cuenta de hello.
6. Después de crearlo se enumerarán en hello **automatización** página.
7. Haga clic en la cuenta de hello y aparecerá la página panel toohello.  
8. En la página de panel de automatización de hello, seleccione **activos**.
9. En hello **activos** página, seleccione **Agregar configuración** situado en la parte inferior de Hola de página de Hola.
10. En hello **Agregar configuración** página, seleccione **Add Credential**.
11. En hello **definir credenciales** página, seleccione **credenciales de Windows PowerShell** de hello **tipo de credencial** lista desplegable lista y proporcione un nombre de credencial de Hola.
12. En los siguientes hello **definir credenciales** página escriba en nombre de usuario de Hola de cuenta de usuario de hello AD que creó anteriormente en hello **nombre de usuario** hello y el campo contraseña en hello **contraseña**y **Confirmar contraseña** campos. Haga clic en **Aceptar** toosave los cambios.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Crear una cuenta de automatización en hello portal de Azure
En esta sección, realizar Hola siguientes pasos toocreate una cuenta de automatización de Azure en hello portal de Azure para su uso con sus runbooks administrar recursos en el modo Azure Resource Manager.  

1. Inicie sesión en toohello portal de Azure como administrador del servicio de suscripción de Azure que desee toomanage Hola.
2. Seleccione **Cuentas de Automation**.
3. En la hoja de cuentas de automatización de hello, haga clic en **agregar**.<br><br>![Agregar cuenta de Automatización](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. Hola **agregar una cuenta de automatización** hoja en hello **nombre** cuadro, escriba un nombre para la nueva cuenta de automatización.
5. Si tiene más de una suscripción, especificar hello para la nueva cuenta de hello, así como un nuevo o existente **grupo de recursos** y un centro de datos Azure **ubicación**.
6. Seleccione el valor de hello **Sí** para hello **crear Azure cuenta de ejecución** opción y haga clic en hello **crear** botón.  
   
    > [!NOTE]
    > Si elige toonot crear cuenta de identificación de hello seleccionando la opción de hello **No**, aparecerá un mensaje de advertencia en hello **agregar una cuenta de automatización** hoja.  Mientras se crea y se asigna toohello cuenta de hello **colaborador** rol en la suscripción de hello, no tendrá una identidad de autenticación correspondiente en el servicio de directorio de suscripciones y por lo tanto, no tiene acceso recursos de la suscripción.  Esto se impide los runbooks que hacen referencia a esta cuenta se pueda tooauthenticate y realizar tareas con los recursos de Azure Resource Manager.
    > 
    >

    <br>![Advertencia para agregar cuenta de Automation](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Mientras Azure crea la cuenta de automatización de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

Cuando se complete la creación de hello de credencial de hello, deberá toocreate Hola de tooassociate de activo de credencial cuenta de automatización con hello cuenta de usuario de AD se creó anteriormente.  Recuerde que hemos creado sólo cuenta de automatización de Hola y no está asociado con una identidad de autenticación.  Lleve a cabo los pasos de hello descritos en hello [credencial activos en el artículo de automatización de Azure](automation-credentials.md#creating-a-new-credential-asset) y escriba el valor de Hola para **nombre de usuario** en formato de hello **dominio ombre de usuario**.

## <a name="use-hello-credential-in-a-runbook"></a>Usar credenciales de hello en un runbook
Puede recuperar la credencial de hello en un runbook con hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) actividad y, a continuación, utilizarlo con [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour suscripción de Azure. Si Hola credencial es un administrador de varias suscripciones de Azure, también debe usar [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify Hola correcto. Esto se muestra en el ejemplo hello Windows PowerShell siguiente que normalmente aparece en la parte superior de saludo de la mayoría de los runbooks de automatización de Azure.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Deberá repetir estas líneas después de cada [punto de control](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) de su runbook. Si Hola runbook se suspende y, a continuación, se reanuda en otro trabajador, será necesario tooperform nuevamente la autenticación de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Revisión Hola runbook diferentes tipos y los pasos para crear sus propios runbooks de Hola artículo siguiente [tipos de runbook de automatización de Azure](automation-runbook-types.md)

