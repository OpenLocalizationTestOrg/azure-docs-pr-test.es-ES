---
title: aaaUsers marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Obtenga información acerca de los usuarios de hello marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Usuarios marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola

Con informes de seguridad de hello en hello Azure Active Directory (Azure AD), puede obtener información sobre la probabilidad de Hola de cuentas de usuario en peligro en su entorno. 

Azure Active Directory detecta acciones sospechosas que son cuentas de usuario de tooyour relacionados. Para cada acción detectada, se crea un registro denominado *evento de riesgo*. Para más información, consulte [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hola detectó que los eventos de riesgo son toocalculate usado:

- **Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario. Para más información, consulte [Inicios de sesión no seguros](active-directory-identityprotection.md#risky-sign-ins). 

- **Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro. Para más información, consulte [Usuarios marcados en riesgo](active-directory-identityprotection.md#users-flagged-for-risk).  

Hola portal de Azure, puede encontrar seguridad Hola informa sobre hello **Azure Active Directory** hoja en hello **seguridad** sección.  

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?  

Todas las ediciones de Azure Active Directory le proporcionan estos informes sobre usuarios marcados en riesgo.  
Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola: 

- Hola **ediciones Azure Active Directory Free y Basic**, ya obtener una lista de usuarios marcados para su riesgo. 

- Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe. 

- Hola **Azure Active Directory Premium 2** edition proporciona información más detallada sobre todos los eventos de riesgo subyacente de Hola y le permite tooconfigure las directivas de seguridad que responden automáticamente tooconfigured riesgo niveles.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edición gratuita y básica de Azure Active Directory

usuarios Hola marcados para su informe de riesgo en las ediciones gratuitas y básicas de Azure Active Directory Hola proporciona una lista de cuentas de usuario que se han comprometido. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/03.png)

Si se selecciona un usuario abre una hoja de datos de usuario relacionada de Hola.
Para los usuarios que están en riesgo, puede revisar el historial de inicio de sesión del usuario de Hola y restablecer la contraseña de hello si es necesario.

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/46.png)


Este cuadro de diálogo proporciona una opción para:

- Descargar informe Hola

- Búsqueda de usuarios

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Ediciones Azure Active Directory Premium

usuarios Hola marcados para su informe de riesgo en las ediciones premium de Azure Active Directory Hola proporciona:

- Una [lista de cuentas de usuario](active-directory-identityprotection.md#users-flagged-for-risk) que podrían estar en peligro 

- Agrega información sobre hello [el riesgo de tipos de evento](active-directory-identity-protection-risk-events.md) que se han detectado

- Un informe de opción toodownload Hola

- Una opción tooconfigure un [directiva de corrección de riesgo de usuario](active-directory-identityprotection.md#user-risk-security-policy)  


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/71.png)

Cuando selecciona un usuario, obtiene una vista detallada del informe para este usuario que le permite:

- Abra Hola que ver todos los inicios de sesión

- Restablecer la contraseña del usuario de Hola

- Descartar todos los eventos

- Investigue los eventos de riesgo incluido para el usuario de Hola. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate un evento de riesgo, seleccione uno de Hola de hello lista tooopen **detalles** hoja para este evento de riesgo. En hello **detalles** hoja, tiene Hola opción tooeither [cerrar manualmente un evento de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o volver a activar un evento de riesgo cerrado manualmente. 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Pasos siguientes

- Para más información acerca de Azure Active Directory Identity Protection, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

