---
title: "Creación de una instancia de Azure Application Gateway mediante la CLI de Azure 2.0 | Microsoft Docs"
description: Aprenda a crear una instancia de Application Gateway mediante la CLI de Azure 2.0 en Resource Manager.
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="6e7f1-103">Creación de una puerta de enlace de aplicaciones mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6e7f1-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e7f1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e7f1-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="6e7f1-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e7f1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="6e7f1-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e7f1-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="6e7f1-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e7f1-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="6e7f1-108">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6e7f1-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="6e7f1-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6e7f1-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="6e7f1-110">Application Gateway es una aplicación virtual dedicada que ofrece un controlador de entrega de aplicaciones (ADC) que se ofrece como servicio y que proporciona numerosas funcionalidades de equilibrio de carga de nivel 7 para una aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6e7f1-111">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="6e7f1-111">CLI versions to complete the task</span></span>

<span data-ttu-id="6e7f1-112">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="6e7f1-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="6e7f1-113">[CLI de Azure 1.0](application-gateway-create-gateway-cli-nodejs.md): la CLI para los modelos de implementación clásica y de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="6e7f1-114">[CLI de Azure 2.0](application-gateway-create-gateway-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="6e7f1-115">Requisito previo: instalar la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6e7f1-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="6e7f1-116">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6e7f1-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="6e7f1-117">Si no tiene una cuenta de Azure, necesitará una.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="6e7f1-118">Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="6e7f1-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="6e7f1-119">Escenario</span><span class="sxs-lookup"><span data-stu-id="6e7f1-119">Scenario</span></span>

<span data-ttu-id="6e7f1-120">En este escenario, aprenderá a crear una puerta de enlace de aplicaciones mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="6e7f1-121">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="6e7f1-121">This scenario will:</span></span>

* <span data-ttu-id="6e7f1-122">Creará una puerta de enlace de aplicaciones media con dos instancias.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="6e7f1-123">Creará una red virtual denominada AdatumAppGatewayVNET con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="6e7f1-124">Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="6e7f1-125">La configuración adicional de la puerta de enlace de aplicaciones, incluidos los sondeos personalizados sobre el estado, las direcciones del grupo de back-end y las reglas se realiza después de que se configura la puerta de enlace de aplicaciones, no durante la implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6e7f1-126">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6e7f1-126">Before you begin</span></span>

<span data-ttu-id="6e7f1-127">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="6e7f1-128">Al crear una red virtual, asegúrese de dejar suficiente espacio de direcciones para que tenga varias subredes.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="6e7f1-129">Una vez que se implementa una puerta de enlace de aplicaciones en una subred adicional solo se pueden agregar a ella puertas de enlace de aplicaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="6e7f1-130">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-130">Log in to Azure</span></span>

<span data-ttu-id="6e7f1-131">Abra el **símbolo del sistema de Microsoft Azure**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="6e7f1-132">También puede usar `az login` sin el modificador de inicio de sesión de dispositivo que exigirá que se escriba un código en aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="6e7f1-133">Una vez que haya escrito el ejemplo anterior, se proporciona un código.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="6e7f1-134">Navegue a https://aka.ms/devicelogin en un explorador para continuar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd que muestra el inicio de sesión de dispositivos][1]

<span data-ttu-id="6e7f1-136">En el explorador, escriba el código que recibió.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="6e7f1-137">Se le redirigirá a una página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-137">You are redirected to a sign-in page.</span></span>

![explorador para escribir código][2]

<span data-ttu-id="6e7f1-139">Una vez especificado el código, habrá iniciado sesión; cierre el explorador para continuar con el escenario.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![ha iniciado sesión correctamente][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="6e7f1-141">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6e7f1-141">Create the resource group</span></span>

<span data-ttu-id="6e7f1-142">Antes de crear la puerta de enlace de aplicaciones, se creará un grupo de recursos para que pueda contenerla.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="6e7f1-143">A continuación, se muestra el comando.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="6e7f1-144">Creación de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6e7f1-144">Create the application gateway</span></span>

<span data-ttu-id="6e7f1-145">Las direcciones IP usadas para el back-end son las direcciones IP del servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="6e7f1-146">Estos valores pueden ser direcciones IP privadas de la red virtual, direcciones IP públicas o nombres de dominio completos de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="6e7f1-147">En el ejemplo siguiente se crea una puerta de enlace de aplicaciones que tiene opciones adicionales para la configuración de http, puertos y reglas.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="6e7f1-148">El ejemplo anterior muestra muchas propiedades que no son necesarias durante la creación de una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="6e7f1-149">En el ejemplo de código siguiente se crea una puerta de enlace de aplicaciones con la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-149">The following code example creates an application gateway with the required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="6e7f1-150">Para ver una lista de parámetros que se pueden usar durante la creación, ejecute el siguiente comando: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="6e7f1-151">Con este ejemplo sea crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha, el grupo de back-end, la configuración de http de back-end y las reglas.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="6e7f1-152">Esta configuración se puede modificar para adaptarse a la implementación una vez que el aprovisionamiento sea correcto.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="6e7f1-153">Si ya definió una aplicación web con el grupo de back-end en los pasos anteriores, una vez creada, comienza el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6e7f1-154">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6e7f1-154">Get application gateway DNS name</span></span>

<span data-ttu-id="6e7f1-155">Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="6e7f1-156">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6e7f1-157">Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="6e7f1-158">[Configuración de un nombre de dominio personalizado en Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="6e7f1-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="6e7f1-159">Para configurar un alias, recupere los detalles de la puerta de enlace de aplicaciones y su nombre de IP o DNS asociado mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="6e7f1-160">El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="6e7f1-161">No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6e7f1-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="6e7f1-162">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="6e7f1-162">Delete all resources</span></span>

<span data-ttu-id="6e7f1-163">Para eliminar todos los recursos creados en este artículo, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6e7f1-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="6e7f1-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e7f1-164">Next steps</span></span>

<span data-ttu-id="6e7f1-165">Para aprender a crear sondeos de estado personalizado, visite [Create a custom probe for Application Gateway by using the portal](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6e7f1-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="6e7f1-166">Para aprender a configurar la descarga de SSL y eliminar la cara descripción de SSL de los servidores web, visite [Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante Azure Resource Manager](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="6e7f1-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
