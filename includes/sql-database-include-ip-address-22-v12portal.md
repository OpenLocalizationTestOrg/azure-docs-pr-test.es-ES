
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) en http://portal.azure.com/.
2. En el encabezado de la izquierda hello, haga clic en **examinar todo**. Hola **examinar** hoja se muestra.
3. Desplácese y haga clic en **Servidores SQL Server**. Hola **servidores SQL Server** hoja se muestra.
   
    ![Busque el servidor de base de datos de SQL Azure en el portal de Hola][b21-FindServerInPortal]
4. Para mayor comodidad, haga clic en hello minimizar control en hello anteriormente **examinar** hoja.
5. En el cuadro de texto del filtro de hello comience a escribir el nombre hello del servidor. Aparecerá su fila.
6. Haga clic en la fila de hello para el servidor. Aparecerá una hoja para el servidor.
7. En la hoja del servidor, haga clic en **Configuración**. Hola **configuración** hoja se muestra.
8. Haga clic en **Firewall**. Hola **configuración de Firewall** hoja se muestra.
   
    ![Haga clic en > Firewall.][b31-SettingsFirewallNavig]
9. Haga clic en **Agregar IP de cliente**. Escriba un nombre para la nueva regla en el primer cuadro de texto hello.
10. Tipo Hola bajo y alto valores de rango de Hola que desea la dirección IP tooenable.
    
    * Se puede terminar de valor bajo de Hola práctica toohave con **.0** alta con hello y **.255**.
    
    ![Agregar un tooallow de intervalo de direcciones IP][b41-AddRange]
11. Haga clic en **Guardar**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
