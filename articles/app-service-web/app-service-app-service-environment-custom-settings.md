---
title: "Configuración personalizada de entornos del Servicio de aplicaciones"
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
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="e2b41-103">Opciones de configuración personalizada para Entornos del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e2b41-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="e2b41-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e2b41-104">Overview</span></span>
<span data-ttu-id="e2b41-105">Puesto que los entornos del Servicio de aplicaciones están aislados en un solo cliente, hay ciertas opciones de configuración que se pueden aplicar exclusivamente a ellos.</span><span class="sxs-lookup"><span data-stu-id="e2b41-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="e2b41-106">En este artículo se documentan las distintas personalizaciones específicas disponibles para los entornos del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="e2b41-107">Si no cuenta con un entorno de Servicio de aplicaciones, consulte [Creación de un entorno del Servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="e2b41-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="e2b41-108">Puede almacenar las personalizaciones del entorno del Servicio de aplicaciones mediante el uso de una matriz en el nuevo atributo **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="e2b41-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="e2b41-109">Este atributo se encuentra en el diccionario de "Propiedades" de la entidad *hostingEnvironments* de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2b41-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="e2b41-110">La siguiente plantilla abreviada de Resource Manager muestra el atributo **clusterSettings** :</span><span class="sxs-lookup"><span data-stu-id="e2b41-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="e2b41-111">El atributo **clusterSettings** se puede incluir en una plantilla de Resource Manager para actualizar el entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="e2b41-112">Uso del Explorador de recursos de Azure para actualizar un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e2b41-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="e2b41-113">Como alternativa, puede actualizar el entorno del Servicio de aplicaciones mediante el [Explorador de recursos de Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2b41-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="e2b41-114">En el Explorador de recursos, vaya al nodo de App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="e2b41-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="e2b41-115">A continuación, haga clic en el entorno del Servicio de aplicaciones específico que quiere actualizar.</span><span class="sxs-lookup"><span data-stu-id="e2b41-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="e2b41-116">En el panel derecho, haga clic en **Lectura/escritura** en la barra de herramientas superior para permitir la edición interactiva en el Explorador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2b41-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="e2b41-117">Haga clic en el botón azul **Editar** para que la plantilla de Resource Manager se pueda editar.</span><span class="sxs-lookup"><span data-stu-id="e2b41-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="e2b41-118">Desplácese hasta la parte inferior del panel derecho.</span><span class="sxs-lookup"><span data-stu-id="e2b41-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="e2b41-119">El atributo **clusterSettings** se encuentra abajo del todo, donde puede especificar o actualizar su valor.</span><span class="sxs-lookup"><span data-stu-id="e2b41-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="e2b41-120">Escriba (o copie y pegue) la matriz de valores de configuración que quiera en el atributo **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="e2b41-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="e2b41-121">Haga clic en el botón verde **PUT** situado en la parte superior del panel derecho para confirmar el cambio en el entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="e2b41-122">Una vez enviado el cambio, tarda en aplicarse aproximadamente 30 minutos multiplicado por el número de front-ends en el entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="e2b41-123">Por ejemplo, si un entorno del Servicio de aplicaciones tiene cuatro front-ends, tardará aproximadamente dos horas en finalizar la actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="e2b41-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="e2b41-124">Mientras se implementa el cambio de configuración, no será posible realizar otras operaciones de escalado o de cambio de configuración en el entorno del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="e2b41-125">Deshabilitación de TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="e2b41-125">Disable TLS 1.0</span></span>
<span data-ttu-id="e2b41-126">Una pregunta recurrente de los clientes, especialmente de aquellos con auditorías de cumplimiento de PCI, es cómo deshabilitar explícitamente TLS 1.0 en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e2b41-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="e2b41-127">TLS 1.0 se puede deshabilitar mediante la siguiente entrada de **clusterSettings** :</span><span class="sxs-lookup"><span data-stu-id="e2b41-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="e2b41-128">Cambio del orden del conjunto de aplicaciones de cifrado TLS</span><span class="sxs-lookup"><span data-stu-id="e2b41-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="e2b41-129">Otra pregunta de los clientes es si pueden modificar la lista de cifrados negociados por su servidor, y si esto puede lograrse mediante la modificación del atributo **clusterSettings** , como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e2b41-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="e2b41-130">La lista de conjuntos de cifrado disponibles se puede recuperar de este [artículo de MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e2b41-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="e2b41-131">Nota: Si se establecen valores incorrectos para el conjunto de aplicaciones de cifrado que SChannel no entiende, toda la comunicación TLS en el servidor podría dejar de funcionar.</span><span class="sxs-lookup"><span data-stu-id="e2b41-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="e2b41-132">En tal caso, debe quitar la entrada *FrontEndSSLCipherSuiteOrder* de **clusterSettings** y enviar la plantilla de Resource Manager actualizada para volver a la configuración de conjunto de cifrado predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e2b41-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="e2b41-133">Utilice esta funcionalidad con precaución.</span><span class="sxs-lookup"><span data-stu-id="e2b41-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="e2b41-134">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="e2b41-134">Get started</span></span>
<span data-ttu-id="e2b41-135">El sitio de inicio rápido de plantillas de Azure Resource Manager incluye una plantilla con la definición base para [crear un entorno del Servicio de aplicaciones](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="e2b41-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
