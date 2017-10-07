---
title: "aaaGet a trabajar con análisis de Data Lake de Azure mediante Azure CLI 2.0 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo crear un trabajo de análisis de Data Lake mediante SQL U toouse Hola 2.0 de la interfaz de línea de comandos de Azure toocreate una cuenta de análisis de Data Lake y enviar el trabajo de Hola. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Introducción al uso de la CLI de Azure 2.0 por parte de Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

En este tutorial, se desarrolla un trabajo que lee un archivo de valores separados por tabulaciones (TSV) y lo convierte en un otro de valores separados por comas (CSV). toogo a través de hello mismo tutorial usar otros admite las herramientas, lista de desplegable Hola de uso en la parte superior de Hola de esta sección.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguientes elementos:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **CLI de Azure 2.0**. Consulte [Instalación y configuración de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

toolog en tooyour suscripción de Azure:

```
azurecli
az login
```

Están solicitada toobrowse tooa una dirección URL y escriba un código de autenticación.  Y, a continuación, siga Hola instrucciones tooenter sus credenciales.

Una vez que haya iniciado sesión, comando de inicio de sesión de hello muestra las suscripciones.

toouse una suscripción específica:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Creación de una cuenta de Análisis de Data Lake
Para poder ejecutar cualquier trabajo es preciso tener una cuenta de Data Lake Analytics. una cuenta de análisis de Data Lake toocreate, debe especificar Hola siguientes elementos:

* **Grupo de recursos de Azure**. Se debe crear una cuenta de Data Lake Analytics en un grupo de recursos de Azure. [El Administrador de recursos Azure](../azure-resource-manager/resource-group-overview.md) permite toowork con recursos de hello en la aplicación como un grupo. Puede implementar, actualizar o eliminar todos los recursos de Hola para su aplicación en una única operación coordinada.  

toolist Hola existente grupos de recursos bajo su suscripción:

```
az group list
```

toocreate un nuevo grupo de recursos:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nombre de la cuenta de Data Lake Analytics**. Cada cuenta de Data Lake Analytics tiene un nombre.
* **Ubicación**. Utilice uno de los centros de datos de Azure de Hola que admita el análisis de Data Lake.
* **Cuenta predeterminada de Data Lake Store**: cada cuenta de Data Lake Analytics tiene una cuenta de Data Lake Store predeterminada.

cuenta toolist Hola existente almacén de Data Lake:

```
az dls account list
```

toocreate una nueva cuenta de almacén de Data Lake:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Usar hello siguiendo la sintaxis toocreate una cuenta de análisis de Data Lake:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Después de crear una cuenta, puede usar hello siguiendo las cuentas de comandos toolist hello y mostrar detalles de la cuenta:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Cargar el almacén de datos tooData Lake
En este tutorial, va a procesar algunos registros de búsqueda.  registro de búsqueda de Hello puede almacenarse en el almacén de Data Lake o almacenamiento de blobs de Azure.

Hola portal de Azure proporciona una interfaz de usuario para copiar algunos ejemplo datos archivos toohello almacén de Data Lake cuenta predeterminada, que incluyen un archivo de registro de búsqueda. Vea [preparar los datos de origen](data-lake-analytics-get-started-portal.md) cuenta de almacén de Data Lake tooupload Hola datos toohello predeterminada.

los archivos de tooupload mediante 2.0 de CLI, utilizan Hola siguientes comandos:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Análisis de Data Lake también puede acceder al almacenamiento de blobs de Azure.  Para cargar el almacenamiento de blobs de tooAzure de datos, vea [Using Hola CLI de Azure con el almacenamiento de Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Envío de trabajos de Análisis de Data Lake
trabajos de análisis de Data Lake de Hola se escriben en lenguaje SQL U Hola. toolearn más información acerca de T-SQL, consulte [empezar a trabajar con lenguaje SQL U](data-lake-analytics-u-sql-get-started.md) y [eence de lenguaje SQL U](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate un script de trabajo de análisis de Data Lake**

Crear un archivo de texto con el siguiente script SQL U y guarde la estación de trabajo de hello texto archivo tooyour:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Este script U-SQL lee el archivo de datos de origen de hello mediante **Extractors.Tsv()**y, a continuación, crea un archivo csv mediante **Outputters.Csv()**.

No modifique dos rutas de acceso de Hola a menos que copie el archivo de código fuente de hello en una ubicación diferente.  Análisis de Data Lake crea la carpeta de salida de hello si no existe.

Resulta más sencillos rutas de acceso relativas toouse para archivos almacenados en las cuentas de almacén de Data Lake de forma predeterminada. También puede usar rutas de acceso absolutas.  Por ejemplo:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Debe usar archivos de tooaccess de rutas de acceso absolutas en las cuentas de almacenamiento vinculadas.  sintaxis de Hola para archivos almacenados en la cuenta de almacenamiento de Azure vinculada es:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> El contenedor de blobs de Azure con blobs públicos no se admite.      
> El contenedor de blobs de Azure con contenedores públicos no se admite.      
>

**trabajos de toosubmit**

Usar hello siguiendo la sintaxis toosubmit un trabajo.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Por ejemplo:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**trabajos de toolist y mostrar detalles del trabajo**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**trabajos de toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Recuperación de los resultados de un trabajo

Después de que se completa un trabajo, puede usar hello siguientes archivos de salida de comandos toolist hello y descargar archivos de hello:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Por ejemplo:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Canalizaciones y repeticiones

**Obtención de información sobre canalizaciones y repeticiones**

Hola de uso `az dla job pipeline` comandos anteriormente envía la información de canalización de Hola de toosee trabajos.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Hola de uso `az dla job recurrence` comandos toosee información de periodicidad de Hola para los trabajos enviados anteriormente.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Pasos siguientes

* Hola toosee documento de referencia de Data Lake Analytics CLI 2.0, consulte [análisis de Data Lake](https://docs.microsoft.com/cli/azure/dla).
* Hola toosee documento de referencia de almacén de Data Lake CLI 2.0, consulte [almacén de Data Lake](https://docs.microsoft.com/cli/azure/dls).
* toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
