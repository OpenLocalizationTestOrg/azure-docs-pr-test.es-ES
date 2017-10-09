---
title: "aaaSchemas para la validación de XML: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Validación de documentos XML con esquemas para Azure Logic Apps y Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Validar XML con esquemas de hello paquete de integración empresarial y las aplicaciones lógicas de Azure

Esquemas confirmación que documentos XML de hello que recibirá son válidos y que han Hola esperado datos en un formato predefinido. Los esquemas también ayudan a validar los mensajes que se intercambian en un escenario B2B.

## <a name="add-a-schema"></a>Agregar un esquema

1. Hola portal de Azure, seleccione **más servicios**.

    ![Azure Portal, "Más servicios"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. En el cuadro de búsqueda del filtro de hello, escriba **integración**y seleccione **cuentas de integración** desde la lista de resultados de Hola.

    ![Cuadro de búsqueda](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Seleccione hello **cuenta integración** donde desea que el esquema de hello tooadd.

    ![Lista de cuentas de integración](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Elija hello **esquemas** icono.

    ![Cuenta de integración de ejemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Incorporación de un archivo de esquema inferior a 2 MB

1. Hola **esquemas** hoja que se abre (de Hola pasos anteriores), elija **agregar**.

    ![Hoja de esquemas, "Agregar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Escriba un nombre para el esquema. Cargar archivo de esquema de hello seleccionando el icono de carpeta hello toohello siguiente **esquema** cuadro. Una vez completado el proceso de carga de hello, seleccione **Aceptar**.

    ![Captura de pantalla de "Agregar esquema" con "Archivo pequeño" resaltado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Agregar un archivo de esquema superior a 2 MB (arriba too8 MB como máximo)

Estos pasos varían en función de nivel de acceso de contenedor de blob de hello: **público** o **ningún acceso anónimo**.

**toodetermine este nivel de acceso**

1.  Abra el **Explorador de Azure Storage**. 

2.  En **contenedores de blobs**, seleccione contenedor de blobs de Hola que desee. 

3.  Seleccione **Seguridad**, **Nivel de acceso**.

Si es el nivel de acceso de seguridad de blob de hello **público**, siga estos pasos.

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Público" resaltados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Cargar la cuenta de almacenamiento de hello esquema tooyour y copie Hola URI.

    ![Cuenta de almacenamiento con URI resaltado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. En **Agregar esquema**, seleccione **archivo grande**y proporcionar Hola URI Hola **contenido URI** cuadro de texto.

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Si es el nivel de acceso de seguridad de blob de hello **ningún acceso anónimo**, siga estos pasos.

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Sin acceso anónimo" resaltados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Cargar la cuenta de almacenamiento de hello esquema tooyour.

    ![Cuenta de almacenamiento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Generar una firma de acceso compartido para el esquema de Hola.

    ![Cuenta de almacenamiento con la ficha firmas de acceso compartido resaltada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. En **Agregar esquema**, seleccione **archivo grande**y proporcione la firma de acceso compartido de hello URI Hola **contenido URI** cuadro de texto.

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. Hola **esquemas** hoja de la cuenta de integración, debe aparecer en el esquema recién agregado.

    ![La cuenta de integración, con "Esquemas" y el esquema nuevo de hello resaltado](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Editar esquemas

1. Elija hello **esquemas** icono.

2. Después de hello **esquemas** hoja se abre, esquema de hello select que desea tooedit.

3. En hello **esquemas** hoja, elija **editar**.

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Archivo de esquema de hello SELECT que desee tooedit, a continuación, seleccione **abiertos**.

    ![Abrir esquema archivo tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure muestra un mensaje que Hola esquema se cargó correctamente.

## <a name="delete-schemas"></a>Eliminar esquemas

1. Elija hello **esquemas** icono.

2. Después de hello **esquemas** hoja se abre, esquema de hello seleccione desea toodelete.

3. En hello **esquemas** hoja, elija **eliminar**.

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm que desea toodelete Hola selecciona esquema, elija **Sí**.

    ![Mensaje de confirmación para "Eliminar esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    Hola **esquemas** hoja, la lista de esquemas de hello actualiza y ya no incluye el esquema de Hola que eliminó.

    ![La cuenta de integración con "Esquemas" resaltado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial hello").  

