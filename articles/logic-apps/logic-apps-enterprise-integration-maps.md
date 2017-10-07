---
title: aaaTransform XML con XSLT mapas - Azure Logic Apps | Documentos de Microsoft
description: "Agregar que XSLT asigna los datos XML de tootransform con hello paquete de integración empresarial y las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Incorporación de mapas para la transformación de datos XML

Usos de la integración de Enterprise asigna datos XML de tootransform entre los formatos. Un mapa es un documento XML que define los datos de hello en un documento que debería transformarse en otro formato. 

## <a name="why-use-maps"></a>¿Por qué se utilizan las asignaciones?

Suponga que recibe con regularidad B2B pedidos o facturas de un cliente que utiliza el formato YYYMMDD de Hola para las fechas. Sin embargo, en su organización, almacenar fechas en formato MMDDYYY Hola. Puede usar una asignación demasiado*transformar* formato de fecha de hello YYYMMDD en hello MMDDYYY antes de almacenar los detalles de pedido o factura de hello en la base de datos de la actividad del cliente.

## <a name="how-do-i-create-a-map"></a>¿Cómo se crea un mapa?

Puede crear proyectos de integración de BizTalk con hello [paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial hello") para Visual Studio 2015. Posteriormente, puede crear un archivo de mapa de Integration que le permite mostrar en un mapa los elementos entre dos archivos de esquema XML. Después de compilar este proyecto, obtendrá un documento XSLT.

## <a name="how-do-i-add-a-map"></a>¿Cómo se puede agregar un mapa?

1. Hola portal de Azure, seleccione **examinar**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. En el cuadro de búsqueda del filtro de hello, escriba **integración**, a continuación, seleccione **cuentas de integración** desde la lista de resultados de Hola.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Seleccione la cuenta de integración de Hola donde desea que el mapa de hello tooadd.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Seleccione hello **mapas** icono.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Después de abre la hoja de mapas de hello, elija **agregar**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Escriba un **nombre** para el mapa. mapa de hello tooupload de archivos, elija el icono de carpeta de hello en hello derecha de hello **mapa** cuadro de texto. Una vez completado el proceso de carga de hello, elija **Aceptar**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Después de Azure agrega la cuenta de integración de hello mapa tooyour, obtendrá un mensaje en la pantalla que muestra si se ha agregado el archivo de asignación o no. Después de obtener este mensaje, elija hello **mapas** mosaico para que pueda ver Hola recién agregado asignación.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>¿Cómo se puede editar un mapa?

Debe cargar un nuevo archivo de asignación con cambios de Hola que desee. En primer lugar, puede descargar mapa Hola para su edición.

tooupload un mapa nuevo que reemplaza la asignación existente de hello, siga estos pasos.

1. Elija hello **mapas** icono.

2. Después de abre la hoja de mapas de hello, seleccione asignación de Hola que desea tooedit.

3. En hello **mapas** hoja, elija **actualización**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. En el selector de archivos de hello, seleccione archivo de mapa de Hola que desee tooupload, a continuación, seleccione **abiertos**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>¿Cómo toodelete un mapa?

1. Elija hello **mapas** icono.

2. Después de abre la hoja de mapas de hello, seleccione asignación de hello desea toodelete.

3. Elija **Eliminar**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Confirme que desea que el mapa de hello toodelete.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  
* [Más información sobre los contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
* [Más información sobre las transformaciones](logic-apps-enterprise-integration-transform.md "Información sobre las transformaciones de integración empresarial")  

