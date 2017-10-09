---
title: aaaBrowsing y administrar recursos de almacenamiento con el Explorador de servidores | Documentos de Microsoft
description: "Exploración y administración de recursos de almacenamiento con el Explorador de servidores"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Exploración y administración de recursos de almacenamiento con el Explorador de servidores
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Información general
Si ha instalado hello Azure Tools para Microsoft Visual Studio, puede ver blob, cola y datos de la tabla de las cuentas de almacenamiento de Azure. nodo de almacenamiento de Azure de Hello en el Explorador de servidores muestra datos que se estén en la cuenta del emulador de almacenamiento local y las demás cuentas de almacenamiento de Azure.

Elija tooview Explorador de servidores en Visual Studio, en la barra de menús de hello, **vista**, **Explorador de servidores**. nodo de almacenamiento de Hello muestra todas las cuentas de almacenamiento de Hola que existen en cada suscripción/certificados de Azure que está conectado a. Si no aparece la cuenta de almacenamiento, puede agregarlo siguiendo las instrucciones de hello [más adelante en este tema](#add-storage-accounts-by-using-server-explorer).

A partir de Azure SDK 2.7, también puede usar Hola nuevo explorador de nube tooview y administrar los recursos de Azure. Consulte [Administración de recursos de Azure con Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) para obtener más información.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Visualización y administración de recursos de almacenamiento en Visual Studio
El Explorador de servidores muestra automáticamente una lista de blobs, colas y tablas en la cuenta del emulador de almacenamiento. cuenta del emulador de almacenamiento Hola aparece en el Explorador de servidores en el nodo de almacenamiento de hello como hello **desarrollo** nodo.

recursos de la cuenta del emulador de almacenamiento Hola de toosee, expanda hello **desarrollo** nodo. Si no se ha iniciado el emulador de almacenamiento de Hola cuando se expande Hola **desarrollo** nodo, se iniciará automáticamente. Esto puede tardar varios segundos. Puede continuar toowork en otras áreas de Visual Studio mientras se inicia el emulador de almacenamiento de Hola.

recursos tooview en una cuenta de almacenamiento, expandir nodo de la cuenta de almacenamiento de hello en el Explorador de servidores. aparece Hola siguientes subnodos:

* Blobs
* Colas
* Tablas

## <a name="work-with-blob-resources"></a>Trabajo con recursos de blob
nodo de Blobs de Hello muestra una lista de contenedores de la cuenta de almacenamiento de hello seleccionado. Los contenedores de blobs incluyen archivos de blob, y puede organizar estos blobs en carpetas y subcarpetas. Vea [cómo toouse almacenamiento de blobs en .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) para obtener más información.

### <a name="toocreate-a-blob-container"></a>toocreate un contenedor de blobs
1. Menú contextual abierto Hola Hola **Blobs** nodo y, a continuación, elija **crear contenedor de blobs**.
2. Hola **crear contenedor de blobs** diálogo cuadro, escriba el nombre de Hola de nuevo contenedor de Hola.  
3. Presione **ENTRAR** en el teclado o se puede, haga clic o toque fuera de contenedor de blobs de hello nombre campo toosave Hola.
   
   > [!NOTE]
   > nombre del contenedor de blob de Hello debe comenzar con una letra minúscula (a-z) o un número (0-9).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete un contenedor de blobs
* Menú contextual de hello abierta para el contenedor de blobs de hello desee tooremove y, a continuación, elija **eliminar**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay una lista de elementos de hello contenidos en un contenedor de blobs
* Abra el menú contextual de Hola para un nombre de contenedor de blob de lista de hello y, a continuación, elija **abiertos**.
  
    Cuando se ve el contenido de Hola de un contenedor de blobs, aparece en una ficha llamada vista del contenedor de blob de Hola.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Puede realizar hello las siguientes operaciones en blobs mediante los botones de hello en la esquina superior derecha de Hola de vista del contenedor de blob de hello:
  
  * Escribir un valor de filtro y aplicarlo
  * Actualizar lista de Hola de blobs en el contenedor de Hola
  * Cargar un archivo
  * Eliminar un blob
    
    > [!NOTE]
    > Eliminar un archivo desde un contenedor de blobs no elimina el archivo subyacente hello; solo quita del contenedor de blob de Hola.
    > 
    > 
  * Abrir un blob
  * Guardar un equipo local de blob toohello

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate una carpeta o subcarpeta en un contenedor de blobs
1. Elegir contenedor de blobs de hello en el explorador en la nube. En la ventana de contenedor de hello, elija hello **cargar Blob** botón.
   
    ![Cargar un archivo en una carpeta de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. Hola **cargar archivo nuevo** diálogo cuadro, elija hello **examinar** archivo de hello toospecify del botón que desee tooupload y, a continuación, escriba un nombre de carpeta en hello **carpeta (opcional)** cuadro .
   
    Puede agregar subcarpetas en carpetas de contenedor siguiendo Hola mismo procedimiento. Si no especifica un nombre de carpeta, archivo hello será cargado toohello de nivel superior del contenedor de blob de Hola. archivo Hello aparece en la carpeta especificada de hello en el contenedor de Hola.
   
    ![Agregar carpeta tooa contenedor de blobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Haga doble clic en la carpeta de Hola o presione ENTRAR contenido de hello toosee de carpeta Hola. Cuando esté en la carpeta del contenedor de hello, puede navegar toohello atrás raíz del contenedor de hello eligiendo hello **Abrir directorio principal** (flecha arriba) botón.

### <a name="toodelete-a-container-folder"></a>toodelete una carpeta de contenedor
* Eliminar todos los archivos de hello en carpeta Hola
  
  > [!NOTE]
  > Dado que las carpetas en contenedores de blobs son carpetas virtuales, no se puede crear una carpeta vacía ni puede eliminar una carpeta toodelete su contenido del archivo. Tener contenido completo de hello toodelete de una carpeta de hello toodelete de carpeta.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter blobs en un contenedor
Puede filtrar los blobs de Hola que se muestran especificando un prefijo común.

Por ejemplo, si escribe el prefijo de hello `hello` en Hola cuadro de texto de filtro y, a continuación, elija hello **Execute** (**!**) aparecen en el botón, solo los blobs que comienzan con "hello".

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> campo de filtro de Hello distingue mayúsculas de minúsculas y no permite filtrar con caracteres comodín. Los blobs solo se pueden filtrar por prefijo. prefijo de Hello puede incluir un delimitador si usas un BLOB de tooorganize delimitador en una jerarquía virtual. Por ejemplo, el filtrado en Hola prefijo HelloFabric / devuelve todos los blobs que comienzan con esa cadena.
> 
> 

### <a name="toodownload-blob-data"></a>datos de blob toodownload
* En **Explorer nube**, abra el menú contextual de Hola de uno o más blobs y, a continuación, elija **abrir**, o elegir nombre de blob de hello y, a continuación, elija hello **abrir** botón, o haga doble clic en nombre de blob de Hola.
  
    Hola el progreso de una descarga de blobs aparece en hello **Azure Activity Log** ventana.
  
    Hola blob se abre en el editor de hello predeterminado para ese tipo de archivo. Si el sistema operativo de hello reconoce el tipo de archivo de hello, abre el archivo hello en una aplicación instalada localmente; en caso contrario, se le pedirá una aplicación que sea adecuada para el tipo de archivo de Hola de blob de hello toochoose. archivo local Hello que se crea cuando se descarga un blob se marca como de solo lectura.
  
    Los datos de BLOB es almacenadas localmente en caché y rebasa Hola de última hora de modificación del blob en hello servicio Blob. Si se ha actualizado el blob de Hola desde última se descargó, se descargará otra vez; en caso contrario, se cargará el blob de Hola desde el disco local de Hola. De forma predeterminada, un blob es el directorio temporal tooa descargado. directorio específico de tooa de toodownload blobs, menú contextual abierto Hola Hola seleccionado nombres de blob y elija **Guardar como**. Cuando se guarda un blob de esta manera, no se abre el archivo de blob de hello y archivo local Hola se crea con atributos de lectura y escritura.

### <a name="tooupload-blobs"></a>blobs tooupload
* Elija hello **cargar Blob** botón cuando se abre para su visualización en la vista de contenedor de blob de hello contenedor Hola.
  
    Puede elegir uno o más tooupload de archivos y se pueden cargar archivos de cualquier tipo. Hola **Azure Activity Log** muestra Hola progreso de carga de Hola. Para obtener más información acerca de cómo toowork con datos de blob, vea [cómo toouse Hola servicio de almacenamiento de blobs de Azure en .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>los registros de tooview transfieren tooblobs
* Si está usando datos de diagnósticos de Azure toolog desde su aplicación de Azure y se ha transferido la cuenta de almacenamiento de registros tooyour, podrá ver contenedores creados por Azure para estos registros. Ver estos registros en el Explorador de servidores es un problemas de tooidentify de manera sencilla de su aplicación, especialmente si se han implementado tooAzure. Para obtener más información sobre Diagnósticos de Azure, vea [Recopilar datos de registro mediante Diagnósticos de Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>dirección URL de hello tooget para un blob
* Abra el menú contextual del blob de hello y, a continuación, elija **Copiar dirección URL**.

### <a name="tooedit-a-blob"></a>tooedit un blob
* Seleccionar Hola blob y, a continuación, elija hello **abrir Blob** botón.
  
    archivo Hello es la ubicación temporal tooa descargado y abiertos en el equipo local de Hola. Debe volver a cargar blob Hola después de realizar cambios.

## <a name="work-with-queue-resources"></a>Trabajo con recursos de cola
Las colas de servicios de almacenamiento se hospedan en una cuenta de almacenamiento de Azure y se puede usar tooallow su toocommunicate de roles de servicio de nube entre sí y con otros servicios mediante un mecanismo de paso de mensajes. Cola de hello puede tener acceso mediante programación a través de un servicio de nube y a través de un servicio web para los clientes externos. También puede tener acceso a la cola Hola directamente si usa el Explorador de servidores en Visual Studio.

Al desarrollar un servicio de nube que usa colas, podría desea toocreate colas de toouse Visual Studio y trabajar con ellos de forma interactiva mientras desarrolla y probar el código.

En el Explorador de servidores, puede ver las colas de hello en una cuenta de almacenamiento, crear y eliminar colas, abrir una cola tooview sus mensajes y agregar la cola de mensajes tooa. Cuando se abre una cola para su visualización, puede ver los mensajes individuales de Hola y puede realizar Hola siguientes acciones en cola hello mediante los botones de hello en la esquina superior izquierda de hello:

* Actualizar vista Hola de cola de Hola
* Agregar una cola de mensajes toohello
* Eliminación de cola de mensajes de bienvenida del nivel superior
* Cola de hello Borrar todo

Hola siguiente imagen muestra una cola que contiene dos mensajes.

![Ver una cola](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Para obtener más información sobre el almacenamiento de servicios de colas, consulte [Cómo: Hola usar servicio de almacenamiento cola](http://go.microsoft.com/fwlink/?LinkID=264702). Para obtener información acerca del servicio web de Hola para colas de servicios de almacenamiento, consulte [conceptos del servicio cola](http://go.microsoft.com/fwlink/?LinkId=264788). Para obtener información acerca de cómo toosend mensajes tooa de servicios de almacenamiento cola mediante Visual Studio, vea [tooa cola de servicios de almacenamiento de información de envío de mensajes](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Las colas de servicios de almacenamiento son distintas de las colas del Bus de servicio. Para obtener más información sobre las colas del Bus de servicio, consulte Colas, temas y suscripciones del Bus de servicio.
> 
> 

## <a name="work-with-table-resources"></a>Trabajo con recursos de tabla
Hola servicio de almacenamiento de tabla de Azure almacena grandes cantidades de datos estructurados. servicio de Hello es autenticado de un almacén de datos NoSQL que acepta llamadas de dentro y fuera de hello nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.

### <a name="toocreate-a-table"></a>toocreate una tabla
1. En el explorador en la nube, seleccione hello **tablas** nodo de almacenamiento de saludo de la cuenta y, a continuación, elija **Create Table**.
2. Hola **Create Table** diálogo cuadro, escriba un nombre para la tabla de Hola.

### <a name="tooview-table-data"></a>datos de la tabla de tooview
1. En el Explorador de nube, abra hello **Azure** nodo y, a continuación, abra hello **almacenamiento** nodo.
2. Nodo de cuenta de almacenamiento abierto Hola que está interesado en y, a continuación, abra hello **tablas** nodo toosee una lista de tablas para la cuenta de almacenamiento de Hola.
3. Abra el menú contextual de Hola para una tabla y, a continuación, elija **ver tabla**.
   
    ![Una tabla de Azure en el Explorador de soluciones](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

tabla de Hola se organiza por entidades (mostradas en filas) y propiedades (mostradas en columnas). Por ejemplo, hello sigue en la ilustración muestra entidades en hello **Diseñador de tablas**:

### <a name="tooedit-table-data"></a>datos de la tabla de tooedit
1. Hola **Diseñador de tablas**, abra el menú contextual de Hola para una entidad (una única fila) o una propiedad (una única celda) y, a continuación, elija **editar**.
   
    ![Agregar o editar una entidad de tabla](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Las entidades de una sola tabla no son hello toohave necesario mismo conjunto de propiedades (columnas). Tenga en hello cuenta después de las restricciones sobre cómo ver y editar datos de la tabla.
   
   * No se pueden ver ni editar datos binarios (tipo byte[]), pero se pueden almacenar en una tabla.
   * No se puede editar hello **PartitionKey** o **RowKey** valores, porque el almacenamiento de tabla en Azure no admite esa operación.
   * No se puede crear una propiedad denominada Timestamp; los servicios de Almacenamiento de Azure usan una propiedad con ese nombre.
   * Si especifica un valor de fecha y hora, debe seguir un formato que es la configuración de región e idioma toohello adecuados de su equipo (por ejemplo, MM/DD/AAAA HH [AM | PM] para EE. UU. de Estados Unidos).

### <a name="tooadd-entities"></a>entidades de tooadd
1. Hola **Diseñador de tablas**, elija hello **Agregar entidad** botón.
   
    ![Agregar entidad](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. Hola **Agregar entidad** diálogo cuadro, escriba los valores de hello de hello **PartitionKey** y **RowKey** propiedades.
   
    ![Cuadro de diálogo Agregar entidad](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Escriba los valores de hello con cuidado porque no se puede cambiar después de cerrar el cuadro de diálogo de Hola a menos que elimina entidad hello y agregarlo de nuevo.

### <a name="toofilter-entities"></a>entidades de toofilter
Puede personalizar el conjunto de Hola de entidades que aparecen en una tabla si utiliza el generador de consultas de Hola.

1. Generador de consultas de hello tooopen, abra una tabla para verla.
2. Elija el botón del generador de consultas de hello en la barra de herramientas de la vista de tabla de Hola.
   
    Hola **generador de consultas** aparece el cuadro de diálogo. Hello en la ilustración siguiente se muestra una consulta que se va a compilar en el generador de consultas de Hola.
   
    ![Generador de consultas](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Cuando haya terminado generar consulta de hello, cierre el cuadro de diálogo de Hola. formato de texto resultante de Hola de consulta de hello aparece en un cuadro de texto como un filtro de WCF Data Services.
4. Hola toorun de consulta, elija el icono de triángulo verde Hola.
   
    También puede filtrar los datos de la entidad que aparece en hello **Diseñador de tablas** si escribe una cadena de filtro de WCF Data Services directamente en el campo de filtro de Hola. Este tipo de cadena es similar tooa cláusula WHERE de SQL, pero se envía toohello server como una solicitud HTTP. Para obtener información acerca de cómo tooconstruct cadenas de filtro, vea [construir cadenas de filtro para el Diseñador de tablas de hello](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Hello en la ilustración siguiente se muestra un ejemplo de una cadena de filtro válida:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Actualización de los datos de almacenamiento
Cuando el Explorador de servidores se conecta tooor obtiene los datos de una cuenta de almacenamiento, podría tardar hasta tooa minuto para hello operación toocomplete. Si no puede conectarse, la operación de hello podría tiempo de espera. Mientras se recuperan los datos, puede continuar toowork en otras partes de Visual Studio. operación de hello toocancel si tarda demasiado, elija hello **Detener actualización** botón de barra de herramientas del explorador de servidores Hola.

#### <a name="toorefresh-blob-container-data"></a>datos del contenedor de blob toorefresh
* Seleccione hello **Blobs** nodo secundario **almacenamiento** y elija hello **actualizar** botón de barra de herramientas del explorador de servidores Hola.
* lista de hello toorefresh de blobs que aparece, elija hello **Execute** botón.

#### <a name="toorefresh-table-data"></a>datos de la tabla de toorefresh
* Seleccione hello **tablas** nodo secundario **almacenamiento** y elija hello **actualizar** botón.
* lista de hello toorefresh de entidades que se muestra en hello **Diseñador de tablas**, elija hello **Execute** botón en hello **Diseñador de tablas**.

#### <a name="toorefresh-queue-data"></a>datos de la cola de toorefresh
* Seleccione hello **colas** nodo y, a continuación, elija hello **actualizar** botón.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh todos los elementos de una cuenta de almacenamiento
* Elija el nombre de la cuenta de hello y, a continuación, elija hello **actualizar** botón de barra de herramientas de hello para el Explorador de servidores.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Adición de cuentas de almacenamiento mediante el Explorador de servidores
Hay dos maneras de cuentas de almacenamiento tooadd utilizando el Explorador de servidores. Puede crear una nueva cuenta de almacenamiento en su suscripción de Azure o puede asociar una cuenta de almacenamiento existente.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate una nueva cuenta de almacenamiento mediante el Explorador de servidores
1. En el Explorador de servidores, abra el acceso directo de hello para el nodo de almacenamiento de hello y, a continuación, elija crear cuenta de almacenamiento.
   
    ![Crear una nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Seleccione o escriba Hola siguiente información para la nueva cuenta de almacenamiento Hola Hola **crear cuenta de almacenamiento** cuadro de diálogo.
   
   * Hola toowhich de suscripción de Azure que desee cuenta de almacenamiento de tooadd Hola.
   * nombre de Hola que desea toouse Hola nueva cuenta de almacenamiento.
   * región de Hola o grupo de afinidad (por ejemplo, oeste de Estados Unidos o Asia oriental).
   * Hola tipo de replicación que desea toouse Hola cuenta de almacenamiento, por ejemplo, con redundancia geográfica.
3. Seleccione **Create**.
   
    Hola nueva cuenta de almacenamiento aparece en hello **almacenamiento** lista en el Explorador de soluciones.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach una cuenta de almacenamiento existente mediante el Explorador de servidores
1. En el Explorador de servidores, abra el acceso directo de hello para el nodo de almacenamiento de Azure de hello y, a continuación, elija **adjuntar almacenamiento externo**.
   
    ![Agregar una cuenta de almacenamiento existente](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Seleccione o escriba Hola siguiente información para la nueva cuenta de almacenamiento Hola Hola **crear cuenta de almacenamiento** cuadro de diálogo.
   
   * nombre de Hola de cuenta Hola de almacenamiento existente que desee tooattach. Puede escribir un nombre o selecciónelo en la lista de Hola.
   * clave de Hola para saludo seleccionado cuenta de almacenamiento. Este valor normalmente se proporciona automáticamente cuando se selecciona una cuenta de almacenamiento. Si desea que la clave de cuenta de almacenamiento de Visual Studio tooremember hello, active la casilla de clave de cuenta de recordar de Hola.
   * Hola protocolo toouse tooconnect toohello cuenta de almacenamiento, como HTTP, HTTPS o un extremo personalizado. Vea [cómo las cadenas de conexión de tooConfigure](https://msdn.microsoft.com/library/azure/ee758697.aspx) para obtener más información sobre los extremos personalizados.

### <a name="tooview-hello-secondary-endpoints"></a>extremos secundarios de hello tooview
* Si ha creado una cuenta de almacenamiento mediante hello **redundancia geográfica con acceso de lectura** opción de replicación, puede ver sus extremos secundarios. Abra el acceso directo de Hola Hola nombre de cuenta y, a continuación, elija **propiedades**.
  
    ![Extremos secundarios de almacenamiento](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove una cuenta de almacenamiento desde el Explorador de servidores
* En el Explorador de servidores, abra el acceso directo de Hola Hola nombre de cuenta y, a continuación, elija **eliminar**. Si elimina una cuenta de almacenamiento, también se quita cualquier información de clave guardada para esa cuenta.
  
  > [!NOTE]
  > Si elimina una cuenta de almacenamiento desde el Explorador de servidores, no afecta a la cuenta de almacenamiento ni los datos que contiene; simplemente se quita la referencia de Hola de explorador de servidores. toopermanently eliminar una cuenta de almacenamiento, use hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de cómo usar los servicios de almacenamiento de Azure, consulte [acceso a los servicios de almacenamiento de Azure de hello](https://msdn.microsoft.com/library/azure/ee405490.aspx).

