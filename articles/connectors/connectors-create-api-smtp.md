---
title: "Conector de aaaSMTP en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conecte el correo electrónico de toosend tooSMTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Empezar a trabajar con el conector SMTP de Hola
Conecte el correo electrónico de toosend tooSMTP.

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Conectar tooSMTP
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio. Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, tooconnect tooSMTP, primero debe SMTP *conexión*. toocreate una conexión, escriba las credenciales de Hola que suele usar tooaccess se conectan a un servicio de Hola. Por lo tanto, en el ejemplo de Hola SMTP, escriba nombre de la conexión de hello credenciales tooyour, dirección del servidor SMTP y tooSMTP de conexión de usuario inicio de sesión información toocreate Hola.  

### <a name="create-a-connection-toosmtp"></a>Crear una conexión tooSMTP
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Uso de un desencadenador de SMTP
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

En este ejemplo, dado que SMTP no tiene un desencadenador de su propio, usaremos hello **Salesforce - cuando se crea un objeto** desencadenador. Este desencadenador se activa al crear un objeto en Salesforce. En nuestro ejemplo, configuraremos lo modo que cada vez que se crea un nuevo cliente potencial en Salesforce, un *enviar correo electrónico* acción tiene lugar mediante el conector de hello SMTP con una notificación de hello nuevo cliente potencial que se está creando.

1. Escriba *salesforce* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **Salesforce - cuando se crea un objeto** desencadenador.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Hola **cuando se crea un objeto** se muestra el control.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Seleccione hello **tipo de objeto** , a continuación, seleccione *provocar* de lista de Hola de objetos. En este paso está indicando que va a crear un desencadenador que enviará una notificación a su aplicación lógica cada vez que se cree un nuevo cliente potencial en Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. se ha creado el desencadenador de Hola.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Uso de una acción de SMTP
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Ahora que hello desencadenador se ha agregado, siga estos acción de tooadd SMTP de pasos que se produce cuando se crea un nuevo cliente potencial en Salesforce.

1. Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando se crea un nuevo cliente potencial.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Seleccione **Add an action**(Agregar una acción). Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Escriba *smtp* toosearch para acciones relacionadas tooSMTP.  
4. Seleccione **SMTP - enviar correo electrónico** como Hola tootake acción cuando se crea el nuevo cliente potencial de Hola. se abre el bloque de control de acción de Hola. Tendrá tooestablish la conexión de smtp en el bloque de diseñador Hola si aún no lo hecho previamente.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Entrada de la información de correo electrónico deseado en hello **SMTP - enviar correo electrónico** bloque.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Guardar su trabajo en orden tooactivate el flujo de trabajo.  

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).
