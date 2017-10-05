---
title: "Configuración de la descarga SSL para Azure Application Gateway mediante Azure Portal | Microsoft Docs"
description: "En esta página se ofrecen instrucciones para crear una puerta de enlace de aplicaciones con descarga SSL mediante el portal"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="17c6c-103">Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante el portal</span><span class="sxs-lookup"><span data-stu-id="17c6c-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17c6c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="17c6c-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="17c6c-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="17c6c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="17c6c-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="17c6c-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="17c6c-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="17c6c-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="17c6c-108">Azure Application Gateway puede configurarse para terminar la sesión Capa de sockets seguros (SSL) en la puerta de enlace para evitar las costosas tareas de descifrado SSL que tienen lugar en la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="17c6c-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="17c6c-109">La descarga SSL también simplifica la configuración del servidor front-end y la administración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="17c6c-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="17c6c-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="17c6c-110">Scenario</span></span>

<span data-ttu-id="17c6c-111">El siguiente escenario pasa por la configuración de la descarga SSL en una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="17c6c-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="17c6c-112">El escenario supone que ya ha seguido los pasos para [crear una puerta de enlace de aplicaciones](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17c6c-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17c6c-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="17c6c-113">Before you begin</span></span>

<span data-ttu-id="17c6c-114">Para configurar la descarga SSL con una puerta de enlace de aplicaciones, se requiere un certificado.</span><span class="sxs-lookup"><span data-stu-id="17c6c-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="17c6c-115">Este certificado se carga en la puerta de enlace de aplicaciones y se usa para cifrar y descifrar el tráfico enviado a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="17c6c-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="17c6c-116">El certificado debe estar en formato Intercambio de información personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="17c6c-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="17c6c-117">Este formato de archivo permite la exportación de la clave privada, necesaria para que la puerta de enlace de aplicaciones realice el cifrado y descifrado del tráfico.</span><span class="sxs-lookup"><span data-stu-id="17c6c-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="17c6c-118">Incorporación de un agente de escucha HTTPS</span><span class="sxs-lookup"><span data-stu-id="17c6c-118">Add an HTTPS listener</span></span>

<span data-ttu-id="17c6c-119">El agente de escucha HTTPS busca tráfico en función de su configuración y ayuda a enrutar el tráfico a los grupos de back-end.</span><span class="sxs-lookup"><span data-stu-id="17c6c-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="17c6c-120">Paso 1</span><span class="sxs-lookup"><span data-stu-id="17c6c-120">Step 1</span></span>

<span data-ttu-id="17c6c-121">Vaya a Azure Portal y seleccione una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="17c6c-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="17c6c-122">Paso 2</span><span class="sxs-lookup"><span data-stu-id="17c6c-122">Step 2</span></span>

<span data-ttu-id="17c6c-123">Haga clic en Agentes de escucha y en el botón Agregar para agregar un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="17c6c-123">Click Listeners and click the Add button to add a listener.</span></span>

![hoja de información general de puerta de enlace de aplicaciones][1]

### <a name="step-3"></a><span data-ttu-id="17c6c-125">Paso 3</span><span class="sxs-lookup"><span data-stu-id="17c6c-125">Step 3</span></span>

<span data-ttu-id="17c6c-126">Rellene la información necesaria para el agente de escucha y cargue el certificado .pfx. Cuando haya terminado, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="17c6c-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="17c6c-127">**Nombre** : este valor es un nombre descriptivo del agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="17c6c-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="17c6c-128">**Configuración de direcciones IP de front-end** : este valor es la configuración de direcciones IP de front-end usada para el agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="17c6c-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="17c6c-129">**Puerto front-end (nombre/puerto)** : un nombre descriptivo para el puerto usado en el front-end de la puerta de enlace de aplicaciones y el puerto real usado.</span><span class="sxs-lookup"><span data-stu-id="17c6c-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="17c6c-130">**Protocolo** : un modificador para determinar si se usa https o http para el front-end.</span><span class="sxs-lookup"><span data-stu-id="17c6c-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="17c6c-131">**Certificado (nombre/contraseña)** : si se usa la descarga SSL, un certificado .pfx se requiere para esta configuración, al igual que un nombre y contraseña descriptivos.</span><span class="sxs-lookup"><span data-stu-id="17c6c-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![agregar hoja del agente de escucha][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="17c6c-133">Creación de una regla y asociación de la misma al agente de escucha</span><span class="sxs-lookup"><span data-stu-id="17c6c-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="17c6c-134">Ahora se ha creado el agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="17c6c-134">The listener has now been created.</span></span> <span data-ttu-id="17c6c-135">Es hora de crear una regla para controlar el tráfico desde el agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="17c6c-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="17c6c-136">Las reglas definen cómo se enruta el tráfico a los grupos de back-end basándose en varias opciones de configuración, incluido el uso o no de afinidad de sesión basada en cookies, protocolos y sondeos de puertos y estados.</span><span class="sxs-lookup"><span data-stu-id="17c6c-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="17c6c-137">Paso 1</span><span class="sxs-lookup"><span data-stu-id="17c6c-137">Step 1</span></span>

<span data-ttu-id="17c6c-138">Haga clic en las **reglas** de la puerta de enlace de aplicaciones y, a continuación, en Agregar.</span><span class="sxs-lookup"><span data-stu-id="17c6c-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![hoja de reglas de puerta de enlace de aplicaciones][3]

### <a name="step-2"></a><span data-ttu-id="17c6c-140">Paso 2</span><span class="sxs-lookup"><span data-stu-id="17c6c-140">Step 2</span></span>

<span data-ttu-id="17c6c-141">En la hoja **Agregar regla básica** , escriba el nombre descriptivo para la regla y elija el agente de escucha creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="17c6c-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="17c6c-142">Elija el grupo de back-end y la configuración HTTP adecuados y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="17c6c-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![ventana de configuración de https][4]

<span data-ttu-id="17c6c-144">Ahora, la configuración está guardada en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="17c6c-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="17c6c-145">El proceso de guardar para esta configuración puede tardar un rato antes de que pueda verse a través del portal o de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17c6c-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="17c6c-146">Una vez guardada, la puerta de enlace de aplicaciones controla el cifrado y descifrado del tráfico.</span><span class="sxs-lookup"><span data-stu-id="17c6c-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="17c6c-147">Todo el tráfico entre la puerta de enlace de aplicaciones y los servidores web de back-end se controlará mediante http.</span><span class="sxs-lookup"><span data-stu-id="17c6c-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="17c6c-148">Cualquier comunicación dirigida de nuevo al cliente iniciada mediante https se devolverá al cliente cifrado.</span><span class="sxs-lookup"><span data-stu-id="17c6c-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17c6c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17c6c-149">Next steps</span></span>

<span data-ttu-id="17c6c-150">Para aprender a configurar un sondeo de estado personalizado con Azure Application Gateway, consulte la sección sobre cómo [crear un sondeo de estado personalizado](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17c6c-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
