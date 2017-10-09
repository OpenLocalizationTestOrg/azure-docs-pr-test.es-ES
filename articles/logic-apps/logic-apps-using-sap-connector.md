---
title: aaaConnect tooan sistema SAP en Azure Logic Apps local | Documentos de Microsoft
description: "Conectar sistema SAP de tooan locales del flujo de trabajo de aplicación lógica a través de puerta de enlace de datos de hello en local"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Conectar sistema SAP de tooan local desde las aplicaciones lógicas con el conector de SAP de Hola 

puerta de enlace de datos de Hello local permite toomanage datos y obtener acceso seguro a recursos que son locales. Este tema muestra cómo puede conectarse el sistema SAP local de lógica aplicaciones tooan. En este ejemplo, la aplicación lógica solicita un IDOC a través de HTTP y envía la respuesta Hola.    

> [!NOTE]
> Limitaciones actuales: 
> - La aplicación lógica agota el tiempo si no finalizan todos los pasos necesarios para la respuesta de hello en hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md). En este escenario, las solicitudes pueden quedar bloqueadas. 
> - Selector de archivos de Hello no muestra todos los campos disponibles de Hola. En este escenario, puede agregar manualmente rutas de acceso.

## <a name="prerequisites"></a>Requisitos previos

- Instalar y configurar hello más reciente [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127) versión 1.15.6150.1 o posterior. [Cómo tooconnect toohello local puerta de enlace de datos en una aplicación de lógica](http://aka.ms/logicapps-gateway) listas Hola pasos. puerta de enlace de Hello debe instalarse en un equipo local para poder continuar.

- Descarga y la biblioteca de cliente SAP más reciente de instalación de hello en hello misma máquina donde se instaló la puerta de enlace de datos de Hola. Use cualquiera de hello después de las versiones SAP: 
    - SAP Server
        - Cualquier servidor de SAP que Hola de soporte técnico de .NET Connector (NCo) 3.0
 
    - SAP Client
        - SAP .NET Connector (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Agregar desencadenadores y acciones para conectar el sistema SAP tooyour

Conector de SAP de Hello tiene acciones, pero no los desencadenadores. Por lo tanto, tenemos toouse otro desencadenador en el inicio de Hola de flujo de trabajo de Hola. 

1. Agregar desencadenador de solicitud/respuesta de hello y, a continuación, seleccione **nuevo paso**.

2. Seleccione **agregar una acción**y, a continuación, seleccione el conector de SAP de hello escribiendo `SAP` en el campo de búsqueda de hello:    

     ![Seleccione el servidor de aplicaciones de SAP o el servidor de mensajes de SAP.](media/logic-apps-using-sap-connector/sap-action.png)

3. Seleccione el [**servidor de aplicaciones de SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o el [**servidor de mensajes de SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), según la configuración de SAP. Si no tiene una conexión existente, son toocreate solicitada uno.

   1. Seleccione **conectar a través de puerta de enlace de datos local**y escriba los detalles de hello para el sistema SAP:   

       ![Agregar tooSAP de cadena de conexión](media/logic-apps-using-sap-connector/picture2.png)  

   2. En **puerta de enlace**, seleccione una puerta de enlace existente o tooinstall una nueva puerta de enlace, seleccione **instalar la puerta de enlace**.

        ![Instalación de una nueva puerta de enlace](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Después de escribir todos los detalles de hello, seleccione **crear**. 
   Lógica de aplicaciones se configura y comprueba la conexión de hello, asegurándose de que la conexión de hello funciona correctamente.

4. Escriba un nombre para la conexión SAP.

5. Ahora hay disponibles distintas opciones de SAP de Hola. toofind la categoría de IDOC, seleccione uno de la lista de Hola. O escriba manualmente en la ruta de acceso de Hola y respuesta de hello seleccione HTTP en hello **cuerpo** campo:

     ![Acción de SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Agregar acción de hello para la creación de un **respuesta HTTP**. mensaje de bienvenida de respuesta debe ser de salida de hello SAP.

7. Guarde la aplicación lógica. Probarla mediante el envío de un IDOC a través de la dirección URL de desencadenador de hello HTTP. Después de Hola que se envía el IDOC, esperar respuesta de Hola de aplicación lógica de hello:   

     > [!TIP]
     > Consulte cómo demasiado[supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Ahora que el conector de SAP de Hola se agrega la aplicación de la lógica de tooyour, empezar a explorar otras funcionalidades:

- BAPI
- RFC

## <a name="get-help"></a>Obtener ayuda

tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo toovalidate, transformación y otras funciones de BizTalk similar en hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Conectar datos locales tooon](../logic-apps/logic-apps-gateway-connection.md) desde las aplicaciones lógicas
