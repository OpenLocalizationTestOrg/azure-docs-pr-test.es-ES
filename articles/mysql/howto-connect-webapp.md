---
title: "Conexión de Azure App Service existente a Azure Database for MySQL | Microsoft Docs"
description: "Instrucciones sobre cómo conectar correctamente un servicio existente de Azure App Service a Azure Database para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="9d7d6-103">Conexión de un servicio existente de Azure App Service a un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="9d7d6-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="9d7d6-104">Este documento explica cómo conectar un servicio existente de Azure App Service a un servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d7d6-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9d7d6-105">Before you begin</span></span>
<span data-ttu-id="9d7d6-106">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d7d6-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d7d6-107">Cree de un servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="9d7d6-108">Para obtener más información, consulte [Creación de un servidor de Azure Database for MySQL con Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md) o [Creación de un servidor de Azure Database for MySQL con la CLI de Azure](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d6-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="9d7d6-109">Actualmente hay dos soluciones para habilitar el acceso desde un servicio de Azure App Service a un servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="9d7d6-110">En ambas soluciones hay que configurar las reglas de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="9d7d6-111">Solución 1: crear una regla de firewall para permitir todas las direcciones IP</span><span class="sxs-lookup"><span data-stu-id="9d7d6-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="9d7d6-112">Azure Database for MySQL proporciona seguridad de acceso mediante un firewall para proteger los datos.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="9d7d6-113">Al conectarse desde un servicio de Azure App Service a un servidor de Azure Database for MySQL server, tenga en cuenta que las direcciones IP de salida de App Service son de naturaleza dinámica.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="9d7d6-114">Para garantizar la disponibilidad del servicio Azure App Service, se recomienda usar esta solución para permitir TODAS las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="9d7d6-115">Microsoft está trabajando para que una solución a largo plazo para evitar permitir todas las direcciones IP para los servicios de Azure en las conexiones a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="9d7d6-116">En la hoja del servidor de MySQL, en el encabezado Configuración, haga clic en **Seguridad de conexión** para abrir la hoja de seguridad de conexión para Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure Portal: haga clic en Seguridad de conexión](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="9d7d6-118">Escriba **NOMBRE DE LA REGLA**, **IP INICIAL** e **IP FINAL**.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="9d7d6-119">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-119">Then click **Save**.</span></span>
   - <span data-ttu-id="9d7d6-120">Nombre de la regla: Permitir-Todas-IP</span><span class="sxs-lookup"><span data-stu-id="9d7d6-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="9d7d6-121">IP inicial: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="9d7d6-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="9d7d6-122">IP final: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="9d7d6-122">End IP: 255.255.255.255</span></span>

   ![Azure Portal: agregar todas las IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="9d7d6-124">Solución 2: crear una regla de firewall para permitir explícitamente las direcciones IP de salida</span><span class="sxs-lookup"><span data-stu-id="9d7d6-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="9d7d6-125">Puede agregar explícitamente todas las IP de salida de su Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="9d7d6-126">En la hoja de propiedades de App Service, consulte su **DIRECCIÓN IP DE SALIDA**.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure Portal: ver direcciones IP de salida](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="9d7d6-128">En la hoja de Seguridad de conexión de MySQL, agregue las direcciones IP de salida una por una.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure Portal: agregar direcciones IP explícitas](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="9d7d6-130">No olvide **Guardar** las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="9d7d6-131">Aunque el Azure App Service intenta que no se modifiquen las direcciones IP con el tiempo, hay casos en los que pueden cambiar las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="9d7d6-132">Por ejemplo, se produce cuando se recicla la aplicación o cuando se realiza una operación de escala, o cuando se añaden nuevos equipos en los centros de datos regionales de Azure para aumentar la capacidad.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="9d7d6-133">Cuando cambian las direcciones IP, la aplicación podría experimentar un tiempo de inactividad en caso de que ya no pueda conectarse al servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="9d7d6-134">Al elegir una de las soluciones anteriores, tenga en cuenta esta posibilidad.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="9d7d6-135">Configuración de SSL</span><span class="sxs-lookup"><span data-stu-id="9d7d6-135">SSL configuration</span></span>
<span data-ttu-id="9d7d6-136">Azure Database for MySQL tiene SSL habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="9d7d6-137">Si la aplicación no usa SSL para conectarse a la base de datos, debe deshabilitar SSL en el servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="9d7d6-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="9d7d6-138">Para obtener más información sobre cómo configurar SSL, consulte [Uso de SSL con Azure Database for MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d6-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d7d6-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d7d6-139">Next steps</span></span>
<span data-ttu-id="9d7d6-140">Para obtener más información sobre las cadenas de conexión, consulte [Cadenas de conexión](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d6-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
