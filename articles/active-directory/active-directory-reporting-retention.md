---
title: "directivas de retención de informes de Active Directory aaaAzure | Documentos de Microsoft"
description: "Directivas de retención de datos de informes en Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Directivas de retención de informes de Azure Active Directory


Este tema proporciona respuestas toohello preguntas más frecuentes junto con la retención de datos de Hola para los informes de actividad diferente de hello en Azure Active Directory. 

**P: ¿cómo se puede obtener colección Hola de datos de la actividad iniciar?**

**R:**

| Edición de Azure AD | Inicio de la recopilación |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Al suscribirse a una suscripción |
| Azure AD Free | Hola la primera vez que abra hello [hoja de Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o usar hello [reporting API](https://aka.ms/aadreports)  |

---
**P: ¿cuándo está disponible en hello portal de Azure los datos de actividad?**

**R:**

- **Inmediatamente** : si ya ha estado trabajando con informes en hello portal de Azure clásico
- **Dentro de 2 horas** : si no has activado reporting Hola portal de Azure clásico

---
**P: ¿cómo se puede obtener colección de Hola de señales de seguridad inició?**  

**R:** señales de seguridad, el proceso de recopilación de Hola se inicia cuando se participación en el centro de protección de identidad de toouse Hola. 


---
**P: ¿por cuánto tiempo es Hola almacenados los datos recopilados?**

**R:**

**Informes de actividad**    

| Informe                 | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Auditoría de directorio        | 7 días        | 30 días             | 30 días             |
| Actividad de inicio de sesión       | 7 días        | 30 días             | 30 días             |

**Señales de seguridad**

| Informe         | Azure AD Free | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Usuarios en riesgo  | 7 días        | 30 días             | 90 días             |
| Inicios de sesión no seguros | 7 días        | 30 días             | 90 días             |

---