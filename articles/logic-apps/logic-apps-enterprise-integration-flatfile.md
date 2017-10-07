---
title: "aaaEncode o descodificar archivos planos de las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "¿Cómo toouse Hola codificador de archivo del archivo o el descodificador Hola paquete de integración empresarial en las aplicaciones lógicas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Información general sobre Enterprise Integration Pack con archivos sin formato

Puede que desee tooencode XML contenido antes de enviarlo a socio comercial de tooa en un escenario de negocio a negocio (B2B). En una aplicación de lógica, puede usar archivos planos Hola codificación conector toodo esto. Hello aplicación lógica que cree puede obtener su XML contenido desde una variedad de orígenes, incluyendo desde un desencadenador de la solicitud HTTP, desde otra aplicación o incluso desde uno de Hola muchas [conectores](../connectors/apis-list.md). Para obtener más información acerca de las aplicaciones lógicas, consulte hello [documentación de aplicaciones de la lógica](logic-apps-what-are-logic-apps.md "obtener más información sobre las aplicaciones lógicas").  

## <a name="create-hello-flat-file-encoding-connector"></a>Crear el conector de codificación de archivo sin formato de Hola
Siga estos pasos tooadd una codificación de aplicación lógica de conector tooyour de archivos sin formato.

1. Crear una aplicación de la lógica y [vincular cuentas de integración de tooyour](logic-apps-enterprise-integration-accounts.md "Obtenga información acerca de una aplicación de la lógica de la cuenta tooa integración toolink"). Esta cuenta contiene esquema Hola utilizará tooencode Hola datos XML.  
2. Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.  
   ![Captura de pantalla de tooselect de desencadenador](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Agregue archivos planos Hola codificación acción, como se indica a continuación:
   
    a. Seleccione hello **más** inicio de sesión.
   
    b. Seleccione hello **agregar una acción** vínculo (aparece después de haber seleccionado hello además de inicio de sesión).
   
    c. En el cuadro de búsqueda de hello, escriba ** toofilter todos Hola toohello acciones uno que desea toouse.
   
    d. Seleccione hello **la codificación de archivo sin formato** opción de lista de Hola.   
   ![Captura de pantalla de la opción Codificación de archivo plano](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. En hello **la codificación de archivo sin formato** cuadro de diálogo, seleccione hello **contenido** cuadro de texto.  
   ![Captura de pantalla del cuadro de texto Contenido](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Seleccionar etiqueta body de hello como contenido que desea tooencode Hola. etiquetas de cuerpo de Hello rellenará el campo contenido Hola.     
   ![Captura de pantalla de la etiqueta Cuerpo](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Seleccione hello **nombre de esquema** cuadro de lista y elija el contenido de la entrada de esquema de hello desea toouse tooencode Hola.    
   ![Captura de pantalla del cuadro de lista Nombre de esquema](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Guarde el trabajo.   
   ![Captura de pantalla del icono Guardar](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

En este momento, ya ha terminado de configurar su conector de codificación de archivos sin formato. En una aplicación real, puede que desee toostore datos de hello codificado en una aplicación de línea de negocio, como Salesforce. O bien, puede enviar esa tooa datos codificados socio comercial. Puede agregar fácilmente una salida de hello toosend de acción de hello codificación acción tooSalesforce o tooyour socio comercial, usando cualquiera de hello otros conectores proporcionados.

Ahora puede probar el conector, un punto de conexión HTTP de solicitud toohello y, incluido el contenido XML de hello en el cuerpo de saludo de solicitud de Hola.  

## <a name="create-hello-flat-file-decoding-connector"></a>Crear archivos planos Hola descodificación de conector

> [!NOTE]
> toocomplete estos pasos, debe toohave un archivo de esquema ya cargado en la cuenta de integración.

1. Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.  
   ![Captura de pantalla de tooselect de desencadenador](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Agregue archivos planos Hola descodificación acción, como se indica a continuación:
   
    a. Seleccione hello **más** inicio de sesión.
   
    b. Seleccione hello **agregar una acción** vínculo (aparece después de haber seleccionado hello además de inicio de sesión).
   
    c. En el cuadro de búsqueda de hello, escriba ** toofilter todos Hola toohello acciones uno que desea toouse.
   
    d. Seleccione hello **descodificación de archivo sin formato** opción de lista de Hola.   
   ![Captura de pantalla de la opción Descodificación de archivo plano](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Seleccione hello **contenido** control. Esto genera una lista de contenido de Hola de los anteriores pasos que puede usar como toodecode contenido Hola. Tenga en cuenta que hello *cuerpo* de hello solicitud HTTP de entrada está disponible toobe usa como Hola toodecode contenido. También puede escribir toodecode contenido Hola directamente en hello **contenido** control.     
4. Seleccione hello *cuerpo* etiqueta. Aviso Hola cuerpo se encuentra ahora en hello **contenido** control.
5. Seleccione el nombre de hello del esquema de Hola que desea que el contenido de toouse toodecode Hola. Hello captura de pantalla siguiente muestra que *OrderFile* es el nombre de esquema seleccionado Hola. Este nombre de esquema tenía se ha cargado previamente en la cuenta de hello de integración.
   
   ![Captura de pantalla del cuadro de diálogo Descodificación de archivo plano](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Guarde el trabajo.  
   ![Captura de pantalla del icono Guardar](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

En este momento, ya ha terminado de configurar su conector de descodificación de archivos sin formato. En una aplicación real, puede que desee toostore datos de hello descodificado en una aplicación de línea de negocio, como Salesforce. Puede agregar fácilmente una salida de hello toosend de acción de hello descodificación tooSalesforce de acción.

Ahora puede probar su conector mediante la realización de un punto de conexión HTTP de solicitud toohello e incluido el contenido XML de hello desea toodecode en el cuerpo de saludo de solicitud de Hola.  

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial").  

