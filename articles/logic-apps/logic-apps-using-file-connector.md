---
title: "local tooon aaaConnect sistema de archivos de las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar sistemas de archivos local tooon del flujo de trabajo de aplicación lógica a través de puerta de enlace de datos de hello en local y el conector de sistema de archivos"
keywords: Sistemas de archivos
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Conectar sistemas de archivos local tooon desde las aplicaciones lógicas con el conector del sistema de archivos de Hola

Conectividad de nube híbrida es aplicaciones toologic central, por lo que toomanage datos y segura acceso a recursos locales, las aplicaciones lógicas pueden usar la puerta de enlace de datos de hello en local. En este artículo, le mostramos cómo tooconnect tooan local sistema de archivos con un escenario básico: copiar un archivo que tooa tooDropbox cargado recurso compartido de archivos, a continuación, envíe un correo electrónico.

## <a name="prerequisites"></a>Requisitos previos

- Instalar y configurar hello más reciente [puerta de enlace de datos local](https://www.microsoft.com/download/details.aspx?id=53127).
- Instalar hello más reciente local data gateway, versión 1.15.6150.1 o superior. [Conectar la puerta de enlace de datos de toohello local](http://aka.ms/logicapps-gateway) listas Hola pasos. puerta de enlace de Hello debe instalarse en un equipo local para poder continuar con el resto de Hola de pasos de Hola.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Agregar desencadenadores y acciones para conectar el sistema de archivos tooyour

1. Cree una aplicación de la lógica y agregue el desencadenador **Dropbox - Cuando se crea un archivo**. 
2. En el desencadenador de hello, elija **paso siguiente** > **agregar una acción**. 
3. En el cuadro de búsqueda de hello, escriba `file system` para que pueda ver todos los admitidos acciones para el conector de sistema de archivos de Hola.

   ![Conector Buscar archivo](media/logic-apps-using-file-connector/search-file-connector.png)

2. Elija hello **crear archivo** acción y crear un sistema de archivos de conexión tooyour.

   Si no tiene una conexión existente, son toocreate solicitada uno.

   1. Seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local). Aparecen más propiedades.
   2. Seleccione la carpeta raíz para el sistema de archivos.
      
       > [!NOTE]
       > Hola raíz carpeta es Hola principales, que se usa para las rutas de acceso relativas para todas las acciones relacionadas con el archivo. Puede especificar una carpeta local en el equipo de Hola donde se instala la puerta de enlace de datos de hello en local o carpeta de hello puede ser puede tener acceso un recurso compartido de red que Hola máquina.

   3. Escriba Hola username y password para puerta de enlace de Hola.
   4. Seleccione la puerta de enlace de Hola que instaló anteriormente.

       ![Configuración de la conexión](media/logic-apps-using-file-connector/create-file.png)

3. Después de proporcionar todos los detalles de hello, elija **crear**. 

   Lógica de aplicaciones se configura y comprueba la conexión, asegurándose de que la conexión de hello funciona correctamente. 
   Si la conexión de hello está configurado correctamente, verá opciones para la acción de Hola que seleccionó anteriormente. 
   Conector de sistema de archivos de Hello ahora está listo para su uso.

4. Especificar que desea toocopy archivos desde la carpeta de Dropbox toohello raíz para el recurso compartido de archivos de local.

   ![Acción Crear archivo](media/logic-apps-using-file-connector/create-file-filled.png)

5. Después de su archivo de Hola copias de aplicación lógica, agregar una acción de Outlook que envía un correo electrónico para que usuarios correspondientes saben el nuevo archivo de Hola. Especifique los destinatarios de hello, título y cuerpo del mensaje de Hola. 

   En el selector de contenido dinámico de hello, puede elegir datos salidas de conector de archivos de Hola para que pueda agregar más correo electrónico de toohello de detalles.

   ![Acción Enviar correo electrónico](media/logic-apps-using-file-connector/send-email.png)

6. Guarde la aplicación lógica. Probar la aplicación mediante la carga de un archivo tooDropbox. archivo Hello debe obtener el recurso compartido de archivos de toohello copiada en local y debe recibir un correo electrónico acerca de la operación de Hola.

   > [!TIP] 
   > Obtenga información acerca de cómo demasiado[supervisar las aplicaciones lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Enhorabuena, ahora tiene una aplicación de lógica de trabajo que se puede conectar el sistema de archivos local tooyour. Intente explorar otras funcionalidades que Hola ofertas de conector, por ejemplo:

- Crear archivo
- Enumerar archivos de la carpeta
- Anexar archivo
- Eliminar archivo
- Obtener contenido de archivo
- Obtener contenido de archivo mediante la ruta de acceso
- Obtener metadatos de archivo
- Obtener metadatos de archivo mediante la ruta de acceso
- Enumerar archivos de la carpeta raíz
- Actualizar archivo

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/fileconnector/). 

## <a name="get-help"></a>Obtener ayuda

tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

- [Conectar datos locales tooon](../logic-apps/logic-apps-gateway-connection.md) desde las aplicaciones lógicas
- Aprenda sobre la [integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md).
