---
title: "aaaCreate identidad de aplicación de portal de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate una nueva aplicación de Azure Active Directory y el servicio principal que se puede utilizar con control de acceso basado en roles de hello en Azure Resource Manager toomanage obtener acceso a tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Usar portal toocreate una aplicación de Azure Active Directory y la entidad de servicio que puede tener acceso a recursos

Cuando haya una aplicación que necesita tooaccess o modificar recursos, debe configurar una aplicación de Azure Active Directory (AD) y asignar Hola requerido permisos tooit. Este enfoque es preferible toorunning Hola aplicación bajo sus propias credenciales porque:

* Puede asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos. Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.
* No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades. 
* Puede usar una autenticación de certificado tooautomate al ejecutar un script de instalación desatendida.

Este tema muestra cómo tooperform los pasos a través de portal de Hola. Se centra en una aplicación de inquilino único donde la aplicación hello es toorun previsto dentro de un único de organización. Normalmente, utiliza aplicaciones de inquilino único para aplicaciones de línea de negocio que se ejecutan dentro de su organización.
 
## <a name="required-permissions"></a>Permisos necesarios
toocomplete en este tema, debe tener tooregister de permisos suficientes en una aplicación con el inquilino de Azure AD y asignar el rol de tooa de aplicación hello en su suscripción de Azure. Asegurémonos de que tienes Hola permisos adecuados tooperform esos pasos.

