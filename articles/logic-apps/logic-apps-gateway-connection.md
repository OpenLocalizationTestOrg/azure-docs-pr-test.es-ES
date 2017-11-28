---
title: "aaaAccess orígenes de datos de forma local para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Configurar la puerta de enlace de datos de hello local por lo que puede tener acceso a orígenes de datos en instalaciones de aplicaciones lógicas"
keywords: "obtener acceso a datos, local, transferencia de datos, cifrado, orígenes de datos"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="042f5-104">Orígenes de datos de Access de forma local desde las aplicaciones lógicas con puerta de enlace de datos de hello local</span><span class="sxs-lookup"><span data-stu-id="042f5-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="042f5-105">orígenes de datos tooaccess local desde las aplicaciones lógicas, configure una puerta de enlace de datos local que pueden usar las aplicaciones lógicas con conectores compatibles.</span><span class="sxs-lookup"><span data-stu-id="042f5-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="042f5-106">puerta de enlace de Hello actúa como un puente que permite el cifrado entre los orígenes de datos de forma local y las aplicaciones lógicas y transferencia de datos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="042f5-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="042f5-107">puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="042f5-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="042f5-108">Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="042f5-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="042f5-109">Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="042f5-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="042f5-110">puerta de enlace de Hello es compatible con orígenes de datos de las conexiones toothese local:</span><span class="sxs-lookup"><span data-stu-id="042f5-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="042f5-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="042f5-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="042f5-112">DB2</span><span class="sxs-lookup"><span data-stu-id="042f5-112">DB2</span></span>  
*   <span data-ttu-id="042f5-113">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="042f5-113">File System</span></span>
*   <span data-ttu-id="042f5-114">Informix</span><span class="sxs-lookup"><span data-stu-id="042f5-114">Informix</span></span>
*   <span data-ttu-id="042f5-115">MQ</span><span class="sxs-lookup"><span data-stu-id="042f5-115">MQ</span></span>
*   <span data-ttu-id="042f5-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="042f5-116">MySQL</span></span>
*   <span data-ttu-id="042f5-117">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="042f5-117">Oracle Database</span></span>
*   <span data-ttu-id="042f5-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="042f5-118">PostgreSQL</span></span>
*   <span data-ttu-id="042f5-119">Servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="042f5-119">SAP Application Server</span></span> 
*   <span data-ttu-id="042f5-120">Servidor de mensajes de SAP</span><span class="sxs-lookup"><span data-stu-id="042f5-120">SAP Message Server</span></span>
*   <span data-ttu-id="042f5-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="042f5-121">SharePoint</span></span>
*   <span data-ttu-id="042f5-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="042f5-122">SQL Server</span></span>
*   <span data-ttu-id="042f5-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="042f5-123">Teradata</span></span>

<span data-ttu-id="042f5-124">Estos pasos muestra cómo tooset seguridad Hola local toowork de puerta de enlace de datos con las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="042f5-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="042f5-125">Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="042f5-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="042f5-126">Para obtener información acerca de cómo toouse Hola puerta de enlace con otros servicios, vea estos artículos:</span><span class="sxs-lookup"><span data-stu-id="042f5-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="042f5-127">Puerta de enlace de datos local de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="042f5-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="042f5-128">Puerta de enlace de datos local de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="042f5-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="042f5-129">Puerta de enlace de datos local de Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="042f5-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="042f5-130">Administración de una puerta de enlace de datos local en Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="042f5-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="042f5-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="042f5-131">Requirements</span></span>

