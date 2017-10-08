---
title: aaaCreate una entidad de servicio para la pila de Azure | Documentos de Microsoft
description: "Describe cómo toocreate una nueva entidad de servicio que puede usarse con control de acceso basado en roles de hello en Azure Resource Manager toomanage acceso tooresources."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a>Proporcionar acceso de las aplicaciones tooAzure pila
Cuando una aplicación necesita acceso toodeploy o configurar los recursos a través del Administrador de recursos de Azure en la pila de Azure, se crea un servicio principal, que es una credencial para la aplicación.  A continuación, puede delegar la entidad de servicio Hola permisos necesarios toothat solo.  

Por ejemplo, puede tener una herramienta de administración de configuración que utiliza Azure tooinventory de administrador de recursos de recursos de Azure.  En este escenario, puede crear a una entidad de servicio, conceder a lector Hola entidad de servicio de rol toothat y limitar Hola configuración herramienta solo tooread acceso a la administración. 

Entidades de servicio son preferibles toorunning Hola aplicación bajo sus propias credenciales porque:

* Puede asignar la entidad de servicio de toohello de permisos que son diferentes de sus propios permisos de cuenta. Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.
* No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades.
* Puede usar una autenticación de certificado tooautomate al ejecutar un script de instalación desatendida.  

## <a name="getting-started"></a>Introducción

Dependiendo de cómo ha implementado Azure Stack, primero debe crear una entidad de servicio.  Este documento le guía a través del proceso de creación de una entidad de servicio para [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) y [Servicios de federación de Active Directory (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).  Una vez que haya creado Hola entidad de servicio, un conjunto de pasos comunes tooboth AD FS y Azure Active Directory se usan demasiado[delegar permisos](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello rol.     

## <a name="create-service-principal-for-azure-ad"></a>Crear una entidad de servicio para Azure AD

Si ha implementado la pila de Azure con Azure AD como almacén de identidades de hello, puede crear a entidades de servicio igual que hacen de Azure.  Esta sección muestra cómo los pasos a través del portal de hello tooperform Hola.  Compruebe que dispone de hello [requiere permisos de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) antes de comenzar.

### <a name="create-service-principal"></a>Creación de una entidad de servicio
En esta sección, creará una aplicación (entidad de servicio) en Azure AD que representará su aplicación.

1. Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).
2. Seleccione **Azure Active Directory** > **Registros de aplicaciones** > **Agregar**.   
3. Proporcione un nombre y la dirección URL para la aplicación hello. Seleccione **aplicación Web / API** o **nativo** para el tipo de saludo de aplicación desea toocreate. Después de establecer valores de hello, seleccione **crear**.

Creó una entidad de servicio para la aplicación.

### <a name="get-credentials"></a>Obtener credenciales
Al iniciar sesión mediante programación, use el identificador de hello para la aplicación y una clave de autenticación. tooget los valores, Hola uso pasos:

1. En **App registrations** (Registros de aplicaciones), en Active Directory, seleccione su aplicación.

2. Hola copia **Id. de aplicación** y almacenarlo en el código de aplicación. Hola aplicaciones Hola [aplicaciones de ejemplo](#sample-applications) sección hacen referencia a valor toothis como identificador de cliente de Hola.

     ![ID. DE CLIENTE](./media/azure-stack-create-service-principal/image12.png)
3. toogenerate una clave de autenticación, seleccione **claves**.

4. Proporcione una descripción de clave de hello y una duración para la clave de Hola. Cuando haya terminado, seleccione **Guardar**.

Después de guardar la clave de hello, se muestra el valor de Hola de clave de Hola. Copie este valor porque no es capaz de tooretrieve clave de hello más tarde. Proporcionar valor de clave de hello con toosign de Id. de aplicación Hola como aplicación hello. Almacene el valor de clave de Hola donde la aplicación pueda recuperarlos.

![clave guardada](./media/azure-stack-create-service-principal/image15.png)


Una vez completado, continuar demasiado[asignar un rol de la aplicación](azure-stack-create-service-principals.md#assign-role-to-service-principal).

## <a name="create-service-principal-for-ad-fs"></a>Crear una entidad de servicio para AD FS
Si ha implementado la pila de Azure con AD FS, puede usar PowerShell toocreate una entidad de servicio, asignar un rol para el acceso e inicio de sesión desde PowerShell utilizando dicha identidad.

### <a name="before-you-begin"></a>Antes de empezar

[Descargar Hola herramientas requiere toowork con el equipo local tooyour de pila de Azure.](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a>Módulo de PowerShell de identidad de Hola de importación
Después de descargar herramientas de hello, desplazarse por las carpetas de toohello descargado e importe el módulo de PowerShell de identidad de hello utilizando Hola siguiente comando:

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

Al importar el módulo de hello, recibirá un error que dice "AzureStack.Connect.psm1 no está firmado digitalmente. script de Hola no se ejecutará en el sistema de Hola". tooresolve este problema, puede establecer tooallow de directiva de ejecución ejecutar script de Hola con hello siguiente comando en una sesión de PowerShell con privilegios elevados:

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a>Crear Hola entidad de servicio
Puede crear una entidad de servicio mediante la ejecución Hola siguiente comando, que realiza seguro hello tooupdate *DisplayName* parámetro:
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a>Asignar un rol
Una vez Hola se crea la entidad de servicio, debe [asignar rol tooa](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>Iniciar sesión a través de PowerShell
Una vez que haya asignado un rol, puede iniciar sesión en tooAzure pila con entidad de servicio de Hola Hola siguiente comando:

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a>Asignar la entidad de seguridad de rol tooservice
tooaccess recursos de la suscripción, debe asignar el rol de tooa de aplicación Hola. Decidir qué rol representa permisos adecuados de hello para la aplicación hello. toolearn sobre los roles disponibles de hello, consulte [RBAC: integrada en Roles](../active-directory/role-based-access-built-in-roles.md).

Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso. Los permisos son heredados toolower niveles de ámbito. Por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos indica que puede leer el grupo de recursos de Hola y los recursos que contenga.

1. En el portal de Azure pila hello, navegue toohello nivel de ámbito que se va tooassign aplicación Hola. Por ejemplo, tooassign un rol en el ámbito de la suscripción de hello, seleccione **suscripciones**. También puede seleccionar un grupo de recursos o un recurso.

2. Seleccionar Hola suscripción en particular (grupo de recursos o recursos) tooassign Hola aplicación.

     ![seleccionar suscripción para la asignación](./media/azure-stack-create-service-principal/image16.png)

3. Seleccione **Access Control (IAM)**.

     ![seleccionar acceso](./media/azure-stack-create-service-principal/image17.png)

4. Seleccione **Agregar**.

5. Seleccione rol Hola desea tooassign toohello aplicación.

6. Busque la aplicación y selecciónela.

7. Seleccione **Aceptar** toofinish asignación de rol de Hola. Verá que su aplicación en la lista de Hola de los usuarios asignados a roles tooa para ese ámbito.

Ahora que ha creado a una entidad de servicio y le asigna un rol, puede empezar a usar esto en los recursos de Azure pila tooaccess de aplicación.  

## <a name="next-steps"></a>Pasos siguientes

[Add users for ADFS](azure-stack-add-users-adfs.md) (Agregar usuarios para ADFS)
[Manage user permissions](azure-stack-manage-permissions.md) (Administrar permisos de usuario)