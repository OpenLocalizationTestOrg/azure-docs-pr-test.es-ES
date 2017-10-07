---
title: "programación de aplicación de revisiones aaaConfigure OS para clústeres de HDInsight basados en Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de programación de aplicación de revisiones tooconfigure OS para HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Aplicación de revisión del SO para HDInsight 
Como un servicio administrado de Hadoop, HDInsight se encarga de aplicar revisiones Hola SO de hello subyacentes de las máquinas virtuales que se usan los clústeres de HDInsight. A partir del 1 de agosto de 2016, hemos cambiado directiva de aplicación de revisión de SO de invitado y Hola para clústeres de HDInsight basados en Linux (versión 3.4 o superior). objetivo de Hola de nueva directiva de hello es toosignificantly reducir el número de Hola de reinicios toopatching due. nueva directiva de Hello continuará toopatch las máquinas virtuales (VM) en Linux clústeres cada el lunes o el jueves a partir de 12.00 UTC de forma escalonada en nodos cualquier clúster determinado. Sin embargo, cualquier máquina virtual determinada solo se reiniciará como máximo una vez cada 30 días debido a la aplicación de revisiones tooguest OS. Además, Hola reiniciar por primera vez para un clúster recién creado no se realizará antes de 30 días a partir de la fecha de creación de clúster de Hola. Revisiones serán efectivos cuando se reinician hello las máquinas virtuales.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>¿Cómo tooconfigure Hola programación de aplicación de revisión de SO para clústeres de HDInsight basados en Linux
máquinas virtuales de Hello en un clúster de HDInsight necesita toobe reinicia ocasionalmente para que se pueden instalar revisiones de seguridad importantes. A partir del 1 de agosto de 2016, nuevos clústeres de HDInsight basados en Linux (versión 3.4 o superior,) se reinician con hello siguiente programación:

1. Una máquina virtual en clúster de hello puede reiniciar sólo para revisiones a lo sumo, una vez en un período de 30 días.
2. Hola reinicie inicial 12.00 UTC.
3. proceso de reinicio de Hola se escalona a lo largo de máquinas virtuales en clúster de hello, por lo que el clúster de hello sigue estando disponible durante el proceso de reinicio de Hola.
4. Hola reiniciar por primera vez para un clúster recién creado no se realizará antes de 30 días después de la fecha de creación de clúster de Hola.

Con la acción de secuencia de comandos de Hola que se describe en este artículo, puede modificar programación de aplicación de revisiones de hello OS como sigue:
1. Habilite o deshabilite los reinicios automáticos.
2. Frecuencia de Hola de conjunto de reinicia (días entre reinicios)
3. Establezca Hola día de semana de hello cuando se produce un reinicio

> [!NOTE]
> Esta acción de script solo funcionará con clústeres de HDInsight basado en Linux que se hayan creado después del 1 de agosto de 2016. Las revisiones solo entrarán en vigor una vez que se reinicien las máquinas virtuales. 
>

## <a name="how-toouse-hello-script"></a>¿Cómo toouse hello secuencia de comandos 

Cuando requiera Hola siguiendo la información mediante este script:
1. ubicación del script de Hola: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight utiliza esta toofind URI y ejecuta script de Hola en todas las máquinas virtuales de hello en clúster de Hola.
  
2. Hola tipos de nodos de clúster que se aplica el script de Hola a: nodo principal, workernode, zookeeper. Esta secuencia de comandos debe ser tipos de nodo de tooall aplicados en el clúster de Hola. Si no es de tipo de nodo tooa aplicado y, a continuación, Hola virtual máquinas para ese tipo de nodo continuará toouse Hola revisiones la programación anterior.


3.  Parámetro: este script acepta tres parámetros numéricos:

    | Parámetro | Definición |
    | --- | --- |
    | Habilite o deshabilite los reinicios automáticos |0 o 1. El valor 0 deshabilita los reinicios automáticos, mientras que 1 los habilita. |
    | Frecuencia |too90 7 (inclusive). número de Hola de toowait días antes de reiniciar las máquinas virtuales de Hola para las revisiones que requieren un reinicio. |
    | Día de la semana |1 too7 (inclusive). Un valor de 1 indica el reinicio de hello debe aparecer un lunes y 7 indica un ejemplo de Sunday.For, con parámetros de 1 60 2 resultados en automático se reinicia cada 60 días (como máximo) del martes. |
    | Persistencia |Al aplicar un clúster existente de script acción tooan, puede marcar el script de Hola conservada. Las secuencias de comandos persistentes se aplican cuando workernodes nuevos se agregan toohello clúster a través de las operaciones de ajuste de escala. |

> [!NOTE]
> Debe marcar esta secuencia de comandos conservada al aplicar tooan de clúster existente. En caso contrario, los nuevos nodos creados a través de las operaciones de ajuste de escala usará predeterminado de hello programación de aplicación de revisiones.
Si aplica la secuencia de comandos de Hola como parte del proceso de creación de clúster de Hola, se mantiene automáticamente.
>

## <a name="next-steps"></a>Pasos siguientes

Para pasos específicos sobre el uso de la acción de secuencia de comandos de hello, vea Hola siguientes secciones en hello [clústeres de HDInsight basados en Linuz personalizar mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md):

* [Uso de una acción de script durante la creación de un clúster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
