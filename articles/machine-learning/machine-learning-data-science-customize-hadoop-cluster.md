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
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="c9203-103">Personalización de los clústeres de Hadoop de HDInsight de Azure para el proceso de ciencia de datos en equipos | Azure</span><span class="sxs-lookup"><span data-stu-id="c9203-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="c9203-104">En este artículo se describe cómo personalizar un clúster de Hadoop para HDInsight mediante la instalación de Anaconda de 64 bits (Python 2.7) en cada nodo cuando el clúster se aprovisiona como un servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9203-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="c9203-105">También muestra cómo obtener acceso al nodo principal para enviar trabajos personalizados al clúster.</span><span class="sxs-lookup"><span data-stu-id="c9203-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="c9203-106">Esta personalización provoca que muchos módulos populares de Python incluidos en Anaconda estén disponibles convenientemente para su uso en funciones definidas por el usuario (UDF) que están diseñadas para procesar los registros de Hive en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c9203-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="c9203-107">Para obtener instrucciones sobre los procedimientos utilizados en este escenario, consulte [Cómo enviar consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="c9203-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="c9203-108">El siguiente menú redirige a temas en los que se describe cómo configurar los diversos entornos de ciencia de datos que usa el [proceso de ciencia de datos en equipos (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9203-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="c9203-109"><a name="customize"></a>Personalizar el clúster de Hadoop de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="c9203-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="c9203-110">Para crear un clúster de Hadoop de HDInsight personalizado, empiece por iniciar sesión en el [**Portal de Azure clásico**](https://manage.windowsazure.com/), haga clic en **Nuevo** en la esquina inferior izquierda y, después, seleccione SERVICIOS DE DATOS -> HDINSIGHT -> **CREACIÓN PERSONALIZADA** para que aparezca la ventana **Detalles del clúster**.</span><span class="sxs-lookup"><span data-stu-id="c9203-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="c9203-112">Especifique el nombre del clúster a crear en la página de configuración 1 y acepte los valores predeterminados para los demás campos.</span><span class="sxs-lookup"><span data-stu-id="c9203-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="c9203-113">Haga clic en la flecha para ir a la página de configuración siguiente.</span><span class="sxs-lookup"><span data-stu-id="c9203-113">Click the arrow to go to the next configuration page.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="c9203-115">En la página de configuración 2, escriba el número de **NODOS DE DATOS**, seleccione la **REGIÓN/RED VIRTUAL** y seleccione los tamaños del **NODO PRINCIPAL** y del **NODO DE DATOS**.</span><span class="sxs-lookup"><span data-stu-id="c9203-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="c9203-116">Haga clic en la flecha para ir a la página de configuración siguiente.</span><span class="sxs-lookup"><span data-stu-id="c9203-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="c9203-117">La **REGIÓN/RED VIRTUAL** tiene que ser la misma que la región de la cuenta de almacenamiento que se va a usar para el clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9203-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c9203-118">De lo contrario, en la cuarta página de configuración, la cuenta de almacenamiento no aparecerá en la lista desplegable de **NOMBRE DE LA CUENTA**.</span><span class="sxs-lookup"><span data-stu-id="c9203-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="c9203-120">En la página de configuración 3, proporcione un nombre de usuario y una contraseña para el clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9203-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c9203-121">**No** seleccione *Especificar la tienda de metadatos de Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="c9203-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="c9203-122">A continuación, haga clic en la flecha para ir a la página de configuración siguiente.</span><span class="sxs-lookup"><span data-stu-id="c9203-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="c9203-124">En la página de configuración 4, especifique el nombre de la cuenta de almacenamiento, el contenedor predeterminado del clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9203-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c9203-125">Si selecciona *Crear contenedor predeterminado* en la lista desplegable **CONTENEDOR PREDETERMINADO**, se creará un contenedor con el mismo nombre que el del clúster.</span><span class="sxs-lookup"><span data-stu-id="c9203-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="c9203-126">Haga clic en la flecha para ir a la última página de configuración.</span><span class="sxs-lookup"><span data-stu-id="c9203-126">Click the arrow to go to the last configuration page.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="c9203-128">En la última página de configuración de **Acciones de script**, haga clic en el botón **Agregar acción de script** y rellene los campos de texto con los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="c9203-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="c9203-129">**NOMBRE**: cualquier cadena como el nombre de esta acción de script.</span><span class="sxs-lookup"><span data-stu-id="c9203-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="c9203-130">**TIPO DE NODO**: seleccione **Todos los nodos**.</span><span class="sxs-lookup"><span data-stu-id="c9203-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="c9203-131">**URI del SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="c9203-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="c9203-132">*publicscripts* es un contenedor público ubicado en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9203-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="c9203-133">*getgoing* se usa para compartir archivos de script de PowerShell para facilitar el trabajo de los usuarios en Azure.</span><span class="sxs-lookup"><span data-stu-id="c9203-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="c9203-134">**PARÁMETROS** : (dejar en blanco)</span><span class="sxs-lookup"><span data-stu-id="c9203-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="c9203-135">Por último, haga clic en la marca de verificación para iniciar la creación del clúster Hadoop de HDInsight personalizado.</span><span class="sxs-lookup"><span data-stu-id="c9203-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="c9203-137"><a name="headnode"></a> Acceso al nodo principal del clúster de Hadoop</span><span class="sxs-lookup"><span data-stu-id="c9203-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="c9203-138">Debe habilitar el acceso remoto al clúster de Hadoop en Azure para poder acceder al nodo principal del clúster de Hadoop a través de RDP.</span><span class="sxs-lookup"><span data-stu-id="c9203-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="c9203-139">Inicie sesión en el [**Portal de Azure clásico**](https://manage.windowsazure.com/), seleccione **HDInsight** a la izquierda, seleccione el clúster de Hadoop en la lista de clústeres, haga clic en la pestaña **CONFIGURACIÓN** y, después, haga clic en el icono **HABILITAR DE FORMA REMOTA** de la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="c9203-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="c9203-141">En la ventana **Configurar escritorio remoto** , escriba los campos NOMBRE DE USUARIO y CONTRASEÑA y seleccione la fecha de expiración del acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="c9203-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="c9203-142">A continuación, haga clic en la marca de verificación para habilitar el acceso remoto en el nodo principal del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c9203-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="c9203-144">El nombre de usuario y la contraseña para el acceso remoto no son el nombre de usuario y la contraseña que se utilizaron al crear el clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c9203-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="c9203-145">Se trata de un conjunto de credenciales independiente.</span><span class="sxs-lookup"><span data-stu-id="c9203-145">This is a separate set of credentials.</span></span> <span data-ttu-id="c9203-146">Asimismo, la fecha de expiración del acceso remoto debe estar dentro de 7 días respecto a la fecha actual.</span><span class="sxs-lookup"><span data-stu-id="c9203-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="c9203-147">Después de habilitar el acceso remoto, haga clic en **CONECTAR** en la parte inferior de la página para conectarse de manera remota al nodo principal.</span><span class="sxs-lookup"><span data-stu-id="c9203-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="c9203-148">Inicie sesión en el nodo principal del clúster de Hadoop mediante la especificación de las credenciales del usuario de acceso remoto que especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9203-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Creación del espacio de trabajo](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="c9203-150">Los pasos siguientes del proceso de análisis avanzado se asignan en el [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir otros que muevan datos a HDInsight, los procese y muestree en esa plataforma con el fin de prepararlos para el aprendizaje a partir de los datos mediante Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c9203-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="c9203-151">Consulte [Envío de consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit) para obtener instrucciones sobre cómo acceder a los módulos de Python que se incluyen en Anaconda desde el nodo principal del clúster en las funciones definidas por el usuario (UDF) que se usan para procesar registros de Hive almacenados en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c9203-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

