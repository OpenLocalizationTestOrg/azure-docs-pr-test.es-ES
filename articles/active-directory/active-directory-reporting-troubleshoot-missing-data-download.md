---
title: "Solución de problemas: faltan datos en los registros de actividad de Azure Active Directory descargados | Microsoft Docs"
description: "Proporciona una solución para los datos que faltan en los registros de actividad de Azure Active Directory descargados."
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
ms.openlocfilehash: 3d56f89035da4d1a0074256b165663f81fc2b01e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="912bd-103">No encuentro datos en los registros de actividad de Azure Active Directory que he descargado</span><span class="sxs-lookup"><span data-stu-id="912bd-103">I can’t find any data in the Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="912bd-104">Síntomas</span><span class="sxs-lookup"><span data-stu-id="912bd-104">Symptoms</span></span>

<span data-ttu-id="912bd-105">Descargue los registros de actividad (auditoría o inicios de sesión) y no veo todos los registros del tiempo que elegí.</span><span class="sxs-lookup"><span data-stu-id="912bd-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="912bd-106">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="912bd-106">Why?</span></span> 

 ![Informes](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="912bd-108">Causa</span><span class="sxs-lookup"><span data-stu-id="912bd-108">Cause</span></span>

<span data-ttu-id="912bd-109">Al descargar los registros de actividad en Azure Portal, limitamos la escala a 120 000 registros, ordenados por antigüedad.</span><span class="sxs-lookup"><span data-stu-id="912bd-109">When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="912bd-110">Resolución</span><span class="sxs-lookup"><span data-stu-id="912bd-110">Resolution</span></span>

<span data-ttu-id="912bd-111">Puede sacar provecho de la [API de creación de informes de Azure AD](active-directory-reporting-api-getting-started.md) para capturar hasta un millones de registros en cualquier momento dado.</span><span class="sxs-lookup"><span data-stu-id="912bd-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="912bd-112">Nuestro enfoque recomendado es ejecutar de forma programada un script que llame a las API de creación de informes para capturar registros de forma incremental durante un período de tiempo (p. ej., a diario o semanalmente).</span><span class="sxs-lookup"><span data-stu-id="912bd-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="912bd-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="912bd-113">Next steps</span></span>
<span data-ttu-id="912bd-114">Consulte [Preguntas más frecuentes sobre informes de Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="912bd-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

