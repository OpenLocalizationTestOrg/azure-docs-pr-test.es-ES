---
title: "Hola aaaUse conector de servidor de SharePoint en las aplicaciones lógicas | Documentos de Microsoft"
description: "Introducción al uso Hola Hola conector de servidor de SharePoint en las aplicaciones lógicas"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Empezar a trabajar con el conector de SharePoint de Hola
Hola conector de SharePoint proporciona un toowork manera con listas en SharePoint.

Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Crear una conexión tooSharePoint
toouse Hola conector de SharePoint, cree primero un **conexión** especifique los detalles de Hola de estas propiedades: 

| Propiedad | Obligatorio | Descripción |
| --- | --- | --- |
| Se necesita el cifrado de tokens |Sí |Proporcionar credenciales de SharePoint |

tooconnect demasiado**SharePoint**, escriba su tooSharePoint de identidad (nombre de usuario y contraseña, las credenciales de tarjeta inteligente, etc.). Una vez que haya autenticado, puede continuar conector de SharePoint de hello toouse en la aplicación lógica. 

Mientras que en el Diseñador de hello de la aplicación lógica, siga estos pasos toosign en conexión de SharePoint toocreate hello **conexión** para su uso en la aplicación lógica:

1. Escriba SharePoint en el cuadro de búsqueda de Hola y espere Hola búsqueda tooreturn todas las entradas con SharePoint en nombre de hello:   
   ![Configurar SharePoint][1]  
2. Seleccione **SharePoint - Cuando se crea un archivo**   
3. Seleccione **iniciar sesión en tooSharePoint**:   
   ![Configurar SharePoint][2]    
4. Proporcione su toosign de credenciales de SharePoint en tooauthenticate con SharePoint   
   ![Configurar SharePoint][3]     
5. Una vez completa la autenticación de hello estará tooyour redirigida lógica aplicación toocomplete, mediante la configuración de SharePoint **cuando se crea un archivo** cuadro de diálogo.          
   ![Configurar SharePoint][4]  
6. A continuación, puede agregar otros desencadenadores y las acciones que necesita toocomplete la aplicación lógica.   
7. Guarde su trabajo mediante la selección **guardar** en la barra de menús de hello anterior.  

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sharepoint/).

## <a name="more-connectors"></a>Más conectores
Volver atrás toohello [lista de las API](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
