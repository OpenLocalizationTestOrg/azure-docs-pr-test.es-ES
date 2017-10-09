---
title: una puerta de enlace de aplicaciones de Azure - plantillas aaaCreate | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate una puerta de enlace de la aplicación de Azure mediante el uso de la plantilla de Azure Resource Manager Hola"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="bf272-103">Crear una puerta de enlace de la aplicación mediante el uso de la plantilla de Azure Resource Manager Hola</span><span class="sxs-lookup"><span data-stu-id="bf272-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf272-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bf272-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="bf272-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bf272-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="bf272-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf272-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="bf272-107">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bf272-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="bf272-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bf272-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="bf272-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="bf272-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="bf272-110">Proporciona conmutación por error y enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="bf272-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="bf272-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="bf272-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="bf272-112">toofind una lista completa de las características admitidas, visite [información general de la puerta de enlace de aplicaciones](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bf272-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="bf272-113">Este artículo le guiará a través de la descarga y modificando una plantilla existente de Azure Resource Manager de GitHub e implementación de plantilla de Hola de hello CLI de Azure, PowerShell y GitHub.</span><span class="sxs-lookup"><span data-stu-id="bf272-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="bf272-114">Si simplemente está implementando la plantilla de Azure Resource Manager Hola directamente desde GitHub sin realizar ningún cambio, omitir toodeploy una plantilla de GitHub.</span><span class="sxs-lookup"><span data-stu-id="bf272-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="bf272-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="bf272-115">Scenario</span></span>

<span data-ttu-id="bf272-116">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="bf272-116">In this scenario you will:</span></span>

* <span data-ttu-id="bf272-117">Creará una instancia de Application Gateway con firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="bf272-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="bf272-118">Creará una red virtual denominada VirtualNetwork1 con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="bf272-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="bf272-119">Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="bf272-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="bf272-120">Configurar dos direcciones IP de back-end configurado previamente para los servidores web de hello desea tooload equilibrar Hola del tráfico.</span><span class="sxs-lookup"><span data-stu-id="bf272-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="bf272-121">En este ejemplo de plantilla, hello direcciones IP de back-end son 10.0.1.10 y 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="bf272-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="bf272-122">Los valores son parámetros de Hola para esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="bf272-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="bf272-123">plantilla de hello toocustomize, puede cambiar reglas, el agente de escucha de hello, SSL y otras opciones de archivo de hello azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="bf272-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Escenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="bf272-125">Descargar y comprender la plantilla de Azure Resource Manager Hola</span><span class="sxs-lookup"><span data-stu-id="bf272-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="bf272-126">Puede descargar Hola existente Azure Resource Manager plantilla toocreate una red virtual y dos subredes desde GitHub, realice los cambios que podría desee y volver a usarla.</span><span class="sxs-lookup"><span data-stu-id="bf272-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="bf272-127">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf272-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="bf272-128">Navegue demasiado[crear puerta de enlace de aplicaciones con el firewall de aplicación web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="bf272-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="bf272-129">Haga clic en **azuredeploy.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="bf272-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="bf272-130">Guarde la carpeta local de hello archivo tooa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bf272-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="bf272-131">Si está familiarizado con las plantillas de Azure Resource Manager, omitir toostep 7.</span><span class="sxs-lookup"><span data-stu-id="bf272-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="bf272-132">Abrir archivo Hola que ha guardado y mire el contenido de hello en **parámetros** en línea</span><span class="sxs-lookup"><span data-stu-id="bf272-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="bf272-133">Los parámetros de la plantilla de Azure Resource Manager proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="bf272-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="bf272-134">Parámetro</span><span class="sxs-lookup"><span data-stu-id="bf272-134">Parameter</span></span> | <span data-ttu-id="bf272-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="bf272-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="bf272-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="bf272-136">**subnetPrefix**</span></span> |<span data-ttu-id="bf272-137">Bloque CIDR de subred de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="bf272-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="bf272-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="bf272-139">Tamaño de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-139">Size of hello application gateway.</span></span>  <span data-ttu-id="bf272-140">WAF solo permite tamaños medianos y grandes.</span><span class="sxs-lookup"><span data-stu-id="bf272-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="bf272-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="bf272-141">**backendIpaddress1**</span></span> |<span data-ttu-id="bf272-142">Dirección IP del primer servidor de web Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="bf272-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="bf272-143">**backendIpaddress2**</span></span> |<span data-ttu-id="bf272-144">Dirección IP del servidor web de la segunda Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="bf272-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="bf272-145">**wafEnabled**</span></span> | <span data-ttu-id="bf272-146">Establecer toodetermine si WAFS está habilitado.</span><span class="sxs-lookup"><span data-stu-id="bf272-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="bf272-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="bf272-147">**wafMode**</span></span> | <span data-ttu-id="bf272-148">Modo de servidor de aplicaciones web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="bf272-149">Las opciones disponibles son **prevención** o **detección**.</span><span class="sxs-lookup"><span data-stu-id="bf272-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="bf272-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="bf272-150">**wafRuleSetType**</span></span> | <span data-ttu-id="bf272-151">Tipo de conjunto de reglas para WAF.</span><span class="sxs-lookup"><span data-stu-id="bf272-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="bf272-152">Actualmente OWASP está Hola solo admite la opción.</span><span class="sxs-lookup"><span data-stu-id="bf272-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="bf272-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="bf272-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="bf272-154">Versión del conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="bf272-154">Ruleset version.</span></span> <span data-ttu-id="bf272-155">OWASP CRS 2.2.9 y 3.0 actualmente son opciones de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="bf272-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="bf272-156">Compruebe el contenido de hello en **recursos** y observe Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="bf272-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="bf272-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="bf272-157">**type**.</span></span> <span data-ttu-id="bf272-158">Tipo de recurso que se está creando plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="bf272-159">En este caso, es de tipo hello `Microsoft.Network/applicationGateways`, que representa una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf272-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="bf272-160">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="bf272-160">**name**.</span></span> <span data-ttu-id="bf272-161">Nombre de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-161">Name for hello resource.</span></span> <span data-ttu-id="bf272-162">Uso de Hola de aviso de `[parameters('applicationGatewayName')]`, lo que significa que ese nombre Hola se proporciona como entrada por usted o por un archivo de parámetros durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="bf272-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="bf272-163">**propiedades**.</span><span class="sxs-lookup"><span data-stu-id="bf272-163">**properties**.</span></span> <span data-ttu-id="bf272-164">Lista de propiedades para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-164">List of properties for hello resource.</span></span> <span data-ttu-id="bf272-165">Esta plantilla utiliza la dirección IP pública y red virtual de Hola durante la creación de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf272-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf272-166">Para más información sobre las plantillas, visite el artículo de [referencia de plantillas de Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="bf272-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="bf272-167">Navegue hacia atrás demasiado[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="bf272-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="bf272-168">Haga clic en **azuredeploy-paremeters.json** y luego en **Sin formato**.</span><span class="sxs-lookup"><span data-stu-id="bf272-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="bf272-169">Guarde la carpeta local de hello archivo tooa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bf272-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="bf272-170">Abrir archivo de Hola que ha guardado y modificar los valores de hello para los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="bf272-171">Usar hello después valores toodeploy Hola aplicación puerta de enlace que se describe en nuestro escenario.</span><span class="sxs-lookup"><span data-stu-id="bf272-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="bf272-172">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="bf272-172">Save hello file.</span></span> <span data-ttu-id="bf272-173">Puede probar las plantillas JSON de Hola y parámetro mediante herramientas de validación de JSON en línea como [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="bf272-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="bf272-174">Implementar la plantilla de Azure Resource Manager hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf272-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="bf272-175">Si nunca ha usado PowerShell de Azure, visite: [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) y seguir Hola instrucciones toosign en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bf272-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="bf272-176">Inicio de sesión tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="bf272-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="bf272-177">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="bf272-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="bf272-178">Son tooauthenticate solicitada con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="bf272-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="bf272-179">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf272-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="bf272-180">Si es necesario, cree un grupo de recursos mediante el uso de hello **New-AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf272-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="bf272-181">En el siguiente ejemplo de Hola, crear un grupo de recursos denominado AppgatewayRG en ubicación UU.</span><span class="sxs-lookup"><span data-stu-id="bf272-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="bf272-182">Ejecute hello **AzureRmResourceGroupDeployment New** cmdlet toodeploy Hola nueva red virtual mediante el uso de hello anteriores de archivos de plantilla y los parámetros que ha descargado y modificado.</span><span class="sxs-lookup"><span data-stu-id="bf272-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="bf272-183">Implementar la plantilla de Azure Resource Manager hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bf272-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="bf272-184">plantilla de Azure Resource Manager hello toodeploy ha descargado mediante la CLI de Azure, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf272-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="bf272-185">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bf272-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="bf272-186">Si es necesario, hello ejecute `az group create` comando toocreate un grupo de recursos, como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="bf272-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="bf272-187">Observe la salida de hello de comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-187">Notice hello output of hello command.</span></span> <span data-ttu-id="bf272-188">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="bf272-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="bf272-189">Para más información sobre los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf272-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="bf272-190">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="bf272-190">**-n (or --name)**.</span></span> <span data-ttu-id="bf272-191">Nombre para el nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-191">Name for hello new resource group.</span></span> <span data-ttu-id="bf272-192">En este escenario, es *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="bf272-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="bf272-193">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="bf272-193">**-l (or --location)**.</span></span> <span data-ttu-id="bf272-194">Región de Azure donde se crea el nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="bf272-195">En este escenario, es *westus*.</span><span class="sxs-lookup"><span data-stu-id="bf272-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="bf272-196">Ejecute hello `az group deployment create` cmdlet toodeploy Hola nueva red virtual mediante el uso de la plantilla de Hola y los parámetros de archivos que ha descargado y modificado en hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="bf272-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="bf272-197">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="bf272-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="bf272-198">Implementar plantilla de Azure Resource Manager hello mediante haga clic en implementar</span><span class="sxs-lookup"><span data-stu-id="bf272-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="bf272-199">Haga clic en implementar es toouse de otra manera plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf272-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="bf272-200">Es una plantilla de toouse fácilmente con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf272-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="bf272-201">Vaya demasiado[crear una puerta de enlace de la aplicación con el servidor de aplicaciones web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="bf272-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="bf272-202">Haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="bf272-202">Click **Deploy tooAzure**.</span></span>

    ![Implementar tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="bf272-204">Rellene los parámetros de Hola para plantilla de implementación de hello en el portal de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bf272-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="bf272-206">Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** y haga clic en **compra**.</span><span class="sxs-lookup"><span data-stu-id="bf272-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="bf272-207">En la hoja de implementación de saludo personalizado, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bf272-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="bf272-208">Proporciona plantillas del Administrador de tooResource de datos de certificado</span><span class="sxs-lookup"><span data-stu-id="bf272-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="bf272-209">Cuando se utiliza SSL con una plantilla, certificado Hola debe toobe proporcionado en una cadena de base64 en lugar de que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="bf272-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="bf272-210">cadena base64 tooa .pfx o .cer tooconvert utilice uno de hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="bf272-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="bf272-211">Hello siguientes comandos convierten cadena base64 de hello certificado tooa, que se puede proporcionar toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="bf272-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="bf272-212">Hola espera el resultado es una cadena que se puede almacenar en una variable y pegar en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf272-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="bf272-213">macOS</span><span class="sxs-lookup"><span data-stu-id="bf272-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="bf272-214">Windows</span><span class="sxs-lookup"><span data-stu-id="bf272-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="bf272-215">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="bf272-215">Delete all resources</span></span>

<span data-ttu-id="bf272-216">toodelete todos los recursos que se crean en este artículo, realice una de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="bf272-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="bf272-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf272-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="bf272-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bf272-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="bf272-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf272-219">Next steps</span></span>

<span data-ttu-id="bf272-220">Si desea que tooconfigure la descarga de SSL, visite: [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="bf272-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="bf272-221">Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, visite: [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="bf272-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="bf272-222">Si desea más información acerca de las opciones de equilibrio de carga en general, visite:</span><span class="sxs-lookup"><span data-stu-id="bf272-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="bf272-223">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="bf272-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="bf272-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="bf272-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

