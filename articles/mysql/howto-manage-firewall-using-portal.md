---
title: aaaCreate y administrar la base de datos de Azure con las reglas de firewall de MySQL con hello portal de Azure | Documentos de Microsoft
description: Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="1316c-103">Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1316c-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="1316c-104">Las reglas de firewall de nivel de servidor habilitar administradores tooaccess una base de datos de Azure para MySQL Server desde una dirección IP o intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1316c-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="1316c-105">Crear una regla de firewall de nivel de servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1316c-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="1316c-106">En la hoja de servidor MySQL hello, bajo Configuración de encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de hello para la base de datos de Azure para MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="1316c-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="1316c-108">Haga clic en **Agregar mis IP** en toocreate de barra de herramientas de hello una regla con la dirección IP de hello del equipo, según lo percibido por hello sistema Azure.</span><span class="sxs-lookup"><span data-stu-id="1316c-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Azure Portal: haga clic en Agregar mi dirección IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="1316c-110">Comprobar la dirección IP antes de guardar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1316c-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="1316c-111">En algunas situaciones, dirección IP de hello observada mediante el portal de Azure difiere de dirección IP de hello utilizada cuando obtiene acceso a Hola internet y servidores de Azure.</span><span class="sxs-lookup"><span data-stu-id="1316c-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="1316c-112">Por lo tanto, puede que tenga toochange Hola IP inicial y final IP toomake Hola regla funcione según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="1316c-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="1316c-113">Usar un motor de búsqueda y otra toocheck herramienta en línea su propia dirección IP (por ejemplo, buscar "¿Cuál es mi dirección IP").</span><span class="sxs-lookup"><span data-stu-id="1316c-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Resultados en Bing para "cuál es mi ip"](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="1316c-115">Agregue intervalos de direcciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="1316c-115">Add additional address ranges.</span></span> <span data-ttu-id="1316c-116">En reglas de Hola para hello base de datos de Azure para firewall de MySQL, puede especificar una única dirección IP o un intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="1316c-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="1316c-117">Si desea que toolimit Hola regla tooone dirección IP única, Hola tipo misma dirección en el campo de Hola para IP inicial y final IP.</span><span class="sxs-lookup"><span data-stu-id="1316c-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="1316c-118">Abrir firewall de Hola permite tooaccess administradores y usuarios de cualquier base de datos MySQL server toowhich tienen credenciales válidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1316c-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="1316c-119">Azure Portal: reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="1316c-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="1316c-120">Haga clic en **guardar** en Hola toosave de barra de herramientas, esta regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="1316c-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="1316c-121">Espere la confirmación de Hola que Hola reglas de firewall de actualización toohello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="1316c-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Azure Portal: haga clic en Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="1316c-123">Administrar reglas de firewall de nivel de servidor existente a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1316c-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="1316c-124">Repita las reglas de firewall de hello pasos toomanage Hola.</span><span class="sxs-lookup"><span data-stu-id="1316c-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="1316c-125">equipo de tooadd Hola actual, haga clic en **+ Agregar mis IP**.</span><span class="sxs-lookup"><span data-stu-id="1316c-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="1316c-126">Escriba las direcciones IP adicionales tooadd, Hola **nombre de la regla**, **IP inicial**, y **IP final**.</span><span class="sxs-lookup"><span data-stu-id="1316c-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="1316c-127">toomodify una regla existente, haga clic en cualquiera de los campos de Hola de regla de Hola y modificar.</span><span class="sxs-lookup"><span data-stu-id="1316c-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="1316c-128">regla de toodelete existente, haga clic en los puntos suspensivos de hello […] y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="1316c-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="1316c-129">Haga clic en **guardar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1316c-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1316c-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1316c-130">Next steps</span></span>
- <span data-ttu-id="1316c-131">Para obtener ayuda en la conexión tooan base de datos de MySQL server, consulte [bibliotecas de conexiones de base de datos de Azure para MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="1316c-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
