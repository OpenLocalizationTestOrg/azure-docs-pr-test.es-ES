---
title: "aaaCreate una puerta de enlace de la aplicación de Azure - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación mediante el uso de Hola 1.0 de CLI de Azure en el Administrador de recursos"
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
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="f25df-103">Crear una puerta de enlace de la aplicación mediante el uso de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f25df-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f25df-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f25df-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="f25df-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f25df-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="f25df-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f25df-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="f25df-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f25df-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="f25df-108">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f25df-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="f25df-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f25df-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="f25df-110">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="f25df-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f25df-111">Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="f25df-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="f25df-112">Puerta de enlace de aplicaciones tiene Hola siguientes características de entrega de aplicación: cargar los sondeos de personalizada del estado de equilibrio, afinidad de sesión basado en cookies y descarga de capa de Sockets seguros (SSL), HTTP y la compatibilidad de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="f25df-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="f25df-113">Requisito previo: Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f25df-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="f25df-114">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](../xplat-cli-install.md) y necesita demasiado[tooAzure de inicio de sesión](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f25df-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="f25df-115">Si no tiene una cuenta de Azure, necesitará una.</span><span class="sxs-lookup"><span data-stu-id="f25df-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="f25df-116">Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="f25df-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="f25df-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="f25df-117">Scenario</span></span>

<span data-ttu-id="f25df-118">En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f25df-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="f25df-119">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="f25df-119">This scenario will:</span></span>

* <span data-ttu-id="f25df-120">Creará una puerta de enlace de aplicaciones media con dos instancias.</span><span class="sxs-lookup"><span data-stu-id="f25df-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="f25df-121">Creará una red virtual denominada ContosoVNET con un bloque CIDR reservado de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="f25df-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="f25df-122">Creará una subred denominada subnet01 que usa 10.0.0.0/28 como bloque CIDR.</span><span class="sxs-lookup"><span data-stu-id="f25df-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="f25df-123">Las comprobaciones de la configuración adicional de puerta de enlace de aplicaciones de hello, incluido el estado personalizado, se configuran las direcciones de grupo back-end y reglas adicionales después de configura la puerta de enlace de aplicaciones de hello y no durante la implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="f25df-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f25df-124">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f25df-124">Before you begin</span></span>

<span data-ttu-id="f25df-125">Azure Application Gateway requiere su propia subred.</span><span class="sxs-lookup"><span data-stu-id="f25df-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="f25df-126">Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes.</span><span class="sxs-lookup"><span data-stu-id="f25df-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="f25df-127">Una vez que se implementa una subred tooa de puerta de enlace de aplicaciones, las puertas de enlace de aplicaciones únicas opciones adicionales son toobe puede agregar subred toohello.</span><span class="sxs-lookup"><span data-stu-id="f25df-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="f25df-128">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="f25df-128">Log in tooAzure</span></span>

<span data-ttu-id="f25df-129">Abra hello **Microsoft Azure Command Prompt**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="f25df-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="f25df-130">Una vez que escriba Hola anterior ejemplo, se proporciona un código.</span><span class="sxs-lookup"><span data-stu-id="f25df-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="f25df-131">Navegue toohttps://aka.ms/devicelogin en un proceso de inicio de sesión de explorador toocontinue Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd que muestra el inicio de sesión de dispositivos][1]

<span data-ttu-id="f25df-133">En el Explorador de hello, escriba el código de hello que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="f25df-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="f25df-134">Está página de inicio de sesión tooa redirigida.</span><span class="sxs-lookup"><span data-stu-id="f25df-134">You are redirected tooa sign-in page.</span></span>

![código de tooenter de explorador][2]

<span data-ttu-id="f25df-136">Una vez que se ha especificado el código de hello ha iniciado sesión, cierre Hola explorador toocontinue con el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![ha iniciado sesión correctamente][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="f25df-138">Cambiar tooResource modo de administrador</span><span class="sxs-lookup"><span data-stu-id="f25df-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="f25df-139">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f25df-139">Create hello resource group</span></span>

<span data-ttu-id="f25df-140">Antes de crear la puerta de enlace de aplicaciones de hello, un grupo de recursos se crea la puerta de enlace de aplicaciones de toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="f25df-141">siguiente Hello muestra comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="f25df-142">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="f25df-142">Create a virtual network</span></span>

<span data-ttu-id="f25df-143">Una vez creado el grupo de recursos de hello, se crea una red virtual de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="f25df-144">En el siguiente ejemplo de Hola, espacio de direcciones de hello era tan 10.0.0.0/16 tal como se define en hello anterior notas de escenario.</span><span class="sxs-lookup"><span data-stu-id="f25df-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="f25df-145">Creación de una subred</span><span class="sxs-lookup"><span data-stu-id="f25df-145">Create a subnet</span></span>

<span data-ttu-id="f25df-146">Después de crea la red virtual de hello, se agrega una subred de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f25df-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="f25df-147">Si tiene previsto toouse la puerta de enlace de aplicaciones con una aplicación web hospedado en hello mismo virtual de red como puerta de enlace de aplicación Hola, tooleave seguro espacio suficiente para otra subred.</span><span class="sxs-lookup"><span data-stu-id="f25df-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="f25df-148">Crear puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="f25df-148">Create hello application gateway</span></span>

<span data-ttu-id="f25df-149">Una vez que se crean, subred y red virtual de hello requisitos previos de hello para la puerta de enlace de aplicaciones de hello están completos.</span><span class="sxs-lookup"><span data-stu-id="f25df-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="f25df-150">Además, un archivo .pfx exportado anteriormente hello y certificado contraseña Hola certificado son necesarios para hello siguiendo el paso: direcciones IP de hello utilizadas para hello back-end son direcciones IP de hello para el servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="f25df-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="f25df-151">Estos valores pueden ser cualquier IP privadas en la red virtual de hello, direcciones IP públicas o nombres de dominio completo para los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f25df-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="f25df-152">Para obtener una lista de parámetros que se pueden proporcionar durante la creación de ejecutar el siguiente comando de hello: **crear aplicación-puerta de enlace de red de azure--ayuda**.</span><span class="sxs-lookup"><span data-stu-id="f25df-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="f25df-153">Este ejemplo crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha de hello, grupo back-end, configuración de http de back-end y reglas.</span><span class="sxs-lookup"><span data-stu-id="f25df-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="f25df-154">Puede modificar estos toosuit configuración su implementación una vez que el aprovisionamiento de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="f25df-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="f25df-155">Si ya tiene la aplicación web definida con el grupo de back-end de Hola Hola anteriores pasos, una vez creados, equilibrio de carga comienza.</span><span class="sxs-lookup"><span data-stu-id="f25df-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f25df-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f25df-156">Next steps</span></span>

<span data-ttu-id="f25df-157">Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f25df-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="f25df-158">Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="f25df-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
