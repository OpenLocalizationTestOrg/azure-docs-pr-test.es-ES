---
title: "informe de inicios de sesión de aaaRisky en el portal de Azure Active Directory Hola | Documentos de Microsoft"
description: "Obtenga información acerca de informes de riesgo de inicios de sesión de hello en el portal de Azure Active Directory de Hola"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Informe de riesgo de inicios de sesión en el portal de Azure Active Directory Hola

Con los informes de seguridad de hello en Azure Active Directory (Azure AD) puede obtener información sobre probabilidad Hola de cuentas de usuario en peligro en su entorno. 

Azure AD detecta acciones sospechosas que son cuentas de usuario de tooyour relacionados. Para cada acción detectada, se crea un registro denominado *evento de riesgo*. Para más información, consulte [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventos de riesgo de Azure Active Directory). 

Hola detectó que los eventos de riesgo son toocalculate usado:

- **Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario. Para más información, consulte la sección sobre los [inicios de sesión peligrosos](active-directory-identityprotection.md#risky-sign-ins). 

- **Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro. Para más información, consulte la sección sobre los [usuarios marcados en riesgo](active-directory-identityprotection.md#users-flagged-for-risk).  

En [Hola portal de Azure](https://portal.azure.com), puede encontrar la seguridad de hello informes en hello **Azure Active Directory** hoja en hello **seguridad** sección. 

![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?  

Todas las ediciones de Azure Active Directory le proporcionan informes sobre inicios de sesión de riesgo.  
Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola: 

- Hola **ediciones Azure Active Directory Free y Basic**, ya que se obtiene una lista de inicios de sesión de riesgos. 

- Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe. 

- Hola **Azure Active Directory Premium 2** edition proporciona con hello más información detallada acerca de todos los eventos de riesgo subyacentes y también permite las directivas de seguridad de tooconfigure que responden automáticamente tooconfigured niveles de riesgo.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edición gratuita y básica de Azure Active Directory

Hello Azure Active Directory libre y ediciones básicas proporcionan una lista de riesgos-inicios de sesión que se han detectado para los usuarios. Este informe muestra:

- **Usuario** : hello nombre de usuario de Hola que se usó durante la operación de inicio de sesión de Hola
- **IP** -Hola dirección IP del dispositivo de Hola que estaba tooAzure tooconnect usa Active Directory
- **Ubicación** -ubicación de hello usa tooconnect tooAzure Active Directory
- **Hora de inicio de sesión** -Hola hora de inicio de sesión de Hola
- **Estado** -Hola estado del inicio de sesión de Hola


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Según la investigación de inicio de sesión arriesgado en hello, puede proporcionar comentarios tooAzure Active Directory en forma de hello siguientes acciones:

- Resolver
- Marcar como falso positivo
- Ignorar
- Reactivar

![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Para más información, consulte [Cierre manual de eventos de riesgo](active-directory-identityprotection.md#closing-risk-events-manually).

Este informe proporciona una opción para:

- Buscar recursos
- Descargar datos de informe de Hola


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Ediciones Azure Active Directory Premium

informe de inicios de sesión arriesgado Hello en las ediciones premium de Azure Active Directory Hola proporciona:

- Agrega información sobre hello [el riesgo de tipos de evento](active-directory-identity-protection-risk-events.md) que se han detectado

- Un informe de opción toodownload Hola


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Cuando selecciona un evento de riesgo, obtiene una vista detallada del informe para este evento de riesgo que le permite:

- Una opción tooconfigure un [directiva de corrección de riesgo de usuario](active-directory-identityprotection.md#user-risk-security-policy)  

- Revise la escala de tiempo de detección de Hola para eventos de riesgo de Hola  

- Revisar una lista de usuarios para los que se ha detectado este evento de riesgo

- [Cerrar manualmente los eventos de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o reactivar un evento de riesgo cerrado manualmente. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Cuando selecciona un usuario, obtiene una vista detallada del informe para este usuario que le permite:

- Abra Hola que ver todos los inicios de sesión

- Restablecer la contraseña del usuario de Hola

- Descartar todos los eventos

- Investigue los eventos de riesgo incluido para el usuario de Hola. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate un evento de riesgo, seleccione uno de la lista de Hola.  
Se abrirá hello **detalles** hoja para este evento de riesgo. En hello **detalles** hoja, tiene Hola opción tooeither [cerrar manualmente un evento de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o volver a activar un evento de riesgo cerrado manualmente. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Pasos siguientes

- Para más información acerca de Azure Active Directory Identity Protection, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

