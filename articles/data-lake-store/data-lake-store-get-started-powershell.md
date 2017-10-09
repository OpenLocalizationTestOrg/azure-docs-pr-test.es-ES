---
title: "aaaUse PowerShell tooget a trabajar con el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar PowerShell de Azure toocreate una cuenta de almacén de Data Lake y realizar operaciones básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Introducción al Almacén de Azure Data Lake mediante Azure PowerShell
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

Obtenga información acerca de cómo toouse Azure PowerShell toocreate un Azure Data Lake almacenar cuenta y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versiones posteriores**. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Autenticación
En este artículo usa un método de autenticación más sencillo con el almacén de Data Lake que te encuentres tooenter solicitada sus credenciales de cuenta de Azure. Hola acceso nivel tooData Lake almacén cuenta de sistema de archivos y, a continuación, se rige por el nivel de acceso de Hola de hello usuario registrado. Sin embargo, hay otros métodos como tooauthenticate bien con el almacén de Data Lake, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Creación de una cuenta de Almacén de Azure Data Lake
1. Desde el escritorio, abra una nueva ventana de Windows PowerShell, escriba Hola después toolog de fragmento de código en tooyour cuenta de Azure, establecer Hola suscripción y registrar proveedor de almacén de Data Lake Hola. Cuando toolog solicitada, asegúrese de que inicie sesión como una suscripción de hello admininistrators/propietario:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure. Comience creando un grupo de recursos de Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Creación de un grupo de recursos de Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Creación de un grupo de recursos de Azure")
3. Cree una cuenta de Almacén de Azure Data Lake. nombre de Hola que especifique debe contener solo letras minúsculas y números.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Creación de una cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Creación de una cuenta de Azure Data Lake Store")
4. Compruebe que la cuenta de hello se creó correctamente.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    Hola de salida para esto debería ser **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Creación de estructuras de directorios en el Almacén de Azure Data Lake
Puede crear directorios en su toomanage de cuenta de almacén de Azure Data Lake y almacenar datos.

1. Especifique un directorio raíz.

        $myrootdir = "/"
