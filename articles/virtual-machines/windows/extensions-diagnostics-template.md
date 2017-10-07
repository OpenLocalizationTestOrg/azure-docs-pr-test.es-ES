---
title: "aaaAdd diagnósticos y supervisión tooan máquina virtual de Azure | Documentos de Microsoft"
description: "Utilice un toocreate de plantilla del Administrador de recursos de Azure una nueva máquina virtual de Windows con la extensión de diagnósticos de Azure."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Uso de la supervisión y el diagnóstico con una máquina virtual Windows y plantillas de Azure Resource Manager
Hola extensión de diagnósticos de Azure proporciona supervisión de Hola y capacidades de diagnóstico en una ventana basada en máquina virtual de Azure. Para habilitar estas capacidades en la máquina virtual de Hola, incluida la extensión de hello como parte de la plantilla de administrador de recursos de azure de Hola. Para obtener más información sobre cómo incluir cualquier extensión como parte de una plantilla de máquina virtual, consulte [Creación de plantillas del Administrador de recursos de Azure con extensiones de máquina virtual](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) . Este artículo describe cómo puede agregar la plantilla de máquina virtual de windows de hello diagnósticos de Azure extensión tooa.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Agregar definición de recursos de la extensión toohello Hola diagnósticos de Azure VM
extensión de diagnósticos de hello tooenable en una máquina Virtual de Windows, necesita la extensión de hello tooadd como un recurso de máquina virtual en Hola plantilla del Administrador de recursos.

Para un administrador de recursos simple basado en Máquina Virtual agregar Hola extensión Configuración toohello *recursos* matriz para hello Máquina Virtual: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Otra convención común es agregar configuración de la extensión de hello en el nodo de recursos de raíz de Hola de plantilla de hello en lugar de definir en el nodo de recursos de la máquina virtual de Hola. Con este enfoque tiene tooexplicitly especificar una relación jerárquica entre la extensión de Hola y de máquina virtual de hello con hello *nombre* y *tipo* valores. Por ejemplo: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

extensión de Hello siempre está asociado a la máquina virtual de Hola, puede ya sea directamente definirla directamente en el nodo de recurso de la máquina virtual Hola o definir en el nivel de base de Hola y usar tooassociate de convención de nomenclatura jerárquico de Hola con hello virtual máquina.

Para las extensiones de conjuntos de escalas de máquina Virtual Hola configuración se especifica en hello *extensionProfile* propiedad de hello *VirtualMachineProfile*.

Hola *publisher* propiedad con el valor de Hola de **Microsoft.Azure.Diagnostics** hello y *tipo* propiedad con el valor de Hola de **IaaSDiagnostics** identificar de forma única extensión de diagnósticos de Azure Hola.

Hola valo hello *nombre* propiedad puede ser usado toorefer toohello extensión en el grupo de recursos de Hola. Si se establece específicamente demasiado**Microsoft.Insights.VMDiagnosticsSettings** permitirá toobe identificada con facilidad por hello asegurar portal de Azure que Hola supervisión gráficos aparecen correctamente en hello portal de Azure.

Hola *typeHandlerVersion* especifica la versión de Hola de extensión de hello le gustaría toouse. Establecer *autoUpgradeMinorVersion* demasiado la versión secundaria**true** garantiza que obtendrá versión secundaria más reciente de Hola de extensión de Hola que está disponible. Se recomienda establecer siempre *autoUpgradeMinorVersion* tooalways ser **true** para que siempre obtendrá extensión toouse Hola de diagnóstico disponible más reciente con todas las características nuevas de Hola y errores correcciones. 

