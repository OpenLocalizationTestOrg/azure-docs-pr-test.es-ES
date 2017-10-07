---
title: aaaInstall sus propias aplicaciones personalizadas de Hadoop en HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de HDInsight de tooinstall en aplicaciones de HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Instalación de aplicaciones personalizadas de Hadoop en Azure HDInsight

En este artículo, aprenderá cómo tooinstall una aplicación de Hadoop en HDInsight de Azure, que no ha sido había publicado toohello portal de Azure. aplicación Hola se instalará en este artículo es [matiz](http://gethue.com/).

Una aplicación de HDInsight es una aplicación que los usuarios pueden instalar en un clúster de HDInsight basado en Linux.  Estas aplicaciones puede desarrollarlas Microsoft, fabricantes de software independientes (ISV) o el propio usuario.  

Otros artículos relacionados:

* [Instalar aplicaciones de HDInsight](hdinsight-apps-install-applications.md): Obtenga información acerca de cómo los clústeres tooinstall una tooyour de aplicación de HDInsight.
* [Publicar aplicaciones de HDInsight](hdinsight-apps-publish-applications.md): Obtenga información acerca de cómo toopublish su tooAzure de aplicaciones personalizada de HDInsight Marketplace.
* [MSDN: Instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Obtenga información acerca de cómo las aplicaciones de HDInsight de toodefine.

## <a name="prerequisites"></a>Requisitos previos
Si desea que las aplicaciones de HDInsight de tooinstall en un clúster de HDInsight existente, debe tener un clúster de HDInsight. toocreate uno, vea [crear clústeres](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). También puede instalar aplicaciones de HDInsight al crear un clúster de HDInsight.

## <a name="install-hdinsight-applications"></a>Install HDInsight applications
Las aplicaciones de HDInsight pueden instalarse cuando se crea un clúster o clúster de HDInsight de tooan existente. Para definir plantillas de Azure Resource Manager, consulte [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx)(MSDN: instalación de una aplicación de HDInsight).

archivos de Hello necesarios para implementar esta aplicación (matiz):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): plantilla de administrador de recursos de hello para la instalación de aplicaciones de HDInsight. Consulte [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: instalación de una aplicación de HDInsight) para desarrollar su propia plantilla de Resource Manager.
* [matiz install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): Hola acción de Script que se va a llamar por plantilla de administrador de recursos de Hola para configurar el nodo del borde Hola.
* [matiz binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): archivo binario del matiz Hola se llama desde hui install_v0.sh.
* [matiz-binarios-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): archivo binario del matiz Hola se llama desde hui install_v0.sh.
* [webwasb tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): una aplicación web de ejemplo (Tomcat) que se llama desde hui install_v0.sh.

**clúster de HDInsight existente tooinstall matiz tooan**

1. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola Portal de Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Este botón abre una plantilla de administrador de recursos en hello portal de Azure.  Hello plantilla del Administrador de recursos se encuentra en [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn cómo toowrite esta plantilla de administrador de recursos, consulte [MSDN: instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. De hello **parámetros** hoja, escriba Hola siguiente:

   * **ClusterName**: escriba nombre de hello del clúster de Hola donde desea que la aplicación de hello tooinstall. Debe ser un clúster existente.
3. Haga clic en **Aceptar** parámetros de hello toosave.
4. De hello **implementación personalizada** hoja, escriba **grupo de recursos**.  grupo de recursos de Hello es un contenedor que agrupa los clúster hello, cuenta de almacenamiento dependientes de Hola y otros recursos. Se requiere toouse Hola mismo grupo de recursos como clúster de Hola.
5. Haga clic en **Términos legales** y, luego, en **Crear**.
6. Comprobar hello **Pin toodashboard** casilla de verificación está seleccionada y, a continuación, haga clic en **crear**. Puede ver el estado de instalación de Hola desde el panel del portal Hola mosaico toohello anclado y notificaciones del portal de hello (haga clic en el icono de campana de hello en la parte superior de hello del portal de hello).  Toma aplicación de hello tooinstall unos 10 minutos.

**tooinstall matiz durante la creación de un clúster**

1. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola Portal de Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Este botón abre una plantilla de administrador de recursos en hello portal de Azure.  Hello plantilla del Administrador de recursos se encuentra en [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn cómo toowrite esta plantilla de administrador de recursos, consulte [MSDN: instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Sigue Hola instrucción toocreate clúster e instale el matiz. Para más información acerca de cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Además toohello portal de Azure, también puede usar [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) y [CLI de Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall plantillas de administrador de recursos.

## <a name="validate-hello-installation"></a>Validar la instalación de Hola
Puede comprobar el estado de la aplicación hello en la instalación de la aplicación de Azure toovalidate portal Hola Hola. Además, también puede validar todas las procedían de extremos HTTP seguridad según lo previsto y la página Web de hello si hay alguno:

**portal de matiz de hello tooopen**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** en el menú de la izquierda Hola.  Si no lo ve, haga clic en **Examinar** y en **Clústeres de HDInsight**.
3. Haga clic en el clúster de Hola donde instaló la aplicación hello.
4. De hello **configuración** hoja, haga clic en **aplicaciones** en hello **General** categoría. Verá que se **matiz** enumerados en hello **instalado aplicaciones** hoja.
5. Haga clic en **matiz** de propiedades de hello lista toolist Hola.  
6. Haga clic en el sitio de Web de hello página Web link toovalidate Hola; Abrir extremo Hola HTTP en un explorador toovalidate Hola matiz interfaz de usuario web, punto de conexión SSH de hello abierto mediante SSH. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Solucionar problemas de instalación de Hola
Puede comprobar el estado de instalación de aplicación Hola de notificaciones del portal de hello (haga clic en el icono de campana de hello en la parte superior de hello del portal de hello).

Si se produce un error en una instalación de la aplicación, puede ver los mensajes de error de Hola y depurar información desde 3 lugares:

* Aplicaciones de HDInsight: información general sobre los errores.

    Abrir clúster Hola desde el portal de Hola y haga clic en aplicaciones de hoja de configuración de hello:

    ![error de instalación de aplicaciones de hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Acción de secuencia de comandos de HDInsight: si el mensaje de error de las aplicaciones de HDInsight de hello indica un error de acción de secuencia de comandos, se presentan más detalles sobre los errores de script de Hola en panel de acciones de script de Hola.

    Haga clic en acción de secuencia de comandos de la hoja de configuración de Hola. Historial de la acción de secuencia de comandos muestra los mensajes de error de Hola

    ![error de acción de script de aplicaciones de hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Interfaz de usuario de Ambari Web: Si script de instalación de hello fue la causa de Hola de error de hello, use registros completos de interfaz de usuario de Ambari Web toocheck acerca de los scripts de instalación de Hola.

    Para más información, consulte [Solución de problemas](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Eliminación de aplicaciones de HDInsight
Hay varias maneras toodelete HDInsight aplicaciones.

### <a name="use-portal"></a>Mediante el portal
**tooremove una aplicación mediante el portal de Hola**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **clústeres de HDInsight** en el menú de la izquierda Hola.  Si no lo ve, haga clic en **Examinar** y en **Clústeres de HDInsight**.
3. Haga clic en el clúster de Hola donde instaló la aplicación hello.
4. De hello **configuración** hoja, haga clic en **aplicaciones** en hello **General** categoría. Aparecerá una lista de aplicaciones instaladas. Para este tutorial, **matiz** enumerados en hello **instalado aplicaciones** hoja.
5. Haga clic en aplicación de Hola que desee tooremove y, a continuación, haga clic en **eliminar**.
6. Haga clic en **Sí** tooconfirm.

Desde el portal de hello, también puede eliminar el clúster de Hola o eliminar el grupo de recursos de Hola que contiene la aplicación hello.

### <a name="use-azure-powershell"></a>Uso de Azure PowerShell
Con Azure PowerShell, puede eliminar el clúster de Hola o eliminar el grupo de recursos de Hola. Consulte [Eliminación de clústeres mediante Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Uso de CLI de Azure
Mediante la CLI de Azure, puede eliminar el clúster de Hola o eliminar grupo de recursos de Hola. Consulte la sección [Eliminación de clústeres mediante la CLI de Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Pasos siguientes
* [MSDN: Instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Obtenga información acerca de cómo toodevelop plantillas de administrador de recursos para la implementación de aplicaciones de HDInsight.
* [Instalar aplicaciones de HDInsight](hdinsight-apps-install-applications.md): Obtenga información acerca de cómo los clústeres tooinstall una tooyour de aplicación de HDInsight.
* [Publicar aplicaciones de HDInsight](hdinsight-apps-publish-applications.md): Obtenga información acerca de cómo toopublish su tooAzure de aplicaciones personalizada de HDInsight Marketplace.
* [Personalizar los clústeres de HDInsight basados en Linux con acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md): Obtenga información acerca de cómo las aplicaciones adicionales de toouse acción de secuencia de comandos tooinstall.
* [Crear clústeres de Linux-based Hadoop en HDInsight con plantillas de administrador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Obtenga información acerca de cómo los clústeres toocreate de plantillas de administrador de recursos de toocall HDInsight.
* [Usar los nodos de borde vacío en HDInsight](hdinsight-apps-use-edge-node.md): Obtenga información acerca de cómo toouse vacío arista nodo para obtener acceso a clúster de HDInsight, probar aplicaciones de HDInsight y hospedaje de aplicaciones de HDInsight.
