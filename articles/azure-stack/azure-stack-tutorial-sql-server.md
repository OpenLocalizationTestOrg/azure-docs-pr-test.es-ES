---
title: aaaMake SQL bases de datos de los usuarios de Azure pila disponible tooyour | Documentos de Microsoft
description: Tutorial tooinstall Hola proveedor de recursos SQL Server y crear ofertas a las que permiten a los usuarios de la pila de Azure crear bases de datos SQL.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a><span data-ttu-id="088a4-103">Asegúrese de bases de datos SQL los usuarios de Azure pila tooyour disponibles</span><span class="sxs-lookup"><span data-stu-id="088a4-103">Make SQL databases available tooyour Azure Stack users</span></span>

<span data-ttu-id="088a4-104">Como administrador de la nube de Azure Stack, puede crear ofertas que permitan a los usuarios (inquilinos) crear bases de datos SQL que se puedan usar con sus aplicaciones en la nube, sitios web y cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="088a4-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="088a4-105">Al proporcionar estos personalizada, a petición, los usuarios de bases de datos en la nube tooyour, puede guardarlos tiempo y recursos.</span><span class="sxs-lookup"><span data-stu-id="088a4-105">By providing these custom, on-demand, cloud-based databases tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="088a4-106">tooset este servicio, tendrá que:</span><span class="sxs-lookup"><span data-stu-id="088a4-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="088a4-107">Implementar el proveedor de recursos de SQL Server de Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-107">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="088a4-108">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="088a4-108">Create an offer</span></span>
> * <span data-ttu-id="088a4-109">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-109">Test hello offer</span></span>

## <a name="deploy-hello-sql-server-resource-provider"></a><span data-ttu-id="088a4-110">Implementar el proveedor de recursos de SQL Server de Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-110">Deploy hello SQL Server resource provider</span></span>

