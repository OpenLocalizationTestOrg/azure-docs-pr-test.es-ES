---
title: "Directivas de retención de informes de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Directivas de retención de informes de Azure Active Directory


Este tema proporciona respuestas a las preguntas más frecuentes en relación a la retención de datos de los distintos informes de actividad de Azure Active Directory. 

**P: ¿Cómo puede empezar la recopilación de datos de actividad?**

**R:**

| Edición de Azure AD | Inicio de la recopilación |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Al suscribirse a una suscripción |
| Azure AD Free | La primera vez que abra la [hoja de Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o use las [API de informes](https://aka.ms/aadreports)  |

---
**P: ¿Cuándo estarán disponibles los datos de actividad en Azure Portal?**

**R:**

- **Inmediatamente**: si ya ha estado trabajando con informes en el Portal de Azure clásico
- **Dentro de 2 horas**: si no ha activado la generación de informes en el Portal de Azure clásico

---
**P: ¿Cómo puede empezar la recopilación de señales de seguridad?**  

**R:** En el caso de las señales de seguridad, el proceso de recopilación se inicia cuando decide usar Identity Protection Center. 


---
**P: ¿Durante cuánto tiempo se almacenan los datos recopilados?**

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