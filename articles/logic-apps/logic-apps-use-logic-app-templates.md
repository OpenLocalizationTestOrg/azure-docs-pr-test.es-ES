---
title: "flujos de trabajo de aaaCreate de plantillas: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Obtener una introducción: crear flujos de trabajo rápidamente mediante el uso de aplicaciones de tooconnect de plantillas de aplicación lógica de Azure e integrar los datos."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Configurar un flujo de trabajo mediante una plantilla precompilada o tooget patrón incluye una rápida introducción

## <a name="what-are-logic-app-templates"></a>¿Qué son las plantillas de aplicaciones lógicas?
Una plantilla de aplicación lógica es una aplicación de lógica pregenerado que puede usar tooquickly empezar a crear su propio flujo de trabajo. 

Estas plantillas es una buena manera toodiscover varios modelos que se pueden compilar usando las aplicaciones lógicas. Puede usar estas plantillas como-es o modificarlos toofit su escenario.

## <a name="overview-of-available-templates"></a>Información general de plantillas disponibles
Hay muchas plantillas disponibles actualmente publicadas en la plataforma de aplicación lógica de Hola. Algunas categorías de ejemplo, así como el tipo de Hola de conectores que se utilizan en ellos, se enumeran a continuación.

### <a name="enterprise-cloud-templates"></a>Plantillas de empresa en la nube
Plantillas que integran Dynamics CRM, Salesforce, Box, Blob de Azure y otros conectores para sus necesidades empresariales en la nube. Entre los ejemplos de lo que se puede hacer con estas plantillas se incluye la organización de sus clientes potenciales y la copia de seguridad de los datos de archivos corporativos.

### <a name="enterprise-integration-pack-templates"></a>Plantillas de Enterprise Integration Pack
Configuraciones de VETER (validar, extraer, transformar, enriquecer, enrutar) canalizaciones, recibir un X12 EDI a través de AS2 de documentos y transformarla tooXML, así como mensajes X12 y AS2 gestionar.

### <a name="protocol-pattern-templates"></a>Plantillas de patrón de protocolo
Estas plantillas constan de aplicaciones lógicas que contienen patrones de protocolo como solicitud-respuesta a través de HTTP así como integraciones a través de FTP y SFTP. Utilícelas tal y como están o como base para crear patrones más complejos de protocolo.  

### <a name="personal-productivity-templates"></a>Plantillas de productividad personal
Patrones toohelp mejorar la productividad personal incluye plantillas que establecer avisos diarios, convierten los elementos de trabajo importante en listas de tareas pendientes y automatizan las tareas largas hacia abajo tooa paso de aprobación de usuario único.

### <a name="consumer-cloud-templates"></a>Plantillas en la nube del consumidor
Plantillas simples que se integran con los servicios de las redes sociales como Twitter, Slack o el correo electrónico, capaces a la larga de reforzar las iniciativas de marketing de las redes sociales. También se incluyen plantillas como la de copia repetitiva que permiten aumentar la productividad mediante el ahorro del tiempo invertido en tareas habitualmente repetitivas. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>¿Cómo toocreate una aplicación lógica mediante una plantilla
vaya tooget iniciado mediante una plantilla de aplicación lógica, en el Diseñador de la aplicación hello lógica. Si está insertando diseñador Hola abriendo una aplicación existente de lógica, aplicación de lógica de Hola se carga automáticamente en la vista del diseñador. Sin embargo, si va a crear una nueva aplicación de lógica, consulte a continuación de pantalla de bienvenida.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

Desde esta pantalla, puede elegir toostart con una aplicación lógica en blanco o una plantilla precompilada. Si selecciona una de las plantillas de hello, se le proporcionará información adicional. En este ejemplo, utilizamos hello *cuando se crea un archivo nuevo en Dropbox, copiarlo tooOneDrive* plantilla.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Si elige la plantilla de hello toouse, basta con seleccionar hello *usar esta plantilla* botón. Se le preguntará toosign en cuentas de tooyour en función de qué plantilla de hello conectores utiliza. O, si ya ha establecido previamente una conexión con estos conectores, puede seleccionar el botón Continuar tal y como se muestra a continuación.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Después de establecer la conexión de Hola y seleccionar *continuar*, aplicación de lógica de Hola se abre en la vista del diseñador.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

En el ejemplo de Hola anterior, como sucede Hola con muchas plantillas, algunos de los campos de propiedades obligatorias de hello pueden debe rellenarse en conectores de hello; Sin embargo, sigue algunas pueden requerir un valor antes de poder tooproperly implementar aplicación de lógica de hello. Si intentas toodeploy sin escribir algunas Hola campos que faltan, se le notificará con un mensaje de error.

Si desea que el Visor de tooreturn toohello plantilla, seleccione hello *plantillas* botón de barra de navegación superior de Hola. Al cambiar el Visor de la plantilla de toohello atrás, perderá cualquier progreso que no haya guardado. Tooswitching anterior en el Visor de plantilla, verá un mensaje de advertencia que informa de esto.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>¿Cómo toodeploy una aplicación lógica creada desde una plantilla
Una vez que ha cargado la plantilla y realiza los cambios que desee, seleccione Hola botón Guardar en la esquina superior izquierda de Hola. Esto permite guardar y publicar la aplicación lógica.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

Si prefiere obtener más información sobre cómo tooadd más pasos en una plantilla de aplicación lógica existente o realizar modificaciones en general, más información, lea [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