<span data-ttu-id="088a4-111">proceso de implementación de Hola se describe detalladamente en hello [bases de datos de uso de SQL en el artículo de la pila de Azure](azure-stack-sql-resource-provider-deploy.md)y se compone de hello siguiendo los pasos principales:</span><span class="sxs-lookup"><span data-stu-id="088a4-111">hello deployment process is described in detail in hello [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and is comprised of hello following primary steps:</span></span>

1.  <span data-ttu-id="088a4-112">[Implementar el proveedor de recursos SQL de hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span><span class="sxs-lookup"><span data-stu-id="088a4-112">[Deploy hello SQL resource provider]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span></span>
2.  <span data-ttu-id="088a4-113">[Comprobar la implementación de hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span><span class="sxs-lookup"><span data-stu-id="088a4-113">[Verify hello deployment]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3.  <span data-ttu-id="088a4-114">[Proporcionar una capacidad mediante la conexión tooa que hospeda SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span><span class="sxs-lookup"><span data-stu-id="088a4-114">[Provide capacity by connecting tooa hosting SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="088a4-115">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="088a4-115">Create an offer</span></span>

1.  <span data-ttu-id="088a4-116">[Establezca una cuota](azure-stack-setting-quotas.md) y asígnele el nombre *CuotaDeSQLServer*.</span><span class="sxs-lookup"><span data-stu-id="088a4-116">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="088a4-117">Seleccione **Microsoft.SQLAdapter** para hello **Namespace** campo.</span><span class="sxs-lookup"><span data-stu-id="088a4-117">Select **Microsoft.SQLAdapter** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="088a4-118">[Cree un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="088a4-118">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="088a4-119">Asígnele el nombre *TestSQLServerPlan*, seleccione hello **Microsoft.SQLAdapter** servicio, y **SQLServerQuota** cuota.</span><span class="sxs-lookup"><span data-stu-id="088a4-119">Name it *TestSQLServerPlan*, select hello **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="088a4-120">los usuarios de toolet crear otras aplicaciones, otros servicios pueden ser necesaria en el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="088a4-120">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="088a4-121">Por ejemplo, las funciones de Azure requiere ese plan Hola incluyen hello **almacenamiento de Microsoft** de servicio, mientras que requiere de Wordpress **Microsoft.MySQLAdapter**.</span><span class="sxs-lookup"><span data-stu-id="088a4-121">For example, Azure Functions requires that hello plan include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>
    > 
    >

3.  <span data-ttu-id="088a4-122">[Crear una oferta](azure-stack-create-offer.md), asígnele el nombre **TestSQLServerOffer** y seleccione hello **TestSQLServerPlan** plan.</span><span class="sxs-lookup"><span data-stu-id="088a4-122">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select hello **TestSQLServerPlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="088a4-123">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-123">Test hello offer</span></span>

<span data-ttu-id="088a4-124">Ahora que ha implementado el proveedor de recursos de SQL Server de Hola y crear una oferta, puede iniciar sesión como un usuario, suscribirse toohello oferta y crear una base de datos.</span><span class="sxs-lookup"><span data-stu-id="088a4-124">Now that you've deployed hello SQL Server resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create a database.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="088a4-125">Suscribirse toohello oferta</span><span class="sxs-lookup"><span data-stu-id="088a4-125">Subscribe toohello offer</span></span>
1. <span data-ttu-id="088a4-126">Inicie sesión en toohello portal de Azure pila (https://portal.local.azurestack.external) como un inquilino.</span><span class="sxs-lookup"><span data-stu-id="088a4-126">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="088a4-127">Haga clic en **Obtener una suscripción** y, a continuación, escriba **SuscripciónDePruebaDeSQLServer** en **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="088a4-127">Click **Get a subscription** and then type **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="088a4-128">Haga clic en **Seleccionar una oferta** > **OfertaDePruebaDeSQLServer** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="088a4-128">Click **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="088a4-129">Haga clic en **Más servicios** > **Suscripciones** > **SuscripciónDePruebaDeSQLServer** > **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="088a4-129">Click **More services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="088a4-130">Haga clic en **registrar** toohello siguiente **Microsoft.SQLAdapter** proveedor.</span><span class="sxs-lookup"><span data-stu-id="088a4-130">Click **Register** next toohello **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="088a4-131">Creación de una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="088a4-131">Create a SQL database</span></span>

1. <span data-ttu-id="088a4-132">Haga clic en **+** > **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="088a4-132">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="088a4-133">Los valores predeterminados de deje Hola para campos de hello, o pueden usar estos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="088a4-133">Leave hello defaults for hello fields, or you can use these examples:</span></span>
    - <span data-ttu-id="088a4-134">**Nombre de la base de datos**: SQLdb</span><span class="sxs-lookup"><span data-stu-id="088a4-134">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="088a4-135">**Tamaño máximo en MB**: 100</span><span class="sxs-lookup"><span data-stu-id="088a4-135">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="088a4-136">**Suscripción**: OfertaDePruebaSQL</span><span class="sxs-lookup"><span data-stu-id="088a4-136">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="088a4-137">**Grupo de recursos**: SQL-RG</span><span class="sxs-lookup"><span data-stu-id="088a4-137">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="088a4-138">Haga clic en **configuración de inicio de sesión**, escriba las credenciales de base de datos de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="088a4-138">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span>
4. <span data-ttu-id="088a4-139">Haga clic en **SKU** > seleccione Hola SQL SKU que ha creado para Hola de hospedaje de SQL Server > **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="088a4-139">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="088a4-140">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="088a4-140">Click **Create**.</span></span>

<span data-ttu-id="088a4-141">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="088a4-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="088a4-142">Implementar el proveedor de recursos de SQL Server de Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-142">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="088a4-143">Creación de una oferta</span><span class="sxs-lookup"><span data-stu-id="088a4-143">Create an offer</span></span>
> * <span data-ttu-id="088a4-144">Oferta de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="088a4-144">Test hello offer</span></span>

<span data-ttu-id="088a4-145">Avanzar toohello siguiente tutorial toolearn cómo para:</span><span class="sxs-lookup"><span data-stu-id="088a4-145">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="088a4-146">Asegúrese de web, móviles y los usuarios de tooyour disponibles de aplicaciones de API</span><span class="sxs-lookup"><span data-stu-id="088a4-146">Make web, mobile, and API apps available tooyour users</span></span>]( azure-stack-tutorial-app-service.md)

