---
title: "Conector de administración de servicio de OMS aaaIT | Documentos de Microsoft"
description: "Use Hola conector de administración de servicios de TI toocentrally supervisión y administrar elementos de trabajo ITSM hello en OMS, y solucione los problemas rápidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="bd2aa-103">Administración centralizada de los elementos de trabajo ITSM con IT Service Management Connector (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="bd2aa-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Símbolo de IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="bd2aa-105">Puede usar hello conector de administración de servicio de TI (ITSMC) en el monitor de toocentrally de análisis de registros de OMS y administrar elementos de trabajo entre sus productos y servicios ITSM.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="bd2aa-106">Hola conector de administración de servicios de TI integra los servicios y productos de administración de servicio de TI (ITSM) existente con análisis de registros de OMS.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="bd2aa-107">solución de Hello tiene integración bidireccional con productos o servicios a ITSM, donde proporciona Hola incidentes toocreate opción de los usuarios de OMS, alertas o eventos de solución ITSM.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="bd2aa-108">Conector de Hello también importa datos tales como incidentes y solicitudes de cambio de solución ITSM en análisis de registros de OMS.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="bd2aa-109">Con IT Service Management Connector, puede:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="bd2aa-110">Supervisar y administrar de manera centralizada elementos de trabajo para productos y servicios de ITSM que se usan en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="bd2aa-111">Crear elementos de trabajo de ITSM (como alertas, eventos, incidentes) en ITSM desde alertas de OMS y a través de la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="bd2aa-112">Leer incidentes y solicitudes de cambio en la solución ITSM y correlacionarlos con los datos de registro correspondientes en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="bd2aa-113">Buscar cualquier evento inesperado e inusual y resolverlos, incluso antes de que los usuarios finales de hello llamar y registrarlos toohello departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="bd2aa-114">Importar datos de elementos de trabajo a Log Analytics y crear informes de indicador de rendimiento clave (KPI).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="bd2aa-115">Con estos informes, puede identificar y evaluar varios elementos importantes, como la evaluación de malware, y actuar en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="bd2aa-116">Ver paneles protegidos para obtener información más detallada sobre incidentes, solicitudes de cambio y sistemas afectados.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="bd2aa-117">Solucionar problemas con mayor rapidez al correlacionar con otras soluciones de administración en el área de trabajo de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bd2aa-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bd2aa-118">Prerequisites</span></span>

<span data-ttu-id="bd2aa-119">elementos de trabajo de tooimport Hola ITSM en análisis de registros de OMS, solución de hello requiere una conexión entre Hola conector de administración de servicios de TI en OMS de Hola y Hola TI SM productos o servicios desde la que importar elementos de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="bd2aa-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="bd2aa-120">Configuration</span></span>

