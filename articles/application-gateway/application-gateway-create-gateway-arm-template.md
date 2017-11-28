---
title: "Creación de una instancia de Azure Application Gateway mediante plantillas | Microsoft Docs"
description: "En esta página se ofrecen instrucciones para crear una instancia de Azure Application Gateway con la plantilla de Azure Resource Manager"
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="ba492-103">Creación de una instancia de Application Gateway con la plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba492-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba492-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ba492-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ba492-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba492-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ba492-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ba492-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ba492-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ba492-109">Puerta de enlace de aplicaciones de Azure es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="ba492-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ba492-110">Proporciona solicitudes HTTP de enrutamiento del rendimiento y conmutación por error y entre distintos servidores, independientemente de que se encuentren en la nube o en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="ba492-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="ba492-111">Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más.</span><span class="sxs-lookup"><span data-stu-id="ba492-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ba492-112">Para encontrar una lista completa de las características admitidas, visite [Introducción a Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba492-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="ba492-113">Este artículo le guiará por los procesos de descarga y modificación de una plantilla de Azure Resource Manager desde GitHub, así como a implementación desde GitHub, PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba492-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="ba492-114">Si simplemente va a implementar la plantilla de Azure Resource Manager directamente desde GitHub sin realizar ningún cambio, vaya a la sección sobre la implementación una plantilla desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba492-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="ba492-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="ba492-115">Scenario</span></span>

<span data-ttu-id="ba492-116">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="ba492-116">In this scenario you will:</span></span>

* <span data-ttu-id="ba492-117">Creará una instancia de Application Gateway con firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ba492-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="ba492-118">Creará una red virtual denominada VirtualNetwork1 con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="ba492-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ba492-119">Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="ba492-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="ba492-120">Instalará dos IP de back-end configuradas con anterioridad para los servidores web cuya carga de tráfico desea equilibrar.</span><span class="sxs-lookup"><span data-stu-id="ba492-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="ba492-121">En esta plantilla de ejemplo, las IP de back-end son 10.0.1.10 y 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="ba492-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="ba492-122">Esos son los parámetros para esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="ba492-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="ba492-123">Para personalizar la plantilla, puede cambiar las reglas, el agente de escucha, la SSL y otras opciones del archivo azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="ba492-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Escenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="ba492-125">Descarga e información sobre la plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="ba492-126">Puede descargar la plantilla de Azure Resource Manager existente para crear una red virtual y dos subredes desde GitHub, realizar todos los cambios que desee y volver a utilizarla.</span><span class="sxs-lookup"><span data-stu-id="ba492-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="ba492-127">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ba492-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="ba492-128">Vaya al artículo sobre la [creación de instancias de Application Gateway con firewall de aplicaciones web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="ba492-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ba492-129">Haga clic en **azuredeploy.json** y luego en **RAW**.</span><span class="sxs-lookup"><span data-stu-id="ba492-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ba492-130">Guarde el archivo en un una carpeta local del equipo.</span><span class="sxs-lookup"><span data-stu-id="ba492-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="ba492-131">Si está familiarizado con las plantillas de Azure Resource Manager, vaya directamente al paso 7.</span><span class="sxs-lookup"><span data-stu-id="ba492-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="ba492-132">Abra el archivo que guardó y vea el contenido de **parameters** en la línea</span><span class="sxs-lookup"><span data-stu-id="ba492-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="ba492-133">Los parámetros de la plantilla de Azure Resource Manager proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ba492-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="ba492-134">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ba492-134">Parameter</span></span> | <span data-ttu-id="ba492-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="ba492-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="ba492-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="ba492-136">**subnetPrefix**</span></span> |<span data-ttu-id="ba492-137">Bloque CIDR de la subred de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ba492-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="ba492-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="ba492-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="ba492-139">Tamaño de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ba492-139">Size of the application gateway.</span></span>  <span data-ttu-id="ba492-140">WAF solo permite tamaños medianos y grandes.</span><span class="sxs-lookup"><span data-stu-id="ba492-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="ba492-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="ba492-141">**backendIpaddress1**</span></span> |<span data-ttu-id="ba492-142">Dirección IP del primer servidor web.</span><span class="sxs-lookup"><span data-stu-id="ba492-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="ba492-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="ba492-143">**backendIpaddress2**</span></span> |<span data-ttu-id="ba492-144">Dirección IP del segundo servidor web.</span><span class="sxs-lookup"><span data-stu-id="ba492-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="ba492-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="ba492-145">**wafEnabled**</span></span> | <span data-ttu-id="ba492-146">Configuración para determinar si WAF está habilitada.</span><span class="sxs-lookup"><span data-stu-id="ba492-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="ba492-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="ba492-147">**wafMode**</span></span> | <span data-ttu-id="ba492-148">Modo del firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ba492-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="ba492-149">Las opciones disponibles son **prevención** o **detección**.</span><span class="sxs-lookup"><span data-stu-id="ba492-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="ba492-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="ba492-150">**wafRuleSetType**</span></span> | <span data-ttu-id="ba492-151">Tipo de conjunto de reglas para WAF.</span><span class="sxs-lookup"><span data-stu-id="ba492-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="ba492-152">Actualmente, OWASP es la única opción compatible.</span><span class="sxs-lookup"><span data-stu-id="ba492-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="ba492-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="ba492-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="ba492-154">Versión del conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="ba492-154">Ruleset version.</span></span> <span data-ttu-id="ba492-155">Actualmente, OWASP CRS 2.2.9 y 3.0 son las opciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="ba492-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="ba492-156">Compruebe el contenido en **resources** y observe las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="ba492-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="ba492-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="ba492-157">**type**.</span></span> <span data-ttu-id="ba492-158">Tipo de recurso que creó la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ba492-158">Type of resource being created by the template.</span></span> <span data-ttu-id="ba492-159">En este caso, el tipo es `Microsoft.Network/applicationGateways`, que representa una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ba492-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="ba492-160">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="ba492-160">**name**.</span></span> <span data-ttu-id="ba492-161">Nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="ba492-161">Name for the resource.</span></span> <span data-ttu-id="ba492-162">Observe el uso de `[parameters('applicationGatewayName')]`, que significa que el nombre lo proporciona el usuario o un archivo de parámetros durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ba492-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="ba492-163">**propiedades**.</span><span class="sxs-lookup"><span data-stu-id="ba492-163">**properties**.</span></span> <span data-ttu-id="ba492-164">Lista de propiedades para el recurso.</span><span class="sxs-lookup"><span data-stu-id="ba492-164">List of properties for the resource.</span></span> <span data-ttu-id="ba492-165">Esta plantilla usa la red virtual y la dirección IP pública durante la creación de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ba492-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ba492-166">Para más información sobre las plantillas, visite el artículo de [referencia de plantillas de Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="ba492-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="ba492-167">Vuelva a [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="ba492-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ba492-168">Haga clic en **azuredeploy-paremeters.json** y luego en **Sin formato**.</span><span class="sxs-lookup"><span data-stu-id="ba492-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ba492-169">Guarde el archivo en un una carpeta local del equipo.</span><span class="sxs-lookup"><span data-stu-id="ba492-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="ba492-170">Abra el archivo que guardó y edite los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="ba492-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="ba492-171">Use los siguientes valores para implementar la instancia de Application Gateway que se describe en nuestro escenario.</span><span class="sxs-lookup"><span data-stu-id="ba492-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="ba492-172">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="ba492-172">Save the file.</span></span> <span data-ttu-id="ba492-173">Puede probar la plantilla de JSON y la plantilla de parámetros mediante las herramientas en línea de validación de JSON como [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="ba492-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="ba492-174">Implementación de la plantilla de Azure Resource Manager mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba492-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="ba492-175">Si es la primera vez que usa Azure PowerShell, visite [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) y siga las instrucciones para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ba492-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="ba492-176">Inicio de sesión en PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba492-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="ba492-177">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="ba492-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="ba492-178">Se le solicita que se autentique con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="ba492-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="ba492-179">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="ba492-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="ba492-180">Si es necesario, cree un grupo de recursos mediante el cmdlet **New-AzureResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ba492-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="ba492-181">En el ejemplo siguiente, se crea un grupo de recursos denominado AppgatewayRG en la ubicación Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="ba492-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="ba492-182">Ejecute el cmdlet **New-AzureRmResourceGroupDeployment** para implementar la nueva red virtual mediante los archivos de plantillas y parámetros que descargó y modificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ba492-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="ba492-183">Implementación de la plantilla de Azure Resource Manager mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ba492-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="ba492-184">Para implementar la plantilla de Azure Resource Manager descargada mediante la CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ba492-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="ba492-185">Si es la primera vez que usa la CLI de Azure, consulte [Instalación de la CLI de Azure](/cli/azure/install-azure-cli) y siga las instrucciones hasta el punto donde tiene que seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba492-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="ba492-186">En caso necesario, ejecute el comando `az group create` para crear un grupo de recursos, como se muestra en el siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="ba492-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="ba492-187">Observe la salida del comando.</span><span class="sxs-lookup"><span data-stu-id="ba492-187">Notice the output of the command.</span></span> <span data-ttu-id="ba492-188">En la lista que se muestra en la salida se explican los parámetros utilizados.</span><span class="sxs-lookup"><span data-stu-id="ba492-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="ba492-189">Para más información sobre los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba492-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="ba492-190">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ba492-190">**-n (or --name)**.</span></span> <span data-ttu-id="ba492-191">Nombre del nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba492-191">Name for the new resource group.</span></span> <span data-ttu-id="ba492-192">En este escenario, es *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="ba492-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="ba492-193">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="ba492-193">**-l (or --location)**.</span></span> <span data-ttu-id="ba492-194">Región de Azure donde se crea el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba492-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="ba492-195">En este escenario, es *westus*.</span><span class="sxs-lookup"><span data-stu-id="ba492-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="ba492-196">Ejecute el cmdlet `az group deployment create` para implementar la nueva red virtual mediante los archivos de plantillas y parámetros que descargó y modificó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="ba492-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="ba492-197">En la lista que se muestra en la salida se explican los parámetros utilizados.</span><span class="sxs-lookup"><span data-stu-id="ba492-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="ba492-198">Implementación de la plantilla de Azure Resource Manager con el método de hacer clic para implementar</span><span class="sxs-lookup"><span data-stu-id="ba492-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="ba492-199">Clic para implementar es otra forma de usar las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba492-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="ba492-200">Se trata de una manera fácil de usar plantillas con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ba492-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="ba492-201">Vaya a [Creación de una instancia de Application Gateway con firewall de aplicaciones web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="ba492-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="ba492-202">Haga clic en **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="ba492-202">Click **Deploy to Azure**.</span></span>

    ![Implementar en Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="ba492-204">Rellene los parámetros de la plantilla de implementación en el portal y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ba492-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="ba492-206">Seleccione **Acepto los términos y condiciones indicados anteriormente** y haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="ba492-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="ba492-207">En la hoja Implementación personalizada, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ba492-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="ba492-208">Proporciona datos de certificado a las plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="ba492-209">Cuando se usa SSL con una plantilla, el certificado debe proporcionarse en una cadena en base 64 en lugar de cargarse.</span><span class="sxs-lookup"><span data-stu-id="ba492-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="ba492-210">Para convertir un archivo .pfx o .cer a una cadena en base 64, use alguno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="ba492-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="ba492-211">Los siguientes comandos convierten el certificado a una cadena en base 64 que se puede proporcionar a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ba492-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="ba492-212">El resultado esperado es una cadena que se puede almacenar en una variable y pegarse en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ba492-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="ba492-213">macOS</span><span class="sxs-lookup"><span data-stu-id="ba492-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="ba492-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ba492-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="ba492-215">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="ba492-215">Delete all resources</span></span>

<span data-ttu-id="ba492-216">Para eliminar todos los recursos creados en este artículo, complete uno de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ba492-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="ba492-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba492-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="ba492-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ba492-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="ba492-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba492-219">Next steps</span></span>

<span data-ttu-id="ba492-220">Si desea configurar la descarga de SSL, consulte [Configuración de una instancia de Application Gateway para la descarga de SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ba492-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ba492-221">Si quiere configurar una instancia de Application Gateway para usarla con un equilibrador de carga interno, consulte [Creación de una instancia de Application Gateway con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="ba492-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="ba492-222">Si desea más información acerca de las opciones de equilibrio de carga en general, visite:</span><span class="sxs-lookup"><span data-stu-id="ba492-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="ba492-223">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="ba492-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ba492-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ba492-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

