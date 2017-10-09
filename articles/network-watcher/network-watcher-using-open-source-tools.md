---
title: "aaaVisualize patrones de tráfico de red con Monitor de red de Azure y herramientas de código abierto | Documentos de Microsoft"
description: "Esta página describe el modo de captura de paquetes de Monitor de red de toouse con patrones de tráfico de Capanalysis toovisualize tooand de las máquinas virtuales."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualizar tooand de patrones de tráfico de red de las máquinas virtuales mediante herramientas de código abierto

Capturas de paquetes contienen datos de red que le permiten tooperform forenses de red y la inspección profunda de paquetes. Hay muchas abre herramientas de origen que puede usar tooanalyze paquete capturas toogain información acerca de la red. Una de estas herramientas es CapAnalysis, una herramienta de código abierto para la visualización de captura de paquetes. Visualización de los datos de captura de paquetes es una forma muy eficaz tooquickly derivar nuevas perspectivas sobre patrones y las anomalías de la red. Las visualizaciones también proporcionan un medio para compartir dicha información de una manera fácil de consumir.

Monitor de red de Azure proporciona que Hola toocapture capacidad captura estos valiosos datos permitiéndole tooperform paquetes en la red. En este artículo, se proporciona un tutorial sobre cómo visión toovisualize y mejora del paquete de captura usando CapAnalysis con Monitor de red.

## <a name="scenario"></a>Escenario

Tiene una aplicación web simple que se implementa en una máquina virtual en Azure desea toouse de código abierto herramientas toovisualize su tooquickly de tráfico de red identificar patrones de flujo y las posibles anomalías. Con Network Watcher, puede obtener una captura de paquetes de su entorno de red y almacenarla directamente en su cuenta de almacenamiento. CapAnalysis, a continuación, puede introducir captura directamente de hello paquetes desde blob de almacenamiento de Hola y ver su contenido.

![escenario][1]

## <a name="steps"></a>Pasos

### <a name="install-capanalysis"></a>Instalar CapAnalysis

tooinstall CapAnalysis en una máquina virtual, puede hacer referencia instrucciones oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aquí.
En el orden de acceso remoto CapAnalysis, necesitamos tooopen puerto 9877 en su máquina virtual mediante la adición de una nueva regla de seguridad de entrada. Para obtener más información sobre cómo crear reglas en grupos de seguridad de red, consulte demasiado[crear reglas en un NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Una vez que se ha agregado correctamente la regla de hello, debe ser capaz de tooaccess CapAnalysis de`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Usar toostart de Monitor de red de Azure un paquete de capturar sesión

Monitor de red permite el tráfico de tootrack de paquetes de toocapture dentro y fuera de una máquina virtual. Puede hacer referencia a las instrucciones de toohello en [captura de paquetes de administrar con Monitor de red](network-watcher-packet-capture-manage-portal.md) toostart una sesión de captura de paquetes. Esta captura de paquetes se puede almacenar en un toobe de blob de almacenamiento acceso CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Cargar un tooCapAnalysis de captura de paquetes
Puede cargar directamente una captura de paquetes realizada por el Monitor de red utilizando la pestaña de "Import from URL" hello y proporcionando un blob de almacenamiento de vínculo toohello donde se almacena la captura de paquetes de saludo.

Cuando se proporciona un vínculo tooCapAnalysis, asegúrese de tooappend seguro de una dirección URL de SAS toohello token almacenamiento blob.  toodo, vaya tooShared firma de acceso de cuenta de almacenamiento de hello, designar Hola permisos permitido y presione Hola generar SAS botón toocreate un token. A continuación, puede anexar esta dirección URL de SAS toohello token paquete captura almacenamiento blob.

Hello URL resultante tendrá un aspecto similar al siguiente: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Análisis de captura de paquetes

CapAnalysis ofrece varios toovisualize de opciones de la captura de paquete, cada análisis proporcionando desde una perspectiva distinta. Con estos resúmenes visuales, podrá entender las tendencias del tráfico de la red y detectar rápidamente cualquier actividad inusual. Hola lista siguiente muestra algunas de estas características:

1. Tablas de flujo

    Esto deja de tabla Hola lista de flujos de datos de paquetes de saludo, Hola marca de tiempo asociada a los flujos de Hola y Hola diversos protocolos asociados con el flujo de hello, así como IP de origen y de destino.

    ![Página de flujo de Capanalysis][5]

1. Información general sobre protocolos

    Este panel le permite tooquickly ver la distribución de Hola de tráfico de red a lo largo Hola distintos protocolos y regiones geográficas.

    ![Información general sobre protocolos de Capanalysis][6]

1. Estadísticas

    Este panel permite que las estadísticas de tráfico de red tooview: bytes enviados y recibidos de origen y destino IP, flujos para cada origen de Hola y de destino de direcciones IP, protocolo usado para varios flujos y la duración de Hola de flujos.

    ![Estadísticas de Capanalysis][7]

1. Geomap

    Este panel proporciona una vista del mapa del tráfico de red con toohello volumen de tráfico de cada país de ajuste de escala de colores. Puede seleccionar las estadísticas de países resaltados tooview flujo adicionales como la proporción de Hola de datos enviados y recibidos desde direcciones IP en ese país.

    ![Geomap][8]

1. Filtros

    CapAnalysis proporciona un conjunto de filtros para el análisis rápido de paquetes específicos. Por ejemplo, puede elegir datos de hello toofilter por información específica de protocolo toogain en ese subconjunto de tráfico.

    ![filters][11]

    Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn más información acerca de las capacidades de todos los CapAnalysis.

## <a name="conclusion"></a>Conclusión

Característica de captura de paquetes del Monitor de red permite análisis forense de red de toocapture Hola datos tooperform necesarios y comprender mejor el tráfico de red. En este escenario, hemos mostrado cómo las capturas de paquetes de Network Watcher se pueden integrar fácilmente con herramientas de visualización de código abierto. Mediante herramientas de código abierto como captura CapAnalysis toovisualize paquetes, puede realizar una inspección profunda de paquetes e identificar rápidamente las tendencias en el tráfico de red.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de los registros de flujo NSG, visite [registros de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)

Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
