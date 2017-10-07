---
title: "clústeres de Hadoop aaaCustomize para hello proceso de ciencia de datos de equipo | Documentos de Microsoft"
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
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Personalizar los clústeres de Hadoop de HDInsight de Azure de hello proceso de ciencia de datos de equipo
Este artículo describe cómo toocustomize una Hadoop de HDInsight de clúster mediante la instalación de 64 bits Anaconda (Python 2.7) en cada nodo al clúster de Hola se proporciona como un servicio HDInsight. También muestra cómo tooaccess Hola clúster de nodo principal toosubmit trabajos personalizados toohello. Esta personalización tiene muchos módulos Python populares, que se incluyen en Anaconda, cómodamente disponibles para su uso en usuario definidas funciones (UDF) que están diseñadas tooprocess registros de Hive de clúster de Hola. Para obtener instrucciones sobre los procedimientos de hello utilizados en este escenario, vea [cómo consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

menú siguiente Hello vincula tootopics que describen cómo tooset seguridad Hola varios entornos de ciencia de datos utilizan hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Personalizar el clúster de Hadoop de HDInsight de Azure
iniciar toocreate un clúster de Hadoop de HDInsight personalizado, iniciando sesión demasiado[**portal de Azure clásico**](https://manage.windowsazure.com/), haga clic en **New** en hello izquierda abajo esquina y, a continuación, seleccione Servicios de datos -> HDINSIGHT -> **creación personalizada** toobring seguridad hello **detalles del clúster** ventana. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Entrada nombre Hola de hello toobe de clúster creado en la página de configuración 1 y acepte los valores predeterminados de Hola otros campos. Haga clic en la página de configuración siguiente de hello flecha toogo toohello. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

En la página de configuración 2, escriba el número de Hola de **nodos de datos**, seleccione hello **región/red VIRTUAL**y seleccione tamaños Hola de hello **nodo principal** hello y**Datos nodo**. Haga clic en la página de configuración siguiente de hello flecha toogo toohello.

> [!NOTE]
> Hola **región/red VIRTUAL** tiene toobe Hola igual como región Hola de cuenta de almacenamiento de Hola que se va toobe destinada Hola clúster de Hadoop de HDInsight. En caso contrario, en la página de configuración de cuarto hello, cuenta de almacenamiento de hello no aparecerá en la lista desplegable de Hola de **nombre de la cuenta**.
> 
> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

En la página de configuración 3, proporcione un nombre de usuario y una contraseña para hello clúster de Hadoop de HDInsight. **No** Hola seleccione *ENTRAR Hola tienda de metadatos Hive/Oozie*. A continuación, haga clic en página de configuración siguiente de hello flecha toogo toohello. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

En la página de configuración 4, especificar nombre de cuenta de almacenamiento hello, contenedor predeterminado de Hola de hello clúster de Hadoop de HDInsight. Si selecciona *crear contenedor predeterminado* en hello **contenedor predeterminado** lista desplegable, un contenedor con hello el mismo nombre que se creará el clúster de Hola. Haga clic en la página de configuración de última de hello flecha toogo toohello.

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

En hello final **acciones de Script** página Configuración, haga clic en **Agregar acción de secuencia de comandos** botón y rellenar los campos de texto hello con hello después de valores.

* **NOMBRE de** -cualquier cadena que el nombre de Hola de esta acción de secuencia de comandos
* **TIPO DE NODO**: seleccione **Todos los nodos**.
* **URI del SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* es un contenedor público en la cuenta de almacenamiento de Hola 
  * *getgoing* usamos tooshare PowerShell script archivos toofacilitate trabajo de los usuarios en Azure
* **PARÁMETROS** : (dejar en blanco)

Por último, haga clic en creación de hello marca de verificación toostart Hola de clúster de Hadoop de HDInsight de saludo personalizado. 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Hola de acceso principal del nodo de clúster de Hadoop
Debe habilitar el clúster de Hadoop de toohello de acceso remoto en Azure antes de poder acceder del nodo principal del clúster de Hadoop de Hola Hola a través de RDP. 

1. Inicie sesión en toohello [ **portal de Azure clásico**](https://manage.windowsazure.com/), seleccione **HDInsight** Hola izquierda, seleccione el clúster de Hadoop en lista de Hola de clústeres, haga clic en hello  **CONFIGURACIÓN** ficha y, a continuación, haga clic en hello **habilitar de forma remota** situado en la parte inferior de Hola de página de Hola.
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. Hola **configurar Escritorio remoto** ventana, escriba Hola nombre de usuario y los campos de contraseña y seleccione la fecha de expiración de hello para el acceso remoto. A continuación, haga clic en hello marca de verificación tooenable Hola acceso remoto toohello nodo principal del clúster de Hadoop de Hola.
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> nombre de usuario de Hello y una contraseña para el acceso remoto de hello no son nombre de usuario de Hola y la contraseña que usa al crear el clúster de Hadoop de Hola. Se trata de un conjunto de credenciales independiente. Además, fecha de expiración de Hola de acceso remoto de hello tiene toobe dentro de 7 días a partir de hello fecha actual.
> 
> 

Después de habilita el acceso remoto, haga clic en **conectar** final Hola de hello tooremote de página en el nodo principal de Hola. Inicie una sesión en toohello nodo principal del clúster de Hadoop de hello escribiendo las credenciales de hello para el usuario de acceso remoto de Hola que especificó anteriormente.

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Hello pasos Hola avanzada de proceso de análisis asignadas en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir los pasos que mover datos a HDInsight, a continuación, procesarán y ejemplo allí como preparación para el aprendizaje a partir de los datos de Hola con el aprendizaje automático de Azure.

Vea [cómo consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) para obtener instrucciones sobre cómo tooaccess Hola módulos de Python que se incluyen en Anaconda nodo principal de Hola de clúster de hello en funciones definidas por el usuario (UDF) que son utilizados tooprocess Hive registros guardados en el clúster de Hola.

