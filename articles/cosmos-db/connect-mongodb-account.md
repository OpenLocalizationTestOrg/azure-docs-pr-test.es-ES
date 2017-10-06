---
title: "cadena de conexión de aaaMongoDB para una cuenta de base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect su tooan de aplicación de MongoDB base de datos de Azure Cosmos cuenta a través de una cadena de conexión de MongoDB."
keywords: "cadena de conexión de mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Conectar un tooAzure de aplicación de MongoDB Cosmos DB
Obtenga información acerca de cómo tooconnect su tooan de aplicación de MongoDB base de datos de Azure Cosmos cuenta a través de una cadena de conexión de MongoDB. A continuación, puede usar una base de datos de la base de datos de Azure Cosmos como datos de hello almacenar para la aplicación de MongoDB. 

Este tutorial proporciona tooretrieve información de la cadena de conexión de dos maneras:

- [Hola quick start (método)](#QuickstartConnection), para su uso con controladores. NET, Node.js, MongoDB Shell, Java y Python
- [Hola método de cadena de conexión personalizada](#GetCustomConnection), para su uso con otros controladores

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Si no tiene una cuenta de Azure, cree ahora una [cuenta de Azure gratuita](https://azure.microsoft.com/free/). 
- Una cuenta de Azure Cosmos DB. Para obtener instrucciones, consulte [compilar una aplicación web de API de MongoDB con .NET y Hola portal de Azure](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Obtener cadena de conexión de MongoDB hello mediante Inicio rápido de Hola
1. En un explorador de Internet, inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola **base de datos de Azure Cosmos** hoja, seleccione Hola API para la cuenta de MongoDB. 
3. En el panel izquierdo de Hola de hoja de la cuenta de hello, haga clic en **inicio rápido**. 
4. Elija la plataforma (**.NET**, **Node.js**, **Shell de MongoDB**, **Java**, **Python**). Si no ve el controlador o la herramienta en la lista, no se preocupe, documentamos constantemente más fragmentos de código de conexión. Comentar a continuación, en lo que gustaría toosee. toolearn cómo toocraft su propia conexión, leer [obtener información de cadena de conexión de la cuenta de hello](#GetCustomConnection).
5. Copie y pegue el fragmento de código de hello en la aplicación de MongoDB.

    ![Hoja de inicio rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Obtener toocustomize de cadena de conexión de MongoDB Hola
1. En un explorador de Internet, inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola **base de datos de Azure Cosmos** hoja, seleccione Hola API para la cuenta de MongoDB. 
3. En el panel izquierdo de Hola de hoja de la cuenta de hello, haga clic en **cadena de conexión**. 
4. Hola **cadena de conexión** abre la hoja. Tiene todos los Hola información necesarios tooconnect toohello cuenta con un controlador para MongoDB, incluida una cadena de conexión preconstructed.

    ![Hoja Cadena de conexión](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Requisitos de la cadena de conexión
> [!Important]
> Azure Cosmos DB tiene estándares y requisitos de seguridad estrictos. Las cuentas de Azure Cosmos DB requieren autenticación y comunicación segura a través de *SSL*. 
>
>

Base de datos de Azure Cosmos admite Hola MongoDB conexión cadena URI formato estándar, con un par de requisitos específicos: cuentas de base de datos de Azure Cosmos requieren autenticación y comunicación segura mediante SSL. Por lo tanto, el formato de cadena de conexión de hello es:

    mongodb://username:password@host:port/[database]?ssl=true

valores de Hello de esta cadena están disponibles en hello **cadena de conexión** hoja mostrada anteriormente:

* Username (obligatorio): nombre de la cuenta de Azure Cosmos DB.
* Password (obligatorio): contraseña de la cuenta de Azure Cosmos DB.
* Host (obligatorio): el FQDN de la cuenta de base de datos de Azure Cosmos Hola.
* Port (obligatorio): 10255.
* (Opcional) de la base de datos: base de datos de Hola que Hola conexión utiliza. Si no se proporciona ninguna base de datos, base de datos de hello predeterminada es "test".
* ssl=true (obligatorio)

Por ejemplo, considere la posibilidad de cuenta de hello mostrado en hello **cadena de conexión** hoja. Una cadena de conexión válida es:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar MongoChef](mongodb-mongochef.md) con una API de base de datos de Azure Cosmos para cuenta de MongoDB.
* Explorar Hola API de base de datos de Azure Cosmos para MongoDB observando [ejemplos](mongodb-samples.md).
