---
title: aaaInstall RStudio con el servidor de R en HDInsight - Azure | Documentos de Microsoft
description: "Cómo tooinstall RStudio con el servidor de R en HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Instalación de RStudio con R Server en HDInsight

Este artículo describe cómo tooinstall Hola (gratis) versión de comunidad de [RStudio Server](https://www.rstudio.com/products/rstudio-server/) en el nodo de hello borde de un clúster con un script personalizado. RStudio Server proporciona un IDE basado en explorador que pueden usar los clientes remotos y se utiliza ampliamente en Linux. Hoy en día, hay varios entornos de desarrollo integrados (IDE) disponibles para R, incluidos los siguientes:

- [Herramientas de R para Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) de Microsoft 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- [StatET](http://www.walware.de/goto/statet) basado en Eclipse de Walware.

ventaja de Hola de instalar servidor de RStudio en el nodo de hello borde de un clúster de HDInsight es que proporciona una experiencia IDE completa para el desarrollo de Hola y ejecutar scripts de R a R Server en clúster de Hola. Esta configuración puede ser mucho más productiva que usan de manera predeterminada de hello consola de R.

> [!NOTE]
> procedimiento de Hello descrito en este artículo solo es pertinente si no ha seleccionado tooinstall edición community de servidor RStudio al aprovisionar el clúster. Si se ha agregado durante el aprovisionamiento, a continuación, tooaccess, hacer clic en hello **R Server paneles** mosaico en hello Azure portal entrada para el clúster, a continuación, en hello **R Studio Server** icono. 

Si lo prefiere toouse Hola comercial con licencia Pro versión del servidor de RStudio, debe seguir las instrucciones de instalación de Hola de [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Si utiliza un clúster de HDInsight para el que se instaló R con hello [acción de secuencia de comandos de R de instalar](hdinsight-hadoop-r-scripts-linux.md), pasos de hello en este documento no funcionarán correctamente tal como requiere que un servidor de R en clúster de HDInsight de Hola.
>
> 

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight de Azure con servidor de R instalado. Para obtener instrucciones, consulte [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md)(Introducción a R Server en clústeres de HDInsight).
* Un cliente SSH. Para distribuciones de Linux y Unix o Macintosh OS X, Hola `ssh` comando se proporciona con el sistema operativo de Hola. Para Windows, se recomienda [Cygwin](http://www.redhat.com/services/custom/cygwin/) con hello [opción OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), o [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Instalar RStudio en un clúster de hello mediante un script personalizado

Estos son los pasos de hello:

1. Identificar hello borde nodo de clúster de Hola. Para un clúster de HDInsight con el servidor de R, siguiente es la convención de nomenclatura de hello para el nodo principal y el nodo del borde.
   * Nodo principal `CLUSTERNAME-ssh.azurehdinsight.net`
   * Nodo perimetral `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH en el nodo del borde Hola de clúster hello mediante el patrón de nomenclatura de hello proporcionado en el paso 1. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Cuando lo haya hecho, se convierten en un usuario raíz en clúster de Hola. En la sesión de SSH de hello, utilice Hola siguiente comando:

        sudo su -

4. Descargue tooinstall de secuencia de comandos personalizada hello RStudio. Usar hello siguiente comando:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Cambiar los permisos de hello en el archivo de script personalizado de hello y ejecute el script de Hola. Usar hello siguientes comandos:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Si utiliza una contraseña SSH al crear un clúster de HDInsight con el servidor de R, puede omitir este paso y continuar toohello a continuación. Si ha usado una clave SSH en su lugar, clúster de hello toocreate, debe establecer una contraseña para el usuario SSH. Necesitará esta contraseña cuando se conecte tooRStudio. Ejecute hello siguientes comandos:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Cuando se le pida la **contraseña Kerberos actual**, presione **ENTRAR**.  Tenga en cuenta que debe reemplazar `USERNAME` por un usuario SSH de su clúster de HDInsight. Si la contraseña se ha configurado correctamente, debería ver Hola siguiente mensaje:

        passwd: password updated successfully

    Salga de sesión SSH Hola.

8. Crear un clúster de toohello de túnel SSH asignando `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` en hello HDInsight el clúster toohello equipo de cliente. Debe crear un túnel SSH antes de abrir una nueva sesión del explorador.

   * En un cliente Linux o un cliente de Windows con [Cygwin](http://www.redhat.com/services/custom/cygwin/), abra una sesión de terminal y usar hello siguiente comando:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Reemplace **nombre de usuario** con un usuario SSH para el clúster de HDInsight y reemplazar **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.
       También puede usar una clave SSH en lugar de una contraseña agregando `-i id_rsa_key`.        
   * Si usa un cliente de Windows con PuTTY:

     1. Abra PuTTY y escriba la información de conexión.
     2. Hola **categoría** toohello de la sección izquierda del cuadro de diálogo de hello, expanda **conexión**, expanda **SSH**y, a continuación, seleccione **túneles**.
     3. Proporcionar Hola siguiente información en hello **reenvío de puerto de opciones que controlan SSH** formulario:

        * **Puerto de origen** -Hola puerto en el cliente de Hola que desea tooforward. Por ejemplo, **8787**.
        * **Destino** : hello destino que se debe asigna toohello equipo de cliente local. Por ejemplo, **localhost:8787**.

            ![Creación de un túnel de SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Creación de un túnel de SSH")

     4. Haga clic en **agregar** tooadd Hola configuración y, a continuación, haga clic en **abiertos** tooopen una conexión SSH.
     5. Cuando se le solicite, inicie sesión en toohello server tooestablish un túnel SSH Hola de sesión y habilitar.

9. Abra un explorador web y escriba Hola después de la dirección URL basada en el puerto de Hola que especificó para el túnel de hello:

        http://localhost:8787/ 

10. Son tooenter solicitadas Hola SSH username y password tooconnect toohello clúster. Si usa una clave SSH al crear el clúster de hello, debe escribir contraseña de Hola que creó en el paso 5.

    ![Conectar visita Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "crear un túnel SSH")

11. tootest si hello RStudio instalación se realizó correctamente, puede ejecutar un script de prueba que ejecuta trabajos MapReduce y Spark en función de R en clúster de Hola. script de prueba de toodownload hello toorun en RStudio, Atrás toohello SSH consola e introduce Hola siguientes comandos:

    *    Si creó un clúster de Hadoop con R, use este comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Si creó un clúster de Spark con R, use este comando:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. En RStudio, verá Hola descargó el script de prueba. Haga doble clic en hello tooopen de archivo, seleccione contenido de hello del archivo hello y, a continuación, haga clic en **ejecutar**. Debería ver el resultado de hello en hello **consola** panel:

   ![Probar la instalación de hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "probar la instalación de Hola")

Otra opción sería tootype `source(testhdi.r)` o `source(testhdi_spark.r)` tooexecute script de Hola.

## <a name="see-also"></a>Otras referencias

* [Opciones de contexto de proceso del servidor de R en HDInsight Premium](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opciones de Azure Storage para R Server en HDInsight](hdinsight-hadoop-r-server-storage.md)

