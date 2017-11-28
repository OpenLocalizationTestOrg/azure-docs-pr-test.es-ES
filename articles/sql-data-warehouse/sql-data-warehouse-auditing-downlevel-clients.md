---
title: "Compatibilidad de SQL Data Warehouse con clientes de nivel inferior para la auditoría de datos | Microsoft Docs"
description: "Obtenga información sobre compatibilidad de Almacenamiento de datos SQL con clientes de nivel inferior para auditoría de datos."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="adb2e-103">SQL Data Warehouse: compatibilidad con clientes de nivel inferior para enmascaramiento de datos dinámicos y auditoría</span><span class="sxs-lookup"><span data-stu-id="adb2e-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="adb2e-104">[Auditoría](sql-data-warehouse-auditing-overview.md) funciona con los clientes SQL que admiten el redireccionamiento de TDS.</span><span class="sxs-lookup"><span data-stu-id="adb2e-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="adb2e-105">Cualquier cliente que implementa TDS 7.4 también debe admitir el redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="adb2e-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="adb2e-106">Entre las excepciones a esto se incluyen JDBC 4.0, en el que la función de redireccionamiento no es totalmente compatible y Tedious para Node.JS, en cuya redireccionamiento no se ha implementado.</span><span class="sxs-lookup"><span data-stu-id="adb2e-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="adb2e-107">Para "clientes de nivel inferior", es decir, los que admiten TDS versión 7.3 e inferiores, debe modificarse el FQDN del servidor en la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="adb2e-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="adb2e-108">FQDN del servidor original en la cadena de conexión: <*nombre del servidor*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="adb2e-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="adb2e-109">FQDN del servidor modificado en la cadena de conexión: <*nombre del servidor*>. database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="adb2e-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="adb2e-110">Una lista parcial de "Clientes de nivel inferior" incluye:</span><span class="sxs-lookup"><span data-stu-id="adb2e-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="adb2e-111">.NET 4.0 y versiones posteriores,</span><span class="sxs-lookup"><span data-stu-id="adb2e-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="adb2e-112">ODBC 10.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="adb2e-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="adb2e-113">JDBC (aunque JDBC admite TDS 7.4, la característica de redireccionamiento de TDS no es totalmente compatible)</span><span class="sxs-lookup"><span data-stu-id="adb2e-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="adb2e-114">Tedious (para Node.JS)</span><span class="sxs-lookup"><span data-stu-id="adb2e-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="adb2e-115">**Comentario:** la anterior modificación de FDQN de servidor puede resultar útil también para aplicar una directiva de auditoría de nivel de SQL Server sin necesidad de un paso de configuración en cada base de datos (mitigación temporal).</span><span class="sxs-lookup"><span data-stu-id="adb2e-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

