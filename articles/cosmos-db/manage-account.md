---
title: "aaaManage una cuenta de base de datos de Azure Cosmos a través de hello Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage cuenta de la base de datos de Azure Cosmos a través de hello Portal de Azure. Buscar a una guía sobre el uso de hello tooview de Portal de Azure, copia, cuentas de acceso y eliminación."
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="86075-105">¿Cómo toomanage una cuenta de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="86075-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="86075-106">Obtenga información acerca de cómo trabajar con claves tooset coherencia global y eliminar una cuenta de base de datos de Azure Cosmos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86075-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="86075-107"><a id="consistency"></a>Administración de la configuración de coherencia de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86075-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="86075-108">Seleccionar nivel de coherencia derecho Hola depende de semántica de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="86075-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="86075-109">Debe familiarizarse con los niveles de coherencia disponibles de hello en base de datos de Azure Cosmos leyendo [utilizando coherencia niveles toomaximize disponibilidad y el rendimiento en la base de datos de Azure Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="86075-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="86075-110">Azure Cosmos DB ofrece garantías de coherencia, disponibilidad y rendimiento, en cada nivel de coherencia disponible para la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="86075-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="86075-111">Configurar la cuenta de base de datos con un nivel de coherencia de seguro requiere que los datos sean tooa reducidos sola región de Azure y no está disponible globalmente.</span><span class="sxs-lookup"><span data-stu-id="86075-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="86075-112">En otra parte de Hola, Hola niveles de coherencia no estricta - uso vinculado, session o eventual enable tooassociate cualquier número de regiones de Azure con su cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="86075-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="86075-113">Hola siguiendo los pasos sencillos mostrarle cómo tooselect Hola a nivel de coherencia predeterminada para la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="86075-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="86075-114">coherencia de toospecify Hola predeterminado para una cuenta de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="86075-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="86075-115">Hola [portal de Azure](https://portal.azure.com/), acceder a su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="86075-116">En la hoja de la cuenta de hello, haga clic en **predeterminado coherencia**.</span><span class="sxs-lookup"><span data-stu-id="86075-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="86075-117">Hola **coherencia predeterminada** hoja, nivel de coherencia de hello seleccione Nuevo y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="86075-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="86075-118">![Sesión de coherencia predeterminada][5]</span><span class="sxs-lookup"><span data-stu-id="86075-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="86075-119"><a id="keys"></a>Visualización, copia y regeneración de las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="86075-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="86075-120">Cuando se crea una cuenta de base de datos de Azure Cosmos, servicio de hello genera dos claves de acceso principal que pueden usarse para la autenticación cuando se tiene acceso a la cuenta de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="86075-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="86075-121">Al proporcionar dos claves de acceso, base de datos de Azure Cosmos permite claves de hello tooregenerate con ninguna cuenta de base de datos de Azure Cosmos tooyour de interrupción.</span><span class="sxs-lookup"><span data-stu-id="86075-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="86075-122">Hola [portal de Azure](https://portal.azure.com/), Hola de acceso **claves** hoja de menú de recursos Hola Hola **cuenta de base de datos de Azure Cosmos** tooview hoja, copiar y regenerar hello las teclas de acceso son tooaccess usa su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Captura de pantalla del Portal de Azure, hoja Claves](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="86075-124">Hola **claves** hoja también incluye principal y las cadenas de conexión secundaria que pueden ser utilizados tooconnect tooyour cuenta de hello [herramienta de migración de datos](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="86075-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="86075-125">Las claves de solo lectura también están disponibles en esta hoja.</span><span class="sxs-lookup"><span data-stu-id="86075-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="86075-126">Las lecturas y consultas son operaciones de solo lectura, mientras que las operaciones de creación, eliminación y reemplazo no lo son.</span><span class="sxs-lookup"><span data-stu-id="86075-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="86075-127">Copiar una tecla de acceso en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="86075-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="86075-128">En hello **claves** hoja, haga clic en hello **copia** toohello botón derecha de la clave de hello desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="86075-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Ver y copiar una tecla de acceso en hello Portal de Azure, hoja de claves](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="86075-130">Regenerar las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="86075-130">Regenerate access keys</span></span>
<span data-ttu-id="86075-131">Debe cambiar la cuenta de base de datos de Azure Cosmos de tooyour de claves de acceso de hello periódicamente toohelp proteger las conexiones.</span><span class="sxs-lookup"><span data-stu-id="86075-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="86075-132">Dos claves de acceso se asignan tooenable se toomaintain conexiones toohello cuenta de base de datos de Azure Cosmos mediante una clave de acceso mientras regenera Hola otra clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="86075-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="86075-133">Volver a generar las claves de acceso afecta a todas las aplicaciones que dependen de la clave actual Hola.</span><span class="sxs-lookup"><span data-stu-id="86075-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="86075-134">Todos los clientes que usan cuenta de base de datos de Azure Cosmos Hola de hello acceso tooaccess clave deben ser clave nueva de hello toouse actualizada.</span><span class="sxs-lookup"><span data-stu-id="86075-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="86075-135">Si tiene aplicaciones o servicios en la nube con la cuenta de base de datos de Azure Cosmos hello, perderá las conexiones de hello si vuelve a generar las claves, a menos que poner las claves.</span><span class="sxs-lookup"><span data-stu-id="86075-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="86075-136">Hello pasos siguientes describen Hola proceso de distribución de las claves.</span><span class="sxs-lookup"><span data-stu-id="86075-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="86075-137">Actualizar la clave de acceso de hello en su clave de acceso secundaria de hello tooreference aplicación de código de hello cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="86075-138">Regenerar clave de acceso principal de Hola para su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="86075-139">Hola [Portal de Azure](https://portal.azure.com/), acceder a su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="86075-140">Hola **cuenta de base de datos de Azure Cosmos** hoja, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="86075-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="86075-141">En hello **claves** hoja, haga clic en botón regenerar hello, a continuación, haga clic en **Aceptar** tooconfirm que desea toogenerate una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="86075-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="86075-142">![Regenerar las claves de acceso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="86075-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="86075-143">Una vez que haya comprobado esa clave nueva Hola está disponible para su uso (aproximadamente 5 minutos después de la regeneración), actualice la clave de acceso de hello en su aplicación código tooreference Hola nueva clave de acceso principal.</span><span class="sxs-lookup"><span data-stu-id="86075-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="86075-144">Regenerar clave de acceso secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="86075-144">Regenerate hello secondary access key.</span></span>
   
    ![Regenerar las claves de acceso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="86075-146">Puede tardar varios minutos antes de que una clave recién generada puede ser tooaccess usa su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="86075-147">Obtener la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="86075-147">Get hello  connection string</span></span>
<span data-ttu-id="86075-148">tooretrieve la conexión de cadena, hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="86075-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="86075-149">Hola [portal de Azure](https://portal.azure.com), acceder a su cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="86075-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="86075-150">En el menú de recursos de hello, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="86075-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="86075-151">Haga clic en hello **copia** botón siguiente toohello **cadena de conexión principal** o **cadena de conexión secundaria** cuadro.</span><span class="sxs-lookup"><span data-stu-id="86075-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="86075-152">Si usas la cadena de conexión de Hola Hola [herramienta de migración de base de datos de base de datos de Azure Cosmos](import-data.md), anexar final de toohello de nombre de base de datos de Hola de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="86075-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="86075-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="86075-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="86075-154"><a id="delete"></a> Eliminar una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86075-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="86075-155">tooremove una base de datos de Azure Cosmos cuenta de hello Portal de Azure que ya no se está usando, nombre de la cuenta de hello en menú contextual y haga clic en **eliminar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="86075-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Cuenta de toodelete una base de datos de Azure Cosmos en Hola Portal de Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="86075-157">Hola [portal de Azure](https://portal.azure.com/), tener acceso a la cuenta de base de datos de Azure Cosmos Hola desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="86075-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="86075-158">En hello **cuenta de base de datos de Azure Cosmos** hoja, haga clic en la cuenta de hello y, a continuación, haga clic en **eliminar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="86075-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="86075-159">En la hoja de confirmación resultante hello, escriba Hola base de datos de Azure Cosmos tooconfirm de nombre de cuenta que desea que la cuenta de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="86075-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="86075-160">Haga clic en hello **eliminar** botón.</span><span class="sxs-lookup"><span data-stu-id="86075-160">Click hello **Delete** button.</span></span>

![Cuenta de toodelete una base de datos de Azure Cosmos en Hola Portal de Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="86075-162"><a id="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86075-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="86075-163">Obtenga información acerca de cómo demasiado[empezar a trabajar con su cuenta de base de datos de Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="86075-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
