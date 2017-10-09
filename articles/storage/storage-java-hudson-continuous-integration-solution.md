---
title: aaaHow toouse Hudson con almacenamiento de blobs | Documentos de Microsoft
description: "Describe cómo toouse Hudson con almacenamiento de blobs de Azure como un repositorio para los artefactos de compilación."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: a23581e4b58526d2e9c936d4f75f6abdc407e27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>Uso del almacenamiento de Azure con una solución de integración continua Hudson
## <a name="overview"></a>Información general
Hello información siguiente muestra cómo utiliza el almacenamiento de blobs de toouse como un repositorio de artefactos de compilación creados por una solución de integración continua Hudson (CI), o como un origen de archivos descargables toobe en un proceso de compilación. Uno de los escenarios de Hola donde esto podría resultar útil es cuando el código se escribe en un entorno de desarrollo ágil (mediante Java u otros lenguajes), compilaciones se están ejecutando en función de la integración continua y necesitan un repositorio para los artefactos de compilación, por lo que se puede realizar , por ejemplo, compartirlos con otros miembros de la organización, los clientes, o mantener un archivo.  Otro escenario es cuando su propio trabajo de compilación requiere otros archivos, por ejemplo, toodownload de dependencias como parte del programa Hola a la entrada de generación.

En este tutorial va a usar Hola complemento de almacenamiento de Azure para CI Hudson facilitados por Microsoft.

## <a name="introduction-toohudson"></a>Introducción tooHudson
Habilita la integración continua Hudson de un proyecto de software al permitir que los desarrolladores tooeasily integrar sus cambios en el código y tienen compilaciones generados automáticamente y con frecuencia, lo que aumenta la productividad de Hola de desarrolladores de Hola. Compilaciones están con control de versiones y artefactos de compilación pueden ser repositorios toovarious cargado. Este artículo le mostrará cómo toouse almacenamiento de blobs de Azure como repositorio de Hola de hello artefactos de compilación. También se mostrará cómo las dependencias de toodownload de almacenamiento de blobs de Azure.

Puede encontrar más información acerca de Hudson en [Meet Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson).

## <a name="benefits-of-using-hello-blob-service"></a>Ventajas de usar el servicio de Blob de Hola
Ventajas de usar Hola Blob servicio toohost los artefactos de compilación de desarrollo ágil incluyen:

* Alta disponibilidad de sus artefactos de compilación o de sus dependencias descargables.
* Rendimiento si la solución de integración continua Hudson carga los artefactos de compilación
* Rendimiento si los clientes y socios descargan los artefactos de compilación
* Control sobre las directivas de acceso de usuarios, con una opción entre acceso anónimo, acceso compartido basado en expiración, acceso mediante firma, acceso privado, etc.

## <a name="prerequisites"></a>Requisitos previos
Se necesita Hola siguientes hello toouse servicio Blob con la solución de integración continua Hudson:

* Una solución de integración continua Hudson.
  
    Si actualmente no tiene una solución de integración continua Hudson, puede ejecutar una solución de integración continua Hudson mediante Hola después técnica:
  
  1. En un equipo habilitado para Java, descarga Hola Hudson WAR de <http://hudson-ci.org/>.
  2. En un símbolo del sistema que es la carpeta toohello abierto que contiene Hola Hudson WAR, ejecute hello Hudson WAR. Por ejemplo, si ha descargado la versión 3.1.2:
     
      `java -jar hudson-3.1.2.war`

  3. En el explorador, abra `http://localhost:8080/`. Se abrirá el panel Hudson Hola.
  4. Al usar primera Hudson, complete la instalación inicial de hello en `http://localhost:8080/`.
  5. Después de completar el programa de instalación inicial de hello, Cancelar Hola ejecutando la instancia de hello Hudson WAR, iniciar Hola Hudson WAR nuevo y vuelva a abrir Hola panel Hudson, `http://localhost:8080/`, que utilizará tooinstall y configurar el complemento de almacenamiento de Azure Hola.
     
      Mientras que una solución de integración continua Hudson típica se configuraría toorun como un servicio, ejecutando Hola war Hudson en línea de comandos de hello será suficiente para este tutorial.
