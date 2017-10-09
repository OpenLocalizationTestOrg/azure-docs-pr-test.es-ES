---
title: "recuperación de aaaDisaster de cuenta de integración B2B; las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Recuperación ante desastres de Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="e5435-103">Recuperación ante desastres de Logic Apps B2B entre regiones</span><span class="sxs-lookup"><span data-stu-id="e5435-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="e5435-104">Las cargas de trabajo de B2B implican transacciones monetarias como pedidos y facturas.</span><span class="sxs-lookup"><span data-stu-id="e5435-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="e5435-105">Durante un desastre, es fundamental para un hello toomeet de negocios tooquickly recuperación que SLA de nivel de negocio acordados con sus socios.</span><span class="sxs-lookup"><span data-stu-id="e5435-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="e5435-106">En este artículo se muestra cómo planear toobuild una continuidad del negocio para cargas de trabajo de B2B.</span><span class="sxs-lookup"><span data-stu-id="e5435-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="e5435-107">Preparación para la recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="e5435-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="e5435-108">Conmutar por región toosecondary durante un evento de desastre</span><span class="sxs-lookup"><span data-stu-id="e5435-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="e5435-109">Revertir tooprimary región después de un evento de desastre</span><span class="sxs-lookup"><span data-stu-id="e5435-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="e5435-110">Preparación para la recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="e5435-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="e5435-111">Identificar una región secundaria y crear un [cuenta integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) en la región secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="e5435-112">Agregar socios comerciales, esquemas y acuerdos para flujos de mensajes de Hola necesario donde hello estado de ejecución necesita toobe replican toosecondary región integración cuenta.</span><span class="sxs-lookup"><span data-stu-id="e5435-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="e5435-113">Asegúrese de que hay coherencia en la convención de nomenclatura del artefacto de cuenta de hello integración entre las regiones.</span><span class="sxs-lookup"><span data-stu-id="e5435-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="e5435-114">Hola toopull estado de la ejecución de la región principal de hello, cree una aplicación de lógica en la región secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="e5435-115">Esta aplicación lógica debe tener un *desencadenador* y una *acción*.</span><span class="sxs-lookup"><span data-stu-id="e5435-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="e5435-116">desencadenador Hola debe conectarse la cuenta de integración de región tooprimary y acción de hello debe conectar con cuenta de integración de región de toosecondary.</span><span class="sxs-lookup"><span data-stu-id="e5435-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="e5435-117">En función de intervalo de tiempo de hello, desencadenador de Hola sondea la tabla de estado de la región principal ejecute hello y extrae los nuevos registros de hello, si existe.</span><span class="sxs-lookup"><span data-stu-id="e5435-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="e5435-118">acción de Hello las actualiza toosecondary cuenta de integración de región.</span><span class="sxs-lookup"><span data-stu-id="e5435-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="e5435-119">Esto ayuda a estado incremental en tiempo de ejecución de tooget desde una región principal toosecondary otra.</span><span class="sxs-lookup"><span data-stu-id="e5435-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="e5435-120">Continuidad del negocio en aplicaciones de lógica de la cuenta de integración es diseñado toosupport basada en protocolos B2B - X12, AS2 y EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5435-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="e5435-121">toofind los pasos detallados, seleccione Hola enlaces correspondientes.</span><span class="sxs-lookup"><span data-stu-id="e5435-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="e5435-122">Hola recomendación es toodeploy todos los recursos de la región principal en una región secundaria demasiado.</span><span class="sxs-lookup"><span data-stu-id="e5435-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="e5435-123">Recursos de la región principal incluyen base de datos de SQL Azure o base de datos de Azure Cosmos, Service Bus de Azure y concentradores de eventos de Azure utiliza para la mensajería, administración de API de Azure y la característica de Azure Logic Apps hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5435-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="e5435-124">Establecer una conexión de una región secundaria de tooa de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5435-125">Hola toopull estado de la ejecución de una región principal, cree una aplicación de lógica en una región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="e5435-126">aplicación de la lógica de Hello debe tener un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="e5435-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="e5435-127">desencadenador de Hello debe conectar tooa cuenta de integración de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="e5435-128">acción de Hello debe conectar tooa cuenta de integración de región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="e5435-129">En función de intervalo de tiempo de hello, desencadenador de Hola sondea la tabla de estado de la región principal ejecute hello y extrae los nuevos registros de hello, si existe.</span><span class="sxs-lookup"><span data-stu-id="e5435-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="e5435-130">acción de Hello las actualiza tooa cuenta de integración de región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="e5435-131">Este proceso ayuda a estado incremental en tiempo de ejecución de tooget desde región secundaria de hello región principal toohello.</span><span class="sxs-lookup"><span data-stu-id="e5435-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="e5435-132">Continuidad del negocio en una cuenta de integración de aplicaciones lógicas proporciona compatibilidad basada en protocolos de B2B hello X12, AS2 y EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5435-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="e5435-133">Para ver los pasos detallados sobre cómo usar X12 y AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) y [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e5435-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="e5435-134">Conmutar por región secundaria tooa durante un evento de desastre</span><span class="sxs-lookup"><span data-stu-id="e5435-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="e5435-135">Durante un evento de desastre, cuando no está disponible para la continuidad del negocio, región secundaria de dirigir el tráfico toohello región principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="e5435-136">Una región secundaria le ayuda a un toorecover empresariales rápidamente funciones hello toomeet RPO/RTO acordado con sus asociados.</span><span class="sxs-lookup"><span data-stu-id="e5435-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="e5435-137">También minimiza toofail esfuerzos a través de una región tooanother otra.</span><span class="sxs-lookup"><span data-stu-id="e5435-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="e5435-138">Hay una latencia esperada mientras se copiaban números de control de una región secundaria de tooa de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5435-139">tooavoid Enviar control generado duplicados números toopartners durante un evento de desastre, recomendación de hello es tooincrement números de control de hello en los contratos de la región secundaria de hello mediante [cmdlets de PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="e5435-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="e5435-140">Revertir el evento de desastre posterior a la región principal tooa</span><span class="sxs-lookup"><span data-stu-id="e5435-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="e5435-141">región principal de toofall tooa atrás cuando esté disponible, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e5435-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="e5435-142">Dejar de aceptar mensajes de socios en la región secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="e5435-143">Incrementar los números de control de hello generado para todos los contratos de la región principal de hello mediante el uso de [cmdlets de PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="e5435-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="e5435-144">Dirigir el tráfico de la región principal de hello región secundaria toohello.</span><span class="sxs-lookup"><span data-stu-id="e5435-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="e5435-145">Comprobar esa aplicación de lógica de hello creada en la región secundaria de Hola para extraer el estado de la ejecución de la región principal de Hola está habilitada.</span><span class="sxs-lookup"><span data-stu-id="e5435-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="e5435-146">X12</span><span class="sxs-lookup"><span data-stu-id="e5435-146">X12</span></span> 

<span data-ttu-id="e5435-147">La continuidad empresarial de los documentos EDI X12 se basa en los números de control:</span><span class="sxs-lookup"><span data-stu-id="e5435-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="e5435-148">También puede usar hello [X12 rápido iniciar plantilla](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="e5435-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="e5435-149">Creación de cuentas de integración principal y secundaria es plantillas de hello toouse de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="e5435-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="e5435-150">Hello plantilla ayuda toocreate dos aplicaciones de lógica, uno para números de control recibidos y otro para los números de control generado.</span><span class="sxs-lookup"><span data-stu-id="e5435-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="e5435-151">Acciones y desencadenadores respectivos se crean en las aplicaciones lógicas de hello, conexión de cuenta de hello desencadenador toohello integración principal y cuenta de hello acción toohello integración secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="e5435-152">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="e5435-152">**Prerequisites**</span></span>

<span data-ttu-id="e5435-153">recuperación ante desastres de tooenable para los mensajes entrantes, seleccione Configuración de comprobación de duplicados de hello en configuración de recepción del acuerdo de hello X12.</span><span class="sxs-lookup"><span data-stu-id="e5435-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Seleccionar comprobar la configuración duplicada](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="e5435-155">Cree una [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en una región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="e5435-156">Busque en **X12** y seleccione **X12: Cuando se modifica un número de control**.</span><span class="sxs-lookup"><span data-stu-id="e5435-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Búsqueda de X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="e5435-158">desencadenador de Hello solicita tooestablish una cuenta de conexión de integración tooan.</span><span class="sxs-lookup"><span data-stu-id="e5435-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5435-159">Hola desencadenador debe estar conectado tooa cuenta de integración de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="e5435-160">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="e5435-162">Hola **número sincronización de fecha y hora toostart control** configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="e5435-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="e5435-163">Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.</span><span class="sxs-lookup"><span data-stu-id="e5435-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="e5435-165">Seleccione **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="e5435-165">Select **New step** > **Add an action**.</span></span>

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="e5435-167">Busque en **X12** y seleccione **X12: Permite agregar o actualizar números de control**.</span><span class="sxs-lookup"><span data-stu-id="e5435-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Agregar o actualizar los números de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="e5435-169">tooconnect una cuenta de integración de acción tooa región secundaria, seleccione **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5435-170">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="e5435-172">Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="e5435-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="e5435-174">Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="e5435-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Campos de contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="e5435-176">Según el intervalo de tiempo de hello, desencadenador de hello sondea la tabla de números de control de región principal recibe hello y extrae los registros nuevos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="e5435-177">acción de Hello actualiza los registros de hello en la cuenta de integración de hello región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="e5435-178">Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.</span><span class="sxs-lookup"><span data-stu-id="e5435-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Tabla de número de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="e5435-180">En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica desde una región secundaria de tooa de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5435-181">Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio.</span><span class="sxs-lookup"><span data-stu-id="e5435-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="e5435-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="e5435-182">EDIFACT</span></span> 

<span data-ttu-id="e5435-183">La continuidad empresarial de los documentos EDI EDIFACT se basa en los números de control.</span><span class="sxs-lookup"><span data-stu-id="e5435-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="e5435-184">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="e5435-184">**Prerequisites**</span></span>

<span data-ttu-id="e5435-185">recuperación ante desastres de tooenable para los mensajes entrantes, seleccione Configuración de comprobación de duplicados de hello en configuración de recepción de su acuerdo EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5435-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Seleccionar comprobar la configuración duplicada](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="e5435-187">Cree una [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en una región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="e5435-188">Busque en **EDIFACT** y seleccione **EDIFACT: Cuando se modifica un número de control**.</span><span class="sxs-lookup"><span data-stu-id="e5435-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Búsqueda de EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="e5435-190">desencadenador de Hello solicita tooestablish una cuenta de conexión de integración tooan.</span><span class="sxs-lookup"><span data-stu-id="e5435-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5435-191">Hola desencadenador debe estar conectado tooa cuenta de integración de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="e5435-192">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="e5435-194">Hola **número sincronización de fecha y hora toostart control** configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="e5435-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="e5435-195">Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.</span><span class="sxs-lookup"><span data-stu-id="e5435-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="e5435-197">Seleccione **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="e5435-197">Select **New step** > **Add an action**.</span></span>    

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="e5435-199">Busque en **EDIFACT** y seleccione **EDIFACT: Permite agregar o actualizar números de control**.</span><span class="sxs-lookup"><span data-stu-id="e5435-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Agregar o actualizar los números de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="e5435-201">tooconnect una cuenta de integración de acción tooa región secundaria, seleccione **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5435-202">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="e5435-204">Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="e5435-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="e5435-206">Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="e5435-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Campos de contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="e5435-208">Según el intervalo de tiempo de hello, desencadenador de hello sondea la tabla de números de control de región principal recibe hello y extrae los registros nuevos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="e5435-209">acción de Hello actualiza cuenta de integración de hello registros toohello región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="e5435-210">Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.</span><span class="sxs-lookup"><span data-stu-id="e5435-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Tabla de número de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="e5435-212">En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica desde una región secundaria de tooa de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5435-213">Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio.</span><span class="sxs-lookup"><span data-stu-id="e5435-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="e5435-214">AS2</span><span class="sxs-lookup"><span data-stu-id="e5435-214">AS2</span></span> 

<span data-ttu-id="e5435-215">Continuidad del negocio en documentos que utilizan el protocolo de AS2 Hola se basa en el Id. de mensaje de Hola y el valor MIC Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="e5435-216">También puede usar hello [plantilla de inicio rápido de AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="e5435-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="e5435-217">Creación de cuentas de integración principal y secundaria es plantillas de hello toouse de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="e5435-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="e5435-218">plantilla de Hello le ayuda a crear una aplicación de lógica que tiene un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="e5435-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="e5435-219">aplicación de la lógica de Hello crea una conexión de una cuenta de desencadenador tooa integración principal y una cuenta de acción tooa integración secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="e5435-220">Crear un [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en la región secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="e5435-221">Busque en **AS2** y seleccione **AS2: Cuando se crea un valor MIC**.</span><span class="sxs-lookup"><span data-stu-id="e5435-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Búsqueda de AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="e5435-223">Un desencadenador le tooestablish una cuenta de conexión de integración tooan.</span><span class="sxs-lookup"><span data-stu-id="e5435-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5435-224">Hola desencadenador debe estar conectado tooa cuenta de integración de región principal.</span><span class="sxs-lookup"><span data-stu-id="e5435-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="e5435-225">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="e5435-227">Hola **sincronización de valor de fecha y hora toostart MIC** configuración es opcional.</span><span class="sxs-lookup"><span data-stu-id="e5435-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="e5435-228">Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.</span><span class="sxs-lookup"><span data-stu-id="e5435-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="e5435-230">Seleccione **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="e5435-230">Select **New step** > **Add an action**.</span></span>  

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="e5435-232">Busque en **AS2** y seleccione **AS2: Agregar o actualizar contenidos MIC**.</span><span class="sxs-lookup"><span data-stu-id="e5435-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Incorporación o actualización de MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="e5435-234">Seleccione una cuenta de acción de integración secundaria tooa tooconnect **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5435-235">Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5435-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="e5435-237">Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="e5435-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="e5435-239">Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="e5435-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="e5435-241">En función de intervalo de tiempo de hello, desencadenador de hello sondea la tabla de la región principal de Hola y extrae los registros nuevos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5435-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="e5435-242">acción de Hello las actualiza toohello cuenta de integración de región secundaria.</span><span class="sxs-lookup"><span data-stu-id="e5435-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="e5435-243">Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.</span><span class="sxs-lookup"><span data-stu-id="e5435-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Tabla de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="e5435-245">En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica de región secundaria de hello región principal toohello.</span><span class="sxs-lookup"><span data-stu-id="e5435-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="e5435-246">Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio.</span><span class="sxs-lookup"><span data-stu-id="e5435-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5435-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5435-247">Next steps</span></span>

[<span data-ttu-id="e5435-248">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="e5435-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

