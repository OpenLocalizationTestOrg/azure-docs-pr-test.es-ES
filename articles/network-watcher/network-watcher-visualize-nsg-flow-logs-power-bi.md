---
title: registros de aaaVisualizing flujo de grupo de seguridad de red de Azure con Power BI | Documentos de Microsoft
description: "Esta página describe el funcionamiento de flujo NSG toovisualize los registros con Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Visualización de registros de flujo del grupo de seguridad de red con Power BI

Los registros de flujo de grupo de seguridad de red permiten tooview información sobre el tráfico IP de entrada y salida sobre los grupos de seguridad de red. Mostrarán salidos estos registros de flujo y flujos de entrada en cada regla, Hola flujo de hello NIC se aplica a, 5-tupla información acerca del flujo de hello (origen/destino IP, puerto de origen/destino, protocolo), y si el tráfico de Hola se permitirá o denegará.

Puede ser difícil toogain visiones flujo de registro de los datos mediante la búsqueda manualmente archivos de registro de hello. En este artículo se proporciona una solución toovisualize el flujo de más reciente registra y obtener información sobre el tráfico en la red.

## <a name="scenario"></a>Escenario

Hola siguiendo el escenario, nos conectamos cuenta de almacenamiento de Power BI desktop toohello que hemos configurado como receptor de Hola para nuestros datos del flujo de registro de NSG. Una vez se conecta la cuenta de almacenamiento tooour, Power BI descarga y analiza Hola registros tooprovide una representación visual del tráfico de Hola que se registra por grupos de seguridad de red.

Uso de objetos visuales de hello proporcionados en la plantilla de hello que puede examinar:

* Top Talkers
* Datos de flujo de serie temporal por decisión de regla y dirección
* Flujos por dirección MAC de la interfaz de red
* Flujos por NSG y regla
* Flujos por puerto de destino

plantilla de Hello proporcionada es editable para que pueda modificarlo tooadd nuevos datos, objetos visuales, o editar consultas toosuit sus necesidades.

## <a name="setup"></a>Configuración

Antes de empezar, tiene que tener el registro de flujo de grupo de seguridad de red habilitado en uno o más grupos de seguridad de red de su cuenta. Para obtener instrucciones acerca de cómo habilitar la seguridad de red de flujo de registros, consulte el artículo siguiente de toohello: [registro tooflow de introducción para grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).

También debe tener Hola Power BI Desktop instalado en su equipo y suficiente espacio libre en los máquina toodownload carga Hola datos del registro y que existe en la cuenta de almacenamiento.

![Diagrama de Visio][1]

### <a name="steps"></a>Pasos

