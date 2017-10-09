---
title: "Conector de Outlook de Office 365 aaaAdd hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Crear aplicaciones lógicas con interacción de tooenable de conector de Office 365 con Office 365. Por ejemplo: crear, editar y actualizar contactos y elementos de calendario."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Empezar a trabajar con el conector de Outlook de Office 365 Hola
Conector de Outlook de Office 365 Hola permite la interacción con Outlook en Office 365. Usar este conector toocreate, editar y actualizar contactos y elementos de calendario y también obtener, enviar y responder a tooemail.

Con Office 365 Outlook:

* Compilar el flujo de trabajo mediante las características de correo electrónico y el calendario de hello en Office 365. 
* Utilice desencadenadores toostart el flujo de trabajo cuando se produce un nuevo correo electrónico cuando se actualiza un elemento de calendario y mucho más.
* Usar acciones toosend un correo electrónico, cree un nuevo evento de calendario y mucho más. Por ejemplo, cuando hay un nuevo objeto de Salesforce (un desencadenador), envíe un correo electrónico tooyour Outlook de Office 365 (acción). 

Este tema muestra cómo toouse Hola conector de Outlook de Office 365 en una aplicación de lógica, y también listas Hola acciones y desencadenadores.

> [!NOTE]
> Esta versión de Hola artículo aplica tooLogic aplicaciones de la disponibilidad general (GA).
> 
> 

toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Conectar tooOffice 365
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio. Una conexión proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, tooconnect tooOffice 365 Outlook, primero debe Office 365 *conexión*. toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess desea tooconnect a. Por lo que con Office 365 Outlook, escriba Hola credenciales tooyour conexión de Hola de toocreate de cuenta de Office 365.

## <a name="create-hello-connection"></a>Crear conexiones de Hola
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Uso de un desencadenador
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. Desencadenadores "sondean" hello servicio en un intervalo y la frecuencia que desee. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. En la aplicación de la lógica de hello, escriba "office 365" tooget una lista de los desencadenadores de hello:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Seleccione **Office 365 Outlook - Cuando un evento próximo va a comenzar pronto**. Si ya existe una conexión, a continuación, seleccione un calendario de la lista desplegable de Hola.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Si son toosign solicitada en, escriba el inicio de sesión de hello en conexión de hello toocreate de detalles. [Crear conexiones de hello](connectors-create-api-office365-outlook.md#create-the-connection) en este tema se enumeran los pasos de Hola. 
   
   > [!NOTE]
   > En este ejemplo, la aplicación de lógica de Hola se ejecuta cuando se actualiza un evento de calendario. resultados de hello toosee de este desencadenador, agregar otra acción que envía un mensaje de texto. Por ejemplo, agregar hello Twilio *enviar mensaje* acción que se está iniciando textos cuando hello eventos de calendario en 15 minutos. 
   > 
   > 
3. Seleccione hello **editar** botón y establezca hello **frecuencia** y **intervalo** valores. Por ejemplo, si desea Hola desencadenador toopoll cada 15 minutos, a continuación, establezca hello **frecuencia** demasiado**minuto**, conjunto hello y **intervalo** demasiado**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.

## <a name="use-an-action"></a>Uso de una acción
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Seleccione el signo más Hola. Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de texto hello, escriba "office 365" tooget una lista de todas las acciones disponibles Hola.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. En nuestro ejemplo, elija **Office 365 Outlook - Crear contacto**. Si ya existe una conexión, a continuación, elija hello **Id. de la carpeta**, **nombre dado**y otras propiedades:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola. [Crear conexiones de hello](connectors-create-api-office365-outlook.md#create-the-connection) en este tema se describen estas propiedades. 
   
   > [!NOTE]
   > En este ejemplo, creamos un nuevo contacto en Office 365 Outlook. Se puede usar la salida de otro desencadenador toocreate Hola póngase en contacto con. Por ejemplo, agregar Hola SalesForce *cuando se crea un objeto* desencadenador. A continuación, agregue Hola Office 365 Outlook *crear contacto* acción que usa Hola SalesForce campos toocreate Hola nueva nuevo contacto en Office 365. 
   > 
   > 
5. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/office365connector/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).

