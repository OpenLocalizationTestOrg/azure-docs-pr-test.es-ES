---
title: "Habilitación de las auditorías y la detección de amenazas en bases de datos de SQL Server en Azure Security Center| Microsoft Docs"
description: "Este documento muestra cómo implementar la recomendación de Azure Security Center ** habilitar la detección de auditoría y de las amenazas en las bases de datos SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="b40f2-103">Habilitación de la auditoría y la detección de amenazas en bases de datos SQL en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b40f2-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="b40f2-104">Azure Security Center recomienda activar la auditoría y la detección de amenazas en todas las bases de datos SQL, en caso de que no se hayan habilitado aún las auditorías.</span><span class="sxs-lookup"><span data-stu-id="b40f2-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="b40f2-105">La auditoría y la detección de amenazas pueden ayudarle a mantener el cumplimiento de normativas, conocer la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o violaciones de la seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="b40f2-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="b40f2-106">Cuando la haya activado, podrá configurar las opciones de Detección de amenazas y los correos electrónicos donde se recibirán alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b40f2-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="b40f2-107">Detección de amenazas detecta actividades anómalas en la base de datos que indican posibles amenazas de seguridad a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b40f2-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="b40f2-108">De este modo, podrá detectar posibles amenazas y reaccionar a ellas a medida que se produzcan.</span><span class="sxs-lookup"><span data-stu-id="b40f2-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="b40f2-109">Esta recomendación se aplica solo al servicio de SQL de Azure; no incluye al servicio SQL que se ejecuta en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b40f2-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="b40f2-110">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b40f2-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b40f2-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="b40f2-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="b40f2-112">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="b40f2-112">Implement the recommendation</span></span>
1. <span data-ttu-id="b40f2-113">En la hoja **Recomendaciones**, seleccione **Enable Auditing & Threat detection on SQL databases** (Habilitar la auditoría y la detección de amenazas en bases de datos SQL).</span><span class="sxs-lookup"><span data-stu-id="b40f2-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="b40f2-114">Se abrirá la hoja **Enable Auditing & Threat detection on SQL databases** (Habilitar la auditoría y la detección de amenazas en bases de datos SQL).</span><span class="sxs-lookup"><span data-stu-id="b40f2-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Habilitación de la auditoría en bases de datos SQL][1]
2. <span data-ttu-id="b40f2-116">Seleccione una base de datos SQL en donde habilitar la auditoría.</span><span class="sxs-lookup"><span data-stu-id="b40f2-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="b40f2-117">Se abre la hoja **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="b40f2-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="b40f2-118">En la hoja **Auditoría y detección de amenazas**, seleccione **Activar** en **Auditoría**.</span><span class="sxs-lookup"><span data-stu-id="b40f2-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activación de la detección de amenazas y auditoría][2]
4. <span data-ttu-id="b40f2-120">Siga los pasos de [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) (Detección de amenazas de SQL Database en Azure Portal) para activar Detección de amenazas, así como para configurar esta funcionalidad y la lista de correos electrónicos que recibirán alertas de seguridad tras detectarse actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="b40f2-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="b40f2-121">Consulte también</span><span class="sxs-lookup"><span data-stu-id="b40f2-121">See also</span></span>
<span data-ttu-id="b40f2-122">En este artículo, se ha mostrado cómo implementar la recomendación de "habilitar la auditoría y la detección de amenazas en bases de datos SQL".</span><span class="sxs-lookup"><span data-stu-id="b40f2-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="b40f2-123">Para obtener más información sobre cómo proteger SQL Database, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="b40f2-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="b40f2-124">Protección de SQL Database</span><span class="sxs-lookup"><span data-stu-id="b40f2-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="b40f2-125">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="b40f2-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="b40f2-126">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b40f2-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b40f2-127">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b40f2-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b40f2-128">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b40f2-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b40f2-129">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b40f2-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b40f2-130">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="b40f2-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="b40f2-131">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="b40f2-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b40f2-132">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="b40f2-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