* Una cuenta de Azure. Puede iniciar sesión en una cuenta de Azure en <http://www.azure.com>.
* Una cuenta de almacenamiento de Azure. Si ya no tiene una cuenta de almacenamiento, puede crear una siguiendo los pasos de hello en [crear una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account).
* Familiaridad con la solución de integración continua Hudson Hola se recomienda, aunque no necesario, como hello siguiente contenido usará un tooshow de ejemplo básica Hola pasos necesarios cuando se usa el servicio de Blob de hello como repositorio para la integración continua Hudson artefactos de compilación.

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>¿Cómo toouse Hola servicio Blob con integración continua Hudson
servicio de Blob de hello toouse con Hudson, necesitará tooinstall Hola complemento de almacenamiento de Azure, configurar Hola complemento toouse su cuenta de almacenamiento y, a continuación, crear una acción posterior a la compilación que carga la cuenta de almacenamiento de tooyour de artefactos de compilación. Estos pasos se describen en las secciones siguientes de Hola.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>¿Cómo tooinstall Hola complemento de almacenamiento de Azure
1. En el panel Hudson hello, haga clic en **administrar Hudson**.
2. En hello **administrar Hudson** página, haga clic en **administrar complementos**.
3. Haga clic en hello **disponible** ficha.
4. Haga clic en **Others**(Otros).
5. Hola **artefacto Uploaders** sección, seleccione **complemento de almacenamiento de Microsoft Azure**.
6. Haga clic en **Instalar**.
7. Una vez completada la instalación de hello, reinicie a Hudson.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>¿Cómo tooconfigure Hola toouse de complemento de almacenamiento de Azure a su cuenta de almacenamiento
1. En el panel Hudson hello, haga clic en **administrar Hudson**.
2. En hello **administrar Hudson** página, haga clic en **configurar el sistema**.
3. Hola **configuración de la cuenta de almacenamiento de Microsoft Azure** sección:
   
    a. Escriba el nombre de cuenta de almacenamiento, que puede obtener de hello [Portal de Azure](https://portal.azure.com).
   
    b. Escriba su clave de cuenta de almacenamiento, también puede obtenerse de hello [Portal de Azure](https://portal.azure.com).
   
    c. Utilizar valor predeterminado de Hola de **dirección URL del extremo de servicio de Blob** si usas la nube pública de Azure Hola. Si utilizas una nube de Azure diferentes, usar el punto de conexión de hello como Hola especificado en [Portal de Azure](https://portal.azure.com) para su cuenta de almacenamiento.
   
    d. Haga clic en **validar las credenciales de almacenamiento** toovalidate su cuenta de almacenamiento.
   
    e. [Opcional] Si tiene cuentas de almacenamiento adicional que desea que realizó tooyour disponible Hudson CI, haga clic en **agregar más cuentas de almacenamiento**.
   
    f. Haga clic en **guardar** toosave la configuración.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>¿Cómo toocreate una acción posterior a la compilación que carga la cuenta de almacenamiento de tooyour de artefactos de compilación
Con fines de instrucción, en primer lugar necesitaremos toocreate un trabajo que creará varios archivos y, a continuación, agregar en la cuenta de almacenamiento tooyour de hello acción posterior a la compilación tooupload Hola archivos.

1. En el panel Hudson hello, haga clic en **nuevo trabajo**.
2. Nombre de trabajo de hello **MyJob**, haga clic en **crear un trabajo de estilo libre software**y, a continuación, haga clic en **Aceptar**.
3. Hola **generar** sección de configuración del trabajo de hello, haga clic en **agregar el paso de compilación** y elija **Windows ejecutar el comando por lotes**.
4. En **comando**, usar hello siguientes comandos:

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. Hola **acciones posteriores a la compilación** sección de configuración del trabajo de hello, haga clic en **cargar el almacenamiento de blobs de Azure de artefactos tooMicrosoft**.
6. Para **nombre de la cuenta de almacenamiento**, seleccione Hola toouse de cuenta de almacenamiento.
7. Para **nombre del contenedor**, especifique el nombre del contenedor de Hola. (contenedor de Hola se creará si aún no existe cuando se cargan los artefactos de compilación de Hola.) Puede utilizar variables de entorno, por lo que en este ejemplo, escriba **${JOB_NAME}** como nombre de contenedor de Hola.
   
    **Sugerencia**
   
    A continuación hello **comando** sección donde se escribe un script para **Windows ejecutar el comando por lotes** es un vínculo de variables de entorno toohello reconocidas Hudson. Haga clic en los que se vinculan los nombres de variable de entorno toolearn hello y descripciones. Tenga en cuenta ese entorno de variables que contienen caracteres especiales, como hello **BUILD_URL** variable de entorno, no se permiten como un nombre de contenedor o la ruta de acceso virtual común.
8. Haga clic en **Make new container public by default** (Hacer público el nuevo contenedor de forma predeterminada) para este ejemplo. (Si desea que toouse un contenedor privado, deberá toocreate un acceso de tooallow de firma de acceso compartido. Que está más allá del ámbito de Hola de este artículo. Puede obtener más información sobre las firmas de acceso compartido en [Uso de Firma de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md)).
9. [Opcional] Haga clic en **limpia contenedor antes de cargar** si desea borra Hola contenedor toobe de contenido antes de cargarán los artefactos de compilación (dejarla desactivada si desea que el no tooclean Hola contenido del contenedor de hello).
10. Para **tooupload de lista de artefactos**, escriba  **texto /*.txt**.
11. En **Common virtual path for uploaded artifacts** (Ruta de acceso virtual común para artefactos cargados), escriba **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Haga clic en **guardar** toosave la configuración.
13. En el panel de Hudson hello, haga clic en **generar ahora** toorun **MyJob**. Examine la salida de la consola de hello para el estado. Mensajes de estado para el almacenamiento de Azure se incluirán en la salida de la consola de hello cuando inicia la acción posterior a la compilación de hello artefactos de compilación tooupload.
14. Tras la finalización correcta de trabajo de hello, puede examinar artefactos de compilación de hello abriendo blob público Hola.
    
    a. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).
    
    b. Haga clic en **Storage**(Almacenamiento).
    
    c. Haga clic en el nombre de cuenta de almacenamiento de Hola que utilizó para Hudson.
    
    d. Haga clic en **Containers**(Contenedores).
    
    e. Haga clic en el contenedor de hello denominado **myjob**, que es Hola versión en minúsculas del nombre de trabajo de Hola que asignó al crear trabajo de Hudson Hola. Los nombres de los contenedores y los nombres de los blobs se guardan en minúscula en el almacenamiento de Azure y, además, distinguen mayúsculas de minúsculas. En lista de Hola de blobs para el contenedor de hello denominado **myjob** verá **Hola.txt** y **date.txt**. Copiar dirección URL de Hola para cada uno de estos elementos y abrirlo en el explorador. Verá el archivo de texto de Hola que se cargó como un artefacto de compilación.

Solo una acción posterior a la compilación que carga los artefactos tooAzure almacenamiento de blobs puede crearse por trabajo. Tenga en cuenta que el almacenamiento de blobs de hello única acción posterior a la compilación tooupload artefactos tooAzure puede especificar distintos archivos (incluidos los caracteres comodín) y las rutas de acceso toofiles dentro de **tooupload de lista de artefactos** con un punto y coma como separador. Por ejemplo, si su Hudson compilación genera archivos TXT en el área de trabajo y archivos JAR **generar** carpeta y desea tooupload ambos tooAzure almacenamiento de blobs, utilice el siguiente de Hola para hello **toouploaddelistadeartefactos** valor: **compilar /\*.jar; compilación /\*.txt**. También puede utilizar la sintaxis de dos puntos dobles toospecify un toouse de ruta de acceso dentro del nombre de blob de Hola. Por ejemplo, si desea Hola archivos JAR tooget cargado mediante **archivos binarios** en la ruta de acceso de blob de Hola y Hola TXT archivos tooget cargados mediante **avisos** en la ruta de acceso de blob de hello, utilice el siguiente de Hola para hello  **Lista de tooupload artefactos** valor: **compilar /\*. jar::binaries; compilación /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>¿Cómo toocreate un paso de compilación que descarga desde el almacenamiento de blobs de Azure
Hola siguientes pasos muestra cómo tooconfigure una compilación paso elementos toodownload desde el almacenamiento de blobs de Azure. Esto resultaría útil si desea tooinclude elementos en la compilación, por ejemplo, archivos JAR que mantiene en el almacenamiento de blobs de Azure.

1. Hola **generar** sección de configuración del trabajo de hello, haga clic en **agregar el paso de compilación** y elija **descargar desde el almacenamiento de blobs de Azure**.
2. Para **nombre de la cuenta de almacenamiento**, seleccione Hola toouse de cuenta de almacenamiento.
3. Para **nombre del contenedor**, especifique el nombre de Hola Hola del contenedor de que tiene blobs Hola desea toodownload. Puede usar variables de entorno.
4. Para **nombre de Blob**, especifique el nombre de blob de Hola. Puede usar variables de entorno. Además, puede usar un asterisco como carácter comodín después de especificar Hola inicial o las letras del nombre de blob de Hola. Por ejemplo, **project\*** especificaría todos los blobs cuyos nombres comiencen por **project**.
5. [Opcional] Para **ruta de acceso de descarga**, especifique la ruta de acceso de hello en hello máquina Hudson donde desea toodownload archivos desde el almacenamiento de blobs de Azure. También se pueden usar variables de entorno. (Si no proporciona un valor para **ruta de acceso de descarga**, Hola desde el almacenamiento de blobs de Azure se generarán área de trabajo del trabajo descargado toohello.)

Si tiene elementos adicionales que desee toodownload desde el almacenamiento de blobs de Azure, puede crear pasos de compilación adicionales.

Después de ejecutar una compilación, puede comprobar Hola generar salida de la consola de historial o vistazo a la ubicación de descarga, toosee si Hola blobs que esperaba que se descargaron correctamente.

## <a name="components-used-by-hello-blob-service"></a>Componentes utilizados por hello servicio Blob
siguiente Hola proporciona una visión general de los componentes del servicio de Blob de Hola.

* **Cuenta de almacenamiento**: todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Se trata de un nivel más alto de Hola de espacio de nombres de hello para tener acceso a blobs. Una cuenta puede contener una cantidad ilimitada de contenedores, siempre que su tamaño total no supere los 100 TB.
* **Contenedor**: un contenedor proporciona una agrupación de un conjunto de blobs. Todos los blobs deben residir en un contenedor. Además, una cuenta puede disponer de un número ilimitado de contenedores y un contenedor puede almacenar un número ilimitado de blobs.
* **Blob**: archivo de cualquier tipo y tamaño. Existen dos tipos de blobs que pueden almacenarse en Almacenamiento de Azure: blobs en páginas y en bloques. La mayoría de los archivos son blobs en bloques. Un blob en bloques solo pueden funcionar too200 GB de tamaño. En este tutorial se usan blobs en bloques. Blobs en páginas, otro tipo de blob, pueden ser hasta too1 TB en tamaño y son más eficaces cuando los intervalos de bytes en un archivo se modifican con frecuencia. Para más información sobre los blobs, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato de dirección URL**: los Blobs son direccionables mediante Hola siguiendo el formato de dirección URL:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (formato de hello anterior aplica a la nube pública de Azure toohello. Si utilizas una nube de Azure diferente, use el extremo de hello dentro de hello [Portal de Azure](https://portal.azure.com) toodetermine el punto de conexión de dirección URL.)
  
    En formato de hello anterior, `storageaccount` representa Hola nombre de la cuenta de almacenamiento `container_name` representa Hola nombre del contenedor, y `blob_name` representa Hola nombre de los blob, respectivamente. En nombre del contenedor de hello, puede tener varias rutas de acceso, separadas por una barra diagonal,  **/** . nombre de contenedor de ejemplo de Hola en este tutorial era **MyJob**, y **${compilar\_Id. de} / ${compilar\_número}** se usó para hello comunes ruta de acceso virtual resultante en hello blob que tiene un Dirección URL de hello siguiente forma:
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>Pasos siguientes
* [Presentación de Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [SDK de almacenamiento de Azure para Java](https://github.com/azure/azure-storage-java)
* [Referencia del SDK de cliente de almacenamiento de Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API de REST de servicios de Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Para obtener más información, consulte también hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).
