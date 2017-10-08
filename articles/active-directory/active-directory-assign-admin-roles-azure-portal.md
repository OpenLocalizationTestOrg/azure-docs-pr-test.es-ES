---
title: roles de administrador de aaaAssigning en Azure Active Directory | Documentos de Microsoft
description: "Un rol de administrador puede crear o editar usuarios, asignar roles administrativos tooothers, restablecer contraseñas de usuario, administrar licencias de usuario o administrar dominios. Un usuario que está asignado un rol de administrador tiene Hola mismos permisos en todos los toowhich de servicios de nube ha suscrito su organización."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: it-pro;
ms.openlocfilehash: 41cddbf311767d9995c99ee386e6d276745dad18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Asignación de roles de administrador en Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-assign-admin-roles-azure-portal.md)
> * [Portal de Azure clásico](active-directory-assign-admin-roles.md)
>
>

Con Azure Active Directory (Azure AD), puede designar administradores independientes tooserve diferentes funciones. Estos administradores tendrán acceso toovarious características de hello portal de Azure o un portal de Azure clásico y, según su función, estarán toocreate capaz o editar usuarios, asignar roles administrativos tooothers, restablecer contraseñas de usuario, administrar licencias de usuario, y administrar dominios, entre otras cosas. Un usuario que está asignado un rol de administrador tendrán Hola Hola rol Hola portal de Office 365 mismos permisos en todos los servicios de nube de Hola que se haya suscrito su organización, independientemente de si se ha asignado u Hola Hola portal de Azure clásico o mediante Módulo de Azure AD para Windows PowerShell.

Hola después de roles de administrador está disponible:

* **Administrador de facturación**: hace compras, administra suscripciones, administra incidencias de soporte técnico y supervisa el estado del servicio.

* **Administrador de cumplimiento de normas**: los usuarios con este rol tienen permisos de administración en Office 365 seguridad Hola & Centro de cumplimiento y centro de administración de Exchange. Más información en "[Acerca de los roles de administrador de Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)".

* **Administrador de servicios de CRM**: los usuarios con este rol tienen permisos globales en Microsoft CRM Online, al servicio de hello está presente, así como de hello capacidad toomanage incidencias de soporte técnico y supervisar el estado del servicio. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administradores de dispositivos**: los usuarios con este rol ser administradores del equipo local en todos los dispositivos Windows 10 tooAzure unido a Active Directory. No tiene objetos de hello capacidad toomanage dispositivos en Azure Active Directory.

* **Lectores de directorio**: este es un rol heredado que está tooapplications toobe asignado que no admiten hello [marco de consentimiento](active-directory-integrating-applications.md). No deben asignarse a los usuarios de tooany.

* **Cuentas de sincronización de directorio**: no se usan. Este rol se asigna automáticamente el servicio de toohello AD Azure Connect y no está diseñado o se admiten para cualquier otro uso.

* **Escritores de directorio**: este es un rol heredado que está tooapplications toobe asignado que no admiten hello [marco de consentimiento](active-directory-integrating-applications.md). No deben asignarse a los usuarios de tooany.

