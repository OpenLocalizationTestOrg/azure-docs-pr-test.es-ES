---
title: las latencias informes de Active Directory de aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de la cantidad de Hola de tiempo que tarda informando tooshow de eventos en el portal de Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Latencias de informes de Azure Active Directory

Con [reporting](active-directory-preview-explainer.md) en hello Azure Active Directory, se obtiene toda la información de hello necesita toodetermine cómo está haciendo su entorno. cantidad de Hola de tiempo que tarda reporting tooshow datos seguridad Hola portal de Azure es también se denomina latencia. 

En este tema muestra información de latencia de Hola de hello todas las categorías informes en hello portal de Azure. 


## <a name="activity-reports"></a>Informes de actividad

Hay dos áreas de informes de actividad:

- **Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario
- **Registros de auditoría** : información de la actividad del sistema acerca de los usuarios y administración de grupos, sus aplicaciones administradas y actividades de directorio

Hello en la tabla siguiente muestra información de latencia de Hola para los informes de actividad.

| Informe | Mínima | Media | Máxima |
| :-- | --- | --- | --- |
| Registros de auditoría             | 30 minutos  | 45 minutos | 1 hora     |
| Inicios de sesión               | 15 minutos  | 15 minutos | 2 horas*   |

>[!NOTE]
> Para algunos datos de actividad de inicios de sesión procedentes de aplicaciones de office heredado, puede tardar horas too8 Hola informando tooshow de datos. 


## <a name="security-reports"></a>Informes de seguridad

Hay dos áreas de informes de seguridad:

- **Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario. 
- **Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro. 

Hello en la tabla siguiente muestra información de latencia de Hola de informes de seguridad.

| Informe | Mínima | Media | Máxima |
| :-- | --- | --- | --- |
| Usuarios en riesgo          | 5 minutos   | 15 minutos  | 2 horas  |
| Inicios de sesión no seguros         | 5 minutos   | 15 minutos  | 2 horas  |

## <a name="risk-events"></a>Eventos de riesgo

Azure Active Directory utiliza algoritmos y heurística acciones sospechosas toodetect que son cuentas de usuario de tooyour relacionados de aprendizaje de automático adaptable. Cada acción sospechosa detectada se almacena en un registro llamado evento de riesgo.

Hello en la tabla siguiente muestra información de latencia de Hola de eventos de riesgo.

| Informe | Mínima | Media | Máxima |
| :-- | --- | --- | --- |
| Inicios de sesión desde direcciones IP anónimas |5 minutos |15 minutos |2 horas |
| Inicios de sesión desde ubicaciones desconocidas |5 minutos |15 minutos |2 horas |
| Usuarios con credenciales perdidas |2 horas |4 horas |8 horas |
| Viaje imposible tooatypical ubicaciones |5 minutos |1 hora |8 horas  |
| Inicios de sesión desde dispositivos infectados |2 horas |4 horas |8 horas  |
| Inicios de sesión desde direcciones IP con actividad sospechosa |2 horas |4 horas |8 horas  |



## <a name="next-steps"></a>Pasos siguientes

Si desea que tooknow más acerca de los informes de actividad de Hola Hola portal de Azure, vea:

- [Informes de actividad de inicio de sesión en el portal de Azure Active Directory Hola](active-directory-reporting-activity-sign-ins.md)
- [Informes de actividad en el portal de Azure Active Directory Hola de auditoría](active-directory-reporting-activity-audit-logs.md)

Si desea que tooknow más acerca de los informes de seguridad de Hola Hola portal de Azure, vea:

- [Usuarios de informes de seguridad de riesgo en el portal de Azure Active Directory Hola](active-directory-reporting-security-user-at-risk.md)
- [Informe de riesgo de inicios de sesión en el portal de Azure Active Directory Hola](active-directory-reporting-security-risky-sign-ins.md)

Si desea más información acerca de los eventos de riesgo tooknow, consulte [eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).
