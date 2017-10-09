---
title: "aaaManage bases de datos de SQL de Azure mediante automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usa las bases de datos SQL de Azure a escala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="b971a-103">Administración de bases de datos SQL de Azure mediante Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="b971a-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="b971a-104">Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa la administración de las bases de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b971a-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b971a-105">¿Qué es Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="b971a-105">What is Azure Automation?</span></span>
<span data-ttu-id="b971a-106">[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos.</span><span class="sxs-lookup"><span data-stu-id="b971a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b971a-107">Mediante automatización de Azure, las tareas de ejecución prolongada, manuales, propensa a errores y repiten con frecuencia pueden ser tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.</span><span class="sxs-lookup"><span data-stu-id="b971a-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b971a-108">Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y alta disponibilidad que escala toomeet sus necesidades a medida que crece la organización.</span><span class="sxs-lookup"><span data-stu-id="b971a-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b971a-109">En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b971a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b971a-110">Reducir la sobrecarga operativa y liberar TI / DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="b971a-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="b971a-111">¿Cómo puede Automatización de Azure ayudar a administrar bases de datos SQL de Azure?</span><span class="sxs-lookup"><span data-stu-id="b971a-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="b971a-112">La base de datos de SQL Azure pueden administrarse en automatización de Azure mediante el uso de hello [cmdlets de PowerShell de base de datos de SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) que están disponibles en hello [herramientas de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b971a-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="b971a-113">Automatización de Azure tiene estos cmdlets de PowerShell de base de datos de SQL Azure disponibles fuera del cuadro de hello, por lo que puede realizar todas las tareas de administración de base de datos SQL en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b971a-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="b971a-114">También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="b971a-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b971a-115">Automatización de Azure tiene también Hola capacidad toocommunicate con servidores SQL Server directamente, mediante la emisión de comandos SQL con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b971a-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="b971a-116">Hola [Galería de runbooks de automatización de Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene una variedad de producto equipo y la Comunidad runbooks tooget iniciado automatizar la administración de bases de datos de SQL Azure, otros servicios de Azure y sistemas de terceros 3rd.</span><span class="sxs-lookup"><span data-stu-id="b971a-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="b971a-117">Los runbooks de la Galería incluyen:</span><span class="sxs-lookup"><span data-stu-id="b971a-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="b971a-118">Ejecución de consultas SQL en una Base de datos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="b971a-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="b971a-119">Escalación vertical (arriba o abajo) de una Base de datos SQL de Azure en una programación</span><span class="sxs-lookup"><span data-stu-id="b971a-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="b971a-120">Truncamiento de una tabla SQL si su base de datos se aproxima al tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="b971a-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="b971a-121">Indexación de tablas en una Base de datos SQL de Azure si están muy fragmentadas</span><span class="sxs-lookup"><span data-stu-id="b971a-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="b971a-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b971a-122">Next steps</span></span>
<span data-ttu-id="b971a-123">Ahora que ha aprendido conceptos básicos de Hola de automatización de Azure y cómo puede resultarle toomanage usado bases de datos de SQL Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="b971a-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="b971a-124">Información general sobre Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="b971a-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="b971a-125">Mi primer runbook</span><span class="sxs-lookup"><span data-stu-id="b971a-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b971a-126">Mapa de aprendizaje de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="b971a-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="b971a-127">Automatización de Azure: El agente de SQL en hello en la nube</span><span class="sxs-lookup"><span data-stu-id="b971a-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

