---
title: aaaUse Robomongo para la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Robomongo con una base de datos de Azure Cosmos: API de MongoDB cuenta"
keywords: Robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Uso de Robomongo con una cuenta de Azure Cosmos DB: API para MongoDB
tooconnect tooan base de datos de Azure Cosmos: API de cuenta de MongoDB utilizando Robomongo, debe:

* Descargar e instalar [Robomongo](https://robomongo.org/)
* Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB

## <a name="connect-using-robomongo"></a>Conectarse mediante Robomongo
tooadd la base de datos de Azure Cosmos: API de MongoDB cuenta toohello Robomongo MongoDB conexiones, realizar Hola pasos.

1. Recuperar la base de datos de Azure Cosmos: API para obtener información de conexión de cuenta MongoDB utilizando instrucciones de hello [aquí](connect-mongodb-account.md).

    ![Captura de pantalla de hoja de cadena de conexión de Hola](./media/mongodb-robomongo/connectionstringblade.png)
2. Ejecute *Robomongo.exe*.

3. Haga clic en el botón de conexión de hello en **archivo** toomanage las conexiones. A continuación, haga clic en **crear** en hello **las conexiones de MongoDB** ventana, que se abrirá hello **configuración de conexión** ventana.

4. Hola **configuración de conexión** ventana, elija un nombre. A continuación, busque hello **Host** y **puerto** de la información de conexión en el paso 1 y escribirlos en **dirección** y **puerto**, respectivamente .

    ![Captura de pantalla de hello Robomongo administrar conexiones](./media/mongodb-robomongo/manageconnections.png)
5. En hello **autenticación** , haga clic en **realizar autenticación**. Después, escriba la base de datos (el valor predeterminado es *Admin*), el **nombre de usuario** y la **contraseña**.
Tanto el **nombre de usuario** como la **contraseña** están en la información de conexión del paso 1.

    ![Captura de pantalla de hello Robomongo ficha de autenticación](./media/mongodb-robomongo/authentication.png)
6. En hello **SSL** ficha, verificación **usar protocolo SSL**, a continuación, cambie hello **método de autenticación** demasiado**certificado autofirmado**.

    ![Captura de pantalla de hello Robomongo SSL pestaña](./media/mongodb-robomongo/SSL.png)
7. Por último, haga clic en **prueba** tooverify que es capaz de tooconnect, a continuación, **guardar**.

## <a name="next-steps"></a>Pasos siguientes
* Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.
