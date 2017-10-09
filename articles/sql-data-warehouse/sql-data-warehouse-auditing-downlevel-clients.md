---
title: "los clientes de nivel inferior de almacenamiento de datos de aaaSQL soporte para auditoría de datos | Documentos de Microsoft"
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
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="596ca-103">SQL Data Warehouse: compatibilidad con clientes de nivel inferior para enmascaramiento de datos dinámicos y auditoría</span><span class="sxs-lookup"><span data-stu-id="596ca-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="596ca-104">[Auditoría](sql-data-warehouse-auditing-overview.md) funciona con los clientes SQL que admiten el redireccionamiento de TDS.</span><span class="sxs-lookup"><span data-stu-id="596ca-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="596ca-105">Cualquier cliente que implementa TDS 7.4 también debe admitir el redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="596ca-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="596ca-106">Excepciones toothis incluyen JDBC 4.0 de qué característica de redirección de hello no es totalmente compatible y tediosas para Node.JS en el que no se implementó la redirección.</span><span class="sxs-lookup"><span data-stu-id="596ca-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="596ca-107">Para "Clientes de nivel inferior", es decir, que admite la versión 7.3 TDS y a continuación - Hola FQDN del servidor en la cadena de conexión de hello debe modificarse:</span><span class="sxs-lookup"><span data-stu-id="596ca-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="596ca-108">FQDN del servidor original en la cadena de conexión de hello: <*nombre del servidor*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="596ca-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="596ca-109">FQDN del servidor modificado en la cadena de conexión de hello: <*nombre del servidor*> base de datos. **seguro**. windows.net</span><span class="sxs-lookup"><span data-stu-id="596ca-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="596ca-110">Una lista parcial de "Clientes de nivel inferior" incluye:</span><span class="sxs-lookup"><span data-stu-id="596ca-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="596ca-111">.NET 4.0 y versiones posteriores,</span><span class="sxs-lookup"><span data-stu-id="596ca-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="596ca-112">ODBC 10.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="596ca-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="596ca-113">JDBC (al mismo tiempo JDBC admiten TDS 7.4, Hola característica de redirección de TDS no es totalmente compatible)</span><span class="sxs-lookup"><span data-stu-id="596ca-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="596ca-114">Tedious (para Node.JS)</span><span class="sxs-lookup"><span data-stu-id="596ca-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="596ca-115">**Comentario:** Hola por encima de la modificación de FQDN de servidor puede ser útil también para aplicar una directiva de auditoría de nivel de SQL Server sin necesidad de una configuración paso a paso en cada base de datos (mitigación temporal).</span><span class="sxs-lookup"><span data-stu-id="596ca-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

