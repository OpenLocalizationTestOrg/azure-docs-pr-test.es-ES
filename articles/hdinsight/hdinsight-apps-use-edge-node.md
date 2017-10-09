---
title: "aaaUse vacía nodos perimetrales en clústeres de Hadoop en HDInsight - Azure | Documentos de Microsoft"
description: "Cómo tooadd una tooan de nodo de borde vacío HDInsight de clúster que puede usarse como un cliente y, a continuación, las aplicaciones de HDInsight de prueba/host."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Uso de nodos perimetrales en clústeres vacíos en HDInsight

Obtenga información acerca de cómo tooadd vacío arista clúster de HDInsight de tooan de nodo. Un nodo del borde vacío es una máquina virtual de Linux con hello mismas herramientas de cliente instalado y configurado como en hello headnodes, pero con ningún servicio de Hadoop que se esté ejecutando. Puede usar el nodo del borde de hello para tener acceso clúster hello, probar las aplicaciones cliente y las aplicaciones cliente de hospedaje. 

Puede agregar un clúster de HDInsight existente de borde vacío nodo tooan, tooa nuevo clúster al crear el clúster de Hola. La adición de un nodo perimetral vacío se realiza mediante una plantilla de Azure Resource Manager.  Hello en el ejemplo siguiente se muestra cómo se hizo utilizando una plantilla:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Tal y como se muestra en el ejemplo hello, si lo desea puede llamar un [acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md) tooperform la configuración adicional, como la instalación de [Apache matiz](hdinsight-hadoop-hue-linux.md) en el nodo del borde de Hola. secuencia de comandos de acción de secuencia de comandos de Hello debe ser públicamente accesible en web Hola.  Por ejemplo, si el script de Hola se almacena en el almacenamiento de Azure, use contenedores públicos o blobs públicos.

