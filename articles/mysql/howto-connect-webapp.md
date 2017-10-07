---
title: tooAzure de servicio de aplicaciones de Azure existente aaaConnect base de datos de MySQL | Documentos de Microsoft
description: "Instrucciones de cómo tooproperly conectarse un tooAzure de servicio de aplicaciones de Azure existente base de datos de MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="4e771-103">Conectar un tooAzure de servicio de aplicaciones de Azure base de datos existente de MySQL server</span><span class="sxs-lookup"><span data-stu-id="4e771-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="4e771-104">Este documento se explica cómo tooconnect un tooyour de servicio de aplicaciones de Azure existente Azure la base de datos de MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4e771-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4e771-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4e771-105">Before you begin</span></span>
<span data-ttu-id="4e771-106">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e771-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e771-107">Cree de un servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e771-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="4e771-108">Para obtener más información, consulte demasiado[cómo toocreate Azure la base de datos de MySQL server del Portal de](quickstart-create-mysql-server-database-using-azure-portal.md) o [cómo toocreate Azure la base de datos para el servidor de MySQL usando CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4e771-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="4e771-109">Actualmente hay dos soluciones tooenable acceso una base de datos de servicio de aplicaciones de Azure tooan de MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e771-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="4e771-110">En ambas soluciones hay que configurar las reglas de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="4e771-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="4e771-111">Solución 1: crear un tooallow de regla de firewall todas las direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4e771-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="4e771-112">Base de datos de Azure para MySQL proporciona seguridad de acceso mediante un firewall tooprotect los datos.</span><span class="sxs-lookup"><span data-stu-id="4e771-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="4e771-113">Cuando se conecta desde un servicio de aplicaciones de Azure de tooAzure base de datos de MySQL server, tenga en cuenta que Hola saliente direcciones IP de servicio de aplicaciones son de naturaleza dinámica.</span><span class="sxs-lookup"><span data-stu-id="4e771-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="4e771-114">disponibilidad de hello tooensure de su servicio de aplicación de Azure, se recomienda usar este tooallow solución todas las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4e771-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="4e771-115">Microsoft está trabajando para una tooavoid solución a largo plazo que permite que todas las direcciones IP para los servicios de Azure tooconnect tooAzure base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e771-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="4e771-116">En la hoja de servidor MySQL hello, bajo Configuración de encabezado, haga clic en **seguridad de conexión** tooopen hoja de seguridad de conexión de hello para la base de datos de Azure para MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="4e771-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="4e771-118">Escriba **NOMBRE DE LA REGLA**, **IP INICIAL** e **IP FINAL**.</span><span class="sxs-lookup"><span data-stu-id="4e771-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="4e771-119">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4e771-119">Then click **Save**.</span></span>
   - <span data-ttu-id="4e771-120">Nombre de la regla: Permitir-Todas-IP</span><span class="sxs-lookup"><span data-stu-id="4e771-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="4e771-121">IP inicial: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="4e771-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="4e771-122">IP final: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="4e771-122">End IP: 255.255.255.255</span></span>

   ![Azure Portal: agregar todas las IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="4e771-124">Solución 2: crear un firewall tooexplicitly de regla permitir saliente direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4e771-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="4e771-125">Puede agregar explícitamente que todos Hola saliente direcciones IP de su servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e771-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="4e771-126">En la hoja de propiedades del servicio de aplicación Hola, ver su **dirección IP saliente**.</span><span class="sxs-lookup"><span data-stu-id="4e771-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure Portal: ver direcciones IP de salida](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="4e771-128">En el módulo de seguridad de conexión de MySQL de hello, agregue direcciones IP saliente uno por uno.</span><span class="sxs-lookup"><span data-stu-id="4e771-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure Portal: agregar direcciones IP explícitas](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="4e771-130">Recuerde demasiado**guardar** las reglas del firewall.</span><span class="sxs-lookup"><span data-stu-id="4e771-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="4e771-131">Aunque Hola servicio de aplicaciones de Azure intenta tookeep IP direcciones constante con el tiempo, hay casos donde pueden cambiar las direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e771-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="4e771-132">Por ejemplo, cuando Hola reciclajes de aplicación o se produce una operación de escala, o cuando se agregan nuevas máquinas en Azure datos regionales centros de capacidad de hello tooincrease.</span><span class="sxs-lookup"><span data-stu-id="4e771-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="4e771-133">Cuando cambian de direcciones IP de hello, aplicación hello podría experimentar un tiempo de inactividad en caso de hello ya no puede conectarse toohello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4e771-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="4e771-134">Tenga en cuenta esta posibilidad al elegir uno de hello anterior soluciones.</span><span class="sxs-lookup"><span data-stu-id="4e771-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="4e771-135">Configuración de SSL</span><span class="sxs-lookup"><span data-stu-id="4e771-135">SSL configuration</span></span>
<span data-ttu-id="4e771-136">Azure Database for MySQL tiene SSL habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4e771-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="4e771-137">Si la aplicación no usa SSL tooconnect toohello database, necesita toodisable SSL en el servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e771-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="4e771-138">Para obtener más información acerca de cómo tooconfigure SSL, vea [uso de SSL con la base de datos de Azure para MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="4e771-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e771-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e771-139">Next steps</span></span>
<span data-ttu-id="4e771-140">Para obtener más información acerca de las cadenas de conexión, consulte demasiado[las cadenas de conexión](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="4e771-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
