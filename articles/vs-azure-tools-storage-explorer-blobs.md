---
title: "recursos de almacenamiento de blobs de Azure de aaaManage con el Explorador de almacenamiento (versión preliminar) | Documentos de Microsoft"
description: "Administración de blobs y contenedores de blobs de Azure con el Explorador de almacenamiento (versión preliminar)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Administración de recursos de Almacenamiento de blobs de Azure con el Explorador de almacenamiento (versión preliminar)
## <a name="overview"></a>Información general
[Almacenamiento de blobs de Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.
Puede usar datos de tooexpose de almacenamiento de Blob públicamente toohello world o datos de la aplicación toostore privada. En este artículo, aprenderá cómo toouse toowork de explorador de almacenamiento (versión preliminar) con contenedores de blob y los blobs.

## <a name="prerequisites"></a>Requisitos previos
pasos de hello toocomplete en este artículo, necesitará Hola siguiente:

* [Descargue e instale el Explorador de almacenamiento (versión preliminar)](http://www.storageexplorer.com)
* [Conectar la cuenta de almacenamiento de Azure tooa o servicio](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Creación de un contenedor de blobs
Todos los blobs deben residir en un contenedor de blobs, que no es más que una agrupación lógica de blobs. Una cuenta puede contener un número ilimitado de contenedores y cada contenedor puede almacenar un número ilimitado de blobs.

Hello siguientes pasos muestran cómo toocreate un contenedor de blobs en el Explorador de almacenamiento (versión preliminar).

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de hello dentro del cual desea contenedor de blobs de toocreate Hola.
3. Haga clic en **contenedores de blobs**y - en el menú contextual de hello: seleccione **crear contenedor de blobs**.

   ![Menú contextual Crear contenedores de blobs][0]
4. Aparecerá un cuadro de texto bajo hello **contenedores de blobs** carpeta. Escriba el nombre de hello para el contenedor de blob. Vea hello [las reglas de nomenclatura de contenedor](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sección para obtener una lista de reglas y restricciones en la nomenclatura de contenedores de blobs.

   ![Crear cuadro de texto Contenedores de blobs][1]
5. Presione **ENTRAR** cuando haya finalizado la toocreate contenedor de blobs de hello, o **Esc** toocancel. Una vez que se ha creado correctamente el contenedor de blob de hello, se mostrará en hello **contenedores de blobs** selecciona la carpeta para hello cuenta de almacenamiento.

   ![Contenedor de blobs creado][2]

## <a name="view-a-blob-containers-contents"></a>Visualización del contenido de un contenedor de blobs
Los contenedores de blobs contienen blobs y carpetas (que también contienen blobs).

Hello siguientes pasos muestran cómo contenido de hello tooview de un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea tooview.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Contenedor de blobs de hello contextual desea tooview y - en el menú contextual de hello: seleccione **abrir Editor de contenedor de Blob**.
   También puede hacer doble clic contenedor de blobs de hello desea tooview.

   ![Menú contextual Abrir editor de contenedor de blobs][19]
5. panel principal Hola mostrará el contenido del contenedor de blob de Hola.

   ![Editor de contenedor de blobs][3]

## <a name="delete-a-blob-container"></a>Eliminación de contenedores de blobs
Los contenedores de blobs se pueden crear fácilmente y eliminarse según sea necesario. (toosee cómo blobs toodelete individuales, consulte sección toohello, [administrar blobs en un contenedor de blobs](#managing-blobs-in-a-blob-container).)

Hello siguientes pasos muestran cómo toodelete un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea tooview.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Contenedor de blobs de hello contextual desea toodelete y - en el menú contextual de hello: seleccione **eliminar**.
   También puede presionar **eliminar** contenedor de toodelete Hola blob actualmente seleccionado.

   ![Menú contextual Eliminar contenedores de blobs][4]
5. Seleccione **Sí** toohello cuadro de diálogo de confirmación.

   ![Cuadro de diálogo de confirmación Eliminar contenedores de blobs][5]

## <a name="copy-a-blob-container"></a>Copia de un contenedor de blobs
Explorador de almacenamiento (vista previa) le permite toocopy un Portapapeles toohello de contenedor de blob y, a continuación, pegue que contenedor de blobs en otra cuenta de almacenamiento. (toosee cómo blobs toocopy individuales, consulte sección toohello, [administrar blobs en un contenedor de blobs](#managing-blobs-in-a-blob-container).)

Hola pasos ilustran toocopy un contenedor de blob desde el almacenamiento de una cuenta y cómo tooanother.

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea toocopy.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Contenedor de blobs de hello contextual desea toocopy y - en el menú contextual de hello: seleccione **contenedor de blobs de copia**.

   ![Menú contextual Copiar contenedor de blobs][6]
5. Haga clic en la cuenta de almacenamiento de destino"hello deseado" en la que desee toopaste contenedor de blobs de Hola y - en el menú contextual de hello: seleccione **contenedor de blobs de pegar**.

   ![Menú contextual Pegar contenedor de blobs][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Obtener Hola SAS para un contenedor de blobs
A [firma de acceso compartido (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) proporciona acceso delegado tooresources en su cuenta de almacenamiento.
Esto significa que puede conceder a que un cliente limitada tooobjects permisos en su cuenta de almacenamiento en un periodo de tiempo y con un conjunto especificado de permisos, sin tener que compartir claves de acceso de su cuenta.

Hello siguientes pasos muestran cómo toocreate una SAS para un contenedor de blobs:

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello para el que desea tooget una SAS.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Haga clic en el contenedor de blobs que se prefiera de Hola y - en el menú contextual de hello: seleccione **obtener firma de acceso compartido**.

   ![Menú contextual Obtener SAS][8]
5. Hola **firma de acceso compartido** cuadro de diálogo, especifique la directiva de hello, las fechas de inicio y finalización, zona horaria y tener acceso a niveles que desee para el recurso de Hola.

   ![Opciones de Obtener SAS][9]
6. Cuando haya terminado de especificar las opciones de SAS de hello, seleccione **crear**.
7. Un segundo **firma de acceso compartido** cuadro de diálogo, a continuación, mostrará que listas Hola contenedor de blobs junto con la dirección URL de Hola y cadenas que se puede usar tooaccess Hola recurso de almacenamiento.
   Seleccione **copia** siguiente dirección URL de toohello desea toocopy toohello Portapapeles.

   ![Copiar direcciones URL de SAS][10]
8. Cuando haya terminado, seleccione **Cerrar**.

## <a name="manage-access-policies-for-a-blob-container"></a>Administración de directivas de acceso para un contenedor de blobs
Hello siguientes pasos muestran cómo toomanage (agregar y quitar) las directivas para un contenedor de blobs de acceso:

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello cuyas directivas de acceso que se va toomanage.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Seleccionar contenedor de blobs deseado de Hola y - en el menú contextual de hello: seleccione **administrar directivas de acceso**.

   ![Menú contextual Administrar directivas de acceso][11]
5. Hola **las directivas de acceso** cuadro de diálogo mostrará una lista de las directivas de acceso creadas anteriormente para el contenedor de blob seleccionados Hola.

   ![Opciones de Directiva de acceso][12]        
6. Siga estos pasos dependiendo de la tarea de administración de directivas de acceso de Hola:

   * **Agregar una nueva directiva de acceso**: seleccione **Agregar**. Una vez generado, Hola **las directivas de acceso** cuadro de diálogo mostrará Hola recién agregado tener acceso a la directiva (con configuración predeterminada).
   * **Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.
   * **Quitar una directiva de acceso** : seleccione esta opción **quitar** siguiente directiva de acceso de toohello desea tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Establecer nivel de acceso público de hello en un contenedor de blob
De forma predeterminada, cada contenedor de blob se establece demasiado "Ningún acceso público".

Hello siguientes pasos muestran cómo toospecify un complemento público tiene acceso a nivel de un contenedor de blobs.

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello cuyas directivas de acceso que se va toomanage.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Seleccionar contenedor de blobs deseado de Hola y - en el menú contextual de hello: seleccione **establecer el nivel de acceso público**.

   ![Menú contextual Establecer nivel de acceso público][13]
5. Hola **establecer el nivel de acceso público de contenedor** cuadro de diálogo, especifique el nivel de acceso de hello deseado.

   ![Opciones de Establecer nivel de acceso público][14]
6. Seleccione **Aplicar**.

## <a name="managing-blobs-in-a-blob-container"></a>Administración de blobs de un contenedor de blobs
Una vez que ha creado un contenedor de blobs, puede cargar un contenedor de blobs de blob toothat, descargue un equipo local de blob tooyour, abrir un blob en el equipo local y mucho más.

Hola siguientes pasos muestra cómo toomanage Hola blobs (y carpetas) dentro de un contenedor de blob.

1. Abra el Explorador de almacenamiento (versión preliminar).
2. En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea toomanage.
3. Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.
4. Haga doble clic en el contenedor de blobs de hello desea tooview.
5. panel principal Hola mostrará el contenido del contenedor de blob de Hola.

   ![Ver contenedor de blobs][3]
6. panel principal Hola mostrará el contenido del contenedor de blob de Hola.
7. Siga estos que pasos dependiendo de la tarea hello desea tooperform:

   * **Cargar el contenedor de blobs de tooa de archivos**

     1. En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar archivos** desde el menú desplegable de Hola.

        ![Menú Cargar archivos][15]
     2. Hola **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **archivos** tooselect Hola archivos desea tooupload de cuadro de texto.

        ![Opciones de Cargar archivos][16]
     3. Especificar tipo de Hola de **tipo de Blob**. artículo de Hello [Introducción al almacenamiento de blobs de Azure mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) se explican las diferencias de hello entre Hola diversos tipos de blob.
     4. Si lo desea, especifique una carpeta de destino en la que se cargarán los archivos seleccionados de Hola. Si no existe la carpeta de destino de hello, se creará.
     5. Seleccione **Cargar**.
   * **Cargar un contenedor de blobs de tooa de carpeta**

     1. En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar carpeta** desde el menú desplegable de Hola.

        ![Menú Cargar carpeta][17]
     2. Hola **carga carpeta** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **carpeta** carpeta de Hola de tooselect de cuadro de texto cuyo contenido desea tooupload.

        ![Opciones de Cargar carpeta][18]
     3. Especificar tipo de Hola de **tipo de Blob**. artículo de Hello [Introducción al almacenamiento de blobs de Azure mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) se explican las diferencias de hello entre Hola diversos tipos de blob.
     4. Si lo desea, especifique una carpeta de destino en qué Hola se cargará el contenido de la carpeta seleccionada. Si no existe la carpeta de destino de hello, se creará.
     5. Seleccione **Cargar**.
   * **Descargar un equipo local de blob tooyour**

     1. Seleccione el blob de hello desea toodownload.
     2. En la barra de herramientas del panel principal de hello, seleccione **descargar**.
     3. Hola **especificar donde hello toosave descarga blob** cuadro de diálogo, especificar ubicación de Hola donde desea blob Hola descargó y Hola nombre que desee toogive se.  
     4. Seleccione **Guardar**.
   * **Abrir un blob en el equipo local**

     1. Seleccione el blob de hello desea tooopen.
     2. En la barra de herramientas del panel principal de hello, seleccione **abiertos**.
     3. blob de Hola se van a descargar y abre con la aplicación hello asociada con el tipo de archivo subyacente del blob de Hola.
   * **Copiar un Portapapeles toohello de blob**

     1. Seleccione el blob de hello desea toocopy.
     2. En la barra de herramientas del panel principal de hello, seleccione **copia**.
     3. En el panel izquierdo de hello, navegar por el contenedor de blobs de tooanother y haga doble clic tooview en el panel principal Hola.
     4. En la barra de herramientas del panel principal de hello, seleccione **pegar** toocreate una copia de blob de Hola.
   * **Eliminar un blob**

     1. Seleccione el blob de hello desea toodelete.
     2. En la barra de herramientas del panel principal de hello, seleccione **eliminar**.
     3. Seleccione **Sí** toohello cuadro de diálogo de confirmación.

## <a name="next-steps"></a>Pasos siguientes
* Hola de vista [notas de la versión de explorador de almacenamiento (versión preliminar) y los vídeos más recientes](http://www.storageexplorer.com).
* Obtenga información acerca de cómo demasiado[crear aplicaciones mediante Azure blobs, tablas, colas y archivos](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
