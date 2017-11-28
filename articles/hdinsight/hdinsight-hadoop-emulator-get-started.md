---
title: Empleo de un espacio aislado o emulador de Hadoop - Azure HDInsight | Microsoft Docs
description: "Para empezar a obtener información sobre el ecosistema de Hadoop, puede configurar un espacio aislado de Hadoop desde Hortonworks en una máquina virtual de Azure. "
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
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="29a76-104">Empleo de un espacio aislado de Hadoop, un emulador en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="29a76-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="29a76-105">Aprenda a instalar el espacio aislado de Hadoop desde Hortonworks en una máquina virtual para obtener información sobre el ecosistema de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="29a76-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="29a76-106">El espacio aislado proporciona un entorno de desarrollo local para comprender Hadoop, el sistema de archivos distribuido de Hadoop (HDFS) y el envío de trabajos.</span><span class="sxs-lookup"><span data-stu-id="29a76-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="29a76-107">Cuando se haya familiarizado con Hadoop, puede empezar a usarlo en Azure mediante la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29a76-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="29a76-108">Para obtener más información sobre cómo empezar, consulte [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="29a76-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a76-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29a76-109">Prerequisites</span></span>
* <span data-ttu-id="29a76-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="29a76-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="29a76-111">Descárguelo e instálelo [aquí](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="29a76-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="29a76-112">Descarga e instalación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="29a76-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="29a76-113">Vaya a las [descargas de Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="29a76-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="29a76-114">Haga clic en **DOWNLOAD FOR VIRTUALBOX** (DESCARGAR PARA VIRTUALBOX) para descargar la última versión de Hortonworks Sandbox en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29a76-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="29a76-115">Se le pedirá que se registre en Hortonworks para poder descargar.</span><span class="sxs-lookup"><span data-stu-id="29a76-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="29a76-116">La descarga tarda de una a dos horas según la velocidad de la red.</span><span class="sxs-lookup"><span data-stu-id="29a76-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Imagen del vínculo para descargar Sandbox de Hortonworks para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="29a76-118">En la misma página web, haga clic en el vínculo **Import on Virtual Box** (Importar en Virtual Box para descargar un archivo PDF que contiene las instrucciones de instalación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29a76-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="29a76-119">Para descargar un espacio aislado de una versión más antigua de HDP, expanda el archivo:</span><span class="sxs-lookup"><span data-stu-id="29a76-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Archivo de Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="29a76-121">Inicio de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="29a76-121">Start the virtual machine</span></span>

1. <span data-ttu-id="29a76-122">Abra Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="29a76-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="29a76-123">En el menú **File** (Archivo), haga clic en **Import Appliance** (Importar aplicación) y luego especifique la imagen de Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a76-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="29a76-124">Seleccione el espacio aislado Hortonworks Sandbox, haga clic en **Start** (Iniciar) y luego en **Normal Start** (Inicio normal).</span><span class="sxs-lookup"><span data-stu-id="29a76-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="29a76-125">Una vez que la máquina virtual ha terminado el proceso de arranque, muestra instrucciones de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="29a76-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="29a76-127">Abra un explorador web y vaya a la dirección URL que se muestra (normalmente http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="29a76-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="29a76-128">Establecimiento de las contraseñas del espacio aislado</span><span class="sxs-lookup"><span data-stu-id="29a76-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="29a76-129">En el paso **get started** (introducción) de la página Sandbox de Hortonworks, seleccione **View Advanced Options** (Ver opciones avanzadas).</span><span class="sxs-lookup"><span data-stu-id="29a76-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="29a76-130">Use la información de esta página para iniciar sesión en el espacio aislado mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="29a76-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="29a76-131">Utilice el nombre y la contraseña proporcionada.</span><span class="sxs-lookup"><span data-stu-id="29a76-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29a76-132">Si no tiene instalado un cliente SSH, puede usar el SSH web que proporciona la máquina virtual en **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="29a76-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="29a76-133">La primera vez que se conecte mediante SSH, se le pedirá que cambie la contraseña de la cuenta raíz.</span><span class="sxs-lookup"><span data-stu-id="29a76-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="29a76-134">Escriba una contraseña nueva, que se usará al iniciar sesión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="29a76-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="29a76-135">Una vez que haya iniciado sesión, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="29a76-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="29a76-136">Cuando se le solicite, proporcione una contraseña para la cuenta de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="29a76-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="29a76-137">Esta se usará para tener acceso a la interfaz de usuario web de Ambari.</span><span class="sxs-lookup"><span data-stu-id="29a76-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="29a76-138">Uso de comandos de Hive</span><span class="sxs-lookup"><span data-stu-id="29a76-138">Use Hive commands</span></span>

1. <span data-ttu-id="29a76-139">Desde una conexión SSH en el espacio aislado, utilice el siguiente comando para iniciar el shell de Hive:</span><span class="sxs-lookup"><span data-stu-id="29a76-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="29a76-140">Una vez que se inició el shell, use lo siguiente para ver las tablas que se proporcionan con el espacio aislado:</span><span class="sxs-lookup"><span data-stu-id="29a76-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="29a76-141">Utilice lo siguiente para recuperar 10 filas de la tabla `sample_07` :</span><span class="sxs-lookup"><span data-stu-id="29a76-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="29a76-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29a76-142">Next steps</span></span>
* [<span data-ttu-id="29a76-143">Aprenda a usar Visual Studio con Sandbox de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="29a76-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="29a76-144">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="29a76-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="29a76-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="29a76-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

