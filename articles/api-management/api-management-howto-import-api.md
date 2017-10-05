---
title: Importar una API en Azure API Management | Microsoft Docs
description: "Obtenga información sobre cómo importar una API y sus operaciones en Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="f8d81-103">Importación de la definición de una API con operaciones en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="f8d81-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="f8d81-104">En Administración de API se pueden crear nuevas API y agregar las operaciones manualmente o se puede importar la API junto con las operaciones en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="f8d81-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="f8d81-105">Las API y sus operaciones se pueden importar con los siguientes formatos.</span><span class="sxs-lookup"><span data-stu-id="f8d81-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="f8d81-106">WADL</span><span class="sxs-lookup"><span data-stu-id="f8d81-106">WADL</span></span>
* <span data-ttu-id="f8d81-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="f8d81-107">Swagger</span></span>

<span data-ttu-id="f8d81-108">En esta guía se muestra cómo crear una API e importar sus operaciones en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="f8d81-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="f8d81-109">Para obtener más información sobre la creación manual de una API y la incorporación de operaciones, consulte [Creación de API][How to create APIs] e [Incorporación de operaciones a una API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="f8d81-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="f8d81-110"><a name="import-api"> </a>Importación de una API</span><span class="sxs-lookup"><span data-stu-id="f8d81-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="f8d81-111">Las API se crean y se configuran en el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="f8d81-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="f8d81-112">Para obtener acceso al portal del publicador, haga clic en el **portal del publicador** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="f8d81-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="f8d81-113">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f8d81-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="f8d81-115">Haga clic en **API** en el menú **API Management** de la izquierda y haga clic en **Importar API**.</span><span class="sxs-lookup"><span data-stu-id="f8d81-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Importar API][api-management-import-apis]

<span data-ttu-id="f8d81-117">La ventana **Importar API** tiene tres pestañas que corresponden a tres formas de proporcionar la especificación de API.</span><span class="sxs-lookup"><span data-stu-id="f8d81-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="f8d81-118">**Desde el portapapeles** permite pegar la especificación de API en el cuadro de texto designado para ello.</span><span class="sxs-lookup"><span data-stu-id="f8d81-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="f8d81-119">**Desde el archivo** permite buscar el archivo que contiene la especificación de API y seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="f8d81-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="f8d81-120">**Desde URL** permite suministrar la dirección URL de la especificación para la API.</span><span class="sxs-lookup"><span data-stu-id="f8d81-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="f8d81-122">Después de proporcionar la especificación de API, use los botones de radio de la derecha para indicar el formato de especificación.</span><span class="sxs-lookup"><span data-stu-id="f8d81-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="f8d81-123">Se admiten los siguientes formatos.</span><span class="sxs-lookup"><span data-stu-id="f8d81-123">The following formats are supported.</span></span>

* <span data-ttu-id="f8d81-124">WADL</span><span class="sxs-lookup"><span data-stu-id="f8d81-124">WADL</span></span>
* <span data-ttu-id="f8d81-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="f8d81-125">Swagger</span></span>

<span data-ttu-id="f8d81-126">A continuación, especifique un **Sufijo de dirección URL API web**.</span><span class="sxs-lookup"><span data-stu-id="f8d81-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="f8d81-127">Este se anexa a la dirección URL base del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f8d81-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="f8d81-128">La dirección URL base es común para todas las API hospedadas en cada instancia de un servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f8d81-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="f8d81-129">Administración de API distingue las API por su sufijo, por lo que el sufijo debe ser único para cada API de una instancia específica de un servicio de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f8d81-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="f8d81-130">Una vez especificados todos los valores, haga clic en **Guardar** para crear la API y las operaciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="f8d81-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="f8d81-131">Para ver un tutorial de la importación de una API de calculadora básica en formato Swagger, consulte [Administración de su primera API en Administración de API de Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f8d81-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="f8d81-132"><a name="export-api"> </a> Exportación de una API</span><span class="sxs-lookup"><span data-stu-id="f8d81-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="f8d81-133">Además de importar nuevas API, puede exportar las definiciones de sus API desde el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="f8d81-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="f8d81-134">Para ello, haga clic en **Exportar API** en la **pestaña Resumen** de la **API**.</span><span class="sxs-lookup"><span data-stu-id="f8d81-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="f8d81-136">Las API se pueden exportar con WADL o Swagger.</span><span class="sxs-lookup"><span data-stu-id="f8d81-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="f8d81-137">Seleccione el formato que desee, haga clic en **Guardar**y elija la ubicación en la que desea guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="f8d81-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="f8d81-139"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8d81-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f8d81-140">Una vez creada una API e importadas las operaciones, se pueden revisar y definir las configuraciones adicionales, agregar la API a un producto y publicarlo para ponerlo a disposición de los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="f8d81-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="f8d81-141">Para obtener más información, consulte las siguientes guías.</span><span class="sxs-lookup"><span data-stu-id="f8d81-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="f8d81-142">[Definición de la configuración de la API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="f8d81-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="f8d81-143">[Creación y publicación de un producto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="f8d81-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
