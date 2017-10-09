
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="e9b45-101">Crear una regla de firewall de nivel de servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e9b45-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="e9b45-102">En la hoja Hola SQL server, en configuración, haga clic en **Firewall** hoja de tooopen Hola Firewall para SQL server de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9b45-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="e9b45-103">Revise la dirección IP del cliente hello muestra y validar que se trata de la dirección IP en Internet mediante un explorador de su elección de Hola (Preguntar "¿Cuál es mi dirección IP).</span><span class="sxs-lookup"><span data-stu-id="e9b45-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="e9b45-104">En ocasiones no coinciden por distintas razones.</span><span class="sxs-lookup"><span data-stu-id="e9b45-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="e9b45-105">Suponiendo que coincide con direcciones IP de hello, haga clic en **agregar dirección IP del cliente** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9b45-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![agregar IP de cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="e9b45-107">Puede abrir firewall de base de datos SQL de hello en hello server tooa única dirección IP o todo un intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="e9b45-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="e9b45-108">Apertura Hola firewall habilita los administradores de SQL y la base de datos de los usuarios toologin tooany en Hola toowhich server tienen credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="e9b45-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="e9b45-109">Haga clic en **guardar** en Hola toosave de barra de herramientas de esta regla de firewall de nivel de servidor y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e9b45-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![agregar IP de cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="e9b45-111">Para ver un tutorial, consulte [Tutorial de SQL Database: crear un servidor, una regla de firewall de nivel de servidor, una base de datos de ejemplo, una regla de firewall de nivel de base de datos y conectar con SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e9b45-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
