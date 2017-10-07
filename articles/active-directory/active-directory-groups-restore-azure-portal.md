---
title: grupo de aaaRestore un eliminado Office 365 en Azure Active Directory | Documentos de Microsoft
description: "¿Cómo toorestore un grupo eliminado y ver grupos pueden restaurarse, permamnently eliminación un grupo en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Restauración de un grupo eliminado de Office 365 en Azure Active Directory

Cuando se elimina un grupo de Office 365 en hello Azure Active Directory (Azure AD), grupo de hello eliminado es retenido pero no está visible durante 30 días desde la fecha de eliminación de Hola. Esto es para que el grupo de Hola y su contenido se puede restaurar si es necesario. Esta funcionalidad está restringida exclusivamente tooOffice 365 grupos en Azure AD. No está disponible para los grupos de seguridad ni los grupos de distribución.

> [!NOTE] 
> No utilice `Remove-MsolGroup` porque purga grupo Hola permanentemente. Utilice siempre `Remove-AzureADMSGroup` grupo toodelete un Office 365. 

se requieren permisos de Hello toorestore un grupo puede ser cualquiera de hello siguientes:

Rol  | Permisos 
--------- | ---------
Administrador de la compañía, Soporte para asociados de nivel 2 y Administradores de servicio de Intune | Puede restaurar cualquier grupo eliminado de Office 365 
Administrador de cuenta de usuario y Soporte para asociados de nivel 1 | Puede restaurar cualquier grupo de Office 365 eliminado excepto los toohello asignado el rol de administrador de la compañía 
Usuario | Puede restaurar cualquier grupo eliminado de Office 365 de su propiedad 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Hola Vista elimina grupos de Office 365 toorestore disponible
Hola siguientes cmdlets puede ser utilizados tooview Hola elimina grupos tooverify que Hola uno o aquellos que le interesa que no aún se hayan permanentemente purgados. Estos cmdlets forman parte del programa Hola a [módulo de PowerShell de Azure AD](https://www.powershellgallery.com/packages/AzureAD/). Para obtener más información acerca de este módulo puede encontrarse en hello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0) artículo.

1.  Ejecute hello siguiente cmdlet toodisplay de eliminar todos los grupos de Office 365 en el inquilino que son toorestore seguirá estando disponible.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Como alternativa, si sabe objectID Hola de un grupo específico (y puede obtenerlo de cmdlet de hello en el paso 1), ejecución Hola después tooverify de cmdlet que Hola específico grupo eliminado no todavía permanentemente purgado.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Cómo toorestore el grupo de Office 365 eliminado
Una vez que haya verificado de que ese grupo de hello es toorestore seguirá estando disponible, restaure grupo Hola eliminado con uno de los pasos de Hola. Si el grupo de hello contiene documentos, sitios de SP u otros objetos persistentes, podría tardar hasta too24 horas toofully restaurar un grupo y su contenido.

1.  Ejecución hello siguientes cmdlet toorestore Hola grupo y su contenido.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Como alternativa, hello siguiente cmdlet se puede ejecutar toopermanently quitar grupo de hello eliminado.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>¿Cómo se puede saber si funcionó?
tooverify que ha restaurado correctamente un grupo de Office 365, ejecute hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay información sobre el grupo de Hola. Después de la restauración de hello completar la solicitud:
- Hola grupo aparecerá en la barra de navegación izquierdo de hello en Exchange
- plan de Hello para el grupo de hello aparecerá en Planificador
- Los sitios de SharePoint y su contenido estarán disponibles
- grupo de Hello son accesibles desde cualquiera de los puntos de conexión de Exchange de Hola y otras cargas de trabajo de Office 365 que admiten los grupos de Office 365


## <a name="next-steps"></a>Pasos siguientes
En estos artículos se proporciona información adicional sobre los grupos de Azure Active Directory.

* [Consulta de los grupos existentes](active-directory-groups-view-azure-portal.md)
* [Administración de la configuración de un grupo](active-directory-groups-settings-azure-portal.md)
* [Administrar miembros de un grupo](active-directory-groups-members-azure-portal.md)
* [Administrar la pertenencia a grupos](active-directory-groups-membership-azure-portal.md)
* [Administrar reglas dinámicas de los usuarios de un grupo](active-directory-groups-dynamic-membership-azure-portal.md)
