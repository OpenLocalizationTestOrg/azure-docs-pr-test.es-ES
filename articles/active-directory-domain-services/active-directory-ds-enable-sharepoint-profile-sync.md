---
title: 'Azure Active Directory Domain Services: Habilitar la compatibilidad con el servicio de perfil de usuario de SharePoint | Microsoft Docs'
description: "Configurar la sincronización de perfil de servicios de dominio de Active Directory de Azure dominios administrados toosupport de SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Configurar una sincronización de perfil de dominio administrados toosupport para SharePoint Server
SharePoint Server incluye un servicio de perfiles de usuario que se usa para la sincronización de perfiles de usuario. tooset seguridad Hola servicio de perfiles de usuario, los permisos adecuados necesitan toobe concedido en un dominio de Active Directory. Para más información, vea [Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

Este artículo explica cómo puede configurar el servicio de sincronización de perfil de usuario de SharePoint Server de servicios de dominio de AD de Azure dominios administrados toodeploy Hola.

## <a name="hello-aad-dc-service-accounts-group"></a>grupo de Hello 'Cuentas de servicio de controlador de dominio de AAD'
Un grupo de seguridad denominado '**cuentas de servicio de controlador de dominio de AAD**' está disponible en la unidad organizativa de hello 'Usuarios' en el dominio administrado. Puede ver este grupo en hello **equipos y usuarios de Active Directory** complemento MMC en el dominio administrado.

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Los miembros de este grupo de seguridad son delegado Hola siguientes privilegios:
- privilegio de 'Replicar los cambios en el directorio' Hello en raíz de hello DSE de hello administrados dominio.
- Hola privilegio 'Replicar los cambios en el directorio' en el contexto de nomenclatura de configuración de hello (cn = contenedor de configuración) del programa Hola a administrar el dominio.

Este grupo de seguridad también es miembro del grupo integrado hello **acceso de compatible con versiones anteriores de Windows 2000**.

![Grupo de seguridad Cuentas de servicio de controlador de dominio de AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Habilitar la sincronización del perfil de usuario de SharePoint Server toosupport de dominio administrado
Puede agregar la cuenta de servicio de hello usada para toohello de sincronización de perfil de usuario de SharePoint **cuentas de servicio de controlador de dominio de AAD** grupo. Como resultado, cuenta de sincronización de hello Obtiene el directorio de los privilegios adecuados tooreplicate cambios toohello. Este paso de configuración permite toowork de sincronización de perfil de usuario de SharePoint Server correctamente.

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Cuentas de servicio de controlador de dominio de AAD - Agregar miembros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Contenido relacionado
* [Referencia técnica - Concesión de permisos de Active Directory Domain Services para la sincronización de perfiles en SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
