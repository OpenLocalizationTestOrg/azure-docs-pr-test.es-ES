---
title: datos XML de aaaConvert con transformaciones - Azure Logic Apps | Documentos de Microsoft
description: "Crear transformaciones o mapps tooconvert datos XML entre los formatos de las aplicaciones lógicas mediante el uso de hello SDK de integración de Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Integración de empresas con transformaciones XML
## <a name="overview"></a>Información general
Conector de transformación de integración de Enterprise Hola convierte los datos de un formato de tooanother de formato. Por ejemplo, puede tener un mensaje entrante que contiene la fecha actual en formato de YearMonthDay Hola de Hola. Puede usar un toobe de transformación tooreformat Hola fecha en formato de MonthDayYear Hola.

## <a name="what-does-a-transform-do"></a>¿Para qué sirve una transformación?
Una transformación, que es también se denomina un mapa, consta de un esquema XML de origen (Hola de entrada) y un esquema XML de destino (salida de hello). Puede utilizar diferentes funciones integradas toohelp manipular o controlar datos de hello, tales como manipulaciones de cadena, las asignaciones de condicionales, expresiones aritméticas, formateadores en tiempo de fecha y construcciones en bucle incluso.

## <a name="how-toocreate-a-transform"></a>¿Cómo toocreate una transformación?
Puede crear una asignación de transformación mediante Visual Studio hello [SDK de integración de Enterprise](https://aka.ms/vsmapsandschemas). Cuando haya terminado de crear y probar la transformación de hello, cargar transformación hello en su cuenta de integración. 

## <a name="how-toouse-a-transform"></a>¿Cómo toouse una transformación
Después de cargar Hola/asignación de transformación en la cuenta de integración, puede usarlo toocreate una aplicación lógica. aplicación de lógica de Hello ejecuta las transformaciones siempre que se desencadena la aplicación de la lógica de hello (y no hay contenido de entrada que necesita toobe transformarse).

**Estos es Hola pasos toouse una transformación**:

### <a name="prerequisites"></a>Requisitos previos

* Crear una cuenta de integración y agregar un mapa tooit  

Ahora que ha tenido en cuenta los requisitos previos de hello, es el tiempo toocreate la aplicación lógica:  

1. Crear una aplicación de la lógica y [vincular cuentas de integración de tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "Obtenga información acerca de una aplicación de la lógica de la cuenta tooa integración toolink") que contiene el mapa de Hola.
2. Agregar un **solicitar** aplicación lógica de desencadenador tooyour  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Agregar hello **transformar XML** acción seleccionando primero **agregar una acción**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Escriba la palabra Hola *transformar* en toofilter de cuadro de búsqueda de hello todos Hola toohello acciones uno que desea toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Seleccione hello **transformar XML** acción   
6. Agregar Hola XML **contenido** que transforman. Puede usar cualquier dato XML recibirá en solicitud de hello HTTP como hello **contenido**. En este ejemplo, seleccione el cuerpo de saludo de solicitud HTTP de Hola que desencadenó la aplicación de la lógica de hello.
7. Nombre seleccione Hola de hello **mapa** que desea que la transformación de toouse tooperform Hola. mapa de Hello ya debe estar en su cuenta de integración. En un paso anterior, ya que dio su cuenta de integración del tooyour de acceso de aplicación lógica que contiene la asignación.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Guarde el trabajo  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

En este momento, ya ha terminado de configurar su asignación. En una aplicación real, puede que desee toostore datos de hello transformado en una aplicación de LOB, como SalesForce. Puede transformar fácilmente como una salida de hello toosend de acción de hello tooSalesforce. 

Ahora puede probar su transformación mediante la realización de un punto de conexión HTTP de solicitud toohello.  

## <a name="features-and-use-cases"></a>Características y casos de uso
* transformación Hola creado en un mapa puede ser simple, como copiar un nombre y una dirección de tooanother de un documento. O bien, puede crear transformaciones más complejas con operaciones de asignación del cuadro de Hola.  
* Hay varias operaciones de asignación o funciones a las que se puede acceder fácilmente, por ejemplo, cadenas, funciones de fecha hora, etc.  
* Para hacer una copia de datos directas entre esquemas de Hola. Hola que asignador incluido en hello SDK, esto es tan sencillo como dibujar una línea que conecta elementos Hola Hola esquema de origen con sus homólogos en el esquema de destino de Hola.  
* Al crear un mapa, ver una representación gráfica de mapa de hello, que muestra todas las relaciones de Hola y vínculos que cree.
* Use la característica tooadd un mensaje XML de ejemplo de Hola comprobar asignación. Con un solo clic, puede probar mapa de Hola que creó y ve un resultado de hello generado.  
* Cargue asignaciones que ya existan.  
* Incluye compatibilidad con formato XML de Hola.

## <a name="learn-more"></a>Más información
* [Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  
* [Más información sobre las asignaciones](../logic-apps/logic-apps-enterprise-integration-maps.md "Información sobre las asignaciones de Enterprise Integration")  

