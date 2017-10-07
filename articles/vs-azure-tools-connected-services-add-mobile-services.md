---
title: "aaaAdding servicios móviles mediante el uso de servicios conectados en Visual Studio | Documentos de Microsoft"
description: "Agregar servicios móviles mediante el cuadro de diálogo de Visual Studio agregar servicios conectados Hola"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Adición de Servicios móviles mediante Servicios conectados de Visual Studio
Con Visual Studio 2015, puede conectarse tooAzure servicios para dispositivos móviles mediante hello **Agregar servicio conectado** cuadro de diálogo. Puede conectarse desde cualquier aplicación cliente de C#, cualquier aplicación de JavaScript o cualquier aplicación de Cordova multiplataforma. Una vez conectado, puede crear y tener acceso a datos, crear API personalizadas y trabajos programados o agregar compatibilidad con notificaciones de inserción.  Hello servicios conectados operación agrega todas las referencias adecuadas y el código de conexión. También puede aprovechar la compatibilidad integrada para la autenticación con diferentes esquemas de identidad populares, como cuentas de Microsoft, Azure AD, Facebook y Twitter.

## <a name="supported-project-types"></a>Tipos de proyecto compatibles
> [!NOTE]
> En Visual Studio 2015, no se admite agregar proyectos universales de Windows (Windows 10) de tooa de servicios móviles de Azure mediante el cuadro de diálogo de hello agregar servicios conectados. Puede agregar servicios móviles de Azure al instalar paquetes de hello adecuada utilizando el Administrador de paquetes de NuGet Hola de su proyecto.
> 
> 

Puede usar Hola servicios conectados diálogo tooconnect tooAzure servicios móviles Hola siguientes tipos de proyecto.

* Proyectos de la Tienda Windows 8.1 de .NET, Phone y aplicación universal
* Proyectos de la Tienda Windows 8.1 de JavaScript, Phone y aplicación universal
* Proyectos creados con herramientas de Visual Studio para Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Conectar tooAzure servicios para dispositivos móviles mediante el cuadro de diálogo de hello agregar servicios conectados
1. Asegúrese de que tiene una cuenta de Azure. Si no tiene una cuenta de Azure, puede registrarse para obtener una [evaluación gratuita](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Abra hello **agregar servicios conectados** cuadro de diálogo.
   
   * Para las aplicaciones. NET, abra el proyecto en Visual Studio, menú contextual abierto Hola Hola **referencias** nodo en el Explorador de soluciones y, a continuación, elija **Agregar servicio conectado**
     
        ![Conexión tooAzure servicio móvil](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Para los proyectos de aplicación de Apache Cordova, abra el proyecto en Visual Studio, abra Hola contexto menú Hola nodo de proyecto en el Explorador de soluciones y, a continuación, elija **Agregar servicio conectado**.
3. Hola **Agregar servicio conectado** diálogo cuadro, elija **servicios móviles de Azure**y, a continuación, elija hello **configurar** botón. Si aún no lo ha hecho, es posible que toolog solicitada en Azure.
   
    ![Adición de un servicio móvil de Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Hola **servicios móviles de Azure** diálogo cuadro, elija un servicio móvil existente si tiene uno. Si necesita toocreate un nuevo servicio móvil de Azure, por lo que siga procedimiento hello debajo de toodo. En caso contrario, omita el paso siguiente toohello.
   
    toocreate una nueva cuenta de servicio móvil:
   
   1. Elija Hola ** Create Service ** vínculo final Hola Hola del cuadro de diálogo.
       ![Agregar nuevo servicio conectado móvil](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. En hello **crear servicio móvil** cuadro de diálogo, puede elegir un servicio móvil de back-end de JavaScript o un servicio móvil de back-end de .NET de hello **en tiempo de ejecución** lista desplegable. 
      
       ![Creación de un servicio móvil](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Un servicio de back-end de JavaScript es sencillo y eficaz. Si crea un servicio móvil de back-end de JavaScript, el código de JavaScript del lado servidor de Hola se almacena en la nube de hello, pero puede editar scripts de servidor utilizando el Explorador de servidores o el portal de administración de Azure Hola. 
      
       Un servicio móvil de back-end de .NET ofrece Hola toda potencia y flexibilidad de API Web y Entity Framework. Si crea un servicio móvil de back-end. NET, un proyecto se crea automáticamente y agrega tooyour solución. 
   3. Elija hello **región** donde desee servicio móvil de hello y, a continuación, escriba un nombre de usuario y una contraseña para el servidor de Hola.
   4. Después de haber especificado toda la información necesaria de hello, elija hello **crear** botón servicio móvil de toocreate Hola.
   5. nuevo servicio móvil de Hello debe aparecer en la lista de servicios de hello en hello **servicios móviles de Azure** cuadro de diálogo. Elija nuevo servicio móvil de hello en lista de Hola y, a continuación, elija Hola **agregar** proyecto tooyour de botón tooadd Hola servicio.
5. Revisión Hola Introducción página que aparece y averiguar cómo se ha modificado el proyecto. Una página Introducción aparece en el explorador siempre que se agregue un servicio conectado. Puede revisar Hola los pasos siguientes sugeridos y ejemplos de código, o bien cambie toohello toosee de página ¿Qué ha ocurrido qué referencias se agregaron tooyour proyecto, y cómo se han modificado los archivos de código y la configuración.
6. Con los ejemplos de código de hello como guía, empiece a escribir código tooaccess su servicio móvil.

## <a name="how-your-project-is-modified"></a>¿Cómo se modifica el proyecto?
Cómo Visual Studio modifica el proyecto depende de tipo de proyecto de Hola. En las aplicaciones cliente de C#, consulte [¿Qué ha ocurrido? - Proyectos de C#](http://go.microsoft.com/fwlink/p/?LinkId=513119). En las aplicaciones cliente de JavaScript, consulte [¿Qué ha ocurrido? - Proyectos de JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). En las aplicaciones de Cordova, consulte [¿Qué ha ocurrido? - Proyectos de Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Pasos siguientes
Formule preguntas y obtenga ayuda: 

* [Foro de MSDN: Servicios móviles de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Servicios móviles de Azure en hello Blog del equipo de Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Servicios móviles de Azure en azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentación de Servicios móviles de Azure en azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