### <a name="check-azure-active-directory-permissions"></a>Comprobación de los permisos de Azure Active Directory
1. Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).
2. Seleccione **Azure Active Directory**.

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. En su instancia de Azure Active Directory, seleccione **Configuración de usuario**.

     ![seleccionar configuración de usuario](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Comprobar hello **registros de aplicación** configuración. Si establece demasiado**Sí**, usuarios no administrativos pueden registrar aplicaciones de AD. Este valor significa que cualquier usuario de inquilino de Azure AD Hola puede registrar una aplicación. Puede continuar demasiado[permisos de suscripción de Azure compruebe](#check-azure-subscription-permissions).

     ![ver registros de aplicaciones](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Si los registros de aplicación Hola configuración se establece demasiado**n**, solo los usuarios administradores pueden registrar las aplicaciones. Debe toocheck si su cuenta es un administrador de inquilinos de Azure AD Hola. Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
6. Busque la cuenta y selecciónela cuando la encuentre.

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png)
7. Para la cuenta, seleccione **Directory role** (Rol de directorio). 

     ![rol de directorio](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Vea el rol de directorio asignado en Azure AD. Si su cuenta se asigna el rol de usuario de toohello pero hello configuración de registro de aplicación (a través de Hola pasos anteriores) es tooadmin limitado a los usuarios, pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.

     ![rol de vista](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Comprobación de los permisos de suscripción de Azure
En su suscripción de Azure, su cuenta debe tener `Microsoft.Authorization/*/Write` acceso tooassign un rol de tooa de aplicación de AD. Esta acción se concede a través de hello [propietario](../active-directory/role-based-access-built-in-roles.md#owner) rol o [Administrador de acceso de usuario](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol. Si su cuenta se asigna toohello **colaborador** rol, no tiene los permisos adecuados. Recibirá un error al tratar de rol de tooa principal de servicio de tooassign Hola. 

toocheck sus permisos de suscripción:

1. Si no ya desea en su cuenta de Azure AD de hello pasos anteriores, seleccione **Azure Active Directory** en el panel izquierdo de Hola.

2. Encuentre la cuenta de Azure AD. Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
2. Busque la cuenta y selecciónela cuando la encuentre.

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Seleccione **Azure resources** (Recursos de Azure).

     ![seleccionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Ver los roles asignados y determine si tiene los permisos adecuados tooassign un rol de tooa de aplicación de AD. Si no es así, pida su tooadd de administrador de suscripción rol Administrador de acceso tooUser. Hola después de la imagen, usuario de hello es rol de propietario de toohello asignado para las dos suscripciones, lo que significa que el usuario tiene los permisos adecuados. 

     ![mostrar permisos](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Creación de una aplicación de Azure Active Directory
1. Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).
2. Seleccione **Azure Active Directory**.

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Seleccione **App registrations** (Registros de aplicaciones).   

     ![seleccionar registros de aplicaciones](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Seleccione **Agregar**.

     ![agregar aplicación](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Proporcione un nombre y la dirección URL para la aplicación hello. Seleccione **aplicación Web / API** o **nativo** para el tipo de saludo de aplicación desea toocreate. Después de establecer valores de hello, seleccione **crear**.

     ![aplicación de nombre](./media/resource-group-create-service-principal-portal/create-app.png)

Ha creado la aplicación.

## <a name="get-application-id-and-authentication-key"></a>Obtención del id. y la clave de autenticación de la aplicación
Al iniciar sesión mediante programación, se necesita Id. de hello para la aplicación y una clave de autenticación. tooget los valores, Hola uso pasos:

1. En **Registros de aplicaciones**, en Azure Active Directory, seleccione su aplicación.

     ![seleccionar aplicación](./media/resource-group-create-service-principal-portal/select-app.png)
2. Hola copia **Id. de aplicación** y almacenarlo en el código de aplicación. Hola aplicaciones Hola [aplicaciones de ejemplo](#sample-applications) sección hacen referencia a valor toothis como identificador de cliente de Hola.

     ![ID. DE CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate una clave de autenticación, seleccione **claves**.

     ![seleccionar claves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Proporcione una descripción de clave de hello y una duración para la clave de Hola. Cuando haya terminado, seleccione **Guardar**.

     ![guardar clave](./media/resource-group-create-service-principal-portal/save-key.png)

     Después de guardar la clave de hello, se muestra el valor de Hola de clave de Hola. Copie este valor porque no es capaz de tooretrieve clave de hello más tarde. Proporcionar valor de clave de hello con toolog de Id. de aplicación hello en como aplicación hello. Almacene el valor de clave de Hola donde la aplicación pueda recuperarlos.

     ![clave guardada](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Obtención del identificador de inquilino
Al iniciar sesión mediante programación, deberá Id. de inquilino de hello toopass con su solicitud de autenticación. 

1. Id. de inquilino de hello tooget, seleccione **propiedades** para su inquilino de Azure AD. 

     ![Selección de las propiedades de Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Hola copia **Id. de directorio**. Este valor es el id. de inquilino.

     ![id. de inquilino](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Asignar toorole de aplicación
tooaccess recursos de la suscripción, debe asignar el rol de tooa de aplicación Hola. Decidir qué rol representa permisos adecuados de hello para la aplicación hello. toolearn sobre los roles disponibles de hello, consulte [RBAC: integrada en Roles](../active-directory/role-based-access-built-in-roles.md).

Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso. Los permisos son heredados toolower niveles de ámbito. Por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos indica que puede leer el grupo de recursos de Hola y los recursos que contenga.

1. Navegue toohello nivel de ámbito que se va tooassign aplicación Hola. Por ejemplo, tooassign un rol en el ámbito de la suscripción de hello, seleccione **suscripciones**. También puede seleccionar un grupo de recursos o un recurso.

     ![seleccionar suscripción](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Seleccionar Hola suscripción en particular (grupo de recursos o recursos) tooassign Hola aplicación.

     ![seleccionar suscripción para la asignación](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Seleccione **Access Control (IAM)**.

     ![seleccionar acceso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Seleccione **Agregar**.

     ![seleccionar agregar](./media/resource-group-create-service-principal-portal/select-add.png)
6. Seleccione rol Hola desea tooassign toohello aplicación. Hello siguiente imagen muestra hello **lector** rol.

     ![seleccionar rol](./media/resource-group-create-service-principal-portal/select-role.png)

8. Busque la aplicación y selecciónela.

     ![buscar aplicación](./media/resource-group-create-service-principal-portal/search-app.png)
9. Seleccione **Aceptar** toofinish asignación de rol de Hola. Verá que su aplicación en la lista de Hola de los usuarios asignados a roles tooa para ese ámbito.

## <a name="log-in-as-hello-application"></a>Inicie sesión como aplicación hello

La aplicación está ahora configurada en Azure Active Directory. Tiene un Id. y clave toouse para iniciar sesión como aplicación hello. aplicación Hello se asigna el rol de tooa que le da algunas acciones que puede realizar. Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [CLI de Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Pasos siguientes
* tooset de una aplicación de varios inquilinos, consulte [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).
* toolearn acerca de cómo especificar directivas de seguridad, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).  
* Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
