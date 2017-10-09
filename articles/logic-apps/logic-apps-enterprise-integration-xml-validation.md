---
title: "aaaValidate XML: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Validar XML con esquemas para los escenarios de aplicaciones de la lógica de Azure y B2B mediante Hola paquete de integración empresarial"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Validación de documentos XML para la integración de empresas

A menudo en escenarios de B2B, socios de hello en un acuerdo deben asegurarse que los mensajes de Hola intercambian son válidos para que pueda comenzar el procesamiento de datos. Puede validar documentos con respecto a un esquema predefinido mediante el conector de validación de XML de Hola de uso de Hola Hola paquete de integración empresarial.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Validar un documento con el conector de validación XML Hola

1. Crear una aplicación de lógica, y [vincular la cuenta de toohello de integración de aplicación Hola](../logic-apps/logic-apps-enterprise-integration-accounts.md "Obtenga información acerca de una aplicación de la lógica de la cuenta tooa integración toolink") con esquema Hola desea toouse para validar datos XML.

2. Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. Hola tooadd **validación XML** acción, elija **agregar una acción**.

4. toofilter todos Hola toohello de acciones que desea, escriba *xml* en el cuadro de búsqueda de Hola. Seleccione **XML Validation** (Validación XML).

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Seleccione toospecify Hola contenido XML que desea toovalidate, **contenido**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Seleccionar etiqueta body de hello como contenido que desea toovalidate Hola.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. esquema de hello toospecify desea toouse para validar Hola anterior *contenido* de entrada, elija **nombre de esquema**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Guarde el trabajo  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Con esto, ha terminado de configurar el conector de validación. En una aplicación real, conviene toostore datos de hello validado en una aplicación de línea de negocio (LOB) como SalesForce. toosend Hola tooSalesforce resultado validado, agregar una acción.

tootest su acción de validación, cree un punto de conexión de toohello HTTP de solicitud.

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")   

