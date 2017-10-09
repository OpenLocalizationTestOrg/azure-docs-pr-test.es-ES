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
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="adec6-103">No se encuentra ningún dato en los registros de actividad de Azure Active Directory Hola que he descargado</span><span class="sxs-lookup"><span data-stu-id="adec6-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="adec6-104">Síntomas</span><span class="sxs-lookup"><span data-stu-id="adec6-104">Symptoms</span></span>

<span data-ttu-id="adec6-105">Descargar los registros de actividad de hello (auditoría o inicios de sesión) y no veo todos los registros de Hola por vez Hola que deseaba.</span><span class="sxs-lookup"><span data-stu-id="adec6-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="adec6-106">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="adec6-106">Why?</span></span> 

 ![Informes](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="adec6-108">Causa</span><span class="sxs-lookup"><span data-stu-id="adec6-108">Cause</span></span>

<span data-ttu-id="adec6-109">Al descargar los registros de actividad de hello portal de Azure, limitamos Hola escala too120K registros ordenados más reciente.</span><span class="sxs-lookup"><span data-stu-id="adec6-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="adec6-110">Resolución</span><span class="sxs-lookup"><span data-stu-id="adec6-110">Resolution</span></span>

<span data-ttu-id="adec6-111">Puede aprovechar [API de informes de Azure AD](active-directory-reporting-api-getting-started.md) toofetch tooa millones de registros en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="adec6-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="adec6-112">Nuestro enfoque recomendado es toorun una secuencia de comandos según una programación que llama Hola informes API toofetch registra de forma incremental durante un período de tiempo (p. ej., diaria o semanal).</span><span class="sxs-lookup"><span data-stu-id="adec6-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="adec6-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="adec6-113">Next steps</span></span>
<span data-ttu-id="adec6-114">Vea hello [Azure Active Directory reporting preguntas más frecuentes sobre](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="adec6-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

