---
title: "bases de datos de detección de auditoría y de las amenazas de aaaEnable en SQL en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** habilitar la detección de auditoría y de las amenazas en las bases de datos SQL **."
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="01cf0-103">Habilitación de la auditoría y la detección de amenazas en bases de datos SQL en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="01cf0-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="01cf0-104">Azure Security Center recomienda activar la auditoría y la detección de amenazas en todas las bases de datos SQL, en caso de que no se hayan habilitado aún las auditorías.</span><span class="sxs-lookup"><span data-stu-id="01cf0-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="01cf0-105">La auditoría y la detección de amenazas pueden ayudarle a mantener el cumplimiento de normativas, conocer la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o violaciones de la seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="01cf0-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="01cf0-106">Una vez has activado la auditoría, puede configurar alertas de seguridad de tooreceive de correos electrónicos y configuración de detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="01cf0-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="01cf0-107">La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales.</span><span class="sxs-lookup"><span data-stu-id="01cf0-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="01cf0-108">Esto le permite toodetect y responder toopotential amenazas cuando se producen.</span><span class="sxs-lookup"><span data-stu-id="01cf0-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="01cf0-109">Esta recomendación aplica toohello solo; el servicio de SQL Azure no se incluye con las máquinas virtuales SQL.</span><span class="sxs-lookup"><span data-stu-id="01cf0-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="01cf0-110">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="01cf0-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="01cf0-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="01cf0-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="01cf0-112">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="01cf0-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="01cf0-113">Hola **recomendaciones** hoja, seleccione **habilitar auditoría y amenaza para la detección en las bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="01cf0-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="01cf0-114">Se abrirá hello **habilitar auditoría y amenaza para la detección en las bases de datos SQL** hoja.</span><span class="sxs-lookup"><span data-stu-id="01cf0-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Habilitación de la auditoría en bases de datos SQL][1]
2. <span data-ttu-id="01cf0-116">Seleccione una auditoría de tooenable de base de datos SQL en.</span><span class="sxs-lookup"><span data-stu-id="01cf0-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="01cf0-117">Se abrirá hello **auditoría y la detección de amenazas** hoja.</span><span class="sxs-lookup"><span data-stu-id="01cf0-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="01cf0-118">En hello **auditoría y la detección de amenazas** hoja, seleccione **ON** en **auditoría**.</span><span class="sxs-lookup"><span data-stu-id="01cf0-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Activación de la detección de amenazas y auditoría][2]
4. <span data-ttu-id="01cf0-120">Siga los pasos de hello en [detección de amenazas de base de datos de SQL en el portal de Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn en y configurar la detección de amenazas y lista de hello tooconfigure de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="01cf0-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="01cf0-121">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="01cf0-121">See also</span></span>
<span data-ttu-id="01cf0-122">En este artículo se ha mostrado cómo tooimplement Hola centro de seguridad recomendación "Habilitar auditoría & amenaza para la detección en las bases de datos SQL".</span><span class="sxs-lookup"><span data-stu-id="01cf0-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="01cf0-123">toolearn más acerca de cómo proteger la base de datos SQL, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="01cf0-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="01cf0-124">Protección de bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="01cf0-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="01cf0-125">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="01cf0-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="01cf0-126">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="01cf0-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="01cf0-127">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="01cf0-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="01cf0-128">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="01cf0-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="01cf0-129">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="01cf0-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="01cf0-130">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="01cf0-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="01cf0-131">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="01cf0-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="01cf0-132">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="01cf0-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
