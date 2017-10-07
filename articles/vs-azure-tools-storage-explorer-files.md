---
title: "aaaUsing Explorador de almacenamiento (versión preliminar) con el almacenamiento de archivos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo obtener información sobre cómo toouse toowork de explorador de almacenamiento (versión preliminar) con el archivo de recursos compartidos y archivos."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Uso del Explorador de Storage (versión preliminar) con Azure File Storage

Archivo de almacenamiento es un servicio que proporciona el archivo de los recursos compartidos de hello en la nube con Azure Hola estándar Protocolo de bloque de mensajes del servidor (SMB). Se admiten SMB 2.1 y SMB 3.0. Con el almacenamiento de archivos de Azure, puede migrar las aplicaciones heredadas que se basan en tooAzure de recursos compartidos de archivo rápidamente y sin costosas de escribir de nuevo. Puede usar datos de tooexpose de almacenamiento de archivo públicamente toohello world o datos de la aplicación toostore privada. En este artículo, aprenderá cómo toouse toowork de explorador de almacenamiento (versión preliminar) con el archivo de recursos compartidos y archivos.

## <a name="prerequisites"></a>Requisitos previos

pasos de hello toocomplete en este artículo, necesitará Hola siguiente:

- [Descargue e instale el Explorador de almacenamiento (versión preliminar)](http://www.storageexplorer.com/)

- [Conectar la cuenta de almacenamiento de Azure tooa o servicio](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Creación de un recurso compartido de archivos

Todos los archivos deben residir en un recurso compartido de archivos, que no es más que una agrupación lógica de archivos. Una cuenta puede contener un número ilimitado de recursos compartidos de archivos y cada uno de ellos puede almacenar un número ilimitado de archivos.

Hola siguientes pasos muestra cómo toocreate un recurso compartido de archivos en el Explorador de almacenamiento (versión preliminar).

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de hello dentro del cual desea toocreate Hola recurso compartido de archivos

3. Haga clic en **recursos compartidos de archivos**y - en el menú contextual de hello: seleccione **crear recurso compartido de archivos**.

    ![Creación un recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Aparecerá un cuadro de texto bajo hello **recursos compartidos de archivos** carpeta. Escriba el nombre de hello para el recurso compartido de archivos. Vea hello [compartir las reglas de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sección para obtener una lista de reglas y restricciones de nomenclatura de recursos compartidos de archivos.

    ![Recurso compartido de Hola de nomenclatura](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Presione **ENTRAR** cuando toocreate done Hola recurso compartido de archivos, o **Esc** toocancel. Una vez que se creó correctamente el recurso compartido de archivos de hello, se mostrará en hello **recursos compartidos de archivos** selecciona la carpeta para hello cuenta de almacenamiento.

    ![nuevo recurso compartido de Hola](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Visualización del contenido de un recurso compartido de archivos

Los recursos compartidos de archivos contienen archivos y carpetas (que también pueden contener archivos).

Hello siguientes pasos muestran cómo comparte contenido de hello tooview de un archivo en el Explorador de almacenamiento (versión preliminar): +

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea tooview.

3. Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4. Recurso compartido de archivos de hello contextual desea tooview y - en el menú contextual de hello: seleccione **abiertos**. Se puede hacer doble clic en recurso compartido de archivos de hello desea tooview.

    ![Abrir recurso compartido](media/vs-azure-tools-storage-explorer-files/image4.png)

5. panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.
    
    ![Hola contenido del recurso compartido](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Eliminación de un recurso compartido de archivos

Los recursos compartidos de archivos se pueden crear y eliminar fácilmente si fuera necesario. (toosee cómo toodelete archivos individuales, consulte la sección toohello, [administrar archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hola siguientes pasos muestra cómo toodelete un recurso compartido de archivos en el Explorador de almacenamiento (versión preliminar):

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea tooview.

3. Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4. Recurso compartido de archivos de hello contextual desea toodelete y - en el menú contextual de hello: seleccione **eliminar**. También puede presionar **eliminar** recurso compartido de archivo actualmente seleccionado de hello toodelete.

    ![Eliminar](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Seleccione **Sí** toohello cuadro de diálogo de confirmación.
    
    ![Cuadro de diálogo Confirmación](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Copia de un recurso compartido de archivos

Explorador de almacenamiento (versión preliminar) permite toocopy un Portapapeles toohello de recurso compartido de archivo y, a continuación, pegue ese recurso compartido de archivos en otra cuenta de almacenamiento. (toosee cómo toocopy archivos individuales, consulte la sección toohello, [administrar archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hola siguientes pasos muestra cómo compartir toocopy un archivo desde una tooanother de cuenta de almacenamiento.

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea toocopy.

3. Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4. Recurso compartido de archivos de hello contextual desea toocopy y - en el menú contextual de hello: seleccione **el recurso compartido de archivos de copia**.

    ![Copiar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Haga clic en la cuenta de almacenamiento de destino"hello deseado" en la que desee recurso compartido de archivos de hello toopaste y - en el menú contextual de hello: seleccione **el recurso compartido de archivos de pegar**.

    ![Pegar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Obtener Hola SAS para un recurso compartido de archivos

A [firma de acceso compartido (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) proporciona acceso delegado tooresources en su cuenta de almacenamiento. Esto significa que puede conceder a que un cliente limitada tooobjects permisos en su cuenta de almacenamiento en un periodo de tiempo y con un conjunto especificado de permisos, sin necesidad de tooshare las claves de acceso de cuenta.

Hello siguientes pasos muestran cómo toocreate una SAS para un archivo compartir: +

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello para el que desea tooget una SAS.

3. Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4. Haga clic en recurso compartido de archivos deseado de Hola y - en el menú contextual de hello: seleccione **obtener firma de acceso compartido**.

    ![Obtener firma de acceso compartido](media/vs-azure-tools-storage-explorer-files/image10.png)

5. Hola **firma de acceso compartido** cuadro de diálogo, especifique la directiva de hello, las fechas de inicio y finalización, zona horaria y tener acceso a niveles que desee para el recurso de Hola.

    ![Cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Cuando haya terminado de especificar las opciones de SAS de hello, seleccione **crear**.

7. Un segundo **firma de acceso compartido** cuadro de diálogo, a continuación, mostrará que listas Hola recurso compartido de archivos junto con la dirección URL de Hola y cadenas que se puede usar tooaccess Hola recurso de almacenamiento. Seleccione **copia** siguiente dirección URL de toohello desea toocopy toohello Portapapeles.
    
    ![Segundo cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Cuando haya terminado, seleccione **Cerrar**.

## <a name="manage-access-policies-for-a-file-share"></a>Administración de directivas de acceso para un recurso compartido de archivos

Hello siguientes pasos muestran cómo toomanage (agregar y quitar) las directivas para un recurso compartido de archivos de acceso: +. las directivas de acceso de Hola se usa para crear direcciones URL de SAS a través del cual las personas pueden utilizar tooaccess Hola recursos de archivo de almacenamiento durante un período de tiempo definido.

1. Abra el Explorador de almacenamiento (versión preliminar).

2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello cuyas directivas de acceso que se va toomanage.

3. Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4. Seleccione el recurso compartido de archivos deseado de Hola y - en el menú contextual de hello: seleccione **administrar directivas de acceso**.

    ![Menú contextual Administrar directivas de acceso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Hola **las directivas de acceso** cuadro de diálogo mostrará una lista de las directivas de acceso creadas anteriormente para el recurso compartido de archivos seleccionado de Hola.
    
    ![Directivas de acceso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Siga estos pasos dependiendo de la tarea de administración de directivas de acceso de Hola:
    
    - **Agregar una nueva directiva de acceso**: seleccione **Agregar**. Una vez generado, Hola **las directivas de acceso** cuadro de diálogo mostrará Hola recién agregado tener acceso a la directiva (con configuración predeterminada).

    - **Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.

    - **Quitar una directiva de acceso** : seleccione esta opción **quitar** siguiente directiva de acceso de toohello desea tooremove.

7. Crear una nueva dirección URL de SAS con hello directivas de acceso que ha creado anteriormente:
    
    ![Obtener SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nombre y propiedades de SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Administración de archivos en un recurso compartido de archivos

Después de crear un recurso compartido de archivos, puede cargar un recurso compartido de archivo toothat, descargue un equipo local de tooyour de archivo, abrir un archivo en el equipo local y mucho más.

Hello siguientes pasos muestran cómo compartan toomanage Hola archivos (y carpetas) dentro de un archivo.

1.  Abra el Explorador de almacenamiento (versión preliminar).

2.  En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea toomanage.

3.  Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.

4.  Haga doble clic en el recurso compartido de archivos de hello desea tooview.

5.  panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.

    ![Hola contenido del recurso compartido](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.

7.  Siga estos que pasos dependiendo de la tarea hello desea tooperform:

    - **Cargar el recurso compartido de archivos de tooa de archivos**

        a.  En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar archivos** desde el menú desplegable de Hola.

        ![Carga de archivos](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. Hola **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **archivos** tooselect Hola archivos desea tooupload de cuadro de texto.

        ![Adición de archivos](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Seleccione **Cargar**.

    - **Cargar un recurso compartido de archivos de carpeta tooa**
        
        a. En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar carpeta** desde el menú desplegable de Hola.

        ![Menú Cargar carpeta](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. Hola **carga carpeta** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **carpeta** carpeta de Hola de tooselect de cuadro de texto cuyo contenido desea tooupload.

        c. Si lo desea, especifique una carpeta de destino en qué Hola se cargará el contenido de la carpeta seleccionada. Si no existe la carpeta de destino de hello, se creará.

        d. Seleccione **Cargar**.

    - **Descargar un equipo local de tooyour de archivo**
        
        a. Seleccione archivo hello desea toodownload.
        
        b. En la barra de herramientas del panel principal de hello, seleccione **descargar**.
        
        c. Hola **especificar donde hello toosave descarga archivo** cuadro de diálogo, especificar ubicación de Hola donde desea descargar el archivo de Hola y Hola nombre que desee toogive se.

        d. Seleccione **Guardar**.

    - **Abrir un archivo en el equipo local**
        
        a.  Seleccione archivo hello desea tooopen.
        
        b.  En la barra de herramientas del panel principal de hello, seleccione **abiertos**.
        
        c.  archivo Hello se van a descargar y abre con la aplicación hello asociada con el tipo de archivo subyacente del archivo Hola.

    - **Copiar un Portapapeles toohello de archivo**

        a. Seleccione archivo hello desea toocopy.

        b. En la barra de herramientas del panel principal de hello, seleccione **copia**.

        c. En el panel izquierdo de hello, navegar tooanother recurso compartido de archivos y haga doble clic tooview en el panel principal Hola.

        d. En la barra de herramientas del panel principal de hello, seleccione **pegar** toocreate una copia del archivo de Hola.

    - **Eliminar un archivo**

        a. Seleccione archivo hello desea toodelete.

        b. En la barra de herramientas del panel principal de hello, seleccione **eliminar**.

        c. Seleccione **Sí** toohello cuadro de diálogo de confirmación.

## <a name="next-steps"></a>Pasos siguientes

- Hola de vista [notas de la versión de explorador de almacenamiento (versión preliminar) y los vídeos más recientes](http://www.storageexplorer.com/).

- Obtenga información acerca de cómo demasiado[crear aplicaciones mediante Azure blobs, tablas, colas y archivos](https://azure.microsoft.com/documentation/services/storage/).
