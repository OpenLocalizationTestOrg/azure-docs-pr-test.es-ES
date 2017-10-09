---
title: "detección de auditoría y de las amenazas de aaaEnable en los servidores de SQL Server en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** habilitar auditoría y amenaza para la detección en servidores SQL **."
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
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="ab2ce-103">Habilitación de la auditoría y la detección de amenazas en servidores SQL Server en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ab2ce-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="ab2ce-104">Azure Security Center recomienda activar la auditoría y la detección de amenazas en todas las bases de datos de los servidores SQL de Azure, en caso de que no se hayan habilitado aún las auditorías.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="ab2ce-105">La auditoría y la detección de amenazas pueden ayudarle a mantener el cumplimiento de normativas, conocer la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o violaciones de la seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="ab2ce-106">Una vez has activado la auditoría, puede configurar alertas de seguridad de tooreceive de correos electrónicos y configuración de detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="ab2ce-107">La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="ab2ce-108">Esto le permite toodetect y responder toopotential amenazas cuando se producen.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="ab2ce-109">Esta recomendación aplica toohello solo; el servicio de SQL Azure no se incluye SQL Server que se ejecutan en las máquinas virtuales en los servicios de infraestructura de Azure (IaaS de Azure).</span><span class="sxs-lookup"><span data-stu-id="ab2ce-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="ab2ce-110">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="ab2ce-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ab2ce-112">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="ab2ce-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="ab2ce-113">Hola **recomendaciones** hoja, seleccione **habilitar auditoría y amenaza para la detección en servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="ab2ce-114">Se abrirá hello **habilitar auditoría y amenaza para la detección en servidores SQL Server** hoja.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Habilitación de la auditoría en servidores SQL][1]
2. <span data-ttu-id="ab2ce-116">Seleccione esta opción una detección de amenaza y auditoría del tooenable de servidor SQL.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="ab2ce-117">Se abrirá hello **auditoría y la detección de amenazas** hoja.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="ab2ce-118">En hello **auditoría y la detección de amenazas** hoja, seleccione **ON** en **auditoría**.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activación de la configuración de auditoría][2]
4. <span data-ttu-id="ab2ce-120">Siga los pasos de hello en [auditoría de base de datos SQL en el portal de Azure de Hola](../sql-database/sql-database-auditing-portal.md) almacenamiento tooconfigure donde se almacenarán los registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="ab2ce-121">Hola cuenta de almacenamiento de la suscripción para la recopilación de datos es cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="ab2ce-122">Siga los pasos de hello en [empezar a trabajar con la detección de amenazas de base de datos de SQL](../sql-database/sql-database-threat-detection.md) tooturn en y configurar la detección de amenazas y lista de hello tooconfigure de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="ab2ce-123">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ab2ce-123">See also</span></span>
<span data-ttu-id="ab2ce-124">En este artículo se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Habilitar la auditoría y detección de servidores SQL Server de amenazas".</span><span class="sxs-lookup"><span data-stu-id="ab2ce-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="ab2ce-125">toolearn más acerca de cómo proteger la base de datos SQL, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab2ce-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="ab2ce-126">Protección de bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ab2ce-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="ab2ce-127">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab2ce-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ab2ce-128">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ab2ce-129">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ab2ce-130">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ab2ce-131">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ab2ce-132">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ab2ce-133">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ab2ce-134">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2ce-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
