---
title: "aaaLearn cómo toouse Hola conector SFTP en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conecte toosend tooSFTP API y recibir archivos. Puede realizar varias operaciones, como crear, actualizar, obtener o eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Empezar a trabajar con el conector de hello SFTP
Utilice Hola SFTP conector tooaccess un toosend de cuenta SFTP y recibir archivos. Puede realizar varias operaciones, como crear, actualizar, obtener o eliminar archivos.  

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Conectar tooSFTP
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio. Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.  

### <a name="create-a-connection-toosftp"></a>Crear una conexión tooSFTP
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Uso de un desencadenador de SFTP
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

En este ejemplo, Hola **SFTP - cuando se agrega o modifica un archivo** desencadenador es tooinitiate usa un flujo de trabajo de aplicación lógica cuando se agregan a un archivo, o modifica en un servidor SFTP. Agregar una condición que comprueba el contenido de Hola de archivo nuevo o modificado de Hola y hace que un archivo de decisión tooextract Hola si su contenido indica que se debe extraer antes de utilizar el contenido de Hola. Por último, agregue un contenido de hello tooextract de acción de un archivo y colocar el contenido de hello extraído en una carpeta de servidor SFTP de Hola. 

En un ejemplo de la empresa, podría utilizar este toomonitor desencadenador una carpeta SFTP para archivos nuevos que representan los pedidos de los clientes.  A continuación, podría utilizar una acción de conector SFTP, como **obtener el contenido del archivo**, contenido de hello tooget de pedido de Hola para su posterior procesamiento y almacenamiento en una base de datos de pedidos.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Agregar una condición
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Uso de una acción de SFTP
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).