* <span data-ttu-id="042f5-132">Debe tener ya [instalada la puerta de enlace de datos de hello en un equipo local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="042f5-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="042f5-133">Cuando inicias sesión en toohello portal de Azure, tendrá toouse Hola mismo trabajo o académica de cuenta que se usó demasiado[instalar la puerta de enlace de datos de hello local](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="042f5-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="042f5-134">Su cuenta de inicio de sesión también debe tener una suscripción de Azure toouse cuando se crea un recurso de puerta de enlace en hello portal de Azure para la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="042f5-135">No puede haber ningún recurso de puerta de enlace de Azure que ya haya solicitado la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="042f5-136">Puede asociar el recurso de una puerta de enlace de Azure de puerta de enlace instalación tooonly.</span><span class="sxs-lookup"><span data-stu-id="042f5-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="042f5-137">Notificación se produce cuando se crea el recurso de puerta de enlace de Hola para que no está disponible para otros recursos de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="042f5-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="042f5-138">Configurar conexión de puerta de enlace de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="042f5-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="042f5-139">1. Hola de instalación de puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="042f5-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="042f5-140">Si no lo ha hecho ya, siga hello [puerta de enlace de pasos tooinstall Hola local datos](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="042f5-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="042f5-141">Antes de continuar con hello otros pasos, asegúrese de que instaló la puerta de enlace de datos de hello en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="042f5-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="042f5-142">2. Crear un recurso de Azure para puerta de enlace de datos de hello local</span><span class="sxs-lookup"><span data-stu-id="042f5-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="042f5-143">Después de instalar la puerta de enlace de hello en un equipo local, debe crear la puerta de enlace de datos como un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="042f5-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="042f5-144">En este paso también se asocia el recurso de puerta de enlace a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="042f5-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="042f5-145">Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="042f5-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="042f5-146">Asegúrese de que toouse Hola mismo trabajo de Azure o dirección de correo electrónico educativa usa puerta de enlace de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="042f5-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="042f5-147">En el menú de la izquierda de hello en Azure, elija **New** > **integración empresarial** > **puerta de enlace de datos local** tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="042f5-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Busque "Puerta de enlace de datos local".](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="042f5-149">En hello **crear puerta de enlace de conexión** hoja, proporcione estos detalles toocreate el recurso de puerta de enlace de datos:</span><span class="sxs-lookup"><span data-stu-id="042f5-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="042f5-150">**Nombre**: escriba un nombre para el recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="042f5-151">**Suscripción**: seleccione Hola tooassociate de suscripción de Azure con su recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="042f5-152">Esta suscripción debe ser Hola misma suscripción que la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="042f5-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="042f5-153">suscripción de Hello predeterminada se basa en hello cuenta de Azure que usan toosign en.</span><span class="sxs-lookup"><span data-stu-id="042f5-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="042f5-154">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente para implementar el recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="042f5-155">Los grupos de recursos le ayudan a administrar recursos de Azure relacionados como una colección.</span><span class="sxs-lookup"><span data-stu-id="042f5-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="042f5-156">**Ubicación**: Azure restringe este toohello ubicación misma región que se seleccionó para su servicio de nube de puerta de enlace de Hola durante [instalación de puerta de enlace](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="042f5-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="042f5-157">Asegúrese de que ubicación de recursos de puerta de enlace de hello coincide con ubicación del servicio de nube de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="042f5-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="042f5-158">En caso contrario, la instalación de puerta de enlace no puede aparecer en lista de puertas de enlace de Hola instalado para tooselect en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="042f5-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="042f5-159">Puede usar regiones diferentes para el recurso de puerta de enlace y la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="042f5-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="042f5-160">**Nombre de la instalación**: si la instalación de puerta de enlace no está seleccionada, seleccionar la puerta de enlace de Hola que instaló anteriormente.</span><span class="sxs-lookup"><span data-stu-id="042f5-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="042f5-161">tooyour de recursos de puerta de enlace tooadd hello Azure panel, elija **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="042f5-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="042f5-162">Cuando termine, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="042f5-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="042f5-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="042f5-163">For example:</span></span>

    ![Proporcionar detalles toocreate la puerta de enlace de datos local](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="042f5-165">toofind o vista de la puerta de enlace de datos en cualquier momento, en hello Azure izquierdo menú principal, vaya demasiado **más servicios** > **integración empresarial** > **datos locales Las puertas de enlace**.</span><span class="sxs-lookup"><span data-stu-id="042f5-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Vaya demasiado "Más servicios", "Integración de la empresa", "Puertas de enlace de datos locales"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="042f5-167">3. Conectar la puerta de enlace de datos de lógica aplicación toohello local</span><span class="sxs-lookup"><span data-stu-id="042f5-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="042f5-168">Ahora que ha creado el recurso de puerta de enlace de datos y su suscripción de Azure asociada a ese recurso, crear una conexión entre la lógica hello y aplicación datos puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="042f5-169">La ubicación de la conexión de puerta de enlace debe existir en hello misma región que la aplicación lógica, pero puede usar una puerta de enlace de datos que existe en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="042f5-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="042f5-170">Hola portal de Azure, cree o abra la aplicación lógica en el Diseñador de la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="042f5-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="042f5-171">Agregue un conector que admita conexiones locales, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="042f5-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="042f5-172">Siguiendo el orden de Hola se muestra, seleccione **conectar a través de puerta de enlace de datos local**, proporcione un nombre único de conexión y Hola información necesaria y seleccionar recurso de puerta de enlace de datos de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="042f5-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="042f5-173">Cuando termine, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="042f5-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="042f5-174">Un nombre de conexión único le ayuda a identificar fácilmente la conexión más adelante, especialmente al crear varias conexiones.</span><span class="sxs-lookup"><span data-stu-id="042f5-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="042f5-175">Si procede, incluir dominio completo de hello para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="042f5-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Creación de conexiones entre la aplicación lógica y la puerta de enlace de datos](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="042f5-177">Enhorabuena, su conexión de puerta de enlace ya está lista para su toouse de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="042f5-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="042f5-178">Editar la configuración de conexión de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="042f5-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="042f5-179">Después de crear una conexión de puerta de enlace de la aplicación lógica, podría interesarle toolater configuración de Hola de actualización para esa conexión concreta.</span><span class="sxs-lookup"><span data-stu-id="042f5-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="042f5-180">conexión de puerta de enlace de Hola toofind:</span><span class="sxs-lookup"><span data-stu-id="042f5-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="042f5-181">En la hoja de la aplicación de lógica de hello, en **herramientas de desarrollo**, seleccione **API conexiones**.</span><span class="sxs-lookup"><span data-stu-id="042f5-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="042f5-182">Hola **API conexiones** panel muestra todas las conexiones de API asociadas a la aplicación lógica, incluidas las conexiones de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="042f5-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Vaya tooyour lógica aplicación, seleccione "API de conexiones"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="042f5-184">O bien, en hello Azure izquierdo menú principal, vaya demasiado **más servicios** > **Web y servicios móviles** > **API conexiones** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociados a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="042f5-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="042f5-185">O bien, en hello Azure izquierdo menú principal, vaya demasiado**todos los recursos** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociadas a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="042f5-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="042f5-186">Seleccionar conexión de puerta de enlace de Hola que desee tooview o editar y elija **conexión editar API**.</span><span class="sxs-lookup"><span data-stu-id="042f5-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="042f5-187">Si las actualizaciones no surten efecto, intente [detener y reiniciar el servicio de puerta de enlace de Windows hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="042f5-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="042f5-188">Cambiar o eliminar el recurso de puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="042f5-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="042f5-189">toocreate un recurso de la puerta de enlace diferente, asociar la puerta de enlace a un recurso diferente o quitar recursos de la puerta de enlace de hello, puede eliminar los recursos de la puerta de enlace de hello sin afectar a la instalación de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="042f5-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="042f5-190">En hello Azure izquierdo menú principal, vaya demasiado**todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="042f5-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="042f5-191">Busque y seleccione el recurso de puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="042f5-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="042f5-192">Elija **puerta de enlace de datos local**y en la barra de herramientas de recursos de hello, elija **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="042f5-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="042f5-193">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="042f5-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="042f5-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="042f5-194">Next steps</span></span>

* [<span data-ttu-id="042f5-195">Protección de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="042f5-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="042f5-196">Ejemplos y escenarios habituales de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="042f5-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