2. Crear un nuevo directorio denominado **mynewdirectory** en la raíz especificada Hola.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Compruebe que ese nuevo directorio Hola se creó correctamente.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Debería mostrarse una salida similar Hola siguiente:

    ![Comprobación del directorio](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Comprobación del directorio")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Cargar el almacén de datos tooyour Azure Data Lake
Puede cargar el almacén de datos tooData Lake directamente en hello tooa o directorio raíz que ha creado en la cuenta de hello. Hola fragmentos siguientes muestran cómo tooupload algún directorio toohello de datos de ejemplo (**mynewdirectory**) que creó en la sección anterior de Hola.

Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Descargar archivo hello y almacenarlo en un directorio local en el equipo, como C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Cambio del nombre, descarga y eliminación de los datos del Almacén de Data Lake
toorename un archivo, use Hola siguiente comando:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload un archivo, use Hola siguiente comando:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete un archivo, use Hola siguiente comando:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Cuando se le solicite, escriba **Y** toodelete elemento de saludo. Si tiene más de un toodelete de archivo, puede proporcionar todas las rutas de acceso de hello separados por coma.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Eliminación de una cuenta del Almacén de Azure Data Lake
Use su cuenta de almacén de Data Lake de hello después toodelete de comando.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Cuando se le solicite, escriba **Y** cuenta de hello toodelete.

## <a name="performance-guidance-while-using-powershell"></a>Guía de rendimiento al usar PowerShell

A continuación se muestran Hola configuraciones más importantes que pueden estar atento tooget Hola obtener el mejor rendimiento al usar PowerShell toowork con almacén de Data Lake:

| Propiedad            | Valor predeterminado | Descripción |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Este parámetro permite a toochoose número de Hola de subprocesos paralelos para cargar o descargar cada archivo. Este número representa Hola número máximo de subprocesos que se pueden asignar por archivo, pero es posible que obtenga menos subprocesos según el escenario (por ejemplo, si está cargando un archivo de 1 KB, obtendrá un subproceso, incluso si se le solicite 20 subprocesos).  |
| ConcurrentFileCount | 10      | Este parámetro es específico para cargar o descargar carpetas. Este parámetro determina el número de Hola de archivos simultáneos que puede ser cargados o descargados. Este número representa el número máximo de Hola de archivos simultáneos que puede ser cargados o descargados al mismo tiempo, pero es posible que obtenga menos simultaneidad según el escenario (por ejemplo, si va a cargar dos archivos, obtendrá dos cargas de archivos simultáneas, incluso si se le solicite 15). |

**Ejemplo**

Este comando descarga los archivos de la unidad local del usuario de almacén de Azure Data Lake toohello con 20 subprocesos por archivo y 100 archivos simultáneos.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>¿Cómo determino hello tooset de valor para estos parámetros?

A continuación hay algunas instrucciones que puede usar.

* **Paso 1: Determinar el número total de subprocesos de hello** -debe empezar por el cálculo toouse de recuento total de subprocesos de Hola. Como norma general, debe usar seis subprocesos por cada núcleo físico.

        Total thread count = total physical cores * 6

    **Ejemplo**

    Suponiendo que se está ejecutando Hola PowerShell comandos de una máquina virtual D14 que tiene 16 núcleos

        Total thread count = 16 cores * 6 = 96 threads


* **Paso 2: Calcular PerFileThreadCount** -calculamos nuestro PerFileThreadCount según Hola tamaño de los archivos de saludo. Para archivos de menos de 2,5 GB, no hay ninguna necesidad de toochange este parámetro porque predeterminado Hola de 10 es suficiente. Para los archivos mayores de GB 2.5, debe usar 10 subprocesos como base Hola Hola primera 2,5 GB y agregar 1 subproceso de cada aumento adicional de 256 MB de tamaño del archivo. Si está copiando una carpeta con muchos tamaños de archivo, considere la posibilidad de agruparlos por tamaños de archivo similares. Tener tamaños de archivo diferentes puede provocar un rendimiento no óptimo. Si no es posible toogroup tamaños de archivo similares, debe establecer PerFileThreadCount según Hola mayor tamaño de archivo.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Ejemplo**

    Suponiendo que tenga 100 archivos comprendido entre 1GB too10GB, usamos Hola 10GB como Hola de mayor tamaño de ecuación, que se lee como Hola siguiente del archivo.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Paso 3: Calcular ConcurrentFilecount** -recuento de uso total de subprocesos de Hola y PerFileThreadCount toocalculate ConcurrentFileCount basándose en hello después de la ecuación.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Ejemplo**

    En función de los valores de ejemplo de Hola que se ha utilizado

        96 = 40 * ConcurrentFileCount

    Por lo tanto, **ConcurrentFileCount** es **2.4**, que se puede redondear demasiado**2**.

### <a name="further-tuning"></a>Ajuste adicional

Es posible que necesite para la optimización adicional porque no hay un intervalo de toowork de tamaños de archivo con. Hola anteriormente cálculo funciona bien si todos o la mayoría de los archivos de hello es intervalos de 10GB de toohello más grandes y más cercano. Por el contrario, si hay muchos tamaños de archivo diferentes, con muchos archivos pequeños, podría reducir PerFileThreadCount. Reduciendo hello PerFileThreadCount, podemos ampliamos ConcurrentFileCount. Por lo tanto, si suponemos que la mayoría de los archivos es más pequeña en el intervalo de 5GB de hello, se puede volver a realizar nuestro cálculo:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Por lo tanto, **ConcurrentFileCount** se ahora 96/20, que es 4.8, redondeará demasiado**4**.

Puede seguir tootune esta configuración cambiando hello **PerFileThreadCount** arriba y abajo según distribución Hola de los tamaños de archivo.

### <a name="limitation"></a>Limitación

* **Número de archivos es menor que ConcurrentFileCount**: si el número de Hola de archivos que se va a cargar es menor que hello **ConcurrentFileCount** que calcula, a continuación, se debe reducir  **ConcurrentFileCount** toobe toohello igual número de archivos. Puede usar cualquier tooincrease de subprocesos restantes **PerFileThreadCount**.

* **Hay demasiados subprocesos**: si se aumenta el subproceso número demasiada sin aumentar el tamaño del clúster, se corre el riesgo de Hola de reducción del rendimiento. Puede haber problemas de contención al cambio de contexto en hello CPU.

* **Simultaneidad suficiente**: si no es suficiente la simultaneidad de hello, el clúster puede ser demasiado pequeño. Puede aumentar el número de Hola de nodos en el clúster lo que le proporcionará más simultaneidad.

* **Errores de limitación**: es posible que vea errores de limitación si la simultaneidad es demasiado alta. Si ve errores de limitación, debe reducir la simultaneidad de Hola o póngase en contacto con nosotros.

## <a name="next-steps"></a>Pasos siguientes
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

