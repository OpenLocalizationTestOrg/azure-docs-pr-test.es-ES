---
title: "configuración de aaaCustom para los entornos de servicio de aplicación"
description: "Opciones de configuración personalizada para Entornos del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="0287f-103">Opciones de configuración personalizada para Entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0287f-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="0287f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0287f-104">Overview</span></span>
<span data-ttu-id="0287f-105">Porque los entornos del servicio de aplicación están aisladas tooa solo cliente, hay ciertas opciones de configuración que se pueden aplican tooApp exclusivamente los entornos del servicio.</span><span class="sxs-lookup"><span data-stu-id="0287f-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="0287f-106">Este artículo se explican Hola distintos personalizaciones específicas que están disponibles para entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0287f-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="0287f-107">Si no tiene un entorno de servicio de aplicaciones, consulte [cómo tooCreate un entorno de servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="0287f-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="0287f-108">Puede almacenar las personalizaciones del entorno del servicio de aplicaciones mediante el uso de una matriz en hello nueva **clusterSettings** atributo.</span><span class="sxs-lookup"><span data-stu-id="0287f-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="0287f-109">Este atributo se encuentra en el diccionario de "Propiedades" hello de hello *hostingEnvironments* entidad Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0287f-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="0287f-110">siguiente fragmento de plantilla de administrador de recursos abreviado Hello muestra hello **clusterSettings** atributo:</span><span class="sxs-lookup"><span data-stu-id="0287f-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="0287f-111">Hola **clusterSettings** atributo puede incluirse en un Hola de tooupdate de plantilla entorno del servicio de aplicación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0287f-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="0287f-112">Utilice el Explorador de recursos de Azure tooupdate un entorno de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0287f-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="0287f-113">Como alternativa, puede actualizar Hola entono mediante [Explorador de recursos de Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0287f-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="0287f-114">En el Explorador de recursos, vaya toohello nodo Hola entono (**suscripciones** > **resourceGroups** > **proveedores**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="0287f-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="0287f-115">A continuación, haga clic en Hola entorno específico de servicio de aplicación que desea tooupdate.</span><span class="sxs-lookup"><span data-stu-id="0287f-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="0287f-116">En el panel derecho de hello, haga clic en **lectura/escritura** en hello superior de la barra de herramientas tooallow interactivo de edición en el Explorador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0287f-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="0287f-117">Haga clic en hello azul **editar** plantilla de administrador de recursos de botón toomake Hola editable.</span><span class="sxs-lookup"><span data-stu-id="0287f-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="0287f-118">Desplazamiento toohello la parte inferior del panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="0287f-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="0287f-119">Hola **clusterSettings** atributo se encuentra en la parte inferior de hello, donde puede especificar o actualizar su valor.</span><span class="sxs-lookup"><span data-stu-id="0287f-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="0287f-120">Matriz de Hola de tipo (o copiar y pegar) de los valores de configuración que desee en hello **clusterSettings** atributo.</span><span class="sxs-lookup"><span data-stu-id="0287f-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="0287f-121">Haga clic en hello verde **colocar** botón que se encuentra en parte superior de Hola de hello panel derecho toocommit Hola cambio toohello entorno del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0287f-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="0287f-122">Sin embargo, enviar cambios de hello, tarda aproximadamente 30 minutos multiplicados por número de Hola de servidores front-end en hello entorno del servicio de aplicación para cambiar tootake efecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0287f-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="0287f-123">Por ejemplo, si un entorno de servicio de aplicaciones tiene cuatro servidores front-end, tardará aproximadamente dos horas para toofinish de actualización de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="0287f-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="0287f-124">Mientras se está implantando el cambio de configuración de hello, no hay otras operaciones de escala o las operaciones de cambio de configuración pueden tener lugar en el entorno del servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="0287f-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="0287f-125">Deshabilitación de TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="0287f-125">Disable TLS 1.0</span></span>
<span data-ttu-id="0287f-126">Una pregunta periódica de los clientes, especialmente los clientes que están relacionados con el cumplimiento del estándar PCI auditorías, es cómo tooexplicitly deshabilitar TLS 1.0 para sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0287f-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="0287f-127">TLS 1.0 se puede deshabilitar mediante siguiente hello **clusterSettings** entrada:</span><span class="sxs-lookup"><span data-stu-id="0287f-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="0287f-128">Cambio del orden del conjunto de aplicaciones de cifrado TLS</span><span class="sxs-lookup"><span data-stu-id="0287f-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="0287f-129">Otra cuestión de los clientes es si puede modificar la lista de Hola de cifrado que se negocia entre el servidor y esto puede lograrse mediante la modificación de hello **clusterSettings** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0287f-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="0287f-130">lista de Hola de conjuntos de cifrado disponibles puede obtenerse de [este artículo MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0287f-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="0287f-131">Si se establecen valores incorrectos para los conjuntos de cifrado de hello SChannel no entiende, todos los servidores de tooyour de comunicación TLS podrían dejar de funcionar.</span><span class="sxs-lookup"><span data-stu-id="0287f-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="0287f-132">En tal caso, será necesario hello tooremove *FrontEndSSLCipherSuiteOrder* entrada de **clusterSettings** y enviar Hola actualiza el Administrador de recursos plantilla toorevert toohello atrás predeterminado cifrado configuración de conjunto.</span><span class="sxs-lookup"><span data-stu-id="0287f-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="0287f-133">Utilice esta funcionalidad con precaución.</span><span class="sxs-lookup"><span data-stu-id="0287f-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="0287f-134">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="0287f-134">Get started</span></span>
<span data-ttu-id="0287f-135">sitio de plantilla de inicio rápido de Azure Resource Manager Hola incluye una plantilla de definición de base de Hola para [crear un entorno de servicio de aplicaciones](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="0287f-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
