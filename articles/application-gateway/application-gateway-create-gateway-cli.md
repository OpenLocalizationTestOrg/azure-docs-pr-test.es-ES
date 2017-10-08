---
title: "aaaCreate una puerta de enlace de la aplicación de Azure - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación mediante el uso de Hola 2.0 de CLI de Azure en el Administrador de recursos"
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
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="0dbfd-103">Crear una puerta de enlace de la aplicación mediante el uso de hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0dbfd-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dbfd-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0dbfd-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="0dbfd-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0dbfd-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="0dbfd-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dbfd-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="0dbfd-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0dbfd-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="0dbfd-108">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0dbfd-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="0dbfd-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="0dbfd-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="0dbfd-110">Application Gateway es una aplicación virtual dedicada que ofrece un controlador de entrega de aplicaciones (ADC) que se ofrece como servicio y que proporciona numerosas funcionalidades de equilibrio de carga de nivel 7 para una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0dbfd-111">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="0dbfd-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="0dbfd-112">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="0dbfd-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0dbfd-113">[Azure 1.0 de CLI](application-gateway-create-gateway-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="0dbfd-114">[Azure 2.0 CLI](application-gateway-create-gateway-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="0dbfd-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="0dbfd-115">Requisito previo: Instalar Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0dbfd-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="0dbfd-116">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0dbfd-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="0dbfd-117">Si no tiene una cuenta de Azure, necesitará una.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="0dbfd-118">Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="0dbfd-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="0dbfd-119">Escenario</span><span class="sxs-lookup"><span data-stu-id="0dbfd-119">Scenario</span></span>

<span data-ttu-id="0dbfd-120">En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="0dbfd-121">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="0dbfd-121">This scenario will:</span></span>

* <span data-ttu-id="0dbfd-122">Creará una puerta de enlace de aplicaciones media con dos instancias.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="0dbfd-123">Creará una red virtual denominada AdatumAppGatewayVNET con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="0dbfd-124">Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="0dbfd-125">Las comprobaciones de la configuración adicional de puerta de enlace de aplicaciones de hello, incluido el estado personalizado, se configuran las direcciones de grupo back-end y reglas adicionales después de configura la puerta de enlace de aplicaciones de hello y no durante la implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0dbfd-126">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0dbfd-126">Before you begin</span></span>

<span data-ttu-id="0dbfd-127">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="0dbfd-128">Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="0dbfd-129">Una vez que se implementa una subred tooa de puerta de enlace de aplicaciones, las puertas de enlace de la aplicación solo adicionales pueden agregarse toohello subred.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="0dbfd-130">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="0dbfd-130">Log in tooAzure</span></span>

<span data-ttu-id="0dbfd-131">Abra hello **Microsoft Azure Command Prompt**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="0dbfd-132">También puede usar `az login` sin el modificador de hello para el inicio de sesión de dispositivo que requiere proporcionar un código en aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="0dbfd-133">Una vez que escriba Hola anterior ejemplo, se proporciona un código.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="0dbfd-134">Navegue toohttps://aka.ms/devicelogin en un proceso de inicio de sesión de explorador toocontinue Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd que muestra el inicio de sesión de dispositivos][1]

<span data-ttu-id="0dbfd-136">En el Explorador de hello, escriba el código de hello que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="0dbfd-137">Está página de inicio de sesión tooa redirigida.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-137">You are redirected tooa sign-in page.</span></span>

![código de tooenter de explorador][2]

<span data-ttu-id="0dbfd-139">Una vez que se ha especificado el código de hello ha iniciado sesión, cierre Hola explorador toocontinue con el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![ha iniciado sesión correctamente][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="0dbfd-141">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="0dbfd-141">Create hello resource group</span></span>

<span data-ttu-id="0dbfd-142">Antes de crear la puerta de enlace de aplicaciones de hello, un grupo de recursos se crea la puerta de enlace de aplicaciones de toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="0dbfd-143">siguiente Hello muestra comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="0dbfd-144">Crear puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="0dbfd-144">Create hello application gateway</span></span>

<span data-ttu-id="0dbfd-145">direcciones IP de Hello usadas para hello back-end son direcciones IP de hello para el servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="0dbfd-146">Estos valores pueden ser cualquier IP privadas en la red virtual de hello, direcciones IP públicas o nombres de dominio completo para los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="0dbfd-147">Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación tiene opciones de configuración de http, los puertos y las reglas de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="0dbfd-148">Hello en el ejemplo anterior se muestra muchas propiedades que no son necesarios durante la creación de hello de una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="0dbfd-149">Hola el ejemplo de código siguiente crea una puerta de enlace de la aplicación con información de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-149">hello following code example creates an application gateway with hello required information.</span></span>

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
> <span data-ttu-id="0dbfd-150">Para obtener una lista de parámetros que se pueden proporcionar durante el siguiente comando de Hola de creación que se ejecute: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="0dbfd-151">Este ejemplo crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha de hello, grupo back-end, configuración de http de back-end y reglas.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="0dbfd-152">Puede modificar estos toosuit configuración su implementación una vez que el aprovisionamiento de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="0dbfd-153">Si ya tiene la aplicación web definida con el grupo de back-end de Hola Hola anteriores pasos, una vez creados, equilibrio de carga comienza.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0dbfd-154">Obtención del nombre DNS de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0dbfd-154">Get application gateway DNS name</span></span>

<span data-ttu-id="0dbfd-155">Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0dbfd-156">Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0dbfd-157">los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="0dbfd-158">[Configuración de un nombre de dominio personalizado en Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="0dbfd-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="0dbfd-159">tooconfigure un alias, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="0dbfd-160">nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="0dbfd-161">no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0dbfd-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="0dbfd-162">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="0dbfd-162">Delete all resources</span></span>

<span data-ttu-id="0dbfd-163">toodelete todos los recursos que se crean en este artículo, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="0dbfd-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="0dbfd-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dbfd-164">Next steps</span></span>

<span data-ttu-id="0dbfd-165">Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0dbfd-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="0dbfd-166">Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="0dbfd-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
