---
title: "Creación de flujos de trabajo a partir de plantillas (Azure Logic Apps) | Microsoft Docs"
description: "Aprenda a crear flujos de trabajo rápidamente mediante plantillas de Azure Logic App para conectar las aplicaciones e integrar los datos."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89272869f7dfaa34cbd2ad32d67dca0955e6158b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="8b70a-103">Configuración de un flujo de trabajo mediante un patrón o una plantilla pregenerados para empezar a trabajar rápidamente</span><span class="sxs-lookup"><span data-stu-id="8b70a-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="8b70a-104">¿Qué son las plantillas de aplicaciones lógicas?</span><span class="sxs-lookup"><span data-stu-id="8b70a-104">What are logic app templates</span></span>
<span data-ttu-id="8b70a-105">Una plantilla de aplicación lógica es una aplicación lógica pregenerada que se puede usar para comenzar rápidamente a crear su propio flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8b70a-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="8b70a-106">Estas plantillas son una buena forma de detectar patrones distintos que se pueden crear mediante aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="8b70a-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="8b70a-107">Puede usar estas plantillas tal cual o modificarlas para adaptarlas a su escenario.</span><span class="sxs-lookup"><span data-stu-id="8b70a-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="8b70a-108">Información general de plantillas disponibles</span><span class="sxs-lookup"><span data-stu-id="8b70a-108">Overview of available templates</span></span>
<span data-ttu-id="8b70a-109">Hay muchas plantillas disponibles publicadas actualmente en la plataforma de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="8b70a-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="8b70a-110">A continuación se muestran algunas categorías de ejemplo, así como los tipos de conectores que utilizan.</span><span class="sxs-lookup"><span data-stu-id="8b70a-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="8b70a-111">Plantillas de empresa en la nube</span><span class="sxs-lookup"><span data-stu-id="8b70a-111">Enterprise cloud templates</span></span>
<span data-ttu-id="8b70a-112">Plantillas que integran Dynamics CRM, Salesforce, Box, Blob de Azure y otros conectores para sus necesidades empresariales en la nube.</span><span class="sxs-lookup"><span data-stu-id="8b70a-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="8b70a-113">Entre los ejemplos de lo que se puede hacer con estas plantillas se incluye la organización de sus clientes potenciales y la copia de seguridad de los datos de archivos corporativos.</span><span class="sxs-lookup"><span data-stu-id="8b70a-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="8b70a-114">Plantillas de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="8b70a-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="8b70a-115">Configuraciones de canalizaciones VETER (Validación, Extracción, Transformación, Enriquecimiento, Enrutamiento), recepción de documentos X12 EDI a través de AS2 y transformación en XML así como control de mensajes X12 y AS2.</span><span class="sxs-lookup"><span data-stu-id="8b70a-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="8b70a-116">Plantillas de patrón de protocolo</span><span class="sxs-lookup"><span data-stu-id="8b70a-116">Protocol pattern templates</span></span>
<span data-ttu-id="8b70a-117">Estas plantillas constan de aplicaciones lógicas que contienen patrones de protocolo como solicitud-respuesta a través de HTTP así como integraciones a través de FTP y SFTP.</span><span class="sxs-lookup"><span data-stu-id="8b70a-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="8b70a-118">Utilícelas tal y como están o como base para crear patrones más complejos de protocolo.</span><span class="sxs-lookup"><span data-stu-id="8b70a-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="8b70a-119">Plantillas de productividad personal</span><span class="sxs-lookup"><span data-stu-id="8b70a-119">Personal productivity templates</span></span>
<span data-ttu-id="8b70a-120">Entre los patrones para ayudar a mejorar la productividad personal se incluyen plantillas que permiten establecer avisos diarios, convierten los elementos de trabajo importantes en listas de tareas pendientes y automatizan las tareas largas con un único paso de aprobación de usuario.</span><span class="sxs-lookup"><span data-stu-id="8b70a-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="8b70a-121">Plantillas en la nube del consumidor</span><span class="sxs-lookup"><span data-stu-id="8b70a-121">Consumer cloud templates</span></span>
<span data-ttu-id="8b70a-122">Plantillas simples que se integran con los servicios de las redes sociales como Twitter, Slack o el correo electrónico, capaces a la larga de reforzar las iniciativas de marketing de las redes sociales.</span><span class="sxs-lookup"><span data-stu-id="8b70a-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="8b70a-123">También se incluyen plantillas como la de copia repetitiva que permiten aumentar la productividad mediante el ahorro del tiempo invertido en tareas habitualmente repetitivas.</span><span class="sxs-lookup"><span data-stu-id="8b70a-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="8b70a-124">Creación de una aplicación lógica mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="8b70a-124">How to create a logic app using a template</span></span>
<span data-ttu-id="8b70a-125">Para comenzar a usar la plantilla de aplicaciones lógicas, vaya al diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="8b70a-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="8b70a-126">Si accede al diseñador abriendo una aplicación lógica que ya existe, esta se cargará automáticamente en la vista del diseñador.</span><span class="sxs-lookup"><span data-stu-id="8b70a-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="8b70a-127">Sin embargo, si va a crear una nueva aplicación lógica, verá la pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="8b70a-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="8b70a-128">En esta pantalla, puede elegir empezar con una aplicación lógica en blanco o una plantilla predefinida.</span><span class="sxs-lookup"><span data-stu-id="8b70a-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="8b70a-129">Si selecciona una de las plantillas, se proporcionará información adicional.</span><span class="sxs-lookup"><span data-stu-id="8b70a-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="8b70a-130">En este ejemplo, se utilizará la plantilla *When a new file is created in Dropbox, copy it to OneDrive* (Si se crea un nuevo archivo en Dropbox, cópiese en OneDrive).</span><span class="sxs-lookup"><span data-stu-id="8b70a-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="8b70a-131">Si decide utilizar la plantilla, solo tiene que seleccionar el botón *Usar esta plantilla* .</span><span class="sxs-lookup"><span data-stu-id="8b70a-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="8b70a-132">Se le pedirá que inicie sesión en sus cuentas en función de los conectores que utiliza la plantilla.</span><span class="sxs-lookup"><span data-stu-id="8b70a-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="8b70a-133">O, si ya ha establecido previamente una conexión con estos conectores, puede seleccionar el botón Continuar tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="8b70a-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="8b70a-134">Después de establecer la conexión y seleccionar el botón *Continuar*, la aplicación lógica se abre en la vista del diseñador.</span><span class="sxs-lookup"><span data-stu-id="8b70a-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="8b70a-135">En el ejemplo anterior, como sucede con muchas plantillas, algunos de los campos de propiedades obligatorios pueden rellenarse dentro de los conectores; sin embargo, puede que algunos requieran un valor antes de poder implementar correctamente la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="8b70a-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="8b70a-136">Si intenta implementar sin rellenar algunos de los campos que faltan, se le notificará con un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="8b70a-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="8b70a-137">Si desea volver al visor de plantillas, seleccione el botón *Plantillas* en la barra de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="8b70a-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="8b70a-138">Al volver al visor de plantillas, perderá cualquier progreso no guardado.</span><span class="sxs-lookup"><span data-stu-id="8b70a-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="8b70a-139">Antes de volver al visor de plantillas, verá un mensaje de advertencia que le avisará de esto.</span><span class="sxs-lookup"><span data-stu-id="8b70a-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="8b70a-140">Implementación de una aplicación lógica creada desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="8b70a-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="8b70a-141">Una vez que ha cargado la plantilla y realizado los cambios deseados, seleccione el botón Guardar situado en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="8b70a-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="8b70a-142">Esto permite guardar y publicar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="8b70a-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="8b70a-143">Para más información sobre cómo agregar más pasos en una plantilla de aplicación lógica existente o realizar modificaciones en general, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b70a-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>