* **Administrador de servicios de Exchange**: los usuarios con este rol tienen permisos globales en Microsoft Exchange Online, cuando el servicio Hola está presente. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrador global o administrador de la compañía**: los usuarios con este rol tienen características administrativas de acceso tooall en Azure Active Directory, así como servicios que tooAzure permite la federación de Active Directory como Exchange Online, SharePoint Online, y Skype empresarial Online. Hola quien se suscribe a los inquilinos de Azure Active Directory Hola se convierte en un administrador global. Los administradores globales son los únicos que pueden asignar otros roles de administrador. Puede haber más de un administrador global en su empresa. Administradores globales pueden restablecer la contraseña de Hola para todos los usuarios y todos los otros administradores.

  > [!NOTE]
  > En la API Graph de Microsoft, la API de Azure AD Graph, y Azure AD PowerShell, este rol se identifica como "administrador de la compañía". Es "Administrador Global" Hola [portal de Azure](https://portal.azure.com).
  >
  >

* **Invitado Invitador**: los usuarios de este rol pueden administrar invitaciones de usuario de invitado de Azure Active Directory B2B cuando Hola "Pueden invitar miembros" usuario se debe establecer tooNo. Para obtener más información acerca de la colaboración B2B en [acerca de la vista previa de la colaboración B2B de Azure AD de hello](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). No incluye otros permisos.

* **Administrador de servicios de Intune**: los usuarios con este rol tienen permisos globales en Microsoft Intune Online, cuando el servicio Hola está presente. Además, esta función contiene los usuarios toomanage de capacidad de Hola y dispositivos en la directiva de orden tooassociate, así como crear y administrar grupos.

* **Administrador de buzones de correo**: este rol solo se usa como parte de la compatibilidad con el correo electrónico de Exchange Online para dispositivos RIM Blackberry. Si su organización no usa el correo electrónico de Exchange Online en dispositivos RIM Blackberry, no utilice este rol.

* **Compatibilidad con el nivel 1 de asociado**: no lo utilice. Esta función está en desuso y se quitará de Azure AD en hello futuras. Este rol está diseñado para que lo usen un pequeño número de asociados de reventa de Microsoft, no para un uso general.

* **Compatibilidad con el nivel 2 de asociado**: no lo utilice. Esta función está en desuso y se quitará de Azure AD en hello futuras. Este rol está diseñado para que lo usen un pequeño número de asociados de reventa de Microsoft, no para un uso general.

* **Administrador de contraseñas / administrador del departamento de soporte técnico**: los usuarios con este rol pueden restablecer contraseñas, administrar solicitudes de servicio y supervisar el estado del servicio. Los administradores de contraseñas pueden restablecer contraseñas solo para los usuarios y otros administradores de contraseñas.

  > [!NOTE]
  > En la API Graph de Microsoft, la API Graph de Azure AD y Azure AD PowerShell, este rol se identifica como "Administrador de soporte técnico". Es "Administrador de contraseñas" en hello [portal de Azure](https://portal.azure.com/).
  >
  >
  
* **Administrador de servicios de Power BI**: los usuarios con este rol tienen permisos globales en Microsoft Power BI, al servicio de hello está presente, así como de hello capacidad toomanage incidencias de soporte técnico y supervisar el estado del servicio. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Administrador de roles con privilegios**: los usuarios con este rol pueden administrar asignaciones de rol en Azure Active Directory, así como también dentro de Azure AD Privileged Identity Management. Además, este rol permite administrar todos los aspectos de Privileged Identity Management.

* **Administrador de seguridad**: los usuarios con este rol tienen todos los permisos de solo lectura de Hola de rol de lector de seguridad de hello, además de toomanage configuración de capacidad de Hola para los servicios relacionados con la seguridad: Azure Active Directory Identity Protection Administración de identidad con privilegios y seguridad de Office 365 y centro de cumplimiento. Para obtener más información acerca de los permisos de Office 365 está disponible en [permisos en Office 365 seguridad Hola & Centro de cumplimiento](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Lector de seguridad**: los usuarios con este rol tiene acceso de solo lectura global, incluida toda la información en Azure Active Directory Identity Protection, Privileged Identity Management, así como Hola inicio de sesión en Azure Active Directory de tooread de capacidad los informes y registros de auditoría. rol de Hello también concede el permiso de solo lectura en el centro de cumplimiento y seguridad de Office 365. Para obtener más información acerca de los permisos de Office 365 está disponible en [permisos en Office 365 seguridad Hola & Centro de cumplimiento](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Administrador de servicios admiten**: los usuarios con este rol pueden abrir solicitudes de soporte técnico con Microsoft para los servicios de Azure y Office 365 y vistas Hola centro de panel y los mensajes de servicio en el portal de Azure de Hola y portal de administración de Office 365. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrador de servicios de SharePoint**: los usuarios con este rol tienen permisos globales dentro de Microsoft SharePoint Online, al servicio de hello está presente, así como de hello capacidad toomanage incidencias de soporte técnico y supervisar el estado del servicio. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype empresarial / Administrador de servicios de Lync**: los usuarios con este rol tiene permisos globales en Microsoft Skype para la empresa, al servicio de hello está presente, así como administrar los atributos de usuario de Skype específicos en Azure Active Directory. Además, este incidencias de soporte técnico de toomanage de capacidad de rol concede Hola y el monitor de estado del servicio. Más información en [Acerca de los roles de administrador de Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > En API Graph de Microsoft, API Graph de Azure AD y Azure AD PowerShell, este rol se identifica como "Administrador de servicio de Lync". Es "Skype para Administrador corporativo de servicio" Hola [portal de Azure](https://portal.azure.com/).
  >
  >

* **Administrador de cuentas de usuario**: los usuarios con este rol pueden crear y administrar todos los aspectos de usuarios y grupos. Además, este rol incluye incidencias de soporte técnico de toomanage de capacidad de Hola y monitores de estado del servicio. Se aplican algunas restricciones. Por ejemplo, este rol no permite eliminar un administrador global, y si bien sí permite que los usuarios no administradores cambien contraseñas, no permite que los administradores globales cambien las contraseñas de toros administradores con privilegios.

## <a name="administrator-permissions"></a>Permisos de administrador

### <a name="billing-administrator"></a>Administrador de facturación

| Puede hacer | No puede hacer |
| --- | --- |
|<p>Ver información de usuario y de la compañía</p><p>Administrar incidencias de soporte técnico de Office</p><p>Realizar operaciones de facturación y compra productos de Office</p> |<p>Restablecer las contraseñas de los usuarios</p><p>Crear y administrar vistas de usuario</p><p>Crear, editar y eliminar usuarios y grupos, y administrar licencias de usuario</p><p>Administrar dominios</p><p>Administrar información de la compañía</p><p>Delegar roles administrativos tooothers</p><p>Usar la sincronización de directorios</p><p>Visualización de registros de auditoría</p>|

### <a name="global-administrator"></a>Administrador global
| Puede hacer | No puede hacer |
| --- | --- |
| <p>Ver información de usuario y de la compañía</p><p>Administrar incidencias de soporte técnico de Office</p><p>Realizar operaciones de facturación y compra productos de Office</p><p>Restablecer las contraseñas de los usuarios</p>
<p>Restablecer las contraseñas de otro administrador</p> <p>Crear y administrar vistas de usuario</p><p>Crear, editar y eliminar usuarios y grupos, y administrar licencias de usuario</p><p>Administrar dominios</p><p>Administrar información de la compañía</p><p>Delegar roles administrativos tooothers</p><p>Usar la sincronización de directorios</p><p>Habilitar o deshabilitar Multi-Factor Authentication</p><p>Visualización de registros de auditoría</p> |N/D |

### <a name="password-administrator"></a>Administrador de contraseñas
| Puede hacer | No puede hacer |
| --- | --- |
| <p>Ver información de usuario y de la compañía</p><p>Administrar incidencias de soporte técnico de Office</p><p>Restablecer las contraseñas de los usuarios</p> <p>Restablecer las contraseñas de otro administrador</p>|<p>Realizar operaciones de facturación y compra productos de Office</p><p>Crear y administrar vistas de usuario</p><p>Crear, editar y eliminar usuarios y grupos, y administrar licencias de usuario</p><p>Administrar dominios</p><p>Administrar información de la compañía</p><p>Delegar roles administrativos tooothers</p><p>Usar la sincronización de directorios</p><p>Ver informes</p>|

### <a name="service-administrator"></a>Administrador de servicios
| Puede hacer | No puede hacer |
| --- | --- |
| <p>Ver información de usuario y de la compañía</p><p>Administrar incidencias de soporte técnico de Office</p> |<p>Restablecer las contraseñas de los usuarios</p><p>Realizar operaciones de facturación y compra productos de Office</p><p>Crear y administrar vistas de usuario</p><p>Crear, editar y eliminar usuarios y grupos, y administrar licencias de usuario</p><p>Administrar dominios</p><p>Administrar información de la compañía</p><p>Delegar roles administrativos tooothers</p><p>Usar la sincronización de directorios</p><p>Visualización de registros de auditoría</p> |

### <a name="user-administrator"></a>Administrador de usuarios
| Puede hacer | No puede hacer |
| --- | --- |
| <p>Ver información de usuario y de la compañía</p><p>Administrar incidencias de soporte técnico de Office</p><p>Restablecer contraseñas de usuarios, con limitaciones.</p><p>Restablecer las contraseñas de otro administrador</p><p>Restablecer las contraseñas de otros usuarios</p><p>Crear y administrar vistas de usuario</p><p>Crear, editar y eliminar usuarios y grupos, y administrar licencias de usuarios, con limitaciones. No puede eliminar un administrador global ni crear otros administradores.</p> |<p>Realizar operaciones de facturación y compra productos de Office</p><p>Administrar dominios</p><p>Administrar información de la compañía</p><p>Delegar roles administrativos tooothers</p><p>Usar la sincronización de directorios</p><p>Habilitar o deshabilitar Multi-Factor Authentication</p><p>Visualización de registros de auditoría</p> |

### <a name="security-reader"></a>Lector de seguridad
| En el | Puede hacer |
| --- | --- |
| Identity Protection Center |Leer todos los informes de seguridad y la información de configuración de las características de seguridad<ul><li>Filtro de correo no deseado<li>Cifrado<li>Prevención de la pérdida de datos<li>Antimalware<li>Protección contra amenazas avanzada<li>Protección contra suplantación de identidad (anti-phishing)<li>Reglas de flujo de correo |
| Privileged Identity Management |<p>Tiene acceso de solo lectura tooall información aparece en Azure AD PIM: directivas e informes para las asignaciones de roles de Azure AD, revisiones de seguridad y en hello futuro lee toopolicy acceder a los datos e informes de escenarios aparte de asignación de roles de Azure AD.<p>**No se puede** suscribirse a Azure AD PIM o realizar cualquier tooit de cambios. En el portal de PIM o a través de PowerShell, alguien de este rol puede activar roles adicionales (por ejemplo, el administrador Global o administrador de roles con privilegios), si el usuario de hello es un candidato para ellos. |
| <p>Supervisión de estado del servicio de Office 365</p><p>Centro de cumplimiento y seguridad de Office 365</p> |<ul><li>Leer y administrar alertas<li>Leer directivas de seguridad<li>Leer inteligencia de amenazas, Cloud App Discovery y cuarentena en búsqueda e investigación<li>Leer todos los informes |

### <a name="security-administrator"></a>Administrador de seguridad
| En el | Puede hacer |
| --- | --- |
| Identity Protection Center |<ul><li>Todos los permisos del rol de seguridad Reader de Hola.<li>Además, Hola capacidad tooperform todas las operaciones de IPC excepto para restablecer contraseñas. |
| Privileged Identity Management |<ul><li>Todos los permisos del rol de seguridad Reader de Hola.<li>**No puede** administrar la configuración de roles de Azure AD o la pertenencia a ellos. |
| <p>Supervisión de estado del servicio de Office 365</p><p>Centro de cumplimiento y seguridad de Office 365 |<ul><li>Todos los permisos del rol de seguridad Reader de Hola.<li>Puede configurar todos los valores en la característica de protección contra amenazas avanzada de hello (protección contra malware y virus, configuración de dirección URL malintencionado, seguimiento de la dirección URL, etcetera). |

## <a name="details-about-hello-global-administrator-role"></a>Obtener más información acerca de la función de administrador global de Hola
Administrador global de Hello tiene características administrativas de acceso tooall. De forma predeterminada, Hola quien se suscribe a una suscripción de Azure se asigna el rol de administrador global de hello para el directorio de Hola. Los administradores globales son los únicos que pueden asignar otros roles de administrador.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd un compañero de trabajo como un administrador global

1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio del inquilino de Hola.

   ![Abrir el Centro de administración de Azure AD](./media/active-directory-assign-admin-roles-azure-portal/active-directory-admin-center.png)

2. Seleccione **Usuarios y grupos &gt; Todos los usuarios**.

3. Busque Hola usuario desee toodesignate como administrador global y abrir la hoja de Hola para ese usuario.

4. En la hoja de usuario de hello, seleccione **rol del directorio**.
 
5. En la hoja de rol del directorio de hello, seleccione hello **administrador Global** rol y guardar.

## <a name="assign-or-remove-administrator-roles"></a>Asignación o eliminación de roles de administrador
toolearn tooassign usuario de tooa funciones administrativas en Azure Active Directory, vea [asignar roles de tooadministrator en la vista previa de Azure Active Directory de un usuario](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Roles en desuso

Hola después de roles no debe usarse. Se está en desuso y se quitará de Azure AD en hello futuras.

* Administrador de licencias ad hoc
* Creador de usuarios comprobados de correo electrónico
* Combinación de dispositivos
* Administradores de dispositivos
* Usuarios de dispositivos
* Combinación de dispositivos de área de trabajo

## <a name="next-steps"></a>Pasos siguientes

* toolearn Obtenga más información sobre cómo los administradores de toochange para una suscripción de Azure, vea [cómo tooadd o cambiar roles de administrador de Azure](../billing-add-change-azure-subscription-administrator.md)
* toolearn más información acerca de cómo se controla el acceso a los recursos en Microsoft Azure, consulte [descripción de acceso a los recursos de Azure](active-directory-understanding-resource-access.md)
* Para obtener más información sobre cómo Azure Active Directory se relaciona tooyour suscripción de Azure, consulte [se asocian con Azure Active Directory las suscripciones de Azure](active-directory-how-subscriptions-associated-directory.md)
* [Administrar usuarios](active-directory-create-users.md)
* [Administrar contraseñas](active-directory-manage-passwords.md)
* [Administrar grupos](active-directory-manage-groups.md)
