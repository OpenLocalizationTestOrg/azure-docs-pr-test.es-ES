---
title: "aaaManage una cuenta de base de datos de Azure Cosmos a través de hello Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage cuenta de la base de datos de Azure Cosmos a través de hello Portal de Azure. Buscar a una guía sobre el uso de hello tooview de Portal de Azure, copia, cuentas de acceso y eliminación."
keywords: Portal de Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>¿Cómo toomanage una cuenta de base de datos de Azure Cosmos
Obtenga información acerca de cómo trabajar con claves tooset coherencia global y eliminar una cuenta de base de datos de Azure Cosmos Hola portal de Azure.

## <a id="consistency"></a>Administración de la configuración de coherencia de Azure Cosmos DB
Seleccionar nivel de coherencia derecho Hola depende de semántica de saludo de la aplicación. Debe familiarizarse con los niveles de coherencia disponibles de hello en base de datos de Azure Cosmos leyendo [utilizando coherencia niveles toomaximize disponibilidad y el rendimiento en la base de datos de Azure Cosmos][consistency]. Azure Cosmos DB ofrece garantías de coherencia, disponibilidad y rendimiento, en cada nivel de coherencia disponible para la cuenta de base de datos. Configurar la cuenta de base de datos con un nivel de coherencia de seguro requiere que los datos sean tooa reducidos sola región de Azure y no está disponible globalmente. En otra parte de Hola, Hola niveles de coherencia no estricta - uso vinculado, session o eventual enable tooassociate cualquier número de regiones de Azure con su cuenta de base de datos. Hola siguiendo los pasos sencillos mostrarle cómo tooselect Hola a nivel de coherencia predeterminada para la cuenta de base de datos. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>coherencia de toospecify Hola predeterminado para una cuenta de base de datos de Azure Cosmos
1. Hola [portal de Azure](https://portal.azure.com/), acceder a su cuenta de base de datos de Azure Cosmos.
2. En la hoja de la cuenta de hello, haga clic en **predeterminado coherencia**.
3. Hola **coherencia predeterminada** hoja, nivel de coherencia de hello seleccione Nuevo y haga clic en **guardar**.
    ![Sesión de coherencia predeterminada][5]

## <a id="keys"></a>Visualización, copia y regeneración de las claves de acceso
Cuando se crea una cuenta de base de datos de Azure Cosmos, servicio de hello genera dos claves de acceso principal que pueden usarse para la autenticación cuando se tiene acceso a la cuenta de base de datos de Azure Cosmos Hola. Al proporcionar dos claves de acceso, base de datos de Azure Cosmos permite claves de hello tooregenerate con ninguna cuenta de base de datos de Azure Cosmos tooyour de interrupción. 

Hola [portal de Azure](https://portal.azure.com/), Hola de acceso **claves** hoja de menú de recursos Hola Hola **cuenta de base de datos de Azure Cosmos** tooview hoja, copiar y regenerar hello las teclas de acceso son tooaccess usa su cuenta de base de datos de Azure Cosmos.

![Captura de pantalla del Portal de Azure, hoja Claves](./media/manage-account/keys.png)

> [!NOTE]
> Hola **claves** hoja también incluye principal y las cadenas de conexión secundaria que pueden ser utilizados tooconnect tooyour cuenta de hello [herramienta de migración de datos](import-data.md).
> 
> 

Las claves de solo lectura también están disponibles en esta hoja. Las lecturas y consultas son operaciones de solo lectura, mientras que las operaciones de creación, eliminación y reemplazo no lo son.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Copiar una tecla de acceso en hello Portal de Azure
En hello **claves** hoja, haga clic en hello **copia** toohello botón derecha de la clave de hello desea toocopy.

![Ver y copiar una tecla de acceso en hello Portal de Azure, hoja de claves](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Regenerar las claves de acceso
Debe cambiar la cuenta de base de datos de Azure Cosmos de tooyour de claves de acceso de hello periódicamente toohelp proteger las conexiones. Dos claves de acceso se asignan tooenable se toomaintain conexiones toohello cuenta de base de datos de Azure Cosmos mediante una clave de acceso mientras regenera Hola otra clave de acceso.

> [!WARNING]
> Volver a generar las claves de acceso afecta a todas las aplicaciones que dependen de la clave actual Hola. Todos los clientes que usan cuenta de base de datos de Azure Cosmos Hola de hello acceso tooaccess clave deben ser clave nueva de hello toouse actualizada.
> 
> 

Si tiene aplicaciones o servicios en la nube con la cuenta de base de datos de Azure Cosmos hello, perderá las conexiones de hello si vuelve a generar las claves, a menos que poner las claves. Hello pasos siguientes describen Hola proceso de distribución de las claves.

1. Actualizar la clave de acceso de hello en su clave de acceso secundaria de hello tooreference aplicación de código de hello cuenta de base de datos de Azure Cosmos.
2. Regenerar clave de acceso principal de Hola para su cuenta de base de datos de Azure Cosmos. Hola [Portal de Azure](https://portal.azure.com/), acceder a su cuenta de base de datos de Azure Cosmos.
3. Hola **cuenta de base de datos de Azure Cosmos** hoja, haga clic en **claves**.
4. En hello **claves** hoja, haga clic en botón regenerar hello, a continuación, haga clic en **Aceptar** tooconfirm que desea toogenerate una nueva clave.
    ![Regenerar las claves de acceso](./media/manage-account/regenerate-keys.png)
5. Una vez que haya comprobado esa clave nueva Hola está disponible para su uso (aproximadamente 5 minutos después de la regeneración), actualice la clave de acceso de hello en su aplicación código tooreference Hola nueva clave de acceso principal.
6. Regenerar clave de acceso secundaria de Hola.
   
    ![Regenerar las claves de acceso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Puede tardar varios minutos antes de que una clave recién generada puede ser tooaccess usa su cuenta de base de datos de Azure Cosmos.
> 
> 

## <a name="get-hello--connection-string"></a>Obtener la cadena de conexión de Hola
tooretrieve la conexión de cadena, hello siguientes: 

1. Hola [portal de Azure](https://portal.azure.com), acceder a su cuenta de base de datos de Azure Cosmos.
2. En el menú de recursos de hello, haga clic en **claves**.
3. Haga clic en hello **copia** botón siguiente toohello **cadena de conexión principal** o **cadena de conexión secundaria** cuadro. 

Si usas la cadena de conexión de Hola Hola [herramienta de migración de base de datos de base de datos de Azure Cosmos](import-data.md), anexar final de toohello de nombre de base de datos de Hola de cadena de conexión de Hola. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a> Eliminar una cuenta de Azure Cosmos DB
tooremove una base de datos de Azure Cosmos cuenta de hello Portal de Azure que ya no se está usando, nombre de la cuenta de hello en menú contextual y haga clic en **eliminar cuenta**.

![Cuenta de toodelete una base de datos de Azure Cosmos en Hola Portal de Azure](./media/manage-account/deleteaccount.png)

1. Hola [portal de Azure](https://portal.azure.com/), tener acceso a la cuenta de base de datos de Azure Cosmos Hola desea toodelete.
2. En hello **cuenta de base de datos de Azure Cosmos** hoja, haga clic en la cuenta de hello y, a continuación, haga clic en **eliminar cuenta**. 
3. En la hoja de confirmación resultante hello, escriba Hola base de datos de Azure Cosmos tooconfirm de nombre de cuenta que desea que la cuenta de hello toodelete.
4. Haga clic en hello **eliminar** botón.

![Cuenta de toodelete una base de datos de Azure Cosmos en Hola Portal de Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[empezar a trabajar con su cuenta de base de datos de Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
