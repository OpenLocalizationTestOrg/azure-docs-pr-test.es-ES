---
title: "Obtener acceso a orígenes de datos locales para Azure Logic Apps | Documentos de Microsoft"
description: "Configure la puerta de enlace de datos local para poder obtener acceso a orígenes de datos locales desde aplicaciones lógicas."
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="1c8b7-104">Obtener acceso a orígenes de datos locales desde aplicaciones lógicas con la puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="1c8b7-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="1c8b7-105">Para obtener acceso a orígenes de datos locales desde las aplicaciones lógicas, configure una puerta de enlace de datos local que puedan usar las aplicaciones lógicas con conectores compatibles.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="1c8b7-106">La puerta de enlace actúa como un puente que permite la transferencia rápida de datos y el cifrado entre orígenes de datos locales y las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="1c8b7-107">La puerta de enlace retransmite datos desde orígenes locales en canales cifrados hasta Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="1c8b7-108">Todo el tráfico se origina como tráfico de salida seguro desde el agente de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="1c8b7-109">Más información sobre [cómo funciona la puerta de enlace de datos](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="1c8b7-110">La puerta de enlace admite conexiones a estos orígenes de datos locales:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="1c8b7-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="1c8b7-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="1c8b7-112">DB2</span><span class="sxs-lookup"><span data-stu-id="1c8b7-112">DB2</span></span>  
*   <span data-ttu-id="1c8b7-113">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="1c8b7-113">File System</span></span>
*   <span data-ttu-id="1c8b7-114">Informix</span><span class="sxs-lookup"><span data-stu-id="1c8b7-114">Informix</span></span>
*   <span data-ttu-id="1c8b7-115">MQ</span><span class="sxs-lookup"><span data-stu-id="1c8b7-115">MQ</span></span>
*   <span data-ttu-id="1c8b7-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="1c8b7-116">MySQL</span></span>
*   <span data-ttu-id="1c8b7-117">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="1c8b7-117">Oracle Database</span></span>
*   <span data-ttu-id="1c8b7-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1c8b7-118">PostgreSQL</span></span>
*   <span data-ttu-id="1c8b7-119">Servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="1c8b7-119">SAP Application Server</span></span> 
*   <span data-ttu-id="1c8b7-120">Servidor de mensajes de SAP</span><span class="sxs-lookup"><span data-stu-id="1c8b7-120">SAP Message Server</span></span>
*   <span data-ttu-id="1c8b7-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="1c8b7-121">SharePoint</span></span>
*   <span data-ttu-id="1c8b7-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1c8b7-122">SQL Server</span></span>
*   <span data-ttu-id="1c8b7-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="1c8b7-123">Teradata</span></span>

<span data-ttu-id="1c8b7-124">En estos pasos se indica cómo configurar la puerta de enlace de datos local para trabajar con las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="1c8b7-125">Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="1c8b7-126">Para información sobre cómo usar la puerta de enlace con otros servicios, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="1c8b7-127">Puerta de enlace de datos local de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="1c8b7-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="1c8b7-128">Puerta de enlace de datos local de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1c8b7-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="1c8b7-129">Puerta de enlace de datos local de Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="1c8b7-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="1c8b7-130">Administración de una puerta de enlace de datos local en Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="1c8b7-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="1c8b7-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1c8b7-131">Requirements</span></span>

