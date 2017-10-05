---
title: "Seguridad de datos de la solución Seguridad y auditoría de Operations Management Suite | Microsoft Docs"
description: "En este documento se explica cómo se administran y protegen los datos en la solución Seguridad y auditoría de Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="75f28-103">Seguridad de datos de la solución Seguridad y auditoría de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="75f28-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="75f28-104">Para ayudar a los clientes a evitar, detectar y responder a amenazas, la [solución Seguridad y auditoría de Operations Management Suite (OMS)](operations-management-suite-overview.md) recopila y procesa los datos sobre los recursos, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="75f28-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="75f28-105">Registro de eventos de seguridad</span><span class="sxs-lookup"><span data-stu-id="75f28-105">Security event log</span></span>
* <span data-ttu-id="75f28-106">Eventos de Seguimiento de eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="75f28-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="75f28-107">Eventos de auditoría de AppLocker</span><span class="sxs-lookup"><span data-stu-id="75f28-107">AppLocker auditing events</span></span>
* <span data-ttu-id="75f28-108">Registro de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="75f28-108">Windows Firewall log</span></span>
* <span data-ttu-id="75f28-109">Eventos de Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="75f28-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="75f28-110">Resultados de evaluación de la línea base</span><span class="sxs-lookup"><span data-stu-id="75f28-110">Results of baseline assessment</span></span>
* <span data-ttu-id="75f28-111">Resultados de evaluación de antimalware</span><span class="sxs-lookup"><span data-stu-id="75f28-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="75f28-112">Resultados de la evaluación de la actualización o revisión</span><span class="sxs-lookup"><span data-stu-id="75f28-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="75f28-113">Transmisiones de Syslogs habilitadas explícitamente en el agente</span><span class="sxs-lookup"><span data-stu-id="75f28-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="75f28-114">Estamos totalmente comprometidos a proteger la privacidad y la seguridad de estos datos.</span><span class="sxs-lookup"><span data-stu-id="75f28-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="75f28-115">Microsoft se adhiere a instrucciones estrictas de seguridad y cumplimiento de normas, desde la codificación hasta la operación de un servicio.</span><span class="sxs-lookup"><span data-stu-id="75f28-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="75f28-116">En este artículo se explica cómo se administran y protegen los datos en Seguridad y auditoría de OMS.</span><span class="sxs-lookup"><span data-stu-id="75f28-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="75f28-117">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="75f28-117">Data sources</span></span>
<span data-ttu-id="75f28-118">La solución Seguridad y auditoría de OMS analiza los datos de sus Virtual Machines y equipos físicos en los que está instalado el agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="75f28-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="75f28-119">La solución Seguridad y auditoría de OMS puede recopilar información de configuración sobre los eventos de seguridad, como los eventos de Windows, los registros de auditoría, los registros de IIS y los mensajes de syslog.</span><span class="sxs-lookup"><span data-stu-id="75f28-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="75f28-120">Estos son algunos ejemplos de dichos datos: tipo y versión, procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="75f28-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="75f28-121">Protección de datos</span><span class="sxs-lookup"><span data-stu-id="75f28-121">Data protection</span></span>
<span data-ttu-id="75f28-122">**Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente a lo largo de todo el servicio.</span><span class="sxs-lookup"><span data-stu-id="75f28-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="75f28-123">Todos los datos se etiquetan por organización.</span><span class="sxs-lookup"><span data-stu-id="75f28-123">All data is tagged per organization.</span></span> <span data-ttu-id="75f28-124">Este etiquetado persiste a lo largo del ciclo de vida de los datos y se aplica en cada nivel del servicio.</span><span class="sxs-lookup"><span data-stu-id="75f28-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="75f28-125">**Acceso a datos**: para proporcionar recomendaciones de seguridad e investigar las posibles amenazas de seguridad, el personal de Microsoft puede acceder a la información recopilada o analizada por los servicios.</span><span class="sxs-lookup"><span data-stu-id="75f28-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="75f28-126">Cumplimos los [términos](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) y la [declaración de privacidad de Microsoft Online Services](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), donde se estipula que Microsoft no utilizará los datos de los clientes ni información derivada de ellos con fines comerciales, publicitarios o similares.</span><span class="sxs-lookup"><span data-stu-id="75f28-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="75f28-127">Para proporcionar recomendaciones de seguridad e investigar las posibles amenazas de seguridad, el personal de Microsoft puede acceder a la información recopilada o analizada por los servicios.</span><span class="sxs-lookup"><span data-stu-id="75f28-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="75f28-128">Solo usamos los datos del cliente necesarios para proporcionar los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="75f28-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="75f28-129">El usuario conserva todos los derechos de sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="75f28-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="75f28-130">**Uso de datos**: Microsoft utiliza los patrones y la información sobre amenazas vistos en varios inquilinos para mejorar las funcionalidades de detección y prevención; esto se realiza según lo dispuesto en los compromisos de privacidad que se describen en nuestra [declaración de privacidad](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="75f28-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="75f28-131">La ubicación de los datos se configura en el nivel del área de trabajo de OMS, durante la creación del área de trabajo, que forma parte del proceso de configuración inicial de Seguridad y auditoría de OMS.</span><span class="sxs-lookup"><span data-stu-id="75f28-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="75f28-132">Consulte también</span><span class="sxs-lookup"><span data-stu-id="75f28-132">See also</span></span>
<span data-ttu-id="75f28-133">En este documento, ha aprendido cómo se administran y protegen los datos en OMS.</span><span class="sxs-lookup"><span data-stu-id="75f28-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="75f28-134">Para aprender más acerca de la solución Seguridad y auditoría de OMS, consulte:</span><span class="sxs-lookup"><span data-stu-id="75f28-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="75f28-135">Información general de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="75f28-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="75f28-136">Supervisión de las alertas de seguridad y su respuesta en la solución Security and Audit de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="75f28-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="75f28-137">Supervisión de los recursos en la solución Security and Audit de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="75f28-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

