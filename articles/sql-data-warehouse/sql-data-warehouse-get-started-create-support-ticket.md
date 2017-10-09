---
title: "aaaHow toocreate una incidencia de soporte técnico para el almacenamiento de datos SQL | Documentos de Microsoft"
description: "¿Cómo toocreate una compatibilidad con vales en el almacén de datos de SQL Azure."
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
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="957dc-103">¿Cómo toocreate compatibilidad vale para almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="957dc-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="957dc-104">Si tiene algún problema con su instancia de SQL Data Warehouse, cree una incidencia de soporte técnico para que nuestro equipo de ingenieros pueda ayudarle.</span><span class="sxs-lookup"><span data-stu-id="957dc-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="957dc-105">A partir de 20/12/2016, comprobación de mantenimiento de recursos de Hola Hola portal de Azure no es exacta.</span><span class="sxs-lookup"><span data-stu-id="957dc-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="957dc-106">Estamos trabajando activamente toofix este problema.</span><span class="sxs-lookup"><span data-stu-id="957dc-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="957dc-107">Creación de una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="957dc-107">Create a support ticket</span></span>
1. <span data-ttu-id="957dc-108">Abra hello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="957dc-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="957dc-109">En la pantalla de inicio de bienvenida, haga clic en hello **ayuda y soporte técnico** icono.</span><span class="sxs-lookup"><span data-stu-id="957dc-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Ayuda y soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="957dc-111">En Hola ayuda + hoja de soporte técnico, haga clic en **crear solicitud de soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="957dc-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nueva solicitud de soporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="957dc-113">Seleccione hello **tipo de solicitud**.</span><span class="sxs-lookup"><span data-stu-id="957dc-113">Select hello **Request Type**.</span></span>
   
    ![Tipo de solicitud](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="957dc-115">De forma predeterminada, cada servidor SQL (por ejemplo, myserver.database.windows.net) tiene una **Cuota de DTU** de 45.000.</span><span class="sxs-lookup"><span data-stu-id="957dc-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="957dc-116">Esta cuota es simplemente un límite de seguridad.</span><span class="sxs-lookup"><span data-stu-id="957dc-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="957dc-117">Puede aumentar la cuota mediante la creación de una incidencia de soporte técnico y seleccionar *cuota* como tipo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="957dc-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="957dc-118">toocalculate necesita, multiplique la DTU Hola 7.5 por hello total [DWU] [ DWU] necesarios.</span><span class="sxs-lookup"><span data-stu-id="957dc-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="957dc-119">Por ejemplo, al igual que toohost dos DW6000s en un servidor SQL server, a continuación, debe solicitar una cuota DTU de 90.000.</span><span class="sxs-lookup"><span data-stu-id="957dc-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="957dc-120">Puede ver el consumo de DTU actual de la hoja de hello SQL server en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="957dc-121">Bases de datos en pausa y continuó cuentan para la cuota de DTU Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="957dc-122">Seleccione hello **suscripción** que hosts Hola base de datos con el que se informe de problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![La suscripción](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="957dc-124">Seleccione **almacenamiento de datos SQL** como Hola recursos.</span><span class="sxs-lookup"><span data-stu-id="957dc-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="957dc-126">Seleccione su [Plan de soporte técnico de Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="957dc-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="957dc-127">**facturación, las cuotas y la administración de suscripciones** .</span><span class="sxs-lookup"><span data-stu-id="957dc-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="957dc-128">El soporte técnico para problemas de tipo **Break-fix** se proporciona a través de los niveles [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="957dc-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="957dc-129">Problemas de break-fix en línea son problemas de los clientes que se ha producido durante el uso de Azure donde hay una expectativa razonable ese problema de Hola de Microsoft que se produjo.</span><span class="sxs-lookup"><span data-stu-id="957dc-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="957dc-130">**Desarrollador de asesoría** y **servicios de consultoría** están disponibles en hello [Professional Direct] [ Professional Direct] y [principal] [ Premier] niveles de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="957dc-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="957dc-131">Si tienes un Premier admitir plan, también puede notificar el almacenamiento de datos de SQL relacionada con problemas en hello [portal en línea de Microsoft Premier][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="957dc-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="957dc-132">Vea [planes de soporte técnico de Azure] [ Azure support plan] toolearn más información acerca de saludo diversos admiten planes, incluidos el ámbito, tiempos de respuesta, precios, etcetera.  Si desea ver las preguntas más frecuentes sobre el soporte técnico de Azure, consulte [Preguntas más frecuentes de soporte técnico de Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="957dc-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plan de soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="957dc-134">Seleccione hello **tipo de problema** y **categoría**.</span><span class="sxs-lookup"><span data-stu-id="957dc-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="957dc-135">En este ejemplo, que hemos elegido "Herramientas" como tipo de problema de Hola y "Herramientas de cliente" como categoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Categoría del tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="957dc-137">Describa el problema de Hola y elegir Hola nivel de impacto empresarial.</span><span class="sxs-lookup"><span data-stu-id="957dc-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Descripción del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="957dc-139">Su **información de contacto** para esta incidencia de soporte técnico se rellenará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="957dc-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="957dc-140">Actualice si es necesario.</span><span class="sxs-lookup"><span data-stu-id="957dc-140">Update this if necessary.</span></span>
    
    ![Información de contacto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="957dc-142">Haga clic en **crear** solicitud de soporte técnico de toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="957dc-143">Supervisión de una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="957dc-143">Monitor a support ticket</span></span>
<span data-ttu-id="957dc-144">Una vez ha enviado la solicitud de soporte técnico de Hola, equipo de soporte técnico de Azure de Hola se comunicará con usted.</span><span class="sxs-lookup"><span data-stu-id="957dc-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="957dc-145">toocheck el estado de la solicitud y los detalles, haga clic en **administrar solicitudes de soporte técnico** en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="957dc-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Comprobar estado](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="957dc-147">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="957dc-147">Other Resources</span></span>
<span data-ttu-id="957dc-148">Además, puede conectarse con hello Comunidad de almacenamiento de datos SQL en [desbordamiento de la pila] [ Stack Overflow] o en hello [foro de MSDN de almacenamiento de datos de SQL Azure] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="957dc-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

