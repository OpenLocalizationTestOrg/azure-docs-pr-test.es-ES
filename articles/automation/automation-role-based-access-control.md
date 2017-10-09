---
title: "control de acceso basado en aaaRole en automatización de Azure | Documentos de Microsoft"
description: "El control de acceso basado en rol (RBAC) permite la administración del acceso en los recursos de Azure. Este artículo se describe cómo tooset la RBAC en automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "automatización de rbac, control de acceso basado en roles, rbac de azure"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Control de acceso basado en rol en Automatización de Azure
## <a name="role-based-access-control"></a>Control de acceso basado en rol
El control de acceso basado en rol (RBAC) permite la administración del acceso en los recursos de Azure. Usar [RBAC](../active-directory/role-based-access-control-configure.md), puede separar los derechos en el equipo y conceder únicamente Hola cantidad de acceso toousers, grupos y aplicaciones que necesitan tooperform sus trabajos. Se puede conceder acceso basado en roles toousers mediante Hola portal de Azure, Azure herramientas de línea de comandos o las API de administración de Azure.

## <a name="rbac-in-automation-accounts"></a>RBAC en cuentas de Automatización de Azure
En la automatización de Azure, se concede acceso mediante la asignación de hello adecuado RBAC rol toousers, grupos y aplicaciones en el ámbito de la cuenta de automatización de Hola. A continuación se Hola funciones integradas compatibles con una cuenta de automatización:  

| **Rol** | **Descripción** |
|:--- |:--- |
| Propietario |rol de propietario de Hello permite acceder a los recursos de tooall y las acciones dentro de una cuenta de automatización que proporcione acceso tooother usuarios, grupos y aplicaciones toomanage Hola cuenta de automatización. |
| Colaborador |rol de colaborador de Hello permite toomanage todo excepto modificar otro usuario tener acceso a la cuenta de automatización de tooan de permisos. |
| Lector |rol de lector de Hello permite tooview todos los recursos de hello en la automatización de una cuenta pero no pueden realizar ningún cambio. |
| Operador de automatización |función de operador de automatización de Hello permite tareas operativas tooperform, como iniciar, detener, suspender, reanudar y programar trabajos. Esta función es útil si desea que tooprotect los recursos de la cuenta de automatización como activos de credenciales y runbooks desde que se va a ver o modificar, pero seguirá permitiendo a los miembros de su organización tooexecute Estos runbooks. |
| Administrador de acceso de usuario |rol de administrador de acceso de usuario de Hello permite cuentas de automatización de tooAzure de acceso de usuario de toomanage. |

> [!NOTE]
> No se puede conceder acceso derechos tooa específico de runbook o runbooks, solo toohello recursos y las acciones dentro de hello cuenta de automatización.  
> 
> 

En este artículo se le guiará por el proceso de tooset seguridad RBAC en automatización de Azure. Pero primero, vamos a tomar una vista más cercana mirar Hola permisos individuales concedidos toohello colaborador, lector, el operador de automatización y el Administrador de acceso de usuario para que se obtenga un buen conocimiento antes de conceder a cualquier persona derechos toohello cuenta de automatización.  De lo contrario, se podrían producir consecuencias imprevistas o no deseadas.     

## <a name="contributor-role-permissions"></a>Permisos del rol Colaborador
Hello tabla siguiente presenta acciones específicas de Hola que pueden realizarse por rol de colaborador de hello en la automatización.

| **Tipo de recurso** | **Lectura** | **Escritura** | **Eliminar** | **Otras acciones** |
|:--- |:--- |:--- |:--- |:--- |
| Cuenta de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de certificado de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de conexión de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de tipo de conexión de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de credencial de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de programación de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Recurso de variable de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Configuración del estado deseado de Automatización | | | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Tipo de recurso de Hybrid Runbook Worker |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Trabajo de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Transmisión de trabajo de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Programación de trabajos de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Módulo de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Borrador de Runbook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Trabajo de prueba del borrador de Runbook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Webhook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Permisos del rol Lector
Hello tabla siguiente presenta acciones específicas de Hola que pueden realizarse por rol de lector de Hola de automatización.

| **Tipo de recurso** | **Lectura** | **Escritura** | **Eliminar** | **Otras acciones** |
|:--- |:--- |:--- |:--- |:--- |
| Administrador de suscripciones clásicas |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Bloqueo de administración |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Permiso |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Operaciones del proveedor |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asignación de roles |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Definición de roles |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Permisos del rol Operador de Automatización
Hello tabla siguiente presenta acciones específicas de Hola que pueden realizarse mediante la función de operador de automatización de hello en automatización.

