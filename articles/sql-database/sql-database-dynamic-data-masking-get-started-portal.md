---
title: "Azure Portal: enmascaramiento dinámico de datos de SQL Database | Microsoft Docs"
description: "¿Cómo tooget partió enmascaramiento Hola Portal de Azure dinámico de datos de base de datos SQL"
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
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="dc8a8-103">Empezar a trabajar con datos dinámicos de base de datos SQL de enmascaramiento con hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dc8a8-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="dc8a8-104">Este tema muestra cómo tooimplement [enmascaramiento dinámico de datos](sql-database-dynamic-data-masking-get-started.md) con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="dc8a8-105">También puede implementar el enmascaramiento de datos dinámicos mediante [cmdlets de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc8a8-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="dc8a8-106">Configurar el enmascaramiento dinámico de datos para la base de datos mediante Hola Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dc8a8-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="dc8a8-107">Inicio Hola Portal de Azure en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc8a8-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc8a8-108">Navegue toohello hoja de configuración de base de datos de Hola que incluya datos confidenciales de hello desea toomask.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="dc8a8-109">Haga clic en hello **Dynamic Data Masking** mosaico que inicia hello **Dynamic Data Masking** hoja de configuración.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="dc8a8-110">Como alternativa, puede desplazarse hacia abajo toohello **Operations** sección y haga clic en **Dynamic Data Masking**.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="dc8a8-112">Hola **Dynamic Data Masking** hoja de configuración es posible que vea algunas columnas de la base de datos que haya marcado ese motor de recomendaciones de Hola de enmascaramiento.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="dc8a8-113">En orden tooaccept recomendaciones de hello, simplemente haga clic en **agregar máscara** para una o varias columnas y una máscara se creará en función de tipo de valor predeterminado de Hola para esta columna.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="dc8a8-114">Puede cambiar Hola función de enmascaramiento haciendo clic en la regla de enmascaramiento de Hola y Hola campo formato tooa otro formato que prefiera el enmascaramiento de edición.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="dc8a8-115">Ser seguro tooclick **guardar** toosave la configuración.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="dc8a8-117">tooadd una máscara de cualquier columna de la base de datos, en parte superior de Hola de hello **Dynamic Data Masking** hoja de configuración, haga clic en **agregar máscara** tooopen hello **Agregar regla de enmascaramiento** hoja de configuración</span><span class="sxs-lookup"><span data-stu-id="dc8a8-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="dc8a8-119">Seleccione hello **esquema**, **tabla** y **columna** hello toodefine designado de campo que se enmascarará.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="dc8a8-120">Elija un **formato del campo enmascaramiento** de lista de Hola de categorías de enmascaramiento de datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="dc8a8-122">Haga clic en **guardar** en conjunto de reglas hoja tooupdate Hola de reglas de directiva de enmascaramiento de datos dinámicos de Hola de enmascaramiento de enmascaramiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="dc8a8-123">Los usuarios SQL de tipo hello o las identidades AAD que deben excluirse del enmascaramiento y tienen datos confidenciales de toohello sin máscara de acceso.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="dc8a8-124">Esto debe ser una lista separada por puntos y coma de usuarios.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="dc8a8-125">Tenga en cuenta que los usuarios con privilegios de administrador siempre tienen datos sin enmascarar de acceso toohello original.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="dc8a8-127">toomake así Hola a nivel de aplicación puede mostrar datos confidenciales para los usuarios de la aplicación con privilegios, Hola usuario SQL o aplicación hello de identidad AAD utiliza base de datos de tooquery Hola.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="dc8a8-128">Se recomienda encarecidamente que esta lista contienen un número mínimo de exposición de toominimize de los usuarios con privilegios de los datos confidenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="dc8a8-129">Haga clic en **guardar** en directiva de enmascaramiento nuevas o actualizadas de configuración hoja toosave Hola de enmascaramiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc8a8-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc8a8-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc8a8-130">Next steps</span></span>

* <span data-ttu-id="dc8a8-131">Para obtener información general sobre el enmascaramiento dinámico de datos, consulte [este artículo](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc8a8-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="dc8a8-132">También puede implementar el enmascaramiento de datos dinámicos mediante [cmdlets de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc8a8-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
