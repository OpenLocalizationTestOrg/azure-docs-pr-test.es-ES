
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="b24ad-101">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) en http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="b24ad-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="b24ad-102">En el encabezado de la izquierda hello, haga clic en **examinar todo**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="b24ad-103">Hola **examinar** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="b24ad-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="b24ad-104">Desplácese y haga clic en **Servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="b24ad-105">Hola **servidores SQL Server** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="b24ad-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Busque el servidor de base de datos de SQL Azure en el portal de Hola][b21-FindServerInPortal]
4. <span data-ttu-id="b24ad-107">Para mayor comodidad, haga clic en hello minimizar control en hello anteriormente **examinar** hoja.</span><span class="sxs-lookup"><span data-stu-id="b24ad-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="b24ad-108">En el cuadro de texto del filtro de hello comience a escribir el nombre hello del servidor.</span><span class="sxs-lookup"><span data-stu-id="b24ad-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="b24ad-109">Aparecerá su fila.</span><span class="sxs-lookup"><span data-stu-id="b24ad-109">Your row is displayed.</span></span>
6. <span data-ttu-id="b24ad-110">Haga clic en la fila de hello para el servidor.</span><span class="sxs-lookup"><span data-stu-id="b24ad-110">Click hello row for your server.</span></span> <span data-ttu-id="b24ad-111">Aparecerá una hoja para el servidor.</span><span class="sxs-lookup"><span data-stu-id="b24ad-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="b24ad-112">En la hoja del servidor, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="b24ad-113">Hola **configuración** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="b24ad-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="b24ad-114">Haga clic en **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-114">Click **Firewall**.</span></span> <span data-ttu-id="b24ad-115">Hola **configuración de Firewall** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="b24ad-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Haga clic en > Firewall.][b31-SettingsFirewallNavig]
9. <span data-ttu-id="b24ad-117">Haga clic en **Agregar IP de cliente**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-117">Click **Add Client IP**.</span></span> <span data-ttu-id="b24ad-118">Escriba un nombre para la nueva regla en el primer cuadro de texto hello.</span><span class="sxs-lookup"><span data-stu-id="b24ad-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="b24ad-119">Tipo Hola bajo y alto valores de rango de Hola que desea la dirección IP tooenable.</span><span class="sxs-lookup"><span data-stu-id="b24ad-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="b24ad-120">Se puede terminar de valor bajo de Hola práctica toohave con **.0** alta con hello y **.255**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Agregar un tooallow de intervalo de direcciones IP][b41-AddRange]
11. <span data-ttu-id="b24ad-122">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b24ad-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
