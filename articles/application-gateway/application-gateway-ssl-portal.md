---
title: 'Portal de Azure - puerta de enlace de aplicaciones de Azure: la descarga de SSL aaaConfigure | Documentos de Microsoft'
description: "Esta página proporciona toocreate de instrucciones mediante el portal de Hola la descarga de una puerta de enlace de la aplicación con SSL"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="f875e-103">Configurar una puerta de enlace de la aplicación para la descarga SSL mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="f875e-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f875e-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f875e-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="f875e-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="f875e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="f875e-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f875e-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="f875e-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f875e-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="f875e-108">Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web.</span><span class="sxs-lookup"><span data-stu-id="f875e-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="f875e-109">Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="f875e-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="f875e-110">Scenario</span></span>

<span data-ttu-id="f875e-111">Hola siguiendo escenario va a través de configuración de la descarga de SSL en una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f875e-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="f875e-112">Hello escenario se supone que ya ha seguido los pasos de hello demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f875e-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f875e-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f875e-113">Before you begin</span></span>

<span data-ttu-id="f875e-114">descarga SSL de tooconfigure con una puerta de enlace de la aplicación, se requiere un certificado.</span><span class="sxs-lookup"><span data-stu-id="f875e-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="f875e-115">Este certificado se carga en la puerta de enlace de aplicaciones de hello, utiliza tooencrypt y descifrar el tráfico de hello enviado a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="f875e-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="f875e-116">certificado de Hello debe toobe en formato de intercambio de información Personal (pfx).</span><span class="sxs-lookup"><span data-stu-id="f875e-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="f875e-117">Este formato de archivo permite Hola privada toobe clave exportado que requiere Hola aplicación puerta de enlace tooperform Hola cifrado y descifrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="f875e-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="f875e-118">Incorporación de un agente de escucha HTTPS</span><span class="sxs-lookup"><span data-stu-id="f875e-118">Add an HTTPS listener</span></span>

<span data-ttu-id="f875e-119">escucha HTTPS de Hello busca tráfico basándose en su configuración y ayuda a los grupos de ruta Hola tráfico toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="f875e-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="f875e-120">Paso 1</span><span class="sxs-lookup"><span data-stu-id="f875e-120">Step 1</span></span>

<span data-ttu-id="f875e-121">Navegue toohello portal de Azure y seleccione una puerta de enlace de la aplicación existente</span><span class="sxs-lookup"><span data-stu-id="f875e-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="f875e-122">Paso 2</span><span class="sxs-lookup"><span data-stu-id="f875e-122">Step 2</span></span>

<span data-ttu-id="f875e-123">Haga clic en agentes de escucha y haga clic en hello Agregar botón tooadd un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f875e-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![hoja de información general de puerta de enlace de aplicaciones][1]

### <a name="step-3"></a><span data-ttu-id="f875e-125">Paso 3</span><span class="sxs-lookup"><span data-stu-id="f875e-125">Step 3</span></span>

<span data-ttu-id="f875e-126">Rellene Hola la información necesaria para el agente de escucha de Hola y Hola .pfx certificado de carga, cuando haya terminado, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="f875e-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="f875e-127">**Nombre de** -este valor es un nombre descriptivo del agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="f875e-128">**Configuración de IP de Frontend** -este valor es la configuración de IP de front-end de Hola que se usa para el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="f875e-129">**Puerto de front-end (nombre/puerto)** -un nombre descriptivo para el puerto de hello usado en front-end de Hola de puerta de enlace de aplicaciones de Hola y Hola puerto real se utilizan.</span><span class="sxs-lookup"><span data-stu-id="f875e-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="f875e-130">**Protocolo** -un toodetermine conmutador si se utiliza https o http para front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="f875e-131">**Certificado (nombre/contraseña)** : si se usa la descarga SSL, un certificado .pfx se requiere para esta configuración, al igual que un nombre y contraseña descriptivos.</span><span class="sxs-lookup"><span data-stu-id="f875e-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![agregar hoja del agente de escucha][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="f875e-133">Crear una regla y asociar el agente de escucha de toohello</span><span class="sxs-lookup"><span data-stu-id="f875e-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="f875e-134">se ha creado el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-134">hello listener has now been created.</span></span> <span data-ttu-id="f875e-135">Es hora toocreate un tráfico de hello toohandle de regla de agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="f875e-136">Las reglas definen cómo el tráfico es enrutado toohello grupos de back-end en función de varios valores de configuración, incluso si se usa la afinidad de sesión basado en cookies, protocolo, puerto y comprobaciones de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="f875e-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="f875e-137">Paso 1</span><span class="sxs-lookup"><span data-stu-id="f875e-137">Step 1</span></span>

<span data-ttu-id="f875e-138">Haga clic en hello **reglas** de puerta de enlace de aplicación Hola y, a continuación, haga clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="f875e-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![hoja de reglas de puerta de enlace de aplicaciones][3]

### <a name="step-2"></a><span data-ttu-id="f875e-140">Paso 2</span><span class="sxs-lookup"><span data-stu-id="f875e-140">Step 2</span></span>

<span data-ttu-id="f875e-141">En hello **Agregar regla básica** hoja, escriba Hola nombre descriptivo para la regla de Hola y elija el agente de escucha de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f875e-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="f875e-142">Elija grupo back-end adecuados de Hola y configuración de http y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="f875e-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![ventana de configuración de https][4]

<span data-ttu-id="f875e-144">configuración de Hello ahora se guarda toohello puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f875e-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="f875e-145">Hola guardar proceso para esta configuración puede tardar unos instantes antes de que se tooview disponible a través del portal de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f875e-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="f875e-146">Puerta de enlace de aplicaciones una vez guardado Hola controla Hola cifrado y descifrado de tráfico.</span><span class="sxs-lookup"><span data-stu-id="f875e-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="f875e-147">Se controlará todo el tráfico entre la puerta de enlace de aplicaciones de Hola y servidores de hello back-end web a través de http.</span><span class="sxs-lookup"><span data-stu-id="f875e-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="f875e-148">Cualquier cliente de atrás toohello comunicación si inicia a través de https se devolverán a cliente toohello cifrada.</span><span class="sxs-lookup"><span data-stu-id="f875e-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f875e-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f875e-149">Next steps</span></span>

<span data-ttu-id="f875e-150">toolearn cómo tooconfigure personalizada del estado de sondeo con puerta de enlace de aplicaciones de Azure, consulte [crear un sondeo de estado personalizado](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f875e-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
