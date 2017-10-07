---
title: "aaaPreview Office 365 agrupa expiración en Azure Active Directory | Documentos de Microsoft"
description: "Cómo agrupa tooset la expiración para Office 365 en Azure Active Directory (versión preliminar)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Configuración de la expiración de grupos de Office 365 (versión preliminar)

Ahora puede administrar el ciclo de vida de Hola de grupos de Office 365 estableciendo la expiración de los grupos de Office 365 que seleccione. Una vez establecida esta expiración, los propietarios de los grupos son más frecuentes toorenew sus grupos si es necesario grupos Hola. Los grupos de Office 365 que no se renueven se eliminarán. Cualquier grupo de Office 365 que se ha eliminado se puede restaurar durante los 30 días propietarios del grupo de Hola o un administrador de Hola.  


> [!NOTE]
> Solo puede establecer la expiración de grupos de Office 365.
>
> El establecimiento de la expiración de grupos de O365 requiere que se asigne una licencia de Azure AD Premium a:
>   - Administrador de Hola que configura la configuración de inquilino de Hola Hola expiración
>   - Todos los miembros de grupos de hello seleccionados para esta configuración

## <a name="set-office-365-groups-expiration"></a>Establecimiento de la expiración de grupos de Office 365

1. Abra hello [centro de administración de Azure AD](https://aad.portal.azure.com) con una cuenta que sea un administrador global de inquilino de Azure AD.

2. Abra Azure AD y seleccione **Usuarios y grupos**.

3. Seleccione **configuración de grupo** y, a continuación, seleccione **caducidad** tooopen configuración de la expiración de Hola.
  
  ![Hoja Expiración](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. En hello **caducidad** hoja, puede:

  * Establecer la duración del grupo de hello en días. Puede seleccionar uno de hello preestablece valores o un valor personalizado (debe ser 31 días o más). 
  * Especifique una dirección de correo electrónico donde se deben enviar notificaciones de caducidad y renovación de hello cuando un grupo no tiene propietario. 
  * Seleccionar los grupos de Office 365 que expiran. Puede habilitar la expiración para **todos los** grupos de Office 365, puede seleccionar de entre los grupos de Office 365 Hola o seleccionar **ninguno** para deshabilitar la expiración de todos los grupos.
  * Guardar la configuración cuando haya terminado seleccionando **Guardar**.

Para obtener instrucciones sobre cómo toodownload e instalar Hola tooconfigure caducidad de módulo de PowerShell de Microsoft para los grupos de Office 365 a través de PowerShell, consulte [módulo Azure Active Directory V2 PowerShell - versión de vista previa pública 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Se envían notificaciones por correo electrónico como éste propietarios del grupo toohello Office 365 30 días, 15 días y tooexpiration anterior del día 1, del grupo de Hola.

![Notificación por correo electrónico de expiración](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

propietario del grupo de Hello, a continuación, puede seleccionar **grupo renovar** toorenew Hola grupo de Office 365, o puede seleccionar **vaya toogroup** toosee miembros de Hola y otros detalles acerca de Hola grupo.

Cuando expira un grupo, el grupo de Hola se elimina un día después de la fecha de expiración de Hola. Se envía una notificación de correo electrónico como éste propietarios del grupo toohello Office 365 que les informa acerca de la expiración de Hola y eliminación posterior de su grupo de Office 365.

![Notificación por correo electrónico de eliminación del grupo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

grupo de Hello puede restaurarse seleccionando **restauración grupo** o mediante cmdlets de PowerShell, tal y como se describe en [grupo de restauración un eliminado Office 365 en Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-restore-Azure-Portal).
    
Si va a restaurar el grupo de hello contiene documentos, los sitios de SharePoint u otros objetos persistentes, podría tardar hasta too24 horas toofully restauración Hola grupo y su contenido.

> [!NOTE]
> * Al implementar la configuración de la expiración de hello, podría haber algunos grupos que sean más antiguos que la ventana de expiración de hello. Estos grupos no se eliminarán inmediatamente, pero son establecer too30 días hasta la expiración. correo electrónico de notificación primer de renovación de Hola se envía dentro de un día. Por ejemplo, un grupo se creó hace 400 días, y se establece el intervalo de expiración de hello too180 días. Cuando aplica la configuración de expiración, un grupo tiene 30 días antes de eliminarla, a menos que el propietario de Hola renueva.
> * Cuando se elimina un grupo dinámico y se restaura, se ve como un nuevo grupo y vuelve a llenar regla toohello correspondiente. Este proceso puede tardar horas too24.

## <a name="next-steps"></a>Pasos siguientes
En estos artículos se proporciona información adicional sobre los grupos de Azure AD.

* [Consulta de los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Administración de la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar miembros de un grupo](active-directory-groups-members-azure-portal.md)
* [Administrar la pertenencia a grupos](active-directory-groups-membership-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