Hola *configuración* elemento contiene las propiedades de las configuraciones de extensión de Hola que se pueden establecer y leer desde la extensión de hello (en ocasiones denominado tooas configuración pública). Hola *xmlcfg* propiedad contiene configuración basada en xml para los registros de diagnóstico de hello, contadores de rendimiento etcetera que se van a recopilar por agente de diagnóstico de Hola. Vea [esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obtener más información sobre el propio esquema de xml Hola. Una práctica común es la configuración de xml real de hello toostore como una variable de plantilla de Azure Resource Manager hello y, a continuación, concatenar y base64 codifican valor de hello tooset para *xmlcfg*. Vea la sección de hello en [variables de configuración de diagnósticos](#diagnostics-configuration-variables) toounderstand más información acerca de cómo toostore Hola xml en variables. Hola *storageAccount* propiedad especifica el nombre de Hola Hola almacenamiento cuenta toowhich de datos de diagnóstico que se van a transferir. 

Hola propiedades en *protectedSettings* (en ocasiones denominado tooas configuración privada) se puede establecer pero no se puede leer después de que se va a establecer. Hola de solo escritura naturaleza de *protectedSettings* resulta útil para almacenar secretos como clave de cuenta de almacenamiento de Hola donde se escribirán los datos de diagnóstico de Hola.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Especificación de la cuenta de almacenamiento de diagnóstico como parámetro
fragmento de json de extensión de diagnósticos de Hello anterior supone dos parámetros *existingdiagnosticsStorageAccountName* y *existingdiagnosticsStorageResourceGroup* diagnósticos de hello toospecify cuenta de almacenamiento donde se almacenarán los datos de diagnóstico. Especificar la cuenta de almacenamiento de diagnósticos de Hola como un parámetro hace que esta cuenta de almacenamiento de diagnósticos de hello toochange fácil entre diferentes entornos, por ejemplo, puede que desee toouse una cuenta de almacenamiento de diagnóstico diferentes para las pruebas y otra diferente para el implementación de producción.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Es mejor práctica toospecify una cuenta de almacenamiento de diagnósticos en otro grupo de recursos de grupo de recursos de hello para la máquina virtual de Hola. Un grupo de recursos puede considerarse como una unidad de implementación con su propia duración toobe, una máquina virtual se pueda implementar y volver a implementar según se realizan nuevas actualizaciones de las configuraciones tooit pero recomendable toocontinue almacenar datos de diagnóstico de Hola Hola misma cuenta de almacenamiento en las implementaciones de máquina virtual. Con la cuenta de almacenamiento de hello en diferentes recursos permite Hola almacenamiento cuenta tooaccept datos de varias implementaciones de máquina virtual para convertirla tootroubleshoot fácil Hola problemas a través de distintas versiones.

> [!NOTE]
> Si crea una plantilla de máquina virtual de windows desde Visual Studio que se puede establecer la cuenta de almacenamiento predeterminada de hello toouse Hola misma cuenta de almacenamiento donde se cargará el VHD de la máquina virtual Hola. Se trata de toosimplify la instalación inicial del programa Hola a máquina virtual. Debe refactorizar Hola plantilla toouse una cuenta de almacenamiento diferentes que puede pasar como un parámetro. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>variables de configuración de diagnóstico
fragmento de json de extensión de diagnósticos de Hello anterior define una *accountid* variable toosimplify obtener clave de cuenta de almacenamiento de hello para el almacenamiento de diagnósticos de hello:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Hola *xmlcfg* propiedad de extensión de diagnósticos de Hola se define mediante varias variables que se concatenan juntos. valores de Hello de estas variables están en xml, por lo que necesitan toobe escape correctamente al establecer las variables de json de Hola.

Hola a continuación describe xml de configuración de diagnósticos de Hola que recopila los contadores de rendimiento de nivel de sistema estándar junto con algunos registros de eventos de windows y los registros de infraestructura de diagnóstico. Se ha de escape y tiene el formato correcto para que hello configuración directamente se puede pegar en la sección de variables de saludo de la plantilla. Vea hello [esquema de configuración de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obtener un ejemplo más usuario legible de xml de configuración de Hola.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

nodo de xml de definición de métricas de Hola Hola por encima de la configuración es un elemento de configuración importantes, tal y como se define cómo los contadores de rendimiento de hello definieron anteriormente en el xml de hello en *PerformanceCounter* nodo se agregarán y almacena. 

> [!IMPORTANT]
> Estas métricas unidad Hola supervisión gráficos y alertas en hello portal de Azure.  Hola **métricas** nodo con hello *resourceID* y **MetricAggregation** deben incluirse en la configuración de diagnóstico de hello para la máquina virtual si desea toosee Hola VM datos de supervisión en hello portal de Azure. 
> 
> 

Hola te mostramos un ejemplo de Hola xml para definiciones de métricas: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Hola *resourceID* atributo identifica singularmente la máquina virtual de hello en su suscripción. Asegúrese de seguro toouse hello subscription() y resourceGroup() las funciones para que hello plantilla actualiza automáticamente los valores basados en grupos de suscripción y recursos de Hola que está implementando.

Si va a crear varias máquinas virtuales en un bucle, tendrá hello toopopulate *resourceID* valor con un toocorrectly de función copyIndex() diferenciar cada máquina virtual individual. Hola *xmlCfg* valor puede ser actualizada toosupport esto como sigue:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Hola MetricAggregation valo *PT1H* y *PT1M* indicar una agregación por minuto y una agregación más de una hora.

## <a name="wadmetrics-tables-in-storage"></a>Tablas de WADMetrics en almacenamiento
configuración de métricas de Hello anterior generará tablas en la cuenta de almacenamiento de diagnósticos con hello sigue las convenciones de nomenclatura:

* **WADMetrics** : prefijo estándar para todas las tablas WADMetrics.
* **PT1H** o **PT1M** : significa que la tabla hello contiene datos agregados en 1 hora o minuto
* **P10D** : indica la tabla de hello contendrá datos de 10 días a partir de cuando tabla Hola iniciado la recopilación de datos
* **V2S** : constante de cadena.
* **AAAAMMDD** : fecha de hello en qué Hola tabla iniciado la recopilación de datos

Ejemplo: *WADMetricsPT1HP10DV2S20151108* contendrá datos de métricas agregados durante una hora durante 10 días a partir del 11 de noviembre de 2015.    

Cada tabla WADMetrics contendrá Hola siguientes columnas:

* **PartitionKey**: Hola partitionkey se crea en función de hello *resourceID* valor toouniquely identificar el recurso de máquina virtual de Hola. para, por ejemplo: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : formato de hello sigue <Descending time tick>:<Performance Counter Name>. Hola descendente cálculo de marca de tiempo es marcas de tiempo máximo menos tiempo Hola del principio de hello del período de agregación de Hola. Por ejemplo, Si un período de muestreo Hola iniciado de 10-noviembre de 2015 y cálculo de UTC, a continuación, hello 00:00Hrs sería: DateTime.MaxValue.Ticks - (nuevo DateTime(2015,11,10,0,0,0,DateTimeKind.Utc). Tics). De clave de fila Hola contador de rendimiento de la bytes disponibles de memoria de hello tendrá un aspecto como: 2519551871999999999__:005CMemory:005CAvailable:0020 Bytes
* **CounterName** : es nombre Hola Hola del contador de rendimiento. Esto coincide con hello *counterSpecifier* definido en el archivo de configuración xml Hola.
* **Máximo** : Hola valor máximo del contador de rendimiento de hello en período de agregación de Hola.
* **Mínimo** : Hola valor mínimo del contador de rendimiento de hello en período de agregación de Hola.
* **Total** : Hola suma de todos los valores de contador de rendimiento de Hola que se expresa en período de agregación de Hola.
* **Recuento de** : número total de Hola de valores se notifica para el contador de rendimiento de Hola.
* **Promedio** : Hola valor promedio (total/recuento) de contador de rendimiento de hello en período de agregación de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una plantilla de ejemplo de una máquina virtual de Windows con la extensión de diagnósticos, consulte [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Implementar la plantilla de administrador de recursos de hello mediante [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [línea de comandos de Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Obtenga más información sobre la [creación de plantillas del Administrador de recursos de Azure](../../resource-group-authoring-templates.md)

