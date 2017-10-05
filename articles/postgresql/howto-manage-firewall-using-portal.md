---
title: "Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante Azure Portal | Microsoft Docs"
description: "Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante Azure Portal"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="740bb-103">Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="740bb-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="740bb-104">Las reglas de firewall de nivel de servidor permiten a los administradores tener acceso a un servidor de Azure Database for PostgreSQL desde una dirección IP o desde un intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="740bb-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="740bb-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="740bb-105">Prerequisites</span></span>
<span data-ttu-id="740bb-106">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="740bb-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="740bb-107">Un servidor [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="740bb-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="740bb-108">Creación de una regla de firewall de nivel de servidor en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="740bb-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="740bb-109">En la hoja del servidor de PostgreSQL, en el encabezado Configuración, haga clic en **Seguridad de conexión** para abrir la hoja de seguridad de conexión para Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="740bb-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="740bb-111">Haga clic en **Agregar mi dirección IP** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="740bb-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="740bb-112">Esto creará automáticamente una regla con la dirección IP del equipo, según lo percibido por el sistema de Azure.</span><span class="sxs-lookup"><span data-stu-id="740bb-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="740bb-114">Compruebe la dirección IP antes de guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="740bb-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="740bb-115">En algunos casos, la dirección IP observada por Azure Portal difiere de la dirección IP utilizada para acceder a Internet y a los servidores de Azure.</span><span class="sxs-lookup"><span data-stu-id="740bb-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="740bb-116">Por tanto, puede necesitar cambiar las direcciones IP inicial y final para que la regla funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="740bb-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="740bb-117">Utilice un motor de búsqueda y otra herramienta en línea para comprobar su propia dirección IP (por ejemplo, busque en Bing "cuál es mi ip").</span><span class="sxs-lookup"><span data-stu-id="740bb-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Búsqueda en Bing "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="740bb-119">Agregue intervalos de direcciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="740bb-119">Add additional address ranges.</span></span> <span data-ttu-id="740bb-120">En las reglas de firewall de Azure Database for PostgreSQL, puede especificar una dirección IP o un intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="740bb-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="740bb-121">Si desea limitar la regla a una única dirección IP, escriba la misma dirección en los campos de dirección IP inicial y dirección IP final.</span><span class="sxs-lookup"><span data-stu-id="740bb-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="740bb-122">Abrir el firewall permite a los administradores y usuarios iniciar sesión en cualquier base de datos del servidor de PostgreSQL para el que tengan unas credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="740bb-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="740bb-123">Azure Portal: reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="740bb-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="740bb-124">Haga clic en **Guardar**, en la barra de herramientas, para guardar esta regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="740bb-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="740bb-125">Espere la confirmación de que la actualización de las reglas de firewall se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="740bb-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="740bb-127">Administración de reglas de firewall de nivel de servidor existentes a través del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="740bb-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="740bb-128">Repita los pasos para administrar las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="740bb-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="740bb-129">Para agregar el equipo actual, haga clic en el botón + **Agregar mi dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="740bb-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="740bb-130">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="740bb-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="740bb-131">Para agregar direcciones IP adicionales, escriba el nombre de la regla, la dirección IP inicial y la dirección IP final.</span><span class="sxs-lookup"><span data-stu-id="740bb-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="740bb-132">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="740bb-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="740bb-133">Para modificar una regla existente, haga clic en cualquiera de los campos de la regla y realice la modificación.</span><span class="sxs-lookup"><span data-stu-id="740bb-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="740bb-134">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="740bb-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="740bb-135">Para eliminar una regla existente, haga clic en el botón de puntos suspensivos […] y haga clic en Eliminar para quitar la regla.</span><span class="sxs-lookup"><span data-stu-id="740bb-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="740bb-136">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="740bb-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="740bb-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="740bb-137">Next steps</span></span>
- <span data-ttu-id="740bb-138">De modo similar, puede utilizar scripts para la [Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure](howto-manage-firewall-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="740bb-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="740bb-139">Para obtener ayuda para la conexión a un servidor de Azure Database for PostgreSQL, consulte [Bibliotecas de conexión para Azure Database for PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="740bb-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
