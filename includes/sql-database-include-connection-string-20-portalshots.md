
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="75325-101">Obtenga la cadena de conexión del portal de Azure</span><span class="sxs-lookup"><span data-stu-id="75325-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="75325-102">Utilice el [Portal de Azure](https://portal.azure.com/) para obtener la cadena de conexión necesaria para que su programa cliente interactúe con Base de datos SQL de Azure:</span><span class="sxs-lookup"><span data-stu-id="75325-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="75325-103">Haga clic en **EXAMINAR** > **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="75325-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="75325-104">Escriba el nombre de la base de datos en el cuadro de texto de filtro situado en la esquina superior izquierda de la hoja **Bases de datos SQL** .</span><span class="sxs-lookup"><span data-stu-id="75325-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="75325-105">Haga clic en la fila correspondiente a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="75325-105">Click the row for your database.</span></span>
4. <span data-ttu-id="75325-106">Cuando aparezca la hoja de su base de datos, para una mayor comodidad visual puede hacer clic en los controles estándar para minimizar para contraer las hojas que utilizó para examinar y filtrar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="75325-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![Aplique un filtro para aislar la base de datos][10-FilterDatabase]
5. <span data-ttu-id="75325-108">En la hoja de la base de datos, haga clic en **Mostrar cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="75325-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="75325-109">Si piensa utilizar la biblioteca de conexiones de ADO.NET, copie la cadena etiquetada con **ADO**.</span><span class="sxs-lookup"><span data-stu-id="75325-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![Copie la cadena de conexión ADO correspondiente a la base de datos][20-CopyAdoConnectionString]
7. <span data-ttu-id="75325-111">En un formato u otro, pegue la información de la cadena de conexión en el código del programa cliente.</span><span class="sxs-lookup"><span data-stu-id="75325-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="75325-112">Para obtener más información, consulte </span><span class="sxs-lookup"><span data-stu-id="75325-112">For more information, see:</span></span><br/><span data-ttu-id="75325-113">[Cadenas de conexión y archivos de configuración](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="75325-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
