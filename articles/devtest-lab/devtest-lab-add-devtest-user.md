---
title: aaaAdd los propietarios y los usuarios en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: Agregar propietarios y usuarios en los laboratorios de desarrollo y pruebas de Azure mediante el portal de Azure de Hola o PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Adición de propietarios y usuarios en Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

El acceso a Azure DevTest Labs se controla mediante el [control de acceso basado en rol (RBAC) de Azure](../active-directory/role-based-access-control-what-is.md). Usar RBAC, puede separar los derechos en el equipo en *roles* que se le concede únicamente cantidad de Hola de acceso necesarios toousers tooperform sus trabajos. Tres de estos roles RBAC son *Propietario*, *Usuario de DevTest Labs* y *Colaborador*. En este artículo, aprenderá qué acciones pueden realizarse en cada una de estas tres funciones principales RBAC Hola. Desde allí, aprenderá cómo práctica de tooadd usuarios tooa: tanto a través de Hola portal y a través de un script de PowerShell y cómo los usuarios de tooadd de Hola a nivel de suscripción.

## <a name="actions-that-can-be-performed-in-each-role"></a>Acciones que se pueden realizar en cada rol
Hay tres roles principales que puede asignar a un usuario:

* Propietario
* Usuario de DevTest Labs
* Colaborador

Hello tabla siguiente muestra las acciones de Hola que se pueden realizar los usuarios en cada uno de estos roles:

| **Acciones que pueden realizar los usuarios de este rol** | **Usuario de DevTest Labs** | **Propietario** | **Colaborador** |
| --- | --- | --- | --- |
| **Tareas de laboratorio** | | | |
| Agregar laboratorio tooa de usuarios |No |Sí |No |
| Actualizar la configuración de costo |No |Sí |Sí |
| **Tareas base de máquina virtual** | | | |
| Agregar y quitar imágenes personalizadas |No |Sí |Sí |
| Agregar, actualizar y eliminar las fórmulas |Sí |Sí |Sí |
| Incluir en la lista de permitidos imágenes de Azure Marketplace |No |Sí |Sí |
| **Tareas de la máquina virtual** | | | |
| Crear máquinas virtuales |Sí |Sí |Sí |
| Iniciar, detener y eliminar máquinas virtuales |Solo las máquinas virtuales creadas por el usuario de Hola |Sí |Sí |
| Actualizar directivas de máquinas virtuales |No |Sí |Sí |
| Agregar discos de datos o quitarlos en máquinas virtuales |Solo las máquinas virtuales creadas por el usuario de Hola |Sí |Sí |
| **Tareas de artefacto** | | | |
| Agregar y quitar repositorios de artefacto |No |Sí |Sí |
| Aplicar artefactos |Sí |Sí |Sí |

> [!NOTE]
> Cuando un usuario crea una máquina virtual, ese usuario se le asigna automáticamente toohello **propietario** rol de hello creado máquina virtual.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Agregar un usuario o propietario en nivel de laboratorio de Hola
Los propietarios y los usuarios pueden agregarse en nivel de laboratorio de Hola a través de hello portal de Azure. Esto incluye a los usuarios externos con una [cuenta Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.
Hola pasos guiarle por proceso Hola para agregar un laboratorio de tooa propietario o usuario en los laboratorios de desarrollo y pruebas de Azure:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.
4. En la hoja del laboratorio de hello, seleccione **configuración**. 
5. En hello **configuración** hoja, seleccione **usuarios**.
6. En hello **usuarios** hoja, seleccione **+ agregar**.
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. En hello **seleccione un rol** hoja, seleccione Hola un rol deseado. Hola sección [acciones que pueden realizarse en cada rol](#actions-that-can-be-performed-in-each-role) listas Hola varias acciones que se pueden realizar los usuarios en roles de propietario, el usuario de desarrollo y pruebas y el colaborador de Hola.
8. En hello **agregar usuarios** hoja, escriba la dirección de correo electrónico de Hola o nombre de usuario de hello desea tooadd en función de Hola que especificó. Si no se encuentra el usuario hello, un mensaje de error explica el problema de Hola. Si se encuentra el usuario hello, ese usuario se muestran y seleccionado. 
9. Elija **Seleccionar**.
10. Seleccione **Aceptar** tooclose hello **agregar acceso** hoja.
11. Cuando vuelva toohello **usuarios** hoja, se ha agregado el usuario Hola.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Agregar un laboratorio de tooa de usuario externo con PowerShell
Además los usuarios de tooadding Hola portal de Azure, puede agregar un laboratorio de tooyour de usuario externo mediante un script de PowerShell. Hola siguiente ejemplo, basta con modificar valores de parámetro de hello en hello **toochange valores** comentario.
Puede recuperar hello `subscriptionId`, `labResourceGroup`, y `labName` valores de hoja de laboratorio Hola Hola portal de Azure.

> [!NOTE]
> script de ejemplo de Hola se da por supuesto que Hola especifica el usuario se ha agregado como un toohello invitado Active Directory y se producirá un error si no es el caso de hello. tooadd un usuario no está en hello laboratorio tooa de Active Directory, utilice el rol de tooa de usuario de hello tooassign portal Azure Hola tal y como se muestra en la sección de hello, [agregar un usuario o propietario en nivel de laboratorio de hello](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Agregar un propietario o usuario en el nivel de suscripción de Hola
Permisos de Azure se propagan de ámbito de toochild ámbito principal en Azure. Por lo tanto, los propietarios de una suscripción de Azure que contiene laboratorios, automáticamente son propietarios de estos. También poseen hello las máquinas virtuales y otros recursos creados por los usuarios del laboratorio de Hola y Hola servicio laboratorios de desarrollo y pruebas de Azure. 

Puede agregar laboratorio de tooa más propietarios a través de la hoja del laboratorio de Hola Hola [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Sin embargo, Hola agrega ámbito del propietario de la administración es más estrecha que el ámbito del propietario de la suscripción de Hola. Por ejemplo, hello agrega propietarios no tiene acceso completo toosome de recursos de Hola que se crean en la suscripción de Hola Hola servicio laboratorios de desarrollo y pruebas. 

tooadd un tooan de propietario de la suscripción de Azure, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **suscripciones** de lista de Hola.
3. Seleccione la suscripción de hello deseado.
4. Seleccione el icono **Acceder** . 
   
    ![Usuarios de acceso](./media/devtest-lab-add-devtest-user/access-users.png)
5. En hello **usuarios** hoja, seleccione **agregar**.
   
    ![Agregar usuario](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. En hello **seleccione un rol** hoja, seleccione **propietario**.
7. En hello **agregar usuarios** hoja, escriba la dirección de correo electrónico de Hola o el nombre de usuario de hello desea tooadd como propietario. Si no se encuentra el usuario hello, obtendrá un mensaje de error que explica el problema de Hola. Si se encuentra el usuario hello, ese usuario aparece en hello **usuario** cuadro de texto.
8. Seleccione el nombre de usuario ubicada de Hola.
9. Elija **Seleccionar**.
10. Seleccione **Aceptar** tooclose hello **agregar acceso** hoja.
11. Cuando vuelva toohello **usuarios** hoja, usuario Hola se ha agregado como un propietario. Este usuario es ahora un propietario de los laboratorios creada con esta suscripción y, por tanto, ser capaz de tooperform tareas de propietario. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

