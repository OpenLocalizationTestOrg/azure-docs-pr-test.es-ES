---
title: "Conexión a Azure Analysis Services con Excel | Microsoft Docs"
description: Aprenda a conectarse a un servidor de Azure Analysis Services mediante Excel.
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
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="ccf61-103">Conexión con Excel</span><span class="sxs-lookup"><span data-stu-id="ccf61-103">Connect with Excel</span></span>

<span data-ttu-id="ccf61-104">Una vez que se ha creado un servidor en Azure y se ha implementado en él un modelo tabular, está preparado para conectarse y comenzar a explorar los datos.</span><span class="sxs-lookup"><span data-stu-id="ccf61-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="ccf61-105">Conexión en Excel</span><span class="sxs-lookup"><span data-stu-id="ccf61-105">Connect in Excel</span></span>

<span data-ttu-id="ccf61-106">La conexión a un servidor en Excel se admite mediante Obtener datos en Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="ccf61-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="ccf61-107">No se admite la conexión mediante el Asistente para importar tablas en Power Pivot.</span><span class="sxs-lookup"><span data-stu-id="ccf61-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="ccf61-108">**Conexión en Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="ccf61-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="ccf61-109">En Excel 2016, en la cinta de opciones **Datos**, haga clic en **Obtener datos externos** > **De otros orígenes** > **Desde Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="ccf61-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="ccf61-110">En el Asistente para conexión de datos, en **Nombre del servidor**, escriba el nombre del servidor incluidos el protocolo y el URI.</span><span class="sxs-lookup"><span data-stu-id="ccf61-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="ccf61-111">Luego, en **Credenciales de inicio de sesión**, seleccione **Utilizar el nombre de usuario y la contraseña siguientes** y escriba el nombre de usuario de la organización (por ejemplo, nancy@adventureworks.com) y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="ccf61-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Conexión desde el inicio de sesión de Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="ccf61-113">En **Seleccionar base de datos y tabla**, seleccione la base de datos y el modelo o la perspectiva y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="ccf61-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Conexión desde el modelo de selección de Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="ccf61-115">Consulte también</span><span class="sxs-lookup"><span data-stu-id="ccf61-115">See also</span></span>
<span data-ttu-id="ccf61-116">[Bibliotecas de cliente](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="ccf61-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="ccf61-117">Administración del servidor</span><span class="sxs-lookup"><span data-stu-id="ccf61-117">Manage your server</span></span>](analysis-services-manage.md)     


