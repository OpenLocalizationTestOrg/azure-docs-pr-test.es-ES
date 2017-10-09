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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Habilitación del cifrado de datos transparente (TDE) para Stretch Database en Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Cifrado de datos transparente (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación.

TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica. clave de cifrado de base de datos de Hello está protegido por un certificado de servidor integrado. certificado de servidor integrado de Hello es único para cada servidor de Azure. Microsoft alterna automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente (TDE)].

## <a name="enabling-encryption"></a>Habilitar el cifrado
tooenable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:

1. Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)
2. En la hoja de la base de datos de hello, haga clic en hello **configuración** botón
3. Seleccione hello **cifrado de datos transparente** opción![][1]
4. Seleccione hello **en** configuración y, a continuación, seleccione **guardar**
   ![][2]

## <a name="disabling-encryption"></a>Deshabilitar el cifrado
toodisable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:

1. Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)
2. En la hoja de la base de datos de hello, haga clic en hello **configuración** botón
3. Seleccione hello **cifrado de datos transparente** opción
4. Seleccione hello **desactivar** configuración y, a continuación, seleccione **guardar**

<!--Anchors-->
[Cifrado de datos transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
