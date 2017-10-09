---
title: datos de aaaCopy de almacenamiento de blobs tooSQL base de datos - Azure | Documentos de Microsoft
description: "Este tutorial muestra cómo toouse actividad de copia de una factoría de datos de Azure de canalización de datos de toocopy de base de datos de tooSQL de almacenamiento de blobs."
keywords: blob SQL, Almacenamiento de blobs, copia de datos
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Tutorial: Copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

En este tutorial, creará una factoría de datos con datos toocopy de canalización de la base de datos de tooSQL de almacenamiento de blobs.

Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure. Funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.  

> [!NOTE]
> Para obtener una descripción detallada del programa Hola a servicio de factoría de datos, vea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Requisitos previos para el tutorial de Hola
Antes de comenzar este tutorial, debe tener Hola siguiendo los requisitos previos:

* **Suscripción de Azure**.  Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos. Vea hello [gratuita](http://azure.microsoft.com/pricing/free-trial/) artículo para obtener más información.
* **Cuenta de almacenamiento de Azure**. Usar el almacenamiento de blobs de Hola como un **origen** almacén de datos en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.
* **Base de datos de SQL Azure**. Usará una base de datos SQL de Azure como un almacén de datos de **destino** en este tutorial. Si no dispone de una base de datos de SQL Azure que puede usar en el tutorial de hello, vea [cómo toocreate y configurar una base de datos de SQL Azure](../sql-database/sql-database-get-started.md) toocreate uno.
* **SQL Server 2012/2014 o Visual Studio 2013**. Usar SQL Server Management Studio o Visual Studio toocreate una base de datos de ejemplo y los datos de resultado de hello tooview en base de datos de Hola.  

## <a name="collect-blob-storage-account-name-and-key"></a>Obtención del nombre y la clave de la cuenta de Almacenamiento de blobs
Necesita cuenta Hola nombre y clave de cuenta de su almacenamiento de Azure cuenta toodo este tutorial. Anote el **nombre de cuenta** y la **clave de cuenta** para su cuenta de Azure Storage.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **más servicios** en hello dejado de menú y seleccione **cuentas de almacenamiento**.

    ![Examinar: Cuentas de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. Hola **cuentas de almacenamiento** hoja, seleccione hello **cuenta de almacenamiento de Azure** que desea toouse en este tutorial.
4. Seleccione **Claves de acceso** en **CONFIGURACIÓN**.
5. Haga clic en **copia** (imagen) aparece al lado demasiado**nombre de la cuenta de almacenamiento** texto cuadro y guardar y pegar, en algún lugar (por ejemplo: en un archivo de texto).
6. Repetir Hola anterior paso toocopy o anote hello **key1**.

    ![Clave de acceso de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Haga clic en Cerrar todos los módulos de hello **X**.

## <a name="collect-sql-server-database-user-names"></a>Recopilación de nombres de usuario, bases de datos y servidores SQL Server
Necesita nombres Hola del servidor SQL Azure, base de datos y toodo de usuario de este tutorial. Anote los nombres del **servidor**, la **base de datos** y el **usuario** de su instancia de Azure SQL Database.

1. Hola **portal de Azure**, haga clic en **más servicios** en hello izquierdo y seleccione **bases de datos SQL**.
2. Hola **hoja de bases de datos de SQL**, seleccione hello **base de datos** que desea toouse en este tutorial. Tome nota de hello **nombre de base de datos**.  
3. Hola **base de datos SQL** hoja, haga clic en **propiedades** en **configuración**.
4. Tome nota de los valores de hello para **nombre del servidor** y **inicio de sesión de administrador de servidor**.
5. Haga clic en Cerrar todos los módulos de hello **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Permitir a los servicios de Azure tooaccess SQL server
Asegúrese de que **permitir acceso a servicios de tooAzure** configuración girada **ON** para el servidor de SQL Azure para ese servicio Data Factory Hola pueda acceder a su servidor de SQL Azure. Hola tooverify y activar esta configuración, lo siguiente:

1. Haga clic en **más servicios** concentrador Hola izquierda y haga clic en **servidores SQL Server**.
2. Seleccione el servidor y haga clic en **Firewall** en **CONFIGURACIÓN**.
3. Hola **configuración del Firewall** hoja, haga clic en **ON** para **permitir acceso a servicios de tooAzure**.
4. Haga clic en Cerrar todos los módulos de hello **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Preparación del Almacenamiento de blobs y Base de datos SQL
Ahora, prepare el almacenamiento de blobs de Azure y base de datos SQL de Azure para tutorial Hola realizando Hola pasos:  

1. Inicie el Bloc de notas. Copie Hola después de texto y guárdelo como **emp.txt** demasiado**C:\ADFGetStarted** carpeta en el disco duro.

    ```
    John, Doe
    Jane, Doe
    ```
2. Usar herramientas como [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** Hola de contenedor y tooupload **emp.txt** contenedor toohello de archivos.

    ![Explorador de almacenamiento de Azure Copiar los datos de la base de datos de tooSQL de almacenamiento de blobs](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Hola de uso después de hello de toocreate de script SQL **emp** tabla en la base de datos de SQL Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Si tiene instalado en el equipo SQL Server 2012/2014:** siga las instrucciones de [administración de Azure SQL Database utilizando SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server y ejecute hello secuencia de comandos SQL. En este artículo usa hello [portal de Azure clásico](http://manage.windowsazure.com), no Hola [nuevo portal de Azure](https://portal.azure.com), firewall de tooconfigure para un servidor de SQL Azure.

    Si el cliente no está permitido a tooaccess Hola servidor SQL de Azure, necesita tooconfigure firewall para el acceso de tooallow de servidor de SQL Azure desde el equipo (dirección IP). Vea [este artículo](../sql-database/sql-database-configure-firewall-settings.md) para firewall de hello tooconfigure de pasos para el servidor de SQL Azure.

## <a name="create-a-data-factory"></a>Crear una factoría de datos
Ha completado los requisitos previos de Hola. Puede crear una factoría de datos mediante uno de hello siguientes formas. Haga clic en una de las opciones de hello en la lista desplegable de hello en parte superior de Hola u Hola sigue vínculos tooperform Hola tutorial.     

* [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
* [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
* [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. No transforma datos de salida de tooproduce de datos de entrada. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar los datos primera canalización tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).
> 
> Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md). 
