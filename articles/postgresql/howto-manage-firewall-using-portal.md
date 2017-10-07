---
title: aaaCreate y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure | Documentos de Microsoft
description: Crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="42d37-103">Crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="42d37-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="42d37-104">Las reglas de firewall de nivel de servidor habilitar administradores tooaccess una base de datos de Azure para PostgreSQL Server desde una dirección IP o intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="42d37-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="42d37-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42d37-105">Prerequisites</span></span>
<span data-ttu-id="42d37-106">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="42d37-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="42d37-107">Un servidor [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="42d37-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="42d37-108">Crear una regla de firewall de nivel de servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="42d37-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="42d37-109">En hoja de servidor PostgreSQL hello, en configuración del encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de Hola para hello base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="42d37-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="42d37-111">Haga clic en **Agregar mis IP** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="42d37-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="42d37-112">Esto creará una regla automáticamente con la dirección IP de hello del equipo, como percibido por hello sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="42d37-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="42d37-114">Comprobar la dirección IP antes de guardar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="42d37-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="42d37-115">En algunas situaciones, dirección IP de hello observada mediante el portal de Azure difiere de dirección IP de hello utilizada cuando obtiene acceso a Hola internet y servidores de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d37-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="42d37-116">Por lo tanto, puede que tenga toochange Hola IP inicial y final IP toomake Hola regla funcione según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="42d37-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="42d37-117">Utilice un motor de búsqueda y otra toocheck herramienta en línea su propia dirección IP (por ejemplo, la búsqueda de Bing "¿Cuál es mi IP").</span><span class="sxs-lookup"><span data-stu-id="42d37-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Búsqueda en Bing "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="42d37-119">Agregue intervalos de direcciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="42d37-119">Add additional address ranges.</span></span> <span data-ttu-id="42d37-120">En reglas de Hola para hello base de datos de Azure para PostgreSQL firewall, puede especificar una única dirección IP o un intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="42d37-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="42d37-121">Si desea que toolimit Hola regla tooone dirección IP única, Hola tipo misma dirección en el campo de Hola para IP inicial y final IP.</span><span class="sxs-lookup"><span data-stu-id="42d37-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="42d37-122">Abrir firewall de Hola permite a los administradores y usuarios toologin tooany base de datos Hola PostgreSQL server toowhich tienen credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="42d37-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="42d37-123">Azure Portal: reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="42d37-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="42d37-124">Haga clic en **guardar** en Hola toosave de barra de herramientas, esta regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="42d37-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="42d37-125">Espere la confirmación de Hola que Hola reglas de firewall de actualización toohello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="42d37-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="42d37-127">Administrar reglas de firewall de nivel de servidor existente a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="42d37-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="42d37-128">Repita las reglas de firewall de hello pasos toomanage Hola.</span><span class="sxs-lookup"><span data-stu-id="42d37-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="42d37-129">equipo de tooadd Hola actual, haga clic en el botón de hello demasiado + **Agregar mis IP**.</span><span class="sxs-lookup"><span data-stu-id="42d37-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="42d37-130">Haga clic en **guardar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="42d37-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42d37-131">las direcciones IP adicionales tooadd, escriba Hola nombre de la regla, la dirección IP inicial y la dirección IP final.</span><span class="sxs-lookup"><span data-stu-id="42d37-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="42d37-132">Haga clic en **guardar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="42d37-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42d37-133">toomodify una regla existente, haga clic en cualquiera de los campos de Hola de regla de Hola y modificar.</span><span class="sxs-lookup"><span data-stu-id="42d37-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="42d37-134">Haga clic en **guardar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="42d37-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="42d37-135">toodelete una regla existente, haga clic en los puntos suspensivos de hello […] y haga clic en eliminar quitar regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="42d37-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="42d37-136">Haga clic en **guardar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="42d37-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42d37-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42d37-137">Next steps</span></span>
- <span data-ttu-id="42d37-138">De forma similar, puede crear scripts demasiado[crear y administrar la base de datos PostgreSQL las reglas de firewall mediante la CLI de Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="42d37-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="42d37-139">Para obtener ayuda sobre conexión tooan base de datos de Azure para PostgreSQL server, vea [bibliotecas de conexiones de base de datos de PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="42d37-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
