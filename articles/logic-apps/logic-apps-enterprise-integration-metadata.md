---
title: "integración de aaaManage cuenta artefacto de metadatos: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Agregue o recupere metadatos de artefactos de cuentas de integración para Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Administración de metadatos de artefactos en cuentas de integración para aplicaciones lógicas

Puede definir metadatos personalizados para artefactos en cuentas de integración y recuperar metadatos durante el tiempo de ejecución para su aplicación lógica. Por ejemplo, puede especificar metadatos para artefactos como asociados, acuerdos, esquemas y asignaciones: todos almacenan metadatos usando pares de clave-valor. Actualmente, los artefactos no pueden crear metadatos a través de la interfaz de usuario, pero puede usar las API de REST toocreate metadatos. metadatos de tooadd al crear o seleccionar un partner, contrato o esquema Hola portal de Azure, elija **editar como JSON**. tooretrieve artefacto metadatos en aplicaciones lógicas, puede usar características de búsqueda de artefactos de cuenta de integración de Hola.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Agregar metadatos tooartifacts en cuentas de integración

1. Cree una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md).

2. Agregar una cuenta de integración de tooyour de artefacto, por ejemplo, un [asociado](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [acuerdo](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), o [esquema](logic-apps-enterprise-integration-schemas.md).

3.  Seleccione el artefacto de hello, elija **editar como JSON**y escriba los detalles de los metadatos.

    ![Introducción de los metadatos](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Recuperación de metadatos de artefactos para aplicaciones lógicas

1. Cree una [aplicación lógica](logic-apps-create-a-logic-app.md).

2. Crear un [vínculo desde su cuenta de lógica de aplicación tooyour integración](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. En el Diseñador de la lógica de aplicaciones, agregar un desencadenador como *solicitar* o *HTTP* tooyour aplicación de lógica.

4.  Elija **Paso siguiente** > **Agregar una acción**. Busque una *integración* para poder encontrar y seleccionar **Búsqueda de artefactos de la cuenta de integración**.

    ![Seleccione Búsqueda de artefactos de la cuenta de integración.](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Seleccione hello **tipo de artefacto**y proporcionar hello **nombre del artefacto**.

    ![Seleccione el tipo de artefacto y proporcione el nombre del artefacto.](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Ejemplo: recuperación de metadatos de asociados

Los metadatos del asociado tienen estos detalles de `routingUrl`:

![Búsqueda de metadatos de "routingURL" de asociado](media/logic-apps-enterprise-integration-metadata/image6.png)

1. En su aplicación lógica, agregue su desencadenador, una acción **Cuenta de integración: Búsqueda de artefactos de la cuenta de integración** para su asociado y un **HTTP**.

    ![Agregar el desencadenador, la búsqueda de artefactos y la aplicación de lógica de "HTTP" tooyour](media/logic-apps-enterprise-integration-metadata/image4.png)

2. Hola tooretrieve URI, vaya tooCode vista para la aplicación lógica. La definición de su aplicación lógica debería ser similar a la de este ejemplo:

    ![Buscar lookup](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los contratos](logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
