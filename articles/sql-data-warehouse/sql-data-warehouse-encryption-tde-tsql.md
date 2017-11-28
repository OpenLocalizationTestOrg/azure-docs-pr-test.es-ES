---
title: Cifrado de datos transparente en SQL Data Warehouse (T-SQL)| Microsoft Docs
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="dfe95-103">Introducción al cifrado de datos transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="dfe95-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfe95-104">Información general sobre seguridad</span><span class="sxs-lookup"><span data-stu-id="dfe95-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="dfe95-105">Autenticación</span><span class="sxs-lookup"><span data-stu-id="dfe95-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="dfe95-106">Cifrado (Portal)</span><span class="sxs-lookup"><span data-stu-id="dfe95-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="dfe95-107">Cifrado (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="dfe95-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="dfe95-108">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="dfe95-108">Required Permssions</span></span>
<span data-ttu-id="dfe95-109">Para habilitar el Cifrado de datos transparente (TDE), debe ser un administrador o un miembro del rol dbmanager.</span><span class="sxs-lookup"><span data-stu-id="dfe95-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="dfe95-110">Habilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="dfe95-110">Enabling Encryption</span></span>
<span data-ttu-id="dfe95-111">Para habilitar TDE para una instancia de SQL Data Warehouse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dfe95-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="dfe95-112">Conéctese a la base de datos *maestra* en el servidor que hospeda la base de datos mediante un inicio de sesión que es un administrador o un miembro del rol **dbmanager** en la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="dfe95-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="dfe95-113">Ejecute la siguiente instrucción para cifrar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dfe95-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="dfe95-114">Deshabilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="dfe95-114">Disabling Encryption</span></span>
<span data-ttu-id="dfe95-115">Para deshabilitar TDE para una instancia de SQL Data Warehouse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dfe95-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="dfe95-116">Conéctese a la base de datos *maestra* mediante un inicio de sesión que es un administrador o un miembro del rol **dbmanager** en la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="dfe95-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="dfe95-117">Ejecute la siguiente instrucción para cifrar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dfe95-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="dfe95-118">Se debe reanudar una instancia de SQL Data Warehouse en pausa antes de realizar cambios en la configuración de TDE.</span><span class="sxs-lookup"><span data-stu-id="dfe95-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="dfe95-119">Comprobación del cifrado</span><span class="sxs-lookup"><span data-stu-id="dfe95-119">Verifying Encryption</span></span>
<span data-ttu-id="dfe95-120">Para comprobar el estado del cifrado para un Almacenamiento de datos SQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dfe95-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="dfe95-121">Conéctese a la base de datos *maestra* o de instancia mediante un inicio de sesión que es un administrador o un miembro del rol **dbmanager** en la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="dfe95-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="dfe95-122">Ejecute la siguiente instrucción para cifrar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dfe95-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="dfe95-123">Un resultado de ```1``` indica una base de datos cifrada, ```0``` indica una base de datos no cifrada.</span><span class="sxs-lookup"><span data-stu-id="dfe95-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="dfe95-124">DMV de cifrado</span><span class="sxs-lookup"><span data-stu-id="dfe95-124">Encryption DMVs</span></span>
* <span data-ttu-id="dfe95-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="dfe95-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="dfe95-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="dfe95-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
