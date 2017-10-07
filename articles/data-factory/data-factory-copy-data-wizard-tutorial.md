---
title: "Tutorial: Creación de una canalización mediante el Asistente para copia | Microsoft Docs"
description: "En este tutorial, crear una canalización del generador de datos de Azure con una actividad de copia mediante Hola Asistente para copiar admite factoría de datos"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Este tutorial muestra cómo hello toouse **Asistente para copiar** toocopy datos desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. 

Hola Data Factory de Azure **Asistente para copiar** permite tooquickly crear una canalización de datos que copia datos de un almacén de datos de destino de origen compatible datos almacén tooa compatible. Por lo tanto, se recomienda utilizar al Asistente de Hola como un primer toocreate de paso una canalización de ejemplo para su escenario de movimiento de datos. Para obtener una lista de almacenes de datos admitidos como orígenes y destinos, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Este tutorial muestra cómo toocreate un generador de datos de Azure, Hola iniciar Asistente para copiar, pasar por una serie de detalles de pasos tooprovide acerca de su escenario de ingesta/movimiento de datos. Cuando termine de pasos del Asistente para hello, el Asistente de hello crea automáticamente una canalización con datos toocopy de actividad de copia de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Para más información acerca de la actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Requisitos previos
Complete los requisitos previos descritos en hello [Tutorial Introducción](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artículo antes de realizar este tutorial.

## <a name="create-data-factory"></a>Creación de Data Factory
En este paso, utilice hello toocreate portal Azure un generador de datos de Azure denominado **ADFTutorialDataFactory**.

1. Inicie sesión demasiado[portal de Azure](https://portal.azure.com).
2. Haga clic en **+ nuevo** desde la esquina superior izquierda de hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**. 
   
   ![New->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. Hola **factoría de datos** hoja:
   
   1. Escriba **ADFTutorialDataFactory** para hello **nombre**.
       nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: `Data factory name “ADFTutorialDataFactory” is not available`, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameADFTutorialDataFactoryYYYYMMDD) y pruebe a crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.  
      
       ![Nombre de Factoría de datos no disponible](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Selección la **suscripción**de Azure.
   3. Para el grupo de recursos, realice una de hello pasos: 
      
      - Seleccione **utilizar existente** tooselect un grupo de recursos existente.
      - Seleccione **crear nuevo** tooenter un nombre para un grupo de recursos.
          
        Algunos de los pasos de hello en este tutorial se supone que usa el nombre de Hola: **ADFTutorialResourceGroup** Hola para grupo de recursos. toolearn acerca de los grupos de recursos, consulte [utilizando recurso agrupa los recursos de Azure de toomanage](../azure-resource-manager/resource-group-overview.md).
   4. Seleccione un **ubicación** de factoría de datos de Hola.
   5. Seleccione **toodashboard Pin** casilla situada en la parte inferior de Hola de hoja de Hola.  
   6. Haga clic en **Crear**.
      
       ![Hoja Nueva Factoría de datos](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en hello después de imagen:
   
   ![Página principal de Factoría de datos](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Inicio del Asistente para copia
1. En la hoja de la factoría de datos de hello, haga clic en **copiar datos [vista previa]** toolaunch hello **Asistente para copiar**. 
   
   > [!NOTE]
   > Si ve ese explorador web de hello está atascado en "Autorizar …", deshabilite o desactive **bloquear las cookies de terceros y datos de sitio** en configuración del explorador hello (o) tenga que habilite y cree una excepción para  **Login.microsoftonline.com** y, a continuación, intente iniciar Asistente de Hola de nuevo.
2. Hola **propiedades** página:
   
   1. Escriba **CopyFromBlobToAzureSql** en **Nombre de tarea**.
   2. Escriba una **descripción** (opcional).
   3. Hola de cambio **fecha hora de inicio** hello y **fecha hora de finalización** para que la fecha de finalización de hello es establecer tootoday e iniciar días antes de fecha toofive.  
   4. Haga clic en **Siguiente**.  
      
      ![Herramienta de copia: página Propiedades](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. En hello **almacén de datos de origen** página, haga clic en **almacenamiento de blobs de Azure** icono. Utilice este almacén de datos de origen de página toospecify hello para la tarea de copia de hello. 
   
    ![Herramienta de copia: página de Almacén de datos de origen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. En hello **especificar cuenta de almacenamiento de blobs de Azure de hello** página:
   
   1. Escriba **AzureStorageLinkedService** en **Nombre de servicio vinculado**.
   2. Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.
   3. Selección la **suscripción**de Azure.  
   4. Seleccione un **cuenta de almacenamiento de Azure** de hello cuentas disponible en la suscripción de hello seleccionado lista de almacenamiento de Azure. También puede elegir tooenter configuración de la cuenta de almacenamiento manualmente mediante la selección **escribir manualmente** opción para hello **método de selección de la cuenta**y, a continuación, haga clic en **siguiente**. 
      
      ![Herramienta Copiar: especificar la cuenta de almacenamiento de blobs de Azure Hola](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. En **Elegir archivo de entrada de Hola o una carpeta** página:
   
   1. Haga doble clic en **adftutorial** (carpeta).
   2. Seleccione **emp.txt** y haga clic en **Elegir**.
      
      ![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. En hello **Elegir archivo de entrada de Hola o una carpeta** página, haga clic en **siguiente**. No seleccione **Binary copy**(Copia binaria). 
   
    ![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. En hello **configuración de formato de archivo** página, verá los delimitadores de Hola y Hola esquema detecta automáticamente por el Asistente de hello bien analizando el archivo hello. También puede escribir manualmente los delimitadores de Hola Hola copia Asistente toostop detecte automáticamente o toooverride. Haga clic en **siguiente** después de revisar los delimitadores de Hola y obtener una vista previa de los datos. 
   
    ![Herramienta de copia: Configuración de formato de archivo](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. En los datos de destino de hello almacenar página, seleccione **base de datos de SQL Azure**y haga clic en **siguiente**.
   
    ![Herramienta de copia: Elegir el almacén de destino](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. En **base de datos de SQL Azure de especificar hello** página:
   
   1. Escriba **AzureSqlLinkedService** para hello **nombre de la conexión** campo.
   2. Confirme que la opción **De suscripciones de Azure** esté seleccionada para **Método de selección de servidor y base de datos**.
   3. Selección la **suscripción**de Azure.  
   4. Seleccione **Nombre de servidor** y **Base de datos**.
   5. En **Nombre de usuario** y **Contraseña**, escriba los valores pertinentes.
   6. Haga clic en **Siguiente**.  
      
      ![Herramienta de copia: Especificar Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. En hello **asignación de tabla** página, seleccione **emp** para hello **destino** de hello lista desplegable y, a continuación, haga clic en **flecha abajo** (opcional) toosee Hola esquema y toopreview Hola los datos.
    
     ![Herramienta de copia: Asignación de tabla](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. En hello **asignación del esquema** página, haga clic en **siguiente**.
    
    ![Herramienta de copia: Asignación de esquemas](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. En hello **configuración de rendimiento** página, haga clic en **siguiente**. 
    
    ![Herramienta de copia: Configuración de rendimiento](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Revise la información en hello **resumen** página y haga clic en **finalizar**. Asistente de Hello crea dos servicios vinculados, dos conjuntos de datos (entrada y salida) y una canalización de factoría de datos de hello (desde donde se haya iniciado Hola Asistente para copiar). 
    
    ![Herramienta de copia: Configuración de rendimiento](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Inicio de la aplicación de supervisión y administración
1. En hello **implementación** página, haga clic en el vínculo de hello: `Click here toomonitor copy pipeline`.
   
   ![Herramienta de copia: Implementación correcta](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. Hola supervisión de la aplicación se inicia en una pestaña independiente en el explorador web.   
   
   ![Aplicación de supervisión](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. estado más reciente de toosee Hola de segmentos por hora, haga clic en **actualizar** botón en hello **WINDOWS actividad** lista final Hola. Verá cinco ventanas de la actividad de cinco días entre las horas de inicio y finalización de la canalización de Hola. lista de Hello no se actualiza automáticamente, por lo que es posible que necesita tooclick actualización de un par de veces para poder ver todas las ventanas de la actividad de hello en estado listo Hola. 
4. Seleccione una ventana de actividad en la lista de Hola. Ver detalles de hello sobre él en hello **Explorer de la ventana de actividad** en hello derecho.

    ![Detalles de ventana de actividad](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Tenga en cuenta que las fechas de hello 11, 12, 13, 14 y 15 son en color verde, lo que significa que ya se han producido Hola los sectores de salida diaria para estas fechas. También vea esta codificación de color en la canalización de Hola y Hola conjunto de datos de salida en la vista de diagrama de Hola. En el paso anterior de hello, tenga en cuenta que ya se han producido dos segmentos, uno de los sectores se está procesando y hello otros dos se esperan toobe procesa (basado en la codificación de colores de hello). 

    Para más información sobre el uso de esta aplicación, consulte el artículo [Supervisión y administración de canalizaciones mediante la aplicación de supervisión](data-factory-monitor-manage-app.md).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Para obtener más información acerca de las propiedades o campos que se ven en el Asistente para copiar de Hola para un almacén de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola. 
