---
title: aaaHow tooRestore un servidor de base de datos de Azure para MySQL | Documentos de Microsoft
description: "Este artículo se describe cómo toorestore un servidor de base de datos de Azure para el uso de MySQL Hola portal de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="4bf0a-103">¿Cómo tooBackup y restaurar un servidor de base de datos de Azure para el uso de MySQL Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4bf0a-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="4bf0a-104">Las copias de seguridad se realizan automáticamente</span><span class="sxs-lookup"><span data-stu-id="4bf0a-104">Backup happens Automatically</span></span>
<span data-ttu-id="4bf0a-105">Cuando se usa la base de datos de Azure para MySQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="4bf0a-106">las copias de seguridad de Hello están disponibles durante 7 días al utilizar el nivel básico y 35 días cuando se utiliza el nivel estándar.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="4bf0a-107">Para más información, consulte [Niveles de servicio de Azure Database for MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="4bf0a-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="4bf0a-108">Con esta característica de copia de seguridad automática, puede restaurar servidor hello y todas sus bases de datos en un nuevo servidor tooan anteriormente en un momento.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="4bf0a-109">Restaurar en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4bf0a-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="4bf0a-110">Azure base de datos de MySQL permite toorestore Hola servidor back-tooa punto en el tiempo y en tooa nueva copia del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="4bf0a-111">Puede usar esta nueva toorecover server los datos.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="4bf0a-112">Por ejemplo, si una tabla no estaba accidentalmente quita al mediodía hoy en día, se podría restaurar toohello tiempo justo antes del mediodía y recuperar Hola falta la tabla y los datos de esa nueva copia del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="4bf0a-113">Hello pasos siguientes punto de restauración Hola ejemplo server tooa en el tiempo:</span><span class="sxs-lookup"><span data-stu-id="4bf0a-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="4bf0a-114">Inicio de sesión en hello [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="4bf0a-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="4bf0a-115">Localice su servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="4bf0a-116">En el panel izquierdo de hello, seleccione **todos los recursos**, a continuación, seleccione el servidor de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="4bf0a-117">En la parte superior de Hola de hoja de información general del servidor de hello, haga clic en **restaurar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="4bf0a-118">se abre la hoja de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-118">hello Restore blade opens.</span></span>
<span data-ttu-id="4bf0a-119">![haga clic en el botón restaurar](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="4bf0a-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="4bf0a-120">Rellene el formulario de restauración de hello con información de hello necesario:</span><span class="sxs-lookup"><span data-stu-id="4bf0a-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="4bf0a-121">**(UTC) del punto de restauración**: mediante el selector de fecha de Hola y Selector de tiempo, seleccione un toorestore en un momento a.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="4bf0a-122">hora de Hello especificada está en formato UTC, por lo que es probable que tenga la hora local de tooconvert hello en UTC.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="4bf0a-123">**Restaurar el servidor de toonew**: proporcionar un nuevo servidor de servidor existente Hola de nombre toorestore en.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="4bf0a-124">**Ubicación**: elección de la región de hello automáticamente rellena con la región de servidor de origen de hello y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="4bf0a-125">**Nivel de precios**: Hola elección de nivel de precios automáticamente se rellena con hello precios de mismo nivel como servidor de origen de hello y no se puede cambiar aquí.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="4bf0a-126">![Restauración de PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="4bf0a-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="4bf0a-127">Haga clic en **Aceptar** toorestore Hola server toorestore tooa punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="4bf0a-128">Una vez finalizada la restauración de hello, localizar el servidor nuevo de Hola que creó hello tooverify bases de datos restauradas según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="4bf0a-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bf0a-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4bf0a-129">Next steps</span></span>
- [<span data-ttu-id="4bf0a-130">Bibliotecas de conexiones de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4bf0a-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)