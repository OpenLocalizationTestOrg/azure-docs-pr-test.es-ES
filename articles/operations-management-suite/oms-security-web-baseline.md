---
title: "aaaOperations Management Suite seguridad y auditoría solución Web previsto | Documentos de Microsoft"
description: "Este documento se explica cómo toouse OMS seguridad y auditoría solución tooperform una evaluación de la línea de base de web de todos los servidores web supervisados para el propósito de seguridad y cumplimiento."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="0a6fb-103">Evaluación de línea de base web en la solución Security and Audit de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="0a6fb-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="0a6fb-104">Este documento le ayuda a toouse [Operations Management Suite (OMS) solución de seguridad y auditoría](operations-management-suite-overview.md) web capacidades tooaccess Hola estado seguro de los recursos supervisados de evaluación de línea de base.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="0a6fb-105">¿Qué es la evaluación de línea de base web?</span><span class="sxs-lookup"><span data-stu-id="0a6fb-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="0a6fb-106">Actualmente, Seguridad de OMS proporciona una evaluación de línea de base de seguridad para sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="0a6fb-107">Analiza la configuración del sistema operativo Hola de los servidores de cada 24 horas y proporciona una vista a la configuración de potencialmente vulnerable.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="0a6fb-108">Consulte [Evaluación de línea base en la solución Security and Audit de Operations Management Suite](oms-security-baseline.md) para más información sobre esto.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="0a6fb-109">objetivo de Hola de evaluación de línea de base de hello web es la configuración del servidor de web potencialmente vulnerable toofind.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="0a6fb-110">Hola tres fuentes principales para las configuraciones de línea de base de hello web: configuración. NET, ASP.NET e IIS.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="0a6fb-111">Simplemente como hello evaluación de línea de base del sistema operativo, seguridad de OMS se va tooscan sus servidores web cada 24 horas y proporcionan una vista de estado de seguridad de ellos.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="0a6fb-112">En los servicios de Internet Information Server (IIS), las configuraciones son personalizables, que permite varias toobe de niveles de sitio y la aplicación se reemplaza.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="0a6fb-113">Analizador de Hello comprueba la configuración de hello en cada nivel de aplicación o el sitio de nivel de raíz de suma toohello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="0a6fb-114">Esto ayuda a ubicaciones de configuración de una vulnerabilidad potencial tooidentify y corregir rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="0a6fb-115">Evaluación de línea de base de seguridad web</span><span class="sxs-lookup"><span data-stu-id="0a6fb-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="0a6fb-116">De esta versión preliminar esta característica va toobe acceso mediante la opción de búsqueda de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="0a6fb-117">Siga los pasos de hello debajo de consulta de hello apropian tooperform:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="0a6fb-118">Hola **Microsoft Operations Management Suite** panel principal haga clic en **seguridad y auditoría** icono.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="0a6fb-119">Hola **seguridad y auditoría** panel, haga clic en **Log Search** botón.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="0a6fb-120">Hola primera consulta, que puede utilizar es hello **Web Resumen de la evaluación de línea de base**.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="0a6fb-121">Hola **empieza la búsqueda aquí** , escriba esta consulta: tipo*= SecurityBaselineSummary BaselineType = web*.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="0a6fb-122">Hola después de la pantalla tiene un ejemplo de salida:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-122">hello following screen has an output sample:</span></span>

![Resumen de evaluación de línea de base web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="0a6fb-124">En esta consulta, cada registro indica el resumen de evaluación para un solo servidor.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="0a6fb-125">Una vez que esté en hello **Log Search**, puede escribir consultas diferentes tooobtain obtener más información acerca de la evaluación de línea de base de hello web.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="0a6fb-126">Además toohello consulta anterior, también sirve Hola los en esta versión preliminar siguiendo.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="0a6fb-127">**Web Baseline Rule Assessment** (Evaluación de regla de la línea de base web): cada registro representa una sola evaluación de regla de la línea de base web en un único servidor.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="0a6fb-128">Incluye todos los datos de la regla de hello, ubicación, resultado de hello esperada y resultado real de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="0a6fb-129">**Consulta**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="0a6fb-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Evaluación de regla de la línea de base web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="0a6fb-131">**Mostrar todos los resultados de un servidor específico**: esta consulta muestra cómo toosee da como resultado de un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="0a6fb-132">**Consulta**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="0a6fb-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Todos los resultados](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="0a6fb-134">También puede utilizar estos registros y consultas toocreate sus propios paneles, informes o alertas.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="0a6fb-135">pantalla de bienvenida a continuación tiene un control de interfaz de usuario de ejemplo que se puede agregar panel tooyour.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="0a6fb-136">Puede obtener información sobre cómo toovisualize los datos mediante el Diseñador de vistas de OMS [aquí](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="0a6fb-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="0a6fb-137">pantalla de bienvenida siguiente es un ejemplo de cómo icono Hola será similar a una vez realizada esta personalización.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Ejemplo de interfaz de usuario](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="0a6fb-139">Si desea que los valores de hello tooknow que se comprueban para la evaluación de la línea de base de hello, puede descargar [esta hoja de cálculo de Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) que contenga esta configuración.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="0a6fb-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0a6fb-140">See also</span></span>
<span data-ttu-id="0a6fb-141">En este documento, ha aprendido acerca de la evaluación de línea de base web de Seguridad y auditoría de OMS.</span><span class="sxs-lookup"><span data-stu-id="0a6fb-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="0a6fb-142">toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="0a6fb-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="0a6fb-143">Información general de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="0a6fb-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="0a6fb-144">Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría</span><span class="sxs-lookup"><span data-stu-id="0a6fb-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="0a6fb-145">Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="0a6fb-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

