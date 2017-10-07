---
title: "ejemplos de inicio rápido de aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de ejemplo de la CLI 1.0 para las características de Azure Monitor. Monitor de Azure es un servicio de Microsoft Azure que permite las notificaciones de alerta de toosend, direcciones URL web de llamada en función de los valores de los datos de telemetría configurado y servicios de escalado automático en la nube, máquinas virtuales y aplicaciones Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Ejemplos de inicio rápido de la CLI multiplataforma de Azure Monitor 1.0
Este artículo se demuestra que tome las muestras toohelp de comandos de interfaz de línea de comandos (CLI) tener acceso a características del Monitor de Azure. Monitor de Azure le permite tooAutoScale servicios en la nube, máquinas virtuales y las aplicaciones Web y toosend notificaciones de alerta o direcciones URL de web de llamada basadas en valores de datos de telemetría configurado.

> [!NOTE]
> Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016. Sin embargo, los espacios de nombres de hello y, por lo tanto, comandos de hello siguientes sigue sin contengan visión"Hola".
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Si aún no ha instalado Hola CLI de Azure, consulte [Install hello Azure CLI](../cli-install-nodejs.md). Si no está familiarizado con la CLI de Azure, puede obtener más información al respecto en [Hola Utilice CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](../xplat-cli-azure-resource-manager.md).

En Windows, instale npm de hello [sitio Web de Node.js](https://nodejs.org/). Después de completar la instalación de hello, usando CMD.exe con privilegios de ejecutar como administrador, ejecute siguiente Hola de carpeta Hola donde está instalado npm:

```console
npm install azure-cli --global
```

A continuación, desplácese tooany/ubicación de la carpeta que desee y escriba en Hola de línea de comandos:

```console
azure help
```

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure
Hola primer paso es toologin tooyour cuenta de Azure.

```console
azure login
```

Después de ejecutar este comando, tiene toosign en a través de instrucciones de hello en pantalla de bienvenida. Después, podrá ver el id. predeterminado de la suscripción, el id. de inquilino y la cuenta. Todos los comandos funcionan en el contexto de Hola de su suscripción de manera predeterminada.

detalles de hello toolist de su suscripción actual, use Hola siguiente comando.

```console
azure account show
```

toochange trabajo contexto tooa otra suscripción, Hola de uso siguiente comando.

```console
azure account set "subscription ID or subscription name"
```

toouse Administrador de recursos de Azure y Azure Monitor comandos, necesita toobe en modo Azure Resource Manager.

```console
azure config mode arm
```

tooview una lista de todos los comandos admitidos de Monitor de Azure, realice siguiente Hola.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Visualización del registro de actividades para una suscripción
tooview una lista de eventos de registro de actividad, realice el siguiente Hola.

```console
azure insights logs list [options]
```

Intente Hola después tooview todas las opciones disponibles.

```console
azure insights logs list -help
```

Este es un ejemplo registros toolist por un grupo de recursos

```console
azure insights logs list --resourceGroup "myrg1"
```

Registros de toolist de ejemplo de llamada

```console
azure insights logs list --caller "myname@company.com"
```

Registros de toolist de ejemplo por el llamador en un tipo de recurso, dentro de una fecha de inicio y finalización

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Uso de alertas
Puede utilizar información de hello en hello sección toowork con las alertas.

### <a name="get-alert-rules-in-a-resource-group"></a>Obtención de reglas de alerta en un grupo de recursos
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Creación de una regla de alerta de métrica
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Creación de una regla de alerta de WebTest
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Creación una regla de alerta
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Perfiles de registro
Utilice la información de hello en este toowork sección con los perfiles de registro.

### <a name="get-a-log-profile"></a>Obtención de un perfil de registro
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Adición de un perfil de registro sin retención de datos
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Eliminación de un perfil de registro
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Adición de un perfil de registro con retención de datos
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Adición de un perfil de registro con retención y EventHub
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnóstico
Utilice la información de hello en este toowork sección con la configuración de diagnóstico.

### <a name="get-a-diagnostic-setting"></a>Obtención de la configuración de diagnóstico
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Deshabilitación de la configuración de diagnóstico
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Habilitación de la configuración de diagnóstico sin retención
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
Utilice la información de hello en este toowork sección con la configuración de escalado automático. Debe toomodify estos ejemplos.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Obtención de la configuración de escalado automático de un grupo de recursos
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Obtención de valores de escalado automático por su nombre en un grupo de recursos
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Establecimiento de la configuración de escalado automático
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
