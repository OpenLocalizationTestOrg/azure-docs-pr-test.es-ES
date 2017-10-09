---
title: informes de Active Directory de aaaAzure | Documentos de Microsoft
description: "Proporciona una visión general sobre los informes de Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Informes de Azure Active Directory

Con los informes de Azure Active Directory, puede obtener información sobre el funcionamiento de su entorno.  
datos de Hello proporciona le permiten:

- Determinar cómo utilizan los usuarios las aplicaciones y servicios
- Detectar riesgos potenciales que afectan a estado de saludo del entorno
- Solucionar problemas que impiden a los usuarios finalizar su trabajo  

arquitectura de los informes Hola se basa en dos pilares principales:

- Informes de seguridad
- Informes de actividad

![Informes](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Informes de seguridad

informes de seguridad de Hello en Azure Active Directory le ayudan a tooprotect las identidades de su organización.  
Hay dos tipos de informes de seguridad en Azure Active Directory:

- **Usuarios marcan para su riesgo** : en hello [usuarios marcan para el informe de seguridad de riesgo](active-directory-reporting-security-user-at-risk.md), obtener una visión general de las cuentas de usuario que podrían haberse visto comprometidos.

- **Inicios de sesión arriesgados** : con hello [informe de seguridad de inicio de sesión arriesgado](active-directory-reporting-security-risky-sign-ins.md), obtendrá un indicador de intentos de inicio de sesión que podrían haber realizado alguna persona no Hola legítimo propietario de una cuenta de usuario. 

**¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?**  
Todas las ediciones de Azure Active Directory le proporcionan estos informes sobre usuarios marcados en riesgo e inicios de sesión de riesgo.  
Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola: 

- Hola **ediciones Azure Active Directory Free y Basic**, ya obtener una lista de usuarios marcados para su riesgo y el riesgo de inicios de sesión. 

- Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe. 

- Hola **Azure Active Directory Premium 2** edition proporciona con hello más información detallada acerca de hello subyacente eventos de riesgo y también permite las directivas de seguridad de tooconfigure que responden automáticamente tooconfigured niveles de riesgo.


## <a name="activity-reports"></a>Informes de actividad

Hay dos tipos de informes de actividad en Azure Active Directory:

- **Registros de auditoría** : hello [informe de actividad de los registros de auditoría](active-directory-reporting-activity-audit-logs.md) proporciona toohello de acceder al historial de cada tarea lleva a cabo en el inquilino.

- **Inicios de sesión** : con hello [informe de actividad de inicios de sesión](active-directory-reporting-activity-sign-ins.md), puede determinar, que ha realizado las tareas de hello notificadas por informe de registros de auditoría de Hola.



Hola **informe de registros de auditoría** proporciona registros de actividades de sistema de cumplimiento de normas.
Entre otras cosas, Hola proporciona datos permiten escenarios comunes de tooaddress como:

- Alguien en mi inquilino obtuviera un grupo de administración de acceso tooan. ¿Quién les dio acceso? 

- Hola tooknow una lista de los usuarios iniciar sesión en una aplicación específica desde I recientemente incorporado Hola aplicación y desea tooknow si está realizando correctamente

- Deseo tooknow contraseña cuántos restablecimientos se producen en mi inquilino


**¿Qué licencia de Azure AD necesita informe de registros de auditoría de hello tooaccess?**  
informe de registros de auditoría de Hello está disponible para características para los que tiene licencias. Si tiene una licencia para una característica específica, también tiene acceso toohello auditar la información de registro para ella.

Para obtener más información, consulte **comparar características disponibles con carácter general de las ediciones Free, Basic y Premium hello** en [capacidades y características de Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Hola **informe de actividad de inicios de sesión** tootoofind habilita responde tooquestions como:

- ¿Qué es el patrón de inicio de sesión de Hola de un usuario?
- ¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?
- ¿Cuál es el estado de Hola de estos inicios de sesión?


**¿Realice la licencia de Azure AD necesita tooaccess Hola informe de actividad de inicios de sesión?**  
tooaccess Hola informe de actividad de inicios de sesión, el inquilino debe tener una licencia de Azure AD Premium asociada a él.


## <a name="programmatic-access"></a>Acceso mediante programación

En la interfaz de usuario de suma toohello, reporting de Azure Active Directory también ofrece [acceso mediante programación](active-directory-reporting-api-getting-started-azure-portal.md) toohello datos de informes. datos de Hola de estos informes pueden ser muy útil tooyour aplicaciones, como sistemas SIEM, auditoría y herramientas de business intelligence. Hello Azure AD reporting que API proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST. Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas. 


## <a name="next-steps"></a>Pasos siguientes

Si desea más información acerca de hello tooknow distintos tipos de informe en Azure Active Directory, consulte:

- [Informe de usuarios marcados en riesgo](active-directory-reporting-security-user-at-risk.md)
- [Informe de inicios de sesión de riesgo](active-directory-reporting-security-risky-sign-ins.md)
- [Informe de registros de auditoría](active-directory-reporting-activity-audit-logs.md)
- [Informe de registros de inicios de sesión](active-directory-reporting-activity-sign-ins.md)

Si desea que tooknow más acerca del acceso a Hola Hola Hola API de informes de uso de datos de informes, vea: 

- [Introducción a hello Azure Active Directory API de informes](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png