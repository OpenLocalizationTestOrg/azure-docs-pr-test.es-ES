---
title: servicio con Visual Studio e IntelliTrace en la nube aaaDebugging un informe publicado un Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo service toodebug una nube con Visual Studio y IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace
Con IntelliTrace, puede registrar información de depuración amplia para una instancia de rol cuando se ejecuta en Azure. Si necesita causa de hello toofind de un problema, puede usar toostep de registros de IntelliTrace de hello recorrer el código de Visual Studio como si se estuviera ejecutando en Azure. De hecho, IntelliTrace registra código de tecla ejecución y el entorno de datos cuando la aplicación de Azure se ejecuta como un servicio de nube en Azure y le permite reproducción los datos de hello registran desde Visual Studio. 

Puede utilizar IntelliTrace si tiene Visual Studio Enterprise instalado y su aplicación de Azure tiene como destino .NET Framework 4 o una versión posterior. IntelliTrace recopila información para sus roles de Azure. máquinas virtuales de Hola para estos roles que siempre se ejecutan sistemas operativos de 64 bits.

Como alternativa, puede usar [depuración remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directamente tooa servicio en la nube que se ejecuta en Azure.

> [!IMPORTANT]
> IntelliTrace está pensado solo para escenarios de depuración y no debe usarse para una implementación de producción.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configuración de una aplicación de Azure para IntelliTrace
tooenable IntelliTrace para una aplicación de Azure, debe crear y publicar la aplicación hello desde un proyecto de Azure en Visual Studio. Debe configurar IntelliTrace para la aplicación de Azure antes de publicarla tooAzure. Si publica la aplicación sin configurar IntelliTrace, necesita toorepublish Hola proyecto. Para más información, consulte cómo [publicar proyectos de servicios en la nube de Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Cuando esté listo toodeploy su aplicación de Azure, compruebe que el destino de compilación del proyecto se establece demasiado**depurar**.

1. En **el Explorador de soluciones**, haga clic en proyecto y, en el menú contextual de hello, seleccione **publicar**.
   
1. Hola **publicar aplicación de Azure** cuadro de diálogo, seleccione Hola suscripción de Azure y seleccione **siguiente**.

1. Hola **configuración** página, seleccione hello **configuración avanzada** ficha.

1. Activar hello **Habilitar IntelliTrace** opción toocollect los registros de IntelliTrace para la aplicación cuando se publica en la nube de Hola.
   
1. toocustomize Hola IntelliTrace configuración básica, seleccione **configuración** siguiente demasiado**Habilitar IntelliTrace**.

    ![Vínculo de configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. Hola **configuración de IntelliTrace** cuadro de diálogo, puede especificar qué eventos toolog, toocollect si la información de llamadas, registra qué toocollect módulos y procesos para y cuánto espacio tooallocate toohello grabación. Para obtener más información sobre IntelliTrace, consulte [Depuración con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

registro de IntelliTrace de Hello es un archivo de registro circular de tamaño máximo de hello especificado en la configuración de IntelliTrace de hello (tamaño predeterminado de hello es 250 MB). Registros de IntelliTrace son recopilados tooa archivo hello sistema de archivos de máquina virtual de Hola. Cuando se solicitan registros hello, una instantánea no se realiza en ese momento en el tiempo y descarga tooyour de equipo local.

Después de hello servicio de nube de Azure ha sido publicado tooAzure, puede determinar si se ha habilitado IntelliTrace en hello Azure nodo **Explorador de servidores**, tal y como se muestra en hello después de imagen:

![Explorador de servidores: IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Descarga de registros de IntelliTrace para una instancia de rol
Con Visual Studio, puede descargar registros de IntelliTrace para una instancia de rol si sigue estos pasos:

1. En **Explorador de servidores**, expanda hello **servicios en la nube** nodo y busque la instancia de rol cuyos registros desea toodownload. 

1. Haga clic en la instancia de rol de hello y, en el menú contextual de hello s, seleccione **ver registros de IntelliTrace**. 

    ![Opción de menú Ver registros de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. registros de IntelliTrace de Hello son archivo tooa descargado en un directorio en el equipo local. Cada vez que se solicita registros de IntelliTrace de hello, se crea una nueva instantánea. Mientras se descargan los registros de hello, Visual Studio muestra el progreso de Hola de operación de Hola Hola **Azure Activity Log** ventana. Tal y como se muestra en la figura siguiente de Hola, puede expandir el elemento de línea de Hola para hello operación toosee más detalle.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Puede continuar toowork en Visual Studio mientras se descargan los registros de IntelliTrace Hola. Al registro de hello haya acabado la descarga, se abre en Visual Studio.

> [!NOTE]
> Hello registros de IntelliTrace podrían contener excepciones framework Hola genera y administra posteriormente. El código del marco interno genera estas excepciones como parte normal del inicio de un rol, por lo que puede omitirlas de forma segura.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
- [Opciones de depuración de servicios en la nube de Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publicación de un servicio en la nube de Azure mediante Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)