---
title: "aaaConfiguring diagnósticos para máquinas virtuales y servicios en la nube | Documentos de Microsoft"
description: "Describe cómo tooconfigure información de diagnóstico para depurar los servicios de nube de Azure y máquinas virtuales (VM) en Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configuración de Diagnósticos en Servicios en la nube y Máquinas virtuales de Azure
Cuando necesite tootroubleshoot una máquina virtual de Azure o el servicio de nube de Azure, puede configurar diagnósticos de Azure más fácilmente con Visual Studio. Diagnósticos de Azure captura los datos del sistema y datos de registro en máquinas virtuales de Hola y las instancias de máquina virtual que ejecutan su servicio de nube y transfieren esos datos en una cuenta de almacenamiento de su elección. Vea [Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) para obtener más información sobre el registro de diagnóstico de Azure.

Este tema muestra cómo tooenable y configurar diagnósticos de Azure en Visual Studio, tanto antes como después de la implementación, así como en máquinas virtuales de Azure. También muestra cómo los tipos de hello tooselect de toocollect de información de diagnóstico y cómo se recopila información de hello tooview una vez.

Puede configurar diagnósticos de Azure de hello siguientes maneras:

* Puede cambiar la configuración de diagnóstico a través de hello **configuración de diagnóstico** cuadro de diálogo de Visual Studio. configuración de Hola se guarda en un archivo denominado diagnostics.wadcfgx (diagnostics.wadcfg en Azure SDK 2.4 o anterior). Como alternativa, puede modificar directamente el archivo de configuración de Hola. Si actualiza manualmente el archivo de hello, cambios de configuración de hello tardarán Hola efecto siguiente vez que implemente tooAzure de servicio de nube de Hola o servicio de ejecución hello en el emulador de Hola.
* Use **Explorer nube** o **Explorador de servidores** en configuración de diagnóstico de Visual Studio toochange Hola para una máquina virtual o un servicio en ejecución en la nube.

## <a name="azure-26-diagnostics-changes"></a>Cambios de diagnóstico de Azure 2.6
Para los proyectos de Azure SDK 2.6 en Visual Studio, Hola siguientes cambios se realizaron. (Estos cambios también aplican toolater versiones del SDK de Azure.)

* un emulador local Hola ahora es compatible con diagnósticos. Esto significa que puede recopilar datos de diagnóstico y asegúrese de que la aplicación está creando Hola seguimientos correctos mientras está desarrollando y pruebas en Visual Studio. cadena de conexión de Hola `UseDevelopmentStorage=true` habilita la recopilación de datos de diagnóstico mientras se ejecuta el proyecto de servicio de nube en Visual Studio mediante Hola emulador de almacenamiento de Azure. Todos los datos de diagnóstico se recopilan en la cuenta de almacenamiento de hello (almacenamiento de desarrollo).
* cadena de conexión de la cuenta para la almacenamiento de diagnósticos Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) se almacena una vez más en el archivo de configuración (.cscfg) del servicio de Hola. En Azure SDK 2.5 cuenta de almacenamiento de diagnósticos de Hola se especificó en el archivo de hello diagnostics.wadcfgx.

Hay algunas diferencias importantes entre la cadena de conexión de hello trabajado en Azure SDK 2.4 y versiones anteriores y cómo funciona en Azure SDK 2.6 y versiones posteriores.

