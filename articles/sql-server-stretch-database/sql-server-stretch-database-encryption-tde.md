---
title: Cifrado de datos transparente para Stretch Database - Azure aaaEnable | Documentos de Microsoft
description: "Habilitación del cifrado de datos transparente (TDE) para SQL Server Stretch Database en Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="d6df7-103">Habilitación del cifrado de datos transparente (TDE) para Stretch Database en Azure</span><span class="sxs-lookup"><span data-stu-id="d6df7-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6df7-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d6df7-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="d6df7-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="d6df7-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="d6df7-106">Cifrado de datos transparente (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6df7-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="d6df7-107">TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="d6df7-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="d6df7-108">clave de cifrado de base de datos de Hello está protegido por un certificado de servidor integrado.</span><span class="sxs-lookup"><span data-stu-id="d6df7-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="d6df7-109">certificado de servidor integrado de Hello es único para cada servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6df7-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="d6df7-110">Microsoft alterna automáticamente estos certificados al menos cada 90 días.</span><span class="sxs-lookup"><span data-stu-id="d6df7-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="d6df7-111">Para obtener una descripción general de TDE, vea [Cifrado de datos transparente (TDE)].</span><span class="sxs-lookup"><span data-stu-id="d6df7-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="d6df7-112">Habilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="d6df7-112">Enabling Encryption</span></span>
<span data-ttu-id="d6df7-113">tooenable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="d6df7-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="d6df7-114">Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d6df7-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="d6df7-115">En la hoja de la base de datos de hello, haga clic en hello **configuración** botón</span><span class="sxs-lookup"><span data-stu-id="d6df7-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="d6df7-116">Seleccione hello **cifrado de datos transparente** opción![][1]</span><span class="sxs-lookup"><span data-stu-id="d6df7-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="d6df7-117">Seleccione hello **en** configuración y, a continuación, seleccione **guardar**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="d6df7-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="d6df7-118">Deshabilitar el cifrado</span><span class="sxs-lookup"><span data-stu-id="d6df7-118">Disabling Encryption</span></span>
<span data-ttu-id="d6df7-119">toodisable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="d6df7-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="d6df7-120">Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d6df7-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="d6df7-121">En la hoja de la base de datos de hello, haga clic en hello **configuración** botón</span><span class="sxs-lookup"><span data-stu-id="d6df7-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="d6df7-122">Seleccione hello **cifrado de datos transparente** opción</span><span class="sxs-lookup"><span data-stu-id="d6df7-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="d6df7-123">Seleccione hello **desactivar** configuración y, a continuación, seleccione **guardar**</span><span class="sxs-lookup"><span data-stu-id="d6df7-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Cifrado de datos transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
