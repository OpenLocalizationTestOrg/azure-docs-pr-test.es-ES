---
title: "aaaTroubleshooting pertenencia dinámica para grupos | Documentos de Microsoft"
description: "Solución de problemas para la pertenencia dinámica para grupos en Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Solución de problemas relacionados con las pertenencias dinámicas para grupos
**He configurado una regla en un grupo pero ningún pertenencias a grupos se actualizan en el grupo de Hola**<br/>Compruebe que hello **Habilitar administración de grupos delegados** opción se establece demasiado**Sí** en hello **configurar** ficha. Verá esta opción únicamente si ha iniciado sesión ya está asignado a un toowhom de usuario una licencia de Azure Active Directory Premium. Comprobar los valores de hello para los atributos de usuario en la regla de hello: ¿hay usuarios que cumplen la regla de hello?

**He configurado una regla, pero ahora se quitan los miembros existentes de Hola de regla de Hola**<br/>Este es el comportamiento esperado. Los miembros existentes del grupo de Hola se quitan cuando se habilita o modifica una regla. los usuarios de Hello procedentes de la evaluación de regla de Hola se agregan como toohello grupo de miembros.     

**No veo los cambios en la pertenencia al instante cuando agrego o cambio una regla, ¿por qué pasa esto?**<br/>La evaluación de pertenencia dedicada se realiza periódicamente en un proceso asincrónico en segundo plano. ¿Durante cuánto tiempo Hola proceso toma viene determinado por número de Hola de los usuarios de su tamaño hello y directorio de los grupos de hello creado como resultado de la regla de Hola. Por lo general, directorios con un número pequeño de usuarios verán los cambios de pertenencia de grupo de hello en unos pocos minutos. Directorios con un gran número de usuarios pueden tardar 30 minutos o más toopopulate.

### <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
