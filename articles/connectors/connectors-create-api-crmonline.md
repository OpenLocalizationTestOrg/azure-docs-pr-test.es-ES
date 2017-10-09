---
title: "aaaConnect tooDynamics 365 (con conexión) de las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Crear la lógica de flujos de trabajo de aplicación que Administración entidades (online) de Dynamics 365 a través de la API proporcionada por el conector de Dynamics 365 Hola Hola"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="d47e4-103">Conectar tooDynamics 365 de flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="d47e4-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="d47e4-104">Con las aplicaciones lógicas, puede conectarse tooDynamics 365 (con conexión) y crear flujos empresariales útiles que crean registros, actualizan los elementos o devuelven una lista de registros.</span><span class="sxs-lookup"><span data-stu-id="d47e4-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="d47e4-105">Con el conector de hello Dynamics 365, puede:</span><span class="sxs-lookup"><span data-stu-id="d47e4-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="d47e4-106">Genera el flujo de negocios basado en datos de hello que obtendrá de Dynamics 365 (con conexión).</span><span class="sxs-lookup"><span data-stu-id="d47e4-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="d47e4-107">Use las acciones que obtención una respuesta y, a continuación, tome salida de hello disponibles para las demás acciones.</span><span class="sxs-lookup"><span data-stu-id="d47e4-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="d47e4-108">Por ejemplo, cuando se actualice un elemento en Dynamics 365 (en línea), puede enviar un correo electrónico mediante Office 365.</span><span class="sxs-lookup"><span data-stu-id="d47e4-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="d47e4-109">Este tema muestra cómo toocreate una lógica de aplicación que crea una tarea en Dynamics 365 cada vez que se crea un nuevo cliente potencial en Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="d47e4-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d47e4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d47e4-110">Prerequisites</span></span>
* <span data-ttu-id="d47e4-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d47e4-111">An Azure account.</span></span>
* <span data-ttu-id="d47e4-112">Una cuenta de Dynamics 365 (en línea).</span><span class="sxs-lookup"><span data-stu-id="d47e4-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="d47e4-113">Creación de una tarea cuando se crea un nuevo cliente potencial en Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="d47e4-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="d47e4-114">[Inicie sesión en tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d47e4-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="d47e4-115">En el cuadro de búsqueda de Azure de hello, escriba `Logic apps`, y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="d47e4-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Búsqueda de Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="d47e4-117">En **Logic Apps**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-117">Under **Logic apps**, click **Add**.</span></span>

      ![Agregar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="d47e4-119">aplicación de lógica de hello toocreate, Hola completa **nombre**, **suscripción**, **grupo de recursos**, y **ubicación** campos y, a continuación, haga clic en  **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="d47e4-120">Seleccione la aplicación lógica de la nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-120">Select hello new logic app.</span></span> <span data-ttu-id="d47e4-121">Cuando aparezca el Hola **se implementó correctamente** notificación, haga clic en **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="d47e4-122">En **Herramientas de desarrollo**, haga clic en **Diseñador de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="d47e4-123">En la lista de plantillas de hello, haga clic en **en blanco de lógica de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="d47e4-124">En el cuadro de búsqueda de hello, escriba `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="d47e4-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="d47e4-125">Desde Hola Dynamics 365 desencadena la lista, seleccione **Dynamics 365: cuando se crea un registro**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="d47e4-126">Si está toosign solicitada en tooDynamics 365, hágalo ahora.</span><span class="sxs-lookup"><span data-stu-id="d47e4-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="d47e4-127">En detalles de desencadenador de hello, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d47e4-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="d47e4-128">**Nombre de la organización**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-128">**Organization Name**.</span></span> <span data-ttu-id="d47e4-129">Seleccione la instancia de Dynamics 365 de Hola que desee toolisten de aplicación lógica de Hola a.</span><span class="sxs-lookup"><span data-stu-id="d47e4-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="d47e4-130">**Nombre de entidad**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-130">**Entity Name**.</span></span> <span data-ttu-id="d47e4-131">Seleccione la entidad de Hola que desee toolisten a.</span><span class="sxs-lookup"><span data-stu-id="d47e4-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="d47e4-132">Este evento actúa como una aplicación de lógica de desencadenador toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="d47e4-133">En este tutorial está seleccionado **Leads**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="d47e4-134">**¿Con qué frecuencia desea toocheck para elementos?**</span><span class="sxs-lookup"><span data-stu-id="d47e4-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="d47e4-135">Estos valores se configuran la frecuencia con aplicación de lógica de hello busca desencadenador toohello relacionadas de las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="d47e4-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="d47e4-136">saludo predeterminado es toocheck actualizaciones cada tres minutos.</span><span class="sxs-lookup"><span data-stu-id="d47e4-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="d47e4-137">**Frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-137">**Frequency**.</span></span> <span data-ttu-id="d47e4-138">Seleccione segundos, minutos, horas o días.</span><span class="sxs-lookup"><span data-stu-id="d47e4-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="d47e4-139">**Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-139">**Interval**.</span></span> <span data-ttu-id="d47e4-140">Escriba Hola número de segundos, minutos, horas o días en los que desee toopass antes de la siguiente comprobación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Detalles del desencadenador de aplicación lógica](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="d47e4-142">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="d47e4-143">En el cuadro de búsqueda de hello, escriba `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="d47e4-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="d47e4-144">En la lista de acciones de hello, seleccione **Dynamics 365: crear un nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="d47e4-145">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d47e4-145">Enter hello following information:</span></span>

    * <span data-ttu-id="d47e4-146">**Nombre de la organización**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-146">**Organization Name**.</span></span> <span data-ttu-id="d47e4-147">Seleccione la instancia de hello Dynamics 365 donde desea que el registro de hello flujo toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="d47e4-148">Observe que esta instancia no tiene toobe Hola misma instancia donde se desencadena el evento de Hola de.</span><span class="sxs-lookup"><span data-stu-id="d47e4-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="d47e4-149">**Nombre de entidad**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-149">**Entity Name**.</span></span> <span data-ttu-id="d47e4-150">Seleccione la entidad de Hola que desea toocreate un registro cuando se desencadene el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="d47e4-151">En este tutorial está seleccionado **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="d47e4-152">Haga clic en hello **asunto** cuadro que aparece.</span><span class="sxs-lookup"><span data-stu-id="d47e4-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="d47e4-153">De hello contenido lista dinámica que aparece, puede seleccionar cualquiera de estos campos:</span><span class="sxs-lookup"><span data-stu-id="d47e4-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="d47e4-154">**Apellido**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-154">**Last Name**.</span></span> <span data-ttu-id="d47e4-155">Al seleccionar este campo inserta last name de Hola de hello responsable campo Asunto Hola tarea hello, cuando se crea el registro de la tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="d47e4-156">**Tema**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-156">**Topic**.</span></span> <span data-ttu-id="d47e4-157">Seleccionar este campo inserciones Hola tema campo cliente potencial de hello en el campo de asunto de hello para la tarea hello, cuando se crea registro de tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="d47e4-158">Haga clic en **tema** tooadd ese toohello **asunto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="d47e4-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Creación de detalles del nuevo registro en la aplicación lógica](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="d47e4-160">En la barra de herramientas del Diseñador de la aplicación lógica hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="d47e4-162">Hola toostart lógica de aplicación, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-162">toostart hello Logic App, click **Run**.</span></span>

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="d47e4-164">Ahora cree un registro de cliente potencial en Dynamics 365 para Ventas y podrá ver el flujo en acción.</span><span class="sxs-lookup"><span data-stu-id="d47e4-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="d47e4-165">Establecimiento de opciones avanzadas para un paso de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="d47e4-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="d47e4-166">toospecify cómo toofilter datos en un paso de aplicación lógica, haga clic en **Mostrar opciones avanzadas** en ese paso, a continuación, agregue un filtro o un pedido por consulta.</span><span class="sxs-lookup"><span data-stu-id="d47e4-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="d47e4-167">Por ejemplo, puede usar un filtro consulta tooget sólo las cuentas activas y se ordena por nombre de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="d47e4-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="d47e4-168">tooperform esta tarea, escriba la consulta de filtro de OData de hello `statuscode eq 1`y seleccione **nombre de la cuenta** de lista de contenido dinámico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="d47e4-169">Para más información consulte: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) y [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="d47e4-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Opciones avanzadas de la aplicación lógica](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="d47e4-171">Procedimientos recomendados al usar las opciones avanzadas</span><span class="sxs-lookup"><span data-stu-id="d47e4-171">Best practices when using advanced options</span></span>

<span data-ttu-id="d47e4-172">Cuando se agrega un campo de valor tooa, debe coincidir con el tipo de campo de hello si escribe un valor o seleccione un valor de la lista de contenido dinámico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="d47e4-173">Tipo de campo</span><span class="sxs-lookup"><span data-stu-id="d47e4-173">Field type</span></span>  |<span data-ttu-id="d47e4-174">Cómo toouse</span><span class="sxs-lookup"><span data-stu-id="d47e4-174">How toouse</span></span>  |<span data-ttu-id="d47e4-175">Donde toofind</span><span class="sxs-lookup"><span data-stu-id="d47e4-175">Where toofind</span></span>  |<span data-ttu-id="d47e4-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="d47e4-176">Name</span></span>  |<span data-ttu-id="d47e4-177">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="d47e4-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="d47e4-178">Campos de texto</span><span class="sxs-lookup"><span data-stu-id="d47e4-178">Text fields</span></span>|<span data-ttu-id="d47e4-179">Los campos de texto requieren una sola línea de texto o contenido dinámico que sea un campo de tipo texto.</span><span class="sxs-lookup"><span data-stu-id="d47e4-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="d47e4-180">Algunos ejemplos son campos de categoría y subcategoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="d47e4-181">Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos</span><span class="sxs-lookup"><span data-stu-id="d47e4-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="d47e4-182">categoría</span><span class="sxs-lookup"><span data-stu-id="d47e4-182">category</span></span> |<span data-ttu-id="d47e4-183">Línea de texto única</span><span class="sxs-lookup"><span data-stu-id="d47e4-183">Single Line of Text</span></span>        
<span data-ttu-id="d47e4-184">Campos numéricos enteros</span><span class="sxs-lookup"><span data-stu-id="d47e4-184">Integer fields</span></span> | <span data-ttu-id="d47e4-185">Algunos campos requieren un número entero o un contenido dinámico que sea un campo de tipo numérico entero.</span><span class="sxs-lookup"><span data-stu-id="d47e4-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="d47e4-186">Algunos ejemplos son Porcentaje completado y Duración.</span><span class="sxs-lookup"><span data-stu-id="d47e4-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="d47e4-187">Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos</span><span class="sxs-lookup"><span data-stu-id="d47e4-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="d47e4-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="d47e4-188">percentcomplete</span></span> |<span data-ttu-id="d47e4-189">Número entero</span><span class="sxs-lookup"><span data-stu-id="d47e4-189">Whole Number</span></span>         
<span data-ttu-id="d47e4-190">Campos de fecha</span><span class="sxs-lookup"><span data-stu-id="d47e4-190">Date fields</span></span> | <span data-ttu-id="d47e4-191">Algunos campos, requieren una fecha escrita en formato mm/dd/aaaa o contenido dinámico que sea un campo de tipo de fecha.</span><span class="sxs-lookup"><span data-stu-id="d47e4-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="d47e4-192">Algunos ejemplos son fecha de creación, fecha de inicio, inicio real, último periodo de retención, finalización real y fecha de vencimiento.</span><span class="sxs-lookup"><span data-stu-id="d47e4-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="d47e4-193">Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos</span><span class="sxs-lookup"><span data-stu-id="d47e4-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="d47e4-194">createdon</span><span class="sxs-lookup"><span data-stu-id="d47e4-194">createdon</span></span> |<span data-ttu-id="d47e4-195">Fecha y hora</span><span class="sxs-lookup"><span data-stu-id="d47e4-195">Date and Time</span></span>
<span data-ttu-id="d47e4-196">Campos que requieren un identificador de registro y un tipo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="d47e4-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="d47e4-197">Algunos campos que hacen referencia a otro registro de entidad requieren Id. de registro de hello y tipo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="d47e4-198">Configuración > personalizaciones > Personalizar Hola sistema > entidades > cuenta > campos</span><span class="sxs-lookup"><span data-stu-id="d47e4-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="d47e4-199">accountid</span><span class="sxs-lookup"><span data-stu-id="d47e4-199">accountid</span></span>  | <span data-ttu-id="d47e4-200">Clave principal</span><span class="sxs-lookup"><span data-stu-id="d47e4-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="d47e4-201">Más ejemplos de campos que requieren tanto un identificador de registro como un tipo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="d47e4-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="d47e4-202">Expandir en la tabla anterior de hello, presentamos más ejemplos de campos que no funcionan con los valores seleccionados de la lista de contenido dinámico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="d47e4-203">En su lugar, estos campos requieren tanto un Id. y búsqueda de tipo de registro especificado en los campos de hello en PowerApps.</span><span class="sxs-lookup"><span data-stu-id="d47e4-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="d47e4-204">Propietario y Tipo de propietario.</span><span class="sxs-lookup"><span data-stu-id="d47e4-204">Owner and Owner Type.</span></span> <span data-ttu-id="d47e4-205">campo de propietario de Hello debe ser un identificador válido usuario o equipo de registro.</span><span class="sxs-lookup"><span data-stu-id="d47e4-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="d47e4-206">Hola, tipo de propietario debe ser **systemusers** o **equipos**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="d47e4-207">Cliente y Tipo de cliente.</span><span class="sxs-lookup"><span data-stu-id="d47e4-207">Customer and Customer Type.</span></span> <span data-ttu-id="d47e4-208">campo de cliente Hello debe ser una cuenta válida o póngase en contacto con el identificador de registro.</span><span class="sxs-lookup"><span data-stu-id="d47e4-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="d47e4-209">Hola, tipo de propietario debe ser **cuentas** o **contactos**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="d47e4-210">Referente a y Tipo referente a.</span><span class="sxs-lookup"><span data-stu-id="d47e4-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="d47e4-211">Hola en relación con el campo debe ser un identificador de registro válido, como una cuenta o póngase en contacto con el identificador de registro.</span><span class="sxs-lookup"><span data-stu-id="d47e4-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="d47e4-212">Hello en relación con tipo debe ser Hola búsqueda para registro de hello, como **cuentas** o **contactos**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="d47e4-213">Hello siguiente ejemplo de acción de creación de tarea agrega un registro de cuenta que se corresponde el Id. de registro de toohello agregar toohello con respecto a los campos de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="d47e4-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="d47e4-215">En este ejemplo también asigna a hello tooa específico usuario de la tarea en función de Id. de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="d47e4-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="d47e4-217">toofind un registro del identificador, consulte los pasos de la sección de Hola: *encuentra el Id. de registro de hello*</span><span class="sxs-lookup"><span data-stu-id="d47e4-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="d47e4-218">Encuentra el Id. de registro de hello</span><span class="sxs-lookup"><span data-stu-id="d47e4-218">Find hello record ID</span></span>

1. <span data-ttu-id="d47e4-219">Abra un registro, como un registro de cuenta.</span><span class="sxs-lookup"><span data-stu-id="d47e4-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="d47e4-220">En la barra de herramientas de hello acciones, haga clic en **emergente** ![registro emergente](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="d47e4-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="d47e4-221">O bien, en barra de herramientas de acciones de hello, toocopy Hola dirección URL completa en el programa de correo electrónico predeterminado, haga clic en **correo electrónico un vínculo**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="d47e4-222">Id. de registro de Hello se muestra entre Hola 7b y %7 %d) la codificación de caracteres de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="d47e4-224">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d47e4-224">Troubleshooting</span></span>
<span data-ttu-id="d47e4-225">tootroubleshoot un paso con errores en una aplicación de lógica, ver detalles de estado de Hola de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="d47e4-226">En **Logic Apps**, seleccione la aplicación lógica y haga clic en **Información general**.</span><span class="sxs-lookup"><span data-stu-id="d47e4-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="d47e4-227">Hola área de resumen se muestra y proporciona Hola ejecutar el estado de aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="d47e4-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Estado de ejecución de la aplicación lógica](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="d47e4-229">tooview obtener más información acerca de todas las ejecuciones de error, haga clic en hello no se pudo eventos.</span><span class="sxs-lookup"><span data-stu-id="d47e4-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="d47e4-230">tooexpand un paso con errores, haga clic en ese paso.</span><span class="sxs-lookup"><span data-stu-id="d47e4-230">tooexpand a failed step, click that step.</span></span>

   ![Expansión del paso con errores](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="d47e4-232">detalles de pasos de Hello aparecen y pueden ayudar a solucionar Hola causa del error de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47e4-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Detalles del paso con errores](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="d47e4-234">Para más información sobre cómo solucionar problemas de las aplicaciones lógicas, consulte [Diagnóstico de errores de aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="d47e4-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="d47e4-235">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="d47e4-235">Connector-specific details</span></span>

<span data-ttu-id="d47e4-236">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="d47e4-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d47e4-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d47e4-237">Next steps</span></span>
<span data-ttu-id="d47e4-238">Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d47e4-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
