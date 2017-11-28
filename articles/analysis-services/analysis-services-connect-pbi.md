---
title: aaaConnect tooAzure Analysis Services con Power BI | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooan Azure Analysis Services server mediante el uso de Power BI."
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="0a827-103">Conexión con Power BI</span><span class="sxs-lookup"><span data-stu-id="0a827-103">Connect with Power BI</span></span>

<span data-ttu-id="0a827-104">Una vez que haya creado un servidor de Azure e implementa un modelo tabular tooit, los usuarios de su organización son tooconnect listo y empezar a explorar los datos.</span><span class="sxs-lookup"><span data-stu-id="0a827-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="0a827-105">Estar seguro de versión más reciente de Hola de toouse de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="0a827-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="0a827-106">Conexión en Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0a827-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="0a827-107">En Power BI Desktop, haga clic en **Obtener datos** > **Azure** > **Base de datos de Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="0a827-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="0a827-108">En **servidor**, escriba el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a827-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="0a827-109">Ser seguro tooinclude Hola dirección URL completa.</span><span class="sxs-lookup"><span data-stu-id="0a827-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="0a827-110">Por ejemplo, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="0a827-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="0a827-111">En **base de datos**, si conoce el nombre de Hola de base de datos de modelo tabular de Hola o una perspectiva que desee tooconnect a, péguelo aquí.</span><span class="sxs-lookup"><span data-stu-id="0a827-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="0a827-112">En caso contrario, puede dejar este campo en blanco y seleccionar una base de datos o una perspectiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="0a827-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="0a827-113">Deje Hola predeterminado **conectar en directo** opción, a continuación, presione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="0a827-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="0a827-114">Escriba sus credenciales de inicio de sesión, si se le solicitan.</span><span class="sxs-lookup"><span data-stu-id="0a827-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="0a827-115">En **navegador**, expanda servidor hello y luego seleccione el modelo de Hola o una perspectiva que desee tooconnect para, a continuación, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="0a827-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="0a827-116">Haga clic en un modelo o perspectiva tooshow todos los objetos de Hola para esa vista.</span><span class="sxs-lookup"><span data-stu-id="0a827-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="0a827-117">modelo de Hola se abre en Power BI Desktop con un informe en blanco en la vista de informe.</span><span class="sxs-lookup"><span data-stu-id="0a827-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="0a827-118">lista de campos de Hello muestra todos los objetos de modelo no ocultos.</span><span class="sxs-lookup"><span data-stu-id="0a827-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="0a827-119">Estado de la conexión se muestra en la esquina inferior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a827-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="0a827-120">Conexión en Power BI (servicio)</span><span class="sxs-lookup"><span data-stu-id="0a827-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="0a827-121">Crear un archivo de Power BI Desktop que tiene un modelo de tooyour de conexión dinámica en el servidor.</span><span class="sxs-lookup"><span data-stu-id="0a827-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="0a827-122">En [Power BI](https://powerbi.microsoft.com), haga clic en **Obtener datos** > **archivos**.</span><span class="sxs-lookup"><span data-stu-id="0a827-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="0a827-123">Localice y seleccione el archivo.</span><span class="sxs-lookup"><span data-stu-id="0a827-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="0a827-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0a827-124">See also</span></span>
<span data-ttu-id="0a827-125">[Conectar tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="0a827-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="0a827-126">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="0a827-126">Client libraries</span></span>](analysis-services-data-providers.md)

