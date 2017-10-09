---
title: "aaaStarting un runbook de automatización de Azure con un webhook | Documentos de Microsoft"
description: "Webhook que permite a un cliente toostart un runbook en automatización de Azure desde una llamada HTTP.  Este artículo se describe cómo toocreate un webhook y cómo toocall una toostart un runbook."
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="31d3e-104">Inicio de un runbook de Azure Automation con un webhook</span><span class="sxs-lookup"><span data-stu-id="31d3e-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="31d3e-105">A *webhook* permite toostart un runbook determinado en la automatización de Azure a través de una única solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="31d3e-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="31d3e-106">Esto permite a servicios externos, como Visual Studio Team Services, GitHub, análisis de registros de Microsoft Operations Management Suite o aplicaciones personalizadas toostart runbooks sin necesidad de implementar una solución completa mediante Hola API de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="31d3e-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="31d3e-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="31d3e-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="31d3e-108">Puede comparar webhooks tooother métodos para iniciar un runbook [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="31d3e-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="31d3e-109">Detalles de un webhook</span><span class="sxs-lookup"><span data-stu-id="31d3e-109">Details of a webhook</span></span>
<span data-ttu-id="31d3e-110">Hello tabla siguiente describe las propiedades de Hola que se deben configurar para un webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="31d3e-111">Propiedad</span><span class="sxs-lookup"><span data-stu-id="31d3e-111">Property</span></span> | <span data-ttu-id="31d3e-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="31d3e-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="31d3e-113">Nombre</span><span class="sxs-lookup"><span data-stu-id="31d3e-113">Name</span></span> |<span data-ttu-id="31d3e-114">Puede proporcionar cualquier nombre que desee para un webhook, puesto que esto es no expone a toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="31d3e-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="31d3e-115">Solo se utiliza para tooidentify Hola runbook de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="31d3e-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="31d3e-116">Como práctica recomendada, debe prestar hello webhook un cliente de toohello relacionados de nombre que va a usar.</span><span class="sxs-lookup"><span data-stu-id="31d3e-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="31d3e-117">URL</span><span class="sxs-lookup"><span data-stu-id="31d3e-117">URL</span></span> |<span data-ttu-id="31d3e-118">dirección URL de Hola de hello webhook es que un cliente llama a un runbook de hello toostart HTTP POST de dirección única Hola vinculado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="31d3e-119">Se genera automáticamente al crear el webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="31d3e-120">No se puede especificar una dirección URL personalizada.</span><span class="sxs-lookup"><span data-stu-id="31d3e-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="31d3e-121">dirección URL de Hello contiene un token de seguridad que permita Hola runbook toobe invocado por un sistema de terceros con ninguna autenticación adicional.</span><span class="sxs-lookup"><span data-stu-id="31d3e-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="31d3e-122">Por este motivo, debe tratarse como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="31d3e-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="31d3e-123">Por motivos de seguridad, puede solo Hola de vista que se crea la dirección URL en el portal de Azure en hello tiempo hello webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="31d3e-124">Tenga en cuenta Hola URL en una ubicación segura para un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="31d3e-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="31d3e-125">Fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="31d3e-125">Expiration date</span></span> |<span data-ttu-id="31d3e-126">Al igual que un certificado, cada webhook tiene una fecha de caducidad en la que ya no se puede usar.</span><span class="sxs-lookup"><span data-stu-id="31d3e-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="31d3e-127">Esta fecha de expiración se puede modificar una vez creado el webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="31d3e-128">habilitado</span><span class="sxs-lookup"><span data-stu-id="31d3e-128">Enabled</span></span> |<span data-ttu-id="31d3e-129">Al crearse, los webhooks se habilitan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="31d3e-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="31d3e-130">Si se establece tooDisabled, entonces no hay ningún cliente será toouse capaz de él.</span><span class="sxs-lookup"><span data-stu-id="31d3e-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="31d3e-131">Puede establecer hello **habilitado** propiedad al crear webhook Hola o en cualquier momento una vez se crea.</span><span class="sxs-lookup"><span data-stu-id="31d3e-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="31d3e-132">parameters</span><span class="sxs-lookup"><span data-stu-id="31d3e-132">Parameters</span></span>
<span data-ttu-id="31d3e-133">Un webhook puede definir valores para parámetros de runbook que se usan al iniciar runbook Hola por ese webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="31d3e-134">Hola webhook debe incluir valores para todos los parámetros obligatorios de runbook de Hola y puede incluir valores para los parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="31d3e-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="31d3e-135">Incluso después de crear hello webhoook se puede modificar un webhook de tooa del valor configurado de parámetro.</span><span class="sxs-lookup"><span data-stu-id="31d3e-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="31d3e-136">Varios webhooks vinculados tooa único runbook puede utilizar distintos valores de parámetros.</span><span class="sxs-lookup"><span data-stu-id="31d3e-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="31d3e-137">Cuando un cliente inicia un runbook mediante un webhook, no pueden invalidar los valores de parámetro hello definidos en hello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="31d3e-138">datos de tooreceive del cliente de hello, Hola runbook puede aceptar un único parámetro denominado **$WebhookData** del tipo [objeto] que contiene datos de ese cliente hello incluye en la solicitud POST de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Propiedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="31d3e-140">Hola **$WebhookData** objeto tendrá Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="31d3e-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="31d3e-141">Propiedad</span><span class="sxs-lookup"><span data-stu-id="31d3e-141">Property</span></span> | <span data-ttu-id="31d3e-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="31d3e-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="31d3e-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="31d3e-143">WebhookName</span></span> |<span data-ttu-id="31d3e-144">nombre de Hola de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="31d3e-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="31d3e-145">RequestHeader</span></span> |<span data-ttu-id="31d3e-146">Tabla hash que contiene Hola encabezados de solicitud POST de Hola entrante.</span><span class="sxs-lookup"><span data-stu-id="31d3e-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="31d3e-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="31d3e-147">RequestBody</span></span> |<span data-ttu-id="31d3e-148">cuerpo de Hola de solicitud POST de Hola entrante.</span><span class="sxs-lookup"><span data-stu-id="31d3e-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="31d3e-149">Esto conservará todo el formato como cadena de JSON, XML o datos codificados de formulario.</span><span class="sxs-lookup"><span data-stu-id="31d3e-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="31d3e-150">Hola runbook debe escribirse toowork con formato de datos de Hola que se espera.</span><span class="sxs-lookup"><span data-stu-id="31d3e-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="31d3e-151">No hay ninguna configuración de Hola webhook requiere toosupport Hola **$WebhookData** parámetro, y Hola runbook no es necesario tooaccept lo.</span><span class="sxs-lookup"><span data-stu-id="31d3e-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="31d3e-152">Si runbook hello no define el parámetro hello, se omite cualquier información de solicitud de hello enviados desde el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="31d3e-153">Si especifica un valor para $WebhookData al crear webhook hello, ese valor será reemplazada cuando hello webhook inicia runbook de hello con datos de saludo de solicitud de envío del cliente de hello, incluso si el cliente hello no incluye ningún dato en el cuerpo de la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="31d3e-154">Si se inicia un runbook con $WebhookData mediante un método que no sea un webhook, puede proporcionar un valor para $Webhookdata que reconocerá Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="31d3e-155">Este valor debe ser un objeto con hello mismo [propiedades](#details-of-a-webhook) como $Webhookdata para dicho runbook Hola correctamente puede trabajar con ella como si estaba trabajando con WebhookData real pasado por un webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="31d3e-156">Por ejemplo, si se están iniciando Hola siguientes runbook de hello Portal de Azure y desea toopass algunos WebhookData de ejemplo para las pruebas, ya que WebhookData es un objeto, se debe pasar como JSON en hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="31d3e-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="31d3e-158">Para hello anteriormente runbook, si tienes Hola propiedades para el parámetro de hello WebhookData siguientes:</span><span class="sxs-lookup"><span data-stu-id="31d3e-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="31d3e-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="31d3e-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="31d3e-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="31d3e-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="31d3e-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="31d3e-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="31d3e-162">A continuación, pasaría Hola siguiente valor JSON en hello interfaz de usuario para el parámetro de Hola WebhookData:</span><span class="sxs-lookup"><span data-stu-id="31d3e-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="31d3e-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="31d3e-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Iniciar el parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="31d3e-165">valores de Hello de todos los parámetros de entrada se registran con el trabajo del runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="31d3e-166">Esto significa que cualquier entrada proporcionada por cliente hello en solicitud de webhook Hola será tooanyone registran y están disponible con el trabajo de automatización de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="31d3e-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="31d3e-167">Por este motivo, debe tener cuidado en cómo incluir información confidencial en las llamadas de webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="31d3e-168">Seguridad</span><span class="sxs-lookup"><span data-stu-id="31d3e-168">Security</span></span>
<span data-ttu-id="31d3e-169">seguridad de Hola de un webhook se basa en privacidad Hola de su dirección URL que contiene un token de seguridad que permita toobe invocada.</span><span class="sxs-lookup"><span data-stu-id="31d3e-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="31d3e-170">Automatización de Azure no realiza ninguna autenticación en la solicitud de hello siempre y cuando se pone a dirección URL correcta de toohello.</span><span class="sxs-lookup"><span data-stu-id="31d3e-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="31d3e-171">Por esta razón, no debe usarse webhooks para runbooks que realizan funciones muy confidenciales sin usar un medio alternativo de validación de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="31d3e-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="31d3e-172">Puede incluir lógica dentro de hello runbook toodetermine que se llamó por un webhook activando hello **WebhookName** propiedad del parámetro hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="31d3e-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="31d3e-173">Hola runbook podría realizar otras validación buscando información específica de hello **RequestHeader** o **RequestBody** propiedades.</span><span class="sxs-lookup"><span data-stu-id="31d3e-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="31d3e-174">Otra estrategia es toohave Hola runbook realizar una validación de una condición externa cuando recibe una solicitud de webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="31d3e-175">Por ejemplo, considere la posibilidad de un runbook que llama a GitHub cada vez que hay un nuevo repositorio de GitHub de tooa de confirmación.</span><span class="sxs-lookup"><span data-stu-id="31d3e-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="31d3e-176">Hola runbook se conecten toovalidate tooGitHub que realmente solo se hubiera producido una confirmación nuevo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="31d3e-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="31d3e-177">Creación de un webhook</span><span class="sxs-lookup"><span data-stu-id="31d3e-177">Creating a webhook</span></span>
<span data-ttu-id="31d3e-178">Usar hello siguiendo el procedimiento toocreate un nuevo runbook de tooa de webhook vinculado en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31d3e-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="31d3e-179">De hello **hoja de Runbooks** Hola portal de Azure, haga clic en runbook Hola que Hola webhook iniciará tooview su hoja de detalle.</span><span class="sxs-lookup"><span data-stu-id="31d3e-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="31d3e-180">Haga clic en **Webhook** en parte superior de Hola Hola de hello hoja tooopen **Webhook agregar** hoja.</span><span class="sxs-lookup"><span data-stu-id="31d3e-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="31d3e-181">
   ![Botón Webhooks](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="31d3e-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="31d3e-182">Haga clic en **crear nueva webhook** tooopen hello **Crear hoja de webhook**.</span><span class="sxs-lookup"><span data-stu-id="31d3e-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="31d3e-183">Especifique un **nombre**, **fecha de expiración** de webhook de Hola y si debe habilitarse.</span><span class="sxs-lookup"><span data-stu-id="31d3e-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="31d3e-184">Vea [Detalles de un webhook](#details-of-a-webhook) para más información sobre estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="31d3e-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="31d3e-185">Haga clic en el icono de copiar hello y presione Ctrl + C toocopy Hola URL del webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="31d3e-186">A continuación, guárdela en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="31d3e-186">Then record it in a safe place.</span></span>  <span data-ttu-id="31d3e-187">**Una vez creado el webhook hello, no se puede recuperar la dirección URL de hello nuevo.**</span><span class="sxs-lookup"><span data-stu-id="31d3e-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="31d3e-188">
   ![Dirección URL de webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="31d3e-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="31d3e-189">Haga clic en **parámetros** tooprovide valores para parámetros de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="31d3e-190">Si Hola runbook tiene parámetros obligatorios, a continuación, no será capaz de toocreate hello webhook a menos que se proporcionan valores.</span><span class="sxs-lookup"><span data-stu-id="31d3e-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="31d3e-191">Haga clic en **crear** toocreate hello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="31d3e-192">Uso de un webhook</span><span class="sxs-lookup"><span data-stu-id="31d3e-192">Using a webhook</span></span>
<span data-ttu-id="31d3e-193">toouse un webhook una vez creada, la aplicación cliente debe emitir una solicitud HTTP POST con dirección URL de Hola Hola webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="31d3e-194">sintaxis de Hola de hello webhook será Hola siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="31d3e-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="31d3e-195">Hola cliente recibirá uno de los siguientes códigos de retorno de solicitud POST Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="31d3e-196">Código</span><span class="sxs-lookup"><span data-stu-id="31d3e-196">Code</span></span> | <span data-ttu-id="31d3e-197">Texto</span><span class="sxs-lookup"><span data-stu-id="31d3e-197">Text</span></span> | <span data-ttu-id="31d3e-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="31d3e-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="31d3e-199">202</span><span class="sxs-lookup"><span data-stu-id="31d3e-199">202</span></span> |<span data-ttu-id="31d3e-200">Accepted</span><span class="sxs-lookup"><span data-stu-id="31d3e-200">Accepted</span></span> |<span data-ttu-id="31d3e-201">se aceptó la solicitud de Hola y Hola runbook se puso en cola correctamente.</span><span class="sxs-lookup"><span data-stu-id="31d3e-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="31d3e-202">400</span><span class="sxs-lookup"><span data-stu-id="31d3e-202">400</span></span> |<span data-ttu-id="31d3e-203">Bad Request</span><span class="sxs-lookup"><span data-stu-id="31d3e-203">Bad Request</span></span> |<span data-ttu-id="31d3e-204">no se aceptó la solicitud de Hola para uno de hello siguientes motivos.</span><span class="sxs-lookup"><span data-stu-id="31d3e-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="31d3e-205">Hola webhook ha expirado.</span><span class="sxs-lookup"><span data-stu-id="31d3e-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="31d3e-206">Hola webhook está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="31d3e-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="31d3e-207">símbolo (token) de Hello en dirección URL de hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="31d3e-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="31d3e-208">404</span><span class="sxs-lookup"><span data-stu-id="31d3e-208">404</span></span> |<span data-ttu-id="31d3e-209">No encontrado</span><span class="sxs-lookup"><span data-stu-id="31d3e-209">Not Found</span></span> |<span data-ttu-id="31d3e-210">no se aceptó la solicitud de Hola para uno de hello siguientes motivos.</span><span class="sxs-lookup"><span data-stu-id="31d3e-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="31d3e-211">no se encontró el webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="31d3e-212">no se encontró el runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="31d3e-213">no se encontró la cuenta de Hello.</span><span class="sxs-lookup"><span data-stu-id="31d3e-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="31d3e-214">500</span><span class="sxs-lookup"><span data-stu-id="31d3e-214">500</span></span> |<span data-ttu-id="31d3e-215">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="31d3e-215">Internal Server Error</span></span> |<span data-ttu-id="31d3e-216">dirección URL de Hello era válida, pero se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="31d3e-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="31d3e-217">Vuelva a enviar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="31d3e-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="31d3e-218">Suponiendo que la solicitud de hello es correcta, respuesta de webhook Hola contiene Id. de trabajo de hello en formato JSON como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="31d3e-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="31d3e-219">Contendrá un identificador de trabajo único, pero permite el formato JSON de Hola para posibles mejoras futuras.</span><span class="sxs-lookup"><span data-stu-id="31d3e-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="31d3e-220">Hola cliente no puede determinar cuando se completa el trabajo del runbook de Hola o su estado de finalización de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="31d3e-221">Puede determinar esta información con el Id. de trabajo de hello con otro método como [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o hello [API de automatización de Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="31d3e-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="31d3e-222">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="31d3e-222">Example</span></span>
<span data-ttu-id="31d3e-223">Hola de ejemplo siguiente usa Windows PowerShell toostart un runbook con un webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="31d3e-224">Tenga en cuenta que cualquier lenguaje que pueda realizar una solicitud HTTP puede utilizar un webhook; Windows PowerShell se usa aquí simplemente como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="31d3e-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="31d3e-225">Hola runbook está esperando una lista de máquinas virtuales con formato JSON en el cuerpo de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="31d3e-226">También incluiremos información sobre quién está iniciando runbook Hola y Hola fecha se está iniciando en el encabezado de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="31d3e-227">Hello siguiente imagen muestra información de encabezado de hello (con un [Fiddler](http://www.telerik.com/fiddler) seguimiento) de esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="31d3e-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="31d3e-228">Esto incluye los encabezados estándar de una solicitud HTTP en suma toohello personalizado de fecha y de encabezados que se agregan.</span><span class="sxs-lookup"><span data-stu-id="31d3e-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="31d3e-229">Cada uno de estos valores es runbook toohello disponible en hello **RequestHeaders** propiedad de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="31d3e-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Botón Webhooks](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="31d3e-231">Hello siguiente imagen muestra cuerpo de saludo de solicitud de hello (con un [Fiddler](http://www.telerik.com/fiddler) seguimiento) que es toohello disponibles runbook Hola **RequestBody** propiedad de **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="31d3e-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="31d3e-232">Dado tenía el formato de Hola que se incluía en el cuerpo de saludo de solicitud de Hola, esto se formatea como JSON.</span><span class="sxs-lookup"><span data-stu-id="31d3e-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Botón Webhooks](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="31d3e-234">Hello siguiente imagen muestra hello solicitud que se envían desde Windows PowerShell y respuesta resultante Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="31d3e-235">Id. de trabajo de Hola se extrae de la respuesta de Hola y cadena tooa convertido.</span><span class="sxs-lookup"><span data-stu-id="31d3e-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Botón Webhooks](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="31d3e-237">Hello runbook de ejemplo siguiente acepta la solicitud de ejemplo de Hola anterior e inicia máquinas virtuales de hello especificadas en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="31d3e-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="31d3e-238">A partir de runbooks en alertas de respuesta de tooAzure</span><span class="sxs-lookup"><span data-stu-id="31d3e-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="31d3e-239">Habilitado Webhook runbooks pueden ser utilizado tooreact demasiado[alertas Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="31d3e-240">Recursos de Azure se pueden supervisar mediante la recopilación de estadísticas de hello como rendimiento, disponibilidad y el uso con la Ayuda de Hola de alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="31d3e-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="31d3e-241">Puede recibir una alerta basada en los eventos o las métricas de supervisión para los recursos de Azure. Actualmente, las cuentas de automatización solo admiten métricas.</span><span class="sxs-lookup"><span data-stu-id="31d3e-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="31d3e-242">Cuando valor Hola de una métrica especificada supera el umbral de hello asignados o si se desencadena el evento Hola configurado, a continuación, se envía una notificación toohello administradores o coadministradores tooresolve Hola alerta de servicio, para obtener más información sobre las métricas y eventos consulte demasiado[ Alertas de Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="31d3e-243">Además de usar las alertas de Azure como un sistema de notificación, puede comenzar runbooks en tooalerts de respuesta.</span><span class="sxs-lookup"><span data-stu-id="31d3e-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="31d3e-244">Automatización de Azure ofrece Hola capacidad toorun habilitado webhook runbooks con alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="31d3e-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="31d3e-245">Cuando se supera una métrica Hola configurado valor de umbral, a continuación, se activa regla de alerta de Hola y desencadenadores Hola webhook de automatización que a su vez ejecuta runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="31d3e-247">Contexto de alerta</span><span class="sxs-lookup"><span data-stu-id="31d3e-247">Alert context</span></span>
<span data-ttu-id="31d3e-248">Considere la posibilidad de un recurso de Azure como una máquina virtual, es el uso de CPU de esta máquina de métrica de rendimiento clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="31d3e-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="31d3e-249">Si el uso de CPU de hello es 100% o más de una determinada cantidad durante un período largo de tiempo, puede el problema hello toofix de toorestart Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="31d3e-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="31d3e-250">Esto se puede resolver mediante la configuración de una máquina virtual de toohello de regla de alerta y porcentaje de CPU como su métrica de toma de esta regla.</span><span class="sxs-lookup"><span data-stu-id="31d3e-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="31d3e-251">Porcentaje de CPU aquí solo se toma como un ejemplo, pero hay muchas otras métricas que se puede configurar tooyour Azure recursos y reiniciando la máquina virtual de hello es una acción que es realizada toofix este problema, puede configurar Hola runbook tootake otras acciones.</span><span class="sxs-lookup"><span data-stu-id="31d3e-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="31d3e-252">Cuando se activa esta regla de alerta de Hola y desencadenadores Hola runbook habilitado webhook, envía Hola contexto de alerta toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="31d3e-253">[Contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene los detalles incluidos **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** y **marca de tiempo** que son necesarios para el recurso de Hola Hola runbook tooidentify en el que va a tener acción.</span><span class="sxs-lookup"><span data-stu-id="31d3e-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="31d3e-254">Alerta de contexto se incrusta en la parte del cuerpo Hola de hello **WebhookData** objeto runbook toohello enviado y puede tener acceso mediante **Webhook.RequestBody** propiedad</span><span class="sxs-lookup"><span data-stu-id="31d3e-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="31d3e-255">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="31d3e-255">Example</span></span>
<span data-ttu-id="31d3e-256">Crear una máquina virtual de Azure en su suscripción y asociar un [alerta métrica del porcentaje de CPU de toomonitor](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="31d3e-257">Durante la creación de alerta de Hola Asegúrese de que se rellene el campo de webhook de hello con dirección URL de Hola de webhook de Hola que se generó durante la creación de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="31d3e-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="31d3e-258">Hello runbook de ejemplo siguiente se desencadena cuando se activa regla de alerta de Hola y recopila los parámetros de contexto de alerta de Hola que son necesarios para el recurso de Hola Hola runbook tooidentify en el que va a tener acción.</span><span class="sxs-lookup"><span data-stu-id="31d3e-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="31d3e-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31d3e-259">Next steps</span></span>
* <span data-ttu-id="31d3e-260">Para obtener detalles sobre las distintas formas toostart un runbook, consulte [a partir de un Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="31d3e-261">Para obtener información sobre Hola ver estado de un Runbook Job, consulte demasiado[ejecución de un Runbook en automatización de Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="31d3e-262">toolearn toouse acción tootake de automatización de Azure en alertas de Azure, vea [corregir las alertas de VM de Azure con Runbooks de automatización](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="31d3e-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
