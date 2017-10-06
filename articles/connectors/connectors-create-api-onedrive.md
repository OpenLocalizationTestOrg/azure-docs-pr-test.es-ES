---
title: "Conector de OneDrive aaaAdd hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de hello OneDrive con parámetros de la API de REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Empezar a trabajar con el conector de hello OneDrive
Conectar tooOneDrive toomanage sus archivos, incluidas la carga, get, elimine los archivos y mucho más. 

Con OneDrive, puede: 

* Crear un flujo de trabajo almacenando archivos en OneDrive o actualizar las archivos que ya tenga en OneDrive. 
* Usar desencadenadores toostart el flujo de trabajo cuando se crea un archivo o se actualiza dentro de su OneDrive.
* Usar acciones toocreate un archivo, eliminar un archivo y mucho más. Por ejemplo, cuando se reciba un nuevo correo electrónico de Office 365 con datos adjuntos (desencadenador), cree un nuevo archivo en OneDrive (acción).

Este tema muestra cómo toouse Hola OneDrive conector en una aplicación de lógica, y también listas Hola acciones y desencadenadores.

toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Conectar tooOneDrive
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio. Una conexión proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, tooconnect tooOneDrive, primero necesita una OneDrive *conexión*. toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess desea tooconnect a. Por lo tanto, con OneDrive, escriba conexión con una Hola Hola credenciales tooyour OneDrive cuenta toocreate.

### <a name="create-hello-connection"></a>Crear conexiones de Hola
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Uso de un desencadenador
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. Desencadenadores "sondean" hello servicio en un intervalo y la frecuencia que desee. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. En la aplicación de la lógica de hello, escriba "onedrive" tooget una lista de los desencadenadores de hello:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Seleccione **Cuando se modifica un archivo**. Si ya existe una conexión, a continuación, seleccione Hola selector Mostrar botón tooselect una carpeta.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Si son toosign solicitada en, escriba el inicio de sesión de hello en conexión de hello toocreate de detalles. [Crear conexiones de hello](connectors-create-api-onedrive.md#create-the-connection) en este tema se enumeran los pasos de Hola. 
   
   > [!NOTE]
   > En este ejemplo, aplicación de lógica de Hola se ejecuta cuando un archivo en la carpeta de Hola que elija se actualiza. resultados de hello toosee de este desencadenador, agregar otra acción que envía un correo electrónico. Por ejemplo, agregar Hola Office 365 Outlook *enviar un correo electrónico* acción que envía por correo electrónico cuando se actualiza un archivo. 

3. Seleccione hello **editar** botón y establezca hello **frecuencia** y **intervalo** valores. Por ejemplo, si desea Hola desencadenador toopoll cada 15 minutos, a continuación, establezca hello **frecuencia** demasiado**minuto**, conjunto hello y **intervalo** demasiado**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.

## <a name="use-an-action"></a>Uso de una acción
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Seleccione el signo más Hola. Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de texto hello, escriba "onedrive" tooget una lista de todas las acciones disponibles Hola.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. En nuestro ejemplo, elija **OneDrive - Crear archivo**. Si ya existe una conexión, a continuación, seleccione hello **ruta de acceso de carpeta** tooput Hola de archivo, escriba Hola **nombre de archivo**y elija hello **contenido del archivo** que desee:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola. [Crear conexiones de hello](connectors-create-api-onedrive.md#create-the-connection) en este tema se describen estas propiedades. 
   
   > [!NOTE]
   > En este ejemplo, creamos un nuevo archivo en una carpeta de OneDrive. Puede utilizar la salida de archivo de otro desencadenador toocreate hello OneDrive. Por ejemplo, agregar Hola Office 365 Outlook *cuando llega un nuevo correo electrónico* desencadenador. A continuación, agregue hello OneDrive *crear archivo* acción que usa Hola datos adjuntos y los campos de tipo de contenido dentro de un archivo nuevo de ForEach toocreate hello en OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.


## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).
