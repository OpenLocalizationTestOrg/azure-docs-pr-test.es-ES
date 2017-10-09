
<span data-ttu-id="6492a-101">Obtendrá más información sobre la distribución global de Azure Cosmos DB en este vídeo de Azure Friday con Scott Hanselman y el administrador de ingeniería principal Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="6492a-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="6492a-102">Para obtener más información sobre cómo funciona la replicación global de bases de datos en Cosmos DB, vea [Distribución de datos global con Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="6492a-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="6492a-103"><a id="addregion"></a>Agregar regiones de base de datos global mediante Hola Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6492a-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="6492a-104">Azure Cosmos DB está disponible en todas las [regiones de Azure][azureregions] de todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="6492a-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="6492a-105">Después de seleccionar el nivel de coherencia de hello predeterminado para la cuenta de base de datos, puede asociar una o más regiones (en función de su elección de las necesidades de distribución global y el nivel de coherencia de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="6492a-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="6492a-106">Hola [portal de Azure](https://portal.azure.com/), en Hola barra de la izquierda, haga clic en **base de datos de Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="6492a-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="6492a-107">Hola **base de datos de Azure Cosmos** hoja, toomodify de cuenta de base de datos de hello select.</span><span class="sxs-lookup"><span data-stu-id="6492a-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="6492a-108">En la hoja de la cuenta de hello, haga clic en **datos se replica globalmente** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="6492a-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="6492a-109">Hola **datos se replica globalmente** hoja, seleccione Hola regiones tooadd o quitar haciendo clic en las regiones en el mapa de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6492a-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="6492a-110">Hay un regiones tooadding de costo, vea hello [página de precios](https://azure.microsoft.com/pricing/details/documentdb/) o hello [distribuir datos globalmente con documentos](../articles/documentdb/documentdb-distribute-data-globally.md) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="6492a-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Haga clic en áreas de hello en hello mapa tooadd o quitarlos][1]
    
<span data-ttu-id="6492a-112">Una vez que agregue otra región, Hola **conmutación por error Manual** opción está habilitada en hello **datos se replica globalmente** hoja en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6492a-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="6492a-113">Puede utilizar este proceso de conmutación por error de opción tootest Hola o cambiar la región principal de escritura de Hola.</span><span class="sxs-lookup"><span data-stu-id="6492a-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="6492a-114">Una vez que agregue una región de terceros, Hola **las prioridades de conmutación por error** opción está habilitada en Hola misma hoja para que se puede cambiar el orden de conmutación por error de Hola para lecturas.</span><span class="sxs-lookup"><span data-stu-id="6492a-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="6492a-115">Selección de regiones de la base de datos global</span><span class="sxs-lookup"><span data-stu-id="6492a-115">Selecting global database regions</span></span>
<span data-ttu-id="6492a-116">Hay dos escenarios comunes para configurar dos o más regiones:</span><span class="sxs-lookup"><span data-stu-id="6492a-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="6492a-117">Brinda acceso de baja latencia toodata tooend usuarios independientemente de dónde se ubicarán mundo Hola</span><span class="sxs-lookup"><span data-stu-id="6492a-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="6492a-118">Agregar resistencia regional para la continuidad empresarial y la recuperación ante desastres (BCDR).</span><span class="sxs-lookup"><span data-stu-id="6492a-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="6492a-119">Para los usuarios-tooend de baja latencia entrega, se recomienda toodeploy ambos Hola aplicación y agregue Cosmos base de datos Azure en regiones de Hola que se corresponden a los usuarios de aplicación de toowhere Hola se encuentran.</span><span class="sxs-lookup"><span data-stu-id="6492a-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="6492a-120">Para BCDR, se recomienda regiones tooadd basándose en pares de región de hello descritos en hello [negocio continuidad y recuperación ante desastres (BCDR): las regiones emparejadas de Azure] [ bcdr] artículo.</span><span class="sxs-lookup"><span data-stu-id="6492a-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
