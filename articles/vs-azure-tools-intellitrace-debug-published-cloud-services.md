---
title: "Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace | Microsoft Docs"
description: "Obtenga información sobre cómo depurar un servicio en la nube con Visual Studio e IntelliTrace"
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
ms.openlocfilehash: 7905dfb97cbd7578a8422567fe674839d00c21ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace
Con IntelliTrace, puede registrar información de depuración amplia para una instancia de rol cuando se ejecuta en Azure. Si necesita encontrar la causa de un problema, puede utilizar los registros de IntelliTrace para recorrer su código desde Visual Studio como si se estuviera ejecutando en Azure. De hecho, IntelliTrace graba datos de entorno y ejecución de código de clave  cuando su aplicación de Azure se ejecuta como servicio en la nube en Azure y le permite reproducir los datos grabados desde Visual Studio. 

Puede utilizar IntelliTrace si tiene Visual Studio Enterprise instalado y su aplicación de Azure tiene como destino .NET Framework 4 o una versión posterior. IntelliTrace recopila información para sus roles de Azure. Las máquinas virtuales para estos roles siempre ejecutan sistemas operativos de 64 bits.

Como alternativa, puede usar la [depuración remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) para conectarse directamente a un servicio en la nube que se ejecuta en Azure.

> [!IMPORTANT]
> IntelliTrace está pensado solo para escenarios de depuración y no debe usarse para una implementación de producción.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configuración de una aplicación de Azure para IntelliTrace
Para habilitar IntelliTrace para una aplicación de Azure, debe crear y publicar la aplicación desde un proyecto de Azure de Visual Studio. Debe configurar IntelliTrace para su aplicación de Azure antes de su publicación en Azure. Si publica la aplicación sin configurar IntelliTrace, deberá volver a publicar el proyecto. Para más información, consulte cómo [publicar proyectos de servicios en la nube de Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Cuando esté preparado para implementar su aplicación de Azure, compruebe que sus destinos de compilación del proyecto se establecen en **Depurar**.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, en el menú contextual, seleccione **Publicar**.
   
1. En el cuadro de diálogo **Publicar aplicaciones de Azure**, seleccione la suscripción de Azure y, luego, **Siguiente**.

1. En la página de **configuración**, seleccione la pestaña de **configuración avanzada**.

1. Active la opción **Habilitar IntelliTrace** para recopilar registros de IntelliTrace de la aplicación cuando se publique en la nube.
   
1. Para personalizar la configuración básica de IntelliTrace, seleccione **Configuración** junto a **Habilitar IntelliTrace**.

    ![Vínculo de configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. En el cuadro de diálogo de **configuración de IntelliTrace**, puede especificar qué eventos se van a registrar, si se va a recopilar información de llamada, para qué módulos y procesos se van a recopilar registros y cuánto espacio se va a asignar a la grabación. Para obtener más información sobre IntelliTrace, consulte [Depuración con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

El registro de IntelliTrace es un archivo de registro circular del máximo tamaño especificado en la configuración de IntelliTrace (el tamaño predeterminado es de 250 MB). Los registros de IntelliTrace se recopilan en un archivo en el sistema de archivos de la máquina virtual. Al solicitar los registros, se toma una instantánea en ese momento en el tiempo y se descarga en su equipo local.

Después de que el servicio en la nube de Azure se publica en Azure, puede determinar si se habilitó IntelliTrace desde el nodo de Azure en el **Explorador de servidores**, tal como se muestra en la imagen siguiente:

![Explorador de servidores: IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Descarga de registros de IntelliTrace para una instancia de rol
Con Visual Studio, puede descargar registros de IntelliTrace para una instancia de rol si sigue estos pasos:

1. En **Explorador de servidores**, expanda el nodo **Servicios en la nube** y ubique la instancia de rol cuyos registros desea descargar. 

1. Haga clic con el botón derecho en la instancia de rol y, en el menú contextual, seleccione **Ver registros de IntelliTrace**. 

    ![Opción de menú Ver registros de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. Los registros de IntelliTrace se descargan en un archivo de un directorio de su equipo local. Cada vez que solicita los registros de IntelliTrace, se crea una nueva instantánea. Cuando se descargan los registros, Visual Studio muestra el avance de la operación en la ventana **Registro de actividad de Azure**. Como se muestra en la ilustración siguiente, puede expandir el artículo de línea de la operación para ver más detalles.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Puede continuar trabajando en Visual Studio mientras se descargan los registros de IntelliTrace. Cuando el registro termine la descarga, se abre en Visual Studio.

> [!NOTE]
> Es posible que los registros de IntelliTrace contengan excepciones que el marco genera y maneja posteriormente. El código del marco interno genera estas excepciones como parte normal del inicio de un rol, por lo que puede omitirlas de forma segura.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
- [Opciones de depuración de servicios en la nube de Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publicación de un servicio en la nube de Azure mediante Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)