<span data-ttu-id="bd2aa-121">Hola de agregar espacio de trabajo OMS de tooyour de la solución de conector de administración de servicios de TI, mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="bd2aa-122">Conector de administración de servicios de TI icono como se ve en la Galería de soluciones de hello:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![icono de conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="bd2aa-124">Tras la adición de correcta, verá Hola conector de administración de servicios de TI en **OMS** > **configuración** > **orígenes conectados.**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="bd2aa-126">De forma predeterminada, Hola conector de administración de servicios de TI actualiza los datos de la conexión de hello una vez en cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="bd2aa-127">toorefresh datos de la conexión al instante para cualquier plantilla o modificaciones actualizan realizados, haga clic en conexión siguiente tooyour de hello actualización botón que se muestra.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Actualización de ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="bd2aa-129">Módulos de administración</span><span class="sxs-lookup"><span data-stu-id="bd2aa-129">Management packs</span></span>
<span data-ttu-id="bd2aa-130">Esta solución no necesita ningún módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="bd2aa-131">Orígenes conectados</span><span class="sxs-lookup"><span data-stu-id="bd2aa-131">Connected sources</span></span>

<span data-ttu-id="bd2aa-132">Hello siguientes ITSM productos/servicios admite Hola conector de administración de servicios de TI:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="bd2aa-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="bd2aa-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="bd2aa-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bd2aa-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="bd2aa-135">Provance</span><span class="sxs-lookup"><span data-stu-id="bd2aa-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="bd2aa-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="bd2aa-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="bd2aa-137">Uso de solución de Hola</span><span class="sxs-lookup"><span data-stu-id="bd2aa-137">Using hello solution</span></span>

<span data-ttu-id="bd2aa-138">Una vez Hola conector de administración de servicios de TI de OMS se conecta con el servicio ITSM, servicios de análisis de registros de hello inicia la recopilación de datos de Hola Hola conectado ITSM productos/service.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="bd2aa-139">Los datos que importa la solución IT Service Management Connector aparecen en Log Analytics como eventos denominados **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="bd2aa-140">Los eventos contienen un campo llamado **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="bd2aa-141">que puede tomar su valor como incidentes, o solicitud de cambio, función hello de elemento de trabajo datos contenidos en hello **ServiceDesk_CL** eventos.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="bd2aa-142">Datos de entrada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-142">Input data</span></span>
<span data-ttu-id="bd2aa-143">Los elementos de trabajo importan de hello ITSM productos y servicios.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="bd2aa-144">Hello información siguiente muestra ejemplos de datos recopilados por el conector de administración de servicios de TI de hello:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="bd2aa-145">Función hello de elemento de trabajo importado en el análisis de registros de tipo **ServiceDesk_CL** contiene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="bd2aa-146">**Elemento de trabajo:****incidentes**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="bd2aa-147">ServiceDeskWorkItemType_s="Incidente"</span><span class="sxs-lookup"><span data-stu-id="bd2aa-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="bd2aa-148">**Fields**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-148">**Fields**</span></span>

- <span data-ttu-id="bd2aa-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="bd2aa-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="bd2aa-150">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="bd2aa-150">Service Desk ID</span></span>
- <span data-ttu-id="bd2aa-151">Estado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-151">State</span></span>
- <span data-ttu-id="bd2aa-152">Urgencia</span><span class="sxs-lookup"><span data-stu-id="bd2aa-152">Urgency</span></span>
- <span data-ttu-id="bd2aa-153">Impacto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-153">Impact</span></span>
- <span data-ttu-id="bd2aa-154">Prioridad</span><span class="sxs-lookup"><span data-stu-id="bd2aa-154">Priority</span></span>
- <span data-ttu-id="bd2aa-155">Escalado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-155">Escalation</span></span>
- <span data-ttu-id="bd2aa-156">Creado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-156">Created By</span></span>
- <span data-ttu-id="bd2aa-157">Resuelto por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-157">Resolved By</span></span>
- <span data-ttu-id="bd2aa-158">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-158">Closed By</span></span>
- <span data-ttu-id="bd2aa-159">Origen</span><span class="sxs-lookup"><span data-stu-id="bd2aa-159">Source</span></span>
- <span data-ttu-id="bd2aa-160">Asignado a</span><span class="sxs-lookup"><span data-stu-id="bd2aa-160">Assigned To</span></span>
- <span data-ttu-id="bd2aa-161">Categoría</span><span class="sxs-lookup"><span data-stu-id="bd2aa-161">Category</span></span>
- <span data-ttu-id="bd2aa-162">Título</span><span class="sxs-lookup"><span data-stu-id="bd2aa-162">Title</span></span>
- <span data-ttu-id="bd2aa-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd2aa-163">Description</span></span>
- <span data-ttu-id="bd2aa-164">Fecha de creación</span><span class="sxs-lookup"><span data-stu-id="bd2aa-164">Created Date</span></span>
- <span data-ttu-id="bd2aa-165">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="bd2aa-165">Closed Date</span></span>
- <span data-ttu-id="bd2aa-166">Fecha de resolución</span><span class="sxs-lookup"><span data-stu-id="bd2aa-166">Resolved Date</span></span>
- <span data-ttu-id="bd2aa-167">Fecha de última modificación</span><span class="sxs-lookup"><span data-stu-id="bd2aa-167">Last Modified Date</span></span>
- <span data-ttu-id="bd2aa-168">Equipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-168">Computer</span></span>


<span data-ttu-id="bd2aa-169">**Elemento de trabajo:****solicitudes de cambio**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="bd2aa-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="bd2aa-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="bd2aa-171">**Fields**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-171">**Fields**</span></span>
- <span data-ttu-id="bd2aa-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="bd2aa-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="bd2aa-173">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="bd2aa-173">Service Desk ID</span></span>
- <span data-ttu-id="bd2aa-174">Creado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-174">Created By</span></span>
- <span data-ttu-id="bd2aa-175">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-175">Closed By</span></span>
- <span data-ttu-id="bd2aa-176">Origen</span><span class="sxs-lookup"><span data-stu-id="bd2aa-176">Source</span></span>
- <span data-ttu-id="bd2aa-177">Asignado a</span><span class="sxs-lookup"><span data-stu-id="bd2aa-177">Assigned To</span></span>
- <span data-ttu-id="bd2aa-178">Título</span><span class="sxs-lookup"><span data-stu-id="bd2aa-178">Title</span></span>
- <span data-ttu-id="bd2aa-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-179">Type</span></span>
- <span data-ttu-id="bd2aa-180">Categoría</span><span class="sxs-lookup"><span data-stu-id="bd2aa-180">Category</span></span>
- <span data-ttu-id="bd2aa-181">Estado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-181">State</span></span>
- <span data-ttu-id="bd2aa-182">Escalado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-182">Escalation</span></span>
- <span data-ttu-id="bd2aa-183">Estado del conflicto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-183">Conflict Status</span></span>
- <span data-ttu-id="bd2aa-184">Urgencia</span><span class="sxs-lookup"><span data-stu-id="bd2aa-184">Urgency</span></span>
- <span data-ttu-id="bd2aa-185">Prioridad</span><span class="sxs-lookup"><span data-stu-id="bd2aa-185">Priority</span></span>
- <span data-ttu-id="bd2aa-186">Riesgo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-186">Risk</span></span>
- <span data-ttu-id="bd2aa-187">Impacto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-187">Impact</span></span>
- <span data-ttu-id="bd2aa-188">Asignado a</span><span class="sxs-lookup"><span data-stu-id="bd2aa-188">Assigned To</span></span>
- <span data-ttu-id="bd2aa-189">Fecha de creación</span><span class="sxs-lookup"><span data-stu-id="bd2aa-189">Created Date</span></span>
- <span data-ttu-id="bd2aa-190">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="bd2aa-190">Closed Date</span></span>
- <span data-ttu-id="bd2aa-191">Fecha de última modificación</span><span class="sxs-lookup"><span data-stu-id="bd2aa-191">Last Modified Date</span></span>
- <span data-ttu-id="bd2aa-192">Fecha de solicitud</span><span class="sxs-lookup"><span data-stu-id="bd2aa-192">Requested Date</span></span>
- <span data-ttu-id="bd2aa-193">Fecha de inicio planeada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-193">Planned Start Date</span></span>
- <span data-ttu-id="bd2aa-194">Fecha de finalización planeada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-194">Planned End Date</span></span>
- <span data-ttu-id="bd2aa-195">Fecha de inicio del trabajo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-195">Work Start Date</span></span>
- <span data-ttu-id="bd2aa-196">Fecha de finalización del trabajo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-196">Work End Date</span></span>
- <span data-ttu-id="bd2aa-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd2aa-197">Description</span></span>
- <span data-ttu-id="bd2aa-198">Equipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="bd2aa-199">Datos de salida para un incidente de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bd2aa-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="bd2aa-200">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-200">OMS field</span></span> | <span data-ttu-id="bd2aa-201">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="bd2aa-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="bd2aa-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-202">ServiceDeskId_s</span></span>| <span data-ttu-id="bd2aa-203">Number</span><span class="sxs-lookup"><span data-stu-id="bd2aa-203">Number</span></span> |
| <span data-ttu-id="bd2aa-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-204">IncidentState_s</span></span> | <span data-ttu-id="bd2aa-205">Estado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-205">State</span></span> |
| <span data-ttu-id="bd2aa-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-206">Urgency_s</span></span> |<span data-ttu-id="bd2aa-207">Urgencia</span><span class="sxs-lookup"><span data-stu-id="bd2aa-207">Urgency</span></span> |
| <span data-ttu-id="bd2aa-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-208">Impact_s</span></span> |<span data-ttu-id="bd2aa-209">Impacto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-209">Impact</span></span>|
| <span data-ttu-id="bd2aa-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-210">Priority_s</span></span> | <span data-ttu-id="bd2aa-211">Prioridad</span><span class="sxs-lookup"><span data-stu-id="bd2aa-211">Priority</span></span> |
| <span data-ttu-id="bd2aa-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-212">CreatedBy_s</span></span> | <span data-ttu-id="bd2aa-213">Abierto por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-213">Opened by</span></span> |
| <span data-ttu-id="bd2aa-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-214">ResolvedBy_s</span></span> | <span data-ttu-id="bd2aa-215">Resuelto por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-215">Resolved by</span></span>|
| <span data-ttu-id="bd2aa-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-216">ClosedBy_s</span></span>  | <span data-ttu-id="bd2aa-217">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-217">Closed by</span></span> |
| <span data-ttu-id="bd2aa-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-218">Source_s</span></span>| <span data-ttu-id="bd2aa-219">Tipo de contacto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-219">Contact type</span></span> |
| <span data-ttu-id="bd2aa-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-220">AssignedTo_s</span></span> | <span data-ttu-id="bd2aa-221">Asignado demasiado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-221">Assigned too</span></span> |
| <span data-ttu-id="bd2aa-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-222">Category_s</span></span> | <span data-ttu-id="bd2aa-223">Categoría</span><span class="sxs-lookup"><span data-stu-id="bd2aa-223">Category</span></span> |
| <span data-ttu-id="bd2aa-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-224">Title_s</span></span>|  <span data-ttu-id="bd2aa-225">Descripción breve</span><span class="sxs-lookup"><span data-stu-id="bd2aa-225">Short description</span></span> |
| <span data-ttu-id="bd2aa-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-226">Description_s</span></span>|  <span data-ttu-id="bd2aa-227">Notas</span><span class="sxs-lookup"><span data-stu-id="bd2aa-227">Notes</span></span> |
| <span data-ttu-id="bd2aa-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-228">CreatedDate_t</span></span>|  <span data-ttu-id="bd2aa-229">Abierto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-229">Opened</span></span> |
| <span data-ttu-id="bd2aa-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-230">ClosedDate_t</span></span>| <span data-ttu-id="bd2aa-231">closed</span><span class="sxs-lookup"><span data-stu-id="bd2aa-231">closed</span></span>|
| <span data-ttu-id="bd2aa-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-232">ResolvedDate_t</span></span>|<span data-ttu-id="bd2aa-233">Resuelto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-233">Resolved</span></span>|
| <span data-ttu-id="bd2aa-234">Equipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-234">Computer</span></span>  | <span data-ttu-id="bd2aa-235">Elemento de configuración</span><span class="sxs-lookup"><span data-stu-id="bd2aa-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="bd2aa-236">Datos de salida para una solicitud de cambio de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="bd2aa-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="bd2aa-237">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-237">OMS field</span></span> | <span data-ttu-id="bd2aa-238">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="bd2aa-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="bd2aa-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-239">ServiceDeskId_s</span></span>| <span data-ttu-id="bd2aa-240">Number</span><span class="sxs-lookup"><span data-stu-id="bd2aa-240">Number</span></span> |
| <span data-ttu-id="bd2aa-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-241">CreatedBy_s</span></span> | <span data-ttu-id="bd2aa-242">Solicitado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-242">Requested by</span></span> |
| <span data-ttu-id="bd2aa-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-243">ClosedBy_s</span></span> | <span data-ttu-id="bd2aa-244">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="bd2aa-244">Closed by</span></span> |
| <span data-ttu-id="bd2aa-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-245">AssignedTo_s</span></span> | <span data-ttu-id="bd2aa-246">Asignado demasiado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-246">Assigned too</span></span> |
| <span data-ttu-id="bd2aa-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-247">Title_s</span></span>|  <span data-ttu-id="bd2aa-248">Descripción breve</span><span class="sxs-lookup"><span data-stu-id="bd2aa-248">Short description</span></span> |
| <span data-ttu-id="bd2aa-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-249">Type_s</span></span>|  <span data-ttu-id="bd2aa-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-250">Type</span></span> |
| <span data-ttu-id="bd2aa-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-251">Category_s</span></span>|  <span data-ttu-id="bd2aa-252">Categoría</span><span class="sxs-lookup"><span data-stu-id="bd2aa-252">Catgory</span></span> |
| <span data-ttu-id="bd2aa-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-253">CRState_s</span></span>|  <span data-ttu-id="bd2aa-254">Estado</span><span class="sxs-lookup"><span data-stu-id="bd2aa-254">State</span></span>|
| <span data-ttu-id="bd2aa-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-255">Urgency_s</span></span>|  <span data-ttu-id="bd2aa-256">Urgencia</span><span class="sxs-lookup"><span data-stu-id="bd2aa-256">Urgency</span></span> |
| <span data-ttu-id="bd2aa-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-257">Priority_s</span></span>| <span data-ttu-id="bd2aa-258">Prioridad</span><span class="sxs-lookup"><span data-stu-id="bd2aa-258">Priority</span></span>|
| <span data-ttu-id="bd2aa-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-259">Risk_s</span></span>| <span data-ttu-id="bd2aa-260">Riesgo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-260">Risk</span></span>|
| <span data-ttu-id="bd2aa-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-261">Impact_s</span></span>| <span data-ttu-id="bd2aa-262">Impacto</span><span class="sxs-lookup"><span data-stu-id="bd2aa-262">Impact</span></span>|
| <span data-ttu-id="bd2aa-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-263">RequestedDate_t</span></span>  | <span data-ttu-id="bd2aa-264">Solicitado por fecha</span><span class="sxs-lookup"><span data-stu-id="bd2aa-264">Requested by date</span></span> |
| <span data-ttu-id="bd2aa-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-265">ClosedDate_t</span></span> | <span data-ttu-id="bd2aa-266">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="bd2aa-266">Closed date</span></span> |
| <span data-ttu-id="bd2aa-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="bd2aa-268">Fecha de inicio planeada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-268">Planned start date</span></span> |
| <span data-ttu-id="bd2aa-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="bd2aa-270">Fecha de finalización planeada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-270">Planned end date</span></span> |
| <span data-ttu-id="bd2aa-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-271">WorkStartDate_t</span></span>  | <span data-ttu-id="bd2aa-272">Fecha de inicio real</span><span class="sxs-lookup"><span data-stu-id="bd2aa-272">Actual start date</span></span> |
| <span data-ttu-id="bd2aa-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="bd2aa-273">WorkEndDate_t</span></span> | <span data-ttu-id="bd2aa-274">Fecha de finalización real</span><span class="sxs-lookup"><span data-stu-id="bd2aa-274">Actual end date</span></span>|
| <span data-ttu-id="bd2aa-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="bd2aa-275">Description_s</span></span> | <span data-ttu-id="bd2aa-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="bd2aa-276">Description</span></span> |
| <span data-ttu-id="bd2aa-277">Equipo</span><span class="sxs-lookup"><span data-stu-id="bd2aa-277">Computer</span></span>  | <span data-ttu-id="bd2aa-278">Elemento de configuración</span><span class="sxs-lookup"><span data-stu-id="bd2aa-278">Configuration Item</span></span> |

<span data-ttu-id="bd2aa-279">**Pantalla de Log Analytics de ejemplo para datos de ITSM:**</span><span class="sxs-lookup"><span data-stu-id="bd2aa-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="bd2aa-281">IT Service Management Connector: integración con otras soluciones de OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="bd2aa-282">Conector de administración de servicio de TI, actualmente admite la integración con hello mapa de servicio de la solución.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="bd2aa-283">Mapa de servicio detecta automáticamente Hola componentes de la aplicación en Windows y los mapas y sistemas Linux Hola comunicación entre los servicios.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="bd2aa-284">Permite tooview los servidores que pensar en ellos, como sistemas interconectados que ofrecen servicios críticos.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="bd2aa-285">Mapa de servicio muestra las conexiones entre servidores, procesos y puertos en cualquier arquitectura conectada TCP sin una configuración necesaria que sea distinta a la instalación de un agente.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="bd2aa-286">Más información: [Mapa de servicio](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="bd2aa-287">Con esta integración, puede ver los elementos de departamento de soporte de servicio Hola creados en soluciones ITSM de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="bd2aa-288">Solución integrada</span><span class="sxs-lookup"><span data-stu-id="bd2aa-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="bd2aa-289">Creación de elementos de trabajo de ITSM para alertas de OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="bd2aa-290">Para las alertas OMS de hello, puede crear elementos de trabajo asociados en los orígenes de ITSM Hola conectado.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="bd2aa-291">toodo, Hola de uso siguiente procedimiento:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="bd2aa-292">De **Log Search** ventana, ejecute un datos tooview de consulta de búsqueda de registro.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="bd2aa-293">Resultados de la consulta son origen de Hola de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="bd2aa-294">En **Log Search**, haga clic en **alerta** tooopen hello **Agregar regla de alerta** página.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="bd2aa-296">En hello **Agregar regla de alerta** ventana, proporcione los detalles de hello necesario de **nombre**, **gravedad**, **consulta de búsqueda**, y  **Criterios de alerta** (medida de ventana/métrica de tiempo).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="bd2aa-297">Seleccione **Sí** en **Acciones de ITSM**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="bd2aa-298">Seleccione la conexión de ITSM de hello **Seleccionar conexión** lista.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="bd2aa-299">Proporcione detalles de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="bd2aa-300">un elemento de trabajo independiente para cada entrada de registro de esta alerta, seleccione hello toocreate **crear elementos de trabajo individuales para cada entrada de registro** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="bd2aa-301">O</span><span class="sxs-lookup"><span data-stu-id="bd2aa-301">Or</span></span>

    <span data-ttu-id="bd2aa-302">Deje esta casilla de verificación toocreate no seleccionados solo un elemento de trabajo para cualquier número de entradas del registro en esta alerta.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="bd2aa-303">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-303">Click **Save**.</span></span>

<span data-ttu-id="bd2aa-304">alerta de OMS Hola se creará bajo **alertas**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="bd2aa-305">Hola elementos se crean cuando se cumpla la condición de alerta especificado Hola de trabajo de la conexión ITSM correspondiente.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="bd2aa-306">Creación de elementos de trabajo de ITSM desde registros de OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="bd2aa-307">Puede crear elementos de trabajo en los orígenes de ITSM Hola conectado mediante búsqueda de registros de OMS.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="bd2aa-308">toodo, Hola de uso siguiente procedimiento:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="bd2aa-309">De **Log Search**, buscar Hola requerido datos, seleccione detalles de Hola y haga clic en **crear elemento de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="bd2aa-310">Hola **elemento de trabajo de ITSM crear** aparecerá la ventana:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Pantalla de Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="bd2aa-312">Agregue Hola detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-312">Add hello following details:</span></span>

  - <span data-ttu-id="bd2aa-313">**Título de elemento de trabajo**: título de elemento de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="bd2aa-314">**Descripción de elemento de trabajo**: descripción de elemento de trabajo nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="bd2aa-315">**Afectado equipo**: nombre del equipo de Hola donde se encontraron estos datos de registro.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="bd2aa-316">**Seleccionar conexión**: conexión ITSM del que desee toocreate este elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="bd2aa-317">**Elemento de trabajo**: tipo de elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="bd2aa-318">toouse una plantilla de elemento de trabajo existente de un incidente, haga clic en **Sí** en **generar elemento de trabajo basado en la plantilla de hello** opción y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="bd2aa-319">O bien,</span><span class="sxs-lookup"><span data-stu-id="bd2aa-319">Or,</span></span>

    <span data-ttu-id="bd2aa-320">Haga clic en **n** si desea tooprovide los valores personalizados.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="bd2aa-321">Proporcione los valores adecuados de Hola Hola **tipo de contacto**, **impacto**, **urgencia**, **categoría**, y **subcategoría**  cuadros de texto y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="bd2aa-322">se creará el elemento de trabajo de Hola Hola ITSM, que también se puede ver en OMS.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="bd2aa-323">Solución de problemas de conexión de ITSM en OMS</span><span class="sxs-lookup"><span data-stu-id="bd2aa-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="bd2aa-324">Si se produce un error en la conexión de la interfaz de usuario del origen conectado y obtener hello **Error al guardar la conexión** de mensajes, Hola después de:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="bd2aa-325">En el caso de las conexiones de ServiceNow, Cherwell y Provance, asegúrese de secreto de cliente y el Id. de nombre de usuario/contraseña y el cliente hello correctamente especificado para cada una de las conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="bd2aa-326">Si Hola error persiste, compruebe si dispone de suficientes privilegios en conexión de hello correspondiente ITSM producto toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="bd2aa-327">En el caso de Service Manager, asegúrese de que se implementa correctamente hello Web app y conexión híbrida se crea.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="bd2aa-328">conexión de hello tooverify correctamente se establece con equipo de Service Manager local hello, visite URL de la aplicación hello Web tal como se detalla en la documentación de Hola para realizar hello [conexión híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="bd2aa-329">Si no obtener se sincronizan datos de ServiceNow en OMS, asegurarse de que esa instancia de ServiceNow hello no está en espera.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="bd2aa-330">En algún momento posible en hello ServiceNow Dev instancias, cuando esté inactivo.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="bd2aa-331">Else, problema de Hola de informe.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="bd2aa-332">Si obtener se activan alertas de OMS, pero no obtener se crean elementos de trabajo en el producto ITSM o elementos de configuración no están recibiendo elementos toowork creado/vinculada o para toda la información genérica, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd2aa-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="bd2aa-333">Solución de conector de administración de servicios de TI en el portal de OMS puede ser usado tooget un resumen de elementos de trabajo/conexiones/equipos etcetera. Haga clic en el mensaje de error de hello en la hoja de estado de hello, navegue demasiado**búsqueda de registros** y ver Hola conexión que tiene el error de hello mediante detalles de hello en el mensaje de error de saludo.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="bd2aa-334">directamente puede ver información de errores/relacionado de Hola Hola **Log Search** página con *tipo = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="bd2aa-335">Solucionar problemas de implementación de aplicaciones web de Service Manager</span><span class="sxs-lookup"><span data-stu-id="bd2aa-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="bd2aa-336">En el caso de los problemas con la implementación de aplicación web, asegúrese de que dispone de suficientes permisos de suscripción de hello mencionado toocreate/implementar recursos.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="bd2aa-337">Si **no establece la referencia de objeto tooinstance de un objeto** aparece el mensaje de error durante la ejecución hello [script](log-analytics-itsmc-service-manager-script.md) Asegúrese de que ha especificado valores válidos en **configuración de usuario**sección.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="bd2aa-338">Si se produce un error de espacio de nombres de retransmisión de bus de servicio de toocreate, asegúrese de que hello necesarios de proveedor de recursos está registrado en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="bd2aa-339">Si no está registrado, crear manualmente de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="bd2aa-340">También puede crear mientras [crear conexión híbrida de hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd2aa-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="bd2aa-341">Ponerse en contacto con nosotros</span><span class="sxs-lookup"><span data-stu-id="bd2aa-341">Contact us</span></span>

<span data-ttu-id="bd2aa-342">Para cualquier consulta o comentarios en hello conector de administración de servicios de TI, póngase en contacto con nosotros en [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd2aa-343">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd2aa-343">Next steps</span></span>
<span data-ttu-id="bd2aa-344">[Agregar tooIT de productos y servicios ITSM Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="bd2aa-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
