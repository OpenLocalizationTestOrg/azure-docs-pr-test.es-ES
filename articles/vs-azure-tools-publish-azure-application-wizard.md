---
title: Hola aaaUsing Visual Studio Azure Asistente para publicar aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure Hola distintas configuraciones en hello Visual Studio Azure Asistente para publicar aplicaciones"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Uso de hello Visual Studio Azure Asistente para publicar aplicaciones
Después de desarrollar una aplicación web en Visual Studio, puede publicar ese tooan aplicación servicio de nube de Azure mediante hello **publicar aplicación de Azure** asistente. 

> [!NOTE]
> Este tema trata sobre la implementación de servicios de toocloud, no tooweb sitios. Para obtener información sobre cómo implementar sitios tooweb, consulte [cómo tooDeploy un sitio Web de Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Acceso al Asistente para publicar aplicación de Azure de Hola

Puede tener acceso el Asistente para publicar aplicación de Azure de Hola de dos maneras según tipo hello de proyecto de Visual Studio que tiene.

**Si tiene un proyecto de servicio en la nube de Azure:**

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **publicar**.

**Si tiene un proyecto de aplicación web no habilitado para Azure:**

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **convertir** > **convertir el proyecto de servicio de nube tooAzure**. 

1. En **el Explorador de soluciones**, haga clic en proyecto de Azure Hola recién creado y, en el menú contextual de hello, seleccione **publicar**.

## <a name="sign-in-page"></a>Página de inicio de sesión

![Página de inicio de sesión](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Cuenta de** : seleccione una cuenta o seleccione **agregar una cuenta** en la lista desplegable de cuenta de hello.

**Elija su suscripción** -elija hello toouse de suscripción para su implementación.
   
## <a name="settings-page---common-settings-tab"></a>Página Configuración: pestaña Configuración común   

![Configuración común](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Servicio de nube** -con hello desplegable, seleccione una nube existente de servicio o seleccione  **&lt;crear nuevo >**y crear un servicio de nube. Centro de datos de Hola se muestra entre paréntesis para cada servicio en la nube. Se recomienda que Hola ubicación de centro de datos para ser hello servicio en la nube Hola igual como ubicación de centro de datos de Hola Hola cuenta de almacenamiento (configuración avanzada).  

**Entorno**: seleccione **Producción** o **Ensayo**. Elija Hola entorno de ensayo si desea que toodeploy la aplicación en un entorno de prueba. 

**Configuración de compilación**: seleccione **Depurar** o **Liberar**.

**Configuración de servicio**: seleccione **Nube** o **Local**.
   
**Habilitar Escritorio remoto para todos los roles** -Compruebe que esta opción si desea que toobe pueda tooremotely conectar toohello servicio. Esta opción se emplea principalmente para la solución de problemas. Cuando se selecciona esta casilla de verificación, Hola **configuración de escritorio remoto** aparece el cuadro de diálogo. Elija hello **configuración** configuración de vínculo toochange Hola.
   
**Habilitar Web Deploy para todos los roles web** -comprobar esta opción, la implementación de web de tooenable para el servicio de Hola. Debe seleccionar hello **habilitar Escritorio remoto para todos los roles** opción toouse esta característica. Para más información, consulte [[Publicación de un servicio en la nube de Azure con Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Página Configuración: pestaña Configuración avanzada

![Configuración avanzada](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Etiqueta de implementación** -acepte el nombre predeterminado de hello, o escriba un nombre de su elección. tooappend Hola fecha toohello etiqueta de implementación, deje Hola casilla activada. 
   
**Cuenta de almacenamiento** : seleccione esta opción Hola toouse de cuenta de almacenamiento para esta implementación, **&lt;crear nuevo > toocreate una cuenta de almacenamiento. Centro de datos de Hola se muestra entre paréntesis para cada cuenta de almacenamiento. Se recomienda que Hola ubicación de centro de datos para ser hello cuenta de almacenamiento Hola igual como ubicación del centro de datos de Hola para servicio de nube de hello (configuración común).  
   
Hola cuenta de almacenamiento de Azure almacena paquete hello para la implementación de aplicación Hola. Una vez implementada la aplicación hello, paquete de Hola se quita de la cuenta de almacenamiento de Hola.

**Eliminar la implementación en caso de error** : seleccione esta opción de implementación de la hello toohave eliminada si se detectan errores durante la publicación. Esto debería ser desactivada si desea toomaintain una dirección IP virtual constante para el servicio de nube.

**Actualización de la implementación** : seleccione esta opción si desea toodeploy solo los componentes actualizados. Este tipo de implementación puede ser más rápido que la implementación completa. Esto se debe comprobar si desea toomaintain una dirección IP virtual constante para el servicio de nube. 

**Actualización de implementación - configuración** -se usa este cuadro de diálogo toofurther especificar cómo desea Hola roles toobe actualizado. Si elige **actualización Incremental**, cada instancia de la aplicación es uno tras otro, por lo que esa aplicación Hola siempre está disponible. Si elige **actualización simultánea**, se actualizan todas las instancias de la aplicación hello en el mismo tiempo. La actualización simultánea es más rápida, pero el servicio podría no estar disponible durante el proceso de actualización de Hola. 

![Configuración de implementación](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Habilitar IntelliTrace** : especifique si desea que tooenable IntelliTrace. Con IntelliTrace, puede registrar información de depuración amplia para una instancia de rol cuando se ejecuta en Azure. Si necesita causa de hello toofind de un problema, puede usar toostep de registros de IntelliTrace de hello recorrer el código de Visual Studio como si se estuviera ejecutando en Azure. Para más información sobre IntelliTrace, consulte [Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Habilitar generación de perfiles** : especifique si desea que la generación de perfiles de rendimiento de tooenable. Generador de perfiles de Visual Studio de Hello permite tooget un análisis detallado de aspectos de cálculo de Hola de cómo se ejecuta el servicio de nube. Para obtener más información sobre cómo utilizar el generador de perfiles de Visual Studio de hello, consulte [probar el rendimiento de Hola de un servicio de nube de Azure](./vs-azure-tools-performance-profiling-cloud-services.md).

**Habilitar depurador remoto para todos los roles** : especifique si desea que la depuración remota de tooenable. Para más información sobre cómo depurar los servicios en la nube con Visual Studio, consulte [Depuración de una máquina virtual o un servicio en la nube de Azure en Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Página Configuración de Diagnósticos

![Configuración de diagnóstico](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Diagnósticos le permite tootroubleshoot un servicio de nube de Azure (o máquina virtual de Azure). Para más información sobre el diagnóstico, consulte [Configuración de Diagnósticos en Azure Cloud Services y Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para más información sobre Application Insights, consulte [¿Qué es Application Insights?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Página de resumen

![Resumen](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Perfil de destino** -puede elegir toocreate un perfil de publicación de configuración de Hola que ha elegido. Por ejemplo, puede crear un perfil para un entorno de pruebas y otro para producción. toosave este perfil, elija hello **guardar** icono. Asistente de Hello crea el perfil de Hola y lo guarda en el proyecto de Visual Studio Hola. nombre del perfil toomodify hello, abra hello **elegir como destino profile** lista y, a continuación, elija **< administrar... >**.
   
   > [!NOTE]
   > perfil de publicación de Hello aparece en el Explorador de soluciones en Visual Studio y configuración de perfil de Hola se escriben tooa archivo con una extensión .azurePubxml. La configuración se guarda como atributos de etiquetas XML.
   > 
   > 

## <a name="publishing-your-application"></a>Publicación de la aplicación

Una vez que configure todos los valores de hello para la implementación del proyecto, seleccione **publicar** final Hola del cuadro de diálogo de Hola. Puede supervisar el estado de proceso de hello en hello **salida** ventana de Visual Studio.

## <a name="next-steps"></a>Pasos siguientes
- [Migrar y publicar un servicio de nube de Azure desde Visual Studio tooan de aplicación Web](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Obtenga información acerca de cómo toouse Visual Studio toopublish un Azure servicio en la nube](./vs-azure-tools-publishing-a-cloud-service.md)
- [Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Probar el rendimiento de Hola de un servicio de nube de Azure](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Configuración de Diagnósticos en Azure Cloud Services y Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [¿Qué es Application Insights?](./application-insights/app-insights-overview.md)