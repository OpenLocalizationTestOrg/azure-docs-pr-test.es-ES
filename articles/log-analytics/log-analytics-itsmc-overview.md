---
title: IT Service Management Connector en OMS | Microsoft Docs
description: "Use IT Service Manager Connector para supervisar y administrar de manera centralizada los elementos de trabajo ITSM en OMS y solucionar rápidamente cualquier problema."
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
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="082c9-103">Administración centralizada de los elementos de trabajo ITSM con IT Service Management Connector (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="082c9-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Símbolo de IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="082c9-105">Puede usar IT Service Management Connector (ITSMC) en Log Analytics de OMS para supervisar y administrar de manera centralizada elementos de trabajo en todos los productos o servicios de ITSM.</span><span class="sxs-lookup"><span data-stu-id="082c9-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="082c9-106">IT Service Management Connector integra los productos y servicios existentes de IT Service Management (ITSM) con Log Analytics de OMS.</span><span class="sxs-lookup"><span data-stu-id="082c9-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="082c9-107">La solución tiene una integración bidireccional con productos o servicios de ITSM, donde proporciona a los usuarios de OMS una opción para crear incidentes, alertas o eventos en la solución ITSM.</span><span class="sxs-lookup"><span data-stu-id="082c9-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="082c9-108">El conector también importa datos como incidentes y solicitudes de cambio desde la solución ITSM a Log Analytics de OMS.</span><span class="sxs-lookup"><span data-stu-id="082c9-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="082c9-109">Con IT Service Management Connector, puede:</span><span class="sxs-lookup"><span data-stu-id="082c9-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="082c9-110">Supervisar y administrar de manera centralizada elementos de trabajo para productos y servicios de ITSM que se usan en toda la organización.</span><span class="sxs-lookup"><span data-stu-id="082c9-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="082c9-111">Crear elementos de trabajo de ITSM (como alertas, eventos, incidentes) en ITSM desde alertas de OMS y a través de la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="082c9-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="082c9-112">Leer incidentes y solicitudes de cambio en la solución ITSM y correlacionarlos con los datos de registro correspondientes en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="082c9-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="082c9-113">Encontrar eventos inesperados e inusuales y resolverlos, incluso antes de que los usuarios finales llamen al departamento de soporte técnico para informarlos.</span><span class="sxs-lookup"><span data-stu-id="082c9-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="082c9-114">Importar datos de elementos de trabajo a Log Analytics y crear informes de indicador de rendimiento clave (KPI).</span><span class="sxs-lookup"><span data-stu-id="082c9-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="082c9-115">Con estos informes, puede identificar y evaluar varios elementos importantes, como la evaluación de malware, y actuar en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="082c9-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="082c9-116">Ver paneles protegidos para obtener información más detallada sobre incidentes, solicitudes de cambio y sistemas afectados.</span><span class="sxs-lookup"><span data-stu-id="082c9-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="082c9-117">Solucionar problemas más rápidamente a través de la correlación con otras soluciones de administración en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="082c9-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="082c9-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="082c9-118">Prerequisites</span></span>

<span data-ttu-id="082c9-119">Para importar los elementos de trabajo de ITSM a Log Analytics de OMS, la solución requiere una conexión entre IT Service Management Connector en OMS y el producto o servicio de ITSM desde el cual importa los elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="082c9-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="082c9-120">Configuration</span></span>

<span data-ttu-id="082c9-121">Agregue la solución IT Service Management Connector al área de trabajo de OMS a través del proceso descrito en [Incorporación de soluciones de Log Analytics desde la galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="082c9-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="082c9-122">Icono de IT Service Management Connector como aparece en la galería de soluciones:</span><span class="sxs-lookup"><span data-stu-id="082c9-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![icono de conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="082c9-124">Después de agregarlo de manera correcta, podrá ver IT Service Management Connector en **OMS** > **Configuración** > **Orígenes conectados.**</span><span class="sxs-lookup"><span data-stu-id="082c9-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="082c9-126">De forma predeterminada, IT Service Management Connector actualiza los datos de la conexión una vez cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="082c9-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="082c9-127">Para actualizar los datos de la conexión al instante para cualquier modificación o actualizaciones de plantilla que se realicen, haga clic en el botón de actualización que se muestra junto a la conexión.</span><span class="sxs-lookup"><span data-stu-id="082c9-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Actualización de ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="082c9-129">Módulos de administración</span><span class="sxs-lookup"><span data-stu-id="082c9-129">Management packs</span></span>
<span data-ttu-id="082c9-130">Esta solución no necesita ningún módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="082c9-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="082c9-131">Orígenes conectados</span><span class="sxs-lookup"><span data-stu-id="082c9-131">Connected sources</span></span>

<span data-ttu-id="082c9-132">IT Service Management Connector admite los siguientes productos o servicios de ITSM:</span><span class="sxs-lookup"><span data-stu-id="082c9-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="082c9-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="082c9-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="082c9-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="082c9-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="082c9-135">Provance</span><span class="sxs-lookup"><span data-stu-id="082c9-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="082c9-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="082c9-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="082c9-137">Uso de la solución</span><span class="sxs-lookup"><span data-stu-id="082c9-137">Using the solution</span></span>

<span data-ttu-id="082c9-138">Una vez que conecta IT Service Management Connector de OMS al servicio de ITSM, los servicios de Log Analytics comienzan a recopilar los datos de los productos o servicios de ITSM conectados.</span><span class="sxs-lookup"><span data-stu-id="082c9-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="082c9-139">Los datos que importa la solución IT Service Management Connector aparecen en Log Analytics como eventos denominados **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="082c9-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="082c9-140">Los eventos contienen un campo llamado **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="082c9-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="082c9-141">que puede tomar su valor como incidente o como solicitud de cambio, según los datos de elemento de trabajo contenidos en el evento **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="082c9-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="082c9-142">Datos de entrada</span><span class="sxs-lookup"><span data-stu-id="082c9-142">Input data</span></span>
<span data-ttu-id="082c9-143">Elementos de trabajo importados desde servicios o productos de ITSM.</span><span class="sxs-lookup"><span data-stu-id="082c9-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="082c9-144">La información siguiente muestra ejemplos de los datos que recopila IT Service Management Connector:</span><span class="sxs-lookup"><span data-stu-id="082c9-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="082c9-145">En función del tipo de elemento de trabajo que se importa a Log Analytics, **ServiceDesk_CL** contiene los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="082c9-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="082c9-146">**Elemento de trabajo:** **incidentes**</span><span class="sxs-lookup"><span data-stu-id="082c9-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="082c9-147">ServiceDeskWorkItemType_s="Incidente"</span><span class="sxs-lookup"><span data-stu-id="082c9-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="082c9-148">**Fields**</span><span class="sxs-lookup"><span data-stu-id="082c9-148">**Fields**</span></span>

- <span data-ttu-id="082c9-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="082c9-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="082c9-150">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="082c9-150">Service Desk ID</span></span>
- <span data-ttu-id="082c9-151">Estado</span><span class="sxs-lookup"><span data-stu-id="082c9-151">State</span></span>
- <span data-ttu-id="082c9-152">Urgencia</span><span class="sxs-lookup"><span data-stu-id="082c9-152">Urgency</span></span>
- <span data-ttu-id="082c9-153">Impacto</span><span class="sxs-lookup"><span data-stu-id="082c9-153">Impact</span></span>
- <span data-ttu-id="082c9-154">Prioridad</span><span class="sxs-lookup"><span data-stu-id="082c9-154">Priority</span></span>
- <span data-ttu-id="082c9-155">Escalado</span><span class="sxs-lookup"><span data-stu-id="082c9-155">Escalation</span></span>
- <span data-ttu-id="082c9-156">Creado por</span><span class="sxs-lookup"><span data-stu-id="082c9-156">Created By</span></span>
- <span data-ttu-id="082c9-157">Resuelto por</span><span class="sxs-lookup"><span data-stu-id="082c9-157">Resolved By</span></span>
- <span data-ttu-id="082c9-158">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="082c9-158">Closed By</span></span>
- <span data-ttu-id="082c9-159">Origen</span><span class="sxs-lookup"><span data-stu-id="082c9-159">Source</span></span>
- <span data-ttu-id="082c9-160">Asignado a</span><span class="sxs-lookup"><span data-stu-id="082c9-160">Assigned To</span></span>
- <span data-ttu-id="082c9-161">Categoría</span><span class="sxs-lookup"><span data-stu-id="082c9-161">Category</span></span>
- <span data-ttu-id="082c9-162">Título</span><span class="sxs-lookup"><span data-stu-id="082c9-162">Title</span></span>
- <span data-ttu-id="082c9-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="082c9-163">Description</span></span>
- <span data-ttu-id="082c9-164">Fecha de creación</span><span class="sxs-lookup"><span data-stu-id="082c9-164">Created Date</span></span>
- <span data-ttu-id="082c9-165">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="082c9-165">Closed Date</span></span>
- <span data-ttu-id="082c9-166">Fecha de resolución</span><span class="sxs-lookup"><span data-stu-id="082c9-166">Resolved Date</span></span>
- <span data-ttu-id="082c9-167">Fecha de última modificación</span><span class="sxs-lookup"><span data-stu-id="082c9-167">Last Modified Date</span></span>
- <span data-ttu-id="082c9-168">Equipo</span><span class="sxs-lookup"><span data-stu-id="082c9-168">Computer</span></span>


<span data-ttu-id="082c9-169">**Elemento de trabajo:** **solicitudes de cambio**</span><span class="sxs-lookup"><span data-stu-id="082c9-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="082c9-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="082c9-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="082c9-171">**Fields**</span><span class="sxs-lookup"><span data-stu-id="082c9-171">**Fields**</span></span>
- <span data-ttu-id="082c9-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="082c9-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="082c9-173">Service Desk ID</span><span class="sxs-lookup"><span data-stu-id="082c9-173">Service Desk ID</span></span>
- <span data-ttu-id="082c9-174">Creado por</span><span class="sxs-lookup"><span data-stu-id="082c9-174">Created By</span></span>
- <span data-ttu-id="082c9-175">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="082c9-175">Closed By</span></span>
- <span data-ttu-id="082c9-176">Origen</span><span class="sxs-lookup"><span data-stu-id="082c9-176">Source</span></span>
- <span data-ttu-id="082c9-177">Asignado a</span><span class="sxs-lookup"><span data-stu-id="082c9-177">Assigned To</span></span>
- <span data-ttu-id="082c9-178">Título</span><span class="sxs-lookup"><span data-stu-id="082c9-178">Title</span></span>
- <span data-ttu-id="082c9-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="082c9-179">Type</span></span>
- <span data-ttu-id="082c9-180">Categoría</span><span class="sxs-lookup"><span data-stu-id="082c9-180">Category</span></span>
- <span data-ttu-id="082c9-181">Estado</span><span class="sxs-lookup"><span data-stu-id="082c9-181">State</span></span>
- <span data-ttu-id="082c9-182">Escalado</span><span class="sxs-lookup"><span data-stu-id="082c9-182">Escalation</span></span>
- <span data-ttu-id="082c9-183">Estado del conflicto</span><span class="sxs-lookup"><span data-stu-id="082c9-183">Conflict Status</span></span>
- <span data-ttu-id="082c9-184">Urgencia</span><span class="sxs-lookup"><span data-stu-id="082c9-184">Urgency</span></span>
- <span data-ttu-id="082c9-185">Prioridad</span><span class="sxs-lookup"><span data-stu-id="082c9-185">Priority</span></span>
- <span data-ttu-id="082c9-186">Riesgo</span><span class="sxs-lookup"><span data-stu-id="082c9-186">Risk</span></span>
- <span data-ttu-id="082c9-187">Impacto</span><span class="sxs-lookup"><span data-stu-id="082c9-187">Impact</span></span>
- <span data-ttu-id="082c9-188">Asignado a</span><span class="sxs-lookup"><span data-stu-id="082c9-188">Assigned To</span></span>
- <span data-ttu-id="082c9-189">Fecha de creación</span><span class="sxs-lookup"><span data-stu-id="082c9-189">Created Date</span></span>
- <span data-ttu-id="082c9-190">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="082c9-190">Closed Date</span></span>
- <span data-ttu-id="082c9-191">Fecha de última modificación</span><span class="sxs-lookup"><span data-stu-id="082c9-191">Last Modified Date</span></span>
- <span data-ttu-id="082c9-192">Fecha de solicitud</span><span class="sxs-lookup"><span data-stu-id="082c9-192">Requested Date</span></span>
- <span data-ttu-id="082c9-193">Fecha de inicio planeada</span><span class="sxs-lookup"><span data-stu-id="082c9-193">Planned Start Date</span></span>
- <span data-ttu-id="082c9-194">Fecha de finalización planeada</span><span class="sxs-lookup"><span data-stu-id="082c9-194">Planned End Date</span></span>
- <span data-ttu-id="082c9-195">Fecha de inicio del trabajo</span><span class="sxs-lookup"><span data-stu-id="082c9-195">Work Start Date</span></span>
- <span data-ttu-id="082c9-196">Fecha de finalización del trabajo</span><span class="sxs-lookup"><span data-stu-id="082c9-196">Work End Date</span></span>
- <span data-ttu-id="082c9-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="082c9-197">Description</span></span>
- <span data-ttu-id="082c9-198">Equipo</span><span class="sxs-lookup"><span data-stu-id="082c9-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="082c9-199">Datos de salida para un incidente de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="082c9-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="082c9-200">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-200">OMS field</span></span> | <span data-ttu-id="082c9-201">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="082c9-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="082c9-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="082c9-202">ServiceDeskId_s</span></span>| <span data-ttu-id="082c9-203">Number</span><span class="sxs-lookup"><span data-stu-id="082c9-203">Number</span></span> |
| <span data-ttu-id="082c9-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="082c9-204">IncidentState_s</span></span> | <span data-ttu-id="082c9-205">Estado</span><span class="sxs-lookup"><span data-stu-id="082c9-205">State</span></span> |
| <span data-ttu-id="082c9-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="082c9-206">Urgency_s</span></span> |<span data-ttu-id="082c9-207">Urgencia</span><span class="sxs-lookup"><span data-stu-id="082c9-207">Urgency</span></span> |
| <span data-ttu-id="082c9-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="082c9-208">Impact_s</span></span> |<span data-ttu-id="082c9-209">Impacto</span><span class="sxs-lookup"><span data-stu-id="082c9-209">Impact</span></span>|
| <span data-ttu-id="082c9-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="082c9-210">Priority_s</span></span> | <span data-ttu-id="082c9-211">Prioridad</span><span class="sxs-lookup"><span data-stu-id="082c9-211">Priority</span></span> |
| <span data-ttu-id="082c9-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="082c9-212">CreatedBy_s</span></span> | <span data-ttu-id="082c9-213">Abierto por</span><span class="sxs-lookup"><span data-stu-id="082c9-213">Opened by</span></span> |
| <span data-ttu-id="082c9-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="082c9-214">ResolvedBy_s</span></span> | <span data-ttu-id="082c9-215">Resuelto por</span><span class="sxs-lookup"><span data-stu-id="082c9-215">Resolved by</span></span>|
| <span data-ttu-id="082c9-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="082c9-216">ClosedBy_s</span></span>  | <span data-ttu-id="082c9-217">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="082c9-217">Closed by</span></span> |
| <span data-ttu-id="082c9-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="082c9-218">Source_s</span></span>| <span data-ttu-id="082c9-219">Tipo de contacto</span><span class="sxs-lookup"><span data-stu-id="082c9-219">Contact type</span></span> |
| <span data-ttu-id="082c9-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="082c9-220">AssignedTo_s</span></span> | <span data-ttu-id="082c9-221">Asignado a</span><span class="sxs-lookup"><span data-stu-id="082c9-221">Assigned to</span></span>  |
| <span data-ttu-id="082c9-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="082c9-222">Category_s</span></span> | <span data-ttu-id="082c9-223">Categoría</span><span class="sxs-lookup"><span data-stu-id="082c9-223">Category</span></span> |
| <span data-ttu-id="082c9-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="082c9-224">Title_s</span></span>|  <span data-ttu-id="082c9-225">Descripción breve</span><span class="sxs-lookup"><span data-stu-id="082c9-225">Short description</span></span> |
| <span data-ttu-id="082c9-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="082c9-226">Description_s</span></span>|  <span data-ttu-id="082c9-227">Notas</span><span class="sxs-lookup"><span data-stu-id="082c9-227">Notes</span></span> |
| <span data-ttu-id="082c9-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-228">CreatedDate_t</span></span>|  <span data-ttu-id="082c9-229">Abierto</span><span class="sxs-lookup"><span data-stu-id="082c9-229">Opened</span></span> |
| <span data-ttu-id="082c9-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-230">ClosedDate_t</span></span>| <span data-ttu-id="082c9-231">closed</span><span class="sxs-lookup"><span data-stu-id="082c9-231">closed</span></span>|
| <span data-ttu-id="082c9-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-232">ResolvedDate_t</span></span>|<span data-ttu-id="082c9-233">Resuelto</span><span class="sxs-lookup"><span data-stu-id="082c9-233">Resolved</span></span>|
| <span data-ttu-id="082c9-234">Equipo</span><span class="sxs-lookup"><span data-stu-id="082c9-234">Computer</span></span>  | <span data-ttu-id="082c9-235">Elemento de configuración</span><span class="sxs-lookup"><span data-stu-id="082c9-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="082c9-236">Datos de salida para una solicitud de cambio de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="082c9-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="082c9-237">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-237">OMS field</span></span> | <span data-ttu-id="082c9-238">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="082c9-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="082c9-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="082c9-239">ServiceDeskId_s</span></span>| <span data-ttu-id="082c9-240">Number</span><span class="sxs-lookup"><span data-stu-id="082c9-240">Number</span></span> |
| <span data-ttu-id="082c9-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="082c9-241">CreatedBy_s</span></span> | <span data-ttu-id="082c9-242">Solicitado por</span><span class="sxs-lookup"><span data-stu-id="082c9-242">Requested by</span></span> |
| <span data-ttu-id="082c9-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="082c9-243">ClosedBy_s</span></span> | <span data-ttu-id="082c9-244">Cerrado por</span><span class="sxs-lookup"><span data-stu-id="082c9-244">Closed by</span></span> |
| <span data-ttu-id="082c9-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="082c9-245">AssignedTo_s</span></span> | <span data-ttu-id="082c9-246">Asignado a</span><span class="sxs-lookup"><span data-stu-id="082c9-246">Assigned to</span></span>  |
| <span data-ttu-id="082c9-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="082c9-247">Title_s</span></span>|  <span data-ttu-id="082c9-248">Descripción breve</span><span class="sxs-lookup"><span data-stu-id="082c9-248">Short description</span></span> |
| <span data-ttu-id="082c9-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="082c9-249">Type_s</span></span>|  <span data-ttu-id="082c9-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="082c9-250">Type</span></span> |
| <span data-ttu-id="082c9-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="082c9-251">Category_s</span></span>|  <span data-ttu-id="082c9-252">Categoría</span><span class="sxs-lookup"><span data-stu-id="082c9-252">Catgory</span></span> |
| <span data-ttu-id="082c9-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="082c9-253">CRState_s</span></span>|  <span data-ttu-id="082c9-254">Estado</span><span class="sxs-lookup"><span data-stu-id="082c9-254">State</span></span>|
| <span data-ttu-id="082c9-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="082c9-255">Urgency_s</span></span>|  <span data-ttu-id="082c9-256">Urgencia</span><span class="sxs-lookup"><span data-stu-id="082c9-256">Urgency</span></span> |
| <span data-ttu-id="082c9-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="082c9-257">Priority_s</span></span>| <span data-ttu-id="082c9-258">Prioridad</span><span class="sxs-lookup"><span data-stu-id="082c9-258">Priority</span></span>|
| <span data-ttu-id="082c9-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="082c9-259">Risk_s</span></span>| <span data-ttu-id="082c9-260">Riesgo</span><span class="sxs-lookup"><span data-stu-id="082c9-260">Risk</span></span>|
| <span data-ttu-id="082c9-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="082c9-261">Impact_s</span></span>| <span data-ttu-id="082c9-262">Impacto</span><span class="sxs-lookup"><span data-stu-id="082c9-262">Impact</span></span>|
| <span data-ttu-id="082c9-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-263">RequestedDate_t</span></span>  | <span data-ttu-id="082c9-264">Solicitado por fecha</span><span class="sxs-lookup"><span data-stu-id="082c9-264">Requested by date</span></span> |
| <span data-ttu-id="082c9-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-265">ClosedDate_t</span></span> | <span data-ttu-id="082c9-266">Fecha de cierre</span><span class="sxs-lookup"><span data-stu-id="082c9-266">Closed date</span></span> |
| <span data-ttu-id="082c9-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="082c9-268">Fecha de inicio planeada</span><span class="sxs-lookup"><span data-stu-id="082c9-268">Planned start date</span></span> |
| <span data-ttu-id="082c9-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="082c9-270">Fecha de finalización planeada</span><span class="sxs-lookup"><span data-stu-id="082c9-270">Planned end date</span></span> |
| <span data-ttu-id="082c9-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-271">WorkStartDate_t</span></span>  | <span data-ttu-id="082c9-272">Fecha de inicio real</span><span class="sxs-lookup"><span data-stu-id="082c9-272">Actual start date</span></span> |
| <span data-ttu-id="082c9-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="082c9-273">WorkEndDate_t</span></span> | <span data-ttu-id="082c9-274">Fecha de finalización real</span><span class="sxs-lookup"><span data-stu-id="082c9-274">Actual end date</span></span>|
| <span data-ttu-id="082c9-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="082c9-275">Description_s</span></span> | <span data-ttu-id="082c9-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="082c9-276">Description</span></span> |
| <span data-ttu-id="082c9-277">Equipo</span><span class="sxs-lookup"><span data-stu-id="082c9-277">Computer</span></span>  | <span data-ttu-id="082c9-278">Elemento de configuración</span><span class="sxs-lookup"><span data-stu-id="082c9-278">Configuration Item</span></span> |

<span data-ttu-id="082c9-279">**Pantalla de Log Analytics de ejemplo para datos de ITSM:**</span><span class="sxs-lookup"><span data-stu-id="082c9-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="082c9-281">IT Service Management Connector: integración con otras soluciones de OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="082c9-282">IT Service Management Connector admite actualmente la integración con la solución Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="082c9-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="082c9-283">Mapa de servicio detecta automáticamente los componentes de la aplicación en sistemas Windows y Linux y asigna la comunicación entre servicios.</span><span class="sxs-lookup"><span data-stu-id="082c9-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="082c9-284">Permite ver los servidores a medida que piensa en ellos, como los sistemas interconectados que ofrecen servicios críticos.</span><span class="sxs-lookup"><span data-stu-id="082c9-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="082c9-285">Mapa de servicio muestra las conexiones entre servidores, procesos y puertos en cualquier arquitectura conectada TCP sin una configuración necesaria que sea distinta a la instalación de un agente.</span><span class="sxs-lookup"><span data-stu-id="082c9-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="082c9-286">Más información: [Mapa de servicio](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="082c9-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="082c9-287">Con esta integración, puede ver los elementos del departamento de servicios creados en la solución ITSM como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="082c9-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="082c9-288">Solución integrada</span><span class="sxs-lookup"><span data-stu-id="082c9-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="082c9-289">Creación de elementos de trabajo de ITSM para alertas de OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="082c9-290">Desde las alertas de OMS, puede crear elementos de trabajo asociados en los orígenes conectados de ITSM.</span><span class="sxs-lookup"><span data-stu-id="082c9-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="082c9-291">Para hacerlo, use el procedimiento siguiente:</span><span class="sxs-lookup"><span data-stu-id="082c9-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="082c9-292">En la ventana **Búsqueda de registros**, ejecute una consulta de búsqueda de registros para ver los datos.</span><span class="sxs-lookup"><span data-stu-id="082c9-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="082c9-293">Los resultados de la consulta son el origen de los elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="082c9-294">En **Búsqueda de registros**, haga clic en **Alerta** para abrir la página **Agregar regla de alerta**.</span><span class="sxs-lookup"><span data-stu-id="082c9-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Pantalla de Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="082c9-296">En la ventana **Agregar regla de alerta**, proporcione los detalles necesarios para **Nombre**, **Gravedad**, **Consulta de búsqueda** y **Criterios de alerta** (Ventana de tiempo/unidad métrica).</span><span class="sxs-lookup"><span data-stu-id="082c9-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="082c9-297">Seleccione **Sí** en **Acciones de ITSM**.</span><span class="sxs-lookup"><span data-stu-id="082c9-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="082c9-298">Seleccione la conexión de ITSM en la lista **Conexión seleccionada**.</span><span class="sxs-lookup"><span data-stu-id="082c9-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="082c9-299">Proporcione los detalles requeridos.</span><span class="sxs-lookup"><span data-stu-id="082c9-299">Provide the details as required.</span></span>
7. <span data-ttu-id="082c9-300">Para crear un elemento de trabajo independiente para cada entrada de registro de esta alerta, active la casilla **Crear elementos de trabajo individuales para cada entrada de registro**.</span><span class="sxs-lookup"><span data-stu-id="082c9-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="082c9-301">o</span><span class="sxs-lookup"><span data-stu-id="082c9-301">Or</span></span>

    <span data-ttu-id="082c9-302">deje desactivada esta casilla para crear solo un elemento de trabajo para cualquier número de entradas de registro en esta alerta.</span><span class="sxs-lookup"><span data-stu-id="082c9-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="082c9-303">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="082c9-303">Click **Save**.</span></span>

<span data-ttu-id="082c9-304">La alerta de OMS se creará en **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="082c9-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="082c9-305">Los elementos de trabajo de la conexión de ITSM correspondientes se crean cuando se cumple la condición de la alerta especificada.</span><span class="sxs-lookup"><span data-stu-id="082c9-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="082c9-306">Creación de elementos de trabajo de ITSM desde registros de OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="082c9-307">Puede crear elementos de trabajo en los orígenes conectados de ITSM a través de Búsqueda de registros de OMS.</span><span class="sxs-lookup"><span data-stu-id="082c9-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="082c9-308">Para hacerlo, use el procedimiento siguiente:</span><span class="sxs-lookup"><span data-stu-id="082c9-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="082c9-309">En **Búsqueda de registros**, busque los datos requeridos, seleccione el detalle y haga clic en **Crear elemento de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="082c9-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="082c9-310">Aparecerá la ventana **Creación de elemento de trabajo de ITSM**:</span><span class="sxs-lookup"><span data-stu-id="082c9-310">The **Create ITSM Work item** window appears:</span></span>

    ![Pantalla de Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="082c9-312">Agregue los detalles siguientes:</span><span class="sxs-lookup"><span data-stu-id="082c9-312">Add the following details:</span></span>

  - <span data-ttu-id="082c9-313">**Título de elemento de trabajo**: el título del elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="082c9-314">**Descripción de elemento de trabajo**: la descripción del nuevo elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="082c9-315">**Equipo afectado**: el nombre del equipo en que se encontraron estos datos de registro.</span><span class="sxs-lookup"><span data-stu-id="082c9-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="082c9-316">**Conexión seleccionada**: la conexión ITSM en la que desea crear este elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="082c9-317">**Elemento de trabajo**: tipo de elemento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="082c9-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="082c9-318">Para usar una plantilla de elemento de trabajo existente para un incidente, haga clic en **Sí** en la opción **Generate work item based on the template** (Generar elemento de trabajo basado en la plantilla) y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="082c9-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="082c9-319">O bien,</span><span class="sxs-lookup"><span data-stu-id="082c9-319">Or,</span></span>

    <span data-ttu-id="082c9-320">Haga clic en **No** si desea proporcionar valores personalizados.</span><span class="sxs-lookup"><span data-stu-id="082c9-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="082c9-321">Proporcione los valores adecuados en los cuadros de texto **Tipo de contacto**, **Impacto**, **Urgencia**, **Categoría** y **Subcategoría** y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="082c9-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="082c9-322">El elemento de trabajo se creará en ITSM, que también puede ver en OMS.</span><span class="sxs-lookup"><span data-stu-id="082c9-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="082c9-323">Solución de problemas de conexión de ITSM en OMS</span><span class="sxs-lookup"><span data-stu-id="082c9-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="082c9-324">Si se produce un error en la conexión de la interfaz de usuario del origen conectado y recibe el mensaje **Error al guardar la conexión**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="082c9-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="082c9-325">En el caso de conexiones de ServiceNow, Cherwell y Provance, asegúrese de que ha introducido correctamente el nombre de usuario y la contraseña, y el Id. y el secreto de cliente de cada una de las conexiones.</span><span class="sxs-lookup"><span data-stu-id="082c9-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="082c9-326">Si el error persiste, compruebe si dispone de privilegios suficientes en el producto ITSM correspondiente para realizar la conexión.</span><span class="sxs-lookup"><span data-stu-id="082c9-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="082c9-327">En el caso de Service Manager, asegúrese de que la aplicación web se implementa correctamente y se crea la conexión híbrida.</span><span class="sxs-lookup"><span data-stu-id="082c9-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="082c9-328">Para comprobar que la conexión se ha establecido correctamente con el equipo de Service Manager local, visite la dirección URL de la aplicación web como se detalla en la documentación para realizar la [conexión híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="082c9-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="082c9-329">Si los datos de ServiceNow no se sincronizan en OMS, asegúrese de que la instancia de ServiceNow no está suspendida.</span><span class="sxs-lookup"><span data-stu-id="082c9-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="082c9-330">Es posible que esto ocurra en algún momento en las instancias de ServiceNow Dev, cuando están inactivas.</span><span class="sxs-lookup"><span data-stu-id="082c9-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="082c9-331">En caso contrario, notifique el problema.</span><span class="sxs-lookup"><span data-stu-id="082c9-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="082c9-332">Si se generan alertas desde OMS pero no se están creando elementos de trabajo en el producto ITSM o bien no se están creando o vinculando elementos de configuración a los elementos de trabajo, o para cualquier información genérica, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="082c9-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="082c9-333">Se puede usar la solución de IT Service Management Connector en el portal de OMS para obtener un resumen de las conexiones, elementos de trabajo, equipos, etc. Haga clic en el mensaje de error en la hoja de estado, vaya a **Búsqueda de registros** y vea la conexión que tiene el error mediante el uso de los detalles del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="082c9-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="082c9-334">Puede ver directamente los errores y la información relacionada en la página **Búsqueda de registros** mediante *Type=ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="082c9-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="082c9-335">Solucionar problemas de implementación de aplicaciones web de Service Manager</span><span class="sxs-lookup"><span data-stu-id="082c9-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="082c9-336">En caso de que se produzcan problemas con la implementación de la aplicación web, asegúrese de que tener los permisos suficientes en la suscripción mencionada para crear o implementar recursos.</span><span class="sxs-lookup"><span data-stu-id="082c9-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="082c9-337">Si aparece el mensaje de error **Referencia a objeto no establecida como instancia de un objeto** mientras se ejecuta el [script](log-analytics-itsmc-service-manager-script.md), asegúrese de que especificó valores válidos en la sección **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="082c9-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="082c9-338">Si no puede crear el espacio de nombres de retransmisión de Service Bus, asegúrese de que el proveedor de recursos necesario está registrado en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="082c9-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="082c9-339">Si no está registrado, créelo manualmente desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="082c9-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="082c9-340">También puede crearlo mientras [crea la conexión híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="082c9-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="082c9-341">Ponerse en contacto con nosotros</span><span class="sxs-lookup"><span data-stu-id="082c9-341">Contact us</span></span>

<span data-ttu-id="082c9-342">Si tiene consultas o comentarios sobre IT Service Management, póngase en contacto con nosotros en [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="082c9-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="082c9-343">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="082c9-343">Next steps</span></span>
<span data-ttu-id="082c9-344">[Incorporación de productos o servicios de ITSM a IT Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="082c9-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
