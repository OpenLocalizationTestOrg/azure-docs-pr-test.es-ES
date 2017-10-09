---
title: aaaMake SQL bases de datos de los usuarios de Azure pila disponible tooyour | Documentos de Microsoft
description: Tutorial tooinstall Hola proveedor de recursos SQL Server y crear ofertas a las que permiten a los usuarios de la pila de Azure crear bases de datos SQL.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a>Asegúrese de bases de datos SQL los usuarios de Azure pila tooyour disponibles

Como administrador de la nube de Azure Stack, puede crear ofertas que permitan a los usuarios (inquilinos) crear bases de datos SQL que se puedan usar con sus aplicaciones en la nube, sitios web y cargas de trabajo. Al proporcionar estos personalizada, a petición, los usuarios de bases de datos en la nube tooyour, puede guardarlos tiempo y recursos. tooset este servicio, tendrá que:

> [!div class="checklist"]
> * Implementar el proveedor de recursos de SQL Server de Hola
> * Creación de una oferta
> * Oferta de prueba Hola

## <a name="deploy-hello-sql-server-resource-provider"></a>Implementar el proveedor de recursos de SQL Server de Hola

proceso de implementación de Hola se describe detalladamente en hello [bases de datos de uso de SQL en el artículo de la pila de Azure](azure-stack-sql-resource-provider-deploy.md)y se compone de hello siguiendo los pasos principales:

1.  [Implementar el proveedor de recursos SQL de hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).
2.  [Comprobar la implementación de hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).
3.  [Proporcionar una capacidad mediante la conexión tooa que hospeda SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).

## <a name="create-an-offer"></a>Creación de una oferta

1.  [Establezca una cuota](azure-stack-setting-quotas.md) y asígnele el nombre *CuotaDeSQLServer*. Seleccione **Microsoft.SQLAdapter** para hello **Namespace** campo.
2.  [Cree un plan](azure-stack-create-plan.md). Asígnele el nombre *TestSQLServerPlan*, seleccione hello **Microsoft.SQLAdapter** servicio, y **SQLServerQuota** cuota.

    > [!NOTE]
    > los usuarios de toolet crear otras aplicaciones, otros servicios pueden ser necesaria en el plan de Hola. Por ejemplo, las funciones de Azure requiere ese plan Hola incluyen hello **almacenamiento de Microsoft** de servicio, mientras que requiere de Wordpress **Microsoft.MySQLAdapter**.
    > 
    >

3.  [Crear una oferta](azure-stack-create-offer.md), asígnele el nombre **TestSQLServerOffer** y seleccione hello **TestSQLServerPlan** plan.

## <a name="test-hello-offer"></a>Oferta de prueba Hola

Ahora que ha implementado el proveedor de recursos de SQL Server de Hola y crear una oferta, puede iniciar sesión como un usuario, suscribirse toohello oferta y crear una base de datos.

### <a name="subscribe-toohello-offer"></a>Suscribirse toohello oferta
1. Inicie sesión en toohello portal de Azure pila (https://portal.local.azurestack.external) como un inquilino.
2. Haga clic en **Obtener una suscripción** y, a continuación, escriba **SuscripciónDePruebaDeSQLServer** en **Nombre para mostrar**.
3. Haga clic en **Seleccionar una oferta** > **OfertaDePruebaDeSQLServer** > **Crear**.
4. Haga clic en **Más servicios** > **Suscripciones** > **SuscripciónDePruebaDeSQLServer** > **Proveedores de recursos**.
5. Haga clic en **registrar** toohello siguiente **Microsoft.SQLAdapter** proveedor.

### <a name="create-a-sql-database"></a>Creación de una base de datos SQL

1. Haga clic en **+** > **Datos y almacenamiento** > **SQL Database**.
2. Los valores predeterminados de deje Hola para campos de hello, o pueden usar estos ejemplos:
    - **Nombre de la base de datos**: SQLdb
    - **Tamaño máximo en MB**: 100
    - **Suscripción**: OfertaDePruebaSQL
    - **Grupo de recursos**: SQL-RG
3. Haga clic en **configuración de inicio de sesión**, escriba las credenciales de base de datos de hello y, a continuación, haga clic en **Aceptar**.
4. Haga clic en **SKU** > seleccione Hola SQL SKU que ha creado para Hola de hospedaje de SQL Server > **Aceptar**.
5. Haga clic en **Crear**.

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Implementar el proveedor de recursos de SQL Server de Hola
> * Creación de una oferta
> * Oferta de prueba Hola

Avanzar toohello siguiente tutorial toolearn cómo para:

> [!div class="nextstepaction"]
> [Asegúrese de web, móviles y los usuarios de tooyour disponibles de aplicaciones de API]( azure-stack-tutorial-app-service.md)

