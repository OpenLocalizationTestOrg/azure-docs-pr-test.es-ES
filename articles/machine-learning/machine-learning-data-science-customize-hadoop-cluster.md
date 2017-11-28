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
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="5e20c-103">Personalizar los clústeres de Hadoop de HDInsight de Azure de hello proceso de ciencia de datos de equipo</span><span class="sxs-lookup"><span data-stu-id="5e20c-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="5e20c-104">Este artículo describe cómo toocustomize una Hadoop de HDInsight de clúster mediante la instalación de 64 bits Anaconda (Python 2.7) en cada nodo al clúster de Hola se proporciona como un servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e20c-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="5e20c-105">También muestra cómo tooaccess Hola clúster de nodo principal toosubmit trabajos personalizados toohello.</span><span class="sxs-lookup"><span data-stu-id="5e20c-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="5e20c-106">Esta personalización tiene muchos módulos Python populares, que se incluyen en Anaconda, cómodamente disponibles para su uso en usuario definidas funciones (UDF) que están diseñadas tooprocess registros de Hive de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="5e20c-107">Para obtener instrucciones sobre los procedimientos de hello utilizados en este escenario, vea [cómo consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="5e20c-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="5e20c-108">menú siguiente Hello vincula tootopics que describen cómo tooset seguridad Hola varios entornos de ciencia de datos utilizan hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e20c-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="5e20c-109"><a name="customize"></a>Personalizar el clúster de Hadoop de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="5e20c-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="5e20c-110">iniciar toocreate un clúster de Hadoop de HDInsight personalizado, iniciando sesión demasiado[**portal de Azure clásico**](https://manage.windowsazure.com/), haga clic en **New** en hello izquierda abajo esquina y, a continuación, seleccione Servicios de datos -> HDINSIGHT -> **creación personalizada** toobring seguridad hello **detalles del clúster** ventana.</span><span class="sxs-lookup"><span data-stu-id="5e20c-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="5e20c-112">Entrada nombre Hola de hello toobe de clúster creado en la página de configuración 1 y acepte los valores predeterminados de Hola otros campos.</span><span class="sxs-lookup"><span data-stu-id="5e20c-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="5e20c-113">Haga clic en la página de configuración siguiente de hello flecha toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="5e20c-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="5e20c-115">En la página de configuración 2, escriba el número de Hola de **nodos de datos**, seleccione hello **región/red VIRTUAL**y seleccione tamaños Hola de hello **nodo principal** hello y**Datos nodo**.</span><span class="sxs-lookup"><span data-stu-id="5e20c-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="5e20c-116">Haga clic en la página de configuración siguiente de hello flecha toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="5e20c-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="5e20c-117">Hola **región/red VIRTUAL** tiene toobe Hola igual como región Hola de cuenta de almacenamiento de Hola que se va toobe destinada Hola clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e20c-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5e20c-118">En caso contrario, en la página de configuración de cuarto hello, cuenta de almacenamiento de hello no aparecerá en la lista desplegable de Hola de **nombre de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="5e20c-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="5e20c-120">En la página de configuración 3, proporcione un nombre de usuario y una contraseña para hello clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e20c-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5e20c-121">**No** Hola seleccione *ENTRAR Hola tienda de metadatos Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="5e20c-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="5e20c-122">A continuación, haga clic en página de configuración siguiente de hello flecha toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="5e20c-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="5e20c-124">En la página de configuración 4, especificar nombre de cuenta de almacenamiento hello, contenedor predeterminado de Hola de hello clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e20c-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="5e20c-125">Si selecciona *crear contenedor predeterminado* en hello **contenedor predeterminado** lista desplegable, un contenedor con hello el mismo nombre que se creará el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="5e20c-126">Haga clic en la página de configuración de última de hello flecha toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="5e20c-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="5e20c-128">En hello final **acciones de Script** página Configuración, haga clic en **Agregar acción de secuencia de comandos** botón y rellenar los campos de texto hello con hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="5e20c-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="5e20c-129">**NOMBRE de** -cualquier cadena que el nombre de Hola de esta acción de secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="5e20c-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="5e20c-130">**TIPO DE NODO**: seleccione **Todos los nodos**.</span><span class="sxs-lookup"><span data-stu-id="5e20c-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="5e20c-131">**URI del SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="5e20c-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="5e20c-132">*publicscripts* es un contenedor público en la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5e20c-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="5e20c-133">*getgoing* usamos tooshare PowerShell script archivos toofacilitate trabajo de los usuarios en Azure</span><span class="sxs-lookup"><span data-stu-id="5e20c-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="5e20c-134">**PARÁMETROS** : (dejar en blanco)</span><span class="sxs-lookup"><span data-stu-id="5e20c-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="5e20c-135">Por último, haga clic en creación de hello marca de verificación toostart Hola de clúster de Hadoop de HDInsight de saludo personalizado.</span><span class="sxs-lookup"><span data-stu-id="5e20c-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="5e20c-137"><a name="headnode"></a>Hola de acceso principal del nodo de clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="5e20c-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="5e20c-138">Debe habilitar el clúster de Hadoop de toohello de acceso remoto en Azure antes de poder acceder del nodo principal del clúster de Hadoop de Hola Hola a través de RDP.</span><span class="sxs-lookup"><span data-stu-id="5e20c-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="5e20c-139">Inicie sesión en toohello [ **portal de Azure clásico**](https://manage.windowsazure.com/), seleccione **HDInsight** Hola izquierda, seleccione el clúster de Hadoop en lista de Hola de clústeres, haga clic en hello  **CONFIGURACIÓN** ficha y, a continuación, haga clic en hello **habilitar de forma remota** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="5e20c-141">Hola **configurar Escritorio remoto** ventana, escriba Hola nombre de usuario y los campos de contraseña y seleccione la fecha de expiración de hello para el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="5e20c-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="5e20c-142">A continuación, haga clic en hello marca de verificación tooenable Hola acceso remoto toohello nodo principal del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="5e20c-144">nombre de usuario de Hello y una contraseña para el acceso remoto de hello no son nombre de usuario de Hola y la contraseña que usa al crear el clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="5e20c-145">Se trata de un conjunto de credenciales independiente.</span><span class="sxs-lookup"><span data-stu-id="5e20c-145">This is a separate set of credentials.</span></span> <span data-ttu-id="5e20c-146">Además, fecha de expiración de Hola de acceso remoto de hello tiene toobe dentro de 7 días a partir de hello fecha actual.</span><span class="sxs-lookup"><span data-stu-id="5e20c-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="5e20c-147">Después de habilita el acceso remoto, haga clic en **conectar** final Hola de hello tooremote de página en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="5e20c-148">Inicie una sesión en toohello nodo principal del clúster de Hadoop de hello escribiendo las credenciales de hello para el usuario de acceso remoto de Hola que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5e20c-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="5e20c-150">Hello pasos Hola avanzada de proceso de análisis asignadas en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir los pasos que mover datos a HDInsight, a continuación, procesarán y ejemplo allí como preparación para el aprendizaje a partir de los datos de Hola con el aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e20c-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="5e20c-151">Vea [cómo consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) para obtener instrucciones sobre cómo tooaccess Hola módulos de Python que se incluyen en Anaconda nodo principal de Hola de clúster de hello en funciones definidas por el usuario (UDF) que son utilizados tooprocess Hive registros guardados en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e20c-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

