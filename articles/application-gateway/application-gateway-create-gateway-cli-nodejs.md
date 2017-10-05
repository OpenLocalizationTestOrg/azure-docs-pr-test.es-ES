---
title: "Creación de una instancia de Azure Application Gateway (CLI de Azure 1.0) | Microsoft Docs"
description: Aprenda a crear una puerta de enlace de aplicaciones mediante la CLI de Azure 1.0 en Resource Manager.
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="d85a9-103">Creación de una puerta de enlace de aplicaciones mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d85a9-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d85a9-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d85a9-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="d85a9-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d85a9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="d85a9-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="d85a9-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="d85a9-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d85a9-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="d85a9-108">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d85a9-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="d85a9-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d85a9-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="d85a9-110">Puerta de enlace de aplicaciones de Azure es un equilibrador de carga de nivel 7 .</span><span class="sxs-lookup"><span data-stu-id="d85a9-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="d85a9-111">Proporciona conmutación por error, solicitudes HTTP de enrutamiento de rendimiento entre distintos servidores, independientemente de que se encuentren en la nube o en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="d85a9-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="d85a9-112">Puerta de enlace de aplicaciones tiene las siguientes características de entrega de aplicaciones: equilibrio de carga HTTP, afinidad de sesiones basada en cookies, descarga SSL (capa de sockets seguros), sondeos personalizados sobre el estado y compatibilidad con sitios múltiples.</span><span class="sxs-lookup"><span data-stu-id="d85a9-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="d85a9-113">Requisito previo: instalar la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d85a9-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="d85a9-114">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](../xplat-cli-install.md) e [iniciar sesión en Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d85a9-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="d85a9-115">Si no tiene una cuenta de Azure, necesitará una.</span><span class="sxs-lookup"><span data-stu-id="d85a9-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="d85a9-116">Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d85a9-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="d85a9-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="d85a9-117">Scenario</span></span>

<span data-ttu-id="d85a9-118">En este escenario, aprenderá a crear una puerta de enlace de aplicaciones mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d85a9-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="d85a9-119">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="d85a9-119">This scenario will:</span></span>

* <span data-ttu-id="d85a9-120">Creará una puerta de enlace de aplicaciones media con dos instancias.</span><span class="sxs-lookup"><span data-stu-id="d85a9-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="d85a9-121">Creará una red virtual denominada ContosoVNET con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="d85a9-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="d85a9-122">Creará una subred denominada subnet01 que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="d85a9-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="d85a9-123">La configuración adicional de la puerta de enlace de aplicaciones, incluidos los sondeos personalizados sobre el estado, las direcciones del grupo de back-end y las reglas se realiza después de que se configura la puerta de enlace de aplicaciones, no durante la implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="d85a9-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d85a9-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d85a9-124">Before you begin</span></span>

<span data-ttu-id="d85a9-125">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="d85a9-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="d85a9-126">Al crear una red virtual, asegúrese de dejar suficiente espacio de direcciones para que tenga varias subredes.</span><span class="sxs-lookup"><span data-stu-id="d85a9-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="d85a9-127">Una vez que se implementa una puerta de enlace de aplicaciones en una subred adicional solo se pueden agregar a ella puertas de enlace de aplicaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="d85a9-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="d85a9-128">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="d85a9-128">Log in to Azure</span></span>

<span data-ttu-id="d85a9-129">Abra el **símbolo del sistema de Microsoft Azure**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="d85a9-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="d85a9-130">Una vez que haya escrito el ejemplo anterior, se proporciona un código.</span><span class="sxs-lookup"><span data-stu-id="d85a9-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="d85a9-131">Navegue a https://aka.ms/devicelogin en un explorador para continuar el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d85a9-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd que muestra el inicio de sesión de dispositivos][1]

<span data-ttu-id="d85a9-133">En el explorador, escriba el código que recibió.</span><span class="sxs-lookup"><span data-stu-id="d85a9-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="d85a9-134">Se le redirigirá a una página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d85a9-134">You are redirected to a sign-in page.</span></span>

![explorador para escribir código][2]

<span data-ttu-id="d85a9-136">Una vez especificado el código, habrá iniciado sesión; cierre el explorador para continuar con el escenario.</span><span class="sxs-lookup"><span data-stu-id="d85a9-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![ha iniciado sesión correctamente][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="d85a9-138">Cambie al modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d85a9-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="d85a9-139">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d85a9-139">Create the resource group</span></span>

<span data-ttu-id="d85a9-140">Antes de crear la puerta de enlace de aplicaciones, se creará un grupo de recursos para que pueda contenerla.</span><span class="sxs-lookup"><span data-stu-id="d85a9-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="d85a9-141">A continuación, se muestra el comando.</span><span class="sxs-lookup"><span data-stu-id="d85a9-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="d85a9-142">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="d85a9-142">Create a virtual network</span></span>

<span data-ttu-id="d85a9-143">Una vez creado el grupo de recursos, se crea una red virtual para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d85a9-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="d85a9-144">En el ejemplo siguiente, el espacio de direcciones era 10.0.0.0/16 tal como se definió en las notas del escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="d85a9-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="d85a9-145">Creación de una subred</span><span class="sxs-lookup"><span data-stu-id="d85a9-145">Create a subnet</span></span>

<span data-ttu-id="d85a9-146">Después de crear la red virtual, se agrega una subred para la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d85a9-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="d85a9-147">Si piensa utilizar la puerta de enlace de aplicaciones con una aplicación web hospedada en la misma red virtual que la puerta de enlace de aplicaciones asegúrese de dejar suficiente espacio para otra subred.</span><span class="sxs-lookup"><span data-stu-id="d85a9-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="d85a9-148">Creación de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d85a9-148">Create the application gateway</span></span>

<span data-ttu-id="d85a9-149">Una vez que se crean la red virtual y la subred, los requisitos previos de la puerta de enlace de aplicaciones están completos.</span><span class="sxs-lookup"><span data-stu-id="d85a9-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="d85a9-150">Además, para el paso siguiente son necesarios un certificado .pfx exportado previamente y la contraseña para el certificado. La direcciones IP que se usan para el back-end son las direcciones IP para el servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="d85a9-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="d85a9-151">Estos valores pueden ser direcciones IP privadas de la red virtual, direcciones IP públicas o nombres de dominio completos de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="d85a9-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="d85a9-152">Para ver una lista de parámetros que se pueden usar durante la creación, ejecute el siguiente comando: **azure network application-gateway create --help**.</span><span class="sxs-lookup"><span data-stu-id="d85a9-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="d85a9-153">Con este ejemplo sea crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha, el grupo de back-end, la configuración de http de back-end y las reglas.</span><span class="sxs-lookup"><span data-stu-id="d85a9-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="d85a9-154">Esta configuración se puede modificar para adaptarse a la implementación una vez que el aprovisionamiento sea correcto.</span><span class="sxs-lookup"><span data-stu-id="d85a9-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="d85a9-155">Si ya definió una aplicación web con el grupo de back-end en los pasos anteriores, una vez creada, comienza el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="d85a9-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d85a9-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d85a9-156">Next steps</span></span>

<span data-ttu-id="d85a9-157">Para aprender a crear sondeos de estado personalizado, visite [Create a custom probe for Application Gateway by using the portal](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d85a9-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="d85a9-158">Para aprender a configurar la descarga de SSL y eliminar la cara descripción de SSL de los servidores web, visite [Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante Azure Resource Manager](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="d85a9-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
