---
title: "Administrar una cuenta de Azure Cosmos DB a través de Azure Portal | Microsoft Docs"
description: "Obtenga información sobre la administración de su cuenta de Azure Cosmos DB mediante Azure Portal. Guía sobre cómo usar el Portal de Azure para ver, copiar, eliminar y obtener acceso a cuentas."
keywords: Portal de Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="9c1e3-105">Administración de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c1e3-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="9c1e3-106">Aprenda a establecer la coherencia global, trabajar con claves y eliminar una cuenta de Azure Cosmos DB en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="9c1e3-107"><a id="consistency"></a>Administración de la configuración de coherencia de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c1e3-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="9c1e3-108">La selección del nivel de coherencia adecuado depende de la semántica de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="9c1e3-109">Para familiarizarse con los niveles de coherencia disponibles en Azure Cosmos DB, consulte [Uso de los niveles de coherencia para maximizar la disponibilidad y el rendimiento en Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="9c1e3-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="9c1e3-110">Azure Cosmos DB ofrece garantías de coherencia, disponibilidad y rendimiento, en cada nivel de coherencia disponible para la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="9c1e3-111">La configuración de la cuenta de base de datos con un nivel de coherencia alto requiere que los datos estén confinados en una sola región de Azure y que no estén disponibles globalmente.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="9c1e3-112">Por otro lado, los niveles de coherencia moderados: uso vinculado, sesión o posible, le permiten asociar un número cualquiera de regiones de Azure con su cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="9c1e3-113">Estos sencillos pasos le muestran cómo seleccionar el nivel de coherencia predeterminado para la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="9c1e3-114">Para especificar la coherencia predeterminada de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c1e3-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="9c1e3-115">Vaya a [Azure Portal](https://portal.azure.com/) y acceda a su cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="9c1e3-116">En la hoja Cuenta, haga clic en **Coherencia predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="9c1e3-117">En la hoja **Coherencia predeterminada**, seleccione el nuevo nivel de coherencia y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="9c1e3-118">![Sesión de coherencia predeterminada][5]</span><span class="sxs-lookup"><span data-stu-id="9c1e3-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="9c1e3-119"><a id="keys"></a>Visualización, copia y regeneración de las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="9c1e3-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="9c1e3-120">Cuando se crea una cuenta de Azure Cosmos DB, el servicio genera dos claves de acceso maestras que se pueden usar para la autenticación cuando se tiene acceso a la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="9c1e3-121">Al proporcionar dos claves de acceso, Azure Cosmos DB permite regenerar las claves sin interrupción en la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="9c1e3-122">En [Azure Portal](https://portal.azure.com/), acceda a la sección **Claves** del menú de recursos de la hoja **Cuenta de Azure Cosmos DB** para ver, copiar y regenerar las claves de acceso que se usan para obtener acceso a la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Captura de pantalla del Portal de Azure, hoja Claves](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="9c1e3-124">La hoja **Claves** también incluye cadenas de conexión principal y secundaria que se pueden utilizar para conectarse a su cuenta desde la [Herramienta de migración de datos](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e3-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="9c1e3-125">Las claves de solo lectura también están disponibles en esta hoja.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="9c1e3-126">Las lecturas y consultas son operaciones de solo lectura, mientras que las operaciones de creación, eliminación y reemplazo no lo son.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="9c1e3-127">Copia de una clave de acceso en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9c1e3-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="9c1e3-128">En la hoja **Claves**, haga clic en el botón **Copiar**, a la derecha de la clave que quiere copiar.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Visualización y copia de una clave de acceso en el Portal de Azure, hoja Claves](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="9c1e3-130">Regenerar las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="9c1e3-130">Regenerate access keys</span></span>
<span data-ttu-id="9c1e3-131">Cambie periódicamente las claves de acceso de la cuenta de Azure Cosmos DB para mantener sus conexiones más seguras.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="9c1e3-132">Se asignan dos claves de acceso para que pueda mantener las conexiones con la cuenta de Azure Cosmos DB, de modo que puede usar una clave de acceso mientras regenera la otra.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="9c1e3-133">La regeneración de las claves de acceso afecta a las aplicaciones que dependen de una clave actual.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="9c1e3-134">Todos los clientes que usan la clave de acceso para obtener acceso a la cuenta de Azure Cosmos DB deben estar actualizados para usar la nueva clave.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="9c1e3-135">Si cuenta con aplicaciones o servicios en la nube que usan la cuenta de Azure Cosmos DB y regenera las claves, perderá las conexiones. Para evitarlo, distribuya las claves.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="9c1e3-136">Los siguientes pasos describen el proceso de distribución de las claves.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="9c1e3-137">Actualice la clave de acceso en el código de aplicación para hacer referencia a la clave de acceso secundaria de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="9c1e3-138">Vuelva a generar la clave de acceso primaria para su cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="9c1e3-139">Vaya a [Azure Portal](https://portal.azure.com/) y acceda a su cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="9c1e3-140">En la hoja **Cuenta de Azure Cosmos DB**, haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="9c1e3-141">En la hoja **Claves**, haga clic en el botón para regenerar y en **Aceptar** para confirmar que quiere generar una clave nueva.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="9c1e3-142">![Regenerar las claves de acceso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="9c1e3-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="9c1e3-143">Tras comprobar que la clave nueva está disponible para su uso (aproximadamente 5 minutos después de la regeneración), actualice la clave de acceso en el código de aplicación para hacer referencia a la nueva clave de acceso principal.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="9c1e3-144">Vuelva a generar la clave de acceso secundaria.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-144">Regenerate the secondary access key.</span></span>
   
    ![Regenerar las claves de acceso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="9c1e3-146">Pueden pasar varios minutos antes de poder obtener acceso a la cuenta de Azure Cosmos DB con la clave que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="9c1e3-147">Obtener la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="9c1e3-147">Get the  connection string</span></span>
<span data-ttu-id="9c1e3-148">Realice lo siguiente para recuperar la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="9c1e3-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="9c1e3-149">Vaya a [Azure Portal](https://portal.azure.com) y acceda a su cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="9c1e3-150">En el menú de recursos, haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="9c1e3-151">Haga clic en el botón **Copiar** situado junto a los cuadros **Cadena de conexión principal** o **Cadena de conexión secundaria**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="9c1e3-152">Si está utilizando la cadena de conexión en la [herramienta de migración de base de datos de Azure Cosmos DB](import-data.md), anexe el nombre de la base de datos al final de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="9c1e3-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="9c1e3-154"><a id="delete"></a> Eliminar una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c1e3-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="9c1e3-155">Para quitar una cuenta de Azure Cosmos DB que ya no usa en Azure Portal, haga clic con el botón derecho en el nombre de cuenta y haga clic en **Eliminar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Eliminación de una cuenta de Azure Cosmos DB en Azure Portal](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="9c1e3-157">En [Azure Portal](https://portal.azure.com/), acceda a la cuenta de Azure Cosmos DB que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="9c1e3-158">En la hoja **Cuenta de Azure Cosmos DB**, haga clic con el botón derecho en la cuenta y, después, en **Eliminar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="9c1e3-159">En la hoja de confirmación que aparece, escriba el nombre de la cuenta de Azure Cosmos DB para confirmar que quiere eliminarla.</span><span class="sxs-lookup"><span data-stu-id="9c1e3-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="9c1e3-160">Haga clic en el botón **Eliminar** .</span><span class="sxs-lookup"><span data-stu-id="9c1e3-160">Click the **Delete** button.</span></span>

![Eliminación de una cuenta de Azure Cosmos DB en Azure Portal](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="9c1e3-162"><a id="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c1e3-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="9c1e3-163">Descubra cómo [comenzar a usar una cuenta de Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="9c1e3-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
