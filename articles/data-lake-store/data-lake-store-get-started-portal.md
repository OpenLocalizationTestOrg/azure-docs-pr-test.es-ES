---
title: "aaaUse tooget de portal de Azure a trabajar con el almacén de Data Lake | Documentos de Microsoft"
description: "Usar hello toocreate portal Azure una cuenta de almacén de Data Lake y realizar operaciones básicas en hello almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Empezar a trabajar con el almacén de Azure Data Lake con hello portal de Azure
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

Obtenga información acerca de cómo toouse Hola toocreate portal Azure una cuenta de almacén de Data Lake de Azure y realizar operaciones básicas, como crear carpetas, cargar y descargar archivos de datos, elimine la cuenta, etcetera. Para más información, consulte [Introducción a Azure Data Lake Store](data-lake-store-overview.md).

Hola siguiendo dos vídeos contiene Hola misma información tal como se describe en este artículo:

* [Crear una cuenta de Almacén de Data Lake](https://mix.office.com/watch/1k1cycy4l4gen)
* [Administrar datos en el almacén de Data Lake con hello Explorador de datos](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguientes elementos:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Creación de una cuenta de Almacén de Azure Data Lake

1. Inicio de sesión toohello nueva [portal de Azure](https://portal.azure.com).
2. Haga clic en **NUEVO**, en **Datos y almacenamiento** y en **Azure Data Lake Store**. Leer la información de Hola Hola **almacén de Azure Data Lake** hoja y, a continuación, haga clic en **crear** en esquina Hola inferior izquierda de la hoja de Hola.
3. Hola **nuevo almacén de Data Lake** hoja, proporcionar valores de hello tal y como se muestra en la siguiente captura de pantalla de hello:
   
    ![Creación de una nueva cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Creación de una nueva cuenta de Azure Data Lake")
   
   * **Nombre**. Escriba un nombre único para la cuenta de almacén de Data Lake Hola.
   * **Suscripción**. Seleccione la suscripción de hello bajo el cual desea toocreate una nueva cuenta de almacén de Data Lake.
   * **Grupo de recursos**. Seleccione un grupo de recursos existente o hello **crear nuevo** toocreate opción uno. Un grupo de recursos es un contenedor que incluye los recursos relacionados de una aplicación. Para más información, consulte [Grupos de recursos en Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Ubicación**: seleccione una ubicación donde desea que la cuenta de almacén de Data Lake hello toocreate.
   * **Configuración de cifrado**. Hay tres opciones:
     
     * **No habilitar el cifrado**.
     * **Usar claves administradas por Azure Data Lake**.  Si desea que el almacén de Azure Data Lake toomanage las claves de cifrado.
     * **Elegir las claves en Azure Key Vault**. Puede seleccionar una instancia de Azure Key Vault existente o crear una nueva. claves de hello toouse desde un almacén de claves, debe asignar permisos para hello cuenta de almacén de Azure Data Lake tooaccess Hola almacén de claves de Azure. Para obtener instrucciones de hello, consulte [asignar permisos tooAzure el almacén de claves](#assign-permissions-to-azure-key-vault).
       
        ![Cifrado de Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Cifrado de Data Lake Store")
       
        Haga clic en **Aceptar** en hello **configuración de cifrado** hoja.

        Para obtener más información, consulte [Cifrado de datos en Azure Data Lake Store](./data-lake-store-encryption.md).

4. Haga clic en **Crear**. Si ha elegido toopin panel de toohello de la cuenta de hello, se le dirigirá de nuevo panel toohello y puede ver progreso de Hola de su almacén de Data Lake el aprovisionamiento de cuentas. Una vez se aprovisiona Hola cuenta de almacén de Data Lake, hoja de la cuenta de hello aparezca.

También puede crear una cuenta de Data Lake Store con plantillas de Azure Resource Manager. Estas plantillas son accesibles desde las [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store):

- Sin cifrado de datos: [Implementación de la cuenta de Azure Data Lake Store sin cifrado de datos](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Con cifrado de datos mediante Data Lake Store: [Implementación de la cuenta de Data Lake Store con cifrado (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Con cifrado de datos mediante Azure Key Vault: [Implementación de la cuenta de Data Lake Store con cifrado (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>Asignar permisos tooAzure el almacén de claves
Si utiliza las claves de un cifrado de tooconfigure de almacén de claves de Azure en hello cuenta de almacén de Data Lake, debe configurar el acceso entre la cuenta de almacén de Data Lake de Hola y Hola almacén de claves de Azure. Realizar Hola siguiendo los pasos toodo así.

1. Si utiliza las claves de hello almacén de claves de Azure, hoja de Hola para hello cuenta de almacén de Data Lake muestra una advertencia en la parte superior de Hola. Haga clic en Hola de hello advertencia tooopen **configurar permisos del almacén de claves** hoja.
   
    ![Cifrado de Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Cifrado de Data Lake Store")
2. hoja de Hello muestra dos opciones tooconfigure acceso.
   
   * En la primera opción hello, haga clic en **permiso Grant** tooconfigure acceso. Hola primera opción está habilitada sólo cuando el usuario de Hola que creó la cuenta de almacén de Data Lake hello también es un administrador de almacén de claves de Azure de Hola.
   * Hello otra opción es cmdlet de PowerShell de hello toorun aparece en la hoja de Hola. Debe tener propietario de hello toobe del almacén de claves de Azure de Hola o tener permisos de toogrant de capacidad de hello en hello almacén de claves de Azure. Después de ejecutar el cmdlet de hello, vuelven a estar toohello hoja y haga clic en **habilitar** tooconfigure acceso.

## <a name="createfolder"></a>Creación de carpetas en una cuenta de Almacén de Azure Data Lake
Puede crear carpetas en su toomanage de cuenta de almacén de Data Lake y almacenar datos.

1. Abrir cuenta de almacén de Data Lake Hola que creó. En el panel izquierdo de hello, haga clic en **examinar**, haga clic en **almacén de Data Lake**y, a continuación, desde la hoja de almacén de Data Lake hello, haga clic en nombre de la cuenta de hello bajo el cual desea toocreate carpetas. Si ancla el panel de inicio de hello cuenta toohello, haga clic en ese icono de cuenta.
2. En la hoja de su cuenta de Almacén de Data Lake, haga clic en **Explorador de datos**.
   
    ![Creación de una cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Creación de una cuenta de Azure Data Lake Store")
3. En la hoja de la cuenta de almacén de Data Lake, haga clic en **nueva carpeta**, escriba un nombre para la nueva carpeta de hello y, a continuación, haga clic en **Aceptar**.
   
    ![Creación de una cuenta de Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Creación de una cuenta de Azure Data Lake Store")
   
    carpeta de Hello recién creado aparece en hello **Explorador de datos** hoja. Puede crear carpetas anidadas hasta cualquier nivel.
   
    ![Creación de carpetas en una cuenta de Data Lake Store](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Creación de carpetas en una cuenta de Data Lake Store")

## <a name="uploaddata"></a>Cargar la cuenta de almacén de Data Lake tooAzure de datos
Puede cargar su cuenta de almacén de Azure Data Lake directamente en hello tooa o nivel de carpeta raíz que ha creado en la cuenta de hello tooan de datos. Hola siguiente captura de pantalla, siga tooupload de pasos de hello una subcarpeta de tooa de archivo de hello **Explorador de datos** hoja. En esta captura de pantalla, archivo hello es subcarpeta tooa cargado se muestra en rutas de hello (marcadas en un cuadro rojo).

Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Cargar datos](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Cargar datos")

## <a name="properties"></a>Propiedades y acciones disponibles en hello los datos almacenados
Haga clic en Hola Hola de tooopen de archivo recién agregada **propiedades** hoja. propiedades de Hello asociadas con el archivo hello y acciones de Hola que puede realizar en el archivo hello están disponibles en esta hoja. También puede copiar toofile de ruta de acceso completa de hello en su cuenta de almacén de Azure Data Lake, resaltada en el cuadro de hello rojo en la siguiente captura de pantalla de hello:

![Propiedades de datos de hello](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "propiedades en los datos de Hola")

* Haga clic en **vista previa** toosee una vista previa del archivo de hello, directamente desde el Explorador de Hola. Puede especificar formato Hola de vista previa de hello así. Haga clic en **vista previa**, haga clic en **formato** en hello **vista previa del archivo** hoja y en hello **formato de archivo de vista previa** hoja especificar opciones de hello como como el número de filas toodisplay, codificación toouse, toouse de delimitador, etcetera.
  
  ![Formato de vista previa de archivo ](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Formato de vista previa de archivo")
* Haga clic en **descargar** equipo tooyour de toodownload Hola archivo.
* Haga clic en **archivo Rename** archivo de hello toorename.
* Haga clic en **eliminar el archivo** archivo de hello toodelete.

## <a name="secure-your-data"></a>Protección de los datos
Puede proteger los datos de hello almacenados en su cuenta de almacén de Azure Data Lake con Azure Active Directory y el control de acceso (ACL). Para obtener instrucciones sobre cómo toodo que vea [proteger los datos en el almacén de Azure Data Lake](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Eliminación de la cuenta de Almacén de Azure Data Lake
Haga clic en una cuenta de almacén de Azure Data Lake, desde la hoja de almacén de Data Lake de toodelete **eliminar**. acción de hello tooconfirm, le nombre de hello tooenter solicitadas de cuenta de hello que desea toodelete. Escriba Hola nombre de cuenta de hello y, a continuación, haga clic en **eliminar**.

![Eliminar cuenta de Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Eliminar cuenta de Data Lake")

## <a name="next-steps"></a>Pasos siguientes
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Acceso a los registros de diagnóstico de Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

