---
title: aaaLearn con un espacio aislado de Hadoop - emulator - HDInsight de Azure | Documentos de Microsoft
description: "toostart de aprendizaje sobre el uso de Hola ecosistema de Hadoop, puede configurar un espacio aislado de Hadoop de Hortonworks en una máquina virtual de Azure. "
keywords: emulador de hadoop, espacio aislado de hadoop
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="41183-104">Empleo de un espacio aislado de Hadoop, un emulador en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="41183-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="41183-105">Obtenga información acerca de cómo tooinstall Hola espacio aislado de Hadoop de Hortonworks en un toolearn de máquina virtual sobre ecosistema de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="41183-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="41183-106">espacio aislado de Hello proporciona un toolearn del entorno de desarrollo local acerca de Hadoop, el sistema de archivos distribuido de Hadoop (HDFS) y el envío de trabajos.</span><span class="sxs-lookup"><span data-stu-id="41183-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="41183-107">Cuando se haya familiarizado con Hadoop, puede empezar a usarlo en Azure mediante la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41183-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="41183-108">Para obtener más información acerca de cómo empezar tooget, consulte [empezar a trabajar con Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41183-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41183-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="41183-109">Prerequisites</span></span>
* <span data-ttu-id="41183-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="41183-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="41183-111">Descárguelo e instálelo [aquí](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="41183-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="41183-112">Descargue e instale la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="41183-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="41183-113">Examinar toohello [Hortonworks descarga](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="41183-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="41183-114">Haga clic en **descargar para VIRTUALBOX** toodownload Hola espacio aislado de Hortonworks más reciente en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41183-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="41183-115">Son solicitada tooregister con Hortonworks antes de que comience la descarga de Hola.</span><span class="sxs-lookup"><span data-stu-id="41183-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="41183-116">Toma una toodownload de horas tootwo según la velocidad de red.</span><span class="sxs-lookup"><span data-stu-id="41183-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Imagen del vínculo para descargar Sandbox de Hortonworks para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="41183-118">De Hola la misma página web, haga clic en hello **importación en Virtual Box** vincular toodownload un PDF que contiene las instrucciones de instalación para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="41183-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="41183-119">toodownload un espacio aislado versión anterior HDP, expanda archivo hello:</span><span class="sxs-lookup"><span data-stu-id="41183-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Archivo de Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="41183-121">Iniciar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="41183-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="41183-122">Abra Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="41183-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="41183-123">De hello **archivo** menú, haga clic en **dispositivo de importación**y, a continuación, especifique Hola imagen de espacio aislado de Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="41183-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="41183-124">Seleccione hello Hortonworks espacio aislado, haga clic en ejecutar **iniciar**y, a continuación, **inicio Normal**.</span><span class="sxs-lookup"><span data-stu-id="41183-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="41183-125">Una vez que la máquina virtual de hello ha terminado el proceso de arranque de hello, muestra las instrucciones de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="41183-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="41183-127">Abra un explorador web y navegue toohello dirección URL se muestra (normalmente http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="41183-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="41183-128">Establecimiento de las contraseñas del espacio aislado</span><span class="sxs-lookup"><span data-stu-id="41183-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="41183-129">De hello **Introducción** paso de hello página de espacio aislado de Hortonworks, seleccione **opciones avanzadas de vista**.</span><span class="sxs-lookup"><span data-stu-id="41183-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="41183-130">Utilice la información de hello en este toolog de página en espacio aislado de toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="41183-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="41183-131">Usar nombre de Hola y la contraseña proporcionados.</span><span class="sxs-lookup"><span data-stu-id="41183-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41183-132">Si no tiene instalado un cliente de SSH, puede usar Hola SSH basada en web proporciona en máquina virtual de hello en **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="41183-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="41183-133">Hello primera vez que se conecte mediante SSH, está toochange solicitadas Hola contraseña para la cuenta de hello raíz.</span><span class="sxs-lookup"><span data-stu-id="41183-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="41183-134">Escriba una contraseña nueva, que se usará al iniciar sesión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="41183-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="41183-135">Una vez iniciada la sesión, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="41183-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="41183-136">Cuando se le solicite, proporcione una contraseña para hello Ambari cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="41183-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="41183-137">Se utiliza cuando se tiene acceso hello Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="41183-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="41183-138">Uso de comandos de Hive</span><span class="sxs-lookup"><span data-stu-id="41183-138">Use Hive commands</span></span>

1. <span data-ttu-id="41183-139">Desde un espacio aislado toohello de conexión SSH, use Hola siguiendo el shell de comandos toostart Hola Hive:</span><span class="sxs-lookup"><span data-stu-id="41183-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="41183-140">Una vez que se inicie el shell de hello, usar hello tooview Hola tablas que se proporcionan con el espacio aislado de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="41183-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="41183-141">Hola de uso siguientes tooretrieve 10 filas de hello `sample_07` tabla:</span><span class="sxs-lookup"><span data-stu-id="41183-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="41183-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41183-142">Next steps</span></span>
* [<span data-ttu-id="41183-143">Obtenga información acerca de cómo toouse Visual Studio con hello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="41183-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="41183-144">Cables de Hola de aprendizaje de hello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="41183-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="41183-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="41183-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

