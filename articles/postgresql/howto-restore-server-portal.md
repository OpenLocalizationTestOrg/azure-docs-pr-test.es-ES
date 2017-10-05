---
title: "Restauración de un servidor de Azure Database for PostgreSQL | Microsoft Docs"
description: "En este artículo se describe cómo restaurar un servidor en Azure Database for PostgreSQL mediante Azure Portal."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="79d63-103">Copia de seguridad y restauración de un servidor en Azure Database for PostgreSQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="79d63-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="79d63-104">Las copias de seguridad se realizan automáticamente</span><span class="sxs-lookup"><span data-stu-id="79d63-104">Backup happens Automatically</span></span>
<span data-ttu-id="79d63-105">Cuando se usa Azure Database for PostgreSQL, el servicio de base de datos realiza automáticamente una copia de seguridad del servicio de cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="79d63-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="79d63-106">Las copias de seguridad están disponibles durante 7 días en el nivel Básico y 35 días en el nivel Estándar.</span><span class="sxs-lookup"><span data-stu-id="79d63-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="79d63-107">Para más información, consulte [Niveles de servicio de Azure Database for PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="79d63-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="79d63-108">Con esta característica de copia de seguridad automática, puede restaurar el servidor y todas sus bases de datos en un servidor nuevo a un momento dado anterior.</span><span class="sxs-lookup"><span data-stu-id="79d63-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="79d63-109">Restauración en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="79d63-109">Restore in the Azure portal</span></span>
<span data-ttu-id="79d63-110">Azure Database for PostgreSQL permite restaurar el servidor a un momento dado y en una nueva copia del servidor.</span><span class="sxs-lookup"><span data-stu-id="79d63-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="79d63-111">Puede usar este nuevo servidor para recuperar los datos.</span><span class="sxs-lookup"><span data-stu-id="79d63-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="79d63-112">Por ejemplo, si una tabla se quitó accidentalmente a mediodía de hoy, podría restaurar al momento justo antes de mediodía y recuperar la tabla y los datos que faltan desde esa copia nueva del servidor.</span><span class="sxs-lookup"><span data-stu-id="79d63-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="79d63-113">Los siguientes pasos restauran el servidor de ejemplo a un momento dado:</span><span class="sxs-lookup"><span data-stu-id="79d63-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="79d63-114">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="79d63-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="79d63-115">Localice su servidor de Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="79d63-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="79d63-116">En Azure Portal, haga clic en **Todos los recursos**, en el menú izquierdo, y escriba el nombre **mypgserver-20170401** para buscar el servidor existente.</span><span class="sxs-lookup"><span data-stu-id="79d63-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="79d63-117">Haga clic en el nombre del servidor que aparece en el resultado de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="79d63-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="79d63-118">Se abrirá la página **Información general** del servidor, que proporciona opciones para continuar la configuración.</span><span class="sxs-lookup"><span data-stu-id="79d63-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure Portal: busque el servidor](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="79d63-120">En la parte superior de la hoja de información general del servidor, haga clic en **Restaurar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="79d63-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="79d63-121">Se abre la hoja Restaurar.</span><span class="sxs-lookup"><span data-stu-id="79d63-121">The Restore blade opens.</span></span>

   ![Azure Database for PostgreSQL - Información general - Botón Restaurar](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="79d63-123">Rellene el formulario Restaurar con la información necesaria:</span><span class="sxs-lookup"><span data-stu-id="79d63-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="79d63-124">Azure Database for PostgreSQL - Información sobre restauración</span><span class="sxs-lookup"><span data-stu-id="79d63-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="79d63-125">**Punto de restauración**: seleccione el momento antes de que se modificara la base de datos.</span><span class="sxs-lookup"><span data-stu-id="79d63-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="79d63-126">**Servidor de destino**: especifique el nombre del nuevo servidor donde desea restaurar</span><span class="sxs-lookup"><span data-stu-id="79d63-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="79d63-127">**Ubicación**: no se puede seleccionar la región; de forma predeterminada, es la misma que la del servidor de origen</span><span class="sxs-lookup"><span data-stu-id="79d63-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="79d63-128">**Plan de tarifa**: no se puede cambiar este valor al restaurar un servidor.</span><span class="sxs-lookup"><span data-stu-id="79d63-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="79d63-129">Es el mismo que el del servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="79d63-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="79d63-130">Haga clic en **Aceptar** para restaurar el servidor a un momento dado.</span><span class="sxs-lookup"><span data-stu-id="79d63-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="79d63-131">Una vez finalizada la restauración, busque el nuevo servidor que se crea para comprobar que los datos se restauraron del modo esperado.</span><span class="sxs-lookup"><span data-stu-id="79d63-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79d63-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79d63-132">Next steps</span></span>
- [<span data-ttu-id="79d63-133">Bibliotecas de conexiones de Azure Database para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="79d63-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
