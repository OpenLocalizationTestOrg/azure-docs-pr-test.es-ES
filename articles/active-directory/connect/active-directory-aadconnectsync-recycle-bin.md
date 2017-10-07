---
title: "Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD | Microsoft Docs"
description: "En este tema recomienda el uso de Hola de característica de Papelera de reciclaje de AD con Azure AD Connect."
services: active-directory
keywords: "Papelera de reciclaje de AD, eliminación accidental, sourceAnchor"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect Sync: Habilitación de la papelera de reciclaje de AD
Se recomienda habilitar característica de Papelera de reciclaje de hello AD para los directorios Active local, que son tooAzure sincronizada AD. 

Si ha eliminado accidentalmente una implementación local objeto de usuario de AD y restauración mediante la característica de hello, Azure AD restaura objeto de usuario de Azure AD correspondiente Hola.  Para obtener información acerca de la característica de Papelera de reciclaje de hello AD, consulte tooarticle [Introducción a los escenarios de restauración de eliminar objetos de Active Directory](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Ventajas de la habilitación de hello AD Papelera de reciclaje
Esta característica ayuda a con la restauración de objetos de usuario de Azure AD mediante acciones Hola siguientes:

* Si ha eliminado accidentalmente una implementación local objeto de usuario de AD, objeto de usuario de Azure AD correspondiente Hola se eliminará de hello siguiente ciclo de sincronización. De forma predeterminada, Azure AD mantiene el objeto de usuario de Azure AD Hola eliminado en estado eliminado durante 30 días.

* Si tienes local habilitada la característica de Papelera de reciclaje de AD, puede restaurar Hola eliminado local objeto de usuario de Active Directory sin cambiar su valor de delimitador de origen. Cuando Hola recuperado local se sincroniza el objeto de usuario de AD tooAzure AD, Azure AD restaurará Hola correspondiente eliminado objeto de usuario de Azure AD. Para obtener información sobre el atributo de delimitador de origen, consulte tooarticle [Azure AD Connect: conceptos de diseño](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Si no tiene local habilitada la característica de Papelera de reciclaje de AD, es posible que toocreate requiere un objeto AD usuario objeto tooreplace Hola eliminado. Si el servicio de sincronización de Connect de Azure AD toouse configurado generados por el sistema AD atributo (por ejemplo, ObjectGuid) para el atributo de delimitador de origen de hello, hello recién creado objetos de usuario de AD no habrá Hola mismo valor de delimitador de origen como Hola eliminado el objeto de usuario de AD. Una vez hello recién creado objetos de usuario de AD tooAzure sincronizada AD, Azure AD crea un nuevo objeto de usuario de Azure AD en lugar de restaurar el objeto de usuario de Azure AD Hola eliminado.

> [!NOTE]
> De forma predeterminada, Azure AD mantiene los objetos de usuario de Azure AD eliminados en estado de eliminación temporal durante 30 días antes de eliminarlos permanentemente. Sin embargo, los administradores pueden acelerar la eliminación de Hola de dichos objetos. Una vez que se eliminan permanentemente los objetos de hello, ya no se pueden recuperar, incluso si está habilitada la característica de Papelera de reciclaje de AD en local real.



## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)

* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
