---
title: "Cifrado de datos en el almacén de datos de SQL (T-SQL) aaaTransparent | Documentos de Microsoft"
description: Cifrado de datos transparente (TDE) en SQL Data Warehouse (T-SQL)
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="63192-103">Introducción al cifrado de datos transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="63192-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="63192-104">Información general sobre seguridad</span><span class="sxs-lookup"><span data-stu-id="63192-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="63192-105">Autenticación</span><span class="sxs-lookup"><span data-stu-id="63192-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="63192-106">Cifrado (Portal)</span><span class="sxs-lookup"><span data-stu-id="63192-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="63192-107">Cifrado (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="63192-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="63192-108">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="63192-108">Required Permssions</span></span>
<span data-ttu-id="63192-109">tooenable cifrado de datos transparente (TDE), debe ser un administrador o un miembro del rol dbmanager de Hola.</span><span class="sxs-lookup"><span data-stu-id="63192-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="63192-110">Habilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="63192-110">Enabling Encryption</span></span>
<span data-ttu-id="63192-111">Siga estos tooenable pasos TDE para un almacenamiento de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="63192-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="63192-112">Conectar toohello *maestro* base de datos servidor hello hospeda Hola base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="63192-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="63192-113">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="63192-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="63192-114">Deshabilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="63192-114">Disabling Encryption</span></span>
<span data-ttu-id="63192-115">Siga estos toodisable pasos TDE para un almacenamiento de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="63192-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="63192-116">Conectar toohello *maestro* base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="63192-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="63192-117">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="63192-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="63192-118">Un almacén de datos de SQL en pausa se debe reanudar antes de realizar cambios de configuración de TDE toohello.</span><span class="sxs-lookup"><span data-stu-id="63192-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="63192-119">Comprobación del cifrado</span><span class="sxs-lookup"><span data-stu-id="63192-119">Verifying Encryption</span></span>
<span data-ttu-id="63192-120">estado de cifrado de tooverify para un almacén de datos SQL, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="63192-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="63192-121">Conectar toohello *maestro* o base de datos de instancia mediante un inicio de sesión que es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="63192-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="63192-122">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="63192-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="63192-123">Un resultado de ```1``` indica una base de datos cifrada, ```0``` indica una base de datos no cifrada.</span><span class="sxs-lookup"><span data-stu-id="63192-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="63192-124">DMV de cifrado</span><span class="sxs-lookup"><span data-stu-id="63192-124">Encryption DMVs</span></span>
* <span data-ttu-id="63192-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="63192-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="63192-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="63192-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