* En Azure SDK 2.4 y versiones anteriores, cadena de conexión de hello usado como un tiempo de ejecución por información de cuenta de almacenamiento de Hola de hello diagnósticos complemento tooget para transferir los registros de diagnóstico.
* En Azure SDK 2.6 y versiones posteriores, se utiliza la cadena de conexión de diagnósticos de Hola por extensión de diagnósticos de Visual Studio tooconfigure Hola con la información de cuenta de almacenamiento apropiada de Hola durante la publicación. cadena de conexión de Hello le permite definir las cuentas de almacenamiento distintas para diferentes configuraciones del servicio que va a usar Visual Studio al publicar. Sin embargo, porque ya no está disponible el complemento de diagnóstico de hello (después de Azure SDK 2.5), archivo de .cscfg de hello por sí mismo no puede habilitar Hola extensión de diagnósticos. Tiene la extensión de hello tooenable por separado mediante herramientas como Visual Studio o PowerShell.
* proceso de hello toosimplify de configuración de extensión de diagnósticos de hello con PowerShell, salida del paquete Hola desde Visual Studio también contiene Hola pública XML de configuración de extensión de diagnósticos de Hola para cada rol. Visual Studio usa Hola conexión cadena toopopulate Hola almacenamiento cuenta información de diagnóstico está presente en la configuración pública de Hola. archivos de configuración pública de Hola se crean en la carpeta de extensiones de Hola y seguir Hola patrón PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Las implementaciones basadas en PowerShell pueden usar este patrón toomap cada rol tooa de configuración.
* También se utiliza la cadena de conexión de Hello en el archivo de .cscfg de hello por hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess Hola datos de diagnóstico para que pueda aparecer en hello **supervisión** se necesita la cadena de conexión de Hola de pestaña. tooconfigure Hola servicio tooshow detallado de los datos en el portal de Hola de supervisión.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrar proyectos tooAzure SDK 2.6 y versiones posterior
Al migrar desde Azure SDK 2.5 tooAzure SDK 2.6 o versiones posteriores, si tuviera una cuenta de almacenamiento de diagnósticos especificada en el archivo .wadcfgx de hello, a continuación, permanecerá allí. cuentas de tootake aprovechar la flexibilidad de hello del uso de almacenamiento diferente para distintas configuraciones de almacenamiento, tendrá que toomanually Agregar proyecto de tooyour de cadena de conexión de Hola. Si está migrando un proyecto de Azure SDK 2.4 o anterior tooAzure SDK 2.6, Hola, a continuación, se conservan las cadenas de conexión de diagnóstico. Sin embargo, tenga en cuenta los cambios de hello en cómo se tratan las cadenas de conexión en Azure SDK 2.6 tal como se especifica en la sección anterior de Hola.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Cómo Visual Studio determina la cuenta de almacenamiento de diagnósticos de Hola
* Si se especifica una cadena de conexión de diagnóstico en el archivo de .cscfg de hello, Visual Studio utiliza extensión de diagnósticos de hello tooconfigure al publicar y al generar archivos xml de configuración pública de Hola durante el empaquetado.
* Si no se especifica ninguna cadena de conexión de diagnóstico en el archivo de .cscfg de hello, a continuación, Visual Studio vuelve cuenta de almacenamiento de hello toousing especificada en hello wadcfgx tooconfigure Hola diagnósticos extensión de archivo al publicar y generar Hola público archivos xml de configuración al empaquetar.
* cadena de conexión de diagnósticos de Hello en el archivo de .cscfg de hello tiene prioridad sobre la cuenta de almacenamiento de hello en el archivo .wadcfgx de Hola. Si es una cadena de conexión de diagnósticos especificado en el archivo de .cscfg de hello, a continuación, Visual Studio usa y omite la cuenta de almacenamiento de hello en wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>¿Qué does Hola "Actualizar cadenas de conexión de almacenamiento de desarrollo..." desarrollo..."?
Hola casilla **actualizar cadenas de conexión de almacenamiento de desarrollo para diagnóstico y almacenamiento en caché con las credenciales de cuenta de almacenamiento de Microsoft Azure al publicar tooMicrosoft Azure** le ofrece una manera cómoda de tooupdate cualquier cadenas de conexión de cuenta de almacenamiento de desarrollo con la cuenta de almacenamiento de Azure Hola especificada durante la publicación.

Por ejemplo, suponga que activa esta casilla y especifica la cadena de conexión de diagnósticos de hello `UseDevelopmentStorage=true`. Cuando publica hello tooAzure de proyecto, Visual Studio actualizará automáticamente cadena de conexión de diagnósticos de Hola con cuenta de almacenamiento de Hola que especificó en el Asistente para publicación de Hola. Sin embargo, si se especificó una cuenta de almacenamiento real como cadena de conexión de diagnósticos de hello, a continuación, dicha cuenta se utiliza en su lugar.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferencias de funcionalidad de diagnóstico entre Azure SDK 2.4 y versiones anteriores y Azure SDK 2.5 y versiones posteriores
Si va a actualizar el proyecto de Azure SDK 2.4 tooAzure SDK 2.5 o versiones posteriores, debe tener en hello cuenta después de las diferencias de funcionalidad de diagnóstico.

