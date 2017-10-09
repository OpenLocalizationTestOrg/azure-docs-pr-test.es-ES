---
title: "Cifrado de datos en el almacén de datos de SQL (Portal) aaaTransparent | Documentos de Microsoft"
description: Cifrado de datos transparente (TDE) en SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="95426-103">Introducción al cifrado de datos transparente (TDE) en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="95426-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95426-104">Información general sobre seguridad</span><span class="sxs-lookup"><span data-stu-id="95426-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="95426-105">Autenticación</span><span class="sxs-lookup"><span data-stu-id="95426-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="95426-106">Cifrado (Portal)</span><span class="sxs-lookup"><span data-stu-id="95426-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="95426-107">Cifrado (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="95426-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="95426-108">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="95426-108">Required Permssions</span></span>
<span data-ttu-id="95426-109">tooenable cifrado de datos transparente (TDE), debe ser un administrador o un miembro del rol dbmanager de Hola.</span><span class="sxs-lookup"><span data-stu-id="95426-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="95426-110">Habilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="95426-110">Enabling Encryption</span></span>
<span data-ttu-id="95426-111">tooenable TDE para un almacén de datos SQL, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="95426-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="95426-112">Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="95426-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="95426-113">En la hoja de la base de datos de hello, haga clic en hello **configuración** botón</span><span class="sxs-lookup"><span data-stu-id="95426-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="95426-114">Seleccione hello **cifrado de datos transparente** opción![][1]</span><span class="sxs-lookup"><span data-stu-id="95426-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="95426-115">Seleccione hello **en** configuración![][2]</span><span class="sxs-lookup"><span data-stu-id="95426-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="95426-116">Seleccione **Guardar**.
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="95426-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="95426-117">Deshabilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="95426-117">Disabling Encryption</span></span>
<span data-ttu-id="95426-118">toodisable TDE para un almacén de datos SQL, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="95426-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="95426-119">Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="95426-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="95426-120">En la hoja de la base de datos de hello, haga clic en hello **configuración** botón</span><span class="sxs-lookup"><span data-stu-id="95426-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="95426-121">Seleccione hello **cifrado de datos transparente** opción![][1]</span><span class="sxs-lookup"><span data-stu-id="95426-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="95426-122">Seleccione hello **desactivar** configuración![][4]</span><span class="sxs-lookup"><span data-stu-id="95426-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="95426-123">Seleccione **Guardar**.
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="95426-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="95426-124">DMV de cifrado</span><span class="sxs-lookup"><span data-stu-id="95426-124">Encryption DMVs</span></span>
<span data-ttu-id="95426-125">El cifrado se puede confirmar con hello las siguientes DMV:</span><span class="sxs-lookup"><span data-stu-id="95426-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="95426-126">[Sys.Databases]</span><span class="sxs-lookup"><span data-stu-id="95426-126">[sys.databases]</span></span>
* <span data-ttu-id="95426-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="95426-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[Sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
