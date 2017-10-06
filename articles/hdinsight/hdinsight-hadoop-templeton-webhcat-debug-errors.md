---
title: aaaUnderstand y resuelva los errores de WebHCat en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooabout los errores comunes devuelven por WebHCat de HDInsight y cómo tooresolve ellos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Entender y resolver errores recibidos de WebHCat en HDInsight

Obtenga información acerca de los errores recibidos al usar WebHCat con HDInsight y cómo tooresolve ellos. WebHCat se usa internamente por herramientas de cliente, como PowerShell de Azure y Hola Data Lake Tools para Visual Studio.

## <a name="what-is-webhcat"></a>¿Qué es WebHCat?

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) es una API de REST para [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), una capa de administración de almacenamiento y tablas para Hadoop. WebHCat está habilitada de forma predeterminada en los clústeres de HDInsight y usa varios trabajos de toosubmit de herramientas, obtener el estado del trabajo, etc. sin iniciar sesión en el clúster de toohello.

## <a name="modifying-configuration"></a>Modificación de la configuración

> [!IMPORTANT]
> Algunos de los errores de hello indicados en este documento se producen porque se ha superado el máximo configurado. Cuando los pasos de resolución de hello mencionan que puede cambiar un valor, debe utilizar uno de hello siguiente tooperform Hola cambio:

* Para **Windows** clústeres: usar un valor de Hola de tooconfigure de acción de secuencia de comandos durante la creación del clúster. Para obtener más información, vea [Desarrollar acciones de script](hdinsight-hadoop-script-actions.md).

* Para **Linux** clústeres: valor de hello toomodify Ambari de uso (web o API de REST). Para obtener más información, vea [Administrar HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Configuración predeterminada

Si se supera Hola siguiendo los valores predeterminados, puede degradar el rendimiento de WebHCat o provocar errores:

| Configuración | Qué hace | Valor predeterminado |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |Hola número máximo de trabajos que pueden estar activas simultáneamente (pendiente o en ejecución) |10.000 |
| [templeton.exec.max-procs][max-procs] |número máximo de Hola de solicitudes que puede servir de forma simultánea |20 | |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |Hola número de días que el historial de trabajos que se conservarán |7 días |

## <a name="too-many-requests"></a>Demasiadas solicitudes

**Código de estado HTTP**: 429

| Causa | Resolución |
| --- | --- |
| Se ha superado Hola máximo de solicitudes simultáneas atendido por WebHCat por minuto (el valor predeterminado es 20) |Reducir el tooensure de carga de trabajo que no enviar más de número máximo de solicitudes simultáneas de Hola o aumentar el límite de solicitudes simultáneas de hello modificando `templeton.exec.max-procs`. Consulte [Modificación de la configuración](#modifying-configuration) para más información. |

## <a name="server-unavailable"></a>Servidor no disponible

**Código de estado HTTP**: 503

| Causa | Resolución |
| --- | --- |
| Este código de estado se produce normalmente durante la conmutación por error entre Hola principal y secundaria nodo principal para el clúster de Hola |Espere dos minutos y vuelva a intentar la operación de Hola |

## <a name="bad-request-content-could-not-find-job"></a>Contenido de solicitud incorrecta: no se encontró el trabajo.

**Código de estado HTTP**: 400

| Causa | Resolución |
| --- | --- |
| Detalles del trabajo se han limpiado por historial de trabajos de hello limpiador |período de retención predeterminado de Hello para el historial de trabajos es 7 días. período de retención de Hello predeterminado puede cambiarse modificando `mapreduce.jobhistory.max-age-ms`. Consulte [Modificación de la configuración](#modifying-configuration) para más información. |
| Se ha suprimido el trabajo debido a tooa conmutación por error |Vuelva a intentar el envío de trabajos para la tootwo minutos |
| Se usó un identificador de trabajo no válido |Compruebe si el Id. de trabajo de hello es correcto |

## <a name="bad-gateway"></a>Puerta de enlace incorrecta

**Código de estado HTTP**: 502

| Causa | Resolución |
| --- | --- |
| Recolección de elementos internos se está produciendo en hello WebHCat proceso |Espere toofinish de la colección de elementos no utilizados o reiniciar el servicio WebHCat de Hola |
| Tiempo de espera esperando una respuesta de hello servicio ResourceManager. Este error puede producirse cuando sale de número de Hola de aplicaciones activas máximo Hola configurado (el valor predeterminado es 10.000) |Espere a que se está ejecutando trabajos toocomplete o aumentar el límite de trabajos simultáneos de hello modificando `yarn.scheduler.capacity.maximum-applications`. Para obtener más información, vea hello [modificar configuración](#modifying-configuration) sección. |
| Intentar tooretrieve todos los trabajos a través de hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) llamada mientras `Fields` se establece demasiado`*` |No recupere *todos* los detalles del trabajo. En su lugar use `jobid` tooretrieve detalles para trabajos mayores sólo a determinados Id. de trabajo. O bien, no use `Fields` |
| Hola servicio WebHCat está inactivo durante la conmutación por error de nodo principal |Espere dos minutos y vuelva a intentar la operación de Hola |
| Hay más de 500 trabajos pendientes enviados a través de WebHCat |Espere hasta que hayan finalizado los trabajos pendientes actualmente antes de enviar más trabajos |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
