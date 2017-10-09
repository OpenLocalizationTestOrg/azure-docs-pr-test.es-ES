---
title: aaaConnect tooan sistema SAP en Azure Logic Apps local | Documentos de Microsoft
description: "Conectar sistema SAP de tooan locales del flujo de trabajo de aplicación lógica a través de puerta de enlace de datos de hello en local"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="446f4-103">Conectar sistema SAP de tooan local desde las aplicaciones lógicas con el conector de SAP de Hola</span><span class="sxs-lookup"><span data-stu-id="446f4-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="446f4-104">puerta de enlace de datos de Hello local permite toomanage datos y obtener acceso seguro a recursos que son locales.</span><span class="sxs-lookup"><span data-stu-id="446f4-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="446f4-105">Este tema muestra cómo puede conectarse el sistema SAP local de lógica aplicaciones tooan.</span><span class="sxs-lookup"><span data-stu-id="446f4-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="446f4-106">En este ejemplo, la aplicación lógica solicita un IDOC a través de HTTP y envía la respuesta Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="446f4-107">Limitaciones actuales:</span><span class="sxs-lookup"><span data-stu-id="446f4-107">Current limitations:</span></span> 
> - <span data-ttu-id="446f4-108">La aplicación lógica agota el tiempo si no finalizan todos los pasos necesarios para la respuesta de hello en hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="446f4-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="446f4-109">En este escenario, las solicitudes pueden quedar bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="446f4-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="446f4-110">Selector de archivos de Hello no muestra todos los campos disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="446f4-111">En este escenario, puede agregar manualmente rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="446f4-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="446f4-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="446f4-112">Prerequisites</span></span>

- <span data-ttu-id="446f4-113">Instalar y configurar hello más reciente [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127) versión 1.15.6150.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="446f4-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="446f4-114">[Cómo tooconnect toohello local puerta de enlace de datos en una aplicación de lógica](http://aka.ms/logicapps-gateway) listas Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="446f4-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="446f4-115">puerta de enlace de Hello debe instalarse en un equipo local para poder continuar.</span><span class="sxs-lookup"><span data-stu-id="446f4-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="446f4-116">Descarga y la biblioteca de cliente SAP más reciente de instalación de hello en hello misma máquina donde se instaló la puerta de enlace de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="446f4-117">Use cualquiera de hello después de las versiones SAP:</span><span class="sxs-lookup"><span data-stu-id="446f4-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="446f4-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="446f4-118">SAP Server</span></span>
        - <span data-ttu-id="446f4-119">Cualquier servidor de SAP que Hola de soporte técnico de .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="446f4-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="446f4-120">SAP Client</span><span class="sxs-lookup"><span data-stu-id="446f4-120">SAP Client</span></span>
        - <span data-ttu-id="446f4-121">SAP .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="446f4-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="446f4-122">Agregar desencadenadores y acciones para conectar el sistema SAP tooyour</span><span class="sxs-lookup"><span data-stu-id="446f4-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="446f4-123">Conector de SAP de Hello tiene acciones, pero no los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="446f4-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="446f4-124">Por lo tanto, tenemos toouse otro desencadenador en el inicio de Hola de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="446f4-125">Agregar desencadenador de solicitud/respuesta de hello y, a continuación, seleccione **nuevo paso**.</span><span class="sxs-lookup"><span data-stu-id="446f4-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="446f4-126">Seleccione **agregar una acción**y, a continuación, seleccione el conector de SAP de hello escribiendo `SAP` en el campo de búsqueda de hello:</span><span class="sxs-lookup"><span data-stu-id="446f4-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Seleccione el servidor de aplicaciones de SAP o el servidor de mensajes de SAP.](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="446f4-128">Seleccione el [**servidor de aplicaciones de SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o el [**servidor de mensajes de SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), según la configuración de SAP.</span><span class="sxs-lookup"><span data-stu-id="446f4-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="446f4-129">Si no tiene una conexión existente, son toocreate solicitada uno.</span><span class="sxs-lookup"><span data-stu-id="446f4-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="446f4-130">Seleccione **conectar a través de puerta de enlace de datos local**y escriba los detalles de hello para el sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="446f4-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Agregar tooSAP de cadena de conexión](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="446f4-132">En **puerta de enlace**, seleccione una puerta de enlace existente o tooinstall una nueva puerta de enlace, seleccione **instalar la puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="446f4-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Instalación de una nueva puerta de enlace](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="446f4-134">Después de escribir todos los detalles de hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="446f4-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="446f4-135">Lógica de aplicaciones se configura y comprueba la conexión de hello, asegurándose de que la conexión de hello funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="446f4-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="446f4-136">Escriba un nombre para la conexión SAP.</span><span class="sxs-lookup"><span data-stu-id="446f4-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="446f4-137">Ahora hay disponibles distintas opciones de SAP de Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-137">hello different SAP options are now available.</span></span> <span data-ttu-id="446f4-138">toofind la categoría de IDOC, seleccione uno de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="446f4-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="446f4-139">O escriba manualmente en la ruta de acceso de Hola y respuesta de hello seleccione HTTP en hello **cuerpo** campo:</span><span class="sxs-lookup"><span data-stu-id="446f4-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Acción de SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="446f4-141">Agregar acción de hello para la creación de un **respuesta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="446f4-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="446f4-142">mensaje de bienvenida de respuesta debe ser de salida de hello SAP.</span><span class="sxs-lookup"><span data-stu-id="446f4-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="446f4-143">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="446f4-143">Save your logic app.</span></span> <span data-ttu-id="446f4-144">Probarla mediante el envío de un IDOC a través de la dirección URL de desencadenador de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="446f4-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="446f4-145">Después de Hola que se envía el IDOC, esperar respuesta de Hola de aplicación lógica de hello:</span><span class="sxs-lookup"><span data-stu-id="446f4-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="446f4-146">Consulte cómo demasiado[supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="446f4-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="446f4-147">Ahora que el conector de SAP de Hola se agrega la aplicación de la lógica de tooyour, empezar a explorar otras funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="446f4-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="446f4-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="446f4-148">BAPI</span></span>
- <span data-ttu-id="446f4-149">RFC</span><span class="sxs-lookup"><span data-stu-id="446f4-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="446f4-150">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="446f4-150">Get help</span></span>

<span data-ttu-id="446f4-151">tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="446f4-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="446f4-152">toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="446f4-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="446f4-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="446f4-153">Next steps</span></span>

- <span data-ttu-id="446f4-154">Obtenga información acerca de cómo toovalidate, transformación y otras funciones de BizTalk similar en hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="446f4-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="446f4-155">[Conectar datos locales tooon](../logic-apps/logic-apps-gateway-connection.md) desde las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="446f4-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
