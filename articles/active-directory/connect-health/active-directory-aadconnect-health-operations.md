---
title: operaciones de Active Directory Connect Health aaaAzure
description: "Este artículo describe las operaciones adicionales que pueden realizarse una vez que haya implementado Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Operaciones de Azure Active Directory Connect Health
Este tema describe Hola varias operaciones puede realizar mediante el mantenimiento de Connect de Azure Active Directory (Azure AD).

## <a name="enable-email-notifications"></a>Habilitación de notificaciones de correo electrónico
Puede configurar notificaciones de correo electrónico de hello Azure AD Connect Health service toosend cuando las alertas indican que la infraestructura de identidad no es correcto. Esto se produce cuando se genera una alerta y cuando se resuelve.

![Captura de pantalla de la configuración de notificaciones de correo electrónico de Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> Las notificaciones de correo electrónico están habilitadas de forma predeterminada.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>notificaciones de correo electrónico de tooenable Azure AD Connect Health
1. Abra hello **alertas** hoja para servicio de hello para el que desea tooreceive notificación de correo electrónico.
2. En la barra de acciones de hello, haga clic en **configuración de notificación**.
3. En el conmutador de notificación de correo electrónico de hello, seleccione **ON**.
4. Active la casilla de verificación de hello si desea que todas las notificaciones de correo electrónico de los administradores globales tooreceive.
5. Si desea que las notificaciones de correo electrónico de tooreceive en ninguna otra dirección de correo electrónico, especifíquelas en hello **los destinatarios de correo electrónico adicionales** cuadro. tooremove una dirección de correo electrónico en esta lista, haga clic en la entrada de Hola y seleccione **eliminar**.
6. toofinalize Hola cambios, haga clic en **guardar**. Los cambios surtirán efecto después de guardar.

## <a name="delete-a-server-or-service-instance"></a>Eliminación de una instancia de servidor o servicio

En algunos casos, es recomendable tooremove un servidor desde el que se está supervisando. Esto es lo necesita tooknow tooremove un servidor de servicio de hello Azure AD Connect Health.

Cuando se dispone a eliminar un servidor, tenga Hola siguiente:

* Esta acción detiene cualquier recopilación de datos de ese servidor. Este servidor se quita del servicio de supervisión de Hola. Después de esta acción no está tooview capaz de nuevas alertas, supervisión o datos de análisis de uso para este servidor.
* Esta acción no desinstala Hola agente de mantenimiento del servidor. Si no ha desinstalado Hola agente de mantenimiento antes de llevar a cabo este paso, podría ver errores relacionados toohello agente de mantenimiento en el servidor de Hola.
* Esta acción no elimina los datos de saludo ya se han recopilado desde este servidor. Esos datos se eliminan según Hola directiva de retención de datos de Azure.
* Después de realizar esta acción, si desea supervisar toostart Hola mismo servidor nuevo, debe desinstalar y volver a instalar agente de mantenimiento de hello en este servidor.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete un servidor de servicio de hello Azure AD Connect Health
Azure AD Connect Health para Servicios de federación de Active Directory (AD FS) y Azure AD Connect (Sync):

1. Hola abierto **Server** hoja de hello **lista de servidores** hoja seleccionando toobe de nombre de servidor hello quitado.
2. En hello **Server** hoja, de la barra de acciones de hello, haga clic en **eliminar**.
3. Confirme escribiendo el nombre del servidor de hello en el cuadro de confirmación de Hola.
4. Hacer clic en **Eliminar**.

Azure AD Connect Health para Azure Active Directory Domain Services:

1. Abra hello **controladores de dominio** panel.
2. Toobe de controlador de dominio de hello seleccione Quitar.
3. En la barra de acciones de hello, haga clic en **eliminar seleccionado**.
4. Confirme el servidor de hello acción toodelete Hola.
5. Hacer clic en **Eliminar**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Eliminación de una instancia de servicio del Servicio de Azure AD Connect Health
En algunos casos, es recomendable tooremove una instancia de servicio. Aquí es lo que necesita tooknow tooremove un servicio en la instancia de servicio de hello Azure AD Connect Health.

Cuando se dispone a eliminar una instancia de servicio, tenga Hola siguiente:

* Esta acción quita la instancia de servicio actual de Hola Hola servicio de supervisión.
* Esta acción no desinstalará ni quitará Hola agente de mantenimiento de cualquiera de los servidores de Hola que se han supervisado como parte de esta instancia del servicio. Si no ha desinstalado Hola agente de mantenimiento antes de realizar este paso, puede ver errores relacionados toohello agente de mantenimiento en los servidores de Hola.
* Todos los datos de esta instancia de servicio se elimina según Hola directiva de retención de datos de Azure.
* Después de realizar esta acción, si desea toostart Hola servicio de supervisión, desinstale y reinstale Hola agente de mantenimiento en todos los servidores de Hola. Después de realizar esta acción, si desea que toostart supervisión Hola mismo servidor nuevo, desinstalar, reinstalar y registrar Hola a agente de mantenimiento en ese servidor.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete una instancia de servicio del servicio de hello Azure AD Connect Health
1. Abra hello **servicio** hoja de hello **lista servicio** hoja, seleccione el identificador del servicio de hello (nombre de granja de servidores) que desea tooremove.
2. En hello **Server** hoja, de la barra de acciones de hello, haga clic en **eliminar**.
3. Confirmar escribiendo el nombre del servicio de hello en el cuadro de confirmación de hello (por ejemplo: sts.contoso.com).
4. Hacer clic en **Eliminar**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Administración de accesos con el control de acceso basado en rol
[Control de acceso basado en roles (RBAC)](../role-based-access-control-configure.md) de Azure AD Connect Health proporciona acceso toousers y grupos distintos de los administradores globales. RBAC asigna roles toohello pensado usuarios y grupos y proporciona un mecanismo de administradores globales de hello toolimit dentro de su directorio.

### <a name="roles"></a>Roles
Azure AD Connect Health admite Hola siguientes funciones integradas:

| Rol | Permisos |
| --- | --- |
| Propietario |Los propietarios pueden *administrar el acceso* (por ejemplo, asignar un rol tooa usuario o grupo), *ver toda la información* (por ejemplo, ver las alertas) desde el portal de hello, y *cambiar la configuración de* () Por ejemplo, notificaciones por correo electrónico) en Azure AD Connect Health. <br>De forma predeterminada, a los administradores globales de Azure AD se les asigna este rol y esto no se puede cambiar. |
| Colaborador |Colaboradores pueden *ver toda la información* (por ejemplo, ver las alertas) desde el portal de hello, y *cambiar la configuración de* (por ejemplo, notificaciones de correo electrónico) en Azure AD Connect Health. |
| Lector |Los lectores pueden *ver toda la información* (por ejemplo, ver las alertas) desde el portal de hello en Azure AD Connect Health. |

