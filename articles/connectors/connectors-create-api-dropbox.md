---
title: "Conector de aaaDropbox en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conectar tooDropbox toomanage los archivos. En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Empezar a trabajar con el conector de Dropbox Hola
Conectar tooDropbox toomanage los archivos. En Dropbox, puede realizar diversas acciones, como cargar, actualizar, obtener y eliminar archivos.

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Puede empezar [creando una aplicación lógica ahora](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Conectar tooDropbox
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio. Una conexión proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, en orden tooconnect tooDropbox, primero necesita una lista desplegable *conexión*. toocreate una conexión, tendría las credenciales de hello tooprovide que suele usar el servicio de hello tooaccess a que desea tooconnect. Por lo tanto, en el ejemplo de Hola a Dropbox, necesitaría Hola credenciales tooyour cuenta de Dropbox en orden toocreate Hola conexión tooDropbox. [Más información sobre las conexiones]()

### <a name="create-a-connection-toodropbox"></a>Crear una conexión tooDropbox
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Uso de un desencadenador de Dropbox
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

En este ejemplo, usaremos hello **cuando se crea un archivo** desencadenador. Cuando se produce este desencadenador, llamaremos a hello **obtener el contenido del archivo con la ruta de acceso** acción Dropbox. 

1. Escriba *dropbox* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de la lógica de hello, a continuación, seleccione hello **Dropbox - cuando se crea un archivo** desencadenador.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Seleccione la carpeta de hello en el que desea tootrack creación del archivo. Seleccione... (identificado en el cuadro de hello rojo) y examinar las carpetas toohello desea tooselect de desencadenador de hello de la entrada.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Uso de una acción de Dropbox
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Ahora que hello desencadenador se ha agregado, siga estas tooadd pasos una acción que se obtendrá el contenido del archivo nuevo de Hola.

1. Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando se crea un nuevo archivo.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Seleccione **Add an action**(Agregar una acción). Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Escriba *dropbox* toosearch para acciones relacionadas tooDropbox.  
4. Seleccione **Dropbox - obtener contenido del archivo con la ruta de acceso** como Hola tootake acción cuando se crea un nuevo archivo en hello seleccionado la carpeta de Dropbox. se abre el bloque de control de acción de Hola. También será solicitada tooauthorize su tooaccess de aplicación lógica su Dropbox cuenta si aún no lo hecho previamente.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Seleccione... (situado en el lado derecho de Hola de hello **ruta de acceso del archivo** control) y busque la ruta de acceso del archivo toohello le gustaría toouse. O bien, use hello **ruta de acceso de archivo** toospeed símbolo (token) de la creación de aplicación lógica.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Guarde su trabajo y crear un nuevo archivo en Dropbox tooactivate el flujo de trabajo.  

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/dropbox/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).
