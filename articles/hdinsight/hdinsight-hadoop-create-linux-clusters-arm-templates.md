---
title: "clústeres de Hadoop aaaCreate mediante plantillas - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate clústeres de HDInsight mediante plantillas de administrador de recursos"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Creación de clústeres de Hadoop en HDInsight con plantillas de Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

En este artículo, aprenderá varias formas de clústeres de toocreate HDInsight de Azure con plantillas del Administrador de recursos de Azure. Para obtener más información, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). toolearn acerca de otras herramientas de creación de clúster y características, haga clic en Tabulador de hello en la parte superior de Hola de esta página o vea [métodos de creación de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

instrucciones de hello toofollow en este artículo, necesitará:

* Una [suscripción de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell o CLI de Azure.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Plantillas de Resource Manager
Una plantilla de administrador de recursos facilita hello toocreate fácil después de la aplicación en una única operación coordinada:
* Clústeres de HDInsight y sus recursos dependientes (como cuenta de almacenamiento predeterminada de hello)
* Otros recursos (por ejemplo, toouse Sqoop Apache de base de datos de SQL Azure)

En la plantilla de hello, definir recursos de Hola que sean necesarios para la aplicación hello. También especificar tooinput valores de parámetros de implementación para diferentes entornos. plantilla de Hello consta de JSON y expresiones que usan valores de tooconstruct para su implementación.

Puede encontrar plantillas de HDInsight de ejemplo en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Usar multiplataforma [código de Visual Studio](https://code.visualstudio.com/#alt-downloads) con hello [extensión del Administrador de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o una plantilla de Hola de toosave de editor de texto en un archivo en la estación de trabajo. Obtenga información acerca cómo toocall Hola plantilla mediante diversos métodos.

Para obtener más información acerca de las plantillas de administrador de recursos, vea Hola siguientes artículos:

* [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Implementación de una aplicación con las plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Generación de plantillas

Mediante el uso de hello portal de Azure, puede configurar todas las propiedades de Hola de un clúster y, a continuación, Guardar plantilla Hola antes de implementarla. A continuación, puede volver a usar plantilla Hola.

**toogenerate una plantilla mediante Hola portal de Azure**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **New** en el menú de la izquierda hello, haga clic en **Intelligence + análisis**y, a continuación, haga clic en **HDInsight**.
3. Siguen Hola instrucciones tooenter propiedades. Puede usar cualquier hello **creación rápida** o hello **personalizado** opción.
4. En hello **resumen** , haga clic en **descargar la plantilla y los parámetros**:

    ![HDInsight Hadoop crear clúster descarga plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Ver una lista de archivo de plantilla de hello, archivo de parámetros y ejemplos que se utilizará toodeploy Hola plantilla:

    ![HDInsight Hadoop crear clúster opciones de descarga de plantilla de Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    Desde aquí, puede descargar la plantilla de hello, guardar biblioteca de plantillas de tooyour o implementar la plantilla de Hola.

    tooaccess una plantilla en la biblioteca, haga clic en **más servicios** del menú izquierdo de hello y, a continuación, haga clic en **plantillas** (en hello **otros** categoría).

    > [!Note]
    > archivo de plantilla y los parámetros de Hello se debe usar conjuntamente. De lo contrario, podría obtener resultados inesperados. Por ejemplo, Hola predeterminado **clusterKind** siempre es el valor de la propiedad **hadoop**, a pesar de lo que se especifique antes de descargar plantilla de Hola.



## <a name="deploy-with-powershell"></a>Implementación con PowerShell

Este procedimiento permite crear el clúster de Hadoop en HDInsight.

1. Guarde el archivo JSON de Hola Hola [apéndice](#appx-a-arm-template) tooyour estación de trabajo. Hola script de PowerShell, nombre de archivo de hello es `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Establecer parámetros de Hola y variables si es necesario.
3. Plantilla de ejecución hello mediante Hola siguiente script de PowerShell:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Hola script de PowerShell configura sólo el nombre de clúster Hola. nombre de cuenta de almacenamiento de Hello está codificado de forma rígida en la plantilla de Hola. Son la contraseña de usuario de clúster de hello tooenter solicitadas. (nombre de usuario de hello predeterminada es **administración**.) También son contraseña de usuario SSH de hello tooenter solicitadas. (nombre de usuario SSH de hello predeterminada es **sshuser**.)  

Para obtener más información, consulte [Implementación con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Implementación con la CLI
Hola según muestra usa la interfaz de línea de comandos (CLI) de Azure. En él, se crea un clúster y su contenedor y cuenta de almacenamiento dependientes mediante una llamada a una plantilla de Resource Manager:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

Son tooenter solicitada:
* nombre del clúster Hola.
* contraseña de usuario del clúster de Hola. (nombre de usuario de hello predeterminada es **administración**.)
* contraseña de usuario SSH de Hola. (nombre de usuario SSH de hello predeterminada es **sshuser**.)

Hola siguiente código proporciona los parámetros de en línea:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Implementar con hello API de REST
Vea [implementar con la API de REST de hello](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Implementación con Visual Studio
 Usar Visual Studio toocreate un proyecto del grupo de recursos e impleméntela tooAzure a través de la interfaz de usuario de Hola. Seleccionar tipo de Hola de tooinclude de recursos en el proyecto. Estos recursos se agregan automáticamente toohello plantilla de administrador de recursos. proyecto de Hello también proporciona una plantilla de Hola de toodeploy de script de PowerShell.

Para una introducción toousing Visual Studio con grupos de recursos, consulte [crear e implementar grupos de recursos de Azure a través de Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido varias formas toocreate un clúster de HDInsight. toolearn más información, vea Hola siguientes artículos:

* Para obtener un ejemplo de la implementación de los recursos a través de la biblioteca de cliente de .NET de hello, consulte [implementar los recursos mediante el uso de bibliotecas de .NET y una plantilla de](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para ver un ejemplo en profundidad de la implementación de una aplicación, consulte [Aprovisionamiento e implementación predecibles de microservicios en Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Para obtener instrucciones sobre la implementación de los entornos de toodifferent de solución, vea [entornos de desarrollo y prueba en Microsoft Azure](../solution-dev-test-environments.md).
* toolearn acerca de las secciones de Hola de plantilla de hello Azure Resource Manager, consulte [crear plantillas](../azure-resource-manager/resource-group-authoring-templates.md).
* Para obtener una lista de funciones de Hola pueden usar en una plantilla de Azure Resource Manager, consulte [funciones de plantilla](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Apéndice: El Administrador de recursos plantilla toocreate un clúster de Hadoop
Hello siguiente plantilla de Azure Resource Manager crea un clúster de Hadoop basados en Linux con cuenta de almacenamiento de Azure dependientes de Hola.

> [!NOTE]
> El ejemplo incluye información de configuración de la tienda de Hive y Oozie Metastore. Quitar sección Hola o configurar sección Hola antes de usar la plantilla de Hola.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Apéndice: El Administrador de recursos plantilla toocreate un clúster Spark

Esta sección proporciona una plantilla de administrador de recursos que puede usar un clúster de HDInsight Spark toocreate. Esta plantilla incluye configuraciones para `spark-defaults` y `spark-thrift-sparkconf` (para clústeres de Spark 1.6) y `spark2-defaults` y `spark2-thrift-sparkconf` (para clústeres de Spark 2). Además la toothis, HDInsight calcula y establece las configuraciones como `spark.executor.instances`, `spark.executor.memory`, y `spark.executor.cores` según el tamaño del clúster Hola. 

Si establece un parámetro en una sección como parte de la propia plantilla hello, HDInsight no calcular y establecer Hola otros parámetros de hello misma sección. Por ejemplo, el parámetro `spark.executor.instances` en hello `spark-defaults` configuración. Si se establece otro parámetro (por ejemplo, `spark.yarn.exector.memoryOverhead`) en hello `spark-defaults` configuración, HDInsight no calcular y establecer hello `spark.executor.instances` parámetro también.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
