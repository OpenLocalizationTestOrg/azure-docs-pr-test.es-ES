---
title: "Azure Portal: enmascaramiento dinámico de datos de SQL Database | Microsoft Docs"
description: "Introducción al uso del enmascaramiento dinámico de datos de SQL Database en Azure Portal"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="553c3-103">Empiece a usar el enmascaramiento dinámico de datos de SQL Database con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="553c3-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="553c3-104">En este tema se muestra cómo implementar el [enmascaramiento dinámico de datos](sql-database-dynamic-data-masking-get-started.md) con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="553c3-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="553c3-105">También puede implementar el enmascaramiento dinámico de datos mediante [cmdlets de Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) o la [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="553c3-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="553c3-106">Configurar el enmascaramiento de datos dinámicos para la base de datos mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="553c3-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="553c3-107">Inicie el Portal de Azure en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="553c3-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="553c3-108">Desplácese hasta la hoja de configuración de la base de datos que incluye los datos confidenciales que desea enmascarar.</span><span class="sxs-lookup"><span data-stu-id="553c3-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="553c3-109">Haga clic en el icono **Enmascaramiento de datos dinámicos**, con lo que se iniciará la hoja de configuración **Enmascaramiento de datos dinámicos**.</span><span class="sxs-lookup"><span data-stu-id="553c3-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="553c3-110">Como alternativa, puede desplazarse hacia abajo hasta la sección **Operaciones** y hacer clic en **Enmascaramiento de datos dinámicos**.</span><span class="sxs-lookup"><span data-stu-id="553c3-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="553c3-112">En la hoja de **Enmascaramiento de datos dinámicos** puede ver algunas columnas de base de datos que el motor de recomendaciones ha marcado para enmascaramiento.</span><span class="sxs-lookup"><span data-stu-id="553c3-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="553c3-113">Para aceptar las recomendaciones, solo tiene que hacer clic en **Agregar máscara** para una o varias columnas y se creará una máscara en función del tipo predeterminado para esta columna.</span><span class="sxs-lookup"><span data-stu-id="553c3-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="553c3-114">Para cambiar la función de enmascaramiento, haga clic en la regla de enmascaramiento y edite formato de campo de enmascaramiento en el formato diferente que elija.</span><span class="sxs-lookup"><span data-stu-id="553c3-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="553c3-115">Asegúrese de hacer clic en **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="553c3-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="553c3-117">Para agregar una máscara para cualquier columna de la base de datos, en la parte superior de la hoja de configuración **Enmascaramiento de datos dinámicos**, haga clic en **Agregar máscara** para abrir la hoja de configuración **Agregar regla de enmascaramiento**.</span><span class="sxs-lookup"><span data-stu-id="553c3-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="553c3-119">Seleccione el **esquema**, la **tabla** y la **columna** para definir el campo designado para enmascararse.</span><span class="sxs-lookup"><span data-stu-id="553c3-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="553c3-120">Elija un **Formato de campo de enmascaramiento** en la lista de categorías de enmascaramiento de datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="553c3-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="553c3-122">Haga clic en **Guardar** en la hoja de regla de enmascaramiento de datos para actualizar el conjunto de reglas de enmascaramiento en la directiva de enmascaramiento dinámico.</span><span class="sxs-lookup"><span data-stu-id="553c3-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="553c3-123">Escriba los usuarios SQL o las identidades AAD que deben excluirse del enmascaramiento y tengan acceso a los datos confidenciales sin máscara.</span><span class="sxs-lookup"><span data-stu-id="553c3-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="553c3-124">Esto debe ser una lista separada por puntos y coma de usuarios.</span><span class="sxs-lookup"><span data-stu-id="553c3-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="553c3-125">Tenga en cuenta que los usuarios con privilegios de administrador siempre tienen acceso a los datos originales sin máscara.</span><span class="sxs-lookup"><span data-stu-id="553c3-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="553c3-127">Para hacer que el nivel de aplicación pueda mostrar datos confidenciales para los usuarios con privilegios de la aplicación, agregue el usuario SQL o identidad AAD que la aplicación usa para consultar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="553c3-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="553c3-128">Se recomienda que esta lista incluya un número mínimo de usuarios con privilegio para minimizar la exposición de los datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="553c3-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="553c3-129">Haga clic en **Guardar** en la hoja de configuración de enmascaramiento de datos para guardar la directiva de enmascaramiento nueva o actualizada.</span><span class="sxs-lookup"><span data-stu-id="553c3-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="553c3-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="553c3-130">Next steps</span></span>

* <span data-ttu-id="553c3-131">Para obtener información general sobre el enmascaramiento dinámico de datos, consulte [este artículo](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="553c3-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="553c3-132">También puede implementar el enmascaramiento dinámico de datos mediante [cmdlets de Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) o la [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="553c3-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>