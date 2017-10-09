---
title: "Hola aaaUse conector demora en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar tooSlack en las aplicaciones lógicas"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Empezar a trabajar con conector demora Hola
Slack es una herramienta de comunicación de equipo, que reúne todas las comunicaciones del equipo en un solo lugar, inmediatamente localizables y disponibles dondequiera que vaya. 

Empiece por crear una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Crear una conexión tooSlack
Conector de demora de hello toouse, cree primero un **conexión** especifique los detalles de Hola de estas propiedades: 

| Propiedad | Obligatorio | Descripción |
| --- | --- | --- |
| Se necesita el cifrado de tokens |Sí |Proporcionar credenciales de Slack |

Siga estos pasos toosign en Slack y la configuración de hello completa de hello demora **conexión** en la aplicación lógica:

1. Seleccione **Periodicidad**
2. Seleccione un valor para **Frequency** (Frecuencia) y especifique el correspondiente a **Interval** (Intervalo)
3. Seleccione **Add an action**(Agregar una acción)  
   ![Configurar Slack][1]  
4. Escriba demora en el cuadro de búsqueda de Hola y espere Hola búsqueda tooreturn todas las entradas con demora en nombre de Hola
5. Seleccione **Slack - exponer mensaje**
6. Seleccione **iniciar sesión en tooSlack**:  
   ![Configurar Slack][2]
7. Proporcione su toosign credenciales demora en la aplicación de hello tooauthorize    
   ![Configurar Slack][3]  
8. Podrá registro de la organización tooyour redirigida en la página. **Autorizar** toointeract demora con la aplicación lógica:      
   ![Configurar Slack][5] 
9. Una vez completa la autorización de hello estará tooyour redirigida lógica aplicación toocomplete, mediante la configuración de hello **una demora: obtener todos los mensajes** sección. Agregue otros desencadenadores y acciones que necesite.  
   ![Configurar Slack][6]
10. Guarde su trabajo mediante la selección **guardar** en la barra de menús de hello anterior.

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/slack/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
