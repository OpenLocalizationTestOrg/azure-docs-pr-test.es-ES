---
title: "Proceso de aaaAzure - extensión de diagnóstico de Linux | Documentos de Microsoft"
description: "Cómo tooconfigure Hola métricas de toocollect de extensión de diagnóstico Linux (LAD) de Azure y registrar los eventos de máquinas virtuales de Linux que se ejecutan en Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Usar registros y las métricas de toomonitor de extensión de diagnóstico de Linux

Este documento describe la versión 3.0 y versiones más reciente de hello extensión de diagnóstico de Linux.

> [!IMPORTANT]
> Para obtener información sobre las versiones 2.3 y anteriores, consulte [este documento](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Introducción

Hola extensión de diagnóstico de Linux ayuda a un usuario monitor Hola el estado de una VM de Linux que se ejecutan en Microsoft Azure. Tiene Hola siguientes capacidades:

* Recopila las métricas de rendimiento del sistema de hello VM y los almacena en una tabla específica en una cuenta de almacenamiento designada.
* Recupera el registro de sucesos de syslog y almacenarlos en una tabla específica en hello designado de la cuenta de almacenamiento.
* Permite a los usuarios toocustomize hello las métricas de datos que se recopilan y cargan.
* Permite los recursos de syslog de usuarios toocustomize hello y niveles de gravedad de los eventos que se recopilan y cargan.
* Permite que los usuarios tooupload registro especificado archivos tooa almacenamiento designadas tabla.
* Admite el envío de las métricas y registro de eventos tooarbitrary EventHub los puntos de conexión y los blobs con formato JSON en hello designado cuenta de almacenamiento.

Esta extensión funciona con los dos modelos de implementación de Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Instalando la extensión de Hola la máquina virtual

Puede habilitar esta extensión mediante cmdlets de PowerShell de Azure de hello, secuencias de comandos de CLI de Azure o las plantillas de implementación de Azure. Para obtener más información, consulte [Funciones de la extensión](./extensions-features.md).

Hola portal de Azure no puede ser usado tooenable o configurar LAD 3.0. En su lugar, instala versión 2.3 y la configura. Alertas y gráficos de portal de azure trabajan con datos de ambas versiones de extensión de Hola.

Mediante estas instrucciones de instalación y una [configuración de ejemplo descargable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) se configura LAD 3.0 para:

* Capture y almacene Hola mismas métricas como proporcionadas por LAD 2.3;
* capturar un conjunto útil de las métricas del sistema de archivo, nuevo tooLAD 3.0;
* captura de la colección de syslog predeterminada Hola habilitada por LAD 2.3;
* Habilitar hello Azure experiencia del portal para gráficos y las alertas relacionadas con las métricas de máquina virtual.

configuración descargable Hello es simplemente un ejemplo; modificar toosuit sus propias necesidades.

### <a name="prerequisites"></a>Requisitos previos

* **Versión 2.2.0 o posterior del agente Linux de Azure**. La mayoría de las imágenes de la galería de máquina virtual Linux de Azure incluyen la versión 2.2.7 o posterior. Ejecutar `/usr/sbin/waagent -version` versión de hello tooconfirm instalada en hello máquina virtual. Si Hola VM está ejecutando una versión anterior del agente de invitado de Hola, siga [estas instrucciones](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate lo.
* **CLI de Azure** [Configurar hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) entorno en su equipo.
* Hola wget comando, si aún no lo tiene: ejecutar `sudo apt-get install wget`.
* Cuenta de una suscripción de Azure y un almacenamiento existente dentro de él toostore datos de saludo.

### <a name="sample-installation"></a>Instalación de ejemplo

Rellenar parámetros correctos de hello en hello tres primeras líneas y, a continuación, ejecutar este script como raíz:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

dirección URL de Hello para la configuración de ejemplo de Hola y su contenido es toochange de asunto. Descargue una copia del archivo JSON de la configuración del portal de Hola y personalizarla en función de sus necesidades. Cualquier plantilla o automatización que genere deberían usar su propia copia en lugar de descargar dicha URL cada vez.

### <a name="updating-hello-extension-settings"></a>Actualizando la configuración de la extensión de Hola

Después de cambiar la configuración pública o protegido, implementarlas toohello VM mediante la ejecución de Hola mismo comando. Si nada cambia en la configuración de hello, configuraciones de hello actualizado se envían toohello extensión. LAD vuelve a cargar la configuración de Hola y se reinicia.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migración desde versiones anteriores de extensión de Hola

Hola la versión más reciente de extensión de hello es **3.0**. **Todas las versiones anteriores (2.x) están en desuso y pueden retirarse a partir del 31 de julio de 2018**.

> [!IMPORTANT]
> Esta extensión introduce la separación de la configuración de toohello de cambios de extensión de Hola. Uno de estos cambios se realizó la seguridad de hello tooimprove de extensión de hello; como resultado, con las versiones anteriores compatibilidad con 2.x no se pudo mantener. Además, Hola publicador de extensión para esta extensión es diferente de publicador Hola para las versiones 2.x Hola.
>
> toomigrate de 2.x toothis nueva versión de extensión de hello, debe desinstalar la extensión anterior de hello (con nombre de publicador antiguo de hello) y, a continuación, instalar la versión 3 de extensión de Hola.

Recomendaciones:

* Instalar extensión de hello con la actualización de versión secundaria automática habilitada.
  * En el modelo de implementación clásica máquinas virtuales, especificar '3.*' como versión de Hola si va a instalar la extensión de Hola a través de Azure XPLAT CLI o Powershell.
  * En la implementación de Azure Resource Manager del modelo de las máquinas virtuales, incluir ' "autoUpgradeMinorVersion": true' en la plantilla de implementación de VM de Hola.
* Use una cuenta de almacenamiento nueva o diferente para LAD 3.0. Hay varias pequeñas incompatibilidades entre LAD 2.3 y LAD 3.0 que hacen que compartir una cuenta sea problemático:
  * LAD 3.0 almacena los eventos de syslog en una tabla con un nombre diferente.
  * counterSpecifier Hola cadenas para `builtin` métricas difieren en LAD 3.0.

## <a name="protected-settings"></a>Configuración protegida

Este conjunto de información de configuración contiene información confidencial que debería protegerse de la vista pública, por ejemplo, las credenciales de almacenamiento. Estos valores son transmitido tooand almacenado por la extensión de hello en formato cifrado.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nombre | Valor
---- | -----
storageAccountName | Hola el nombre de cuenta de almacenamiento de hello en el que los datos se escriben por extensión Hola.
storageAccountEndPoint | identificar en qué Hola existe la cuenta de almacenamiento en la nube Hola el extremo de hello (opcional). Si este valor está ausente, LAD predeterminado toohello nube pública de Azure, `https://core.windows.net`. toouse una cuenta de almacenamiento de Azure en Alemania, Azure Government o Azure China, establezca este valor en consecuencia.
storageAccountSasToken | Un [token de SAS de cuenta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para los servicios Blob y tabla (`ss='bt'`), toocontainers aplicables y los objetos (`srt='co'`), que concede agrega, crear, enumerar, actualizar y permisos de escritura (`sp='acluw'`). Hacer *no* incluyen hello inicial interrogación (?).
mdsdHttpProxy | (opcional) La información necesaria de proxy HTTP tooenable Hola extensión tooconnect toohello especifica cuenta de almacenamiento y del extremo.
sinksConfig | (opcional) Detalles de las métricas de toowhich destinos alternativos y eventos se pueden entregar. detalles específicos de Hola de cada receptor de datos compatibles con la extensión de Hola se tratan en secciones de Hola que siguen.

Puede construir fácilmente Hola requerido el token de SAS a través de hello portal de Azure.

1. Seleccione toowhich de cuenta de almacenamiento general Hola desea Hola extensión toowrite
1. Seleccione "Firma de acceso compartido" de parte de la configuración de hello del menú izquierdo Hola
1. Asegúrese de secciones correspondientes de hello como se describió anteriormente
1. Haga clic en el botón de "Generar SAS" Hola.

![imagen](./media/diagnostic-extension/make_sas.png)

Hola copia genera SAS en el campo de hello storageAccountSasToken; quitar Hola inicial de interrogación ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Esta sección opcional define otros destinos de extensión de hello toowhich envía información de hello recopila. matriz de "receptor" Hello contiene un objeto para cada receptor de datos adicionales. Hola determina el atributo "type" Hola otros atributos de objeto de Hola.

Elemento | Valor
------- | -----
name | Receptor de toothis toorefer en otra parte de la configuración de la extensión de hello usa una cadena.
type | tipo de Hello del receptor que se está definiendo. Hola otros valores (si existe) se determina en instancias de este tipo.

La versión 3.0 de hello extensión de diagnóstico de Linux admite dos tipos de receptor: EventHub y JsonBlob.

#### <a name="hello-eventhub-sink"></a>receptor de EventHub Hola

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

entrada de "sasURL" Hello contiene Hola debe publicarse la dirección URL completa, incluido el token SAS, para hello datos toowhich de concentrador de eventos. LAD requiere una SAS una directiva que habilita la notificación de envío de Hola de nomenclatura. Por ejemplo:

* Cree un espacio de nombres de Event Hubs llamado `contosohub`.
* Crear un concentrador de eventos en el espacio de nombres de hello denominado`syslogmsgs`
* Crear una directiva de acceso compartido en hello concentrador de eventos denominado `writer` que permite Hola notificación de envío

Si ha creado una SAS buena hasta medianoche UTC en el 1 de enero de 2018, el valor de sasURL de hello podría ser:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Para obtener más información sobre la generación de tokens de SAS para Event Hubs, consulte [esta página web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>receptor de Hello JsonBlob

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Los datos de dirigir tooa JsonBlob receptor se almacena en blobs en almacenamiento de Azure. Cada instancia de LAD crea un blob cada hora para cada nombre de receptor. Todos los blobs siempre contienen una matriz de objeto JSON válida sintácticamente. Las nuevas entradas se agregan atómicamente toohello matriz. BLOB se almacenan en un contenedor con el mismo nombre como receptor de Hola de Hola. Hola reglas de almacenamiento de Azure para los nombres de contenedor de blob aplican nombres toohello de receptores JsonBlob: entre 3 y 63 caracteres ASCII alfanuméricos en minúsculas o guiones.

## <a name="public-settings"></a>Configuración pública

Esta estructura contiene varios bloques de configuración que controla la información de hello recopilada por extensión Hola. Cada valor de configuración es opcional. Si especifica `ladCfg`, también debe especificar `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Elemento | Valor
------- | -----
StorageAccount | Hola el nombre de cuenta de almacenamiento de hello en el que los datos se escriben por extensión Hola. Debe ser Hola mismo nombre tal y como se especifica en hello [protegido configuración](#protected-settings).
mdsdHttpProxy | (opcional) Igual que hello [protegido configuración](#protected-settings). Hola pública valor se sustituye por valor privada de hello, si establece. Colocar valores de proxy que contienen un secreto, como una contraseña, en hello [protegido configuración](#protected-settings).

los elementos restantes de Hola se describen en detalle en las secciones siguientes de Hola.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Los receptores de esta recopilación de Hola de controles de estructura opcional de las métricas y los registros para entrega toohello datos de servicio y tooother de métricas de Azure. Debe especificar `performanceCounters`, `syslogEvents` o ambos. Debe especificar hello `metrics` estructura.

Elemento | Valor
------- | -----
eventVolume | (opcional) Número de particiones creadas dentro de la tabla de almacenamiento de Hola Hola a controles. Debe ser uno de los siguientes valores: `"Large"`, `"Medium"` o `"Small"`. Si no se especifica, el valor predeterminado de hello es `"Medium"`.
sampleRateInSeconds | intervalo predeterminado de hello (opcional) entre la colección de métricas (prolongadas) sin formato. velocidad de muestra de Hola menor admitida es de 15 segundos. Si no se especifica, el valor predeterminado de hello es `15`.

#### <a name="metrics"></a>Métricas

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Elemento | Valor
------- | -----
resourceId | Identificador de recurso de Azure Resource Manager Hola de hello VM o de escala de máquinas virtuales de hello establece hello toowhich que pertenece la máquina virtual. Este valor debe ser también especifica si se utiliza cualquier receptor JsonBlob en configuración de Hola.
scheduledTransferPeriod | frecuencia de Hello en el que métricas agregadas son toobe se calcula y transfiere tooAzure métricas, expresado como un intervalo de tiempo es 8601. período de transferencia más pequeño de Hello es 60 segundos, es decir, PT1M. Debe especificar al menos un elemento scheduledTransferPeriod.

Ejemplos de hello métricas especificadas en la sección de performanceCounters de Hola se recopilan cada 15 segundos o en la velocidad de muestra de Hola definida explícitamente para el contador de Hola. Si aparecen varias frecuencias de scheduledTransferPeriod (como en el ejemplo de Hola), cada agregación se calcula de forma independiente.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Colección de Hola de métricas de controles de esta sección opcional. Ejemplos sin formato se agregan para cada [scheduledTransferPeriod](#metrics) tooproduce estos valores:

* mean
* minimum
* maximum
* last-collected value
* recuento de muestras sin formato utiliza el agregado de hello toocompute

Elemento | Valor
------- | -----
sinks | (opcional) Una lista separada por comas de nombres de los receptores toowhich que LAD envía los resultados de métrica agregado. Todas las métricas agregadas son tooeach publicado aparece receptor. Consulte [sinksConfig](#sinksconfig). Ejemplo: `"EHsink1, myjsonsink"`.
type | Identifica Hola proveedor real de métrica de Hola.
class | Junto con "counter" identifica métrica específica de hello en el espacio de nombres del proveedor de Hola.
counter | Junto con "clase", identifica métrica específica de hello en el espacio de nombres del proveedor de Hola.
counterSpecifier | Identifica la métrica específica de hello en el espacio de nombres de hello las métricas de Azure.
condition | (opcional) Selecciona una instancia específica de la métrica de hello objeto toowhich Hola se aplica o selecciona Hola agregación en todas las instancias de ese objeto. Para obtener más información, vea hello [ `builtin` definiciones de métrica](#metrics-supported-by-builtin).
sampleRate | ES el intervalo de 8601 que establece la tasa de hello en el que se recopilaron las muestras sin procesar para esta métrica. Si no se establece, el intervalo de recopilación de Hola se establece por valor de Hola de [sampleRateInSeconds](#ladcfg). velocidad de muestreo admitida más corta de Hello es 15 segundos (PT15S).
unit | Debería ser una de estas cadenas: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond" o "Millisecond". Define la unidad de Hola de métrica de Hola. Los consumidores de hello recopilan datos esperar Hola recopila datos valores toomatch esta unidad. LAD omite este campo.
DisplayName | Hola etiqueta (en el lenguaje de hello especificado por la configuración regional asociada de hello establecer) toobe adjunta toothis datos de métricas de Azure. LAD omite este campo.

counterSpecifier Hello es un identificador arbitrario. Los consumidores de métricas, como Hola diagramación de portal de Azure y las alertas de característica, usan counterSpecifier como Hola "clave" que identifica una métrica o una instancia de una métrica. Para las métricas de `builtin`, se recomienda usar valores counterSpecifier que empiecen por `/builtin/`. Si va a recopilar una instancia específica de una métrica, se recomienda que asociar identificador hello de valor de hello instancia toohello counterSpecifier. Estos son algunos ejemplos:

* `/builtin/Processor/PercentIdleTime`: tiempo de inactividad promediado en todos los núcleos
* `/builtin/Disk/FreeSpace(/mnt)`-Espacio para el sistema de archivos de Hola/mnt
* `/builtin/Disk/FreeSpace`: espacio libre promediado entre todos los elementos filesystem montados

LAD ni Hola portal de Azure espera hello counterSpecifier valor toomatch cualquier patrón. Sea coherente en el modo de construcción de valores counterSpecifier.

Cuando se especifica `performanceCounters`, LAD siempre escribe tooa tabla de datos en el almacenamiento de Azure. Se puede haber Hola mismo datos escritos tooJSON blobs o centros de eventos, pero no se puede deshabilitar la tabla de tooa de almacenar datos. Todas las instancias de hello configurada de diagnóstico extensión toouse Hola misma cuenta de almacenamiento, nombre y el extremo agregan su toohello registros y las métricas misma tabla. Si hay demasiadas máquinas virtuales son escribir toohello puede limitar la misma partición de tabla, Azure escribe toothat partición. eventVolume Hola establecer causas entradas toobe se reparten entre 1 (pequeño), 10 (medio) o 100 particiones diferentes (grande). Por lo general, "Medio" es suficiente tooensure tráfico no está limitado. característica de las métricas de Azure Hola de hello portal de Azure usa datos de hello en este gráficos tooproduce de tabla o tootrigger alertas. nombre de la tabla de Hello es la concatenación de Hola de estas cadenas:

* `WADMetrics`
* Hola "scheduledTransferPeriod" para hello agrega valores almacenados en la tabla de Hola
* `P10DV2S`
* Una fecha, en forma de Hola "AAAAMMDD", que cambia cada 10 días

Algunos ejemplos son `WADMetricsPT1HP10DV2S20170410` y `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Esta sección opcional controla la recolección de Hola de registrar eventos de syslog. Si se omite la sección de hello, eventos de syslog no se capturan en absoluto.

colección de Hello syslogEventConfiguration tiene una entrada para cada utilidad syslog de interés. Si minSeverity es "NONE" para un servicio determinado, o si dicha instalación no aparece en el elemento de hello en absoluto, no se captura ningún evento de dicha instalación.

Elemento | Valor
------- | -----
sinks | Una lista separada por comas de nombres de los receptores de registro individuales toowhich los eventos se publican. Todos los eventos de registro que coinciden con las restricciones de hello en syslogEventConfiguration son tooeach publicado aparece receptor. Por ejemplo, "EHforsyslog".
facilityName | Es un nombre de recurso de syslog (como "LOG\_USER" o "LOG\_LOCAL0"). Consulte la sección de "instalación de" hello de hello [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para la lista completa de Hola.
minSeverity | Es un nivel de gravedad de syslog (como "LOG\_ERR" o "LOG\_INFO"). Consulte la sección de "nivel" hello de hello [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para la lista completa de Hola. extensión de Hello captura eventos enviados toohello instalaciones en o por encima de hello especifica el nivel.

Cuando se especifica `syslogEvents`, LAD siempre escribe tooa tabla de datos en el almacenamiento de Azure. Se puede haber Hola mismo datos escritos tooJSON blobs o centros de eventos, pero no se puede deshabilitar la tabla de tooa de almacenar datos. Hola comportamiento para esta tabla de la partición es Hola igual al descrito en `performanceCounters`. nombre de la tabla de Hello es la concatenación de Hola de estas cadenas:

* `LinuxSyslog`
* Una fecha, en forma de Hola "AAAAMMDD", que cambia cada 10 días

Algunos ejemplos son `LinuxSyslog20170410` y `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Esta sección opcional controla la exclusión de consultas [OMI](https://github.com/Microsoft/omi) arbitrarias.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
espacio de nombres | (opcional) Hola OMI espacio de nombres dentro de qué Hola se debe ejecutar la consulta. Si no se especifica, el valor de predeterminado de hello es "root/scx", implementada por hello [System Center multiplataforma proveedores](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Hola OMI toobe de consulta ejecutado.
table | tabla de almacenamiento de Azure de hello (opcional), en hello designado de la cuenta de almacenamiento (vea [protegido configuración](#protected-settings)).
frequency | número de hello (opcional) de segundos entre ejecuciones de consulta de Hola. El valor predeterminado es de 300 (5 minutos) y el mínimo es de 15 segundos.
sinks | (opcional) Debe publicarse una lista separada por comas de nombres de los resultados de métrica de receptores adicionales toowhich ejemplo sin formato. Ninguna agregación de estos ejemplos sin procesar se calcula por la extensión de Hola o las métricas de Azure.

Deben especificarse "table", "sinks" o ambos.

### <a name="filelogs"></a>fileLogs

Hola de controles de captura de los archivos de registro. LAD captura nuevas líneas de texto, tal y como se escriben toohello archivo y los escribe filas tootable o los receptores especificados (JsonBlob o EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
file | ruta de acceso completa de Hola de toobe de archivo de registro de hello visto y capturado. ruta de acceso de Hello debe asignar un nombre único de un archivo, no puede nombrar un directorio o contiene caracteres comodines.
table | tabla de almacenamiento de Azure de hello (opcional), en el almacenamiento de hello designado de la cuenta (tal y como se especifica en la configuración de hello protegido), en las nuevas líneas de Hola "cola" del archivo hello se escribe.
sinks | (opcional) Envía una lista separada por comas de nombres de las líneas de registro de toowhich de receptores adicionales.

Deben especificarse "table", "sinks" o ambos.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Métricas de hello builtin proveedor admitidas

proveedor de Hello builtin métrica es un origen de métricas más interesantes tooa amplio conjunto de usuarios. Estas métricas se dividen en cinco clases amplias:

* Procesador
* Memoria
* Red
* Filesystem
* Disco

### <a name="builtin-metrics-for-hello-processor-class"></a>métricas de Builtin para hello clase de procesador

Hola clase de procesador de métricas proporciona información sobre el uso de procesador en hello máquina virtual. Al agregar porcentajes, resultado de hello es promedio de hello en todas las CPU. En una máquina virtual de dos núcleos, si un núcleo era ocupados al 100% y Hola otro era 100% inactivo, Hola informa que percentidletime sería 50. Si cada núcleo es 50% ocupado para Hola mismo período, Hola notifica el resultado también sería 50. En una de máquina virtual, de cuatro núcleos con un núcleo ocupados al 100% y Hola otros inactivo, Hola indicados que percentidletime sería 75.

counter | Significado
------- | -------
PercentIdleTime | Porcentaje de tiempo durante la ventana de la agregación de Hola que procesadores estaban ejecutando bucle inactivo de hello kernel
PercentProcessorTime | Porcentaje de tiempo de ejecución de un subproceso no inactivo
PercentIOWaitTime | Porcentaje de tiempo de espera para toocomplete de las operaciones de E/S
PercentInterruptTime | Porcentaje de tiempo de ejecución de interrupciones de hardware o software y DPC (llamadas a procedimiento aplazadas)
PercentUserTime | Tiempo no está inactivo durante la ventana de la agregación de hello, porcentaje de Hola de tiempo invertido en usuario más con prioridad normal
PercentNiceTime | Tiempo no está inactivo, porcentaje de hello dedicado con menor prioridad ("nice")
PercentPrivilegedTime | De momento no está inactivo, Hola porcentaje empleado en modo privilegiado (kernel)

Hello primero cuatro contadores deberían sumar too100%. Hello última tres contadores también suma too100%; subdivide suma Hola de PercentProcessorTime, PercentIOWaitTime y PercentInterruptTime.

tooobtain una sola métrica se agrega a lo largo de todos los procesadores, establezca `"condition": "IsAggregate=TRUE"`. tooobtain una métrica para un procesador específico, como el segundo procesador lógico Hola de un cuatro principales de máquina virtual, establece `"condition": "Name=\\"1\\""`. Números de procesador lógico están en el intervalo de hello `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>métricas de Builtin para hello Memory (clase)

Hola Memory (clase) de métricas proporciona información acerca del uso de memoria, la paginación y el intercambio.

counter | Significado
------- | -------
AvailableMemory | Memoria física disponible en MiB
PercentAvailableMemory | Memoria física disponible en forma de porcentaje del total de memoria
UsedMemory | Memoria física en uso (MiB)
PercentUsedMemory | Memoria física en uso en forma de porcentaje del total de memoria
PagesPerSec | Paginación total (lectura y escritura)
PagesReadPerSec | Páginas leídas desde la memoria auxiliar (archivo de intercambio, archivo de programa, archivo asignado, etc.)
PagesWrittenPerSec | Páginas escritas toobacking almacenan (archivo de intercambio, archivo asignado, etcetera.)
AvailableSwap | Espacio de intercambio sin usar (MiB)
PercentAvailableSwap | Espacio de intercambio sin usar en forma de porcentaje del total de intercambio
UsedSwap | Espacio de intercambio (MiB) en uso
PercentUsedSwap | Espacio de intercambio en uso en forma de porcentaje del total de intercambio

Esta clase de métricas tiene una sola instancia. atributo de "condición" Hello no tiene ningún valor útil y debe omitirse.

### <a name="builtin-metrics-for-hello-network-class"></a>métricas de Builtin para hello clase de red

Hola clase red de métricas proporciona información acerca de la actividad de red en interfaces de red individuales de una desde el inicio. LAD no expone las métricas de ancho de banda, las cuales pueden recuperarse a partir de métricas de host.

counter | Significado
------- | -------
BytesTransmitted | Total de bytes enviados desde el arranque
BytesReceived | Total de bytes recibidos desde el arranque
BytesTotal | Total de bytes enviados o recibidos desde el arranque
PacketsTransmitted | Total de paquetes enviados desde el arranque
PacketsReceived | Total de paquetes recibidos desde el arranque
TotalRxErrors | Número de errores de recepción desde el arranque
TotalTxErrors | Número de errores de transmisión desde el arranque
TotalCollisions | Número de conflictos notificados por los puertos de red de Hola desde el inicio

 Aunque esta clase está instanciada, LAD no admite la captura de agregados de métricas Network de todos los dispositivos de red. conjunto de métricas de hello tooobtain para una interfaz específica, como eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>métricas de Builtin para hello Filesystem (clase)

Hola clase Filesystem de métricas proporciona información sobre el uso del sistema de archivos. Valores absolutos y el porcentaje se notifican como se haría usuario ordinaria tooan mostrado (no raíz).

counter | Significado
------- | -------
FreeSpace | Espacio disponible en disco en bytes
UsedSpace | Espacio usado en disco en bytes
PercentFreeSpace | Porcentaje de espacio libre
PercentUsedSpace | Porcentaje de espacio usado
PercentFreeInodes | Porcentaje de inodes sin usar
PercentUsedInodes | Porcentaje de inodes asignados (en uso) sumado de todos los sistemas de archivos
BytesReadPerSecond | Bytes leídos por segundo
BytesWrittenPerSecond | Bytes escritos por segundo
BytesPerSecond | Bytes leídos o escritos por segundo
ReadsPerSecond | Operaciones de lectura por segundo
WritesPerSecond | Operaciones de escritura por segundo
TransfersPerSecond | Operaciones de lectura o escritura por segundo

Los valores agregados de todos los archivos del sistema pueden obtenerse estableciendo `"condition": "IsAggregate=True"`. Los valores para un sistema de archivos montado específico, como "/mnt", pueden obtenerse estableciendo `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>métricas de Builtin para hello clase de disco

Hola, clase de disco de las métricas de proporciona información sobre el uso de dispositivos de disco. Estas estadísticas aplican toohello toda la unidad. Si hay varios sistemas de archivos en un dispositivo, contadores de Hola para dicho dispositivo son, de hecho, agregan a lo largo de todas ellas.

counter | Significado
------- | -------
ReadsPerSecond | Operaciones de lectura por segundo
WritesPerSecond | Operaciones de escritura por segundo
TransfersPerSecond | Total de operaciones por segundo
AverageReadTime | Promedio de segundos por operación de lectura
AverageWriteTime | Promedio de segundos por operación de escritura
AverageTransferTime | Promedio de segundos por operación
AverageDiskQueueLength | Promedio de operaciones de disco en cola
ReadBytesPerSecond | Número de bytes leídos por segundo
WriteBytesPerSecond | Número de bytes escritos por segundo
BytesPerSecond | Número de bytes leídos o escritos por segundo

Los valores agregados de todos los discos pueden obtenerse estableciendo `"condition": "IsAggregate=True"`. conjunto de información de tooget para un dispositivo específico (por ejemplo, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Instalación y configuración de LAD 3.0 a través de CLI

Suponiendo que es la configuración protegida en el archivo hello PrivateConfig.json y la información de configuración pública está en PublicConfig.json, ejecute este comando:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

comando de Hola se da por supuesto que se usa el modo de administración de recursos de Azure de hello (arm) de hello CLI de Azure. tooconfigure LAD para implementación clásica del modelo de máquinas virtuales (ASM), cambiar demasiado el modo "asm" (`azure config mode asm`) y se omite el nombre del grupo de recursos de hello en comando Hola. Para obtener más información, vea hello [documentación de CLI multiplataforma](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Una configuración de LAD 3.0 de ejemplo

Se basa en hello anteriores definiciones, aquí un ejemplo de configuración de extensión de LAD 3.0 con algunas explicaciones. tooapply este ejemplo tooyour caso, debe usar su propio nombre de cuenta de almacenamiento, la cuenta de token de SAS y tokens EventHubs SAS.

### <a name="privateconfigjson"></a>PrivateConfig.json

Estos valores privados configuran lo siguiente:

* Una cuenta de almacenamiento
* Un token de SAS de cuenta que coincida
* Varios receptores (Json BLOB o Event Hubs con tokens SAS)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Estos valores públicos hacen que LAD:

* Cargar las métricas de porcentaje de tiempo de procesador y espacio en disco utilizado toohello `WADMetrics*` tabla
* Cargar mensajes de syslog facility "usuario" y la gravedad "información" toohello `LinuxSyslog*` tabla
* Cargar sin formato OMI consulta resultados (PercentProcessorTime y PercentIdleTime) toohello denominado `LinuxCPU` tabla
* Cargar anexadas líneas en el archivo `/var/log/myladtestlog` toohello `MyLadTestLog` tabla

En cualquier caso, también se cargan datos en:

* Almacenamiento de blobs de Azure (nombre del contenedor es tal como se define en el receptor de hello JsonBlob)
* Punto de conexión EventHubs (según lo especificado en el receptor de hello EventHubs)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Hola `resourceId` Hola configuración debe coincidir con que de escalas de máquina virtual VM u Hola Hola establecido.

* Métricas de la plataforma Windows Azure gráficos y las alertas sabe Hola resourceId de hello VM que está trabajando. Espera datos de hello toofind para la máquina virtual con la clave de búsqueda de hello resourceId Hola.
* Si usa el escalado automático de Azure, resourceId hello en la configuración de escalado automático de hello debe coincidir con resourceId hello usa LAD.
* Hola resourceId se integra en nombres de Hola de JsonBlobs escrito LAD.

## <a name="view-your-data"></a>Consulta de los datos

Usar datos de rendimiento de tooview portal Azure de Hola o establecer alertas:

![imagen](./media/diagnostic-extension/graph_metrics.png)

Hola `performanceCounters` datos siempre se almacenan en una tabla de almacenamiento de Azure. Las API de Azure Storage están disponibles para múltiples lenguajes y plataformas.

Datos que se envían los receptores tooJsonBlob se almacenan en blobs en la cuenta de almacenamiento de hello denominada Hola [protegido configuración](#protected-settings). Puede consumir datos de blob de hello mediante las API de almacenamiento de blobs de Azure.

Además, puede usar estos datos de Hola de tooaccess de herramientas de interfaz de usuario en el almacenamiento de Azure:

* Explorador de servidores de Visual Studio.
* [Explorador de Microsoft Azure Storage](https://azurestorageexplorer.codeplex.com/ "Explorador de Azure Storage").

Esta instantánea de una sesión de Microsoft Azure Storage Explorer muestra hello genera tablas de almacenamiento de Azure y contenedores desde una extensión de LAD 3.0 configurada correctamente en una máquina virtual de prueba. imagen de Hello no coincide exactamente con hello [configuración del ejemplo LAD 3.0](#an-example-lad-30-configuration).

![imagen](./media/diagnostic-extension/stg_explorer.png)

Vea Hola relevante [EventHubs documentación](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn cómo tooconsume mensajes publican tooan EventHubs extremo.

## <a name="next-steps"></a>Pasos siguientes

* Crear alertas métricas en [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para las métricas de Hola que recopila.
* Cree [gráficos de supervisión](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para las métricas.
* Obtenga información acerca de cómo demasiado[crear un conjunto de escalas de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) mediante el escalado automático toocontrol de métricas.
