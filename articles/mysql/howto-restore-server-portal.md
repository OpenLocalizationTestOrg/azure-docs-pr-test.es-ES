---
title: "Restauración de un servidor en Azure Database for MySQL | Microsoft Docs"
description: "En este artículo se describe cómo restaurar un servidor en Azure Database for MySQL mediante Azure Portal."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="5673a-103">Copia de seguridad y restauración de un servidor en Azure Database for MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5673a-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="5673a-104">Las copias de seguridad se realizan automáticamente</span><span class="sxs-lookup"><span data-stu-id="5673a-104">Backup happens Automatically</span></span>
<span data-ttu-id="5673a-105">Cuando se usa Azure Database for MySQL, el servicio de base de datos realiza automáticamente una copia de seguridad del servicio de cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="5673a-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="5673a-106">Las copias de seguridad están disponibles durante 7 días en el nivel Básico y 35 días en el nivel Estándar.</span><span class="sxs-lookup"><span data-stu-id="5673a-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="5673a-107">Para más información, consulte [Niveles de servicio de Azure Database for MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="5673a-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="5673a-108">Con esta característica de copia de seguridad automática, puede restaurar el servidor y todas sus bases de datos en un servidor nuevo a un momento dado anterior.</span><span class="sxs-lookup"><span data-stu-id="5673a-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="5673a-109">Restauración en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5673a-109">Restore in the Azure portal</span></span>
<span data-ttu-id="5673a-110">Azure Database for MySQL permite restaurar el servidor a un momento dado y en una nueva copia del servidor.</span><span class="sxs-lookup"><span data-stu-id="5673a-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="5673a-111">Puede usar este nuevo servidor para recuperar los datos.</span><span class="sxs-lookup"><span data-stu-id="5673a-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="5673a-112">Por ejemplo, si una tabla se quitó accidentalmente a mediodía de hoy, podría restaurar al momento justo antes de mediodía y recuperar la tabla y los datos que faltan desde esa copia nueva del servidor.</span><span class="sxs-lookup"><span data-stu-id="5673a-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="5673a-113">Los siguientes pasos restauran el servidor de ejemplo a un momento dado:</span><span class="sxs-lookup"><span data-stu-id="5673a-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="5673a-114">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5673a-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="5673a-115">Localice su servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="5673a-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="5673a-116">En el panel izquierdo, seleccione **Todos los recursos** y seleccione el servidor en la lista.</span><span class="sxs-lookup"><span data-stu-id="5673a-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="5673a-117">En la parte superior de la hoja de información general del servidor, haga clic en **Restaurar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="5673a-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="5673a-118">Se abre la hoja Restaurar.</span><span class="sxs-lookup"><span data-stu-id="5673a-118">The Restore blade opens.</span></span>
<span data-ttu-id="5673a-119">![haga clic en el botón restaurar](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="5673a-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="5673a-120">Rellene el formulario Restaurar con la información necesaria:</span><span class="sxs-lookup"><span data-stu-id="5673a-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="5673a-121">**Punto de restauración (UTC)**: use el selector de fecha y el selector de tiempo para seleccionar el momento al que se restaurará.</span><span class="sxs-lookup"><span data-stu-id="5673a-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="5673a-122">La hora especificada está en formato UTC, por lo que es probable que deba convertir la hora local a UTC.</span><span class="sxs-lookup"><span data-stu-id="5673a-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="5673a-123">**Restaurar en el servidor nuevo**: especifique el nombre del nuevo servidor donde se restaurará el servidor existente.</span><span class="sxs-lookup"><span data-stu-id="5673a-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="5673a-124">**Ubicación**: la opción de región se rellena automáticamente con la región del servidor de origen, y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="5673a-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="5673a-125">**Plan de tarifa**: la opción de plan de tarifa se rellena automáticamente con el mismo plan de tarifa que el servidor de origen, y no se puede cambiar aquí.</span><span class="sxs-lookup"><span data-stu-id="5673a-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="5673a-126">![Restauración de PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="5673a-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="5673a-127">Haga clic en **Aceptar** para restaurar el servidor a un momento dado.</span><span class="sxs-lookup"><span data-stu-id="5673a-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="5673a-128">Una vez finalizada la restauración, busque el nuevo servidor que se crea para comprobar que las bases de datos se restauraron del modo esperado.</span><span class="sxs-lookup"><span data-stu-id="5673a-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5673a-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5673a-129">Next steps</span></span>
- [<span data-ttu-id="5673a-130">Bibliotecas de conexiones de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="5673a-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)