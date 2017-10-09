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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Empleo de un espacio aislado de Hadoop, un emulador en una máquina virtual

Obtenga información acerca de cómo tooinstall Hola espacio aislado de Hadoop de Hortonworks en un toolearn de máquina virtual sobre ecosistema de Hadoop de Hola. espacio aislado de Hello proporciona un toolearn del entorno de desarrollo local acerca de Hadoop, el sistema de archivos distribuido de Hadoop (HDFS) y el envío de trabajos. Cuando se haya familiarizado con Hadoop, puede empezar a usarlo en Azure mediante la creación de un clúster de HDInsight. Para obtener más información acerca de cómo empezar tooget, consulte [empezar a trabajar con Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Requisitos previos
* [Oracle VirtualBox](https://www.virtualbox.org/). Descárguelo e instálelo [aquí](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Descargue e instale la máquina virtual de Hola
1. Examinar toohello [Hortonworks descarga](http://hortonworks.com/downloads/#sandbox).

2. Haga clic en **descargar para VIRTUALBOX** toodownload Hola espacio aislado de Hortonworks más reciente en una máquina virtual. Son solicitada tooregister con Hortonworks antes de que comience la descarga de Hola. Toma una toodownload de horas tootwo según la velocidad de red.
   
    ![Imagen del vínculo para descargar Sandbox de Hortonworks para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. De Hola la misma página web, haga clic en hello **importación en Virtual Box** vincular toodownload un PDF que contiene las instrucciones de instalación para la máquina virtual de Hola.

toodownload un espacio aislado versión anterior HDP, expanda archivo hello:

![Archivo de Hortonworks Sandbox](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Iniciar la máquina virtual de Hola

1. Abra Oracle VM VirtualBox.
2. De hello **archivo** menú, haga clic en **dispositivo de importación**y, a continuación, especifique Hola imagen de espacio aislado de Hortonworks.
1. Seleccione hello Hortonworks espacio aislado, haga clic en ejecutar **iniciar**y, a continuación, **inicio Normal**. Una vez que la máquina virtual de hello ha terminado el proceso de arranque de hello, muestra las instrucciones de inicio de sesión.
   
    ![Normal Start](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Abra un explorador web y navegue toohello dirección URL se muestra (normalmente http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Establecimiento de las contraseñas del espacio aislado

1. De hello **Introducción** paso de hello página de espacio aislado de Hortonworks, seleccione **opciones avanzadas de vista**. Utilice la información de hello en este toolog de página en espacio aislado de toohello mediante SSH. Usar nombre de Hola y la contraseña proporcionados.
   
   > [!NOTE]
   > Si no tiene instalado un cliente de SSH, puede usar Hola SSH basada en web proporciona en máquina virtual de hello en **http://localhost:4200 /**.
   > 
   
    Hello primera vez que se conecte mediante SSH, está toochange solicitadas Hola contraseña para la cuenta de hello raíz. Escriba una contraseña nueva, que se usará al iniciar sesión mediante SSH.

2. Una vez iniciada la sesión, escriba Hola siguiente comando:
   
        ambari-admin-password-reset
   
    Cuando se le solicite, proporcione una contraseña para hello Ambari cuenta de administrador. Se utiliza cuando se tiene acceso hello Ambari Web UI.

## <a name="use-hive-commands"></a>Uso de comandos de Hive

1. Desde un espacio aislado toohello de conexión SSH, use Hola siguiendo el shell de comandos toostart Hola Hive:
   
        hive
2. Una vez que se inicie el shell de hello, usar hello tooview Hola tablas que se proporcionan con el espacio aislado de hello siguientes:
   
        show tables;
3. Hola de uso siguientes tooretrieve 10 filas de hello `sample_07` tabla:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información acerca de cómo toouse Visual Studio con hello espacio aislado de Hortonworks](hdinsight-hadoop-emulator-visual-studio.md)
* [Cables de Hola de aprendizaje de hello espacio aislado de Hortonworks](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

