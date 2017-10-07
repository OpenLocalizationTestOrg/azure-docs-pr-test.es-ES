---
title: aaaConnect tooAzure Analysis Services con Excel | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooan Azure Analysis Services server mediante el uso de Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="3d48f-103">Conexión con Excel</span><span class="sxs-lookup"><span data-stu-id="3d48f-103">Connect with Excel</span></span>

<span data-ttu-id="3d48f-104">Una vez que haya creado un servidor de Azure e implementa un modelo tabular tooit, está listo tooconnect y empezar a explorar los datos.</span><span class="sxs-lookup"><span data-stu-id="3d48f-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="3d48f-105">Conexión en Excel</span><span class="sxs-lookup"><span data-stu-id="3d48f-105">Connect in Excel</span></span>

<span data-ttu-id="3d48f-106">Conectar el servidor de tooa en Excel se admite mediante obtener datos en Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="3d48f-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="3d48f-107">No se puede conectar usando Hola Asistente para importación de tabla de PowerPivot.</span><span class="sxs-lookup"><span data-stu-id="3d48f-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="3d48f-108">**tooconnect en Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="3d48f-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="3d48f-109">En Excel 2016, en hello **datos** la cinta de opciones, haga clic en **obtener datos externos** > **desde otros orígenes** > **de Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="3d48f-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="3d48f-110">En Hola Asistente para la conexión de datos, en **nombre del servidor**, escriba nombre del servidor hello incluidos el protocolo y URI.</span><span class="sxs-lookup"><span data-stu-id="3d48f-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="3d48f-111">A continuación, en **las credenciales de inicio de sesión**, seleccione **Hola de uso después de nombre de usuario y contraseña**y, a continuación, escriba nombre de usuario de la organización de hello, por ejemplo nancy@adventureworks.comy la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3d48f-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Conexión desde el inicio de sesión de Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="3d48f-113">En **Seleccionar base de datos y tabla**, seleccione la base de datos de Hola y modelo o perspectiva y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="3d48f-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Conexión desde el modelo de selección de Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="3d48f-115">Consulte también</span><span class="sxs-lookup"><span data-stu-id="3d48f-115">See also</span></span>
<span data-ttu-id="3d48f-116">[Bibliotecas de cliente](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="3d48f-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="3d48f-117">Administración del servidor</span><span class="sxs-lookup"><span data-stu-id="3d48f-117">Manage your server</span></span>](analysis-services-manage.md)     


