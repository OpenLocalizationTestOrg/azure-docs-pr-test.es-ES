---
title: "aaaImport una API a la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimport una API y sus operaciones en la administración de API de Azure."
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="5753f-103">¿Cómo tooimport Hola definición de una API con las operaciones de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="5753f-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="5753f-104">Administración de API, se pueden crear nuevas API y operaciones de hello agregó manualmente o hello API puede importarse junto con operaciones de hello en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="5753f-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="5753f-105">Las API y sus operaciones pueden importarse mediante Hola después de formatos.</span><span class="sxs-lookup"><span data-stu-id="5753f-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="5753f-106">WADL</span><span class="sxs-lookup"><span data-stu-id="5753f-106">WADL</span></span>
* <span data-ttu-id="5753f-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="5753f-107">Swagger</span></span>

<span data-ttu-id="5753f-108">En esta guía se muestra cómo crear una API e importar sus operaciones en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="5753f-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="5753f-109">Para obtener información sobre cómo crear manualmente una API y las operaciones de adición, vea [cómo toocreate API] [ How toocreate APIs] y [cómo tooadd operaciones tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="5753f-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="5753f-110"><a name="import-api"></a>Importación de una API</span><span class="sxs-lookup"><span data-stu-id="5753f-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="5753f-111">Las API se crean y configuran en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="5753f-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="5753f-112">tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="5753f-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="5753f-113">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5753f-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="5753f-115">Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **importar API**.</span><span class="sxs-lookup"><span data-stu-id="5753f-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Importar API][api-management-import-apis]

<span data-ttu-id="5753f-117">Hola **API de importación** ventana tiene tres pestañas correspondientes de la especificación de toohello tres formas tooprovide Hola API.</span><span class="sxs-lookup"><span data-stu-id="5753f-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="5753f-118">**Desde el Portapapeles** permite toopaste especificación de hello API en el cuadro de texto designado Hola.</span><span class="sxs-lookup"><span data-stu-id="5753f-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="5753f-119">**Desde archivo** permite archivo seleccione Hola de toobrowse tooand que contiene la especificación de hello API.</span><span class="sxs-lookup"><span data-stu-id="5753f-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="5753f-120">**Desde URL** permite la especificación de toohello de dirección URL de toosupply Hola para hello API.</span><span class="sxs-lookup"><span data-stu-id="5753f-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="5753f-122">Después de proporcionar la especificación de API de hello, utilice los botones de radio de hello en formato de especificación de hello tooindicate derecho Hola.</span><span class="sxs-lookup"><span data-stu-id="5753f-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="5753f-123">Hola siguientes formatos es compatibles.</span><span class="sxs-lookup"><span data-stu-id="5753f-123">hello following formats are supported.</span></span>

* <span data-ttu-id="5753f-124">WADL</span><span class="sxs-lookup"><span data-stu-id="5753f-124">WADL</span></span>
* <span data-ttu-id="5753f-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="5753f-125">Swagger</span></span>

<span data-ttu-id="5753f-126">A continuación, especifique un **Sufijo de dirección URL API web**.</span><span class="sxs-lookup"><span data-stu-id="5753f-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="5753f-127">Se trata de toohello anexado de dirección URL base para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="5753f-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="5753f-128">dirección URL base de Hello es común para todas las API que se hospedan en cada instancia de un servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="5753f-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="5753f-129">Administración de API distingue API mediante su sufijo y, por tanto, el sufijo de hello debe ser único para todas las API en una instancia de servicio de administración de API específica.</span><span class="sxs-lookup"><span data-stu-id="5753f-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="5753f-130">Una vez que se escriben todos los valores, haga clic en **guardar** hello y API de hello toocreate asociados operaciones.</span><span class="sxs-lookup"><span data-stu-id="5753f-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="5753f-131">Para ver un tutorial de la importación de una API de calculadora básica en formato Swagger, consulte [Administración de su primera API en Administración de API de Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5753f-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="5753f-132"><a name="export-api"></a> Exportación de una API</span><span class="sxs-lookup"><span data-stu-id="5753f-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="5753f-133">En suma tooimporting nuevas API, puede exportar las definiciones de saludo de las API de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="5753f-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="5753f-134">toodo por lo tanto, haga clic en **API exportar** de hello **ficha Resumen** de su **API**.</span><span class="sxs-lookup"><span data-stu-id="5753f-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="5753f-136">Las API se pueden exportar con WADL o Swagger.</span><span class="sxs-lookup"><span data-stu-id="5753f-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="5753f-137">Seleccione el formato deseado de hello, haga clic en **guardar**y elija la ubicación de hello en qué archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5753f-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="5753f-139"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5753f-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="5753f-140">Una vez que se crea una API y operaciones de hello importadas, puede revisar y configurar cualquier configuración adicional, agregue Hola API tooa producto y publicarlo para que esté disponible para los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5753f-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="5753f-141">Para obtener más información, vea Hola siguiendo a las guías.</span><span class="sxs-lookup"><span data-stu-id="5753f-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="5753f-142">[¿Cómo tooconfigure API de configuración][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="5753f-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="5753f-143">[¿Cómo toocreate y publicación de productos][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="5753f-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
