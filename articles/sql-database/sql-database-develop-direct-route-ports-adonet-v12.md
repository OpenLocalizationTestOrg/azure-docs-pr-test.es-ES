---
title: "Puertos más allá de 1433 para SQL Database | Microsoft Docs"
description: "Las conexiones de cliente de ADO.NET a Azure SQL Database omiten el proxy e interactúan directamente con la base de datos. Los puertos que no sean 1433 se convierten en puertos importantes."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="f3a63-104">Puertos más allá de 1433 para ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f3a63-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="f3a63-105">En este tema se describe el comportamiento de conexión de Azure SQL Database para clientes que usan ADO.NET 4.5 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="f3a63-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f3a63-106">Para obtener información acerca de la arquitectura de conectividad, consulte [Arquitectura de conectividad de Azure SQL Database](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="f3a63-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="f3a63-107">Fuera o dentro</span><span class="sxs-lookup"><span data-stu-id="f3a63-107">Outside vs inside</span></span>
<span data-ttu-id="f3a63-108">Para las conexiones a Azure SQL Database, debemos preguntar si el programa cliente se ejecuta *fuera* o *dentro* del límite de la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3a63-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="f3a63-109">En las subsecciones se describen dos escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="f3a63-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="f3a63-110">*Fuera:* el cliente se ejecuta en el equipo de escritorio</span><span class="sxs-lookup"><span data-stu-id="f3a63-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="f3a63-111">El puerto 1433 es el único puerto que debe estar abierto en su equipo de escritorio que hospeda su aplicación de cliente de la Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f3a63-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="f3a63-112">*Dentro:* el cliente se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="f3a63-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="f3a63-113">Cuando el cliente se ejecuta dentro del límite de la nube de Azure, usa lo que podemos llamar una *ruta directa* para interactuar con el servidor de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f3a63-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="f3a63-114">Cuando se ha establecido una conexión, las interacciones posteriores entre el cliente y la base de datos no implican ningún proxy de middleware.</span><span class="sxs-lookup"><span data-stu-id="f3a63-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="f3a63-115">La secuencia es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3a63-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="f3a63-116">ADO.NET 4.5 (o posterior) inicia una breve interacción con la nube de Azure y recibe un número de puerto identificado dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="f3a63-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="f3a63-117">El número de puerto identificado dinámicamente se encuentra en el intervalo de 11000-11999 o 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="f3a63-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="f3a63-118">Luego, ADO.NET se conecta al servidor de Base de datos SQL directamente, sin ningún middleware entre ellos.</span><span class="sxs-lookup"><span data-stu-id="f3a63-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="f3a63-119">Las consultas se envían directamente a la base de datos y los resultados se devuelven directamente al cliente.</span><span class="sxs-lookup"><span data-stu-id="f3a63-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="f3a63-120">Asegúrese de que los intervalos de puertos de 11000 a 11999 y de 14000 a 14999 en el equipo cliente de Azure queden disponibles para las interacciones de cliente de ADO.NET 4.5 con SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f3a63-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="f3a63-121">En concreto, los puertos del intervalo deben estar libres de cualquier otro bloqueador de salida.</span><span class="sxs-lookup"><span data-stu-id="f3a63-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="f3a63-122">En la máquina virtual de Azure, **Firewall de Windows con seguridad avanzada** controla la configuración de puertos.</span><span class="sxs-lookup"><span data-stu-id="f3a63-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="f3a63-123">Puede usar la [interfaz de usuario del firewall](http://msdn.microsoft.com/library/cc646023.aspx) para agregar una regla para la que se especifique el protocolo **TCP** junto con un intervalo de puertos con una sintaxis similar a **11000-11999**.</span><span class="sxs-lookup"><span data-stu-id="f3a63-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="f3a63-124">Aclaraciones de versiones</span><span class="sxs-lookup"><span data-stu-id="f3a63-124">Version clarifications</span></span>
<span data-ttu-id="f3a63-125">En esta sección se explican los monikers que hacen referencia a las versiones de producto.</span><span class="sxs-lookup"><span data-stu-id="f3a63-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="f3a63-126">También se muestran algunos emparejamientos de versiones entre productos.</span><span class="sxs-lookup"><span data-stu-id="f3a63-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="f3a63-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="f3a63-127">ADO.NET</span></span>
* <span data-ttu-id="f3a63-128">ADO.NET 4.0 admite el protocolo TDS 7.3, pero no 7.4.</span><span class="sxs-lookup"><span data-stu-id="f3a63-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="f3a63-129">ADO.NET 4.5 y versiones posteriores admite el protocolo TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="f3a63-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="f3a63-130">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="f3a63-130">Related links</span></span>
* <span data-ttu-id="f3a63-131">ADO.NET 4.6 se publicó el 20 de julio de 2015.</span><span class="sxs-lookup"><span data-stu-id="f3a63-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="f3a63-132">Hay un anuncio de blog del equipo de .NET disponible [aquí](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3a63-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="f3a63-133">ADO.NET 4.5 se publicó el 15 de julio de 2012.</span><span class="sxs-lookup"><span data-stu-id="f3a63-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="f3a63-134">Hay un anuncio de blog del equipo de .NET disponible [aquí](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3a63-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="f3a63-135">Hay una entrada de blog sobre ADO.NET 4.5.1 disponible [aquí](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3a63-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="f3a63-136">Lista de versiones del protocolo TDS</span><span class="sxs-lookup"><span data-stu-id="f3a63-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="f3a63-137">Información general de desarrollo de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f3a63-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="f3a63-138">Firewall de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f3a63-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="f3a63-139">Configuración del firewall en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f3a63-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

