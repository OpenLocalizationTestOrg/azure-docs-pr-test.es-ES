---
title: "Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal | Microsoft Docs"
description: "Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="11839-103">Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11839-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="11839-104">Las reglas de firewall de nivel de servidor permiten a los administradores tener acceso a un servidor de Azure Database for MySQL desde una dirección IP o desde un intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="11839-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="11839-105">Creación de una regla de firewall de nivel a servidor en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11839-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="11839-106">En la hoja del servidor de MySQL, en el encabezado Configuración, haga clic en **Seguridad de conexión** para abrir la hoja de seguridad de conexión para Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="11839-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="11839-108">Haga clic en **Agregar mi dirección IP** en la barra de herramientas para crear una regla con la dirección IP del equipo, según lo percibido por el sistema de Azure.</span><span class="sxs-lookup"><span data-stu-id="11839-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="11839-110">Compruebe la dirección IP antes de guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="11839-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="11839-111">En algunos casos, la dirección IP observada por Azure Portal difiere de la dirección IP utilizada para acceder a Internet y a los servidores de Azure.</span><span class="sxs-lookup"><span data-stu-id="11839-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="11839-112">Por tanto, puede necesitar cambiar las direcciones IP inicial y final para que la regla funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="11839-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="11839-113">Utilice un motor de búsqueda y otra herramienta en línea para comprobar su propia dirección IP (por ejemplo, busque "cuál es mi dirección ip").</span><span class="sxs-lookup"><span data-stu-id="11839-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Resultados en Bing para "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="11839-115">Agregue intervalos de direcciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="11839-115">Add additional address ranges.</span></span> <span data-ttu-id="11839-116">En las reglas de firewall de Azure Database for MySQL, puede especificar una dirección IP o un intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="11839-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="11839-117">Si desea limitar la regla a una única dirección IP, escriba la misma dirección en los campos de dirección IP inicial y dirección IP final.</span><span class="sxs-lookup"><span data-stu-id="11839-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="11839-118">Abrir el firewall permite a los administradores y usuarios tener acceso a cualquier base de datos del servidor de MySQL para el que tengan unas credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="11839-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="11839-119">Azure Portal: reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="11839-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="11839-120">Haga clic en **Guardar**, en la barra de herramientas, para guardar esta regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="11839-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="11839-121">Espere la confirmación de que la actualización de las reglas de firewall se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="11839-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="11839-123">Administración de reglas de firewall de nivel de servidor existentes a través del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="11839-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="11839-124">Repita los pasos para administrar las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="11839-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="11839-125">Para agregar el equipo actual, haga clic en **+ Agregar mi dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="11839-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="11839-126">Para agregar direcciones IP adicionales, escriba el **nombre de la regla**, la **dirección IP inicial** y la **dirección IP final**.</span><span class="sxs-lookup"><span data-stu-id="11839-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="11839-127">Para modificar una regla existente, haga clic en cualquiera de los campos de la regla y realice la modificación.</span><span class="sxs-lookup"><span data-stu-id="11839-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="11839-128">Para eliminar una regla existente, haga clic en los puntos suspensivos […] y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="11839-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="11839-129">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="11839-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11839-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11839-130">Next steps</span></span>
- <span data-ttu-id="11839-131">Para obtener ayuda para la conexión a un servidor de Azure Database for MySQL, consulte [Bibliotecas de conexiones para Azure Database for MySQL](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="11839-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
