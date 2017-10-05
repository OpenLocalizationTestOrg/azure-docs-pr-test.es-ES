---
title: "Incorporación del conector de Google Drive a Logic Apps | Microsoft Docs"
description: "Información general del conector de Google Drive con parámetros de la API de REST"
services: 
suite: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2bcebc5-02d2-435b-b0da-ef53bc51c4b6
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c066a10b33e172eb5f16eede43ec407794000c90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-google-drive-connector"></a><span data-ttu-id="11f0a-103">Introducción al conector de Google Drive</span><span class="sxs-lookup"><span data-stu-id="11f0a-103">Get started with the Google Drive connector</span></span>
<span data-ttu-id="11f0a-104">Conéctese a Google Drive para crear archivos, obtener filas, etc.</span><span class="sxs-lookup"><span data-stu-id="11f0a-104">Connect to Google Drive to create files, get rows, and more.</span></span> <span data-ttu-id="11f0a-105">Con Google Drive, puede:</span><span class="sxs-lookup"><span data-stu-id="11f0a-105">With Google Drive, you can:</span></span> 

* <span data-ttu-id="11f0a-106">Compilar el flujo de negocio en función de los datos obtenidos de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="11f0a-106">Build your business flow based on the data you get from your search.</span></span> 
* <span data-ttu-id="11f0a-107">Usar acciones para buscar imágenes, noticias, etc.</span><span class="sxs-lookup"><span data-stu-id="11f0a-107">Use actions to search images, search the news, and more.</span></span> <span data-ttu-id="11f0a-108">Estas acciones obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="11f0a-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="11f0a-109">Por ejemplo, puede buscar un vídeo y luego usar Twitter para publicar ese vídeo en una fuente de Twitter.</span><span class="sxs-lookup"><span data-stu-id="11f0a-109">For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.</span></span>

<span data-ttu-id="11f0a-110">Puede empezar creando una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11f0a-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-the-connection-to-google-drive"></a><span data-ttu-id="11f0a-111">Creación de la conexión a Google Drive</span><span class="sxs-lookup"><span data-stu-id="11f0a-111">Create the connection to Google Drive</span></span>
<span data-ttu-id="11f0a-112">Al agregar este conector a las aplicaciones lógicas, debe autorizar a estas para que se conecten a su Google Drive.</span><span class="sxs-lookup"><span data-stu-id="11f0a-112">When you add this connector to your logic apps, you must authorize logic apps to connect to your Google Drive.</span></span>

> [!INCLUDE [Steps to create a connection to googledrive](../../includes/connectors-create-api-googledrive.md)]
> 
> 

<span data-ttu-id="11f0a-113">Después de crear la conexión, especifique las propiedades de Google Drive, como la ruta de acceso a la carpeta o el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="11f0a-113">After you create the connection, you enter the Google Drive properties, like the folder path or file name.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="11f0a-114">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="11f0a-114">Connector-specific details</span></span>

<span data-ttu-id="11f0a-115">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/googledrive/).</span><span class="sxs-lookup"><span data-stu-id="11f0a-115">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/googledrive/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="11f0a-116">Más conectores</span><span class="sxs-lookup"><span data-stu-id="11f0a-116">More connectors</span></span>
<span data-ttu-id="11f0a-117">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="11f0a-117">Go back to the [APIs list](apis-list.md).</span></span>
