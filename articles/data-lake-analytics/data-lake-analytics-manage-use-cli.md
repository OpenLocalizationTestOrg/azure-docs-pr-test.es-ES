---
title: "aaaManage análisis de Data Lake de Azure mediante la interfaz de línea de comandos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo trabajos de cuentas de análisis de Data Lake toomanage, orígenes de datos y los usuarios mediante la CLI de Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Administración del Análisis de Azure Data Lake mediante Interfaz de línea de comandos (CLI) de Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake toomanage, orígenes de datos, los usuarios y trabajos mediante Hola CLI de Azure. temas de administración de toosee con otras herramientas, haga clic en Seleccionar de pestaña de hello anterior.


**Requisitos previos**

Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI**. Consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md).
  * Descargue e instale hello **preliminares** [herramientas de Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) en orden toocomplete esta demostración.
* **Autenticación**con Hola comando siguiente:
  
        azure login
    Para obtener más información acerca de cómo autenticar con una cuenta profesional o educativa, consulte [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).
* **Modo del conmutador toohello Azure Resource Manager**con Hola comando siguiente:
  
        azure config mode arm

**comandos de almacén de Data Lake y análisis de Data Lake de Hola toolist:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Administrar cuentas
Antes de ejecutar un trabajo de Análisis de Data Lake, debe tener una cuenta de Análisis de Data Lake. A diferencia de HDInsight de Azure, no se paga por una cuenta de Análisis cuando no está ejecutando un trabajo.  Solo paga por vez hello cuando se ejecuta un trabajo.  Para obtener más información, consulte la página con [información general sobre Análisis con Azure Data Lake](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Creación de cuentas
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Actualización de cuentas
Hello comando siguiente actualiza las propiedades de Hola de una cuenta de análisis de Data Lake existente

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Enumeración de cuentas
Enumeración de cuentas de Análisis de Data Lake 

    azure datalake analytics account list

Enumerar cuentas de Análisis de Data Lake dentro de un grupo de recursos específico

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Obtener detalles de una cuenta específica de Análisis de Data Lake

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Eliminación de cuentas de Análisis de Data Lake
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Administración de orígenes de datos de cuenta
Análisis de Data Lake admite actualmente Hola siguientes orígenes de datos:

* [Almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Cuando se crea una cuenta de análisis, debe designar una cuenta de almacenamiento predeterminada de almacenamiento de Azure datos Lake cuenta toobe Hola. Hello cuenta de almacenamiento predeterminado ADL se utiliza registros de auditoría de metadatos de trabajo toostore y trabajo. Una vez creada la cuenta de Análisis, puede agregar más cuentas de Almacén de Data Lake y/o cuentas de Almacenamiento de Azure. 

### <a name="find-hello-default-adl-storage-account"></a>Busque la cuenta de almacenamiento de hello predeterminado ADL
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

valor de Hello aparece en propiedades: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Adición de más cuentas de almacenamiento de blobs de Azure
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Solo se admiten nombres cortos de almacenamiento de blobs.  No use el FQDN, por ejemplo "myblob.blob.core.windows.net".
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Adición de más cuentas de Almacén de Data Lake
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-[d] es un modificador opcional tooindicate si Hola Data Lake añadidos es cuenta de Data Lake de hello predeterminada. 

### <a name="update-existing-data-source"></a>Actualizar el origen de datos existente
tooset una existente almacén de Data Lake cuenta toobe Hola de forma predeterminada:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate una clave de cuenta de almacenamiento de blobs existente:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Enumeración de orígenes de datos:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Eliminar orígenes de datos:
toodelete una cuenta de almacén de Data Lake:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete una cuenta de almacenamiento de blobs:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Trabajos de administración
Debe tener una cuenta de Análisis de Data Lake para poder crear un trabajo.  Para obtener más información, consulte [Administración de cuentas de Análisis de Data Lake](#manage-accounts).

### <a name="list-jobs"></a>Enumeración de trabajos
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Obtención de detalles del trabajo
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Envío de trabajos
> [!NOTE]
> prioridad de Hello predeterminada de un trabajo es 1000 y grado de hello predeterminado de paralelismo para un trabajo es 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Cancelación de trabajos
Usar identificador de trabajo de hello toofind del comando de la lista hello y, a continuación, usar Cancelar toocancel Hola trabajo.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Administrar catálogo
catálogo de Hello U-SQL es toostructure usa datos y el código para que pueda compartir por secuencias de comandos SQL U. catálogo de Hello permite Hola mayor rendimiento posible con los datos de Azure Data Lake. Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Enumeración de elementos del catálogo
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

los tipos de Hello incluyen la base de datos, esquema, ensamblado, origen de datos externo, tabla, función con valores de tabla o las estadísticas de tabla.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Usar grupos ARM
Las aplicaciones normalmente se componen de muchos componentes,por ejemplo una aplicación web, base de datos, servidor de base de datos, almacenamiento y servicios de terceros. Azure Resource Manager (ARM) permite toowork con recursos de hello en la aplicación como un grupo, denominado tooas un grupo de recursos de Azure. Puede implementar, actualizar, supervisar o eliminar todos los recursos de Hola para su aplicación en una única operación coordinada. Para la implementación se utiliza una plantilla, y esta plantilla puede trabajar en diferentes entornos, como pruebas, ensayo y producción. Para aclarar la facturación para su organización mediante la visualización de los costos de consolidada de hello para el grupo completo de Hola. Para obtener más información, consulte [Información general del Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md). 

Un servicio de análisis de Data Lake puede incluir Hola de los componentes siguientes:

* Cuenta de Análisis de Azure Data Lake
* Cuenta predeterminada y necesaria de Almacén de Azure Data Lake
* Cuentas adicionales de Almacén de Azure Data Lake
* Cuentas adicionales de Almacenamiento de Azure

Puede crear todos estos componentes en un BRAZO grupo toomake les toomanage más fácil.

![Cuenta y almacenamiento de Análisis de Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Una cuenta de análisis de Data Lake y cuentas de almacenamiento dependientes de hello deben colocarse en hello mismo centro de datos de Azure.
grupo de Hello ARM no obstante puede encontrarse en otro centro de datos.  

## <a name="see-also"></a>Otras referencias
* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Introducción a Análisis de Data Lake mediante el Portal de Azure](data-lake-analytics-get-started-portal.md)
* [Administración de Análisis de Azure Data Lake mediante el Portal de Azure](data-lake-analytics-manage-use-portal.md)
* [Supervisión y solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

