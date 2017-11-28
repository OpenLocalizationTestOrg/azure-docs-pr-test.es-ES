---
title: Inicio de un runbook de Azure Automation con un webhook | Microsoft Docs
description: "Un webhook que permite a un cliente iniciar un runbook en Automatización de Azure desde una llamada HTTP.  Este artículo describe cómo crear un webhook y cómo llamar a uno para que inicie un runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="0e0b3-104">Inicio de un runbook de Azure Automation con un webhook</span><span class="sxs-lookup"><span data-stu-id="0e0b3-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="0e0b3-105">Un *webhook* le permite iniciar un runbook determinado en Automatización de Azure a través de una sola solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="0e0b3-106">Esto permite a los servicios externos, como Visual Studio Team Services, GitHub, Log Analytics de Microsoft Operations Management Suite o aplicaciones personalizadas, iniciar runbooks sin necesidad de implementar una solución completa mediante la API de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="0e0b3-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="0e0b3-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="0e0b3-108">Puede comparar webhooks con otros métodos para iniciar un runbook [a partir un runbook de Automatización de Azure.](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0e0b3-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="0e0b3-109">Detalles de un webhook</span><span class="sxs-lookup"><span data-stu-id="0e0b3-109">Details of a webhook</span></span>
<span data-ttu-id="0e0b3-110">En la tabla siguiente se describen las propiedades que debe configurar para un webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="0e0b3-111">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0e0b3-111">Property</span></span> | <span data-ttu-id="0e0b3-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="0e0b3-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0e0b3-113">Nombre</span><span class="sxs-lookup"><span data-stu-id="0e0b3-113">Name</span></span> |<span data-ttu-id="0e0b3-114">Puede proporcionar cualquier nombre que desee para un webhook, ya que esto no se expone al cliente.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="0e0b3-115">Solo se utiliza para que identifique el runbook en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="0e0b3-116">Como práctica recomendada, debe proporcionar al webhook un nombre relacionado con el cliente que lo va a usar.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="0e0b3-117">URL</span><span class="sxs-lookup"><span data-stu-id="0e0b3-117">URL</span></span> |<span data-ttu-id="0e0b3-118">La dirección URL del webhook es la dirección única que llama a un cliente con una solicitud HTTP POST para iniciar el runbook vinculado al webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="0e0b3-119">Se genera automáticamente al crear el webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="0e0b3-120">No se puede especificar una dirección URL personalizada.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="0e0b3-121">La dirección URL contiene un token de seguridad que permite que el runbook se invoque por un sistema de terceros sin autenticación adicional.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="0e0b3-122">Por este motivo, debe tratarse como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="0e0b3-123">Por motivos de seguridad, solo puede ver la dirección URL en el Portal de Azure en el momento en que se crea el Webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="0e0b3-124">Debe anotar la dirección URL en una ubicación segura para su uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="0e0b3-125">Fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="0e0b3-125">Expiration date</span></span> |<span data-ttu-id="0e0b3-126">Al igual que un certificado, cada webhook tiene una fecha de caducidad en la que ya no se puede usar.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="0e0b3-127">Esta fecha de expiración se puede modificar una vez creado el webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="0e0b3-128">Enabled</span><span class="sxs-lookup"><span data-stu-id="0e0b3-128">Enabled</span></span> |<span data-ttu-id="0e0b3-129">Al crearse, los webhooks se habilitan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="0e0b3-130">Si se establece como Disabled, ningún cliente podrá usarlo.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="0e0b3-131">Puede establecer la propiedad **Enabled** al crear el webhook o en cualquier momento una vez creado.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="0e0b3-132">Parámetros</span><span class="sxs-lookup"><span data-stu-id="0e0b3-132">Parameters</span></span>
<span data-ttu-id="0e0b3-133">Un webhook puede definir valores para parámetros de runbook que se usan cuando se inicia dicho webhook inicia el runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="0e0b3-134">El webhook debe incluir los valores de los parámetros obligatorios del runbook y puede incluir valores para los parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="0e0b3-135">Un valor de parámetro configurado para un webhook se puede modificar incluso después de crear el webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="0e0b3-136">Varios webhooks vinculados a un único runbook puede utilizar distintos valores de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="0e0b3-137">Cuando un cliente inicia un runbook mediante un webhook, no puede reemplazar los valores de parámetros definidos en el webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="0e0b3-138">Para recibir datos del cliente, el runbook puede aceptar un único parámetro denominado **$WebhookData** del tipo [object] que contendrá los datos que el cliente incluye en la solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Propiedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="0e0b3-140">El objeto **$WebhookData** tendrá las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0e0b3-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="0e0b3-141">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0e0b3-141">Property</span></span> | <span data-ttu-id="0e0b3-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="0e0b3-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0e0b3-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="0e0b3-143">WebhookName</span></span> |<span data-ttu-id="0e0b3-144">Nombre del webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-144">The name of the webhook.</span></span> |
| <span data-ttu-id="0e0b3-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="0e0b3-145">RequestHeader</span></span> |<span data-ttu-id="0e0b3-146">Tabla hash que contiene los encabezados de la solicitud POST entrante.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="0e0b3-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="0e0b3-147">RequestBody</span></span> |<span data-ttu-id="0e0b3-148">El cuerpo de la solicitud POST entrante.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="0e0b3-149">Esto conservará todo el formato como cadena de JSON, XML o datos codificados de formulario.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="0e0b3-150">El runbook debe escribirse para que trabaje con el formato de datos que se espera.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="0e0b3-151">No hay ninguna configuración del webhook obligatoria para admitir el parámetro **$WebhookData** , y el runbook no tiene que aceptarlo.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="0e0b3-152">Si el runbook no define el parámetro, se ignoran los detalles de la solicitud enviados desde el cliente.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="0e0b3-153">Si especifica un valor para $WebhookData al crear el webhook, el valor se reemplazará cuando el webhook inicie el runbook con los datos de la solicitud POST del cliente, incluso si el cliente no incluye ningún dato en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="0e0b3-154">Si inicia un runbook con $WebhookData mediante un método que no sea un webhook, puede proporcionar un valor para $Webhookdata que el runbook reconocerá.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="0e0b3-155">Este valor debe ser un objeto con las mismas [propiedades](#details-of-a-webhook) que $Webhookdata para que el runbook pueda funcionar correctamente con él con si trabajara con WebhookData pasado por un webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="0e0b3-156">Por ejemplo, si se está iniciando el siguiente runbook desde el Portal de Azure y quiere pasar algún WebhookData de ejemplo para prueba, porque WebhookData es un objeto, se debe pasar como JSON en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="0e0b3-158">Para el runbook anterior, si tiene las siguientes propiedades para el parámetro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="0e0b3-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="0e0b3-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="0e0b3-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="0e0b3-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="0e0b3-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="0e0b3-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="0e0b3-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="0e0b3-162">Luego pasaría el siguiente valor JSON en la interfaz de usuario para el parámetro WebhookData:</span><span class="sxs-lookup"><span data-stu-id="0e0b3-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="0e0b3-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="0e0b3-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Iniciar el parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="0e0b3-165">Los valores de todos los parámetros de entrada se registran con el trabajo de runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="0e0b3-166">Esto significa que se registrará cualquier entrada que proporcione el cliente en la solicitud de webhook y que estará disponible para cualquiera con acceso al trabajo de automatización.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="0e0b3-167">Por este motivo, debe tener cuidado en cómo incluir información confidencial en las llamadas de webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="0e0b3-168">Seguridad</span><span class="sxs-lookup"><span data-stu-id="0e0b3-168">Security</span></span>
<span data-ttu-id="0e0b3-169">La seguridad de un webhook se basa en la privacidad de su dirección URL que contiene un token de seguridad que permite que se invoque.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="0e0b3-170">Automatización de Azure no realiza ninguna autenticación en la solicitud siempre que se haga en la dirección URL correcta.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="0e0b3-171">Por esta razón, no deben utilizarse webhooks de runbooks que realicen funciones altamente confidenciales sin utilizar medios alternativos para validar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="0e0b3-172">Puede incluir lógica en el runbook para determinar que se llamó por un webhook; para ello, active la propiedad **WebhookName** del parámetro $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="0e0b3-173">El runbook puede realizar más validaciones buscando información concreta en las propiedades **RequestHeader** o **RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="0e0b3-174">Otra estrategia es hacer que el runbook realice alguna validación de una condición externa cuando recibe una solicitud de webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="0e0b3-175">Por ejemplo, considere un runbook llamado por GitHub cuando hay una nueva confirmación a un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="0e0b3-176">El runbook puede conectarse a GitHub para asegurarse de que una nueva confirmación se ha realizado realmente antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="0e0b3-177">Creación de un webhook</span><span class="sxs-lookup"><span data-stu-id="0e0b3-177">Creating a webhook</span></span>
<span data-ttu-id="0e0b3-178">Use el procedimiento siguiente para crear un nuevo Webhook vinculado a un Runbook en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="0e0b3-179">Desde la **Hoja de Runbooks** en el Portal de Azure, haga clic en el Runbook que va a iniciar el Webhook para ver su hoja de detalles.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="0e0b3-180">Haga clic en **Webhook** en la parte superior de la hoja para abrir la hoja **Add Webhook** (Agregar webhook).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="0e0b3-181">
   ![Botón Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="0e0b3-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="0e0b3-182">Haga clic en **Create new webhook** (Create new webhook) to open la hoja **Create webhook** (Crear webhook).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="0e0b3-183">Especifique el **nombre** y la **fecha de expiración** del webhook y si debe habilitarse.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="0e0b3-184">Vea [Detalles de un webhook](#details-of-a-webhook) para más información sobre estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="0e0b3-185">Haga clic en el icono de copiar y presione Ctrl+C para copiar la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="0e0b3-186">A continuación, guárdela en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-186">Then record it in a safe place.</span></span>  <span data-ttu-id="0e0b3-187">**Una vez creado el webhook, la dirección URL no se podrá volver a recuperar.**</span><span class="sxs-lookup"><span data-stu-id="0e0b3-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="0e0b3-188">
   ![Dirección URL de webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="0e0b3-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="0e0b3-189">Haga clic en **Parámetros** para especificar los valores de los parámetros del runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="0e0b3-190">Si el runbook tiene parámetros obligatorios, no podrá crear el webhook, salvo que se especifiquen los valores.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="0e0b3-191">Haga clic en **Crear** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="0e0b3-192">Uso de un webhook</span><span class="sxs-lookup"><span data-stu-id="0e0b3-192">Using a webhook</span></span>
<span data-ttu-id="0e0b3-193">Para utilizar un webhook después de que se haya creado, la aplicación cliente debe emitir una solicitud HTTP POST con la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="0e0b3-194">La sintaxis del webhook estará en el formato siguiente.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="0e0b3-195">El cliente recibirá uno de los siguientes códigos de retorno de la solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="0e0b3-196">Código</span><span class="sxs-lookup"><span data-stu-id="0e0b3-196">Code</span></span> | <span data-ttu-id="0e0b3-197">Texto</span><span class="sxs-lookup"><span data-stu-id="0e0b3-197">Text</span></span> | <span data-ttu-id="0e0b3-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="0e0b3-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0e0b3-199">202</span><span class="sxs-lookup"><span data-stu-id="0e0b3-199">202</span></span> |<span data-ttu-id="0e0b3-200">Accepted</span><span class="sxs-lookup"><span data-stu-id="0e0b3-200">Accepted</span></span> |<span data-ttu-id="0e0b3-201">La solicitud se aceptó y el runbook se puso en cola correctamente.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="0e0b3-202">400</span><span class="sxs-lookup"><span data-stu-id="0e0b3-202">400</span></span> |<span data-ttu-id="0e0b3-203">Bad Request</span><span class="sxs-lookup"><span data-stu-id="0e0b3-203">Bad Request</span></span> |<span data-ttu-id="0e0b3-204">No se aceptó la solicitud por uno de los siguientes motivos.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0e0b3-205">El webhook ha expirado.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="0e0b3-206">El webhook está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="0e0b3-207">El token de la dirección URL no es válido.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="0e0b3-208">404</span><span class="sxs-lookup"><span data-stu-id="0e0b3-208">404</span></span> |<span data-ttu-id="0e0b3-209">No encontrado</span><span class="sxs-lookup"><span data-stu-id="0e0b3-209">Not Found</span></span> |<span data-ttu-id="0e0b3-210">No se aceptó la solicitud por uno de los siguientes motivos.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="0e0b3-211">No se encontró el webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="0e0b3-212">No se encontró el runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="0e0b3-213">No se encontró la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="0e0b3-214">500</span><span class="sxs-lookup"><span data-stu-id="0e0b3-214">500</span></span> |<span data-ttu-id="0e0b3-215">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="0e0b3-215">Internal Server Error</span></span> |<span data-ttu-id="0e0b3-216">La dirección URL es válida, pero se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="0e0b3-217">Vuelva a enviar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-217">Please resubmit the request.</span></span> |

<span data-ttu-id="0e0b3-218">Asumiendo que la solicitud sea correcta, la respuesta del webhook contendrá el Id. de trabajo en formato JSON como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="0e0b3-219">Contendrá un solo Id. de trabajo, pero el formato JSON permite realizar potenciales mejoras en el futuro.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="0e0b3-220">El cliente no puede determinar cuando se completa el trabajo del runbook ni su estado de finalización a partir del webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="0e0b3-221">Sin embargo, puede determinar esta información si usa el identificador del trabajo con otro método como [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o la [API de Azure Automation](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="0e0b3-222">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0e0b3-222">Example</span></span>
<span data-ttu-id="0e0b3-223">En el ejemplo siguiente se usa Windows PowerShell para iniciar un runbook con un webhook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="0e0b3-224">Tenga en cuenta que cualquier lenguaje que pueda realizar una solicitud HTTP puede utilizar un webhook; Windows PowerShell se usa aquí simplemente como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="0e0b3-225">El runbook espera una lista de máquinas virtuales con formato JSON en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="0e0b3-226">También se incluye información sobre quién inicia el runbook y la fecha y hora en que se inicia en el encabezado de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="0e0b3-227">La siguiente imagen muestra la información del encabezado (con un seguimiento de [Fiddler](http://www.telerik.com/fiddler) ) de esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="0e0b3-228">Aquí se incluyen los encabezados estándar de una solicitud HTTP, además de los encabezados de fecha y hora personalizados y que se han agregado.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="0e0b3-229">Todos estos valores están disponibles para el runbook en la propiedad **RequestHeaders** de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Botón Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="0e0b3-231">La siguiente imagen muestra el cuerpo de la solicitud (con un seguimiento de [Fiddler](http://www.telerik.com/fiddler)) que está disponible para el runbook en la propiedad **RequestBody** de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="0e0b3-232">Tiene formato JSON porque ese era el formato que se incluía en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Botón Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="0e0b3-234">La siguiente imagen muestra la solicitud que se envía desde Windows PowerShell y la respuesta resultante.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="0e0b3-235">El Id. de trabajo se extrae de la respuesta y se convierte en una cadena.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-235">The job id is extracted from the response and converted to a string.</span></span>

![Botón Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="0e0b3-237">El siguiente runbook de muestra acepta la solicitud del ejemplo anterior e inicia las máquinas virtuales especificadas en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="0e0b3-238">Iniciar runbooks en respuesta a alertas de Azure</span><span class="sxs-lookup"><span data-stu-id="0e0b3-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="0e0b3-239">Los runbooks con Webhook se pueden usar para reaccionar frente a [alertas de Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0e0b3-240">Los recursos de Azure se pueden supervisar recopilando estadísticas como rendimiento, disponibilidad y uso con la ayuda de las alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="0e0b3-241">Puede recibir una alerta basada en los eventos o las métricas de supervisión para los recursos de Azure. Actualmente, las cuentas de automatización solo admiten métricas.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="0e0b3-242">Cuando el valor de una métrica especificada supera el umbral asignado o si se desencadena el evento configurado, se envía una notificación al administrador o a los coadministradores del servicio para resolver la alerta; para más información sobre eventos y métricas, consulte el artículo sobre las [alertas de Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="0e0b3-243">Además de usar alertas de Azure como sistema de notificación, también puede iniciar runbooks en respuesta a alertas.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="0e0b3-244">La automatización de Azure ofrece la funcionalidad de ejecutar runbooks habilitados con webhooks con alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="0e0b3-245">Cuando una métrica supera el valor de umbral configurado, la regla de alerta se activa y desencadena el webhook de automatización que a su vez ejecuta el runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="0e0b3-247">Contexto de alerta</span><span class="sxs-lookup"><span data-stu-id="0e0b3-247">Alert context</span></span>
<span data-ttu-id="0e0b3-248">Piense en un recurso de Azure como una máquina virtual; el uso de la CPU de este equipo es una de las métricas clave de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="0e0b3-249">Si el uso de la CPU es del 100 % o más de una cantidad determinada durante un período largo de tiempo, es posible que quiera reiniciar la máquina virtual para corregir el problema.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="0e0b3-250">Esto puede resolverse configurando una regla de alerta para la máquina virtual y esta regla toma el porcentaje de la CPU como su métrica.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="0e0b3-251">El porcentaje de la CPU aquí solo se toma como ejemplo pero hay otras muchas métricas que se pueden configurar para sus recursos de Azure y el reinicio de la máquina virtual es una acción que se lleva a cabo para corregir este problema; puede configurar el runbook para realizar otras acciones.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="0e0b3-252">Cuando esta regla de alerta se activa y desencadena el runbook habilitado con webhook, envía el contexto de la alerta al runbook.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="0e0b3-253">El [contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene los detalles, entre los que se incluyen **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** y **Timestamp**, que se requieren para que el runbook identifique el recurso en el que realizará la acción.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="0e0b3-254">El contexto de alerta se inserta en la parte del cuerpo del objeto **WebhookData** enviado al runbook y se puede acceder a él con la propiedad **Webhook.RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="0e0b3-255">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0e0b3-255">Example</span></span>
<span data-ttu-id="0e0b3-256">Cree una máquina virtual de Azure en su suscripción y asocie una [alerta para supervisar la métrica del porcentaje de CPU](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="0e0b3-257">Al crear la alerta, asegúrese de que rellenar el campo del webhook con la dirección URL del webhook que se generó al crear el webhook .</span><span class="sxs-lookup"><span data-stu-id="0e0b3-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="0e0b3-258">El siguiente runbook de ejemplo se desencadena cuando se activa la regla de alerta y recopila los parámetros de contexto de la alerta que son necesarios para que el runbook identifique el recurso en el que va a realizar la acción.</span><span class="sxs-lookup"><span data-stu-id="0e0b3-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="0e0b3-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e0b3-259">Next steps</span></span>
* <span data-ttu-id="0e0b3-260">Para más información sobre las distintas maneras de iniciar un runbook, vea [Inicio de un runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="0e0b3-261">Para más información sobre cómo ver el estado de un trabajo de runbook, vea [Ejecución de un runbook en Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="0e0b3-262">Para más información sobre cómo utilizar Azure Automation para tomar medidas relativas a las alertas de Azure, vea [Escenario de Azure Automation: corrección de las alertas de la máquina virtual de Azure](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="0e0b3-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
