---
title: aaaGet iniciar PowerShell para Azure Batch | Documentos de Microsoft
description: "Una introducción rápida se toohello cmdlets de PowerShell de Azure se pueden utilizar los recursos de proceso por lotes toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Administración de recursos de Batch con cmdlets de PowerShell

Con hello cmdlets de PowerShell de lote de Azure, se puede realizar y programan muchas Hola mismas tareas que llevar a cabo con las API de lote, hello Hola portal de Azure y Hola interfaz de línea de comandos (CLI) de Azure. Se trata de una cmdlets de toohello introducción rápida, puede usar toomanage sus cuentas de lote y trabajar con sus recursos de proceso por lotes como grupos, los trabajos y tareas.

Para obtener una lista completa de cmdlets de lote y la sintaxis de cmdlet detallados, vea hello [referencia de cmdlets de Azure Batch](/powershell/module/azurerm.batch/#batch).

Este artículo se basa en los cmdlets de Azure PowerShell versión 3.0.0. Le recomendamos que actualice su PowerShell de Azure con frecuencia tootake aprovechar las mejoras y las actualizaciones del servicio.

## <a name="prerequisites"></a>Requisitos previos
Realizar Hola siguiendo las operaciones toouse Azure PowerShell toomanage los recursos de proceso por lotes.

* [Instalación y configuración de Azure PowerShell](/powershell/azure/overview)
* Ejecute hello **AzureRmAccount de inicio de sesión** cmdlet tooconnect tooyour suscripción (Hola directa de cmdlets de Azure Batch en módulo de Azure Resource Manager hello):
  
    `Login-AzureRmAccount`
* **Registrar con el espacio de nombres del proveedor de lote de hello**. Esta operación solo es necesario toobe realiza **una vez por cada suscripción**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Administrar claves y cuentas por lotes
### <a name="create-a-batch-account"></a>Crear una cuenta de lote
**New-AzureRmBatchAccount** crea una cuenta de Batch en un grupo de recursos especificado. Si ya no tiene un grupo de recursos, crear uno mediante la ejecución de hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet. Especifique uno de hello Azure regiones en hello **ubicación** parámetro, como "Central US". Por ejemplo:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

A continuación, cree una cuenta de lote en grupo de recursos de hello, especificar un nombre de cuenta de hello en <*account_name*> Hola, ubicación y nombre de su grupo de recursos. Crear cuenta de lote de hello puede tardar algún tiempo toocomplete. Por ejemplo:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> cuenta de lote de Hello nombre debe ser único toohello región de Azure para el grupo de recursos de hello, contener entre 3 y 24 caracteres y usar letras minúsculas y números solo.
> 
> 

### <a name="get-account-access-keys"></a>Obtener claves de acceso de cuenta
**Get-AzureRmBatchAccountKeys** muestra las teclas de acceso de hello asociadas con una cuenta de lote de Azure. Por ejemplo, ejecute hello siguiendo las claves principal y secundaria del Hola de tooget de cuenta de hello que ha creado.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Generar una nueva clave de acceso
**New-AzureBatchAccountKey** genera una nueva clave de cuenta principal o secundaria para una cuenta de Lote de Azure. Por ejemplo, toogenerate una nueva clave principal para la cuenta de proceso por lotes, escriba:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate una nueva clave secundaria, especifique "Secundaria" de hello **KeyType** parámetro. Tener claves primarias y secundarias de hello tooregenerate por separado.
> 
> 

### <a name="delete-a-batch-account"></a>Eliminar una cuenta de lote
**Remove-AzureBatchAccount** elimina una cuenta de Lote. Por ejemplo:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Cuando se le pida, confirme la cuenta de hello tooremove. Eliminación de cuenta puede tardar algún tiempo toocomplete.

## <a name="create-a-batchaccountcontext-object"></a>Creación de un objeto BatchAccountContext
usar tooauthenticate Hola cmdlets de PowerShell de lote cuando cree y administre los grupos de proceso por lotes, los trabajos, tareas, y otros recursos, cree primero un toostore de objeto BatchAccountContext el nombre de cuenta y las claves:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Se pasa hello BatchAccountContext objeto en cmdlets que Hola de uso **BatchContext** parámetro.

> [!NOTE]
> De forma predeterminada, se utiliza la clave principal de la cuenta de hello para la autenticación, pero puede seleccionar explícitamente Hola clave toouse cambiando el objeto BatchAccountContext **KeyInUse** propiedad: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Creación y modificación de recursos de Lote
Usar cmdlets como **New-AzureBatchPool**, **New-AzureBatchJob**, y **New-AzureBatchTask** toocreate recursos bajo una cuenta de lote. Hay correspondientes **Get -** y **Set -** propiedades de hello tooupdate de cmdlets de recursos existentes, y **Remove -** cmdlets tooremove recursos bajo una cuenta de lote.

Al utilizar muchos de estos cmdlets en suma toopassing un objeto BatchContext, necesita toocreate o pasar objetos que contienen la configuración de recursos detallado, como se muestra en el siguiente ejemplo de Hola. Vea Hola ayuda detallada de cada cmdlet para obtener ejemplos adicionales.

### <a name="create-a-batch-pool"></a>Crear un grupo de Lote
Al crear o actualizar un grupo de lote, seleccione Configuración del servicio de nube de Hola o configuración de máquina virtual de Hola para hello sistema operativo en hello nodos de proceso (consulte [Introducción a la característica por lotes](batch-api-basics.md#pool)). Si especifica la configuración del servicio de nube de hello, se crea la imagen de sus nodos de proceso con uno de hello [versiones del SO invitado de Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Si se especifica la configuración de máquina virtual de hello, puede especificar uno de hello admite Linux u Hola enumerada en las imágenes de máquina virtual de Windows [máquinas virtuales de Azure Marketplace][vm_marketplace], o proporcionar un personalizado imagen que haya preparado.

Al ejecutar **New-AzureBatchPool**, pasar la configuración de sistema operativo de hello en un objeto PSCloudServiceConfiguration o PSVirtualMachineConfiguration. Por ejemplo, hello siguiente cmdlet crea un nuevo grupo de lote con nodos de proceso pequeñas de tamaño en la configuración del servicio de nube de hello, crea la imagen con la versión de sistema operativo más reciente de Hola de familia 3 (Windows Server 2012). En este caso, Hola **CloudServiceConfiguration** parámetro especifica hello *$configuration* variable como objeto de PSCloudServiceConfiguration Hola. Hola **BatchContext** parámetro especifica una variable definida anteriormente *$context* como objeto de BatchAccountContext Hola.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

número de destino de Hola de nodos de cálculo en el nuevo grupo de hello viene determinado por una fórmula de Autoescala. En este caso, es simplemente fórmula hello **$TargetDedicated = 4**, que indica el número de Hola de nodos de proceso en el grupo de hello es 4 como máximo.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Consulta de grupos, trabajos, tareas y otros detalles
Usar cmdlets como **Get-AzureBatchPool**, **Get AzureBatchJob**, y **AzureBatchTask Get** tooquery para entidades creadas en una cuenta de lote.

### <a name="query-for-data"></a>Consulta de datos
Por ejemplo, usar **AzureBatchPools Get** toofind sus grupos. De forma predeterminada, esta consulta para todos los grupos en su cuenta, suponiendo que ya almacenado Hola BatchAccountContext objeto *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Uso de un filtro OData
Puede proporcionar un filtro de OData mediante hello **filtro** parámetro toofind Hola solo objetos que le interesa. Por ejemplo, puede encontrar todos los grupos cuyos id. empiecen por "myPool":

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Este método no es tan flexible como "Where-Object" en una canalización local. Sin embargo, Hola consulta obtiene envía toohello servicio por lotes directamente para que todos los filtros, se produce en el lado del servidor hello, ahorra ancho de banda de Internet.

### <a name="use-hello-id-parameter"></a>Utilice el parámetro de Id. de Hola
Un filtro de OData tooan alternativo es hello de toouse **identificador** parámetro. tooquery para un grupo específico con identificador "myPool":

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Hola **identificador** parámetro admite sólo búsqueda de identificador completo, no de caracteres comodín o filtros de estilo de OData.

### <a name="use-hello-maxcount-parameter"></a>Use el parámetro MaxCount de hello
De forma predeterminada, cada cmdlet devuelve un máximo de 1000 objetos. Si se alcanza este límite, refinar su toobring filtro nuevo menos objetos o establecer explícitamente el máximo con hello **MaxCount** parámetro. Por ejemplo:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

establecer el límite superior de tooremove hello, **MaxCount** too0 o menos.

### <a name="use-hello-powershell-pipeline"></a>Usar la canalización de PowerShell de Hola
Cmdlets de proceso por lotes puede aprovechar datos de toosend de canalización de PowerShell de hello entre cmdlets. Esto tiene el mismo efecto que si se especifica un parámetro, pero hace que trabajar con varias entidades sea más fácil de Hola.

Por ejemplo, busque y muestre todas las tareas de su cuenta:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Reinicie todos los nodos de proceso de un grupo:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Administración de paquetes de aplicación
Paquetes de aplicación proporcionan una manera simplificada toodeploy aplicaciones toohello nodos de cálculo en los grupos. Con hello cmdlets de PowerShell de lote, puede cargar y administrar paquetes de aplicaciones en su cuenta de lote e implementar nodos de toocompute de versiones de paquete.

**Cree** una aplicación:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Agregue** un paquete de aplicación:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Conjunto hello **versión predeterminada** para la aplicación hello:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Muestre** los paquetes de la aplicación:

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Elimine** un paquete de aplicación:

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Elimine** una aplicación:

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Debe eliminar todas las versiones de paquete de aplicación de la aplicación antes de eliminar la aplicación hello. Si intentas toodelete una aplicación que tiene actualmente los paquetes de aplicación, recibirá un error de 'Conflicto'.
> 
> 

### <a name="deploy-an-application-package"></a>Implementación de un paquete de aplicación
Al crear un grupo, puede especificar uno o varios paquetes de aplicación para implementarlos. Cuando se especifica un paquete en el momento de creación de grupo, es el nodo de implementada tooeach como grupo de combinaciones de nodo de Hola. También se implementan paquetes cuando un nodo se reinicia o se restablece su imagen inicial.

Especificar hello `-ApplicationPackageReference` opción al crear un grupo toodeploy nodos de un paquete toohello grupo de aplicaciones cuando se unen a grupo Hola. En primer lugar, cree un **PSApplicationPackageReference** de objetos y configurarlo con la versión de identificador y el paquete de la aplicación de hello desea toodeploy toohello grupo de nodos de proceso:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Ahora crear grupo de Hola y especificar el objeto de referencia de paquete de Hola Hola argumento toohello `ApplicationPackageReferences` opción:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Puede encontrar más información sobre los paquetes de aplicación en [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).

> [!IMPORTANT]
> Debe [vincular una cuenta de almacenamiento de Azure](#linked-storage-account-autostorage) tooyour lote cuenta toouse paquetes de aplicación.
> 
> 

### <a name="update-a-pools-application-packages"></a>Actualización de los paquetes de aplicación de un grupo
las aplicaciones de hello tooupdate asignadas tooan grupo existente, cree primero un objeto de PSApplicationPackageReference con propiedades de hello deseado (paquete y el Id. de versión de la aplicación):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

A continuación, obtener grupo de hello del lote, borrar todos los paquetes existentes, agregar la nueva referencia de paquete y actualizar servicio por lotes de hello con la nueva configuración de la agrupación de hello:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Ahora ha actualizado propiedades del grupo de hello en el servicio de lote de Hola. tooactually implementar Hola nueva aplicación paquete toocompute nodos de grupo de hello, sin embargo, debe reiniciar o Restablecer imagen inicial de dichos nodos. Puede reiniciar todos los nodos de un grupo con este comando:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Puede implementar varias aplicaciones paquetes toohello nodos de proceso en un grupo. Si lo desea demasiado*agregar* un paquete de aplicación en lugar de reemplazar los paquetes de saludo implementada actualmente, omitir hello `$pool.ApplicationPackageReferences.Clear()` línea anterior.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Para conocer la sintaxis detallada de cmdlets y ejemplos de los mismos, consulte [Azure Batch Cmdlets](/powershell/module/azurerm.batch/#batch)(Cmdlets de Lote de Azure).
* Para obtener más información acerca de las aplicaciones y paquetes de aplicaciones en el lote, vea [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/