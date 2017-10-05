---
title: "Creación del primer flujo de trabajo entre aplicaciones de nube y servicios en la nube: Azure Logic Apps | Microsoft Docs"
description: "Automatización de los procesos empresariales en escenarios de integración de aplicaciones empresariales (EAI) e integración de sistemas en Azure Logic Apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "flujo de trabajo, aplicaciones de nube, servicios en la nube, procesos empresariales, integración de sistemas, integración de aplicaciones empresariales, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="69a22-104">Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="69a22-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="69a22-105">Puede automatizar los procesos empresariales de manera más fácil y rápida cuando crea y ejecuta flujos de trabajo con [Azure Logic Apps](logic-apps-what-are-logic-apps.md), sin necesidad de escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="69a22-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="69a22-106">En este primer ejemplo se muestra cómo crear un flujo de trabajo básico de aplicaciones lógicas que busca nuevo contenido de un sitio web en una fuente RSS.</span><span class="sxs-lookup"><span data-stu-id="69a22-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="69a22-107">Cuando aparecen nuevos elementos en la fuente del sitio web, la aplicación lógica envía un correo electrónico desde una cuenta de Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="69a22-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="69a22-108">Para crear y ejecutar una aplicación lógica, necesita estos elementos:</span><span class="sxs-lookup"><span data-stu-id="69a22-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="69a22-109">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="69a22-109">An Azure subscription.</span></span> <span data-ttu-id="69a22-110">Si no tiene una suscripción, puede [comenzar con una cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="69a22-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="69a22-111">También puede [registrarse para obtener una suscripción de pago por uso](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="69a22-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="69a22-112">Su suscripción de Azure se usa para facturar el uso de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="69a22-113">Aprenda cómo funciona el [medidor de uso](../logic-apps/logic-apps-pricing.md) y los [precios](https://azure.microsoft.com/pricing/details/logic-apps) en Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="69a22-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="69a22-114">Además, para este ejemplo se necesitan estos elementos:</span><span class="sxs-lookup"><span data-stu-id="69a22-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="69a22-115">Una cuenta de Outlook.com, Office 365 Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="69a22-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="69a22-116">Si tiene una [cuenta de Microsoft](https://account.microsoft.com/account) personal, tiene una cuenta de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="69a22-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="69a22-117">También, si tiene una cuenta de Azure profesional o educativa, tiene una cuenta de **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="69a22-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="69a22-118">Un vínculo a la fuente RSS de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="69a22-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="69a22-119">Este ejemplo utiliza la [fuente RSS para noticias destacadas desde el sitio web de CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="69a22-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="69a22-120">Adición de un desencadenador que inicie el flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="69a22-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="69a22-121">Un [*desencadenador*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que inicia el flujo de trabajo de la aplicación lógica y es el primer elemento que necesita la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="69a22-122">Inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="69a22-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="69a22-123">En el menú izquierdo, elija **Nuevo** > **Enterprise Integration** > **Logic App**, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="69a22-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portal de Azure, Nuevo, Enterprise Integration, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="69a22-125">También puede elegir **Nuevo** y, después, en el cuadro de búsqueda escribir `logic app` y presionar Entrar.</span><span class="sxs-lookup"><span data-stu-id="69a22-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="69a22-126">A continuación, elija **Logic App** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="69a22-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="69a22-127">Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="69a22-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="69a22-128">Ahora, cree o seleccione un grupo de recursos de Azure, que le ayuda a organizar y administrar los recursos de Azure relacionados.</span><span class="sxs-lookup"><span data-stu-id="69a22-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="69a22-129">Por último, seleccione la ubicación del centro de datos para hospedar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="69a22-130">Cuando esté listo, elija **Anclar al panel** y, luego, **Crear**.</span><span class="sxs-lookup"><span data-stu-id="69a22-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Detalles de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="69a22-132">Al seleccionar **Anclar al panel**, la aplicación lógica aparece en el panel de Azure después de la implementación y se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="69a22-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="69a22-133">Si la aplicación lógica no aparece en el panel, en el icono **Todos los recursos**, elija **See More** (Ver más) y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="69a22-134">O, en el menú de la izquierda, elija **More services** (Más servicios).</span><span class="sxs-lookup"><span data-stu-id="69a22-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="69a22-135">En **Enterprise Integration**, elija **Logic Apps** y seleccione su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="69a22-136">La primera vez que se abre una aplicación lógica, el Diseñador de aplicación lógica muestra plantillas que puede usar para comenzar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="69a22-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="69a22-137">Por ahora, elija **Aplicación lógica en blanco** para que pueda crear la aplicación lógica desde el principio.</span><span class="sxs-lookup"><span data-stu-id="69a22-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="69a22-138">El Diseñador de la aplicación lógica se abre y muestra los servicios disponibles y *desencadenadores* que puede usar en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="69a22-139">En el cuadro de búsqueda, escriba `RSS` y seleccione este desencadenador: **RSS: Cuando se publica un elemento de fuente**.</span><span class="sxs-lookup"><span data-stu-id="69a22-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Desencadenador de RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="69a22-141">Especifique el vínculo de la fuente RSS del sitio Web del que desea realizar un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="69a22-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="69a22-142">También puede cambiar la **frecuencia** y el **intervalo**.</span><span class="sxs-lookup"><span data-stu-id="69a22-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="69a22-143">Esta configuración determina la frecuencia con que la aplicación lógica busca nuevos elementos y devuelve todos los elementos encontrados durante ese intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69a22-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="69a22-144">En este ejemplo, vamos a comprobar cada día las noticias destacadas publicadas en el sitio web de CNN.</span><span class="sxs-lookup"><span data-stu-id="69a22-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Configuración del desencadenador con la fuente RSS, la frecuencia y el intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="69a22-146">Por ahora, guarde el trabajo.</span><span class="sxs-lookup"><span data-stu-id="69a22-146">Save your work for now.</span></span> <span data-ttu-id="69a22-147">(En la barra de comandos del diseñador, elija **Guardar**).</span><span class="sxs-lookup"><span data-stu-id="69a22-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Guardado de la aplicación lógica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="69a22-149">Al guardar, la aplicación lógica se activa; pero, actualmente, la aplicación lógica solo comprueba si hay nuevos elementos en la fuente RSS especificada.</span><span class="sxs-lookup"><span data-stu-id="69a22-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="69a22-150">Para que este ejemplo sea más útil, agregamos una acción que la aplicación lógica realiza después de que se dispara el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="69a22-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="69a22-151">Adición de una acción que responde al desencadenador</span><span class="sxs-lookup"><span data-stu-id="69a22-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="69a22-152">Una [*acción*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="69a22-153">Después de agregar un desencadenador a la aplicación lógica, puede agregar una acción para llevar a cabo operaciones con los datos generados por ese desencadenador.</span><span class="sxs-lookup"><span data-stu-id="69a22-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="69a22-154">En nuestro ejemplo, ahora agregamos una acción que envía un correo electrónico cuando aparecen nuevos elementos en la fuente RSS del sitio web.</span><span class="sxs-lookup"><span data-stu-id="69a22-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="69a22-155">En el diseñador, bajo el desencadenador, elija **Nuevo paso** > **Agregar una acción**, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="69a22-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Agregar una acción](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="69a22-157">El diseñador muestra los [conectores disponibles](../connectors/apis-list.md) de modo que puede seleccionar una acción para realizar cuando se dispare el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="69a22-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="69a22-158">Según su cuenta de correo electrónico, siga los pasos para Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="69a22-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="69a22-159">Para enviar un correo electrónico desde su cuenta de Outlook, escriba `outlook` en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="69a22-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="69a22-160">En **Servicios**, elija **Outlook.com** para cuentas de Microsoft personales, o elija **Office 365 Outlook** para cuentas de Azure profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="69a22-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="69a22-161">En **Acciones**, seleccione **Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="69a22-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selección de la acción "Enviar un correo electrónico" de Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="69a22-163">Para enviar un correo electrónico desde su cuenta de Gmail, escriba `gmail` en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="69a22-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="69a22-164">En **Acciones**, seleccione **Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="69a22-164">Under **Actions**, select **Send email**.</span></span>

       ![Selección de "Gmail: Enviar un correo electrónico"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="69a22-166">Cuando se le pidan las credenciales, inicie sesión con el nombre de usuario y la contraseña de su cuenta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="69a22-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="69a22-167">Proporcione los detalles de esta acción, como la dirección de correo electrónico de destino, y elija los parámetros de los datos que se incluirán en el correo electrónico, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69a22-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Selección de los datos que se incluirán en el correo electrónico](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="69a22-169">Si eligió Outlook, la aplicación lógica podría parecerse a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69a22-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Aplicación lógica completada](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="69a22-171">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="69a22-171">Save your changes.</span></span> <span data-ttu-id="69a22-172">(En la barra de comandos del diseñador, elija **Guardar**).</span><span class="sxs-lookup"><span data-stu-id="69a22-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="69a22-173">Ahora puede ejecutar manualmente la aplicación lógica para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="69a22-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="69a22-174">En la barra de comandos del diseñador, elija **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="69a22-175">También, puede dejar que la aplicación lógica compruebe la fuente RSS especificada según la programación que haya configurado.</span><span class="sxs-lookup"><span data-stu-id="69a22-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="69a22-176">Si la aplicación lógica encuentra nuevos elementos, envía un correo electrónico que incluye los datos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="69a22-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="69a22-177">Si no encuentra ningún elemento nuevo, la aplicación lógica omite la acción de enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="69a22-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="69a22-178">Para supervisar y comprobar el historial de ejecución y desencadenamiento de la aplicación lógica, elija **Overview** (Información general).</span><span class="sxs-lookup"><span data-stu-id="69a22-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Supervisión y visualización del historial de ejecución y desencadenamiento de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="69a22-180">Si no encuentra los datos que espera, en la barra de comandos, elija **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="69a22-181">Para más información sobre el estado de la aplicación lógica o el historial de ejecución y desencadenamiento, o para diagnosticar la aplicación lógica, consulte [Solución de problemas de las aplicaciones lógicas](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="69a22-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="69a22-182">La aplicación lógica continúa ejecutándose hasta que desactiva la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69a22-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="69a22-183">Por ahora, para desactivar la aplicación elija **Overview** (Información general) en el menú de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="69a22-184">En la barra de comandos, haga clic en **Deshabilitar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="69a22-185">Enhorabuena, acaba de configurar y ejecutar la primera aplicación lógica básica.</span><span class="sxs-lookup"><span data-stu-id="69a22-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="69a22-186">También ha aprendido cómo puede crear fácilmente flujos de trabajo que automatizan los procesos, y a integrar aplicaciones de nube y servicios en la nube sin necesidad de código.</span><span class="sxs-lookup"><span data-stu-id="69a22-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="69a22-187">Administración de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="69a22-187">Manage your logic app</span></span>

<span data-ttu-id="69a22-188">Para administrar la aplicación, puede realizar tareas como editar la aplicación lógica, desactivarla, eliminarla, comprobar su estado o ver su historial.</span><span class="sxs-lookup"><span data-stu-id="69a22-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="69a22-189">Inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="69a22-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="69a22-190">En el menú de la izquierda, elija **More services** (Más servicios).</span><span class="sxs-lookup"><span data-stu-id="69a22-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="69a22-191">En **Enterprise Integration**, elija **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="69a22-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="69a22-192">Seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="69a22-192">Select your logic app.</span></span> 

   <span data-ttu-id="69a22-193">En el menú de la aplicación lógica, puede encontrar estas tareas de administración de aplicaciones lógicas:</span><span class="sxs-lookup"><span data-stu-id="69a22-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="69a22-194">Tarea</span><span class="sxs-lookup"><span data-stu-id="69a22-194">Task</span></span>|<span data-ttu-id="69a22-195">Pasos</span><span class="sxs-lookup"><span data-stu-id="69a22-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="69a22-196">Ver el estado de la aplicación, el historial de ejecución e información general</span><span class="sxs-lookup"><span data-stu-id="69a22-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="69a22-197">Elija **Overview** (Información general).</span><span class="sxs-lookup"><span data-stu-id="69a22-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="69a22-198">Editar la aplicación</span><span class="sxs-lookup"><span data-stu-id="69a22-198">Edit your app</span></span> | <span data-ttu-id="69a22-199">Elija **Diseñador de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="69a22-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="69a22-200">Ver la definición JSON del flujo de trabajo de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69a22-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="69a22-201">Elija **Vista de código de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="69a22-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="69a22-202">Ver las operaciones realizadas en la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="69a22-202">View operations performed on your logic app</span></span> | <span data-ttu-id="69a22-203">Elija **Registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="69a22-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="69a22-204">Ver las versiones pasadas de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="69a22-204">View past versions for your logic app</span></span> | <span data-ttu-id="69a22-205">Elija **Versiones**.</span><span class="sxs-lookup"><span data-stu-id="69a22-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="69a22-206">Desactivar la aplicación temporalmente</span><span class="sxs-lookup"><span data-stu-id="69a22-206">Turn off your app temporarily</span></span> | <span data-ttu-id="69a22-207">Elija **Overview** (Información general) y, en la barra de comandos, elija **Desactivar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="69a22-208">Eliminar la aplicación</span><span class="sxs-lookup"><span data-stu-id="69a22-208">Delete your app</span></span> | <span data-ttu-id="69a22-209">Elija **Overview** (Información general) y, en la barra de comandos, elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="69a22-210">Escriba el nombre de la aplicación lógica y elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="69a22-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="69a22-211">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="69a22-211">Get help</span></span>

<span data-ttu-id="69a22-212">Para formular preguntas, o responderlas, y saber lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="69a22-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="69a22-213">Para ayudar a mejorar Azure Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="69a22-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69a22-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69a22-214">Next steps</span></span>

*  [<span data-ttu-id="69a22-215">Adición de condiciones y ejecución de flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="69a22-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="69a22-216">Plantillas de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="69a22-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="69a22-217">Creación de aplicaciones lógicas a partir de plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69a22-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
