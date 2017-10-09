---
title: "aaaPorts más allá de 1433 para la base de datos SQL | Documentos de Microsoft"
description: "Conexiones de cliente de ADO.NET tooAzure base de datos SQL a veces omiten el proxy de Hola e interactúan directamente con la base de datos de Hola. Los puertos que no sean 1433 se convierten en puertos importantes."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="9f84a-104">Puertos más allá de 1433 para ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9f84a-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="9f84a-105">Este tema describe el comportamiento de conexión de base de datos de SQL Azure de Hola para los clientes que utilizan ADO.NET 4.5 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="9f84a-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9f84a-106">Para obtener información acerca de la arquitectura de conectividad, consulte [Arquitectura de conectividad de Azure SQL Database](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="9f84a-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="9f84a-107">Fuera o dentro</span><span class="sxs-lookup"><span data-stu-id="9f84a-107">Outside vs inside</span></span>
<span data-ttu-id="9f84a-108">Para las conexiones tooAzure base de datos SQL, debemos primero pedimos si se ejecuta el programa cliente *fuera* o *dentro de* límite de nube de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9f84a-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="9f84a-109">subsecciones de Hola describen dos escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="9f84a-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="9f84a-110">*Fuera:* el cliente se ejecuta en el equipo de escritorio</span><span class="sxs-lookup"><span data-stu-id="9f84a-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="9f84a-111">Puerto 1433 es Hola solo que deben estar abiertos en el equipo de escritorio que hospeda la aplicación de cliente de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9f84a-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="9f84a-112">*Dentro:* el cliente se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="9f84a-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="9f84a-113">Cuando el cliente se ejecuta dentro del límite de la nube de Azure de hello, usa lo que podemos llamar un *ruta directa* toointeract con el servidor de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f84a-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="9f84a-114">Una vez establecida una conexión, las interacciones entre el cliente de Hola y de base de datos no implican a ningún proxy de middleware.</span><span class="sxs-lookup"><span data-stu-id="9f84a-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="9f84a-115">secuencia de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="9f84a-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="9f84a-116">ADO.NET 4.5 (o posterior) inicia una interacción breve con hello nube de Azure y recibe un número de puerto identificada de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="9f84a-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="9f84a-117">número de puerto de Hello identificada de manera dinámica esté entre Hola 11000 a 11999 o 14000 a 14999.</span><span class="sxs-lookup"><span data-stu-id="9f84a-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="9f84a-118">ADO.NET, a continuación, se conecta toohello servidor de base de datos SQL directamente, con ningún middleware en medio.</span><span class="sxs-lookup"><span data-stu-id="9f84a-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="9f84a-119">Las consultas se envían directamente toohello base de datos y los resultados se devuelven directamente toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="9f84a-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="9f84a-120">Asegúrese de que el puerto Hola intervalos de 11000 a 11999 y 14000 a 14999 en el equipo cliente de Azure quedan disponibles para las interacciones de cliente de ADO.NET 4.5 con base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="9f84a-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="9f84a-121">En concreto, los puertos Hola intervalo deben permanecer sin bloqueadores de otros elementos de salida.</span><span class="sxs-lookup"><span data-stu-id="9f84a-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="9f84a-122">En la VM de Azure, Hola **Firewall de Windows con seguridad avanzada** controles Hola configuración del puerto.</span><span class="sxs-lookup"><span data-stu-id="9f84a-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="9f84a-123">Puede usar hello [interfaz de usuario del servidor de seguridad](http://msdn.microsoft.com/library/cc646023.aspx) tooadd una regla para la que se especifique hello **TCP** como protocolo junto con un intervalo de puertos con la sintaxis de hello **11000 a 11999**.</span><span class="sxs-lookup"><span data-stu-id="9f84a-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="9f84a-124">Aclaraciones de versiones</span><span class="sxs-lookup"><span data-stu-id="9f84a-124">Version clarifications</span></span>
<span data-ttu-id="9f84a-125">En esta sección se aclara los monikers de Hola que hacen referencia a las versiones de tooproduct.</span><span class="sxs-lookup"><span data-stu-id="9f84a-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="9f84a-126">También se muestran algunos emparejamientos de versiones entre productos.</span><span class="sxs-lookup"><span data-stu-id="9f84a-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="9f84a-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9f84a-127">ADO.NET</span></span>
* <span data-ttu-id="9f84a-128">ADO.NET 4.0 es compatible con el protocolo de hello TDS 7.3, pero no 7.4.</span><span class="sxs-lookup"><span data-stu-id="9f84a-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="9f84a-129">ADO.NET 4.5 y posterior admite protocolo de hello TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="9f84a-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="9f84a-130">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="9f84a-130">Related links</span></span>
* <span data-ttu-id="9f84a-131">ADO.NET 4.6 se publicó el 20 de julio de 2015.</span><span class="sxs-lookup"><span data-stu-id="9f84a-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="9f84a-132">Hay un anuncio del blog del equipo de .NET de hello [aquí](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f84a-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="9f84a-133">ADO.NET 4.5 se publicó el 15 de julio de 2012.</span><span class="sxs-lookup"><span data-stu-id="9f84a-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="9f84a-134">Hay un anuncio del blog del equipo de .NET de hello [aquí](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f84a-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="9f84a-135">Hay una entrada de blog sobre ADO.NET 4.5.1 disponible [aquí](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f84a-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="9f84a-136">Lista de versiones del protocolo TDS</span><span class="sxs-lookup"><span data-stu-id="9f84a-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="9f84a-137">Información general de desarrollo de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="9f84a-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="9f84a-138">Firewall de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="9f84a-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="9f84a-139">Configuración del firewall en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="9f84a-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