| **Tipo de recurso** | **Lectura** | **Escritura** | **Eliminar** | **Otras acciones** |
|:--- |:--- |:--- |:--- |:--- |
| Cuenta de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de certificado de automatización | | | | |
| Recurso de conexión de automatización | | | | |
| Recurso de tipo de conexión de Automatización | | | | |
| Recurso de credencial de automatización | | | | |
| Recurso de programación de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Recurso de variable de automatización | | | | |
| Configuración del estado deseado de Automatización | | | | |
| Tipo de recurso de Hybrid Runbook Worker | | | | |
| Trabajo de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |
| Transmisión de trabajo de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Programación de trabajos de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Módulo de Automatización | | | | |
| Runbook de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Borrador de Runbook de Automatización | | | | |
| Trabajo de prueba del borrador de Runbook de Automatización | | | | |
| Webhook de Automatización | | | | |

Para obtener más información, Hola [acciones de operador de automatización](../active-directory/role-based-access-built-in-roles.md#automation-operator) listas Hola acciones admitidas por la función de operador de automatización de hello en la cuenta de automatización de Hola y sus recursos.

## <a name="user-access-administrator-role-permissions"></a>Permisos del rol Administrador de acceso de usuario
Hello tabla siguiente presenta acciones específicas de Hola que pueden realizarse por rol de administrador de acceso de usuario de hello en la automatización.

| **Tipo de recurso** | **Lectura** | **Escritura** | **Eliminar** | **Otras acciones** |
|:--- |:--- |:--- |:--- |:--- |
| Cuenta de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de certificado de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de conexión de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de tipo de conexión de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de credencial de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de programación de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Recurso de variable de automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Configuración del estado deseado de Automatización | | | | |
| Tipo de recurso de Hybrid Runbook Worker |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Trabajo de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Transmisión de trabajo de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Programación de trabajos de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Módulo de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook de Automatización de Azure |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Borrador de Runbook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Trabajo de prueba del borrador de Runbook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Webhook de Automatización |![Estado verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Configuración de RBAC para una Cuenta de Automatización mediante el Portal de Azure
1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) y abra su cuenta de automatización de la hoja de cuentas de automatización de Hola.  
2. Haga clic en hello **acceso** control en hello esquina superior derecha. Se abrirá hello **usuarios** hoja donde puede agregar los nuevos toomanage de usuarios, grupos y aplicaciones su cuenta de automatización y roles existentes de la vista que se pueden configurar para Hola cuenta de automatización.  
   
   ![Botón de acceso](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Los administradores de suscripciones** ya existe como usuario de hello predeterminado. grupo de active directory de administradores de Hello suscripción incluye administradores de servicio de Hola y co-administrator(s) para su suscripción de Azure. Hola, Administrador de servicio es propietario de Hola de su suscripción de Azure y sus recursos, y habrá rol de propietario de hello heredar para cuentas de automatización de hello demasiado. Esto significa que el acceso de hello es **Inherited** para **los administradores y coadministradores del servicio** de una suscripción y **asignado** de Hola a todos los otros usuarios. Haga clic en **los administradores de suscripciones** tooview más detalles sobre sus permisos.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Adición de usuarios nuevos y asignación de roles
1. En la hoja de usuarios de hello, haga clic en **agregar** tooopen hello **hoja de acceso agregar** donde puede agregar un usuario, grupo o aplicación y asignar un rol toothem.  
   
   ![Agregar usuario](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Seleccione un rol de la lista de Hola de roles disponibles. Elegiremos hello **lector** rol, pero puede elegir cualquiera de las funciones integradas disponibles Hola que admite una cuenta de automatización o cualquier rol personalizado que haya definido.  
   
   ![Seleccionar rol](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Haga clic en **agregar usuarios** tooopen hello **agregar usuarios** hoja. Si ha agregado ninguna toomanage usuarios, grupos o las aplicaciones se muestran su suscripción, a continuación, los usuarios y puede seleccionar tooadd acceso. Si no hay ningún usuario aparece, o si el usuario de Hola que le interese agregar no aparece, a continuación, haga clic en **invitar a** tooopen hello **invitar a un invitado** hoja, donde puede invitar a un usuario con una cuenta válida de Microsoft dirección de correo electrónico como Outlook.com, OneDrive, Xbox Live ID. Una vez que ha escrito la dirección de correo electrónico de saludo del usuario de hello, haga clic en **seleccione** tooadd Hola de usuario y, a continuación, haga clic en **Aceptar**. 
   
   ![Agregar usuarios](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Ahora debería ver usuario Hola agregado toohello **usuarios** hoja con hello **lector** rol asignado.  
   
   ![Enumerar usuarios](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   También puede asignar un usuario de toohello de rol de hello **Roles** hoja. 
4. Haga clic en **Roles** de Hola de hello usuarios hoja tooopen **hoja Roles**. En esta hoja, puede ver Hola nombre del rol de hello, número de Hola de usuarios y grupos asignados a función toothat.
   
    ![Asignar rol en la hoja de usuarios](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Control de acceso basado en roles solo se puede establecer en hello nivel de automatización de la cuenta y no en cualquier recurso siguiente Hola cuenta de automatización.
   > 
   > 
   
    Puede asignar más de un usuario de tooa de rol, grupo o aplicación. Por ejemplo, si se agrega hello **automatización operador** rol junto con hello **rol lector** toohello usuario, a continuación, se puede ver todos los recursos de automatización de hello, así como ejecutar trabajos de runbook de Hola. Puede expandir Hola desplegable tooview una lista de los usuarios de toohello roles asignados.  
   
    ![Ver varios roles](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Eliminación de un usuario
Puede quitar el permiso de acceso de Hola de un usuario que no administra Hola cuenta de automatización o que ya no funciona para la organización de Hola. A continuación se Hola pasos tooremove un usuario: 

1. De hello **usuarios** hoja, asignación de roles de hello select que desea tooremove.
2. Haga clic en hello **quitar** botón en la hoja de detalles de asignación de Hola.
3. Haga clic en **Sí** tooconfirm eliminación. 
   
   ![Quitar usuarios](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Usuario con rol asignado
Cuando se inicia un rol de usuario asignado tooa en tootheir cuenta de automatización, ahora puede ver cuenta del propietario de hello enumerado en la lista de Hola de **directorios predeterminado**. Hola de orden tooview cuenta de automatización que se hayan agregado a, deben cambiar directorio de predeterminado del propietario de hello predeterminado directorio toohello.  

![Directorio predeterminado](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Experiencia del usuario en el rol Operador de automatización
Cuando un usuario, que está asignado a vistas de rol de operador de automatización de toohello cuenta de automatización de hello a que están asignadas, pueden solo ver lista de Hola de runbooks, programaciones y trabajos de runbook crean Hola cuenta de automatización, pero no pueden ver su definición. Puede iniciar, detener, suspender, reanudar o programar el trabajo del runbook Hola. usuario de Hello no tendrán acceso a los recursos de automatización de tooother como configuraciones, grupos de trabajo híbrido o nodos de DSC.  

![No hay tooresourcres de acceso](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Cuando hace clic en usuario de hello en runbook hello, hello comandos tooview Hola origen o editar runbook hello no se proporcionan como función de operador de automatización de hello no permite acceso toothem.  

![Ningún runbook tooedit de acceso](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

Hola usuario tendrá acceso tooview y toocreate programaciones pero no tendrá acceso tooany otro tipo de recurso.  

![No hay tooassets de acceso](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Este usuario no tiene también acceso tooview hello webhooks asociadas a un runbook

![No hay toowebhooks de acceso](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Configuración de RBAC para una Cuenta de Automatización mediante Azure PowerShell
Acceso basado en rol también puede ser configurado tooan cuenta de automatización con hello siguientes [cmdlets de PowerShell de Azure](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) enumera todos los roles RBAC disponibles en Azure Active Directory. Puede utilizar este comando junto con hello **nombre** toolist propiedad todos Hola acciones que pueden realizarse mediante un rol específico.  
    **Ejemplo:**  
    ![Obtener definición de rol](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [AzureRmRoleAssignment get](https://msdn.microsoft.com/library/mt619413.aspx) enumera las asignaciones de roles de Azure AD RBAC en hello especifica el ámbito. Sin parámetros, este comando devuelve todas las asignaciones de roles de hello realizadas en la suscripción de Hola. Hola de uso **ExpandPrincipalGroups** asignaciones de acceso de parámetro toolist para hello especificado usuario así como los grupos de Hola Hola usuario es miembro de.  
    **Ejemplo:** siguiente Hola de uso del comando toolist todos los usuarios de Hola y sus funciones dentro de una cuenta de automatización.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Obtener asignación de rol](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, grupos y aplicaciones tooa determinado ámbito de acceso.  
    **Ejemplo:** siguiente Hola de uso del comando tooassign rol de "Operador de automatización" hello para un usuario en el ámbito de la cuenta de automatización de Hola.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nueva asignación de rol](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Uso [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove acceso de un usuario especificado, el grupo o la aplicación a partir de un ámbito determinado.  
    **Ejemplo:** siguiente Hola de uso de comandos usuario de hello tooremove de función de "Operador de automatización" Hola Hola ámbito de la cuenta de automatización.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

Hola por encima de los ejemplos, reemplace **iniciar sesión en el Id. de**, **Id. de suscripción**, **nombre del grupo de recursos** y **nombre de la cuenta de automatización** con su detalles de la cuenta. Elija **Sí** cuando se le pida tooconfirm antes de continuar tooremove asignación de roles de usuario.   

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información sobre maneras tooconfigure RBAC de automatización de Azure, consulte demasiado[administrar RBAC con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Para obtener detalles sobre las distintas formas toostart un runbook, consulte [a partir de un runbook](automation-starting-a-runbook.md)
* Para obtener información acerca de los tipos de runbook diferente, consulte demasiado[tipos de runbook de automatización de Azure](automation-runbook-types.md)

