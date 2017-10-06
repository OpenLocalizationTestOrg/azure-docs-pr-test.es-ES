---
title: "Azure Portal: replicación geográfica de SQL Database | Microsoft Docs"
description: "Configurar la replicación geográfica para la base de datos de SQL Azure en el portal de Azure de Hola y de conmutación por error de inicio"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Configurar la replicación geográfica activa para base de datos de SQL Azure en el portal de Azure de Hola y de conmutación por error de inicio

Este artículo muestra cómo tooconfigure replicación geográfica activa para base de datos SQL en hello [portal de Azure](http://portal.azure.com) y tooinitiate conmutación por error.

conmutación por error de tooinitiate con hello portal de Azure, consulte [iniciar una conmutación por error planeada o no planeada de la base de datos de SQL Azure con hello portal de Azure](sql-database-geo-replication-portal.md).

tooconfigure replicación geográfica activa mediante el uso de hello portal de Azure, necesita Hola siguientes recursos:

* Una base de datos de SQL Azure: Hola base de datos principal que desea tooa tooreplicate otra región geográfica.

> [!Note]
Replicación geográfica activa debe estar comprendido entre bases de datos de hello misma suscripción.

## <a name="add-a-secondary-database"></a>Agregar una base de datos secundaria
Hello pasos siguientes crea una nueva base de datos secundaria en una asociación de replicación geográfica.  

tooadd una base de datos secundaria, debe ser propietario de la suscripción de Hola o copropietario.

base de datos secundaria de Hello tiene el mismo nombre como base de datos principal de Hola de Hola y tiene, de forma predeterminada, Hola mismo nivel de servicio. base de datos secundaria de Hello puede ser una sola base de datos o una base de datos en un grupo elástico. Para obtener más información, consulte el artículo sobre [niveles de servicio](sql-database-service-tiers.md).
Después de crear y propagado Hola secundaria, datos comienzan a replicarse de hello base de datos principal toohello nueva base de datos secundaria.

> [!NOTE]
> Si la base de datos de hello asociado ya existe (por ejemplo, como resultado de terminación de una relación de replicación geográfica anterior) Hola comando produce un error.
> 

1. Hola [portal de Azure](http://portal.azure.com), examinar la base de datos de toohello que desea tooset hacia arriba para replicación geográfica.
2. En la página de base de datos SQL de hello, seleccione **georreplicación**y, a continuación, seleccione Hola región toocreate Hola base de datos secundaria. Puede seleccionar una región distinta de región de Hola que hospeda la base de datos principal de hello, pero se recomienda hello [región emparejada](../best-practices-availability-paired-regions.md).
   
    ![Configuración de la replicación geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Seleccione o configurar el servidor de Hola y el nivel de precios para base de datos secundaria de Hola.
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Si lo desea, puede agregar un grupo elástico de base de datos secundaria tooan. toocreate Hola base de datos secundaria un grupo, haga clic en **grupo elástico** y seleccione un grupo en el servidor de destino de Hola. Ya debe existir un grupo en el servidor de destino de Hola. Este flujo de trabajo no crea un grupo.
5. Haga clic en **crear** tooadd Hola secundaria.
6. se crea la base de datos secundaria de Hola y Hola propagación proceso comienza.
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/seeding0.png)
7. Una vez completada Hola proceso de transferencia, base de datos secundaria de hello muestra su estado.
   
    ![Propagación completa](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Inicio de una conmutación por error

base de datos secundaria de Hello puede ser toobecome conmutada Hola principal.  

1. Hola [portal de Azure](http://portal.azure.com), examinar toohello base de datos principal en colaboración de replicación geográfica de Hola.
2. En la hoja de la base de datos SQL de hello, seleccione **toda la configuración de** > **georreplicación**.
3. Hola **secundarias** lista, base de datos de hello seleccione desea toobecome Hola nuevo elemento principal y haga clic en **conmutación por error**.
   
    ![Conmutación por error](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Haga clic en **Sí** conmutación por error de toobegin Hola.

comando de Hello cambia inmediatamente base de datos secundaria de hello en rol principal Hola. 

Hay un breve período durante el cual ambas bases de datos no están disponibles (en orden de Hola de 0 segundos too25) mientras conmutación de roles de Hola. Si la base de datos principal de hello tiene varias bases de datos secundarias, comando hello automáticamente reconfigura Hola otro secundarias tooconnect toohello nuevo elemento principal. toda operación de Hello tardará menos de un minuto toocomplete en circunstancias normales. 

> [!NOTE]
> Este comando está diseñado para una rápida recuperación de base de datos de hello en el caso de una interrupción. Desencadena una conmutación por error sin sincronización de datos (conmutación por error forzada).  Si Hola principal está en línea y confirmación de transacciones cuando se emite el comando de hello alguna pérdida de datos puede producir. 
> 
> 

## <a name="remove-secondary-database"></a>Elimine una base de datos secundaria
Esta operación finaliza permanentemente la base de datos secundaria de hello replicación toohello y cambios Hola rol de base de datos de lectura y escritura normal de hello tooa secundaria. Si se interrumpe la base de datos secundaria de hello conectividad toohello, comando Hola se realiza correctamente pero Hola secundaria hace que no se convierten en lectura y escritura hasta que una vez restaurada la conectividad.  

1. Hola [portal de Azure](http://portal.azure.com), examinar toohello base de datos principal en colaboración de replicación geográfica de Hola.
2. En la página de base de datos SQL de hello, seleccione **georreplicación**.
3. Hola **secundarias** lista, base de datos de hello seleccione desea tooremove de perfil de replicación geográfica de Hola.
4. Haga clic en **Detener replicación**.
   
    ![Quitar secundaria](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Se abrirá una ventana de confirmación. Haga clic en **Sí** base de datos de tooremove Hola de perfil de replicación geográfica de Hola. (Establecer base de datos de lectura y escritura de tooa no forma parte de ninguna replicación.)

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la replicación geográfica activa, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md).
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).