* <span data-ttu-id="1c8b7-132">Debe tener [instalada la puerta de enlace de datos local en un equipo local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="1c8b7-133">Al iniciar sesión en Azure Portal, tiene que usar la misma cuenta profesional o educativa que se usó para [instalar la puerta de enlace de datos local](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="1c8b7-134">Además, su cuenta de inicio de sesión debe tener una suscripción de Azure que se usará cuando cree un recurso de puerta de enlace en Azure Portal para la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="1c8b7-135">No puede haber ningún recurso de puerta de enlace de Azure que ya haya solicitado la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="1c8b7-136">Solo puede asociar la instalación de la puerta de enlace a un recurso de puerta de enlace de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="1c8b7-137">La notificación se produce al crear el recurso de puerta de enlace, de modo que la instalación no está disponible para otros recursos.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="1c8b7-138">Configuración de una conexión de puerta de enlace de datos</span><span class="sxs-lookup"><span data-stu-id="1c8b7-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="1c8b7-139">1. Instalación de la puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="1c8b7-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="1c8b7-140">Si aún no lo ha hecho, siga los [pasos para instalar la puerta de enlace de datos local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="1c8b7-141">Antes de continuar con los demás pasos, asegúrese de haber instalado la puerta de enlace de datos en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="1c8b7-142">2. Creación de un recurso de Azure para la puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="1c8b7-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="1c8b7-143">Después de instalar la puerta de enlace en un equipo local, debe crear la puerta de enlace de datos como recurso en Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="1c8b7-144">En este paso también se asocia el recurso de puerta de enlace a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="1c8b7-145">Inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="1c8b7-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="1c8b7-146">Asegúrese de usar la misma dirección de correo electrónico profesional o educativa de Azure que se usó para instalar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="1c8b7-147">En el menú de la izquierda de Azure, elija **Nuevo** > **Enterprise Integration** > **Puerta de enlace de datos local**, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Busque "Puerta de enlace de datos local".](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="1c8b7-149">En la hoja **Crear puerta de enlace de conexión**, proporcione estos detalles para crear el recurso de puerta de enlace de datos:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="1c8b7-150">**Nombre**: escriba un nombre para el recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="1c8b7-151">**Suscripción**: seleccione la suscripción de Azure que se asociará al recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="1c8b7-152">Esta suscripción debe ser la misma que la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="1c8b7-153">La suscripción predeterminada se basa en la cuenta de Azure que usó para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="1c8b7-154">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente para implementar el recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="1c8b7-155">Los grupos de recursos le ayudan a administrar recursos de Azure relacionados como una colección.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="1c8b7-156">**Ubicación**: Azure restringe esta ubicación a la misma región que se seleccionó para el servicio en la nube de puerta de enlace durante la [instalación de la puerta de enlace](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="1c8b7-157">Asegúrese de que la ubicación del recurso de puerta de enlace coincide con la ubicación del servicio en la nube de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="1c8b7-158">De lo contrario, es posible que la instalación de la puerta de enlace no aparezca en la lista de puertas de enlace instaladas para que la pueda seleccionar en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="1c8b7-159">Puede usar regiones diferentes para el recurso de puerta de enlace y la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="1c8b7-160">**Nombre de la instalación**: si la instalación de la puerta de enlace no está seleccionada, seleccione la puerta de enlace que ha instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="1c8b7-161">Para agregar el recurso de puerta de enlace al panel de Azure, elija **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="1c8b7-162">Cuando termine, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="1c8b7-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-163">For example:</span></span>

    ![Proporcionar detalles para crear la puerta de enlace de datos local](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="1c8b7-165">Para buscar o ver la puerta de enlace de datos en cualquier momento, en el menú principal de Azure de la izquierda, vaya a **Más servicios** > **Enterprise Integration** > **Puertas de enlace de datos locales**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Vaya a "Más servicios", "Enterprise Integration", "Puertas de enlace de datos locales"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="1c8b7-167">3. Conexión de la aplicación lógica a la puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="1c8b7-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="1c8b7-168">Ahora que ha creado el recurso de puerta de enlace de datos y ha asociado su suscripción de Azure a ese recurso, cree una conexión entre la aplicación lógica y la puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="1c8b7-169">La ubicación de la conexión de puerta de enlace debe existir en la misma región que la aplicación lógica, pero puede usar una puerta de enlace de datos que exista en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="1c8b7-170">En Azure Portal, cree o abra la aplicación lógica en el Diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="1c8b7-171">Agregue un conector que admita conexiones locales, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="1c8b7-172">Siguiendo con el orden que se muestra, seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local), proporcione un nombre único de conexión y la información necesaria, y seleccione el recurso de puerta de enlace de datos que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="1c8b7-173">Cuando termine, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="1c8b7-174">Un nombre de conexión único le ayuda a identificar fácilmente la conexión más adelante, especialmente al crear varias conexiones.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="1c8b7-175">Si procede, incluya también el dominio completo para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![Creación de conexiones entre la aplicación lógica y la puerta de enlace de datos](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="1c8b7-177">Enhorabuena, la conexión de la puerta de enlace ya está lista para que la use la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="1c8b7-178">Editar la configuración de conexión de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="1c8b7-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="1c8b7-179">Después de crear una conexión de puerta de enlace para la aplicación lógica, es posible que quiera actualizar más tarde la configuración de esa conexión concreta.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="1c8b7-180">Para buscar la conexión de puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="1c8b7-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="1c8b7-181">En la hoja de la aplicación lógica, en **Herramientas de desarrollo**, seleccione **Conexiones de API**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="1c8b7-182">En el panel **Conexiones de API** se muestran todas las conexiones de API asociadas a la aplicación lógica, incluidas las conexiones de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Vaya a la aplicación lógica y seleccione "Conexiones de API".](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="1c8b7-184">O bien, en el menú principal de Azure de la izquierda, vaya a **Más servicios** > **Servicios web y móviles** > **Conexiones de API** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociadas con la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="1c8b7-185">O bien, en el menú principal de Azure de la izquierda, vaya a **Todos los recursos** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociadas con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="1c8b7-186">Seleccione la conexión de puerta de enlace que quiere ver o editar y elija **Editar conexión de API**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="1c8b7-187">Si las actualizaciones no surten efecto, intente [detener y reiniciar el servicio de Windows de puerta de enlace](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="1c8b7-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="1c8b7-188">Cambiar o eliminar el recurso de puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="1c8b7-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="1c8b7-189">Para crear un recurso de puerta de enlace diferente, asociar la puerta de enlace a un recurso diferente o quitar el recurso de puerta de enlace, puede eliminar el recurso de puerta de enlace sin que afecte a la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="1c8b7-190">En el menú principal de Azure de la izquierda, vaya a **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="1c8b7-191">Busque y seleccione el recurso de puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="1c8b7-192">Elija **Puerta de enlace de datos local** y, en la barra de herramientas de recursos, elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="1c8b7-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="1c8b7-193">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="1c8b7-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="1c8b7-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c8b7-194">Next steps</span></span>

* [<span data-ttu-id="1c8b7-195">Protección de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="1c8b7-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="1c8b7-196">Ejemplos y escenarios habituales de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="1c8b7-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
