---
title: "aaaHow toodelete un clúster de HDInsight - Azure | Documentos de Microsoft"
description: "Obtener información sobre Hola distintas formas que puede eliminar un clúster de HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Eliminar un clúster de HDInsight con el explorador, PowerShell u Hola CLI de Azure

La facturación de clúster de HDInsight empieza cuando un clúster se crea y se detiene cuando se elimina el clúster de Hola. Se facturan por minuto realizando una prorrata, por lo que siempre debe eliminar aquellos que ya no se estén utilizando. En este documento, aprenderá cómo toodelete un clúster con Hola portal de Azure y Azure PowerShell, Hola 1.0 de CLI de Azure.

> [!IMPORTANT]
> Eliminación de un clúster de HDInsight no elimina las cuentas de almacenamiento de Azure de Hola o almacén de Data Lake asociado con el clúster de Hola. Puede volver a usar los datos almacenados en esos servicios Hola futuras.

## <a name="azure-portal"></a>Azure Portal

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y seleccione el clúster de HDInsight. Si su clúster de HDInsight no está anclado toohello panel, puede buscarlo por nombre mediante el campo de búsqueda de Hola.
   
    ![búsqueda del portal](./media/hdinsight-delete-cluster/navbar.png)

2. Una vez que abre hoja hello para el clúster de hello, seleccione hello **eliminar** icono. Cuando se le pida, seleccione **Sí** clúster de hello toodelete.
   
    ![eliminar icono](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Desde un símbolo del sistema de PowerShell, use Hola después de clúster de hello toodelete de comando:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.

## <a name="azure-cli-10"></a>CLI de Azure 1.0

Desde un símbolo del sistema, use Hola después de clúster de Hola toodelete:

    azure hdinsight cluster delete CLUSTERNAME

Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.

> [!NOTE]
> CLI de Azure 2.0 no admite la eliminación de clústeres de HDInsight en la actualidad (31 de julio de 2017).