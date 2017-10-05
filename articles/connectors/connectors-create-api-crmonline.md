---
title: "Conexión a Dynamics 365 (en línea) desde Azure Logic Apps | Microsoft Docs"
description: "Creación de flujos de trabajo de aplicación lógica para administrar entidades de Dynamics 365 (en línea) a través de la API proporcionada por el conector de Dynamics 365"
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
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="fca54-103">Conexión a Dynamics 365 desde flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fca54-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="fca54-104">Con Logic Apps puede conectarse a Dynamics 365 (en línea) y crear flujos de negocio útiles que creen registros, actualicen elementos o devuelvan una lista de registros.</span><span class="sxs-lookup"><span data-stu-id="fca54-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="fca54-105">Con el conector de Dynamics 365, puede:</span><span class="sxs-lookup"><span data-stu-id="fca54-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="fca54-106">Compilar el flujo de negocio en función de los datos que obtiene de Dynamics 365 (en línea).</span><span class="sxs-lookup"><span data-stu-id="fca54-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="fca54-107">Usar acciones que obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="fca54-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="fca54-108">Por ejemplo, cuando se actualice un elemento en Dynamics 365 (en línea), puede enviar un correo electrónico mediante Office 365.</span><span class="sxs-lookup"><span data-stu-id="fca54-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="fca54-109">En este tema se muestra cómo crear una aplicación lógica que crea una tarea en Dynamics 365 cada vez que se crea un nuevo cliente potencial en Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="fca54-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fca54-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fca54-110">Prerequisites</span></span>
* <span data-ttu-id="fca54-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fca54-111">An Azure account.</span></span>
* <span data-ttu-id="fca54-112">Una cuenta de Dynamics 365 (en línea).</span><span class="sxs-lookup"><span data-stu-id="fca54-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="fca54-113">Creación de una tarea cuando se crea un nuevo cliente potencial en Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="fca54-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="fca54-114">[Inicie de sesión en Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fca54-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="fca54-115">En el cuadro de búsqueda de Azure, escriba `Logic apps` y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="fca54-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Búsqueda de Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="fca54-117">En **Logic Apps**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fca54-117">Under **Logic apps**, click **Add**.</span></span>

      ![Agregar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="fca54-119">Para crear la aplicación lógica, rellene los campos **Nombre**, **Suscripción**, **Grupo de recursos** y **Ubicación**, y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fca54-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="fca54-120">Seleccione la nueva aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fca54-120">Select the new logic app.</span></span> <span data-ttu-id="fca54-121">Cuando reciba la notificación **Implementación correcta**, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="fca54-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="fca54-122">En **Herramientas de desarrollo**, haga clic en **Diseñador de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="fca54-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="fca54-123">En la lista de plantillas, haga clic en **Aplicación lógica en blanco**.</span><span class="sxs-lookup"><span data-stu-id="fca54-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="fca54-124">En el cuadro de búsqueda, escriba `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="fca54-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="fca54-125">En la lista de desencadenadores de Dynamics 365, seleccione **Dynamics 365: Al crear un registro**.</span><span class="sxs-lookup"><span data-stu-id="fca54-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="fca54-126">Si se le pide que inicie sesión en Dynamics 365, hágalo.</span><span class="sxs-lookup"><span data-stu-id="fca54-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="fca54-127">Escriba la información a continuación en los detalles del desencadenador:</span><span class="sxs-lookup"><span data-stu-id="fca54-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="fca54-128">**Nombre de la organización**.</span><span class="sxs-lookup"><span data-stu-id="fca54-128">**Organization Name**.</span></span> <span data-ttu-id="fca54-129">Seleccione la instancia de Dynamics 365 a la que desea que la aplicación lógica escuche.</span><span class="sxs-lookup"><span data-stu-id="fca54-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="fca54-130">**Nombre de entidad**.</span><span class="sxs-lookup"><span data-stu-id="fca54-130">**Entity Name**.</span></span> <span data-ttu-id="fca54-131">Seleccione la entidad que desea escuchar.</span><span class="sxs-lookup"><span data-stu-id="fca54-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="fca54-132">Este evento actúa como desencadenador para iniciar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fca54-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="fca54-133">En este tutorial está seleccionado **Leads**.</span><span class="sxs-lookup"><span data-stu-id="fca54-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="fca54-134">**¿Con qué frecuencia quiere comprobar elementos?**</span><span class="sxs-lookup"><span data-stu-id="fca54-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="fca54-135">Estos valores configuran la frecuencia con la que la aplicación lógica busca actualizaciones relacionadas con el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="fca54-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="fca54-136">El valor predeterminado es comprobar si hay actualizaciones cada tres minutos.</span><span class="sxs-lookup"><span data-stu-id="fca54-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="fca54-137">**Frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="fca54-137">**Frequency**.</span></span> <span data-ttu-id="fca54-138">Seleccione segundos, minutos, horas o días.</span><span class="sxs-lookup"><span data-stu-id="fca54-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="fca54-139">**Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="fca54-139">**Interval**.</span></span> <span data-ttu-id="fca54-140">Escriba el número de segundos, minutos, horas o días que deben pasar para la siguiente comprobación.</span><span class="sxs-lookup"><span data-stu-id="fca54-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Detalles del desencadenador de aplicación lógica](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="fca54-142">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="fca54-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="fca54-143">En el cuadro de búsqueda, escriba `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="fca54-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="fca54-144">En la lista de acciones, seleccione **Dynamics 365: Crear un nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="fca54-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="fca54-145">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="fca54-145">Enter the following information:</span></span>

    * <span data-ttu-id="fca54-146">**Nombre de la organización**.</span><span class="sxs-lookup"><span data-stu-id="fca54-146">**Organization Name**.</span></span> <span data-ttu-id="fca54-147">Seleccione la instancia de Dynamics 365 en la que desea que el flujo cree el registro.</span><span class="sxs-lookup"><span data-stu-id="fca54-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="fca54-148">Tenga en cuenta que no tiene que ser la misma instancia desde la que se desencadena el evento.</span><span class="sxs-lookup"><span data-stu-id="fca54-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="fca54-149">**Nombre de entidad**.</span><span class="sxs-lookup"><span data-stu-id="fca54-149">**Entity Name**.</span></span> <span data-ttu-id="fca54-150">Seleccione la entidad que desea que cree un registro cuando se desencadene el evento.</span><span class="sxs-lookup"><span data-stu-id="fca54-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="fca54-151">En este tutorial está seleccionado **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="fca54-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="fca54-152">Haga clic en el cuadro **Asunto** que aparece.</span><span class="sxs-lookup"><span data-stu-id="fca54-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="fca54-153">En la lista de contenido dinámica que aparece, puede seleccionar cualquiera de estos campos:</span><span class="sxs-lookup"><span data-stu-id="fca54-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="fca54-154">**Apellido**.</span><span class="sxs-lookup"><span data-stu-id="fca54-154">**Last Name**.</span></span> <span data-ttu-id="fca54-155">Al seleccionar este campo, se inserta el apellido del cliente potencial en el campo de Asunto de la tarea, cuando se cree el registro de tareas.</span><span class="sxs-lookup"><span data-stu-id="fca54-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="fca54-156">**Tema**.</span><span class="sxs-lookup"><span data-stu-id="fca54-156">**Topic**.</span></span> <span data-ttu-id="fca54-157">Al seleccionar este campo, se inserta el campo Tema del cliente potencial en el campo de Asunto de la tarea, cuando se cree el registro de tareas.</span><span class="sxs-lookup"><span data-stu-id="fca54-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="fca54-158">Haga clic en **Tema** para agregarlo al cuadro **Asunto**.</span><span class="sxs-lookup"><span data-stu-id="fca54-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Creación de detalles del nuevo registro en la aplicación lógica](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="fca54-160">Haga clic en **Guardar** en la barra de herramientas del Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fca54-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="fca54-162">Para iniciar la aplicación lógica, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="fca54-162">To start the Logic App, click **Run**.</span></span>

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="fca54-164">Ahora cree un registro de cliente potencial en Dynamics 365 para Ventas y podrá ver el flujo en acción.</span><span class="sxs-lookup"><span data-stu-id="fca54-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="fca54-165">Establecimiento de opciones avanzadas para un paso de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fca54-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="fca54-166">Para especificar cómo filtrar datos en un paso de la aplicación de lógica, haga clic en **Mostrar opciones avanzadas** en ese paso y agregue un filtro u ordenar por consulta.</span><span class="sxs-lookup"><span data-stu-id="fca54-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="fca54-167">Por ejemplo, puede usar una consulta de filtro para recuperar solo cuentas activas y ordenar según el nombre de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="fca54-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="fca54-168">Para realizar esta tarea, escriba la consulta de filtro OData `statuscode eq 1` y seleccione **Nombre de cuenta** en la lista de contenido dinámica.</span><span class="sxs-lookup"><span data-stu-id="fca54-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="fca54-169">Para más información consulte: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) y [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="fca54-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Opciones avanzadas de la aplicación lógica](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="fca54-171">Procedimientos recomendados al usar las opciones avanzadas</span><span class="sxs-lookup"><span data-stu-id="fca54-171">Best practices when using advanced options</span></span>

<span data-ttu-id="fca54-172">Cuando agregue un valor a un campo, el tipo de campo tiene que coincidir, tanto si escribe el valor como si lo selecciona de la lista de contenido dinámica.</span><span class="sxs-lookup"><span data-stu-id="fca54-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="fca54-173">Tipo de campo</span><span class="sxs-lookup"><span data-stu-id="fca54-173">Field type</span></span>  |<span data-ttu-id="fca54-174">Modo de uso</span><span class="sxs-lookup"><span data-stu-id="fca54-174">How to use</span></span>  |<span data-ttu-id="fca54-175">Dónde encontrarlo</span><span class="sxs-lookup"><span data-stu-id="fca54-175">Where to find</span></span>  |<span data-ttu-id="fca54-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="fca54-176">Name</span></span>  |<span data-ttu-id="fca54-177">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="fca54-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="fca54-178">Campos de texto</span><span class="sxs-lookup"><span data-stu-id="fca54-178">Text fields</span></span>|<span data-ttu-id="fca54-179">Los campos de texto requieren una sola línea de texto o contenido dinámico que sea un campo de tipo texto.</span><span class="sxs-lookup"><span data-stu-id="fca54-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="fca54-180">Algunos ejemplos son los campos de categoría y subcategoría.</span><span class="sxs-lookup"><span data-stu-id="fca54-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="fca54-181">Configuración > Personalizaciones > Personalizar el sistema > Entidades > Tarea > Campos</span><span class="sxs-lookup"><span data-stu-id="fca54-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="fca54-182">categoría</span><span class="sxs-lookup"><span data-stu-id="fca54-182">category</span></span> |<span data-ttu-id="fca54-183">Línea de texto única</span><span class="sxs-lookup"><span data-stu-id="fca54-183">Single Line of Text</span></span>        
<span data-ttu-id="fca54-184">Campos numéricos enteros</span><span class="sxs-lookup"><span data-stu-id="fca54-184">Integer fields</span></span> | <span data-ttu-id="fca54-185">Algunos campos requieren un número entero o un contenido dinámico que sea un campo de tipo numérico entero.</span><span class="sxs-lookup"><span data-stu-id="fca54-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="fca54-186">Algunos ejemplos son Porcentaje completado y Duración.</span><span class="sxs-lookup"><span data-stu-id="fca54-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="fca54-187">Configuración > Personalizaciones > Personalizar el sistema > Entidades > Tarea > Campos</span><span class="sxs-lookup"><span data-stu-id="fca54-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="fca54-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="fca54-188">percentcomplete</span></span> |<span data-ttu-id="fca54-189">Número entero</span><span class="sxs-lookup"><span data-stu-id="fca54-189">Whole Number</span></span>         
<span data-ttu-id="fca54-190">Campos de fecha</span><span class="sxs-lookup"><span data-stu-id="fca54-190">Date fields</span></span> | <span data-ttu-id="fca54-191">Algunos campos, requieren una fecha escrita en formato mm/dd/aaaa o contenido dinámico que sea un campo de tipo de fecha.</span><span class="sxs-lookup"><span data-stu-id="fca54-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="fca54-192">Algunos ejemplos son fecha de creación, fecha de inicio, inicio real, último periodo de retención, finalización real y fecha de vencimiento.</span><span class="sxs-lookup"><span data-stu-id="fca54-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="fca54-193">Configuración > Personalizaciones > Personalizar el sistema > Entidades > Tarea > Campos</span><span class="sxs-lookup"><span data-stu-id="fca54-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="fca54-194">createdon</span><span class="sxs-lookup"><span data-stu-id="fca54-194">createdon</span></span> |<span data-ttu-id="fca54-195">Fecha y hora</span><span class="sxs-lookup"><span data-stu-id="fca54-195">Date and Time</span></span>
<span data-ttu-id="fca54-196">Campos que requieren un identificador de registro y un tipo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="fca54-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="fca54-197">Algunos campos que hacen referencia a otro registro de entidad requieren el identificador de registro y el tipo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="fca54-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="fca54-198">Configuración > Personalizaciones > Personalizar el sistema > Entidades > Cuenta > Campos</span><span class="sxs-lookup"><span data-stu-id="fca54-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="fca54-199">accountid</span><span class="sxs-lookup"><span data-stu-id="fca54-199">accountid</span></span>  | <span data-ttu-id="fca54-200">Clave principal</span><span class="sxs-lookup"><span data-stu-id="fca54-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="fca54-201">Más ejemplos de campos que requieren tanto un identificador de registro como un tipo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="fca54-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="fca54-202">Ampliando la tabla anterior, aquí tiene más ejemplos de campos que no funcionan con valores seleccionados de la lista de contenido dinámica.</span><span class="sxs-lookup"><span data-stu-id="fca54-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="fca54-203">En su lugar, estos campos requieren tanto un identificador de registro como un tipo de búsqueda especificados en los campos en PowerApps.</span><span class="sxs-lookup"><span data-stu-id="fca54-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="fca54-204">Propietario y Tipo de propietario.</span><span class="sxs-lookup"><span data-stu-id="fca54-204">Owner and Owner Type.</span></span> <span data-ttu-id="fca54-205">El campo Propietario tiene que ser un usuario válido o un identificador de registro de equipo.</span><span class="sxs-lookup"><span data-stu-id="fca54-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="fca54-206">El Tipo de propietario tiene que ser **systemusers** o **equipos**.</span><span class="sxs-lookup"><span data-stu-id="fca54-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="fca54-207">Cliente y Tipo de cliente.</span><span class="sxs-lookup"><span data-stu-id="fca54-207">Customer and Customer Type.</span></span> <span data-ttu-id="fca54-208">El campo Cliente tiene que ser una cuenta válida o un identificador de registro de contacto.</span><span class="sxs-lookup"><span data-stu-id="fca54-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="fca54-209">El Tipo de propietario tiene que ser **cuentas** o **contactos**.</span><span class="sxs-lookup"><span data-stu-id="fca54-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="fca54-210">Referente a y Tipo referente a.</span><span class="sxs-lookup"><span data-stu-id="fca54-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="fca54-211">El campo Referente a tiene que ser un identificador de registro válido, como una cuenta o un identificador de registro de contacto.</span><span class="sxs-lookup"><span data-stu-id="fca54-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="fca54-212">El Tipo referente a tiene que ser el tipo de búsqueda para el registro, como **cuentas** o **contactos**.</span><span class="sxs-lookup"><span data-stu-id="fca54-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="fca54-213">El siguiente ejemplo de acción de creación de tarea agrega un registro de cuenta que corresponde al identificador de registro, agregándolo al campo Referente a de la tarea.</span><span class="sxs-lookup"><span data-stu-id="fca54-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="fca54-215">Este ejemplo también asigna la tarea a un usuario específico basado en el identificador de registro. del usuario.</span><span class="sxs-lookup"><span data-stu-id="fca54-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="fca54-217">Para obtener un identificador de registro, consulte la siguiente sección *Localización del identificador de registro*.</span><span class="sxs-lookup"><span data-stu-id="fca54-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="fca54-218">Localización del identificador de registro</span><span class="sxs-lookup"><span data-stu-id="fca54-218">Find the record ID</span></span>

1. <span data-ttu-id="fca54-219">Abra un registro, como un registro de cuenta.</span><span class="sxs-lookup"><span data-stu-id="fca54-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="fca54-220">En la barra de herramientas de acciones, haga clic en el **emergente** ![registro emergente](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="fca54-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="fca54-221">O bien, en la barra de herramientas de acciones, haga clic en **ENVIAR UN VÍNCULO POR CORREO ELECTRÓNICO** para copiar la dirección URL completa en el programa de correo electrónico predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fca54-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="fca54-222">El identificador de registro se muestra entre los caracteres codificados %7b y %7d de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="fca54-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="fca54-224">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="fca54-224">Troubleshooting</span></span>
<span data-ttu-id="fca54-225">Para solucionar problemas de un paso con errores en una aplicación de lógica, vea los detalles de estado del evento.</span><span class="sxs-lookup"><span data-stu-id="fca54-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="fca54-226">En **Logic Apps**, seleccione la aplicación lógica y haga clic en **Información general**.</span><span class="sxs-lookup"><span data-stu-id="fca54-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="fca54-227">Se muestra el área de resumen y se proporciona el estado de ejecución de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fca54-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Estado de ejecución de la aplicación lógica](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="fca54-229">Para ver más información sobre cualquier ejecución que haya fallado, haga clic en el evento con error.</span><span class="sxs-lookup"><span data-stu-id="fca54-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="fca54-230">Para expandir un paso con errores, haga clic en ese paso.</span><span class="sxs-lookup"><span data-stu-id="fca54-230">To expand a failed step, click that step.</span></span>

   ![Expansión del paso con errores](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="fca54-232">Los detalles del paso aparecen y pueden ayudar a solucionar la causa del error.</span><span class="sxs-lookup"><span data-stu-id="fca54-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Detalles del paso con errores](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="fca54-234">Para más información sobre cómo solucionar problemas de las aplicaciones lógicas, consulte [Diagnóstico de errores de aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="fca54-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="fca54-235">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="fca54-235">Connector-specific details</span></span>

<span data-ttu-id="fca54-236">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="fca54-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fca54-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fca54-237">Next steps</span></span>
<span data-ttu-id="fca54-238">Explore los demás conectores disponibles en Logic Apps en nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="fca54-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
