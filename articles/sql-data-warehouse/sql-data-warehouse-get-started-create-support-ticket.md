---
title: "Creación de una incidencia de soporte técnico para SQL Data Warehouse | Microsoft Docs"
description: "Creación de una incidencia de soporte técnico en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="e865d-103">Creación de una incidencia de soporte técnico para Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e865d-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="e865d-104">Si tiene algún problema con su instancia de SQL Data Warehouse, cree una incidencia de soporte técnico para que nuestro equipo de ingenieros pueda ayudarle.</span><span class="sxs-lookup"><span data-stu-id="e865d-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="e865d-105">A partir del 20/12/2016, la comprobación de estado de los recursos en Azure Portal no es exacta.</span><span class="sxs-lookup"><span data-stu-id="e865d-105">As of 12/20/2016, the resource health check in the Azure portal is not accurate.</span></span> <span data-ttu-id="e865d-106">Estamos trabajando activamente para solucionar este problema.</span><span class="sxs-lookup"><span data-stu-id="e865d-106">We are actively working to fix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="e865d-107">Creación de una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="e865d-107">Create a support ticket</span></span>
1. <span data-ttu-id="e865d-108">Abra [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e865d-108">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e865d-109">En la pantalla de inicio, haga clic en el icono **Ayuda y soporte técnico** .</span><span class="sxs-lookup"><span data-stu-id="e865d-109">On the Home screen, click the **Help + support** tile.</span></span>
   
    ![Ayuda y soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="e865d-111">En la hoja Ayuda y soporte técnico, haga clic en **Crear una solicitud de soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="e865d-111">On the Help + Support blade, click **Create support request**.</span></span>
   
    ![Nueva solicitud de soporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="e865d-113">Seleccione el **Tipo de solicitud**.</span><span class="sxs-lookup"><span data-stu-id="e865d-113">Select the **Request Type**.</span></span>
   
    ![Tipo de solicitud](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="e865d-115">De forma predeterminada, cada servidor SQL (por ejemplo, myserver.database.windows.net) tiene una **Cuota de DTU** de 45.000.</span><span class="sxs-lookup"><span data-stu-id="e865d-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="e865d-116">Esta cuota es simplemente un límite de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e865d-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="e865d-117">Puede aumentar la cuota creando una incidencia de soporte técnico y seleccionando *Cuota* como el tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="e865d-117">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="e865d-118">Para calcular las necesidades de DTU, multiplique 7,5 por el total de [DWU][DWU] necesario.</span><span class="sxs-lookup"><span data-stu-id="e865d-118">To calculate your DTU needs, multiply the 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="e865d-119">Por ejemplo, desea hospedar dos DW6000s en un servidor SQL, así que debe solicitar una cuota de DTU de 90 000.</span><span class="sxs-lookup"><span data-stu-id="e865d-119">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="e865d-120">Puede ver el consumo de DTU actual en la hoja del servidor SQL en el portal.</span><span class="sxs-lookup"><span data-stu-id="e865d-120">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="e865d-121">El recuento de las bases de datos, tanto en pausa como continuo, hacia la cuota de DTU.</span><span class="sxs-lookup"><span data-stu-id="e865d-121">Both paused and un-paused databases count toward the DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="e865d-122">Seleccione la **suscripción** que hospeda la base de datos con el problema que va a notificar.</span><span class="sxs-lookup"><span data-stu-id="e865d-122">Select the **Subscription** that hosts the database with the problem you are reporting.</span></span>
   
    ![suscripción](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="e865d-124">Seleccione **Almacenamiento de datos SQL** como Recurso.</span><span class="sxs-lookup"><span data-stu-id="e865d-124">Select **SQL Data Warehouse** as the Resource.</span></span>
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="e865d-126">Seleccione su [Plan de soporte técnico de Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="e865d-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="e865d-127">**facturación, las cuotas y la administración de suscripciones** .</span><span class="sxs-lookup"><span data-stu-id="e865d-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="e865d-128">El soporte técnico para problemas de tipo **Break-fix** se proporciona a través de los niveles [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="e865d-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="e865d-129">Los problemas "break-fix" son aquellos que experimentan los clientes mientras usan Azure en los que hay una posibilidad razonable de que hayan sido causados por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e865d-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="e865d-130">El **aprendizaje para desarrolladores** y los **servicios de asesoramiento** están disponibles en los niveles de soporte técnico [Professional Direct][Professional Direct] y [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="e865d-130">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="e865d-131">Si tiene un plan de soporte técnico Premier, también puede informar sobre problemas relacionados con SQL Data Warehouse en el [portal Microsoft Premier Online][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="e865d-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="e865d-132">Consulte [Soporte técnico de Azure][Azure support plan] para clientes para más información sobre los diversos planes de soporte técnico, incluyendo detalles como ámbito, tiempos de respuesta, precios, etc.  Si desea ver las preguntas más frecuentes sobre el soporte técnico de Azure, consulte [Preguntas más frecuentes de soporte técnico de Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="e865d-132">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plan de soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="e865d-134">Seleccionar el **tipo de problema** y la **categoría**.</span><span class="sxs-lookup"><span data-stu-id="e865d-134">Select the **Problem Type** and **Category**.</span></span> <span data-ttu-id="e865d-135">En este ejemplo, se ha elegido "Herramientas" como el tipo de problema y "Herramientas de cliente" como la categoría.</span><span class="sxs-lookup"><span data-stu-id="e865d-135">In this example, we have chosen "Tools" as the Problem type and "Client tools" as the category.</span></span> 
   
    ![Categoría del tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="e865d-137">Describa el problema y elija el nivel de impacto empresarial.</span><span class="sxs-lookup"><span data-stu-id="e865d-137">Describe the problem and choose the level of business impact.</span></span>
   
    ![Descripción del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="e865d-139">Su **información de contacto** para esta incidencia de soporte técnico se rellenará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e865d-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="e865d-140">Actualice si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e865d-140">Update this if necessary.</span></span>
    
    ![Información de contacto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="e865d-142">Haga clic en **Crear** para enviar la solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="e865d-142">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="e865d-143">Supervisión de una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="e865d-143">Monitor a support ticket</span></span>
<span data-ttu-id="e865d-144">Una vez que ha enviado la solicitud de asistencia, el equipo de soporte técnico de Azure se pondrá en contacto con usted.</span><span class="sxs-lookup"><span data-stu-id="e865d-144">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="e865d-145">Para comprobar el estado de la solicitud y los detalles, haga clic en **Administrar solicitudes de soporte técnico** en el panel.</span><span class="sxs-lookup"><span data-stu-id="e865d-145">To check your request status and details, click **Manage support requests** on the dashboard.</span></span>

![Comprobar estado](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="e865d-147">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="e865d-147">Other Resources</span></span>
<span data-ttu-id="e865d-148">Además, puede conectar con la comunidad de SQL Data Warehouse en [Stack Overflow][Stack Overflow] o en el [foro de MSDN de Azure SQL Data Warehouse][Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="e865d-148">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

