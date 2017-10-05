---
title: "Conexión a un sistema SAP local en Azure Logic Apps | Microsoft Docs"
description: "Conexión a un sistema SAP local en el flujo de trabajo de aplicaciones lógicas a través de la puerta de enlace de datos local"
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
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="0a4c2-103">Conexión a un sistema SAP local en el flujo de trabajo de aplicaciones lógicas con el conector SAP</span><span class="sxs-lookup"><span data-stu-id="0a4c2-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="0a4c2-104">La puerta de enlace de datos local le permite administrar los datos y acceder de manera segura a los recursos locales.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="0a4c2-105">En este tema se muestra cómo se pueden conectar las aplicaciones lógicas a un sistema SAP local.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="0a4c2-106">En este ejemplo, la aplicación lógica solicita un IDOC a través de HTTP y devuelve la respuesta.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="0a4c2-107">Limitaciones actuales:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-107">Current limitations:</span></span> 
> - <span data-ttu-id="0a4c2-108">La aplicación lógica agota el tiempo si todos los pasos necesarios para la respuesta no finalizan dentro del [límite de tiempo de espera de la solicitud](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="0a4c2-109">En este escenario, las solicitudes pueden quedar bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="0a4c2-110">El selector de archivos no muestra todos los campos disponibles.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="0a4c2-111">En este escenario, puede agregar manualmente rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a4c2-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a4c2-112">Prerequisites</span></span>

- <span data-ttu-id="0a4c2-113">Instale y configure la versión 1.15.6150.1 u otra más reciente de la [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="0a4c2-114">En [Conexión a la puerta de enlace de datos local para las aplicaciones lógicas](http://aka.ms/logicapps-gateway) se enumeran los pasos.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="0a4c2-115">La puerta de enlace debe instalarse en una máquina local para poder continuar.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="0a4c2-116">Descargue e instale la última biblioteca de clientes de SAP en la misma máquina en la que instaló la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="0a4c2-117">Use cualquiera de las versiones de SAP siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="0a4c2-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="0a4c2-118">SAP Server</span></span>
        - <span data-ttu-id="0a4c2-119">Cualquier SAP Server que admita .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="0a4c2-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="0a4c2-120">SAP Client</span><span class="sxs-lookup"><span data-stu-id="0a4c2-120">SAP Client</span></span>
        - <span data-ttu-id="0a4c2-121">SAP .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="0a4c2-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="0a4c2-122">Incorporación de desencadenadores y acciones para conectarse al sistema SAP</span><span class="sxs-lookup"><span data-stu-id="0a4c2-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="0a4c2-123">El conector SAP tiene acciones, pero no desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="0a4c2-124">Por lo tanto, tenemos que usar otro desencadenador al principio del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="0a4c2-125">Agregue el desencadenador Request/Response (Solicitud/respuesta) y, a continuación, seleccione **Nuevo paso**.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="0a4c2-126">Seleccione **Agregar una acción**y, a continuación, seleccione el conector SAP escribiendo `SAP` en el campo de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Seleccione el servidor de aplicaciones de SAP o el servidor de mensajes de SAP.](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="0a4c2-128">Seleccione el [**servidor de aplicaciones de SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o el [**servidor de mensajes de SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), según la configuración de SAP.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="0a4c2-129">Si no tiene una conexión existente, se le pedirá que cree una.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="0a4c2-130">Seleccione **Connect via on-premises data gateway** (Conectarse mediante la puerta de enlace de datos local) y especifique los detalles del sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Agregue una cadena de conexión a SAP.](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="0a4c2-132">En **Puerta de enlace**, seleccione una puerta de enlace existente, o instale una nueva; seleccione **Instalar puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Instalación de una nueva puerta de enlace](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="0a4c2-134">Después de escribir todos los detalles, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="0a4c2-135">Logic Apps configura y comprueba la conexión, asegurándose de que la conexión funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="0a4c2-136">Escriba un nombre para la conexión SAP.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="0a4c2-137">Las distintas opciones de SAP ahora están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-137">The different SAP options are now available.</span></span> <span data-ttu-id="0a4c2-138">Para buscar la categoría IDOC, selecciónela en la lista.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="0a4c2-139">O escriba manualmente en la ruta de acceso y seleccione la respuesta HTTP en el campo **cuerpo**:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![Acción de SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="0a4c2-141">Agregue la acción para crear una **respuesta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="0a4c2-142">El mensaje de respuesta debe proceder de la salida SAP.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="0a4c2-143">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-143">Save your logic app.</span></span> <span data-ttu-id="0a4c2-144">Pruébela enviando un IDOC a través de la dirección URL del desencadenador HTTP.</span><span class="sxs-lookup"><span data-stu-id="0a4c2-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="0a4c2-145">Una vez enviado el IDOC, espere a recibir la respuesta de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="0a4c2-146">Consulte cómo [supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="0a4c2-147">Ahora que se ha agregado el conector SAP a la aplicación lógica, empiece a explorar otras funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="0a4c2-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="0a4c2-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="0a4c2-148">BAPI</span></span>
- <span data-ttu-id="0a4c2-149">RFC</span><span class="sxs-lookup"><span data-stu-id="0a4c2-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="0a4c2-150">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="0a4c2-150">Get help</span></span>

<span data-ttu-id="0a4c2-151">Para formular preguntas, o responderlas, y saber lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="0a4c2-152">Para ayudar a mejorar Azure Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a4c2-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a4c2-153">Next steps</span></span>

- <span data-ttu-id="0a4c2-154">Obtenga información acerca de cómo validar, transformar y realizar otras funciones similares a las de BizTalk en [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a4c2-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="0a4c2-155">[Conexión a datos locales](../logic-apps/logic-apps-gateway-connection.md) desde aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="0a4c2-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
