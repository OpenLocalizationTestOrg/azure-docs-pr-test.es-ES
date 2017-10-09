---
title: "aaaUse 2.0 de línea de comandos de Azure interfaz tooget a trabajar con el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar línea de comandos multiplataforma Azure 2.0 toocreate una cuenta de almacén de Data Lake y realizar operaciones básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Introducción a Azure Data Lake Store mediante la CLI de Azure 2.0
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Obtenga información acerca de cómo toouse CLI de Azure 2.0 toocreate un Azure Data Lake almacenar cuenta y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).

Hola 2.0 de CLI de Azure es la nueva experiencia de línea de comandos de Azure para administrar recursos de Azure. Se puede usar en macOS, Linux y Windows. Para más información, consulte la [introducción a la CLI 2.0 de Azure](https://docs.microsoft.com/cli/azure/overview). También puede mirar hello [referencia de Azure Data Lake almacén CLI 2.0](https://docs.microsoft.com/cli/azure/dls) para obtener una lista completa de comandos y la sintaxis.


## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

* **CLI 2.0 de Azure**: consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalación de la CLI 2.0 de Azure) para obtener instrucciones.

## <a name="authentication"></a>Autenticación

En este artículo se utiliza un enfoque de autenticación más sencillo con Data Lake Store, donde inicia sesión como usuario final. Hola acceso nivel tooData Lake almacén cuenta de sistema de archivos y, a continuación, se rige por el nivel de acceso de Hola de hello usuario registrado. Sin embargo, hay otros métodos como tooauthenticate bien con el almacén de Data Lake, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Inicie sesión en tooyour suscripción de Azure

1. Inicie sesión en su suscripción de Azure.

    ```azurecli
    az login
    ```

    Obtener un toouse de código en el paso siguiente de saludo. Use un https://aka.ms/devicelogin web explorador tooopen Hola página e introduzca hello código tooauthenticate. Son toolog solicitada en con sus credenciales.

2. Una vez que inicie sesión en todas las listas de ventanas de Hola Hola suscripciones de Azure que están asociadas a su cuenta. Usar hello después comando toouse una suscripción específica.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Creación de una cuenta de Almacén de Azure Data Lake

1. Cree un nuevo grupo de recursos. En el siguiente comando de hello, proporcionar Hola valores de parámetro que desee toouse. Si el nombre de la ubicación de hello contiene espacios en blanco, poner entre comillas. Por ejemplo "East US 2". 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Crear cuenta de almacén de Data Lake Hola.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Crear carpetas en una cuenta de Almacén de Data Lake

Puede crear carpetas en su toomanage de cuenta de almacén de Azure Data Lake y almacenar datos. Hola de uso después de toocreate comando llama a una carpeta **MiNuevaCarpeta** en raíz Hola Hola almacén de Data Lake.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Hola `--folder` parámetro garantiza que el comando de hello crea una carpeta. Si este parámetro no está presente, el comando de hello crea un archivo vacío denominado MiNuevaCarpeta en raíz Hola Hola cuenta de almacén de Data Lake.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Cargar la cuenta de almacén de Data Lake tooa de datos

Puede cargar el almacén de datos tooData Lake directamente en hello tooa o nivel de carpeta raíz que ha creado en la cuenta de hello. Hola fragmentos siguientes muestran cómo tooupload alguna carpeta de toohello de datos de ejemplo (**MiNuevaCarpeta**) que creó en la sección anterior de Hola.

Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Descargar archivo hello y almacenarlo en un directorio local en el equipo, como C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Para el destino de hello, debe especificar ruta completa de hello incluido el nombre de archivo de Hola.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Enumeración de archivos en una cuenta de Data Lake Store

Usar hello siguientes comando toolist Hola archivos en una cuenta de almacén de Data Lake.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

salida de Hello de este debe ser similar siguiente toohello:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Cambio del nombre, descarga y eliminación de datos en Data Lake Store 

* **toorename un archivo**, usar hello siguiente comando:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **toodownload un archivo**, utilizar el siguiente comando de Hola. Asegúrese de que la ruta de acceso de destino de hello especificada ya existe.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > comando de Hello crea la carpeta de destino de hello si no existe.
    > 
    >

* **toodelete un archivo**, usar hello siguiente comando:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Si desea que la carpeta de hello toodelete **MiNuevaCarpeta** y archivo hello **vehicle1_09142014_copy.csv** juntos en un solo comando, use Hola--recurse parámetro

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Uso de permisos y listas ACL para una cuenta de Data Lake Store

En esta sección aprenderá cómo toomanage ACL y permisos mediante la CLI de Azure 2.0. Para obtener una explicación detallada sobre cómo se implementan las listas ACL de Azure Data Lake Store, consulte [Control de acceso en Azure Data Lake Store](data-lake-store-access-control.md).

* **propietario de hello tooupdate de una archivo o carpeta**, usar hello siguiente comando:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **permisos de hello tooupdate para un archivo o carpeta**, usar hello siguiente comando:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **Hola tooget ACL para una ruta de acceso dada**, usar hello siguiente comando:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    salida de Hello debe ser similar siguiente toohello:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset una entrada para una ACL**, usar hello siguiente comando:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove una entrada para una ACL**, usar hello siguiente comando:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **tooremove una ACL predeterminada todo**, usar hello siguiente comando:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **tooremove una ACL no predeterminado toda**, usar hello siguiente comando:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Eliminar una cuenta del Almacén de Data Lake
Usar hello después comando toodelete una cuenta de almacén de Data Lake.

```azurecli
az dls account delete --account mydatalakestore
```

Cuando se le solicite, escriba **Y** cuenta de hello toodelete.

## <a name="next-steps"></a>Pasos siguientes

* [Referencia de la CLI 2.0 de Azure Data Lake Store](https://docs.microsoft.com/cli/azure/dls)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
