---
title: "Personalización de los clústeres de Hadoop para el proceso de ciencia de datos en equipos | Microsoft Docs"
description: "Están disponibles módulos de Python populares en los clústeres de Hadoop de HDInsight de Azure personalizados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a>Personalización de los clústeres de Hadoop de HDInsight de Azure para el proceso de ciencia de datos en equipos | Azure
En este artículo se describe cómo personalizar un clúster de Hadoop para HDInsight mediante la instalación de Anaconda de 64 bits (Python 2.7) en cada nodo cuando el clúster se aprovisiona como un servicio HDInsight. También muestra cómo obtener acceso al nodo principal para enviar trabajos personalizados al clúster. Esta personalización provoca que muchos módulos populares de Python incluidos en Anaconda estén disponibles convenientemente para su uso en funciones definidas por el usuario (UDF) que están diseñadas para procesar los registros de Hive en el clúster. Para obtener instrucciones sobre los procedimientos utilizados en este escenario, consulte [Cómo enviar consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).

El siguiente menú redirige a temas en los que se describe cómo configurar los diversos entornos de ciencia de datos que usa el [proceso de ciencia de datos en equipos (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Personalizar el clúster de Hadoop de HDInsight de Azure
Para crear un clúster de Hadoop de HDInsight personalizado, empiece por iniciar sesión en el [**Portal de Azure clásico**](https://manage.windowsazure.com/), haga clic en **Nuevo** en la esquina inferior izquierda y, después, seleccione SERVICIOS DE DATOS -> HDINSIGHT -> **CREACIÓN PERSONALIZADA** para que aparezca la ventana **Detalles del clúster**. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Especifique el nombre del clúster a crear en la página de configuración 1 y acepte los valores predeterminados para los demás campos. Haga clic en la flecha para ir a la página de configuración siguiente. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

En la página de configuración 2, escriba el número de **NODOS DE DATOS**, seleccione la **REGIÓN/RED VIRTUAL** y seleccione los tamaños del **NODO PRINCIPAL** y del **NODO DE DATOS**. Haga clic en la flecha para ir a la página de configuración siguiente.

> [!NOTE]
> La **REGIÓN/RED VIRTUAL** tiene que ser la misma que la región de la cuenta de almacenamiento que se va a usar para el clúster de Hadoop de HDInsight. De lo contrario, en la cuarta página de configuración, la cuenta de almacenamiento no aparecerá en la lista desplegable de **NOMBRE DE LA CUENTA**.
> 
> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

En la página de configuración 3, proporcione un nombre de usuario y una contraseña para el clúster de Hadoop de HDInsight. **No** seleccione *Especificar la tienda de metadatos de Hive/Oozie*. A continuación, haga clic en la flecha para ir a la página de configuración siguiente. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

En la página de configuración 4, especifique el nombre de la cuenta de almacenamiento, el contenedor predeterminado del clúster de Hadoop de HDInsight. Si selecciona *Crear contenedor predeterminado* en la lista desplegable **CONTENEDOR PREDETERMINADO**, se creará un contenedor con el mismo nombre que el del clúster. Haga clic en la flecha para ir a la última página de configuración.

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

En la última página de configuración de **Acciones de script**, haga clic en el botón **Agregar acción de script** y rellene los campos de texto con los valores siguientes.

* **NOMBRE**: cualquier cadena como el nombre de esta acción de script.
* **TIPO DE NODO**: seleccione **Todos los nodos**.
* **URI del SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* es un contenedor público ubicado en la cuenta de almacenamiento. 
  * *getgoing* se usa para compartir archivos de script de PowerShell para facilitar el trabajo de los usuarios en Azure.
* **PARÁMETROS** : (dejar en blanco)

Por último, haga clic en la marca de verificación para iniciar la creación del clúster Hadoop de HDInsight personalizado. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a> Acceso al nodo principal del clúster de Hadoop
Debe habilitar el acceso remoto al clúster de Hadoop en Azure para poder acceder al nodo principal del clúster de Hadoop a través de RDP. 

1. Inicie sesión en el [**Portal de Azure clásico**](https://manage.windowsazure.com/), seleccione **HDInsight** a la izquierda, seleccione el clúster de Hadoop en la lista de clústeres, haga clic en la pestaña **CONFIGURACIÓN** y, después, haga clic en el icono **HABILITAR DE FORMA REMOTA** de la parte inferior de la página.
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. En la ventana **Configurar escritorio remoto** , escriba los campos NOMBRE DE USUARIO y CONTRASEÑA y seleccione la fecha de expiración del acceso remoto. A continuación, haga clic en la marca de verificación para habilitar el acceso remoto en el nodo principal del clúster de Hadoop.
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> El nombre de usuario y la contraseña para el acceso remoto no son el nombre de usuario y la contraseña que se utilizaron al crear el clúster de Hadoop. Se trata de un conjunto de credenciales independiente. Asimismo, la fecha de expiración del acceso remoto debe estar dentro de 7 días respecto a la fecha actual.
> 
> 

Después de habilitar el acceso remoto, haga clic en **CONECTAR** en la parte inferior de la página para conectarse de manera remota al nodo principal. Inicie sesión en el nodo principal del clúster de Hadoop mediante la especificación de las credenciales del usuario de acceso remoto que especificó anteriormente.

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Los pasos siguientes del proceso de análisis avanzado se asignan en el [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir otros que muevan datos a HDInsight, los procese y muestree en esa plataforma con el fin de prepararlos para el aprendizaje a partir de los datos mediante Azure Machine Learning.

Consulte [Envío de consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit) para obtener instrucciones sobre cómo acceder a los módulos de Python que se incluyen en Anaconda desde el nodo principal del clúster en las funciones definidas por el usuario (UDF) que se usan para procesar registros de Hive almacenados en el clúster.

