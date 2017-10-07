---
title: "aaaTroubleshooting almacenamiento de Azure con diagnósticos y analizador de mensajes | Documentos de Microsoft"
description: "Tutorial en el que se explica cómo solucionar problemas totalmente por medio del análisis de Almacenamiento de Azure, AzCopy y el analizador de mensajes de Microsoft."
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 6b23cba5-0d53-439e-870b-de8e406107d8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 74ee126bab30b9a45f4904a065b6fe3006f76101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Solución integral de problemas mediante los registros y las métricas de Azure Storage, AzCopy y el analizador de mensajes
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

## <a name="overview"></a>Información general
Poder diagnosticar y solucionar problemas es una habilidad clave a la hora de crear y mantener aplicaciones de cliente con el servicio Almacenamiento de Microsoft Azure. Debido a la naturaleza toohello distribuida de una aplicación de Azure, diagnosticar y solucionar problemas de rendimiento y errores pueden ser más complejos que en los entornos tradicionales.

En este tutorial, demostraremos cómo tooidentify cliente algunos errores que pueden afectar al rendimiento y solucionar los errores de principio a fin mediante las herramientas proporcionadas por Microsoft y el almacenamiento de Azure, en aplicación de cliente de orden toooptimize Hola.

Aquí encontrará un análisis práctico de un escenario de solución integral de problemas. Para una aplicación de almacenamiento de Azure de tootroubleshooting guía conceptual detallada, vea [supervisar, diagnosticar y solucionar problemas de almacenamiento de Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Herramientas para solucionar problemas de aplicaciones de Almacenamiento de Azure
las aplicaciones cliente de tootroubleshoot con almacenamiento de Microsoft Azure, puede usar una combinación de herramientas toodetermine cuando se ha producido un problema y qué causa Hola de problema de hello puede ser. Estas herramientas son:

* **Análisis de almacenamiento de Azure**. [Análisis de almacenamiento de Azure](http://msdn.microsoft.com/library/azure/hh343270.aspx) proporciona las métricas y registros del servicio Almacenamiento de Azure.

  * **métricas de almacenamiento** realizan un seguimiento de las métricas de transacciones y de capacidad relativas a la cuenta de almacenamiento. Usar las métricas, puede determinar el rendimiento de la aplicación correspondiente tooa diversas medidas distintas. Vea [esquema de tabla de métricas de análisis de almacenamiento](http://msdn.microsoft.com/library/azure/hh343264.aspx) para obtener más información acerca de los tipos de Hola de métricas que se hace un seguimiento mediante el análisis de almacenamiento.
  * **El registro de almacenamiento** registra cada registro de solicitudes de toohello el almacenamiento de Azure servicios tooa en el servidor. Hola registro pistas datos detallados de cada solicitud, incluidos la operación de hello realizadas, estado de Hola de operación de Hola y obtener información de latencia. Vea [formato de registro de análisis de almacenamiento](http://msdn.microsoft.com/library/azure/hh343259.aspx) para obtener más información sobre los datos de solicitud y respuesta de Hola que se escriben los registros de toohello análisis de almacenamiento.

> [!NOTE]
> Cuentas de almacenamiento con un tipo de replicación de almacenamiento con redundancia de zona (ZRS) no tiene las métricas de Hola o capacidad de registro habilitada en este momento.
>
>

* **Portal de Azure clásico**. Puede configurar las métricas y registro de la cuenta de almacenamiento en hello [Portal clásico de Azure](https://manage.windowsazure.com). También puede ver diagramas y gráficos que muestran el rendimiento de la aplicación con el tiempo y configurar toonotify alertas que si la aplicación funciona de manera diferente que esperaba de una métrica especificada.

    Vea [supervisar una cuenta de almacenamiento en el Portal de Azure hello](storage-monitor-storage-account.md) para obtener información acerca de cómo configurar la supervisión en hello Portal clásico de Azure.
* **AzCopy**. Registros del servidor para el almacenamiento de Azure se almacenan como blobs, por lo que puede usar directorio local del tooa de blobs de AzCopy toocopy Hola registro para el análisis mediante el analizador de mensajes de Microsoft. Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) para obtener más información acerca de AzCopy.
* **Analizador de mensajes de Microsoft**. Analizador de mensajes es una herramienta que consume los archivos de registro y muestra los datos de registro en un formato visual que resulta fácil toofilter, búsqueda y registrar los datos en conjuntos útiles que puede usar tooanalyze errores y problemas de rendimiento de grupo. Vea la [Guía de funcionamiento del analizador de mensajes de Microsoft](http://technet.microsoft.com/library/jj649776.aspx) para más información sobre el analizador de mensajes.

## <a name="about-hello-sample-scenario"></a>Acerca de escenario de ejemplo de Hola
Para este tutorial, analizaremos un escenario donde las métricas de Almacenamiento de Azure indican una tasa de éxito de bajo porcentaje de una aplicación que llama a Almacenamiento de Azure. Hola métrica de velocidad de porcentaje de operaciones correctas baja (se muestra como **PercentSuccess** en hello Portal clásico de Azure y en tablas de métricas de hello) realiza un seguimiento de las operaciones que se realice correctamente, pero que devuelven un código de estado HTTP es mayor que 299. En archivos de registro de almacenamiento de servidor de hello, estas operaciones se registran con un estado de transacción **ClientOtherErrors**. Para obtener más información acerca de la métrica de éxito de porcentaje bajo de hello, consulte [métricas muestran PercentSuccess baja o las entradas del registro de análisis tienen operaciones con el estado de transacción de ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Como parte de su funcionalidad habitual, es posible que las operaciones de Almacenamiento de Azure devuelvan códigos de estado HTTP mayores que 299. Pero estos errores en algunos casos indican que es posible que pueda toooptimize la aplicación de cliente para un rendimiento mejorado.

En este escenario, utilizaremos un toobe de tasa de éxito de porcentaje bajo nada inferiores al 100%. Puede elegir un nivel métrico diferentes, sin embargo, según las necesidades de tooyour. Le recomendamos que, mientras esté probando la aplicación, establezca una tolerancia de línea de base de las métricas de rendimiento clave. Según las pruebas que haga, puede establecer que la aplicación tenga una tasa de porcentaje de éxito constante de, por ejemplo, un 90% o de un 85%. Si los datos de métricas muestran que la aplicación hello se desvían de ese número, puede investigar lo que puedan estar causando Hola aumento.

Para nuestro escenario de ejemplo, una vez que se ha establecido que métrica de velocidad de porcentaje de operaciones correctas de hello es inferior al 100%, se examinará Hola registra toofind Hola los errores que se correlacionan métricas toohello y usarlos toofigure qué está causando tasa de éxito por ciento inferior de Hola. Echemos un vistazo específicamente errores en el intervalo de 400 Hola. Después, revisaremos con más detalle los errores 404 (no encontrado).

### <a name="some-causes-of-400-range-errors"></a>Algunas de las causas de los errores del intervalo 400
ejemplos de Hello siguientes se muestra un muestreo de algunos errores de intervalo de 400 para las solicitudes en el almacenamiento de blobs de Azure y sus causas posibles. Cualquiera de estos errores, así como los errores en el intervalo de 300 de Hola y Hola intervalo 500, pueden contribuir tasa de éxito de porcentaje bajo de tooa.

Tenga en cuenta que Hola listas siguientes están lejos completa. Vea [estado y códigos de Error](http://msdn.microsoft.com/library/azure/dd179382.aspx) para obtener más información acerca de errores generales de almacenamiento de Azure y tooeach específico de errores de servicios de almacenamiento de Hola.

**Ejemplos de código de estado 404 (no encontrado)**

Se produce cuando se produce un error en una operación de lectura en un contenedor o blob porque no se encuentra el blob de Hola o contenedor.

* Se produce cuando otro cliente elimina un contenedor o un blob antes de realizar la solicitud.
* Se produce si usa una llamada de API que crea el contenedor de Hola o blob después de comprobar si existe. Hola CreateIfNotExists APIs realizar un encabezado llamada toocheck primera existencia de Hola de hello contenedor o blob; Si no existe, se devuelve un error 404 y, a continuación, se realiza una segunda llamada PUT toowrite Hola contenedor o blob.

**Ejemplos de código de estado de 409 (conflicto)**

* Se produce si usa un toocreate de API de crear un nuevo contenedor o blob, sin comprobar existencia en primer lugar, y un contenedor o blob con ese nombre ya existe.
* Se produce si se está eliminando un contenedor y se intenta realizar un nuevo contenedor con el mismo nombre antes de que finalice la operación de eliminación de Hola de hello toocreate.
* Se produce si especifica una concesión en un contenedor o un blob y ya hay una concesión.

**Ejemplos de código de estado 412 (error de condición previa)**

* Se produce cuando no se cumplió la condición de hello especificada por un encabezado condicional.
* Se produce cuando el identificador de concesión de hello especificado no coincide con el identificador de concesión Hola Hola contenedor o blob.

## <a name="generate-log-files-for-analysis"></a>Generar archivos de registro para el análisis
En este tutorial, usaremos toowork analizador de mensajes con tres tipos diferentes de archivos de registro, aunque puede elegir toowork con cualquiera de ellos:

* Hola **registro del servidor**, que se crea cuando se habilita el registro de almacenamiento de Azure. registro de servidor de Hello contiene datos sobre cada operación llamado en uno de los servicios de almacenamiento de Azure de hello: blob, cola, tabla y archivo. registro de servidor Hello indica qué operación se llamó y el código de estado fue devueltas, así como otros detalles sobre Hola solicitud y respuesta.
* Hola **registro de cliente de .NET**, que se crea cuando se habilita el registro de cliente desde dentro de la aplicación. NET. registro de cliente de Hello incluye información detallada acerca de cómo cliente hello prepara la solicitud de Hola y recibe y procesa la respuesta de Hola.
* Hola **registro de seguimiento de red HTTP**, que recopila datos en HTTP/HTTPS solicitud y respuesta datos, incluidos los de operaciones en el almacenamiento de Azure. En este tutorial, se generará el seguimiento de la red de Hola a través de analizador de mensajes.

### <a name="configure-server-side-logging-and-metrics"></a>Configurar el registro y las métricas del lado servidor
En primer lugar, necesitaremos tooconfigure el registro de almacenamiento de Azure y las métricas, por lo que tiene datos de tooanalyze de aplicación de cliente de Hola. Puede configurar el registro y métricas de varias maneras: a través de hello [Portal clásico de Azure](https://manage.windowsazure.com), mediante el uso de PowerShell, o mediante programación. Consulte [Habilitar las métricas de almacenamiento y ver los datos de métricas](http://msdn.microsoft.com/library/azure/dn782843.aspx) y [Habilitar el almacenamiento de registro y obtener acceso a los datos de registro](http://msdn.microsoft.com/library/azure/dn782840.aspx) para obtener más información sobre la configuración del registro y las métricas.

**A través de hello Portal clásico de Azure**

tooconfigure registro y métricas para la cuenta de almacenamiento mediante el portal de hello, siga las instrucciones de hello en [supervisar una cuenta de almacenamiento en el Portal de Azure hello](storage-monitor-storage-account.md).

> [!NOTE]
> No es posible tooset métricas por minuto con hello Portal clásico de Azure. Sin embargo, se recomienda que establecerlos para fines de Hola de este tutorial y para investigar los problemas de rendimiento con la aplicación. Puede establecer las métricas de minuto con PowerShell tal como se muestra a continuación, o mediante programación o a través de Hola Portal clásico de Azure.
>
> Tenga en cuenta que Hola Portal clásico de Azure no puede mostrar métricas por minuto, solo las métricas por hora.
>
>

**Con PowerShell**

tooget a trabajar con PowerShell de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

1. Hola de uso [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) tooadd cmdlet toohello ventana de PowerShell de la cuenta de su usuario de Azure:

    ```powershell
     Add-AzureAccount
    ```

2. Hola **iniciar sesión en Azure tooMicrosoft** ventana, escriba Hola dirección de correo electrónico y contraseña asociadas a su cuenta. Azure autentica y guarda la información de credenciales de hello y, a continuación, cierra la ventana hello.
3. Establecer Hola cuenta toohello almacenamiento cuenta de almacenamiento predeterminada que usa para el tutorial de hello mediante la ejecución de estos comandos en la ventana de PowerShell de hello:

    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Habilitar el registro de hello servicio Blob de almacenamiento:

    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Habilitar las métricas de almacenamiento para hello servicio de Blob, que realiza seguro tooset **- MetricsType** demasiado`Minute`:

    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Configurar el registro del lado cliente de .NET
el registro para una aplicación. NET, tooconfigure del lado cliente habilitar los diagnósticos de .NET en hello del archivo de configuración (app.config o web.config). Vea [registro con hello biblioteca de cliente de almacenamiento en el lado de cliente](http://msdn.microsoft.com/library/azure/dn782839.aspx) y [lado cliente registro con hello SDK de almacenamiento de Microsoft Azure para Java](http://msdn.microsoft.com/library/azure/dn782844.aspx) para obtener más información.

registro del lado cliente Hello incluye información detallada acerca de cómo cliente hello prepara la solicitud de Hola y recibe y procesa la respuesta de Hola.

Hola biblioteca cliente de almacenamiento almacena datos del registro de cliente en la ubicación de hello especificada en el archivo de configuración de la aplicación hello (app.config o web.config).

### <a name="collect-a-network-trace"></a>Recopilar un seguimiento de red
Puede usar el analizador de mensajes toocollect un seguimiento de red HTTP/HTTPS mientras se ejecuta la aplicación cliente. Usos de analizador de mensajes [Fiddler](http://www.telerik.com/fiddler) en hello back-end. Antes de recopilar el seguimiento de la red de hello, recomendamos que configure Fiddler toorecord sin cifrar el tráfico HTTPS:

1. Instale [Fiddler](http://www.telerik.com/download/fiddler).
2. Inicie Fiddler.
3. Seleccione **Tools | Fiddler Options** (Herramientas | Opciones de Fiddler).
4. En el cuadro de diálogo de opciones de hello, asegúrese de que **capturar HTTPS conecta** y **descifrar el tráfico HTTPS** están seleccionadas, tal y como se muestra a continuación.

![Configurar opciones de Fiddler](./media/storage-e2e-troubleshooting-classic-portal/fiddler-options-1.png)

Para el tutorial de hello, recopilar y guardar un seguimiento de red en primer lugar en el analizador de mensajes, a continuación, crear una traza de hello análisis tooanalyze de sesión y Hola registros. toocollect un seguimiento de red en el analizador de mensajes:

1. En el analizador de mensajes, seleccione **File | Quick Trace | Unencrypted HTTPS** (Archivo | Seguimiento rápido | HTTPS sin cifrar).
2. seguimiento de Hello comenzará inmediatamente. Seleccione **detener** toostop Hola seguimiento para que podamos configurarlo tootrace únicamente el tráfico de almacenamiento.
3. Seleccione **editar** sesión de seguimiento de tooedit Hola.
4. Seleccione hello **configurar** vincular toohello derecha de hello **Microsoft-Pef-WebProxy** del proveedor de ETW.
5. Hola **configuración avanzada** cuadro de diálogo, haga clic en hello **proveedor** ficha.
6. Hola **filtro de nombre de host** , especifique los extremos de almacenamiento, separados por espacios. Por ejemplo, puede especificar los extremos de la manera siguiente: cambiar `storagesample` toohello nombre de la cuenta de almacenamiento:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Salir del cuadro de diálogo de Hola y haga clic en **reiniciar** toobegin recopilar seguimiento Hola con filtro de nombre de host de hello en su lugar, para que solo el tráfico de red de almacenamiento de Azure se incluye en el seguimiento de Hola.

> [!NOTE]
> Cuando haya terminado de recopilar el seguimiento de la red, se recomienda encarecidamente que revertir configuración Hola que puede haber cambiado el tráfico HTTPS de Fiddler toodecrypt. En el cuadro de diálogo de opciones de Fiddler hello, anule la selección de hello **capturar HTTPS conecta** y **descifrar el tráfico HTTPS** casillas de verificación.
>
>

Vea [usar las características de seguimiento de red de hello](http://technet.microsoft.com/library/jj674819.aspx) en Technet para obtener más detalles.

## <a name="review-metrics-data-in-hello-azure-classic-portal"></a>Revise los datos de métricas de hello Portal clásico de Azure
Una vez que la aplicación se ha estado ejecutando durante un período de tiempo, puede revisar los gráficos de métricas de Hola que aparecen en hello Portal clásico de Azure tooobserve cómo realizar el servicio. En primer lugar, vamos a agregar hello **porcentaje de éxito** toohello métrica supervisión página:

1. Navegue toohello panel para su cuenta de almacenamiento en hello [Portal clásico de Azure](https://manage.windowsazure.com), a continuación, seleccione **Monitor** hello tooview página de supervisión.
2. Haga clic en **agregar métricas** toodisplay hello **elegir métricas** cuadro de diálogo.
3. Desplácese hacia abajo en hello toofind **porcentaje de éxito** grupo, expándalo y, a continuación, seleccione **agregado**, tal y como se muestra en figura Hola siguiente. Con esta métrica se agregan los datos de porcentaje de éxito de todas las operaciones de Blob.

![Elegir métricas](./media/storage-e2e-troubleshooting-classic-portal/choose-metrics-portal-1.png)

Hola Portal clásico de Azure, ahora verá **porcentaje de éxito** Hola gráfico de supervisión, junto con las otras métricas que puedas haber agregado (seguridad toosix puede mostrarse en hello gráfico a la vez). En la imagen de Hola a continuación, puede ver que esa tasa de éxito de porcentaje de hello es ligeramente inferiores al 100%, que es el escenario de Hola que se deberá investigar a continuación mediante el análisis de registros de hello en el analizador de mensajes:

![Gráfico de métricas del portal](./media/storage-e2e-troubleshooting-classic-portal/portal-metrics-chart-1.png)

Para obtener más información sobre cómo agregar página de supervisión de toohello de métricas, vea [Cómo: agregar la tabla de métricas de métricas toohello](storage-monitor-storage-account.md#add-metrics-charts-to-the-portal-dashboard).

> [!NOTE]
> Después de habilitar las métricas de almacenamiento puede tardar algún tiempo antes de su tooappear de datos de métricas en hello Portal clásico de Azure. Esto es porque las métricas por hora de hello hora anterior no se muestran en hello Portal clásico de Azure hasta que no Hola transcurra la hora actual. Además, no se muestran métricas por minuto en hello Portal clásico de Azure. Por lo que dependiendo de si habilitar las métricas, puede tardar hasta datos de métricas de toosee tootwo horas.
>
>

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Utilizar AzCopy toocopy registros server tooa directorio local
Almacenamiento de Azure escribe tooblobs de datos de registro de servidor, mientras que las métricas se escriben tootables. Blobs del registro están disponibles en hello conocido `$logs` contenedor para la cuenta de almacenamiento. Blobs del registro se denominan jerárquicamente por año, mes, día y hora, para que pueda localizar fácilmente intervalo Hola de tiempo que se va tooinvestigate. Por ejemplo, en hello `storagesample` cuenta, contenedor de Hola para blobs del registro de hello 01/02/2015, de 8-9 am, es `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. blobs individuales de Hello en este contenedor se denominan secuencialmente, comenzando con `000000.log`.

Puede usar toodownload de herramienta de línea de comandos de AzCopy Hola estos ubicación de tooa de archivos de registro de servidor de su elección en el equipo local. Por ejemplo, puede usar Hola siguiendo los archivos de registro de comando toodownload Hola para colocar las operaciones de blob que ha tardado en 2 de enero de 2015 toohello carpeta `C:\Temp\Logs\Server`; reemplazar `<storageaccountname>` con el nombre de saludo de la cuenta de almacenamiento y `<storageaccountkey>` con su tecla de acceso de cuenta:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```

AzCopy está disponible para su descarga en hello [descargas de Azure](https://azure.microsoft.com/downloads/) página. Para obtener más información sobre el uso de AzCopy, vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

Para obtener más información sobre cómo descargar los registros del lado servidor, consulte [Descarga de datos de registro del registro de almacenamiento](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Usar datos de registro de tooanalyze de analizador de mensajes de Microsoft
El analizador de mensajes de Microsoft es una herramienta para capturar, mostrar y analizar el protocolo del tráfico de mensajes, eventos y otros mensajes del sistema o de una aplicación, usando para ello escenarios de diagnóstico y de solución de problemas. Analizador de mensajes también permite tooload, agregado y analizar los datos de registro y guarda los archivos de seguimiento. Para más información sobre el analizador de mensajes, vea la [Guía de funcionamiento del analizador de mensajes de Microsoft](http://technet.microsoft.com/library/jj649776.aspx).

Analizador de mensajes incluye activos para el almacenamiento de Azure que le ayudarán a tooanalyze servidor, cliente y registros de la red. En esta sección, analizaremos cómo toouse esos tooaddress herramientas Hola problema de porcentaje bajo de operaciones correctas en Hola registros de almacenamiento.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Descargue e instale el analizador de mensajes y Hola activos de almacenamiento de Azure
1. Descargar [analizador de mensajes](http://www.microsoft.com/download/details.aspx?id=44226) de Hola Microsoft Download Center y ejecute el programa de instalación de Hola.
2. Inicie el analizador de mensajes.
3. De hello **herramientas** menú, seleccione **Asset Manager**. Hola **Asset Manager** cuadro de diálogo, seleccione **descarga**, a continuación, filtre en **el almacenamiento de Azure**. Verá Hola activos de almacenamiento de Azure, como se muestra en la siguiente imagen se Hola.
4. Haga clic en **sincronizar todos los elementos de muestra** tooinstall Hola activos de almacenamiento de Azure. activos de Hello disponibles incluyen:
   * **Reglas de Color de almacenamiento Azure:** permiten toodefine filtros especiales que usan color de texto, las reglas de color de almacenamiento de Azure y toohighlight mensajes que contienen información específica en un seguimiento de estilos de fuente.
   * **Gráficos de Almacenamiento de Azure:** los gráficos de Almacenamiento de Azure son gráficos predefinidos que en los que se trazan datos de los registro de servidor. Tenga en cuenta que toouse el almacenamiento de Azure ofrece un gráfico en este momento, es posible que solo registro de servidor de carga hello en hello cuadrícula de análisis.
   * **Analizadores de almacenamiento de Azure:** Hola Hola almacenamiento de Azure cliente de almacenamiento de Azure analizadores el análisis, el servidor y HTTP registra en orden toodisplay en hello cuadrícula de análisis.
   * **Filtros en el almacenamiento de Azure:** filtros de almacenamiento de Azure son criterios predefinidos que puede usar los datos tooquery Hola cuadrícula de análisis.
   * **Diseños de la vista de almacenamiento Azure:** diseños de la vista de almacenamiento de Azure son diseños de columna predefinidos y agrupaciones en hello cuadrícula de análisis.
5. Reinicie el analizador de mensajes después de instalar a activos Hola.

![Administrador de activos del analizador de mensajes](./media/storage-e2e-troubleshooting-classic-portal/mma-start-page-1.png)

> [!NOTE]
> Instalar todos los activos de almacenamiento de Azure Hola que se muestra para propósitos de Hola de este tutorial.
>
>

### <a name="import-your-log-files-into-message-analyzer"></a>Importar los archivos de registro al analizador de mensajes
Puede importar todos los archivos de registro guardados (del lado servidor, del lado cliente y de red) en una sola sesión en el analizador de mensajes de Microsoft para analizarlos.

1. En hello **archivo** menú en Analizador de mensajes de Microsoft, haga clic en **nueva sesión**y, a continuación, haga clic en **en blanco sesión**. Hola **nueva sesión** cuadro de diálogo, escriba un nombre para la sesión de análisis. Hola **detalles de la sesión** del panel, haga clic en hello **archivos** botón.
2. datos de seguimiento de red tooload Hola generados por el analizador de mensajes, haga clic en **agregar archivos**, busque la ubicación de toohello donde guardó el archivo .matp de la sesión de seguimiento de web, archivo de .matp de hello seleccione, y haga clic en **abrir**.
3. datos de registro de servidor de hello tooload, haga clic en **agregar archivos**, examine la ubicación de toohello donde descargó los registros de servidor, seleccione los archivos de registro de Hola Hola intervalo de tiempo que desee tooanalyze y haga clic en **abrir**. A continuación, en hello **detalles de la sesión** panel, conjunto hello **configuración de registro de texto** lista desplegable para cada archivo de registro del lado servidor demasiado**AzureStorageLog** tooensure que Microsoft Analizador de mensajes puede analizar el archivo de registro de hello correctamente.
4. datos de registro de cliente de hello tooload, haga clic en **agregar archivos**, examine la ubicación de toohello donde guardó los registros de cliente, seleccione los archivos de registro de hello desee tooanalyze y haga clic en **abiertos**. A continuación, en hello **detalles de la sesión** panel, conjunto hello **configuración de registro de texto** lista desplegable para cada archivo de registro de cliente demasiado**AzureStorageClientDotNetV4** tooensure que Analizador de mensajes de Microsoft puede analizar el archivo de registro de hello correctamente.
5. Haga clic en **iniciar** en hello **nueva sesión** diálogo tooload y el análisis Hola datos del registro. datos del registro de Hello muestran de Hola cuadrícula de análisis de analizador de mensajes.

imagen de Hola a continuación muestra una sesión en el ejemplo se configura con el servidor, cliente y archivos de registro de seguimiento de red.

![Configurar una sesión del analizador de mensajes](./media/storage-e2e-troubleshooting-classic-portal/configure-mma-session-1.png)

Tenga en cuenta que el analizador de mensajes carga los archivos en la memoria. Si tiene un conjunto grande de datos de registro, le interesará toofilter en orden tooget Hola mejor partido analizador de mensajes.

En primer lugar, determinar el período de tiempo de Hola que esté interesado en la revisión y mantener este período de tiempo tan pequeño como sea posible. En muchos casos, le interesará tooreview un punto de minutos u horas como máximo. Importar el conjunto más pequeño de Hola de registros que pueden satisfacer sus necesidades.

Si todavía tiene una gran cantidad de datos de registro, a continuación, puede que desee toospecify un toofilter de filtro de la sesión los datos de registro antes de cargarlos. Hola **sesión filtro** cuadro, seleccione hello **biblioteca** botón toochoose un filtro predefinido; por ejemplo, elegir **Global tiempo filtro I** de hello filtra el almacenamiento de Azure toofilter en un intervalo de tiempo. A continuación, puede editar Hola Hola del toospecify del criterio de filtro a partir de y finalizar la marca de tiempo para el intervalo de saludo desea toosee. También puede filtrar por un código de estado determinado; Por ejemplo, puede elegir solo entradas del registro tooload donde el código de estado de hello es 404.

Para más información sobre cómo importar datos de registro al analizador de mensajes de Microsoft, vea el tema de [recuperación de datos de mensajes](http://technet.microsoft.com/library/dn772437.aspx) en TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Usar datos de archivo registro toocorrelate de Id. de la solicitud de cliente de Hola
Hola biblioteca de cliente de almacenamiento de Azure genera automáticamente un Id. de solicitud de cliente único para cada solicitud. Este valor se escribe el registro del cliente de toohello, registro de servidor hello y seguimiento de la red de hello, por lo que se pueden usar toocorrelate datos a través de todos los registros de tres en Analizador de mensajes. Vea [Id. de solicitud de cliente](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) identificador de solicitud para obtener información adicional sobre los clientes Hola

Hello las siguientes secciones describen cómo toouse configurado previamente y las vistas de diseño personalizado toocorrelate y agrupar datos en función de la solicitud de cliente hello identificador.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Seleccione un toodisplay de diseño de la vista de hello cuadrícula de análisis
los activos de almacenamiento de Hello para el analizador de mensajes incluyen diseños de la vista del almacenamiento de Azure que corresponden a las vistas configuradas previamente que puede usar toodisplay los datos con columnas y agrupaciones útiles para diferentes escenarios. También puede crear diseños de vista personalizados y guardarlos para volver a usarlos.

Figura Hola siguiente muestra hello **vista Diseño** menú, disponible al seleccionar **diseño de la vista** desde la cinta de opciones de barra de herramientas de Hola. diseños de la vista de Hello para el almacenamiento de Azure están agrupados en hello **el almacenamiento de Azure** nodo en el menú de Hola. Puede buscar `Azure Storage` en toofilter de cuadro de búsqueda de hello en el almacenamiento de Azure ver solo los diseños. También puede seleccionar Hola estrella siguiente tooa vista Diseño toomake TI un favorito y mostrarla en la parte superior de hello del menú de Hola.

![Menú de diseño de vista](./media/storage-e2e-troubleshooting-classic-portal/view-layout-menu.png)

toobegin con select **agrupados por módulo y ClientRequestID**. Este diseño de vista agrupa los datos de registro de los tres registros de la siguiente manera: primero, por identificador de solicitud de cliente y, después, por archivo de registro de origen (o **Module** en el analizador de mensajes). Con esta vista, podrá explorar en profundidad un identificador de solicitud de cliente en particular y ver los datos de los tres archivos de registro relativos a ese identificador de solicitud de cliente.

Figura Hola siguiente muestra estos datos de registro de diseño vista aplicada toohello ejemplo, con un subconjunto de las columnas mostradas. Puede ver que para un Id. de solicitud de cliente en particular, Hola Analysis cuadrícula muestra los datos de registro de cliente de Hola y registro de servidor, seguimiento de la red.

![Diseño de vista de Almacenamiento de Azure](./media/storage-e2e-troubleshooting-classic-portal/view-layout-client-request-id-module.png)

> [!NOTE]
> Archivos de registro diferentes tienen distintas columnas, por lo que cuando se muestran datos de varios archivos de registro en hello cuadrícula de análisis, algunas columnas no pueden contener los datos de una fila determinada. Por ejemplo, en la imagen de hello anterior, las filas del registro de cliente no muestre datos para hello **Timestamp**, **TimeElapsed**, **origen**, y **destino** columnas, ya que estas columnas no existen en el registro de cliente de hello, pero existen en el seguimiento de la red de Hola. De forma similar, Hola **marca de tiempo** columna muestra los datos de marca de tiempo de registro del servidor hello, pero se muestre ningún dato para hello **TimeElapsed**, **origen**, y  **Destino** columnas, que no forman parte del registro del servidor hello.
>
>

Además diseños de la vista de almacenamiento de Azure de toousing hello, se puede definir y guardar sus propios diseños de la vista. Puede seleccionar otros campos que desee para agrupar los datos y guardar agrupación hello como parte de su diseño personalizado también.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Aplicar reglas de color toohello cuadrícula de análisis
Activos de almacenamiento de Hello también incluyen reglas de color, que ofrecen que un objeto visual significa tooidentify diferentes tipos de errores de hello cuadrícula de análisis. Hola predefinida aplicar reglas de color tooHTTP errores, para que aparezcan solo para el seguimiento de red y de registro del servidor de Hola.

Seleccione las reglas de color de tooapply **las reglas de Color** desde la cinta de opciones de barra de herramientas de Hola. Podrá ver las reglas de color del almacenamiento de Azure de hello en el menú de Hola. Para el tutorial de hello, seleccione **errores del cliente (StatusCode entre 400 y 499)**, tal y como se muestra en figura Hola siguiente.

![Diseño de vista de Almacenamiento de Azure](./media/storage-e2e-troubleshooting-classic-portal/color-rules-menu.png)

Además de hello toousing almacenamiento de Azure color reglas, también puede definir y guardar sus propias reglas de color.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Grupo y filtrar datos toofind intervalo de 400 errores del registro
A continuación, se podrá agrupar y filtrar toofind de datos de registro de hello todos los errores de intervalo de hello 400.

1. Busque hello **StatusCode** columna Hola Analysis cuadrícula, menú contextual columna de hello encabezado y, a continuación, seleccione **grupo**.
2. A continuación, agrupar por hello **ClientRequestId** columna. Verá que datos Hola Hola que Analysis cuadrícula ahora están organizado por estado de código y solicitud de cliente por identificador.
3. Mostrar ventana de herramientas de filtro de la vista de hello si no está ya visible. En la cinta de opciones de barra de herramientas de hello, seleccione **las ventanas de herramientas**, a continuación, **filtro de vista**.
4. toofilter Hola datos toodisplay intervalo de 400 solo errores del registro, agregue Hola después toohello de criterios de filtro **filtro de vista** ventana y haga clic en **aplicar**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

Figura Hola siguiente muestra los resultados de Hola de esta agrupación y filtro. Hola expansión **ClientRequestID** campo debajo Hola agrupar para el código de estado 409, por ejemplo, se muestra una operación que dieron lugar a ese código de estado.

![Diseño de vista de Almacenamiento de Azure](./media/storage-e2e-troubleshooting-classic-portal/400-range-errors1.png)

Después de aplicar este filtro, verá que se excluyen las filas del registro de cliente de hello, como Hola registro de cliente no incluye un **StatusCode** columna. toobegin con, revisaremos servidor hello y errores de 404 de toolocate de registros de seguimiento de red y, a continuación, se tendrá que volver toohello registro tooexamine Hola cliente las operaciones de cliente que ha provocado toothem.

> [!NOTE]
> También puede filtrar por hello **StatusCode** columna y muestre los datos de todos los registros de tres, incluidos Hola registro de cliente, si agrega un filtro de toohello de expresión que incluye entradas del registro donde el código de estado de hello es null. tooconstruct esta expresión de filtro, use:
>
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
>
> Este filtro devuelve todas las filas de cliente hello registro y sólo las filas de registro del servidor de Hola y de registro HTTP donde el código de estado de hello es superior a 400. Si aplica diseño de la vista de toohello agrupado por identificador de solicitud de cliente y el módulo, puede buscar o desplácese por hello registrar entradas toofind aquellos que se representan todas las tres registros.   
>
>

### <a name="filter-log-data-toofind-404-errors"></a>Filtrar 404 errores de toofind de datos de registro
los activos de almacenamiento de Hello incluyen filtros predefinidos que puede usar toonarrow registro toofind Hola errores o datos tendencias que está buscando. A continuación, se podrá aplicar dos filtros predefinidos: uno que filtra el servidor hello y los registros de seguimiento de red para 404 errores y otro que filtra los datos de hello en un intervalo de tiempo especificado.

1. Mostrar ventana de herramientas de filtro de la vista de hello si no está ya visible. En la cinta de opciones de barra de herramientas de hello, seleccione **las ventanas de herramientas**, a continuación, **filtro de vista**.
2. En la ventana de filtro de la vista de hello, seleccione **biblioteca**y buscar en `Azure Storage` hello toofind filtra el almacenamiento de Azure. Filtro de hello SELECT para **404 (no encontrado) los mensajes en todos los registros**.
3. Hola de presentación **biblioteca** menú nuevo y busque y seleccione hello **Global filtro de tiempo**.
4. Editar hello las marcas de tiempo que se muestra en el intervalo de hello filtro toohello que desea tooview. Esto le ayudará a intervalo de hello toonarrow de tooanalyze de datos.
5. El filtro debe aparecer similar toohello de ejemplo siguiente. Haga clic en **aplicar** tooapply Hola filtro toohello cuadrícula de análisis.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

![Diseño de vista de Almacenamiento de Azure](./media/storage-e2e-troubleshooting-classic-portal/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analizar los datos de registro
Ahora que ha agrupado y filtrar los datos, puede examinar los detalles de Hola de las solicitudes individuales que generó 404 errores. En el diseño de la vista actual de hello, datos de Hola se agrupan por Id. de solicitud de cliente, a continuación, por el origen del registro. Puesto que se filtra en las solicitudes donde el campo de hello StatusCode contiene 404, veremos sólo servidor hello y datos de seguimiento de red, no datos de registro de hello cliente.

Hola imagen siguiente muestra una solicitud específica donde produjo un error 404 en una operación Get Blob porque no existe el blob de Hola. Tenga en cuenta que algunas columnas se han quitado de la vista estándar de hello en los datos relevantes de orden toodisplay Hola.

![Registros de servidor y de seguimiento de red filtrados](./media/storage-e2e-troubleshooting-classic-portal/server-filtered-404-error.png)

A continuación, se podrá correlacionar este Id. de solicitud de cliente con toosee de datos de registro de cliente de hello estaba tardando qué cliente Hola de acciones cuando se ha producido un error de Hola. Puede mostrar una nueva vista de cuadrícula de análisis para esta sesión tooview Hola cliente datos del registro, que se abreen en una segunda pestaña:

1. En primer lugar, Copiar valor de Hola de hello **ClientRequestId** Portapapeles toohello de campo. Para hacer esto seleccionando cualquier fila, buscar hello **ClientRequestId** campo, haciendo doble clic en el valor de datos de Hola y elegir **copia 'ClientRequestId'**.
2. En la cinta de opciones de barra de herramientas de hello, seleccione **nuevo visor**, a continuación, seleccione **Analysis cuadrícula** tooopen una nueva pestaña Hola nueva pestaña muestra todos los datos en los archivos de registro, sin agrupar, filtrar o las reglas de color.
3. En la cinta de opciones de barra de herramientas de hello, seleccione **vista Diseño**, a continuación, seleccione **todas las columnas de cliente de .NET** en hello **el almacenamiento de Azure** sección. Este diseño de la vista muestra datos de registro de cliente de hello, así como Hola registros de seguimiento de red y el servidor. De forma predeterminada se ordena en hello **MessageNumber** columna.
4. A continuación, busque el registro del cliente de Hola Id. de solicitud de cliente de Hola. En la cinta de opciones de barra de herramientas de hello, seleccione **buscar mensajes**, a continuación, especifique un filtro personalizado del Id. de solicitud del cliente de Hola de hello **buscar** campo. Use esta sintaxis de filtro de Hola y especificar su propio Id. de solicitud de cliente:

    ```  
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Analizador de mensajes busca y selecciona la primera entrada de registro Hola donde los criterios de búsqueda de hello coincide con Id. de solicitud de cliente de Hola. En el registro de cliente de hello, hay varias entradas para cada Id. de solicitud de cliente, por lo que puede toogroup usarlas en hello **ClientRequestId** toomake de campo sea más fácil toosee ellos todos juntos. imagen de Hello siguiente muestra todos los mensajes de saludo de cliente hello de registro de hello especificado identificador de solicitud de cliente.

![Registro de cliente con errores 404](./media/storage-e2e-troubleshooting-classic-portal/client-log-analysis-grid1.png)

Con los datos de Hola que se muestra en los diseños de la vista de hello en estos dos pestañas, puede analizar Hola solicitud datos toodetermine cuál puede ser la causa errores de Hola. También puede mirar las solicitudes que precedió a este uno toosee si un evento anterior puede hayan originado el error 404 toohello. Por ejemplo, puede revisar las entradas del registro de cliente de hello anterior a este toodetermine de Id. de solicitud de cliente si el blob de Hola se haya eliminado, o si Hola error se produjo debido toohello aplicación de cliente al llamar a una API de CreateIfNotExists en un contenedor o blob. En el registro de cliente de hello, puede encontrar dirección del blob de Hola Hola **descripción** campo; en el servidor de Hola y registros de seguimiento de red, esta información aparece en hello **resumen** campo.

Una vez que sepa dirección Hola del blob de Hola que produjo el error 404 hello, puede investigar más. Si desea buscar entradas de registro de hello para otros mensajes relacionados con operaciones en hello mismo blob, puede comprobar si el cliente de hello eliminado previamente entidad Hola.

## <a name="analyze-other-types-of-storage-errors"></a>Analizar otros tipos de errores de almacenamiento
Ahora que está familiarizado con el analizador de mensajes tooanalyze los datos de registro, puede analizar los otros tipos de errores mediante vista diseños, las reglas de color y búsqueda de filtrado. Hola tablas a continuación se indican algunos problemas que pueden surgir y Hola criterios de filtro que se puede usar toolocate ellos. Para obtener más información sobre la creación de filtros y analizador de mensajes de Hola filtrado de idioma, consulte [filtrar datos de mensaje](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Use la expresión de filtro... | Expresión se aplica tooLog (cliente, servidor, red, todos) |
| --- | --- | --- |
| Retrasos inesperados en la entrega de mensajes en una cola |AzureStorageClientDotNetV4.Description contiene "Intentando de nuevo la operación con error." |Cliente |
| Aumento de HTTP en PercentThrottlingError |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |Red |
| Aumento en PercentTimeoutError |HTTP.Response.StatusCode   == 500 |Red |
| Aumento en PercentTimeoutError (todos) |*StatusCode   == 500 |Todo |
| Aumento de PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |Cliente |
| Mensajes HTTP 403 (Prohibido) |HTTP.Response.StatusCode   == 403 |Red |
| Mensajes HTTP 404 (No encontrado) |HTTP.Response.StatusCode   == 404 |Red |
| 404 (Todo) |*StatusCode   == 404 |Todo |
| Problema de autorización de la Firma de acceso compartido (SAS) |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |Red |
| Mensajes HTTP 409 (conflicto) |HTTP.Response.StatusCode   == 409 |Red |
| 409 (Todo) |*StatusCode   == 409 |Todo |
| Valor de PercentSuccess bajo o las entradas de registro de análisis tienen operaciones con el estado de transacción ClientOtherErrors |AzureStorageLog.RequestStatus ==   "ClientOtherError" |Server |
| Advertencia de Nagle |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) y (AzureStorageLog.RequestPacketSize <1460) y (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |Server |
| Intervalo de tiempo en los registros de servidor y red |#Timestamp   >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39 |Servidor, red |
| Intervalo de tiempo en registros de servidor |AzureStorageLog.Timestamp   >= 2014-10-20T16:36:38 y AzureStorageLog.Timestamp <=   2014-10-20T16:36:39 |Server |

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre los escenarios de solución integral de problemas en Almacenamiento de Azure, vea los siguientes recursos:

* [Supervisión, diagnóstico y solución de problemas de Almacenamiento de Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md)
* [Análisis de almacenamiento](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Supervisar una cuenta de almacenamiento en hello Portal de Azure](storage-monitor-storage-account.md)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)
* [Guía de funcionamiento del analizador de mensajes de Microsoft](http://technet.microsoft.com/library/jj649776.aspx)
