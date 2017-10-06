---
title: aaaUnlicensed informe de uso | Documentos de Microsoft
description: "Hola informes de uso sin licencia ayuda a que identificar a los usuarios sin licencia que usan características de Azure AD de pago."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Informe de uso sin licencia
Hola informes de uso sin licencia ayuda a que identificar a los usuarios sin licencia que usan características de Azure AD de pago. Esto le permite toomake un mejor uso de licencias que ha adquirido y tooidentify sabrá cuando necesite obtener licencias adicionales. 

informe de Hello muestra el uso de activo de hello características de pago en hello últimos 30 días. 

## <a name="report-structure"></a>Estructura del informe
| Nombre de la columna | Descripción |
|:--- |:--- |
| Usuario sin licencia |Nombre de usuario de Hola |
| Característica |nombre de la característica de Hola. Por ejemplo: acceso condicional |
| Aplicación a la que se accede |nombre de Hola de aplicación Hola que se tiene acceso con la característica de Hola. Por ejemplo: Office 365 SharePoint Online |

> [!NOTE]
> Si se ha eliminado una cuenta de usuario Hola 'Sin licencia User' columna se rellenará con el identificador, como 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Características de acceso condicional
A los usuarios sin licencia se les marcará cuando accedan a un servicio al que se haya aplicado la directiva de acceso condicional, siempre que no tengan una licencia de Azure AD Premium. 

Esto aplica tooMFA / directivas de ubicación, así como dispositivo directivas que usar Intune.

## <a name="see-also"></a>Otras referencias
* [Protección del acceso a Office 365 y otras aplicaciones conectadas a Azure Active Directory](active-directory-conditional-access.md)
* [Introducción a acceso condicional tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

