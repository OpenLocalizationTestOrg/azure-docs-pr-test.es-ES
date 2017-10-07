---
title: "aaaIIS registros de análisis de registros | Documentos de Microsoft"
description: "Internet Information Services (IIS) almacena la actividad de usuario en archivos de registro que Log Analytics puede recopilar.  Este artículo describe cómo tooconfigure colección de registros de IIS y los detalles de los registros de hello crean en el repositorio de OMS Hola."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Registros de IIS en Log Analytics
Internet Information Services (IIS) almacena la actividad de usuario en archivos de registro que Log Analytics puede recopilar.  

![Registros IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configuración de registros de IIS
Log Analytics recopila entradas de archivos de registro creados por IIS, por lo que debe [configurar IIS para el registro](https://technet.microsoft.com/library/hh831775.aspx).

Log Analytics solo admite archivos de registro de IIS almacenados en el formato W3C y no admite campos personalizados ni Advanced Logging de IIS.  
Log Analytics no recopila registros en formato nativo de IIS ni NCSA.

Configurar registros de IIS en el análisis de registros de hello [menú datos de configuración de análisis de registro](log-analytics-data-sources.md#configuring-data-sources).  No se requiere otra configuración que seleccionar **Collect W3C format IIS log files**(Recopilar archivos de registro de IIS en formato W3C).

Se recomienda que, cuando se habilita la recopilación de registros IIS, debe configurar configuración de sustitución incremental de registro IIS de hello en cada servidor.

## <a name="data-collection"></a>Colección de datos
Log Analytics recopila entradas de registro de IIS de cada origen conectado a intervalos de, aproximadamente, 15 minutos.  agente de Hello registra su lugar en cada registro de eventos que recopila de.  Si el agente de Hola se queda sin conexión, análisis de registros recopila eventos desde donde se quedó, incluso si se crearon los eventos mientras el agente de hello estaba sin conexión.

## <a name="iis-log-record-properties"></a>Propiedades de registro de IIS
Entradas del registro de IIS tienen un tipo de **W3CIISLog** y que tienen propiedades de hello en hello en la tabla siguiente:

| Propiedad | Descripción |
|:--- |:--- |
| Equipo |Nombre del equipo de Hola que Hola eventos se recopilaron de. |
| cIP |Dirección IP del cliente de Hola. |
| csMethod |Método de solicitud de hello como GET o POST. |
| csReferer |Sitio que Hola usuario seguido un vínculo de sitio actual toohello. |
| csUserAgent |Tipo de explorador del cliente de Hola. |
| csUserName |Nombre del programa Hola a autentica el usuario que ha tenido acceso Hola servidor. Los usuarios anónimos se indican con un guion. |
| csUriStem |Destino de la solicitud de hello como una página web. |
| csUriQuery |Consulta, si los hay, ese cliente hello estaba intentando tooperform. |
| ManagementGroupName |Nombre del grupo de administración de hello agentes de Operations Manager.  En el caso de los otros agentes, es AOI-\<id. de área de trabajo\>. |
| RemoteIPCountry |País de dirección IP de hello del cliente de Hola. |
| RemoteIPLatitude |Latitud de la dirección IP del cliente Hola. |
| RemoteIPLongitude |Longitud de dirección IP del cliente Hola. |
| scStatus |Código de estado HTTP. |
| scSubStatus |Código de error de subestado. |
| scWin32Status |Código de estado de Windows. |
| sIP |Dirección IP del servidor web de Hola. |
| SourceSystem |OpsMgr |
| sPort |Puerto en el cliente de Hola Hola server conectado a. |
| sSiteName |Nombre del sitio IIS de Hola. |
| TimeGenerated |Se registró la entrada de Hola de fecha y hora. |
| TimeTaken |Solicitud de longitud de hello tooprocess de tiempo en milisegundos. |

## <a name="log-searches-with-iis-logs"></a>Búsquedas de registros con registros de IIS
Hello tabla siguiente proporciona diferentes ejemplos de consultas de registro que recuperar entradas de registro IIS.

| Consultar | Descripción |
|:--- |:--- |
| Type=W3CIISLog |Todos los registros de IIS. |
| Type=W3CIISLog scStatus=500 |Todas las entradas de registro IIS con un estado de retorno de 500. |
| Type=W3CIISLog &#124; Measure count() by cIP |Contador de entradas de registro de IIS por dirección IP del cliente. |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Recuento de IIS entradas del registro por dirección URL sobre Hola host www.contoso.com. |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |Total de bytes recibidos por cada equipo de IIS |

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.

> | Consultar | Descripción |
|:--- |:--- |
| W3CIISLog |Todos los registros de IIS. |
| W3CIISLog &#124; where scStatus==500 |Todas las entradas de registro IIS con un estado de retorno de 500. |
| W3CIISLog &#124; summarize count() by cIP |Contador de entradas de registro de IIS por dirección IP del cliente. |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Recuento de IIS entradas del registro por dirección URL sobre Hola host www.contoso.com. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |Total de bytes recibidos por cada equipo de IIS |

## <a name="next-steps"></a>Pasos siguientes
* Configurar análisis de registros toocollect otros [orígenes de datos](log-analytics-data-sources.md) para el análisis.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.
* Configurar alertas en los análisis de registros tooproactively avisarle de condiciones importantes que se encuentra en los registros de IIS.
