---
title: Cifrado de datos transparente para la base de datos Stretch TSQL - Azure aaaEnable | Documentos de Microsoft
description: "Habilitación del cifrado de datos transparente (TDE) para SQL Server Stretch Database en Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="f8de6-103">Habilitación del cifrado de datos transparente (TDE) para Stretch Database en Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="f8de6-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8de6-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f8de6-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="f8de6-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="f8de6-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="f8de6-106">Cifrado de datos transparente (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="f8de6-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="f8de6-107">TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="f8de6-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="f8de6-108">clave de cifrado de base de datos de Hello está protegido por un certificado de servidor integrado.</span><span class="sxs-lookup"><span data-stu-id="f8de6-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="f8de6-109">certificado de servidor integrado de Hello es único para cada servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8de6-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="f8de6-110">Microsoft alterna automáticamente estos certificados al menos cada 90 días.</span><span class="sxs-lookup"><span data-stu-id="f8de6-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="f8de6-111">Para obtener una descripción general de TDE, vea [Cifrado de datos transparente (TDE)].</span><span class="sxs-lookup"><span data-stu-id="f8de6-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="f8de6-112">Habilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="f8de6-112">Enabling Encryption</span></span>
<span data-ttu-id="f8de6-113">tooenable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="f8de6-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="f8de6-114">Conectar toohello *maestro* base de datos en hello Azure hospedaje Hola datos del servidor mediante un inicio de sesión que es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="f8de6-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f8de6-115">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="f8de6-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="f8de6-116">Deshabilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="f8de6-116">Disabling Encryption</span></span>
<span data-ttu-id="f8de6-117">toodisable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="f8de6-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="f8de6-118">Conectar toohello *maestro* base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="f8de6-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f8de6-119">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="f8de6-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="f8de6-120">Comprobación del cifrado</span><span class="sxs-lookup"><span data-stu-id="f8de6-120">Verifying Encryption</span></span>
<span data-ttu-id="f8de6-121">estado de cifrado de tooverify para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="f8de6-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="f8de6-122">Conectar toohello *maestro* o base de datos de instancia mediante un inicio de sesión que es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola</span><span class="sxs-lookup"><span data-stu-id="f8de6-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f8de6-123">Ejecute hello después de la base de datos de instrucción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="f8de6-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="f8de6-124">Un resultado de ```1``` indica una base de datos cifrada, ```0``` indica una base de datos no cifrada.</span><span class="sxs-lookup"><span data-stu-id="f8de6-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Cifrado de datos transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
