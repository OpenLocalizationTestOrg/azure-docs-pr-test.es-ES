---
title: "Solución de problemas: Los datos que faltan en hello descargan registros de actividad de Azure Active Directory | Documentos de Microsoft"
description: "Proporciona datos toomissing resolución en los registros de actividad de Azure Active Directory descargados."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>No se encuentra ningún dato en los registros de actividad de Azure Active Directory Hola que he descargado


## <a name="symptoms"></a>Síntomas

Descargar los registros de actividad de hello (auditoría o inicios de sesión) y no veo todos los registros de Hola por vez Hola que deseaba. ¿Por qué? 

 ![Informes](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Causa

Al descargar los registros de actividad de hello portal de Azure, limitamos Hola escala too120K registros ordenados más reciente. 

## <a name="resolution"></a>Resolución

Puede aprovechar [API de informes de Azure AD](active-directory-reporting-api-getting-started.md) toofetch tooa millones de registros en un momento determinado. Nuestro enfoque recomendado es toorun una secuencia de comandos según una programación que llama Hola informes API toofetch registra de forma incremental durante un período de tiempo (p. ej., diaria o semanal).

## <a name="next-steps"></a>Pasos siguientes
Vea hello [Azure Active Directory reporting preguntas más frecuentes sobre](active-directory-reporting-faq.md).