tamaño de máquina virtual de nodo de Hello borde debe cumplir los requisitos de tamaño de vm de nodo de hello HDInsight clúster trabajo. Para hello recomienda trabajo tamaños de máquinas virtuales de nodo, vea [Hadoop crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Después de haber creado un nodo del borde, puede conectar los nodos de borde de toohello mediante SSH y ejecutar el cliente de clúster de Hadoop de herramientas tooaccess hello en HDInsight.

> [!WARNING] 
> El uso de un nodo perimetral vacío con HDInsight se permite actualmente en versión preliminar. Componentes personalizados que están instalados en el nodo del borde de Hola reciban soporte comercialmente razonable de Microsoft. Esto podría suponer que disponga de su ayuda en los problemas que pueda encontrar. O bien, es posible que los recursos que se hace referencia toocommunity para obtener más ayuda. siguiente Hola es algunas de hello mayoría sitios activos para obtener ayuda de comunidad de hello:
>
> * [Foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Si usa una tecnología de Apache, es posible que pueda toofind asistencia a través de hello sitios de proyecto de Apache en [http://apache.org](http://apache.org), por ejemplo, hello [Hadoop](http://hadoop.apache.org/) sitio.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Agregar un clúster existente de borde nodo tooan
En esta sección, utilice un tooadd de plantilla un clúster de HDInsight existente de borde nodo tooan de administrador de recursos.  plantilla de administrador de recursos de Hello puede encontrarse en [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). plantilla de administrador de recursos de Hello llama a una acción de secuencia de comandos situada https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. script de Hola no realiza ninguna acción.  Es toodemonstrate al llamar a la acción de secuencia de comandos desde una plantilla de administrador de recursos.

**un clúster existente de borde vacío nodo tooan tooadd**

1. Si todavía no tiene uno, cree un clúster de HDInsight.  Vea el [Tutorial de Hadoop: introducción al uso de Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de Azure Resource Manager abierto Hola Hola portal de Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurar Hola propiedades siguientes:
   
   * **Suscripción**: seleccione una suscripción de Azure que se usa para crear clúster Hola.
   * **Grupo de recursos**: grupo de recursos de hello seleccione usado para clúster de HDInsight existente Hola.
   * **Ubicación**: Seleccionar ubicación de Hola Hola existente del clúster de HDInsight.
   * **Nombre del clúster**: escriba Hola nombre de un clúster de HDInsight existente.
   * **Tamaño de nodo en la periferia**: seleccione uno de los tamaños de máquinas virtuales de Hola. tamaño de máquina virtual de Hello debe cumplir los requisitos de tamaño de vm de nodo de trabajo de Hola. Para hello recomienda trabajo tamaños de máquinas virtuales de nodo, vea [Hadoop crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Arista nodo prefijo**: es el valor predeterminado de hello **nueva**.  Con el valor predeterminado de hello, es el nombre del nodo de hello borde **nueva edgenode**.  Puede personalizar el prefijo de Hola desde el portal de Hola. También puede personalizar el nombre completo de Hola de plantilla de Hola.

4. Comprobar **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**y, a continuación, haga clic en **compra** nodo del toocreate hello borde.

>[!IMPORTANT]
> Convertir un grupo de recursos de Azure de Hola de tooselect seguro para clúster de HDInsight existente Hola.  De lo contrario, obtendrá Hola error mensaje "no puede realizar la operación solicitada en el recurso anidado. No se encontró el recurso primario "&lt;ClusterName>"".

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Adición de un nodo perimetral al crear un clúster
En esta sección, se utiliza un clúster de HDInsight de toocreate de plantilla de administrador de recursos con un nodo del borde.  plantilla de administrador de recursos de Hello puede encontrarse en hello [Galería de plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). plantilla de administrador de recursos de Hello llama a una acción de secuencia de comandos situada https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. script de Hola no realiza ninguna acción.  Es toodemonstrate al llamar a la acción de secuencia de comandos desde una plantilla de administrador de recursos.

**un clúster existente de borde vacío nodo tooan tooadd**

1. Si todavía no tiene uno, cree un clúster de HDInsight.  Vea la [Introducción al uso de Hadoop en HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de Azure Resource Manager abierto Hola Hola portal de Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configurar Hola propiedades siguientes:
   
   * **Suscripción**: seleccione una suscripción de Azure que se usa para crear clúster Hola.
   * **Grupo de recursos**: crear un nuevo grupo de recursos usado para el clúster de Hola.
   * **Ubicación**: seleccione una ubicación para el grupo de recursos de Hola.
   * **Nombre del clúster**: escriba un nombre para hello toocreate de clúster nuevo.
   * **Nombre de usuario de inicio de sesión del clúster**: escriba nombre de usuario de Hadoop HTTP Hola.  es el nombre predeterminado de Hello **administración**.
   * **Contraseña de inicio de sesión del clúster**: escriba la contraseña de usuario de Hadoop HTTP Hola.
   * **SSH nombre de usuario**: escriba el nombre de usuario SSH de Hola. es el nombre predeterminado de Hello **sshuser**.
   * **SSH contraseña**: escriba la contraseña de usuario SSH de Hola.
   * **Instalar la acción de secuencia de comandos**: mantener el valor predeterminado de Hola para ir a través de este tutorial.
     
     Algunas propiedades han sido codificado de forma rígida en la plantilla de hello: tipo de clúster, el número de nodos de clúster trabajador, tamaño de nodo de borde y el nombre del nodo de borde.
4. Comprobar **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**y, a continuación, haga clic en **compra** clúster de hello toocreate con el nodo del borde de Hola.

## <a name="access-an-edge-node"></a>Acceso a un nodo perimetral
Hello borde nodo ssh extremo es &lt;EdgeNodeName >.&lt; Nombre del clúster >-ssh.azurehdinsight.net:22.  Por ejemplo, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

nodo de Hello borde aparece como una aplicación en hello portal de Azure.  Proporciona portal Hola Hola Hola de tooaccess información arista nodo mediante SSH.

**punto de conexión de tooverify hello borde nodo SSH**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Abra el clúster de HDInsight de hello con un nodo del borde.
3. Haga clic en **aplicaciones** de hoja de clúster de Hola. Verá que el nodo del borde de Hola.  es el nombre predeterminado de Hello **nueva edgenode**.
4. Haga clic en el nodo del borde de Hola. Verá que el punto de conexión de hello SSH.

**toouse Hive en el nodo del borde de Hola**

1. Utilice el nodo del borde SSH tooconnect toohello. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Después de haber conectado los nodos de borde de toohello mediante SSH, utilice Hola después de la consola de comandos tooopen Hola Hive:
   
        hive
3. Ejecute hello comando tooshow Hive tablas en clúster de hello siguientes:
   
        show tables;

## <a name="delete-an-edge-node"></a>Eliminación de un nodo perimetral
Puede eliminar un nodo del borde de hello portal de Azure.

**tooaccess un nodo del borde**

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Abra el clúster de HDInsight de hello con un nodo del borde.
3. Haga clic en **aplicaciones** de hoja de clúster de Hola. Verá una lista de nodos perimetrales.  
4. Nodo del menú contextual hello borde que desee toodelete y, a continuación, haga clic en **eliminar**.
5. Haga clic en **Sí** tooconfirm.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo tooadd un nodo del borde y cómo tooaccess Hola nodo del borde. toolearn más información, vea Hola siguientes artículos:

* [Instalar aplicaciones de HDInsight](hdinsight-apps-install-applications.md): Obtenga información acerca de cómo los clústeres tooinstall una tooyour de aplicación de HDInsight.
* [Instalar aplicaciones personalizadas de HDInsight](hdinsight-apps-install-custom-applications.md): Obtenga información acerca de cómo toodeploy una tooHDInsight de aplicación de HDInsight no publicado.
* [Publicar aplicaciones de HDInsight](hdinsight-apps-publish-applications.md): Obtenga información acerca de cómo toopublish su tooAzure de aplicaciones personalizada de HDInsight Marketplace.
* [MSDN: Instalar una aplicación de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Obtenga información acerca de cómo las aplicaciones de HDInsight de toodefine.
* [Personalizar los clústeres de HDInsight basados en Linux con acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md): Obtenga información acerca de cómo las aplicaciones adicionales de toouse acción de secuencia de comandos tooinstall.
* [Crear clústeres de Linux-based Hadoop en HDInsight con plantillas de administrador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Obtenga información acerca de cómo los clústeres toocreate de plantillas de administrador de recursos de toocall HDInsight.

