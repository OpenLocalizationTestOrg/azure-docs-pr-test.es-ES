---
title: "aaaOperations seguridad del conjunto de administración y seguridad de datos de auditoría soluciones | Documentos de Microsoft"
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
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="18079-103">Seguridad de datos de la solución Seguridad y auditoría de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="18079-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="18079-104">los clientes de toohelp evitar, detectar y responder toothreats, [Operations Management Suite (OMS) solución de seguridad y auditoría](operations-management-suite-overview.md) recopila y procesa los datos sobre los recursos, que incluye:</span><span class="sxs-lookup"><span data-stu-id="18079-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="18079-105">Registro de eventos de seguridad</span><span class="sxs-lookup"><span data-stu-id="18079-105">Security event log</span></span>
* <span data-ttu-id="18079-106">Eventos de Seguimiento de eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="18079-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="18079-107">Eventos de auditoría de AppLocker</span><span class="sxs-lookup"><span data-stu-id="18079-107">AppLocker auditing events</span></span>
* <span data-ttu-id="18079-108">Registro de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="18079-108">Windows Firewall log</span></span>
* <span data-ttu-id="18079-109">Eventos de Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="18079-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="18079-110">Resultados de evaluación de la línea base</span><span class="sxs-lookup"><span data-stu-id="18079-110">Results of baseline assessment</span></span>
* <span data-ttu-id="18079-111">Resultados de evaluación de antimalware</span><span class="sxs-lookup"><span data-stu-id="18079-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="18079-112">Resultados de la evaluación de la actualización o revisión</span><span class="sxs-lookup"><span data-stu-id="18079-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="18079-113">Secuencias de Syslogs que se habilitan de manera explícita en el agente de Hola</span><span class="sxs-lookup"><span data-stu-id="18079-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="18079-114">Hacemos privacidad de hello tooprotect compromisos segura y la seguridad de estos datos.</span><span class="sxs-lookup"><span data-stu-id="18079-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="18079-115">Microsoft adhiere a las directrices de seguridad y cumplimiento de toostrict: desde la codificación toooperating un servicio.</span><span class="sxs-lookup"><span data-stu-id="18079-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="18079-116">En este artículo se explica cómo se administran y protegen los datos en Seguridad y auditoría de OMS.</span><span class="sxs-lookup"><span data-stu-id="18079-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="18079-117">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="18079-117">Data sources</span></span>
<span data-ttu-id="18079-118">Solución de auditoría y seguridad de OMS analizan los datos de las máquinas virtuales y equipos físicos donde está instalado el agente de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="18079-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="18079-119">La solución Seguridad y auditoría de OMS puede recopilar información de configuración sobre los eventos de seguridad, como los eventos de Windows, los registros de auditoría, los registros de IIS y los mensajes de syslog.</span><span class="sxs-lookup"><span data-stu-id="18079-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="18079-120">Estos son algunos ejemplos de dichos datos: tipo y versión, procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="18079-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="18079-121">Protección de datos</span><span class="sxs-lookup"><span data-stu-id="18079-121">Data protection</span></span>
<span data-ttu-id="18079-122">**Segregación de datos**: los datos se mantienen separados de forma lógica en cada componente en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18079-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="18079-123">Todos los datos se etiquetan por organización.</span><span class="sxs-lookup"><span data-stu-id="18079-123">All data is tagged per organization.</span></span> <span data-ttu-id="18079-124">Este etiquetado persiste a lo largo del ciclo de vida de datos de Hola y se aplica en cada nivel de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18079-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="18079-125">**Acceso a datos**: recomendaciones de seguridad de tooprovide e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios.</span><span class="sxs-lookup"><span data-stu-id="18079-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="18079-126">Cumplimos toohello [condiciones de Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) y [declaración de privacidad](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), qué estado que Microsoft usará no los datos del cliente o derivar información de él para publicación o similar con fines comerciales.</span><span class="sxs-lookup"><span data-stu-id="18079-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="18079-127">recomendaciones de seguridad de tooprovide e investigar posibles amenazas de seguridad, personal de Microsoft puede tener acceso a la información recopilada o analizar por servicios.</span><span class="sxs-lookup"><span data-stu-id="18079-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="18079-128">Solo se utilizan los datos del cliente como tooprovide necesaria con Azure de servicios, incluido con fines compatible con el suministro de dichos servicios.</span><span class="sxs-lookup"><span data-stu-id="18079-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="18079-129">Conservar todos los datos propios tooyour de permisos.</span><span class="sxs-lookup"><span data-stu-id="18079-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="18079-130">**Uso de datos**: Microsoft utiliza patrones e inteligencia sobre amenazas visto entre varios inquilinos tooenhance nuestras capacidades de detección y prevención; lo hacemos según se describe en los compromisos de privacidad de hello nuestro [privacidad Instrucción](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="18079-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="18079-131">Ubicación de los datos se configura a nivel de área de trabajo OMS de hello, durante la creación de área de trabajo de hello, que forma parte Hola inicial OMS seguridad y auditoría del proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="18079-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="18079-132">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="18079-132">See also</span></span>
<span data-ttu-id="18079-133">En este documento, ha aprendido cómo se administran y protegen los datos en OMS.</span><span class="sxs-lookup"><span data-stu-id="18079-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="18079-134">toolearn más información sobre la seguridad de OMS y la solución de auditoría, vea:</span><span class="sxs-lookup"><span data-stu-id="18079-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="18079-135">Información general de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="18079-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="18079-136">Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría</span><span class="sxs-lookup"><span data-stu-id="18079-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="18079-137">Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="18079-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

