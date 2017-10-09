---
title: paquetes de aplicaciones de aaaInstall en nodos de proceso - Azure Batch | Documentos de Microsoft
description: "Característica de paquetes de aplicación de uso Hola de Azure Batch tooeasily administrar varias aplicaciones y nodos de ejecución de versiones para la instalación en lote."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote

característica de paquetes de aplicación Hola de lote de Azure proporciona una administración sencilla de aplicaciones de la tarea y su toohello implementación nodos de cálculo en el grupo. Con paquetes de aplicaciones, puede cargar y administrar varias versiones de aplicaciones de hello que ejecutarán sus tareas, incluidas sus archivos auxiliares. Se puede, a continuación, implementar automáticamente una o varias de estas aplicaciones toohello nodos de cálculo en el grupo.

En este artículo, aprenderá cómo tooupload y administrar paquetes de aplicación Hola portal de Azure. A continuación, aprenderá cómo tooinstall en un grupo de proceso nodos con hello [.NET de lotes] [ api_net] biblioteca.

> [!NOTE]
> 
> Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017. Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube. Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones.
>
> las API para crear y administrar paquetes de aplicación Hello forman parte de hello [.NET de administración de lotes] [[api_net_mgmt]] biblioteca. las API para la instalación de paquetes de aplicaciones en un nodo de proceso Hello forman parte del programa Hola a [.NET de lotes] [ api_net] biblioteca.  
>
> característica de paquetes de aplicación Hola aquí descrito reemplaza a la característica de aplicaciones de lote de hello disponible en versiones anteriores del servicio de Hola.
> 
> 

