---
title: "aaaCreate el primer flujo de trabajo entre aplicaciones de nube y servicios en la nube: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="2f4a2-104">Crear su primera aplicación de lógica de procesos de tooautomate de flujo de trabajo entre las aplicaciones de nube y servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2f4a2-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="2f4a2-105">Puede automatizar los procesos empresariales de manera más fácil y rápida cuando crea y ejecuta flujos de trabajo con [Azure Logic Apps](logic-apps-what-are-logic-apps.md), sin necesidad de escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="2f4a2-106">Este primer ejemplo muestra cómo toocreate fuente de un flujo de trabajo de aplicación lógica básica que comprueba una RSS para el nuevo contenido en un sitio Web.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="2f4a2-107">Cuando aparezcan nuevos artículos de fuente de distribución del sitio Web de hello, aplicación de lógica de hello envía correo electrónico desde una cuenta de Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="2f4a2-108">toocreate y ejecutar una aplicación de lógica, necesita estos elementos:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="2f4a2-109">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-109">An Azure subscription.</span></span> <span data-ttu-id="2f4a2-110">Si no tiene una suscripción, puede [comenzar con una cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="2f4a2-111">También puede [registrarse para obtener una suscripción de pago por uso](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="2f4a2-112">Su suscripción de Azure se usa para facturar el uso de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="2f4a2-113">Aprenda cómo funciona el [medidor de uso](../logic-apps/logic-apps-pricing.md) y los [precios](https://azure.microsoft.com/pricing/details/logic-apps) en Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="2f4a2-114">Además, para este ejemplo se necesitan estos elementos:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="2f4a2-115">Una cuenta de Outlook.com, Office 365 Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="2f4a2-116">Si tiene una [cuenta de Microsoft](https://account.microsoft.com/account) personal, tiene una cuenta de Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="2f4a2-117">También, si tiene una cuenta de Azure profesional o educativa, tiene una cuenta de **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="2f4a2-118">Un vínculo tooa la fuente RSS del sitio Web.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="2f4a2-119">Este ejemplo utiliza hello [fuente RSS para artículos destacados de sitio Web de CNN.com Hola](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="2f4a2-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="2f4a2-120">Adición de un desencadenador que inicie el flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="2f4a2-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="2f4a2-121">A [ *desencadenador* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que se inicia el flujo de trabajo de aplicación lógica y es Hola primer elemento que necesita la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="2f4a2-122">Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="2f4a2-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="2f4a2-123">Desde el menú de la izquierda hello, elegir **nuevo** > **integración empresarial** > **aplicación lógica** tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portal de Azure, Nuevo, Enterprise Integration, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="2f4a2-125">También puede elegir **New**, a continuación, en el cuadro de búsqueda de hello, escriba `logic app`, y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="2f4a2-126">A continuación, elija **Logic App** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="2f4a2-127">Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="2f4a2-128">Ahora, cree o seleccione un grupo de recursos de Azure, que le ayuda a organizar y administrar los recursos de Azure relacionados.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="2f4a2-129">Por último, seleccione la ubicación de centro de datos de Hola para hospedar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="2f4a2-130">Cuando esté listo, elija **Pin toodashboard** y, a continuación, **crear**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Detalles de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="2f4a2-132">Cuando se selecciona **toodashboard Pin**, la aplicación lógica aparece en hello Azure panel después de la implementación y se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="2f4a2-133">Si la aplicación lógica no aparece en panel de hello, vaya a hello **todos los recursos** icono, elija **vea más**y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="2f4a2-134">O, en el menú de la izquierda hello, elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="2f4a2-135">En **Enterprise Integration**, elija **Logic Apps** y seleccione su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="2f4a2-136">Cuando se abre la aplicación lógica para hello primera vez, Hola lógica de aplicación diseñador muestra plantillas que puede usar tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="2f4a2-137">Por ahora, elija **Aplicación lógica en blanco** para que pueda crear la aplicación lógica desde el principio.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="2f4a2-138">Hello lógica de aplicación diseñador se abre y muestra los servicios disponibles y *desencadenadores* que puede usar en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="2f4a2-139">En el cuadro de búsqueda de hello, escriba `RSS`y seleccione este desencadenador: **RSS - cuando se publica un elemento de fuente**</span><span class="sxs-lookup"><span data-stu-id="2f4a2-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Desencadenador de RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="2f4a2-141">Especifique el vínculo de Hola de fuente RSS del sitio Web de Hola que desea tootrack.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="2f4a2-142">También puede cambiar la **frecuencia** y el **intervalo**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="2f4a2-143">Esta configuración determina la frecuencia con que la aplicación lógica busca nuevos elementos y devuelve todos los elementos encontrados durante ese intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="2f4a2-144">En este ejemplo, vamos a comprobar cada día para casos superiores registra el sitio Web CNN toohello.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Configuración del desencadenador con la fuente RSS, la frecuencia y el intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="2f4a2-146">Por ahora, guarde el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-146">Save your work for now.</span></span> <span data-ttu-id="2f4a2-147">(En la barra de comandos del Diseñador de hello, elija **guardar**.)</span><span class="sxs-lookup"><span data-stu-id="2f4a2-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Guardado de la aplicación lógica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="2f4a2-149">Cuando guarda, poner en marcha la aplicación lógica, pero en la actualidad, la aplicación lógica sólo busca nuevos elementos en hello Especifica fuente RSS.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="2f4a2-150">toomake se activa en este ejemplo más útil, que agregamos una acción que realiza la aplicación lógica el desencadenador after.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="2f4a2-151">Agregar una acción que responde el desencadenador de tooyour</span><span class="sxs-lookup"><span data-stu-id="2f4a2-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="2f4a2-152">Una [*acción*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="2f4a2-153">Después de agregar una aplicación de lógica de desencadenador tooyour, puede agregar un operaciones tooperform de acción con los datos generados por este desencadenador.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="2f4a2-154">En nuestro ejemplo, ahora se agregue una acción que envía el correo electrónico cuando aparezcan nuevos artículos en la fuente de RSS del sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="2f4a2-155">En el Diseñador de hello, en el desencadenador, elija **nuevo paso** > **agregar una acción** tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Agregar una acción](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="2f4a2-157">Hola diseñador muestra [conectores disponibles](../connectors/apis-list.md) para que pueda seleccionar una acción tooperform cuando se activa el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="2f4a2-158">En función de su cuenta de correo electrónico, siga los pasos de Hola para Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="2f4a2-159">correo electrónico toosend de su cuenta de Outlook, en el cuadro de búsqueda de hello, escriba `outlook`.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="2f4a2-160">En **Servicios**, elija **Outlook.com** para cuentas de Microsoft personales, o elija **Office 365 Outlook** para cuentas de Azure profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="2f4a2-161">En **Acciones**, seleccione **Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selección de la acción "Enviar un correo electrónico" de Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="2f4a2-163">correo electrónico toosend de su cuenta de Gmail, en el cuadro de búsqueda de hello, escriba `gmail`.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="2f4a2-164">En **Acciones**, seleccione **Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-164">Under **Actions**, select **Send email**.</span></span>

       ![Selección de "Gmail: Enviar un correo electrónico"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="2f4a2-166">Cuando se le pidan las credenciales, inicie sesión con hello username y password para su cuenta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="2f4a2-167">Proporcionar detalles de Hola para esta acción, como la dirección de correo electrónico de destino de hello y elegir parámetros Hola Hola datos tooinclude del correo electrónico de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Seleccione tooinclude de datos de correo electrónico](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="2f4a2-169">Si eligió Outlook, la aplicación lógica podría parecerse a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Aplicación lógica completada](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="2f4a2-171">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-171">Save your changes.</span></span> <span data-ttu-id="2f4a2-172">(En la barra de comandos del Diseñador de hello, elija **guardar**.)</span><span class="sxs-lookup"><span data-stu-id="2f4a2-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="2f4a2-173">Ahora puede ejecutar manualmente la aplicación lógica para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="2f4a2-174">En la barra de comandos del Diseñador de hello, elija **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="2f4a2-175">En caso contrario, puede dejar que la aplicación lógica comprobar Hola especificado fuente RSS basada en programación de Hola que configuró.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="2f4a2-176">Si la aplicación lógica busca nuevos elementos, aplicación de lógica de hello envía correo electrónico que incluirá los datos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="2f4a2-177">Si no se encuentra ningún elemento nuevo, la aplicación lógica omite la acción de Hola que envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="2f4a2-178">toomonitor y comprobación de la aplicación lógica de ejecución de la y desencadenar historial, en el menú de aplicación lógica, eligen **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Supervisión y visualización del historial de ejecución y desencadenamiento de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="2f4a2-180">Si no encuentra datos Hola que espera, en la barra de comandos de hello, pruebe a elegir **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="2f4a2-181">toolearn más información sobre el estado de la aplicación lógica o ejecute y desencadenar historial o toodiagnose la aplicación lógica, consulte [solucionar problemas de la aplicación lógica](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="2f4a2-182">La aplicación lógica continúa ejecutándose hasta que desactiva la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="2f4a2-183">Elija tooturn desactivar la aplicación por ahora, en el menú de aplicación lógica, **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="2f4a2-184">En la barra de comandos de hello, elija **deshabilitar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="2f4a2-185">Enhorabuena, acaba de configurar y ejecutar la primera aplicación lógica básica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="2f4a2-186">También ha aprendido cómo puede crear fácilmente flujos de trabajo que automatizan los procesos, y a integrar aplicaciones de nube y servicios en la nube sin necesidad de código.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="2f4a2-187">Administración de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="2f4a2-187">Manage your logic app</span></span>

<span data-ttu-id="2f4a2-188">toomanage la aplicación, puede realizar tareas como comprobar el estado de hello, editar, ver el historial, desactivar o eliminar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="2f4a2-189">Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="2f4a2-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="2f4a2-190">En el menú de la izquierda hello, elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="2f4a2-191">En **Enterprise Integration**, elija **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="2f4a2-192">Seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-192">Select your logic app.</span></span> 

   <span data-ttu-id="2f4a2-193">En el menú de la aplicación de lógica de hello, puede encontrar estas tareas de administración de aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="2f4a2-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="2f4a2-194">Tarea</span><span class="sxs-lookup"><span data-stu-id="2f4a2-194">Task</span></span>|<span data-ttu-id="2f4a2-195">Pasos</span><span class="sxs-lookup"><span data-stu-id="2f4a2-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="2f4a2-196">Ver el estado de la aplicación, el historial de ejecución e información general</span><span class="sxs-lookup"><span data-stu-id="2f4a2-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="2f4a2-197">Elija **Overview** (Información general).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="2f4a2-198">Editar la aplicación</span><span class="sxs-lookup"><span data-stu-id="2f4a2-198">Edit your app</span></span> | <span data-ttu-id="2f4a2-199">Elija **Diseñador de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="2f4a2-200">Ver la definición JSON del flujo de trabajo de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2f4a2-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="2f4a2-201">Elija **Vista de código de aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="2f4a2-202">Ver las operaciones realizadas en la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="2f4a2-202">View operations performed on your logic app</span></span> | <span data-ttu-id="2f4a2-203">Elija **Registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="2f4a2-204">Ver las versiones pasadas de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="2f4a2-204">View past versions for your logic app</span></span> | <span data-ttu-id="2f4a2-205">Elija **Versiones**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="2f4a2-206">Desactivar la aplicación temporalmente</span><span class="sxs-lookup"><span data-stu-id="2f4a2-206">Turn off your app temporarily</span></span> | <span data-ttu-id="2f4a2-207">Elija **Introducción**, a continuación, en la barra de comandos de hello, elija **deshabilitar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="2f4a2-208">Eliminar la aplicación</span><span class="sxs-lookup"><span data-stu-id="2f4a2-208">Delete your app</span></span> | <span data-ttu-id="2f4a2-209">Elija **Introducción**, a continuación, en la barra de comandos de hello, elija **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="2f4a2-210">Escriba el nombre de la aplicación lógica y elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2f4a2-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="2f4a2-211">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="2f4a2-211">Get help</span></span>

<span data-ttu-id="2f4a2-212">tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2f4a2-213">toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2f4a2-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f4a2-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f4a2-214">Next steps</span></span>

*  [<span data-ttu-id="2f4a2-215">Adición de condiciones y ejecución de flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="2f4a2-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="2f4a2-216">Plantillas de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="2f4a2-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="2f4a2-217">Creación de aplicaciones lógicas a partir de plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f4a2-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
