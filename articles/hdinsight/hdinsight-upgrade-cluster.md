---
title: "versión más reciente del tooa de clúster HDInsight aaaUpgrade-Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooUpgrade HDInsight clúster tooa de versión más reciente."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Actualizar la versión más reciente de tooa de clúster de HDInsight
tootake aprovechar Hola características más recientes de HDInsight, se recomienda que los clústeres de HDInsight sea versión toolatest actualizado. Siga hello debajo directrices tooupgrade las versiones del clúster de HDInsight.

> [!NOTE]
> Los clústeres de HDInsight de las versiones 3.2 y 3.3 se están acercando a la fecha de retirada. Para más información sobre las versiones admitidas de HDInsight, consulte [Versiones de los componentes de HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Tareas de actualización
tooupgrade de flujo de trabajo de Hola clúster de HDInsight es como sigue.

![Diagrama de flujo de trabajo de actualización](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Leer cada sección de este documento toounderstand cambios que podrían ser necesarios cuando se actualiza el clúster de HDInsight.
2. Cree un clúster como entorno de control de calidad o de pruebas. Para obtener más información acerca de cómo crear un clúster, consulte [Obtenga información acerca de cómo toocreate HDInsight basados en Linux clústeres](hdinsight-hadoop-provision-linux-clusters.md)
3. Copia receptores toohello nuevo entorno, orígenes de datos y trabajos existentes. Vea [copiar datos tooTest entorno](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para obtener más detalles.
4. Realizar pruebas toomake seguro de que los trabajos funcionan según lo previsto en el nuevo clúster de Hola de validación.


Una vez haya comprobado que todo funciona según lo esperado, programe el tiempo de inactividad para la migración de Hola. Durante este tiempo de inactividad, Hola acciones siguientes:

1.  Realizar una copia de los datos transitorios almacenados localmente en nodos de clúster de Hola. Por ejemplo, si tiene datos que se almacenan directamente en un nodo principal.
2.  Eliminar el clúster existente de Hola.
3.  Crear un clúster de Hola misma red virtual subred con más reciente (o compatibles) HDI versión mediante Hola mismo almacén de datos predeterminada que Hola anterior clúster utilizado. Esto permite Hola nuevo clúster toocontinue trabajan con los datos de producción existentes.
4.  Importe los datos transitorios cuya copia de seguridad realizó.
5.  Iniciar trabajos/continuar procesando usando Hola nuevo clúster.

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información acerca de cómo toocreate HDInsight basados en Linux clústeres](hdinsight-hadoop-provision-linux-clusters.md)
* [Conectar tooHDInsight mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Administración de un clúster basado en Linux mediante Ambari](hdinsight-hadoop-manage-ambari.md)