1. Descarga y Hola abierto después de la plantilla de Power BI en Power BI Desktop aplicación Hola [plantilla de registros de flujo de PowerBI de Monitor de red](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Escriba los parámetros de consulta de hello necesario
    1. **StorageAccountName** – toohello especifica el nombre de cuenta de almacenamiento de hello registros de flujo NSG Hola contenedor que desea tooload y visualizar.
    1. **NumberOfLogFiles** : especifica el número de Hola de archivos de registro que se desee toodownload y visualizar en Power BI. Por ejemplo, si se especifica 50, Hola 50 archivos de registro más recientes. FF tenemos 2 NSG habilitado y configurado toosend NSG flujo registros toothis cuenta y luego hello las últimas 25 horas de registros se pueden ver.

    ![Ventana principal de Power BI][2]

1. Escriba Hola clave de acceso para la cuenta de almacenamiento. Puede encontrar las claves de acceso válido desplazándose tooyour cuenta de almacenamiento en hello Azure portal y seleccione **teclas de acceso** desde el menú de configuración de Hola. Haga clic en **Conectar** y aplique los cambios.

    ![Claves de acceso][3]

    ![Clave de acceso 2][4]

4.  Los registros están descargar y analizar y ahora pueden usar objetos visuales de hello creada previamente.

## <a name="understanding-hello-visuals"></a>Descripción de los objetos visuales de Hola

Proporcionado en hello plantilla son un conjunto de objetos visuales que le ayudan a tener sentido del programa Hola a los datos de registro de flujo de NSG. Hello siguientes imágenes muestran un ejemplo de panel Hola aspecto cuando se rellena con datos. A continuación se examina con más detalle cada objeto visual 

![Power BI][5]
 
Emisores de parte superior de Hello visual muestra Hola direcciones IP que se ha iniciado Hola mayoría de las conexiones a través de hello periodo especificado. tamaño de Hola de cuadros de hello corresponde toohello relativa número de conexiones. 

![Toptalkers][6]

Hello gráficos de series de tiempo siguientes muestran el número de Hola de flujos en el período de Hola. gráfico de Hello superior está segmentada por la dirección del flujo de Hola y Hola inferior se segmenta por decisión de hello realizada (permitir o denegar). Con este objeto visual, puede examinar las tendencias del tráfico a través del tiempo y detectar cualquier pico o disminución anómala la segmentación del tráfico.

![flowsoverperiod][7]

Hello gráficos siguientes muestran Hola flujos interfaz de red, con hello superior segmentadas por la dirección del flujo y Hola inferior segmentadas por decisión realizada por. Con esta información, puede obtener información sobre cuáles de las máquinas virtuales que se comunicó Hola mayoría tooothers relativa, y si el tráfico tooa VM específica se está permitido o denegado.

![flowspernic][8]

Hola siguiendo el gráfico de anillos rueda muestra un desglose de los flujos por puerto de destino. Con esta información, puede ver los puertos de destino de hello suelen usada utilizados en hello especificado período.

![anillo][9]

Hello siguiente gráfico de barras muestra hello flujo NSG y reglas. Con esta información, puede ver hello NSG responsables de hello mayoría tráfico y desglose de Hola de tráfico en un NSG por regla.

![gráfico de barras][10]
 
Hello siguientes gráficos informativos muestran información acerca de los NSG Hola presente en los registros de hello, Hola número de flujos capturados por período de Hola y fecha de Hola de registro más antiguo de hello capturado. Esta información ofrece una idea de qué NSG se registren y Hola intervalo de fechas de flujos.

![infochart1][11]

![infochart2][12]

Esta plantilla incluye Hola siguientes tooallow segmentaciones de datos solo datos de hello tooview está más interesado en. Puede filtrar por grupos de recursos, NSG y reglas. También puede filtrar por información de la tupla de 5, la decisión y la hora de Hola Hola registro se escribe.

![segmentaciones][13]

## <a name="conclusion"></a>Conclusión

También hemos mostrado en este escenario que mediante el uso de registros de flujo de grupo de seguridad de red proporcionados por el Monitor de red y Power BI, estamos toovisualize capaz y comprender el tráfico Hola. Mediante la plantilla de hello proporcionado, Power BI descarga registros de hello directamente desde el almacenamiento y las procesa localmente. Plantilla de tiempo que tarda tooload Hola varía en función número Hola de archivos solicitados y descarga de tamaño total de archivos.

Sentirse toocustomize libre esta plantilla para sus necesidades. Hay muchas formas en las que puede utilizar Power BI con los registros de flujo de grupo de seguridad de red. 

## <a name="notes"></a>Notas

* De forma predeterminada los registros se almacenan en `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Si hay otros datos en otro directorio Hola a toopull de las consultas y proceso Hola datos deben modificarse.

* plantilla de Hello proporcionada no se recomienda para su uso con más de 1 GB de registros.

* Si tiene una gran cantidad de registros, recomendamos que investigue una solución utilizando otro almacén de datos como Data Lake o SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toovisualize su flujo NSG registra con hello Elastick pila visitando [visualizar tooand de patrones de tráfico de red de las máquinas virtuales mediante herramientas de código abierto](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