* **Las API de configuración están desusadas** : la configuración mediante programación del diagnóstico está disponible en Azure SDK 2.4 o versiones anteriores, pero está en desuso en Azure SDK 2.5 y versiones posteriores. Si su configuración de diagnóstico está definida actualmente en el código, deberá tooreconfigure estos valores desde cero en el proyecto migrado de hello en orden para trabajar de tookeep de diagnóstico. archivo de configuración de diagnósticos de Hola para Azure SDK 2.4 es diagnostics.wadcfg y diagnostics.wadcfgx para Azure SDK 2.5 y versiones posteriores.
* **Los diagnósticos para aplicaciones de servicio de nube solo pueden configurarse en el nivel de rol de hello, no en el nivel de instancia de Hola.**
* **Cada vez que implementa la aplicación, se actualiza la configuración de diagnóstico de Hola** : Esto puede causar problemas de paridad si cambia la configuración de diagnóstico del explorador de servidores y, a continuación, volver a implementar la aplicación.
* **En Azure SDK 2.5 y versiones posteriores, los volcados de memoria se configuran en el archivo de configuración de diagnósticos de hello, no en el código** : si tiene volcados de memoria configurados en el código, deberá volver configuración de Hola de transferencia de toomanually toohello configuración archivo de código, no se transfieren porque volcados de Hola durante la migración de hello tooAzure SDK 2.6.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Habilitar diagnósticos en los proyectos de servicios en la nube antes de implementarlos
En Visual Studio, puede elegir toocollect datos de diagnóstico para los roles que se ejecutan en Azure, al ejecutar el servicio de hello en el emulador de hello antes de implementarla. Todas las configuraciones de toodiagnostics de cambios en Visual Studio se guardan en el archivo de configuración de hello diagnostics.wadcfgx. Estos valores de configuración especifican cuenta de almacenamiento de Hola donde se guardan los datos de diagnóstico cuando se implementa el servicio en la nube.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>diagnóstico de tooenable en Visual Studio antes de la implementación
1. En el menú contextual de hello para el rol de Hola que le interese, elija **propiedades**y, a continuación, elija hello **configuración** ficha del rol de hello **propiedades** ventana.
2. Hola **diagnósticos** sección, asegúrese de que ese hello **habilitar diagnósticos** casilla está activada.
   
    ![Obtener acceso a la opción de habilitar diagnósticos de Hola](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Elija almacenamiento Hola puntos suspensivos (...) botón toospecify Hola cuenta donde desea toobe de datos de diagnóstico de hello almacenado. cuenta de almacenamiento de Hola que elija será ubicación Hola donde se almacenan los datos de diagnóstico.
   
    ![Especificar toouse de cuenta de almacenamiento de Hola](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Hola **crear cadenas de conexión de almacenamiento** cuadro de diálogo, especifique si desea tooconnect con hello emulador de almacenamiento de Azure, una suscripción a Azure o credenciales escritas manualmente.
   
    ![Cuadro de diálogo Cuenta de almacenamiento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Si elige la opción de emulador de almacenamiento de Microsoft Azure hello, cadena de conexión de Hola se establece tooUseDevelopmentStorage = true.
   * Si elige la opción de suscripción hello, puede elegir Hola desea hello y toouse nombre de la cuenta de suscripción de Azure. Puede que administrar cuentas de hello botón toomanage las suscripciones de Azure.
   * Si se elige la opción de credenciales de hello escrita manualmente, dispone de nombre de hello tooenter solicitada y la clave de cuenta de Azure que desee toouse Hola.
5. Elija hello **configurar** Hola de botón tooview **configuración de diagnóstico** cuadro de diálogo. Cada pestaña (excepto para **General** y **Directorios de registro**) representa un origen de datos de diagnóstico que puede recopilar. ficha predeterminada de Hello, **General**, ofrece Hola siguientes opciones de recopilación de datos de diagnóstico: **solo errores**, **toda la información de**, y **plan personalizado** . Hola opción predeterminada, **solo errores**, toma Hola menor cantidad de almacenamiento porque no transfiere las advertencias o mensajes de seguimiento. Hola todas las transferencias de opción de información Hola mayor cantidad de información y es, por lo tanto, Hola opción más cara en términos de almacenamiento.
   
    ![Habilitar configuración y diagnóstico de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. En este ejemplo, seleccione hello **plan personalizado** opción para que pueda personalizar datos de hello recopilados.
7. Hola **cuota de disco en MB** cuadro especifica la cantidad de espacio que desea tooallocate en el almacenamiento de la cuenta para los datos de diagnóstico. Puede cambiar el valor predeterminado de hello si desea.
8. En cada ficha de datos de diagnóstico que desee toocollect, seleccione su **Habilitar transferencia de <log type>**  casilla de verificación. Por ejemplo, si desea que los registros de aplicación toocollect, seleccione hello **Habilitar transferencia de registros de aplicaciones** casilla de verificación de hello **registros de la aplicación** ficha. Además, especifique cualquier otra información requerida por cada tipo de datos de diagnóstico. Consulte la sección de hello **configurar orígenes de datos de diagnóstico** más adelante en este tema para obtener información de configuración en cada pestaña.
9. Después de habilitar la colección de todos los datos de diagnóstico de Hola que desee, elija hello **Aceptar** botón.
10. Abra el proyecto del servicio en la nube de Azure en Visual Studio de la manera habitual. Cuando usa su aplicación, información de registro de hello que ha habilitado se guarda toohello cuenta de almacenamiento de Azure que especificó.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Habilitar diagnósticos en máquinas virtuales de Azure
En Visual Studio, puede elegir toocollect datos de diagnóstico para máquinas virtuales de Azure.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>tooenable diagnósticos en máquinas virtuales de Azure
1. En **Explorador de servidores**, elija Hola nodos de Azure y, a continuación, conecte tooyour suscripción de Azure, si aún no está conectado.
2. Expanda hello **máquinas virtuales** nodo. Puede crear una nueva máquina virtual o seleccionar uno que ya exista.
3. En el menú contextual de hello para la máquina virtual de Hola que le interese, elija **configurar**. Esto muestra el cuadro de diálogo de configuración de máquina virtual de Hola.
   
    ![Configuración de una máquina virtual de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Si aún no está instalado, agregue la extensión de diagnósticos del agente de supervisión de Microsoft de Hola. Esta extensión le permite recopilar datos de diagnóstico para la máquina virtual de Azure Hola. En la lista de extensiones instaladas de hello, elija Hola seleccione una extensión disponible desplegable menú y, a continuación, elija diagnóstico de agente de supervisión de Microsoft.
   
    ![Instalación de una extensión de máquina virtual de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Hay otras extensiones de diagnóstico disponibles para las máquinas virtuales. Para obtener más información, vea Características y extensiones de máquina virtual de Azure.
   > 
   > 
5. Elija hello **agregar** botón tooadd Hola extensión y ver su **configuración de diagnóstico** cuadro de diálogo.
6. Elija hello **configurar** botón toospecify una cuenta de almacenamiento y, a continuación, elija hello **Aceptar** botón.
   
    Cada pestaña (excepto para **General** y **Directorios de registro**) representa un origen de datos de diagnóstico que puede recopilar.
   
    ![Habilitar configuración y diagnóstico de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    ficha predeterminada de Hello, **General**, ofrece Hola siguientes opciones de recopilación de datos de diagnóstico: **solo errores**, **toda la información de**, y **plan personalizado** . Hola opción predeterminada, **solo errores**, toma Hola menor cantidad de almacenamiento porque no transfiere las advertencias o mensajes de seguimiento. Hola **toda la información de** opción transferencias Hola mayor cantidad de información y es, por lo tanto, la opción más cara de hello en términos de almacenamiento.
7. En este ejemplo, seleccione hello **plan personalizado** opción para que pueda personalizar datos de hello recopilados.
8. Hola **cuota de disco en MB** cuadro especifica la cantidad de espacio que desea tooallocate en el almacenamiento de la cuenta para los datos de diagnóstico. Puede cambiar el valor predeterminado de hello si desea.
9. En cada ficha de datos de diagnóstico que desee toocollect, seleccione su **Habilitar transferencia de <log type>**  casilla de verificación.
   
    Por ejemplo, si desea que los registros de aplicación toocollect, seleccione hello **Habilitar transferencia de registros de aplicaciones** casilla de verificación de hello **registros de la aplicación** ficha. Además, especifique cualquier otra información requerida por cada tipo de datos de diagnóstico. Consulte la sección de hello **configurar orígenes de datos de diagnóstico** más adelante en este tema para obtener información de configuración en cada pestaña.
10. Después de habilitar la colección de todos los datos de diagnóstico de Hola que desee, elija hello **Aceptar** botón.
11. Guarde el proyecto de hello actualizado.
    
     Verá un mensaje de Hola **Microsoft Azure Activity Log** ventana que Hola máquina virtual se ha actualizado.

## <a name="configure-diagnostics-data-sources"></a>Configurar orígenes de datos de diagnósticos
Después de habilitar la recopilación de datos de diagnóstico, puede elegir exactamente qué orígenes de datos que desea toocollect y qué información se recopila. Hello siguiente es una lista de las pestañas en hello **configuración de diagnóstico** cuadro de diálogo y significa qué cada opción de configuración.

### <a name="application-logs"></a>Registros de aplicación
**Application logs** contienen información de diagnóstico generada por una aplicación web. Si desea que los registros de aplicación toocapture, seleccione hello **Habilitar transferencia de registros de la aplicación** casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de la aplicación hello tooyour cuenta de almacenamiento cambiando hello **período de transferencia (min)** valor. También puede cambiar la cantidad de Hola de información capturada en el registro de hello estableciendo el valor de nivel de registro de hello. Por ejemplo, puede elegir **detallado** tooget obtener más información o elija **crítico** toocapture sólo crítico errores. Si tiene un proveedor de diagnósticos específicos que emite registros de aplicaciones, puede capturarlos agregando toohello GUID del proveedor de hello **GUID de proveedor** cuadro.

  ![Registros de aplicación](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Vea [Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) para obtener más información sobre los registros de aplicación.

### <a name="windows-event-logs"></a>Registros de eventos de Windows
Si desea que toocapture registros de eventos de Windows, seleccione hello **Habilitar transferencia de registros de eventos de Windows** casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de eventos de hello tooyour cuenta de almacenamiento cambiando hello **período de transferencia (min)** valor. Hola seleccione las casillas de verificación para los tipos de Hola de eventos que desee tootrack.

  ![Registros de eventos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Si está usando Azure SDK 2.6 o posterior y desea toospecify un origen de datos personalizado, escríbalo en hello  **<Data source name>**  texto y, a continuación, elija hello **agregar** tooit siguiente botón. origen de datos de Hola se agrega el archivo diagnostics.cfcfg de toohello.

Si está usando Azure SDK 2.5 y desea toospecify un origen de datos personalizado, puede agregarlo toohello `WindowsEventLog` archivo de sección de hello diagnostics.wadcfgx, como se muestra en el siguiente ejemplo de Hola.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Contadores de rendimiento
La información del contador de rendimiento puede ayudarle a buscar cuellos de botella del sistema y a optimizar el rendimiento del sistema y de la aplicación. Vea [Crear y usar contadores de rendimiento en una aplicación de Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) para obtener más información. Si desea que los contadores de rendimiento toocapture, seleccione hello **Habilitar transferencia de contadores de rendimiento** casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de eventos de hello tooyour cuenta de almacenamiento cambiando hello **período de transferencia (min)** valor. Active la casillas de verificación de Hola para hello contadores de rendimiento que desea tootrack.

  ![Contadores de rendimiento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack un contador de rendimiento que no está en la lista, introdúzcalo utilizando Hola sintaxis sugerida y, a continuación, elija hello **agregar** botón. sistema operativo de Hello en la máquina virtual de hello determina qué contadores de rendimiento que se puede realizar un seguimiento. Para obtener más información sobre la sintaxis, vea [Especificación de una ruta de contador](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Registros de infraestructura
Si desea que los registros de infraestructura de toocapture, que contienen información acerca de hello infraestructura de diagnóstico de Azure, el módulo de RemoteAccess de Hola y el módulo RemoteForwarder de hello, seleccione hello **Habilitar transferencia de registros de infraestructura**casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de hello tooyour cuenta de almacenamiento cambiando el valor de período de transferencia (min) de Hola.

  ![Registros de infraestructura de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Consulte [Recopilar datos de registro mediante Diagnósticos de Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) para obtener más información.

### <a name="log-directories"></a>Directorios de registro
Si desea que los directorios de registro de toocapture, que contienen datos recopilados de los directorios de registro para las solicitudes de Internet Information Services (IIS), las solicitudes con error, o las carpetas que elija, seleccione hello **Habilitar transferencia de directorios de registro**casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de hello tooyour cuenta de almacenamiento cambiando hello **período de transferencia (min)** valor.

Puede activar las casillas de Hola de registros de hello desee toocollect, por ejemplo, **registros de IIS** y **solicitudes con error** registros. Se proporcionan los nombres de contenedor de almacenamiento de forma predeterminada, pero puede cambiar nombres de hello si lo desea.

Además, puede capturar registros desde cualquier carpeta. Simplemente especificar ruta de acceso de Hola Hola **registro de directorio absoluto** sección y, a continuación, elija hello **Agregar directorio** botón. Hello registros se capturarán toohello especifica contenedores.

  ![Directorios de registro](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Registros de ETW
Si usa [seguimiento de eventos para Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) y desea que los registros ETW toocapture, seleccione hello **Habilitar transferencia de registros de ETW** casilla de verificación. Puede aumentar o reducir Hola número de minutos cuando se transfieren los registros de hello tooyour cuenta de almacenamiento cambiando hello **período de transferencia (min)** valor.

Hola eventos se capturan de orígenes de eventos y los manifiestos de eventos que especifique. toospecify un origen de eventos, escriba un nombre en hello **orígenes de eventos** sección y, a continuación, elija hello **agregar origen de evento** botón. De forma similar, puede especificar un manifiesto de evento en hello **manifiestos de eventos** sección y, a continuación, elija hello **agregar manifiesto de evento** botón.

  ![Registros de ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  marco ETW de Hola se admite en ASP.NET a través de las clases de hello [System.Diagnostics.aspx] (espacio de nombres https://msdn.microsoft.com/library/system.diagnostics (110). Hola Microsoft.WindowsAzure.Diagnostics espacio de nombres, que hereda de y amplía estándar (clases https://msdn.microsoft.com/library/system.diagnostics (110), habilita el uso de Hola de [System.Diagnostics.aspx] ([System.Diagnostics.aspx] https://msdn.Microsoft.com/library/System.Diagnostics (110) como un marco de registro de hello entorno de Azure. Para más información, vea [Tomar el control del registro y el seguimiento en Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) y [Habilitación de diagnósticos en Azure Cloud Services y Azure Virtual Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Volcados de memoria
Si desea que toocapture información acerca de cuándo se bloquea una instancia de rol, seleccione hello **Habilitar transferencia de volcados** casilla de verificación. (Puesto que ASP.NET controla la mayoría de las excepciones, normalmente solo es útil para roles de trabajo.) Puede aumentar o reducir el porcentaje de Hola de almacenamiento espacio dedicado a volcados de memoria toohello cambiando hello **cuota de directorio (%)** valor. Puede cambiar el contenedor de almacenamiento de Hola donde se almacenan los volcados de Hola y puede seleccionar si desea que toocapture una **completa** o **Mini** volcado de memoria.

se enumeran los procesos de Hello está realizando el seguimiento. Seleccione Hola casillas para los procesos de Hola que desea toocapture. tooadd otra lista de toohello de proceso, escriba el nombre del proceso de hello y, a continuación, elija hello **Agregar proceso** botón.

  ![Volcados de memoria](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Vea [Tomar el control del registro y el seguimiento en Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) y [Diagnósticos de Microsoft Azure Parte 4: Componentes de registro personalizados y cambios de Diagnósticos de Azure 1.3](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) para obtener más información.

## <a name="view-hello-diagnostics-data"></a>Ver datos de diagnóstico de Hola
Después de haber recopilado los datos de diagnóstico de Hola para un servicio de nube o una máquina virtual, puede verlo.

### <a name="tooview-cloud-service-diagnostics-data"></a>datos de diagnóstico de servicio de nube tooview
1. Implemente su servicio en nube como de costumbre y luego ejecútelo.
2. Puede ver datos de diagnóstico de hello en un informe que genera Visual Studio o en tablas en la cuenta de almacenamiento. datos de hello tooview en un informe, abra **Explorer nube** o **Explorador de servidores**, abra el acceso directo de hello del nodo de hello para el rol de Hola que le interese y, a continuación, elija **ver datos de diagnóstico** .
   
    ![Ver datos de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Aparece un informe que muestra los datos disponibles de Hola.
   
    ![Informe de diagnósticos de Microsoft Azure en Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Si no aparecen los datos más recientes de hello, podría tener toowait para tooelapse período de transferencia de Hola.
   
    Elija hello **actualizar** vincular los datos de tooimmediately actualización hello, o elegir un intervalo de hello **actualización automática** lista desplegable lista cuadro toohave Hola datos se actualicen automáticamente. datos de error de hello tooexport, elija hello **exportar tooCSV** botón toocreate un archivo de valores separados por comas se pueden abrir en una hoja de cálculo.
   
    En **nube explorador** o **Explorador de servidores**, abra la cuenta de almacenamiento de Hola que esté asociada con la implementación de Hola.
3. Abrir tablas de diagnósticos de hello en el Visor de la tabla de hello y, a continuación, revise los datos de Hola que haya recopilado. Para los registros de IIS y los registros personalizados, puede abrir un contenedor de blobs. Si revisa hello en la tabla siguiente, encontrará Hola tabla o contenedor de blobs que contiene datos de Hola que le interese. Además toohello datos para que el archivo de registro, las entradas de tabla de hello contienen EventTickCount, DeploymentId, Role y toohelp RoleInstance identificar qué máquina virtual y el rol genera datos de Hola y cuándo. 
   
   | Datos de diagnóstico | Descripción | La ubicación |
   | --- | --- | --- |
   | Registros de aplicación |Registra que el código se genera mediante una llamada a métodos de hello clase System.Diagnostics.Trace. |WADLogsTable |
   | Registros de eventos |Estos datos son de registros de eventos de Windows hello en máquinas virtuales de Hola. Windows almacena información en estos registros, pero las aplicaciones y servicios también usarlos tooreport errores o información de registro. |WADWindowsEventLogsTable |
   | Contadores de rendimiento |Puede recopilar datos de cualquier contador de rendimiento que está disponible en la máquina virtual de Hola. sistema operativo de Hello proporciona contadores de rendimiento, que incluyen muchas estadísticas como el tiempo de procesador y el uso de memoria. |WADPerformanceCountersTable |
   | Registros de infraestructura |Estos registros se generan a partir de la propia infraestructura de diagnóstico Hola. |WADDiagnosticInfrastructureLogsTable |
   | Registros IIS |Estos registros registran solicitudes web. Si su servicio en la nube obtiene una cantidad importante de tráfico, estos registros pueden ser bastante largos, por lo que debe recopilar y almacenar estos datos solo cuando los necesite. |Puede encontrar registros de solicitudes con error en el contenedor de blobs de hello en wad-iis-failedreqlogs bajo una ruta de acceso para esa implementación, rol e instancia. Puede encontrar registros completos en wad-iis-logfiles. Entradas de cada archivo se realizan en la tabla WADDirectories de Hola. |
   | Volcados de memoria |Esta información ofrece imágenes binarias del proceso del servicio en la nube (normalmente un rol de trabajo). |contenedor de blobs de wad-crush-dumps |
   | Archivos de registro personalizados |Registros de datos que ha predefinido. |Puede especificar en ubicación de Hola de código personalizado de archivos de registro en la cuenta de almacenamiento. Por ejemplo, puede especificar un contenedor de blobs personalizado. |
4. Si se truncan los datos de cualquier tipo, puede intentar creciente búfer Hola para ese tipo de datos o reducir el intervalo de saludo entre las transferencias de datos de cuenta de almacenamiento de tooyour Hola máquina virtual.
5. (opcional) Purgar datos desde almacenamiento de hello en ocasiones cuenta tooreduce los costes generales de almacenamiento.
6. Cuando realice una implementación completa, archivo de hello diagnostics.cscfg (.wadcfgx para Azure SDK 2.5) se actualiza en Azure y su servicio de nube recoge cualquier configuración de diagnóstico de tooyour de cambios. Si, en su lugar, actualiza una implementación existente, archivo de .cscfg de hello no se actualiza en Azure. Todavía puede cambiar la configuración de diagnósticos, no obstante, siguiendo los pasos de hello en la sección siguiente Hola. Para obtener más información sobre cómo realizar una implementación completa y actualizar una implementación existente, vea [Asistente Publicar aplicaciones de Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>datos de diagnóstico de máquina virtual de tooview
1. En el menú contextual de hello para la máquina virtual de hello, elija **ver datos de diagnóstico**.
   
    ![Ver datos de diagnóstico en la máquina virtual de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Se abrirá hello **resumen de diagnóstico** ventana.
   
    ![Resumen de diagnóstico de máquina virtual de Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Si no aparecen los datos más recientes de hello, podría tener toowait para tooelapse período de transferencia de Hola.
   
    Elija hello **actualizar** vincular los datos de tooimmediately actualización hello, o elegir un intervalo de hello **actualización automática** lista desplegable lista cuadro toohave Hola datos se actualicen automáticamente. datos de error de hello tooexport, elija hello **exportar tooCSV** botón toocreate un archivo de valores separados por comas se pueden abrir en una hoja de cálculo.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Configurar el diagnóstico de servicio en la nube después de la implementación
Si está investigando un problema con un servicio de nube que ya está ejecutando, conviene toocollect datos que especificó antes de el rol de hello originalmente implementada. En este caso, puede iniciar toocollect esos datos mediante la configuración de hello en el Explorador de servidores. Puede configurar diagnósticos para una sola instancia o de todas las instancias de hello en un rol, dependiendo de si abre el cuadro de diálogo de configuración de diagnóstico de hello en menú contextual Hola instancia Hola o el rol de Hola. Si configura el nodo de rol de hello, los cambios aplican tooall instancias. Si configura el nodo de la instancia de hello, los cambios aplican toothat instancia única.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>tooconfigure diagnósticos para un servicio en ejecución en la nube
1. En el Explorador de servidores, expanda hello **servicios en la nube** nodo y a continuación, expanda el rol de Hola de toolocate de nodos o la instancia que desea tooinvestigate o ambos.
   
    ![Configuración de diagnósticos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. En el menú contextual de Hola para un nodo de instancia o un nodo de rol, elija **actualizar valores de diagnóstico**y, a continuación, elija Hola configuración de diagnóstico que desea toocollect.
   
    Para obtener información sobre opciones de configuración de hello, consulte **configurar orígenes de datos de diagnóstico** en este tema. Para obtener información acerca de cómo tooview Hola datos de diagnóstico, vea **ver datos de diagnóstico de hello** en este tema.
   
    Si cambia la colección de datos en el **Explorador de servidores**, estos cambios permanecerán en vigor hasta que vuelva a implementar totalmente su servicio en la nube. Si utiliza configuración de publicación predeterminada de hello, cambios de hello no se sobrescriben, puesto que la publicación Hola predeterminada configuración es implementación existente de tooupdate hello, en lugar de hacer una implementación completa. configuración de Hola de toomake seguro de que se borra durante la implementación, vaya toohello **configuración avanzada** ficha en el Asistente para publicación de Hola y Hola desactive **actualización de la implementación** casilla de verificación. Si vuelve a implementar con esa casilla borrada, configuración de hello revierte toothose en archivo wadcfgx (o .wadcfg) de hello como conjunto a través del editor de propiedades de hello para el rol de Hola. Si actualiza su implementación, Azure mantiene la configuración anterior de Hola.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Solucionar problemas del servicio en la nube de Azure
Si experimenta problemas con los proyectos de servicio en la nube, como un rol que se queda bloqueado en un estado "ocupado", se recicla repetidamente o produce un error interno del servidor, existen herramientas y técnicas que puede usar toodiagnose y corregir estos problemas. Para ver ejemplos específicos de problemas comunes y soluciones, así como información general de conceptos de Hola y herramientas usa toodiagnose y corregir estos errores, vea [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Preguntas y respuestas
**¿Qué es el tamaño del búfer de Hola y cómo debería ser?**

En cada instancia de máquina virtual, las cuotas limitan cuántos datos de diagnóstico pueden almacenarse en el sistema de archivos local de Hola. Además, especifique un tamaño de búfer para cada tipo de datos de diagnóstico que está disponible. Este tamaño de búfer actúa como una cuota individual para ese tipo de datos. Comprobando la parte inferior de Hola Hola del cuadro de diálogo, puede determinar Hola cuota total y cantidad de Hola de memoria que queda. Si se especifican búferes mayores o más tipos de datos, se alcanzará Hola cuota total. Puede cambiar Hola cuota total modificando el archivo de configuración de hello diagnostics.wadcfg/.wadcfgx. datos se almacenan en el diagnóstico de Hola Hola mismo sistema de archivos como datos de la aplicación, por lo que si la aplicación utiliza una gran cantidad de espacio en disco, no se incrementa Hola cuota de diagnóstico total.

**¿Cuál es el período de transferencia de Hola y cuánto tiempo debería ser?**

período de transferencia de Hello es la cantidad de Hola de tiempo que transcurre entre los datos de captura. Después de cada período de transferencia, los datos se mueven desde el sistema de archivos local de hello en una máquina virtual tootables en su cuenta de almacenamiento. Si cantidad Hola de datos que se recopilan supera la cuota de hello antes del fin Hola de un período de transferencia, se descartan los datos más antiguos. Conviene período de transferencia de hello toodecrease si pierde datos porque los datos superan el tamaño del búfer de Hola u Hola cuota total.

**¿Qué zona horaria son Hola marcas de tiempo en?**

marcas de tiempo de Hello están en la zona horaria local Hola Hola del centro de datos que hospeda el servicio de nube. Hello siguientes tres columnas de marca de tiempo en tablas de registro de hello se utilizan.

* **PreciseTimeStamp** es Hola ETW marca de tiempo del evento de Hola. Es decir, se registra el evento de Hola de tiempo de Hola desde el cliente de Hola.
* **Marca de tiempo** es PreciseTimeStamp redondeado hacia abajo toohello límite de frecuencia de carga. Por lo tanto, si la frecuencia de carga es 5 minutos y eventos de hello hora 00:17:12, marca de tiempo será 00:15:00.
* **Marca de tiempo** es marca de tiempo de hello en qué Hola entidad creada en hello tabla de Azure.

**¿Cómo administrar los costos al recopilar información de diagnóstico?**

Hola configuración predeterminada (**nivel de registro** establecido demasiado**Error** y **período de transferencia** establecido demasiado**1 minuto**) están diseñada toominimize costo. Sus gastos de proceso aumentará si recopilar más datos de diagnóstico o reducir el período de transferencia de Hola. No recopile más datos de los que necesita y no olvide toodisable la recopilación de datos cuando ya no lo necesite. Puede siempre habilitarlo de nuevo, incluso en tiempo de ejecución, como se muestra en la sección anterior de Hola.

**¿Cómo recopilo registros de solicitudes con error de IIS?**

De forma predeterminada, IIS no recopila registros de solicitud con error. Puede configurar toocollect IIS ellos si edita Hola archivo web.config para su rol web.

**No estoy obteniendo información de seguimiento desde métodos RoleEntryPoint como OnStart. ¿Cuál es el problema?**

métodos de Hola de RoleEntryPoint se invocan en el contexto de Hola de WAIISHost.exe, no IIS. Por lo tanto, Hola información de configuración en el archivo web.config que normalmente no se aplica habilita la traza. tooresolve este problema, agregue un proyecto de rol .config archivo tooyour web y nombre hello archivo toomatch Hola ensamblado de salida que contiene código de hello RoleEntryPoint. En el proyecto de rol web de hello predeterminado el nombre de hello del archivo .config de hello sería WAIISHost.exe.config. A continuación, agregue Hola líneas toothis archivo siguiente:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Ahora, en hello **propiedades** (ventana), conjunto hello **copiar tooOutput directorio** propiedad demasiado**copiar siempre**.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de los diagnósticos de registro en Azure, consulte [habilitar diagnósticos en servicios en la nube y máquinas virtuales](cloud-services/cloud-services-dotnet-diagnostics.md) y [habilitar el registro de diagnósticos para aplicaciones web en el servicio de aplicaciones de Azure](app-service-web/web-sites-enable-diagnostic-log.md).

