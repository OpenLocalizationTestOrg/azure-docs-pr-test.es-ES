
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Crear una regla de firewall de nivel de servidor en hello portal de Azure

1. En la hoja Hola SQL server, en configuración, haga clic en **Firewall** hoja de tooopen Hola Firewall para SQL server de Hola.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Revise la dirección IP del cliente hello muestra y validar que se trata de la dirección IP en Internet mediante un explorador de su elección de Hola (Preguntar "¿Cuál es mi dirección IP). En ocasiones no coinciden por distintas razones.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Suponiendo que coincide con direcciones IP de hello, haga clic en **agregar dirección IP del cliente** en la barra de herramientas de Hola.

    ![agregar IP de cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Puede abrir firewall de base de datos SQL de hello en hello server tooa única dirección IP o todo un intervalo de direcciones. Apertura Hola firewall habilita los administradores de SQL y la base de datos de los usuarios toologin tooany en Hola toowhich server tienen credenciales válidas.
    >

4. Haga clic en **guardar** en Hola toosave de barra de herramientas de esta regla de firewall de nivel de servidor y, a continuación, haga clic en **Aceptar**.

    ![agregar IP de cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Para ver un tutorial, consulte [Tutorial de SQL Database: crear un servidor, una regla de firewall de nivel de servidor, una base de datos de ejemplo, una regla de firewall de nivel de base de datos y conectar con SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
