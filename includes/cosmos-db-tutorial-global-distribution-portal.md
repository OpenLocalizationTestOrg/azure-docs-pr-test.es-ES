
Obtendrá más información sobre la distribución global de Azure Cosmos DB en este vídeo de Azure Friday con Scott Hanselman y el administrador de ingeniería principal Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Para obtener más información sobre cómo funciona la replicación global de bases de datos en Cosmos DB, vea [Distribución de datos global con Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Agregar regiones de base de datos global mediante Hola Portal de Azure
Azure Cosmos DB está disponible en todas las [regiones de Azure][azureregions] de todo el mundo. Después de seleccionar el nivel de coherencia de hello predeterminado para la cuenta de base de datos, puede asociar una o más regiones (en función de su elección de las necesidades de distribución global y el nivel de coherencia de forma predeterminada).

1. Hola [portal de Azure](https://portal.azure.com/), en Hola barra de la izquierda, haga clic en **base de datos de Azure Cosmos**.
2. Hola **base de datos de Azure Cosmos** hoja, toomodify de cuenta de base de datos de hello select.
3. En la hoja de la cuenta de hello, haga clic en **datos se replica globalmente** en el menú de Hola.
4. Hola **datos se replica globalmente** hoja, seleccione Hola regiones tooadd o quitar haciendo clic en las regiones en el mapa de hello y, a continuación, haga clic en **guardar**. Hay un regiones tooadding de costo, vea hello [página de precios](https://azure.microsoft.com/pricing/details/documentdb/) o hello [distribuir datos globalmente con documentos](../articles/documentdb/documentdb-distribute-data-globally.md) artículo para obtener más información.
   
    ![Haga clic en áreas de hello en hello mapa tooadd o quitarlos][1]
    
Una vez que agregue otra región, Hola **conmutación por error Manual** opción está habilitada en hello **datos se replica globalmente** hoja en el portal de Hola. Puede utilizar este proceso de conmutación por error de opción tootest Hola o cambiar la región principal de escritura de Hola. Una vez que agregue una región de terceros, Hola **las prioridades de conmutación por error** opción está habilitada en Hola misma hoja para que se puede cambiar el orden de conmutación por error de Hola para lecturas.  

### <a name="selecting-global-database-regions"></a>Selección de regiones de la base de datos global
Hay dos escenarios comunes para configurar dos o más regiones:

1. Brinda acceso de baja latencia toodata tooend usuarios independientemente de dónde se ubicarán mundo Hola
2. Agregar resistencia regional para la continuidad empresarial y la recuperación ante desastres (BCDR).

Para los usuarios-tooend de baja latencia entrega, se recomienda toodeploy ambos Hola aplicación y agregue Cosmos base de datos Azure en regiones de Hola que se corresponden a los usuarios de aplicación de toowhere Hola se encuentran.

Para BCDR, se recomienda regiones tooadd basándose en pares de región de hello descritos en hello [negocio continuidad y recuperación ante desastres (BCDR): las regiones emparejadas de Azure] [ bcdr] artículo.

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
