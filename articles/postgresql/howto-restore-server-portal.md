---
title: "¿Cómo tooRestore un servidor de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Este artículo se describe cómo toorestore un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="580ac-103">¿Cómo tooBackup y restaurar un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="580ac-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="580ac-104">Las copias de seguridad se realizan automáticamente</span><span class="sxs-lookup"><span data-stu-id="580ac-104">Backup happens Automatically</span></span>
<span data-ttu-id="580ac-105">Cuando se usa la base de datos de Azure para PostgreSQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="580ac-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="580ac-106">las copias de seguridad de Hello están disponibles durante 7 días al utilizar el nivel básico y 35 días cuando se utiliza el nivel estándar.</span><span class="sxs-lookup"><span data-stu-id="580ac-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="580ac-107">Para más información, consulte [Niveles de servicio de Azure Database for PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="580ac-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="580ac-108">Con esta característica de copia de seguridad automática, puede restaurar servidor hello y todas sus bases de datos en un nuevo servidor tooan anteriormente en un momento.</span><span class="sxs-lookup"><span data-stu-id="580ac-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="580ac-109">Restaurar en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="580ac-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="580ac-110">Azure base de datos PostgreSQL permite toorestore Hola servidor back-tooa punto en el tiempo y en tooa nueva copia del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="580ac-111">Puede usar esta nueva toorecover server los datos.</span><span class="sxs-lookup"><span data-stu-id="580ac-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="580ac-112">Por ejemplo, si una tabla no estaba accidentalmente quita al mediodía hoy en día, se podría restaurar toohello tiempo justo antes del mediodía y recuperar Hola falta la tabla y los datos de esa nueva copia del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="580ac-113">Hello pasos siguientes punto de restauración Hola ejemplo server tooa en el tiempo:</span><span class="sxs-lookup"><span data-stu-id="580ac-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="580ac-114">Inicio de sesión en hello [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="580ac-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="580ac-115">Localice su servidor de Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="580ac-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="580ac-116">Hola portal de Azure, haga clic en **todos los recursos** del menú izquierdo de Hola y escriba el nombre de hello, como **mypgserver 20170401**, toosearch para el servidor existente.</span><span class="sxs-lookup"><span data-stu-id="580ac-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="580ac-117">Haga clic en nombre del servidor de hello, en el resultado de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="580ac-118">Hola **Introducción** página para el servidor se abre y proporciona opciones para otra configuración.</span><span class="sxs-lookup"><span data-stu-id="580ac-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portal de Azure: el servidor de búsqueda de toolocate](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="580ac-120">En la parte superior de Hola de hoja de información general del servidor de hello, haga clic en **restaurar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="580ac-121">se abre la hoja de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-121">hello Restore blade opens.</span></span>

   ![Azure Database for PostgreSQL - Información general - Botón Restaurar](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="580ac-123">Rellene el formulario de restauración de hello con información de hello necesario:</span><span class="sxs-lookup"><span data-stu-id="580ac-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="580ac-124">Azure Database for PostgreSQL - Información sobre restauración</span><span class="sxs-lookup"><span data-stu-id="580ac-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="580ac-125">**Punto de restauración**: seleccione un punto-in-time que se produce antes de que se cambió el servidor hello</span><span class="sxs-lookup"><span data-stu-id="580ac-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="580ac-126">**Servidor de destino**: especifique un nuevo nombre de servidor que desee toorestore a</span><span class="sxs-lookup"><span data-stu-id="580ac-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="580ac-127">**Ubicación**: no se puede seleccionar una región hello, de forma predeterminada es igual que el servidor de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="580ac-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="580ac-128">**Plan de tarifa**: no se puede cambiar este valor al restaurar un servidor.</span><span class="sxs-lookup"><span data-stu-id="580ac-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="580ac-129">Es igual que el servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="580ac-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="580ac-130">Haga clic en **Aceptar** toorestore Hola server toorestore tooa punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="580ac-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="580ac-131">Una vez finalizada la restauración de hello, localizar el servidor nuevo de hello confeccionadas hello tooverify se restauran datos según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="580ac-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="580ac-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="580ac-132">Next steps</span></span>
- [<span data-ttu-id="580ac-133">Bibliotecas de conexiones de Azure Database para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="580ac-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
