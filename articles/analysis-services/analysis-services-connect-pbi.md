---
title: "Conexión a Azure Analysis Services con Power BI | Microsoft Docs"
description: Aprenda a conectarse a un servidor de Azure Analysis Services mediante Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="22113-103">Conexión con Power BI</span><span class="sxs-lookup"><span data-stu-id="22113-103">Connect with Power BI</span></span>

<span data-ttu-id="22113-104">Una vez que se ha creado un servidor en Azure y se ha implementado un modelo tabular, los usuarios de su organización pueden conectarse y comenzar a explorar los datos.</span><span class="sxs-lookup"><span data-stu-id="22113-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="22113-105">Asegúrese de usar la versión más reciente de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="22113-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="22113-106">Conexión en Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="22113-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="22113-107">En Power BI Desktop, haga clic en **Obtener datos** > **Azure** > **Base de datos de Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="22113-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="22113-108">En **Servidor**, escriba el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="22113-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="22113-109">No olvide incluir la dirección URL completa.</span><span class="sxs-lookup"><span data-stu-id="22113-109">Be sure to include the full URL.</span></span> <span data-ttu-id="22113-110">Por ejemplo, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="22113-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="22113-111">En **Base de datos**, si conoce el nombre de la base de datos de modelo tabular o la perspectiva a la que desea conectarse, péguelo aquí.</span><span class="sxs-lookup"><span data-stu-id="22113-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="22113-112">En caso contrario, puede dejar este campo en blanco y seleccionar una base de datos o una perspectiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="22113-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="22113-113">Deje la opción predeterminada **Conectar en directo** y presione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="22113-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="22113-114">Escriba sus credenciales de inicio de sesión, si se le solicitan.</span><span class="sxs-lookup"><span data-stu-id="22113-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="22113-115">En **Navegador**, expanda el servidor, seleccione el modelo o la perspectiva a la que desea conectarse y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="22113-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="22113-116">Haga clic en un modelo o una perspectiva para mostrar todos los objetos de esa vista.</span><span class="sxs-lookup"><span data-stu-id="22113-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="22113-117">El modelo se abre en Power BI Desktop con un informe en blanco en la vista de informe.</span><span class="sxs-lookup"><span data-stu-id="22113-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="22113-118">La lista de campos muestra todos los objetos del modelo no ocultos.</span><span class="sxs-lookup"><span data-stu-id="22113-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="22113-119">El estado de la conexión se muestra en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="22113-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="22113-120">Conexión en Power BI (servicio)</span><span class="sxs-lookup"><span data-stu-id="22113-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="22113-121">Cree un archivo de Power BI Desktop que tenga una conexión en directo con el modelo del servidor.</span><span class="sxs-lookup"><span data-stu-id="22113-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="22113-122">En [Power BI](https://powerbi.microsoft.com), haga clic en **Obtener datos** > **archivos**.</span><span class="sxs-lookup"><span data-stu-id="22113-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="22113-123">Localice y seleccione el archivo.</span><span class="sxs-lookup"><span data-stu-id="22113-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="22113-124">Consulte también</span><span class="sxs-lookup"><span data-stu-id="22113-124">See also</span></span>
<span data-ttu-id="22113-125">[Conexión a Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="22113-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="22113-126">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="22113-126">Client libraries</span></span>](analysis-services-data-providers.md)

