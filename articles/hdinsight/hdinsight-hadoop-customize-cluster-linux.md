---
title: "clústeres de HDInsight aaaCustomize mediante acciones de script - Azure | Documentos de Microsoft"
description: "Agregar componentes personalizados de que clústeres de HDInsight basados en tooLinux mediante acciones de Script. Acciones de script son scripts de Bash que pueden ser usado toocustomize configuración de clúster de Hola o agregar servicios adicionales y utilidades como el matiz, Solr o R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)

HDInsight proporciona una opción de configuración denominada **acción de secuencia de comandos** que invoca scripts personalizados que personalizan el clúster de Hola. Estas secuencias de comandos son tooinstall usa componentes adicionales y cambiar la configuración. Las acciones de script pueden usarse durante la creación del clúster o después.

> [!IMPORTANT]
> acciones de script de Hola capacidad toouse en un clúster ya se está ejecutando solo está disponible para clústeres de HDInsight basados en Linux.
>
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Acciones de script también pueden ser publicado toohello Azure Marketplace como una aplicación de HDInsight. Algunos ejemplos de hello en este documento muestran cómo puede instalar una aplicación de HDInsight mediante comandos de acción de secuencia de comandos de PowerShell y Hola .NET SDK. Para obtener más información sobre las aplicaciones de HDInsight, vea [HDInsight publicar aplicaciones en Azure Marketplace hello](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Permisos

Si está usando un clúster de HDInsight Unidos a un dominio, hay dos permisos Ambari que son necesarios para usar acciones de script con el clúster de hello:

* **AMBARI. EJECUTAR\_personalizado\_comando**: rol de administrador de Ambari de hello tiene este permiso de forma predeterminada.
* **CLÚSTER. EJECUTAR\_personalizado\_comando**: tanto el Administrador de clústeres de HDInsight de Hola y Ambari Administrador tienen este permiso de forma predeterminada.

Para más información sobre cómo trabajar con permisos con clústeres de HDInsight unidos a un dominio, consulte [Administrar clústeres de HDInsight unidos a un dominio](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Control de acceso

Si no estás Hola administrador o propietario de la suscripción de Azure, la cuenta debe tener al menos **colaborador** grupo de recursos de toohello de acceso que contiene el clúster de HDInsight Hola.

Además, si está creando un clúster de HDInsight, alguien que tenga al menos **colaborador** acceso toohello suscripción de Azure debe haber registrado previamente proveedor Hola para HDInsight. Registro del proveedor se produce cuando un usuario con la suscripción de colaborador acceso toohello crea un recurso de hello primera vez en la suscripción de Hola. También puede realizarse sin crear ningún recurso mediante el [registro de un proveedor con REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Para obtener más información sobre cómo trabajar con la administración de acceso, vea Hola siguientes documentos:

* [Empezar a trabajar con la administración de acceso de hello portal de Azure](../active-directory/role-based-access-control-what-is.md)
* [Usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Descripción de las acciones de script

Una acción de script es simplemente un script de Bash al que proporciona un URI y para el que proporciona parámetros. Hola script se ejecuta en nodos de clúster de HDInsight Hola. Hola continuación se indican las características y las características de las acciones de script.

* Se debe almacenar en un URI que sea accesible desde el clúster de HDInsight Hola. siguiente Hola es ubicaciones de almacenamiento posibles:

    * Un **almacén de Azure Data Lake** cuenta que sea accesible para el clúster de HDInsight Hola. Para más información sobre el uso de Azure Data Lake Store con HDInsight, consulte [Creación de un clúster de HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Cuando se usa un script almacenado en el almacén de Data Lake, el formato del URI de hello es `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hola servicio principal HDInsight utiliza tooaccess almacén de Data Lake debe tener acceso de lectura toohello script.

    * Un blob en un **cuenta de almacenamiento de Azure** que es cualquier cuenta de almacenamiento principal o adicional de hello para el clúster de HDInsight de Hola. HDInsight se concede acceso tooboth de estos tipos de cuentas de almacenamiento durante la creación del clúster.

    * Un servicio público de uso compartido de archivos, como Azure Blob, GitHub, OneDrive, Dropbox, etc.

        Por ejemplo, URI, consulte hello [secuencias de comandos de acción de secuencia de comandos de ejemplo](#example-script-action-scripts) sección.

        > [!WARNING]
        > HDInsight solo admite cuentas de Azure Storage de __uso general__. No es compatible actualmente con hello __almacenamiento de blobs__ tipo de cuenta.

* Pueden estar restringidas demasiado**ejecutar en solo determinados tipos de nodos**, por nodos principales del ejemplo o nodos de trabajador.

  > [!NOTE]
  > Cuando se usa con HDInsight Premium, puede especificar que se debe usar el script de hello en el nodo del borde de Hola.

* Puede ser **persistente** o **ad hoc**.

    **Conserva** scripts son tooworker aplicada con nodos toohello agregado clústeres después de ejecutar script de Hola. Por ejemplo, cuando se escala ascendentemente clúster Hola.

    Un script persistente también podría aplicar el tipo de nodo tooanother cambios, por ejemplo, un nodo principal.

  > [!IMPORTANT]
  > Las acciones de scripts persistentes deben tener un nombre único.

    Los scripts **ad hoc** no son persistentes. No son clúster toohello agregado de tooworker aplicado nodos después de que se ejecutó el script de Hola. Posteriormente puede promover una secuencia de comandos ad hoc tooa conservarse script, o puede disminuir el nivel de una secuencia de comandos de script persistentes tooan ad hoc.

  > [!IMPORTANT]
  > Las acciones de script usadas durante la creación de un clúster se guardan automáticamente.
  >
  > Los scripts que dan error no se guardan, aunque indique específicamente que lo hagan.

* Puede aceptar **parámetros** que se usan para script de Hola durante la ejecución.
* Ejecutar con **privilegios en el nivel de raíz** en nodos de clúster de Hola.
* Puede utilizar a través de hello **portal de Azure**, **Azure PowerShell**, **CLI de Azure**, o **HDInsight .NET SDK**

clúster de Hello mantiene un historial de todos los scripts que se ha ejecutado. historial de Hello es útil cuando necesita Id. de hello toofind de una secuencia de comandos para las operaciones de promoción o degradación.

> [!IMPORTANT]
> No hay ningún tooundo de manera automática Hola cambios realizados por una acción de secuencia de comandos. O bien manualmente revertir cambios de Hola o proporcionar un script que se invierte.


### <a name="script-action-in-hello-cluster-creation-process"></a>Acción de secuencia de comandos en el proceso de creación de clúster de Hola

Las acciones de script usadas durante la creación de un clúster son algo diferentes de las ejecutadas en un clúster existente:

* script de Hola es **automáticamente persistente**.
* A **error** en hello script puede provocar toofail de proceso de creación de clúster de Hola.

Hello siguiente diagrama se muestra cuando se ejecuta la acción de secuencia de comandos durante el proceso de creación de hello:

![Fases y personalización de clústeres de HDInsight durante la creación de clústeres][img-hdi-cluster-states]

script de Hola se ejecuta mientras se está configurando HDInsight. En esta fase, Hola script se ejecuta en paralelo en todos los Hola nodos especificados en el clúster de Hola y se ejecuta con privilegios de raíz en los nodos de Hola.

> [!NOTE]
> Como script de Hola se ejecuta con privilegios de nivel de raíz en nodos de clúster de hello, puede realizar operaciones, como detener e iniciar servicios, incluidos los servicios relacionados con Hadoop. Si se detiene servicios, debe asegurarse de que servicio de Ambari de Hola y otros servicios relacionados con Hadoop están activados y ejecutándose antes de que finaliza la ejecución de script de Hola. Estos servicios son necesarios toosuccessfully determinar Hola mantenimiento y el estado del clúster de hello mientras se está creando.


Durante la creación del clúster, puede usar varias acciones de script a la vez. Estas secuencias de comandos se invocan en orden de hello en el que se especificaron.

> [!IMPORTANT]
> Las acciones de script se tienen que completar dentro de un periodo de 60 minutos o se superará el tiempo de espera. Durante el aprovisionamiento de clústeres, el script de Hola se ejecuta simultáneamente con otros procesos de instalación y configuración. La competición por los recursos, como el ancho de banda de red o de tiempo de CPU puede provocar Hola script tootake más toofinish que lo hace en el entorno de desarrollo.
>
> Hola toominimize tiempo toma toorun Hola script, evitar las tareas como la descarga y la compilación de aplicaciones de origen. Precompilar las aplicaciones y almacenar binario de hello en el almacenamiento de Azure.


### <a name="script-action-on-a-running-cluster"></a>Acción de script en un clúster en ejecución

A diferencia de la secuencia de comandos de acciones que se usan durante la creación del clúster, un error en una secuencia de comandos se ejecutaban en un clúster ya se está ejecutando no provoca automáticamente Hola clúster toochange tooa error de estado. Una vez completada una secuencia de comandos, el clúster de hello debe devolver tooa "estado" en ejecución.

> [!IMPORTANT]
> Aunque el clúster de hello tiene un estado "running", hello errores de secuencia de comandos puede han interrumpido cosas. Por ejemplo, una secuencia de comandos podría eliminar archivos necesarios para el clúster de Hola.
>
> Acciones de secuencias de comandos se ejecutan con privilegios de raíz, por lo que debe asegurarse de que comprende lo que hace una secuencia de comandos antes de aplicarla tooyour clúster.

Al aplicar un clúster de secuencia de comandos tooa, estado del clúster Hola cambia toofrom **ejecutando** demasiado**aceptado**, a continuación, **configuración de HDInsight**y finalmente, se vuelven demasiado**Ejecuta** para las secuencias de comandos correcta. estado del script de Hola se registra en el historial de acciones de script de Hola y puede usar esta información toodetermine si el script de Hola se realizó correctamente o no se pudo. Por ejemplo, hello `Get-AzureRmHDInsightScriptActionHistory` cmdlet de PowerShell puede ser utilizados tooview Hola estado de una secuencia de comandos. Devuelve información toohello similar siguiente texto:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Si ha cambiado la contraseña de usuario (admin) de clúster de Hola después de que se ha creado el clúster de hello, puede producir un error en la secuencia de comandos de acciones que se ejecutaron en este clúster. Si tiene las acciones de script persistentes que nodos de trabajo de destino, estos scripts producirán errores al escalar el clúster de Hola.

## <a name="example-script-action-scripts"></a>Ejemplo de scripts de acción de script

Pueden utilizar secuencias de comandos de acción de secuencia de comandos mediante Hola siguientes utilidades:

* Azure Portal
* Azure PowerShell
* Azure CLI
* SDK .NET de HDInsight

HDInsight proporciona hello tooinstall de secuencias de comandos de los componentes siguientes en clústeres de HDInsight:

| Nombre | Script |
| --- | --- |
| **Agregar una cuenta de Azure Storage** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Vea [clúster de HDInsight de agregar almacenamiento adicional tooan](hdinsight-hadoop-add-storage.md). |
| **Instalación de Hue** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Consulte [Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md) |
| **Instalar Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Vea [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md) (Instalación y uso de Presto en clústeres de HDInsight). |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md). |
| **Instalación de Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md). |
| **Carga previa de las bibliotecas de Hive** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Vea [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md) (Adición de bibliotecas de Hive en clústeres de HDInsight). |
| **Instalación o actualización de Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. Vea [Instalación o actualización de Mono en HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Uso de una acción de script durante la creación de un clúster

En esta sección se proporciona ejemplos en hello distintas formas que puede usar acciones de script al crear un clúster de HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Usar una acción de secuencia de comandos durante la creación del clúster de hello portal de Azure

1. Comience a crear un clúster, tal y como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Deténgase cuando llegue a hello __resumen de clúster__ sección.

2. De hello __resumen de clúster__ sección, seleccione hello __editar__ de vínculos para __configuración avanzada__.

    ![Vínculo Configuración avanzada](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. De hello __configuración avanzada__ sección, seleccione __acciones de Script__. De hello __acciones de Script__ sección, seleccione __+ nuevo envío__

    ![Enviar una nueva acción de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Hola de uso __seleccione una secuencia de comandos__ tooselect de entrada una secuencia de comandos elaborado previamente. toouse una secuencia de comandos personalizada, seleccione __personalizado__ y, a continuación, proporcionar hello __nombre__ y __Bash URI del script__ para la secuencia de comandos.

    ![Agregar un script de Hola select en forma de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello en la tabla siguiente describe los elementos de hello en forma de hello:

    | Propiedad | Valor |
    | --- | --- |
    | Seleccione un script | toouse sus propias secuencias de comandos, seleccione __personalizado__. En caso contrario, seleccione una de las secuencias de comandos de hello proporcionado. |
    | Nombre |Especifique un nombre para la acción de secuencia de comandos de Hola. |
    | URI de script de Bash |Especifique Hola URI toohello script que es invocado toocustomize Hola clúster. |
    | Principal, Trabajo o Zookeeper |Especifique los nodos de hello (**Head**, **trabajo**, o **ZooKeeper**) en qué personalización Hola se ejecuta el script. |
    | parameters |Especificar parámetros de hello, si así lo requiere el script de Hola. |

    Hola de uso __conservar esta acción de secuencia de comandos__ tooensure de entrada que hello secuencia de comandos se aplica durante las operaciones de ajuste de escala.

5. Seleccione __crear__ secuencia de comandos de toosave Hola. A continuación, puede usar __+ Enviar nueva__ tooadd otra secuencia de comandos.

    ![Varias acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Cuando haya terminado de agregar secuencias de comandos, utilice hello __seleccione__ botón y, a continuación, Hola __siguiente__ botón tooreturn toohello __resumen de clúster__ sección.

3. clúster de hello toocreate, seleccione __crear__ de hello __resumen de clúster__ selección.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Use una acción de script de las plantillas de Azure Resource Manager

ejemplos de Hello en esta sección muestra cómo toouse script acciones con plantillas del Administrador de recursos de Azure.

#### <a name="before-you-begin"></a>Antes de empezar

* Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight Powershell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).
* Para obtener instrucciones sobre cómo toocreate plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md).
* Si todavía no ha utilizado Azure PowerShell con el Administrador de recursos, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../azure-resource-manager/powershell-azure-resource-manager.md)

#### <a name="create-clusters-using-script-action"></a>Creación de clústeres mediante acciones de script

1. Copie Hola después de ubicación de tooa la plantilla en el equipo. Esta plantilla instala Giraph en nodos headnodes y de trabajo Hola Hola clúster. También puede comprobar si la plantilla JSON de hello es válida. Pegue el contenido de la plantilla en [JSONLint](http://jsonlint.com/), herramienta de validación JSON en línea.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Inicie PowerShell de Azure e inicie sesión tooyour cuenta de Azure. Después de proporcionar sus credenciales, comando hello devuelve información sobre su cuenta.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Si tiene varias suscripciones, proporcione el identificador de suscripción de hello desea toouse para la implementación.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Puede usar `Get-AzureRmSubscription` tooget una lista de todas las suscripciones asociadas con su cuenta, que incluye el Id. de suscripción de Hola para cada uno de ellos.

4. Si no tiene un grupo de recursos existente, puede crear uno. Proporcione el nombre de hello del grupo de recursos de Hola y la ubicación que necesite para su solución. Se devuelve un resumen del nuevo grupo de recursos Hola.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. una implementación para el grupo de recursos, ejecute hello toocreate **AzureRmResourceGroupDeployment New** comando y especifique los parámetros necesarios de Hola. parámetros de Hello incluyen hello datos siguientes:

    * Un nombre para la implementación
    * nombre de Hola de su grupo de recursos
    * ruta de acceso de Hola o plantilla de toohello de dirección URL que ha creado.

  Si la plantilla requiere parámetros, tiene que pasar también esos parámetros. En este caso, hello tooinstall de acción de script R en clúster de hello no requiere ningún parámetro.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Son valores tooprovide solicitadas para los parámetros de hello definidos en la plantilla de Hola.

1. Cuando se ha implementado el grupo de recursos de hello, se muestra un resumen de implementación de Hola.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Si se produce un error en la implementación, puede usar Hola siguiente cmdlets tooget información acerca de los errores de Hola.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Uso de una acción de script durante la creación de un clúster desde Azure PowerShell

En esta sección, se utiliza hello [AzureRmHDInsightScriptAction agregar](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts mediante el uso de la acción de secuencia de comandos toocustomize un clúster. Antes de continuar, asegúrese de que ha instalado y configurado Azure PowerShell. Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight PowerShell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).

Hello secuencia de comandos siguiente se muestra cómo tooapply una acción de secuencia de comandos al crear un clúster con PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Puede tardar varios minutos antes de que se crea un clúster Hola.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Usar una acción de secuencia de comandos durante la creación del clúster de HDInsight .NET SDK Hola

Hola HDInsight .NET SDK proporciona bibliotecas de cliente que resulta más fácil toowork con HDInsight desde una aplicación. NET. Para obtener un ejemplo de código, vea [basados en Linux crear clústeres de HDInsight utilizando Hola .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster

En esta sección, obtenga información acerca de cómo tooapply script tooa de acciones que se ejecuta el clúster.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello portal de Azure

1. De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.

2. En información general del clúster de HDInsight de hello, seleccione hello **acciones de Script** icono.

    ![Icono Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > También puede seleccionar **toda la configuración de** y, a continuación, seleccione **acciones de Script** de hello sección de configuración.

3. Desde la parte superior de la sección de acciones de Script de Hola Hola seleccione **Enviar nueva**.

    ![Agregar un tooa de secuencia de comandos ejecutando el clúster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Hola de uso __seleccione una secuencia de comandos__ tooselect de entrada una secuencia de comandos elaborado previamente. toouse una secuencia de comandos personalizada, seleccione __personalizado__ y, a continuación, proporcionar hello __nombre__ y __Bash URI del script__ para la secuencia de comandos.

    ![Agregar un script de Hola select en forma de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello en la tabla siguiente describe los elementos de hello en forma de hello:

    | Propiedad | Valor |
    | --- | --- |
    | Seleccione un script | toouse sus propias secuencias de comandos, seleccione __personalizado__. En caso contrario, seleccione uno de los que se proporcionan. |
    | Nombre |Especifique un nombre para la acción de secuencia de comandos de Hola. |
    | URI de script de Bash |Especifique Hola URI toohello script que es invocado toocustomize Hola clúster. |
    | Principal, Trabajo o Zookeeper |Especifique los nodos de hello (**Head**, **trabajo**, o **ZooKeeper**) en qué personalización Hola se ejecuta el script. |
    | parameters |Especificar parámetros de hello, si así lo requiere el script de Hola. |

    Hola de uso __conservar esta acción de secuencia de comandos__ secuencia de comandos de entrada toomake seguro Hola se aplica durante las operaciones de ajuste de escala.

5. Por último, utilice hello **crear** clúster toohello de botón tooapply hello secuencia de comandos.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster en PowerShell de Azure

Antes de continuar, asegúrese de que ha instalado y configurado Azure PowerShell. Para obtener información acerca de cómo configurar un toorun de estación de trabajo HDInsight PowerShell cmdlets, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).

Hello ejemplo siguiente se muestra cómo tooapply un clúster de ejecución de tooa de acción de secuencia de comandos:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Una vez completada la operación de hello, recibirá información toohello similar siguiente texto:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello CLI de Azure

Antes de continuar, asegúrese de que ha instalado y configurado Hola CLI de Azure. Para obtener más información, consulte [Install hello Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure el modo de administrador de recursos, utilice Hola siguiente comando en la línea de comandos de hello:

        azure config mode arm

2. Usar hello después tooauthenticate tooyour suscripción de Azure.

        azure login

3. Usar hello después comando tooapply un tooa de acción de secuencia de comandos ejecutando el clúster

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Si omite los parámetros de este comando, se le solicitan. Si Hola script especifica con `-u` acepta parámetros, puede especificar mediante hello `-p` parámetro.

    Los tipos de nodo válidos son `headnode`, `workernode` y `zookeeper`. Si el script de Hola debe estar toomultiple aplicado los tipos de nodo, especificar tipos de hello separados por un ';'. Por ejemplo: `-n headnode;workernode`.

    toopersist Hola script, agregue hello `--persistOnSuccess`. También puede conservar el script de Hola más adelante mediante el uso de `azure hdinsight script-action persisted set`.

    Cuando se completa el trabajo de hello, recibirá toohello similar de salida siguiente texto:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster que usa la API de REST

Consulte [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx)(Ejecución de acciones de script en un clúster en ejecución).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Aplicar un tooa de acción de secuencia de comandos ejecutando el clúster de hello HDInsight .NET SDK

Para obtener un ejemplo del uso de clústeres de tooa de hello .NET SDK tooapply secuencias de comandos, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Visualización del historial, promover y disminuir de nivel acciones de script

### <a name="using-hello-azure-portal"></a>Uso de hello portal de Azure

1. De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.

2. En información general del clúster de HDInsight de hello, seleccione hello **acciones de Script** icono.

    ![Icono Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > También puede seleccionar **toda la configuración de** y, a continuación, seleccione **acciones de Script** de hello sección de configuración.

4. Un historial de las secuencias de comandos para este clúster se muestra en la sección de acciones de Script de Hola. Esta información incluye una lista de scripts persistentes. En la captura de pantalla de hello siguiente, puede ver que hello Solr ha sido script se ejecutó en este clúster. captura de pantalla de Hello no muestra las secuencias de comandos persistentes.

    ![Sección Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Seleccionar una secuencia de comandos del historial de hello muestra la sección de propiedades de Hola para esta secuencia de comandos. Desde la parte superior de la pantalla de bienvenida Hola puede volver a ejecutar el script de Hola o promoverlo.

    ![Propiedades de Acciones de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. También puede usar hello **...**  toohello derecha de las entradas en las acciones tooperform de sección de acciones de Script de Hola.

    ![Acciones de script... uso](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Uso de Azure PowerShell

| Utilice la siguiente de Hola... | demasiado... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Recuperar información sobre acciones de script persistentes |
| Get-AzureRmHDInsightScriptActionHistory |Recuperar un historial de clústeres de secuencia de comandos acciones aplicadas toohello, o los detalles de una secuencia de comandos específica |
| Set-AzureRmHDInsightPersistedScriptAction |Promociona ad hoc tooa de acción de secuencia de comandos conserva la acción de secuencia de comandos |
| Remove-AzureRmHDInsightPersistedScriptAction |Degrada una acción de script persistentes acción tooan ad hoc |

> [!IMPORTANT]
> Usar `Remove-AzureRmHDInsightPersistedScriptAction` deshacer las acciones de hello realizadas por una secuencia de comandos. Este cmdlet quita solo marca persistente Hola.

Hola siguiente secuencia de comandos de ejemplo muestra cómo utilizar Hola cmdlets toopromote, a continuación, disminuir de nivel de una secuencia de comandos.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Uso de hello CLI de Azure

| Utilice la siguiente de Hola... | demasiado... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Recuperar una lista de las acciones de script persistentes |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Recuperar información sobre una acción de script persistente específica |
| `azure hdinsight script-action history list <clustername>` |Recuperar un historial de clústeres de secuencia de comandos acciones aplicadas toohello |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Recuperar información sobre una acción de script específica |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Promociona ad hoc tooa de acción de secuencia de comandos conserva la acción de secuencia de comandos |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Degrada una acción de script persistentes acción tooan ad hoc |

> [!IMPORTANT]
> Usar `azure hdinsight script-action persisted delete` deshacer las acciones de hello realizadas por una secuencia de comandos. Este cmdlet quita solo marca persistente Hola.

### <a name="using-hello-hdinsight-net-sdk"></a>Uso de hello HDInsight .NET SDK

Para obtener un ejemplo del uso de historial de script de Hola .NET SDK tooretrieve desde un clúster, promocionar o degradar las secuencias de comandos, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> En este ejemplo también muestra cómo tooinstall una aplicación de HDInsight con Hola .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Soporte técnico para el software de código abierto utilizado en clústeres de HDInsight

Hola servicio HDInsight de Azure de Microsoft usa un ecosistema de tecnologías de código abierto formado alrededor de Hadoop. Microsoft Azure proporciona un nivel general de soporte técnico para las tecnologías de código abierto. Para obtener más información, vea hello **compatibilidad con ámbito** sección de hello [sitio Web de preguntas más frecuentes de soporte técnico de Azure](https://azure.microsoft.com/support/faq/). Hola servicio HDInsight proporciona un nivel adicional de compatibilidad para componentes integrados.

Hay dos tipos de componentes de código abierto que están disponibles en hello servicio HDInsight:

* **Componentes integrados** -estos componentes se instalan previamente en clústeres de HDInsight y proporcionan la funcionalidad básica de clúster de Hola. Por ejemplo, ResourceManager hilo, lenguaje de consulta de Hive hello (HiveQL) y biblioteca de Mahout Hola pertenecen toothis categoría. Una lista completa de componentes del clúster está disponible en [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight](hdinsight-component-versioning.md).
* **Componentes personalizados** -, como un usuario del clúster hello, puede instalar o usar en la carga de trabajo cualquier componente disponible en la Comunidad de Hola o creado por el usuario.

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles. Microsoft Support le ayuda a tooisolate y resolver los problemas relacionados toothese componentes.
>
> Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Soporte técnico de Microsoft puede ser capaz de tooresolve problema de Hola o pueden pedirle que tooengage los canales disponibles para las tecnologías de código abierto de Hola donde se encuentra la amplia experiencia para que la tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).

Hola servicio HDInsight proporciona varias maneras de componentes personalizados de toouse. Hola al mismo nivel de compatibilidad se aplica, sin tener en cuenta cómo un componente se utiliza o instalado en el clúster de Hola. Hello lista siguiente describen los usos más comunes de Hola que se puedan usar componentes personalizados en clústeres de HDInsight:

1. Envío de trabajos - Hadoop u otros tipos de trabajos que se ejecutan o utilizan componentes personalizados pueden clúster toohello enviado.

2. Personalización de clúster - durante la creación del clúster, puede especificar opciones de configuración adicionales y componentes personalizados que están instalados en nodos de clúster de Hola.

3. Ejemplos: para componentes personalizados populares, Microsoft y otros elementos pueden proporcionar ejemplos de cómo se pueden usar estos componentes en clústeres de HDInsight Hola. Estas muestras se proporcionan sin soporte técnico.

## <a name="troubleshooting"></a>Solución de problemas

Puede usar Ambari web UI tooview información registrada por acciones de script. Si se produce un error en el script de Hola durante la creación del clúster, también están disponibles en hello cuenta de almacenamiento predeterminado asociado con el clúster de Hola Hola registros. En esta sección se proporciona información sobre cómo tooretrieve Hola registros con ambas opciones.

### <a name="using-hello-ambari-web-ui"></a>Uso de hello Ambari Web UI

1. En el explorador, navegue toohttps://CLUSTERNAME.azurehdinsight.net. Reemplace CLUSTERNAME por nombre de Hola de su clúster de HDInsight.

    Cuando se le solicite, escriba nombre de cuenta de administrador de hello (admin) y la contraseña para el clúster de Hola. Puede que tenga credenciales de administrador de hello tooreenter en un formulario web Forms.

2. En barra de hello al principio de Hola de página de hello, seleccione hello **ops** entrada. Se muestra una lista de las operaciones actuales y anteriores realizadas en clúster de Hola a través de Ambari.

    ![Barra de interfaz de usuario web de Ambari con ops seleccionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Buscar entradas de Hola que tienen **ejecutar\_customscriptaction** en hello **Operations** columna. Estas entradas se crean al ejecutar las acciones de Script de Hola.

    ![Captura de pantalla de operaciones](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    Hola tooview STDOUT y resultado STDERR, seleccione hello run\customscriptaction entrada y explorar en profundidad los vínculos de Hola. Esta salida se genera cuando se ejecuta el script de Hola y pueden contener información útil.

### <a name="access-logs-from-hello-default-storage-account"></a>Registros de acceso de la cuenta de almacenamiento predeterminada de Hola

Si se produce un error en la creación del clúster Hola debido a error de acción de secuencia de comandos de tooa, Hola registros pueden tener acceso de cuenta de almacenamiento de clúster de Hola.

* Hello registros de almacenamiento están disponibles en `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Captura de pantalla de operaciones](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    En este directorio, registros de Hola se organizan por separado para el nodo principal, workernode y zookeeper nodos. A continuación, se indican algunos ejemplos:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Nodo de trabajo** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Nodo Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Todos los stdout y stderr de host correspondiente Hola está cargado toohello cuenta de almacenamiento. Hay un archivo **output-\*.txt** and **errors-\*.txt** para cada acción de script. archivo de salida *.txt Hello contiene información sobre Hola URI del script de Hola que obtuvo ejecutar en el host de Hola. Por ejemplo:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Es posible crear un clúster de acción de secuencia de comandos repetidamente con hello mismo nombre. En este caso, puede distinguir los registros pertinentes Hola basados en el nombre de la carpeta de hello fecha. Por ejemplo, estructura de carpetas de Hola para un clúster (mycluster) creado en diferentes fechas aparece toohello similar siguiendo las entradas del registro:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Si crea un clúster de acción de secuencia de comandos con hello mismo nombre en hello mismo día, puede usar archivos de registro correspondientes de hello prefijo único tooidentify Hola.

* Si crea un clúster cerca de 12:00 A.M. (medianoche), es posible que los archivos de registro de hello abarcan dos días. En tales casos, verá dos carpetas de otra fecha para hello mismo clúster.

* Contenedor de carga registro archivos toohello predeterminado puede tardar hasta too5 minuto (s), especialmente para grandes clústeres. Por lo tanto, si desea que los registros de hello tooaccess, no debe inmediatamente Eliminar clúster Hola si se produce un error en una acción de secuencia de comandos.

### <a name="ambari-watchdog"></a>Guardián Ambari

> [!WARNING]
> No se cambia la contraseña de Hola de hello Ambari guardián (hdinsightwatchdog) en el clúster de HDInsight basados en Linux. Cambiar la contraseña para esta cuenta de hello interrumpe acciones nuevo script de Hola capacidad toorun en clúster de HDInsight Hola.

### <a name="cant-import-name-blobservice"></a>No se puede importar el nombre BlobService

__Síntomas__: Hola error en la acción de secuencia de comandos. Texto toohello similar siguiente error se muestra cuando ve operación hello en Ambari:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Causa__: este error se produce si actualiza el cliente de almacenamiento de Azure de Python de Hola que se incluye con clúster de HDInsight Hola. HDInsight espera el cliente de Azure Storage 0.20.0.

__Resolución__: tooresolve este error, conecte manualmente el nodo de clúster de tooeach con `ssh` y use Hola siguiendo versión de cliente de almacenamiento correcta de comando tooreinstall hello:

```
sudo pip install azure-storage==0.20.0
```

Para obtener información sobre la conexión de toohello de clúster mediante SSH, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>El historial no muestra los scripts usados durante la creación del clúster

Si el clúster se creó antes del 15 de marzo de 2016, puede que no vea una entrada en el historial de acciones de script. Si cambia el tamaño de clúster de hello después del 15 de marzo de 2016, secuencias de comandos de hello mediante durante la creación del clúster aparecen en un historial cuando se aplican toonew nodos de clúster de hello como parte del programa Hola a cambiar el tamaño de operación.

Hay dos excepciones:

* Si el clúster se creó antes del 1 de septiembre de 2015. Esta es la fecha en que se presentaron las acciones de script. Cualquier clúster creado con anterioridad a esta fecha no ha podido usar acciones de script para su creación.

* Si usa varias acciones de Script durante la creación del clúster y lo usó Hola mismo nombre para varias secuencias de comandos, u Hola mismo nombre, mismo URI, pero distintos parámetros de varias secuencias de comandos. En estos casos, recibirá Hola siguiente error:

    Se ejecutó ningún script nuevo las acciones pueden ser en este clúster debido tooconflicting nombres de secuencia de comandos en secuencias de comandos existentes. Los nombres de script proporcionados en la creación del clúster deben ser únicos. Los scripts existentes se ejecutan con el cambio de tamaño.

## <a name="next-steps"></a>Pasos siguientes

* [Desarrollo de la acción de script con HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Agregar clúster de HDInsight de tooan de almacenamiento adicional](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fases durante la creación del clúster"
