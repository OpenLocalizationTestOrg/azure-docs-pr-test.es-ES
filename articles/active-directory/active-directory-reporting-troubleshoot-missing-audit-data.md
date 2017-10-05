---
title: "Solución de problemas: faltan datos en el registro de actividad de Azure Active Directory | Microsoft Docs"
description: Enumera los distintos informes disponibles para Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="3b33f-103">No encuentro algunas acciones que realicé en el registro de actividad de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b33f-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="3b33f-104">Síntomas</span><span class="sxs-lookup"><span data-stu-id="3b33f-104">Symptoms</span></span>

<span data-ttu-id="3b33f-105">Realice algunas acciones en Azure Portal y esperaba ver los registros de auditoría de dichas acciones en la hoja `Activity logs > Audit Logs`, pero no los encuentro.</span><span class="sxs-lookup"><span data-stu-id="3b33f-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Informes](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="3b33f-107">Causa</span><span class="sxs-lookup"><span data-stu-id="3b33f-107">Cause</span></span>

<span data-ttu-id="3b33f-108">Las acciones no aparecen inmediatamente en el registro de auditoría de la actividad.</span><span class="sxs-lookup"><span data-stu-id="3b33f-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="3b33f-109">Puede tardar entre 15 minutos y una hora para ver los registros de auditoría en el portal a partir del momento en que se realiza la operación.</span><span class="sxs-lookup"><span data-stu-id="3b33f-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="3b33f-110">Resolución</span><span class="sxs-lookup"><span data-stu-id="3b33f-110">Resolution</span></span>

<span data-ttu-id="3b33f-111">Espere entre 15 minutos y una hora para ver si las acciones aparecen en el registro.</span><span class="sxs-lookup"><span data-stu-id="3b33f-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="3b33f-112">Si sigue sin verlas, genere una incidencia de soporte técnico y examinaremos el problema.</span><span class="sxs-lookup"><span data-stu-id="3b33f-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b33f-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b33f-113">Next steps</span></span>
<span data-ttu-id="3b33f-114">Consulte [Preguntas más frecuentes sobre informes de Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3b33f-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>