## <a name="application-package-requirements"></a>Requisitos de los paquetes de aplicación
paquetes de aplicaciones de toouse, necesita demasiado[vincular una cuenta de almacenamiento de Azure](#link-a-storage-account) tooyour cuenta de lote.

Esta característica se introdujo en [API de REST de lote] [ api_rest] versión 2015-12-01.2.2 y Hola correspondiente [.NET de lotes] [ api_net] versión de la biblioteca 3.1.0. Se recomienda usar siempre la última versión de la API de hello cuando se trabaja con el lote.

> [!NOTE]
> Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017. Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube. Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones.
>
>

## <a name="about-applications-and-application-packages"></a>Acerca de las aplicaciones y los paquetes de aplicación
En el lote de Azure, un *aplicación* hace referencia tooa conjunto de archivos binarios con control de versiones que pueden ser nodos de proceso toohello automáticamente descargado en el grupo. Un *paquete de aplicación* hace referencia tooa *conjunto específico* de los archivos binarios y representa un determinado *versión* de aplicación hello.

![Diagrama de alto nivel de aplicaciones y paquetes de aplicación][1]

### <a name="applications"></a>Aplicaciones
Una aplicación en el lote contiene una o más aplicaciones, paquetes y especifica las opciones de configuración para la aplicación hello. Por ejemplo, una aplicación puede especificar Hola predeterminado aplicación paquete versión tooinstall en nodos de proceso y si se pueden actualizar o eliminar sus paquetes.

### <a name="application-packages"></a>paquetes de aplicación
Un paquete de aplicación es un archivo .zip que contiene los archivos binarios de aplicación de Hola y archivos auxiliares necesarios para la aplicación de hello toorun de tareas. Cada paquete de aplicación representa una versión específica de la aplicación hello.

Puede especificar los paquetes de aplicación en los niveles de grupo y tarea de Hola. Puede especificar uno o varios de estos paquetes y (opcionalmente) una versión cuando crea un grupo o tarea.

* **Grupo de paquetes de aplicaciones** se implementan demasiado*cada* nodo de grupo de Hola. Las aplicaciones se implementan cuando un nodo se une a un grupo y cuando se reinicia o se restablece la imagen inicial.
  
    Los paquetes de aplicación de grupo son adecuados cuando todos los nodos de un grupo ejecutan las tareas de un trabajo. Puede especificar uno o más paquetes de aplicación cuando se crea un grupo y puede agregar o actualizar los paquetes de un grupo ya existente. Si actualiza los paquetes de aplicación de un grupo existente, debe reiniciar el nuevo paquete de nodos tooinstall Hola.
* **Paquetes de aplicación de tareas** se implementan solo de nodos de proceso tooa toorun una tarea programada, justo antes de ejecutar línea de comandos de la tarea hello. Si especifica Hola versión y el paquete de aplicación ya está en el nodo de hello, no se vuelve a implementar y se utiliza el paquete existente de Hola.
  
    Paquetes de aplicación de tareas son útiles en entornos de grupo compartido, donde distintos trabajos que se ejecutan en un grupo y no se elimina el grupo de hello cuando se completa un trabajo. Si el trabajo tiene menos tareas que los nodos de grupo de hello, paquetes de aplicaciones de la tarea pueden minimizar la transferencia de datos ya que la aplicación está implementada toohello solo nodos que se ejecutan las tareas.
  
    Otros escenarios que pueden beneficiarse de los paquetes de aplicación de tareas son los trabajos que ejecutan una aplicación grande, pero solo para unas pocas tareas. Por ejemplo, una fase previa al procesamiento o una tarea de mezcla, donde la aplicación de procesamiento previo o combinación de hello es pesado, puede beneficiarse del uso de paquetes de aplicaciones de la tarea.

> [!IMPORTANT]
> Hay restricciones en número de Hola de aplicaciones y paquetes de aplicaciones dentro de una cuenta de lote y en el tamaño de paquete de hello máxima de la aplicación. Vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener más información acerca de estos límites.
> 
> 

### <a name="benefits-of-application-packages"></a>Ventajas de los paquetes de aplicación
Paquetes de aplicaciones pueden simplificar código de hello en la solución de lote y el inferior Hola sobrecarga toomanage necesario hello las aplicaciones que se ejecutan las tareas.

Con paquetes de aplicaciones, tarea de inicio de la agrupación no tiene toospecify una lista larga de tooinstall de archivos de recursos individuales en nodos de Hola. No es necesario toomanually administrar varias versiones de los archivos de aplicación en el almacenamiento de Azure, o en los nodos. Y no necesita tooworry acerca de cómo generar [direcciones URL de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide acceder a los archivos de toohello en su cuenta de almacenamiento. Procesar por lotes funciona en segundo plano de hello con paquetes de aplicaciones de almacenamiento de Azure toostore e implementarlas toocompute nodos.

> [!NOTE] 
> Hello tamaño total de una tarea de inicio debe ser menor o igual too32768 caracteres, incluidos los archivos de recursos y las variables de entorno. Si la tarea de inicio supera este límite, en este caso usar paquetes de aplicación es otra opción. Puede crear un archivo comprimido que contiene los archivos de recursos, cargarlo como un almacenamiento de blob tooAzure y, a continuación, descomprímalo desde línea de comandos de saludo de la tarea de inicio. 
>
>

## <a name="upload-and-manage-applications"></a>Carga y administración de aplicaciones
Puede usar hello [portal de Azure] [ portal] o hello [.NET de administración de lotes](batch-management-dotnet.md) paquetes de aplicación de biblioteca toomanage hello en su cuenta de lote. En a continuación Hola secciones, se muestra primero cómo toolink una cuenta de almacenamiento, a continuación, analice agregando aplicaciones y paquetes y administrarlos con Hola portal.

### <a name="link-a-storage-account"></a>Vínculo a una cuenta de Almacenamiento
paquetes de aplicaciones de toouse, primero debe vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure. Si aún no ha configurado una cuenta de almacenamiento, hello portal de Azure muestra una advertencia hello primera vez que haga clic en hello **aplicaciones** el icono Servicios hello **cuenta de lote** hoja.

> [!IMPORTANT]
> Procesar por lotes admite actualmente *sólo* hello **general** tipo de cuenta de almacenamiento tal como se describe en el paso 5, [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account), en [acerca de Azure las cuentas de almacenamiento](../storage/common/storage-create-storage-account.md). Al vincular un tooyour de cuenta de almacenamiento de Azure cuenta de lote, se vinculan *sólo* una **general** cuenta de almacenamiento.
> 
> 

![Advertencia de que no hay cuentas de almacenamiento configuradas en Azure Portal][9]

Hola Hola de usos de servicio de lote había asociado toostore de cuenta de almacenamiento los paquetes de aplicaciones. Una vez haya vinculado dos cuentas de hello, lote automáticamente puede implementar paquetes de saludo almacenados en nodos de proceso de tooyour de cuenta de almacenamiento de hello vinculado. toolink un tooyour de cuenta de almacenamiento cuenta de lote, haga clic en **configuración de la cuenta de almacenamiento** en hello **advertencia** hoja y, a continuación, haga clic en **cuenta de almacenamiento** en hello **Cuenta de almacenamiento** hoja.

![Hoja Elegir de cuenta de almacenamiento en Azure Portal][10]

Se recomienda crear una cuenta de Storage *específicamente* para su uso con la cuenta de Batch y seleccionarla aquí. Para obtener más información acerca de cómo toocreate una cuenta de almacenamiento, vea "Crear una cuenta de almacenamiento" en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md). Después de crear una cuenta de almacenamiento, puede, a continuación, vincúlelo tooyour cuenta de lote mediante el uso de hello **cuenta de almacenamiento** hoja.

> [!WARNING]
> Hola servicio por lotes utiliza el almacenamiento de Azure toostore los paquetes de aplicaciones como blobs en bloques. Está [carga como normal] [ storage_pricing] para datos de blob de bloque de saludo. Estar seguro de tamaño de hello tooconsider y el número de los paquetes de aplicaciones y quitan periódicamente los costos de toominimize de los paquetes en desuso.
> 
> 

### <a name="view-current-applications"></a>Visualización de las aplicaciones actuales
las aplicaciones de hello tooview en su cuenta de lote, haga clic en hello **aplicaciones** elemento de menú en el menú de la izquierda Hola durante la visualización de hello **cuenta de lote** hoja.

![Icono Aplicaciones][2]

Al seleccionar esta opción de menú abre hello **aplicaciones** hoja:

![Lista de aplicaciones][3]

Hola **aplicaciones** hoja muestra Hola Id. de cada aplicación en su cuenta y Hola propiedades siguientes:

* **Paquetes**: Hola número de versiones asociadas a esta aplicación.
* **Versión predeterminada**: versión de la aplicación hello instalado si no indica una versión cuando se especifica la aplicación hello para un grupo. Esta configuración es opcional.
* **Permitir actualizaciones**: valor de Hola que especifica si las actualizaciones de paquete, eliminaciones y las adiciones se permiten. Si se establece demasiado**n**, paquete actualizaciones y eliminaciones se deshabilitan para la aplicación hello. Solo se pueden agregar versiones nuevas del paquete de aplicación. valor predeterminado de Hello es **Sí**.

### <a name="view-application-details"></a>Visualización de los detalles de una aplicación
hoja de hello tooopen que incluye detalles de Hola para una aplicación de la aplicación, seleccione Hola Hola **aplicaciones** hoja.

![Detalles de la aplicación][4]

En la hoja de detalles de la aplicación de hello, puede configurar Hola siguientes opciones para la aplicación.

* **Permitir actualizaciones**: especifica si se pueden actualizar o eliminar sus paquetes de aplicación. Consulte "Actualización o eliminación de un paquete de aplicación" más adelante en este artículo.
* **Versión predeterminada**: especificar un nodos de toocompute predeterminados toodeploy de paquete de aplicación.
* **Nombre para mostrar**: especificar descriptivo nombre que el lote de solución puede utilizar cuando se muestra información acerca de la aplicación hello, por ejemplo, en hello interfaz de usuario de un servicio que proporciona a los clientes de tooyour a través de lote.

### <a name="add-a-new-application"></a>Adición de una nueva aplicación
toocreate una nueva aplicación, agregue un paquete de aplicación y especifique un identificador de aplicación nueva y única. Hola primer paquete de la aplicación que se agrega con el nuevo identificador de aplicación Hola también crea Hola nueva aplicación.

Haga clic en **agregar** en hello **aplicaciones** Hola de hoja tooopen **nueva aplicación** hoja.

![Hoja Nueva aplicación en Azure Portal][5]

Hola **nueva aplicación** hoja proporciona la configuración de Hola de toospecify de la nueva aplicación y el paquete de aplicación de los campos siguientes de Hola.

**Id. de la aplicación**

Este campo especifica el Id. de saludo de la nueva aplicación, que es de reglas de validación de Id. de lote de Azure estándares de asunto toohello. reglas de Hola para proporcionar un identificador de aplicación son los siguientes:

* En los nodos de Windows, el identificador de hello puede contener cualquier combinación de caracteres alfanuméricos, guiones y caracteres de subrayado. En los nodos de Linux, solo se permiten caracteres alfanuméricos y caracteres de subrayado.
* No pueden contener más de 64 caracteres.
* Debe ser único dentro de hello cuenta de lote.
* Conserva las mayúsculas y minúsculas, aunque no las distingue.

**Versión**

Este campo especifica la versión de Hola Hola del paquete de aplicación que va a cargar. Cadenas de versión son toohello asunto siguiendo las reglas de validación:

* En los nodos de Windows, la cadena de versión de Hola puede contener cualquier combinación de caracteres alfanuméricos, guiones, caracteres de subrayado y puntos. En los nodos de Linux, la cadena de versión de Hola puede contener solo caracteres alfanuméricos y caracteres de subrayado.
* No pueden contener más de 64 caracteres.
* Debe ser único dentro de la aplicación hello.
* Conservan las mayúsculas y minúsculas, aunque no las distinguen.

**Paquete de aplicación**

Este campo especifica el archivo .zip de Hola que contiene los archivos binarios de aplicación de Hola y archivos auxiliares que son de la aplicación hello tooexecute necesarios. Haga clic en hello **seleccionar un archivo** cuadro o hello tooand de toobrowse del icono de carpeta seleccione un archivo .zip que contiene archivos de la aplicación.

Después de seleccionar un archivo, haga clic en **Aceptar** toobegin Hola carga tooAzure almacenamiento. Una vez completada la operación de carga de hello, portal de hello muestra una notificación y cierra la hoja de Hola. Función tamaño Hola de archivo hello que son hello y carga de velocidad de la conexión de red, esta operación puede tardar algún tiempo.

> [!WARNING]
> No cierre hello **nueva aplicación** hoja antes de que finalice la operación de carga de Hola. Si lo hace, se detendrá el proceso de carga de Hola.
> 
> 

### <a name="add-a-new-application-package"></a>Adición de un nuevo paquete de aplicación
tooadd una nueva versión del paquete de aplicación para una aplicación existente, seleccione una aplicación Hola **aplicaciones** hoja, haga clic en **paquetes**, a continuación, haga clic en **agregar** tooopen Hola **Agregar paquete** hoja.

![Hoja Agregar paquete de aplicación en Azure Portal][8]

Como puede ver, los campos de hello coinciden con los de hello **nueva aplicación** hoja, pero hello **Id. de aplicación** casilla está deshabilitada. Tal y como lo hizo para aplicación Hola, especifique hello **versión** para el nuevo paquete, examinar tooyour **paquete de aplicación** .zip de archivos, a continuación, haga clic en **Aceptar** hello tooupload paquete.

### <a name="update-or-delete-an-application-package"></a>Actualización o eliminación de un paquete de aplicación
tooupdate o eliminar un paquete de aplicación existente, hoja de detalles de hello abierto para la aplicación hello, haga clic en **paquetes** tooopen hello **paquetes** hoja, haga clic en hello **puntos suspensivos**de fila Hola Hola del paquete de aplicación que desee toomodify y seleccionar acción de Hola que desea tooperform.

![Actualizar o eliminar paquete en Azure Portal][7]

**Actualizar**

Al hacer clic en **actualización**, hello *paquete de actualización* hoja se muestra. Esta hoja es similar toohello *nuevo paquete de aplicación* hoja, el campo de selección del paquete de hello sin embargo, solo está habilitado, lo que le toospecify un nuevo tooupload del archivo ZIP.

![Hoja Actualizar paquete en Azure Portal][11]

**Eliminar**

Al hacer clic en **eliminar**, se le pedirá la eliminación de hello tooconfirm de versión del paquete de Hola y paquete Hola de eliminaciones por lotes de almacenamiento de Azure. Si elimina la versión de Hola predeterminada de una aplicación, Hola **versión predeterminada** configuración se quita de la aplicación hello.

![Eliminar aplicación][12]

## <a name="install-applications-on-compute-nodes"></a>Instalación de aplicaciones en nodos de proceso
Ahora que ha aprendido cómo paquetes de la aplicación toomanage con hello portal de Azure, veremos cómo toodeploy les toocompute nodos y ejecutarlos con las tareas por lotes.

### <a name="install-pool-application-packages"></a>Instalación de paquetes de aplicación de grupos
tooinstall un paquete de aplicación en todos los nodos de cálculo en un grupo, especifique uno o más paquetes de aplicación *referencias* para el grupo de Hola. paquetes de aplicación Hola que especifique para un grupo se instalan en cada nodo de ejecución cuando une a ese nodo grupo de Hola y al nodo de Hola se reinicia o se restablece la imagen inicial.

En el entorno de .NET para Batch, especifique una o varias [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] al crear el grupo o para un grupo existente. Hola [ApplicationPackageReference] [ net_pkgref] clase especifica un identificador de la aplicación y la versión tooinstall en un grupo de nodos de proceso.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Si se produce un error en una implementación de paquete de aplicación por algún motivo, marcas de servicio de lote de Hola Hola nodo [inutilizable][net_nodestate], y no las tareas se programan para su ejecución en ese nodo. En este caso, debería **reiniciar** Hola implementación de paquetes de nodo tooreinitiate Hola. Reiniciar nodo hello también permite la programación de tareas de nuevo en el nodo de Hola.
> 
> 

### <a name="install-task-application-packages"></a>Instalación de paquetes de aplicación de tareas
Grupo tooa similares, especifique el paquete de aplicación *referencias* para una tarea. Cuando una tarea está programada toorun en un nodo, paquete de hello es descargado y extraído justo antes de que se ejecuta la línea de comandos de la tarea hello. Si una versión y el paquete especificado ya está instalado en el nodo de hello, no se descarga el paquete de Hola y se usa el paquete existente de Hola.

tooinstall un paquete de aplicación de la tarea, configure la tarea hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propiedad:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Ejecutar aplicaciones de hello instalado
Hello paquetes que ha especificado para un grupo o una tarea se descargan y ha extraído tooa con el nombre de directorio en hello `AZ_BATCH_ROOT_DIR` del nodo de Hola. Proceso por lotes también crea una variable de entorno que contiene hello toohello de ruta de acceso con el nombre de directorio. Las líneas de comando de la tarea use esta variable de entorno cuando se hace referencia a la aplicación hello en el nodo de Hola. 

En los nodos de Windows, variable de hello es Hola siguiendo el formato:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

En los nodos de Linux, el formato de hello es ligeramente diferente. Puntos (.), guiones (-) y signos de número (##) son toounderscores planas en la variable de entorno de Hola. Por ejemplo:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`y `version` son valores que corresponden a toohello aplicación y versión del paquete que haya especificado para la implementación. Por ejemplo, si especifica que la versión 2.7 de aplicación *blender* debe estar instalado en los nodos de Windows, las líneas de comando de la tarea se utilice este tooaccess de variable de entorno sus archivos:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

En los nodos de Linux, especifique la variable de entorno de Hola en este formato:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Cuando se carga un paquete de aplicación, puede especificar nodos de ejecución de un tooyour de toodeploy de versión de manera predeterminada. Si ha especificado una versión predeterminada para una aplicación, puede omitir el sufijo de la versión de hello cuando se hace referencia la aplicación hello. Puede especificar versión de la aplicación predeterminada Hola Hola portal de Azure, en la hoja de aplicaciones de hello, tal y como se muestra en [cargar y administrar aplicaciones](#upload-and-manage-applications).

Por ejemplo, si establece "2.7" como versión predeterminada de Hola para aplicación *blender*y hacer referencia a las tareas de hello después de variable de entorno, a continuación, los nodos de Windows ejecutarán la versión 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hello fragmento de código siguiente muestra un ejemplo de línea de comando de tarea que se inicia la versión predeterminada de Hola de hello *blender* aplicación:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Vea [configuración del entorno para tareas](batch-api-basics.md#environment-settings-for-tasks) en hello [Introducción a la característica por lotes](batch-api-basics.md) para obtener más información acerca de la configuración de entorno del nodo de proceso.
> 
> 

## <a name="update-a-pools-application-packages"></a>Actualización de los paquetes de aplicación de un grupo
Si ya ha configurado un grupo existente con un paquete de aplicación, puede especificar un nuevo paquete para el grupo de Hola. Si especifica una nueva referencia de paquete para un grupo, Hola después de aplicar:

* Hola servicio por lotes instala el paquete recién especificado de hello en todos los nodos nuevos que unirse a grupo de Hola y en cualquier nodo existente que se reinicia o se restablece la imagen inicial.
* Proceso de nodos que ya están en el grupo de hello al actualizar las referencias del paquete hello no instalan automáticamente el nuevo paquete de aplicación Hola. Estos nodos deben reiniciarse o proceso tooreceive con imagen inicial restablecida Hola nuevo paquete.
* Cuando se implementa un paquete nuevo, Hola creado variables de entorno refleja nuevas referencias de paquete de aplicación Hola.

En este ejemplo, grupo existente de hello tiene la versión 2.7 de hello *blender* aplicación configurada como uno de sus [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. nodos del grupo de tooupdate Hola con versión 2.76b, especificar un nuevo [ApplicationPackageReference] [ net_pkgref] con la nueva versión de hello y cambio de Hola de confirmación.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Ahora que hello nueva versión se ha configurado, Hola servicio por lotes instala versión 2.76b tooany *nueva* nodo que se une a grupo Hola. tooinstall 2.76b en nodos de Hola que sean *ya* en el grupo de hello, reiniciar o Restablecer imagen inicial de ellos. Tenga en cuenta que nodos reiniciados conservan archivos Hola desde implementaciones anteriores de paquetes.

## <a name="list-hello-applications-in-a-batch-account"></a>Enumerar las aplicaciones de hello en una cuenta de lote
Puede enumerar las aplicaciones de Hola y sus paquetes en una cuenta de lote mediante hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] método.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Encapsulado
Con paquetes de aplicaciones, puede ayudar a sus clientes seleccione aplicaciones de Hola para sus tareas y especificar Hola versión exacta toouse al procesar los trabajos con el servicio de lote activado. También podría proporcionan capacidad de hello para el tooupload de los clientes y realizar un seguimiento de sus propias aplicaciones en su servicio.

## <a name="next-steps"></a>Pasos siguientes
* Hola [API de REST de lote] [ api_rest] también proporciona compatibilidad con toowork con paquetes de aplicaciones. Por ejemplo, vea hello [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [agregar una cuenta del grupo de tooan] [ rest_add_pool] para obtener información acerca de cómo toospecify tooinstall de paquetes mediante el uso de hello API de REST. Vea [aplicaciones] [ rest_applications] para obtener más información acerca de cómo tooobtain información de la aplicación mediante el uso de Hola API de REST de lote.
* Obtenga información acerca de cómo tooprogrammatically [administrar cuentas de lote de Azure y las cuotas con .NET de administración de lotes](batch-management-dotnet.md). Hola [.NET de administración de lotes][api_net_mgmt] biblioteca puede habilitar características de creación y eliminación de cuenta para la aplicación de proceso por lotes o el servicio.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagrama de alto nivel de paquetes de aplicación"
[2]: ./media/batch-application-packages/app_pkg_02.png "Icono Aplicaciones en Azure Portal"
[3]: ./media/batch-application-packages/app_pkg_03.png "Hoja Aplicaciones en Azure Portal"
[4]: ./media/batch-application-packages/app_pkg_04.png "Hoja Detalles de aplicación en Azure Portal"
[5]: ./media/batch-application-packages/app_pkg_05.png "Hoja Nueva aplicación en Azure Portal"
[7]: ./media/batch-application-packages/app_pkg_07.png "Lista desplegable Actualizar o eliminar paquetes en Azure Portal"
[8]: ./media/batch-application-packages/app_pkg_08.png "Hoja Nuevo paquete de aplicación en Azure Portal"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerta de ausencia de cuenta de almacenamiento vinculada"
[10]: ./media/batch-application-packages/app_pkg_10.png "Hoja Elegir de cuenta de almacenamiento en Azure Portal"
[11]: ./media/batch-application-packages/app_pkg_11.png "Hoja Actualizar paquete en Azure Portal"
[12]: ./media/batch-application-packages/app_pkg_12.png "Cuadro de diálogo de confirmación de eliminación de paquetes en Azure Portal"