Todos los demás roles (por ejemplo, los administradores de acceso de usuario o los usuarios de laboratorios de desarrollo y pruebas) no tengan ningún tooaccess impacto dentro de Azure AD Connect Health, aunque Hola roles están disponibles en la experiencia del portal Hola.

### <a name="access-scope"></a>Ámbito de acceso
Azure AD Connect Health admite la administración de acceso a dos niveles:

* **Todas las instancias de servicio**: se trata de hello recomendada la ruta de acceso en la mayoría de los casos. Controla el acceso a todas las instancias de servicio (por ejemplo, a una granja de servidores de AD FS) en todos los tipos de rol que se estén supervisando mediante Azure AD Connect Health.
* **Instancia del servicio**: en algunos casos, puede que tenga acceso toosegregate basado en tipos de rol o por una instancia de servicio. En este caso, puede administrar el acceso en el nivel de instancia del servicio de Hola.  

El permiso se concede si un usuario final tiene acceso al directorio de Hola o servicio nivel de instancia.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Permitir que los usuarios o grupos acceso tooAzure AD Connect Health
Hello pasos siguientes muestran cómo tener acceso tooallow.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Paso 1: Seleccione el ámbito de acceso adecuado de Hola
un acceso de usuario en hello tooallow *todas las instancias de servicio* nivel dentro de Azure AD Connect Health, hoja principal de hello abierto en Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Paso 2: Agregar usuarios, grupos y asignar roles
1. De hello **configurar** sección, haga clic en **usuarios**.<br>
   ![Captura de pantalla de la hoja principal del control de acceso basado en rol de Azure AD Connect Health, con usuarios resaltados](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Seleccione **Agregar**.
3. Hola **seleccione un rol** panel, seleccione un rol (por ejemplo, **propietario**).<br>
   ![Captura de pantalla de la ventana Usuarios del control de acceso basado en rol de Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Escriba el nombre de Hola o identificador de usuario de destino de Hola o grupo. Puede seleccionar uno o más usuarios o grupos en hello mismo tiempo. Haga clic en **Seleccionar**.
   ![Captura de pantalla de la ventana Usuarios del control de acceso basado en rol de Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Seleccione **Aceptar**.<br>
6. Una vez completada la asignación de roles de hello, Hola usuarios y grupos aparecen en la lista de Hola.<br>
   ![Captura de pantalla de la ventana Usuarios del control de acceso basado en rol de Azure AD Connect Health, con nuevos usuarios resaltados](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Hello muestra ahora los usuarios y grupos tienen acceso, según tootheir asignan roles.

> [!NOTE]
> * Los administradores globales tienen siempre las operaciones de acceso completo tooall hello, pero las cuentas de administrador global no están presentes en hello precede a lista.
> * no se admite la característica de invitar a usuarios de Hello en Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Paso 3: Compartir ubicación de la hoja de hello con usuarios o grupos
1. Después de asignar permisos, un usuario puede acceder a Azure AD Connect Health yendo [aquí](http://aka.ms/aadconnecthealth).
2. En la hoja de hello, puede anclar usuario Hola hoja Hola o partes diferentes del mismo, toohello panel. Simplemente haga clic en hello **toodashboard Pin** icono.<br>
   ![Captura de pantalla de la hoja del control de acceso basado en rol de Azure AD Connect Health, con el icono de anclaje resaltado](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Un usuario con rol de lector de hello asignado no es capaz de tooget extensión de Azure AD Connect Health de hello Azure Marketplace. usuario de Hello no puede realizar por lo que Hola necesarios toodo operación "crear". usuario de Hello todavía puede obtener hoja toohello por toohello vaya delante de vínculo. Para un uso posterior, usuario Hola puede anclar el panel de toohello de hoja de Hola.
>
>

### <a name="remove-users-or-groups"></a>Eliminación de usuarios o grupos
Puede quitar un usuario o un grupo agregado tooAzure AD RBAC de mantenimiento de conexión. Simplemente haga Hola usuario o grupo y a continuación **quitar**.<br>
![Captura de pantalla de la ventana Usuarios del control de acceso basado en rol de Azure AD Connect Health, con la opción Quitar resaltada](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Pasos siguientes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalación del Agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
