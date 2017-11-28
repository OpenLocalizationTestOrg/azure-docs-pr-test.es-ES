---
title: "Habilitación de la auditoría y la detección de amenazas en servidores SQL Server en Azure Security Center| Microsoft Docs"
description: "Este documento muestra cómo implementar la recomendación de Azure Security Center ** habilitar auditoría y amenaza para la detección en servidores SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="e050c-103">Habilitación de la auditoría y la detección de amenazas en servidores SQL Server en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e050c-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="e050c-104">Azure Security Center recomienda activar la auditoría y la detección de amenazas en todas las bases de datos de los servidores SQL de Azure, en caso de que no se hayan habilitado aún las auditorías.</span><span class="sxs-lookup"><span data-stu-id="e050c-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="e050c-105">La auditoría y la detección de amenazas pueden ayudarle a mantener el cumplimiento de normativas, conocer la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o violaciones de la seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="e050c-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="e050c-106">Cuando la haya activado, podrá configurar las opciones de Detección de amenazas y los correos electrónicos donde se recibirán alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e050c-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="e050c-107">Detección de amenazas detecta actividades anómalas en la base de datos que indican posibles amenazas de seguridad a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e050c-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="e050c-108">De este modo, podrá detectar posibles amenazas y reaccionar a ellas a medida que se produzcan.</span><span class="sxs-lookup"><span data-stu-id="e050c-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="e050c-109">Esta recomendación solo se aplica en el servicio Azure SQL; no se incluyen las instancias de SQL Server que se ejecutan en las máquinas virtuales de los servicios de infraestructura de Azure (IaaS de Azure).</span><span class="sxs-lookup"><span data-stu-id="e050c-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="e050c-110">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e050c-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="e050c-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="e050c-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e050c-112">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="e050c-112">Implement the recommendation</span></span>
1. <span data-ttu-id="e050c-113">En la hoja **Recomendaciones**, seleccione **Enable Auditing & Threat detection on SQL servers** (Habilitar la auditoría y la detección de amenazas en servidores de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e050c-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="e050c-114">Se abrirá la hoja **Enable Auditing & Threat detection on SQL servers** (Habilitar la auditoría y la detección de amenazas en servidores de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e050c-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Habilitación de la auditoría en servidores SQL][1]
2. <span data-ttu-id="e050c-116">Seleccione un servidor de SQL Server para habilitar la auditoría y la detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="e050c-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="e050c-117">Se abre la hoja **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="e050c-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="e050c-118">En la hoja **Auditoría y detección de amenazas**, seleccione **Activar** en **Auditoría**.</span><span class="sxs-lookup"><span data-stu-id="e050c-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activación de la configuración de auditoría][2]
4. <span data-ttu-id="e050c-120">Siga los pasos del artículo sobre [auditoría de bases de datos SQL en Azure Portal](../sql-database/sql-database-auditing-portal.md) para configurar el almacenamiento donde se guardarán los registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="e050c-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="e050c-121">La cuenta de almacenamiento de la suscripción en la que se recopilarán datos es la predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e050c-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="e050c-122">Siga los pasos de [Introducción a Detección de amenazas de SQL Database](../sql-database/sql-database-threat-detection.md) para activar Detección de amenazas, así como para configurar esta funcionalidad y la lista de correos electrónicos que recibirán alertas de seguridad tras detectarse actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="e050c-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="e050c-123">Consulte también</span><span class="sxs-lookup"><span data-stu-id="e050c-123">See also</span></span>
<span data-ttu-id="e050c-124">En este artículo, se ha mostrado cómo implementar la recomendación de "habilitar la auditoría y la detección de amenazas en servidores de SQL Server".</span><span class="sxs-lookup"><span data-stu-id="e050c-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="e050c-125">Para obtener más información sobre cómo proteger SQL Database, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="e050c-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="e050c-126">Protección de SQL Database</span><span class="sxs-lookup"><span data-stu-id="e050c-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="e050c-127">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="e050c-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e050c-128">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e050c-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e050c-129">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e050c-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e050c-130">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e050c-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e050c-131">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e050c-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e050c-132">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="e050c-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="e050c-133">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="e050c-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e050c-134">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="e050c-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
