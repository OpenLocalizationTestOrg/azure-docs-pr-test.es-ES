---
title: aaaDevelop localmente con hello Azure Cosmos DB emulador | Documentos de Microsoft
description: "Hola emulador de base de datos de Azure Cosmos puede desarrollar y probar la aplicación localmente para forma gratuita, sin necesidad de crear una suscripción de Azure."
services: cosmos-db
documentationcenter: 
keywords: Emulador de Azure Cosmos DB
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Usar hello Azure Cosmos DB emulador para desarrollo local y las pruebas

<table>
<tr>
  <td><strong>Archivos binarios</strong></td>
  <td>[Descargar MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker Hub](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Origen de Docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure Cosmos DB emulador proporciona un entorno local que emula Hola servicio de base de datos de Azure Cosmos para fines de desarrollo. Hola emulador de base de datos de Azure Cosmos puede desarrollar y probar su aplicación localmente, sin crear una suscripción de Azure o incurrir en los costos. Cuando esté satisfecho con cómo funciona la aplicación en el emulador de base de datos de Azure Cosmos hello, puede cambiar una cuenta de base de datos de Azure Cosmos en nube de hello toousing.

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Instalar Hola emulador
> * Hola ejecución emulador en Docker para Windows
> * Autenticación de solicitudes
> * Uso de hello Explorador de datos en hello emulador
> * Exportación de certificados SSL
> * Llamar a Hola emulador desde línea de comandos de Hola
> * Recopilación de archivos de seguimiento

Se recomienda introducción, inspeccionando Hola después de vídeo, donde se muestra cómo tooget partió hello Azure Cosmos DB emulador Kirill Gavrylyuk. Tenga en cuenta que vídeo Hola hace referencia toohello emulador como Hola emulador de documentos, pero se ha cambiado el nombre de la propia herramienta de Hola Hola Azure Cosmos DB emulador desde punteando en vídeo de Hola. Toda la información de vídeo hello es precisa para hello Azure Cosmos DB emulador. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Cómo funciona la Hola emulador
Hola emulador de base de datos de Azure Cosmos proporciona una emulación de alta fidelidad del servicio de base de datos de Azure Cosmos Hola. Admite una funcionalidad idéntica a la de Azure Cosmos DB, incluida la compatibilidad con la creación y la consulta de documentos JSON, el aprovisionamiento y el escalado de colecciones y la ejecución de procedimientos y desencadenadores almacenados. Puede desarrollar y probar las aplicaciones que usan el emulador de base de datos de Azure Cosmos hello e implementarlos tooAzure a escala global realizando simplemente una sola configuración cambiar toohello extremo de la conexión de base de datos de Azure Cosmos.

Mientras se crea una emulación local de alta fidelidad del servicio de base de datos de Azure Cosmos real de hello, implementación de Hola de hello Azure Cosmos DB emulador es diferente del servicio de Hola. Por ejemplo, hello Azure Cosmos DB emulador usa componentes del sistema operativo estándares, como sistema de archivos local de hello para la persistencia y la pila del protocolo HTTPS para la conectividad. Esto significa que alguna funcionalidad que se basa en la infraestructura de Azure como replicación global, latencia de milisegundos de un solo dígito para lectura/escritura y niveles de coherencia de los no están disponibles a través de hello Azure Cosmos DB emulador.

> [!NOTE]
> En este Hola Explorador de datos de tiempo en hello emulador solo admite la creación de hello de colecciones de API de documentos y MongoDB. Hola Explorador de datos en el emulador de hello no admite actualmente la creación de hello de tablas y gráficos. 

## <a name="system-requirements"></a>Requisitos del sistema
Hola emulador de base de datos de Azure Cosmos tiene Hola según los requisitos de hardware y software:

* Requisitos de software
  * Windows Server 2012 R2, Windows Server 2016 o Windows 10
*   Requisitos mínimos de hardware
  * 2 GB DE RAM
  * 10 GB de espacio disponible en disco duro

## <a name="installation"></a>Instalación
Puede descargar e instalar hello Azure Cosmos DB emulador de hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, configurar y ejecutar el emulador de base de datos de Azure Cosmos hello, debe tener privilegios administrativos en el equipo de Hola.

## <a name="running-on-docker-for-windows"></a>Ejecución en Docker para Windows

Hola emulador de Azure Cosmos DB se puede ejecutar en Docker para Windows. Hola emulador no funciona en Docker para Oracle Linux.

Una vez que tenga [Docker para Windows](https://www.docker.com/docker-windows) instalado, se puede extraer de imagen del emulador Hola de Docker Hub ejecutando el siguiente comando desde el shell de favoritos de Hola (cmd.exe, PowerShell, etcetera.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
imagen de hello toostart, ejecute hello siga los comandos.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

respuesta de Hello tiene un aspecto similar siguiente toohello:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Cierre Hola shell interactiva cuando se ha iniciado el emulador de hello va contenedor del emulador de apagado Hola.

Use punto de conexión de Hola y de clave maestra en el de respuesta de hello en el cliente e importe el certificado SSL de hello en el host. Hola tooimport certificado SSL, Hola siguiente desde un símbolo del sistema de administración:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Iniciar el emulador de Hola

Hola toostart emulador de base de datos de Azure Cosmos, seleccione el botón de inicio de Hola o presione la tecla de Windows hello. Comience a escribir **emulador de base de datos de Azure Cosmos**y seleccione Hola emulador de lista de Hola de aplicaciones. 

![Seleccione Hola o presionen Hola Windows clave de inicio, comience a escribir ** Azure Cosmos DB emulador ** y seleccione Hola emulador de lista de Hola de aplicaciones](./media/local-emulator/database-local-emulator-start.png)

Cuando se ejecuta el emulador de hello, verá un icono en el área de notificación de barra de tareas de Windows hello. ![Notificación en la barra de tareas del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

Hola emulador de base de datos de Azure Cosmos de forma predeterminada se ejecuta en máquina local de hello ("localhost") escuchando en el puerto 8081.

Hello Azure Cosmos DB emulador instala predeterminado toohello `C:\Program Files\Azure Cosmos DB Emulator` directory. También puede iniciar y detener el emulador de Hola desde Hola de línea de comandos. Vea la [referencia de la herramienta de la línea de comandos](#command-line) para obtener más información.

## <a name="start-data-explorer"></a>Inicio del Explorador de datos

Cuando se inicia el emulador de base de datos de Azure Cosmos Hola abrirá automáticamente Hola Explorador de datos de base de datos de Azure Cosmos en el explorador. dirección de Hello aparecerá como [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Si cerrar Hola explorador y desearía toore abierto más adelante, puede abrir dirección URL de hello en el explorador o iniciarlo desde hello Azure Cosmos DB emulador en el icono de la Bandeja de Windows hello, tal y como se muestra a continuación.

![Iniciador del Explorador de datos del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Búsqueda de actualizaciones
En el Explorador de datos se indica si hay una nueva actualización disponible para descarga. 

> [!NOTE]
> Datos que se crean en una versión de hello Azure Cosmos DB emulador no está garantizados toobe accesible cuando se usa una versión diferente. Si necesita toopersist los datos para a largo plazo de hello, se recomienda que almacene esos datos en una cuenta de base de datos de Azure Cosmos, en lugar de hello Azure Cosmos DB emulador. 

## <a name="authenticating-requests"></a>Autenticación de solicitudes
Al igual que con la base de datos de Azure Cosmos en nube de hello, todas las solicitudes que se realizan con hello Azure Cosmos DB emulador deben autenticarse. Hola emulador de base de datos de Azure Cosmos admite una cuenta única fija y una clave de autenticación conocido para la autenticación de clave maestra. Esta cuenta y clave son Hola únicas credenciales permitidas para su uso con hello Azure Cosmos DB emulador. Son las siguientes:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> clave maestra de Hello admitido hello Azure Cosmos DB emulador está pensado para uso únicamente con el emulador de Hola. No puede usar su cuenta de base de datos de Azure Cosmos de producción y la clave con hello Azure Cosmos DB emulador. 

> [!NOTE] 
> Si ha iniciado el emulador de hello con hello opción/Key, a continuación, usar la clave de hello generado en lugar de "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Además, al igual que el servicio de base de datos de Azure Cosmos, hello Azure Cosmos DB emulador Hola admite solo una comunicación segura mediante SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Emulador en ejecución hello en una red local

Puede ejecutar el emulador de hello en una red local. tooenable acceso a la red, especifique la opción de /AllowNetworkAccess hello en hello [línea de comandos](#command-line-syntax), que también requiere que especifique/Key = key_string o/keyfile = nombre_archivo. Puede usar /GenKeyFile = nombre_archivo toogenerate un archivo con una clave aleatoria por adelantado.  A continuación, puede pasar dicho demasiado/KeyFile = nombre_archivo o/Key = contents_of_file.

acceso a la red tooenable Hola Hola usuario debe cerrar el emulador de Hola y eliminar el directorio de datos del emulador de hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Desarrollar con hello emulador
Una vez que haya hello Azure Cosmos DB emulador que se ejecute en el escritorio, puede usar cualquier admite [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) o hello [API de REST de base de datos de Azure Cosmos](/rest/api/documentdb/) toointeract con hello emulador. Hola emulador de base de datos de Azure Cosmos también incluye un explorador de datos integrados que le permite crear colecciones hello documentos y MongoDB APIs y ver y editar documentos sin escribir ningún código.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Si usas [base de datos de Azure Cosmos compatibilidad con el protocolo para MongoDB](mongodb-introduction.md), use Hola después de la cadena de conexión:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

También puede usar herramientas existentes como [estudio de DocumentDB](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB emulador. También puede migrar datos entre hello Azure Cosmos DB emulador y el servicio de base de datos de Azure Cosmos hello mediante hello [herramienta de migración de datos de base de datos de Azure Cosmos](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Si ha iniciado el emulador de hello con hello opción/Key, a continuación, usar la clave de hello generado en lugar de "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Mediante el emulador de base de datos de Azure Cosmos hello, de forma predeterminada, puede crear colecciones de una única partición too25 o 1 colección particionada. Para obtener más información acerca de cómo cambiar este valor, consulte [establecer valor de hello PartitionCount](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Exportar el certificado SSL de Hola

Lenguajes .NET y en tiempo de ejecución use Hola almacén de certificados de Windows toosecurely conectan emulador local de base de datos de Azure Cosmos toohello. Otros lenguajes tienen sus propios métodos de administración y uso de certificados. Java utiliza su propio [almacén de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), mientras que Python utiliza [contenedores de sockets](https://docs.python.org/2/library/ssl.html).

En orden tooobtain un toouse de certificado con los idiomas y tiempo de ejecución que no se integra con el almacén de certificados de Windows hello, será necesario tooexport mediante el Administrador de certificados de Windows hello. Puede iniciarlo, ejecute certlm.msc o siga las instrucciones paso a paso de hello en [exportar hello Azure Cosmos DB emulador certificados](./local-emulator-export-ssl-certificates.md). Una vez que se ejecuta el Administrador de certificados de hello, certificados personales de hello abrir tal y como se muestra a continuación y exportación Hola certificado con el nombre descriptivo de Hola "DocumentDBEmulatorCertificate" como archivo X.509 (.cer) codificado en BASE 64.

![Certificado SSL del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

certificado X.509 de Hello puede importarse al almacén de certificados de Java de hello siguiendo las instrucciones de hello en [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Una vez que se importa el certificado de hello en el almacén de certificados de hello, aplicaciones de Java y MongoDB será toohello tooconnect capaz de emulador de base de datos de Azure Cosmos.

Cuando se conecte toohello emulador del SDK de Node.js y Python, deshabilitar la comprobación de SSL.

## <a id="command-line"></a>Referencia de la herramienta de la línea de comandos
Desde la ubicación de instalación de hello, puede usar toostart de línea de comandos de Hola y detener el emulador de hello, configurar las opciones y realizar otras operaciones.

### <a name="command-line-syntax"></a>Sintaxis de línea de comandos

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

lista de hello tooview de opciones, tipo `CosmosDB.Emulator.exe /?` en línea de comandos de Hola.

<table>
<tr>
  <td><strong>Opción</strong></td>
  <td><strong>Descripción</strong></td>
  <td><strong>Comando</strong></td>
  <td><strong>Argumentos</strong></td>
</tr>
<tr>
  <td>[Sin argumentos]</td>
  <td>Se inicia hello Azure Cosmos DB emulador con la configuración predeterminada.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Ayuda]</td>
  <td>Muestra una lista de hello admite argumentos de línea de comandos.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Se cierra hello Azure Cosmos DB emulador.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Especifica la ruta de acceso de hello en los archivos de datos de toostore. El valor predeterminado es %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt;: una ruta accesible</td>
</tr>
<tr>
  <td>Port</td>
  <td>Especifica toouse de número de puerto de hello para el emulador de Hola.  El valor predeterminado es 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;port&gt;</td>
  <td>&lt;port&gt;: número de puerto sencillo</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Especifica el puerto número toouse de hello para la compatibilidad de MongoDB API. El valor predeterminado es 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: número de puerto sencillo</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Especifica hello toouse de puertos para la conectividad directa. Los valores predeterminados son 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: una lista delimitada por comas de 4 puertos</td>
</tr>
<tr>
  <td>Clave</td>
  <td>Clave de autorización para el emulador de Hola. Clave debe ser Hola codificación de base 64 de un vector de 64 bytes.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;key&gt;</td>
  <td>&lt;clave&gt;: las claves deben ser Hola codificación de base 64 de un vector de 64 bits</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Especifica que el comportamiento de limitación de velocidad de solicitudes está habilitado.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Especifica que el comportamiento de limitación de velocidad de solicitudes está deshabilitado.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>No mostrar el emulador de hello interfaz de usuario.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>No muestra el Explorador de documentos en el inicio.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Especifica el número máximo de Hola de las colecciones particionadas. Vea [cambiar número de Hola de colecciones](#set-partitioncount) para obtener más información.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;: número máximo de colecciones de una sola partición permitidas. El valor predeterminado es 25. El máximo permitido es 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Especifica el número predeterminado de Hola de particiones para una colección con particiones.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>El valor predeterminado de &lt;defaultpartitioncount&gt; es 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Permite tener acceso a toohello emulador a través de una red. También debe pasar/key =&lt;key_string&gt; o/keyfile =&lt;file_name&gt; tooenable acceso a la red.</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;<br><br>o<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>No ajuste las reglas de firewall cuando se utiliza /AllowNetworkAccess.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Generar una nueva clave de autorización y guarde el archivo especificado toohello. clave de Hello generado se puede utilizar con opciones / keyfile u Hola/Key.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;ruta al archivo tookey&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Coherencia</td>
  <td>Establezca el nivel de coherencia de hello predeterminado para la cuenta de hello.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;coherencia&gt;: valor debe ser uno de los siguientes hello [niveles de coherencia](consistency-levels.md): sesión segura, Eventual o BoundedStaleness.  valor predeterminado de Hello es la sesión.</td>
</tr>
<tr>
  <td>?</td>
  <td>Mostrar mensaje de Ayuda de saludo.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Diferencias entre hello Azure Cosmos DB emulador y base de datos de Azure Cosmos 
Dado que hello Azure Cosmos DB emulador proporciona un entorno emulado ejecutando en una estación de trabajo de desarrollador local, hay algunas diferencias de funcionalidad entre emulador hello y una cuenta de base de datos de Azure Cosmos en nube de hello:

* Hola emulador de base de datos de Azure Cosmos admite solo una cuenta única fija y una clave maestra conocida.  Regeneración de claves no es posible en hello Azure Cosmos DB emulador.
* Hello Azure Cosmos DB emulador no es un servicio escalable y no será compatible con un gran número de colecciones.
* Hello Azure Cosmos DB emulador no simular diferentes [niveles de coherencia de base de datos de Azure Cosmos](consistency-levels.md).
* Hello Azure Cosmos DB emulador no simular [varias regiones replicación](distribute-data-globally.md).
* Hello Azure Cosmos DB emulador no admite invalidaciones de cuota de servicio de Hola que están disponibles en el servicio de base de datos de Azure Cosmos hello (por ejemplo, límites de tamaño del documento, colección particionada mayor almacenamiento).
* Como la copia de hello Azure Cosmos DB emulador no puede ser una toodate con los cambios más recientes de hello con el servicio de base de datos de Azure Cosmos hello, inicie [programador de capacidad de la base de datos de Azure Cosmos](https://www.documentdb.com/capacityplanner) rendimiento de producción de estimación de tooaccurately (RUs) necesidades de la aplicación.

## <a id="set-partitioncount"></a>Cambiar el número de Hola de colecciones

De forma predeterminada, puede crear colecciones de una única partición too25 o 1 colección con particiones mediante hello Azure Cosmos DB emulador. Mediante la modificación de hello **PartitionCount** valor, puede crear colecciones de una única partición too250 o 10 colecciones con particiones o cualquier combinación de dos que no superan los 250 único Hola particiones (donde 1 dividida colección = 25 colección de una sola partición).

Si intentas toocreate una colección después de que se superó el número de partición actual de hello, emulador Hola produce una excepción ServiceUnavailable, con el siguiente mensaje de Hola.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

número de hello toochange de colecciones disponibles toohello emulador de base de datos de Azure Cosmos, Hola siguientes:

1. Eliminar todos los datos de Azure Cosmos DB emulador locales con el botón secundario hello **emulador de base de datos de Azure Cosmos** icono de bandeja del sistema de hello y, a continuación, haga clic en **restablecer datos...** .
2. Elimine todos los datos del emulador en la carpeta C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Salir de todas las instancias abiertas con el botón secundario hello **emulador de base de datos de Azure Cosmos** icono de bandeja del sistema de hello y, a continuación, haga clic en **Exit**. Puede tardar un minuto para tooexit de todas las instancias.
4. Instalar la versión más reciente de hello del programa Hola a [emulador de base de datos de Azure Cosmos](https://aka.ms/cosmosdb-emulator).
5. Inicie el emulador de hello con hello PartitionCount marca estableciendo un valor < = 250. Por ejemplo: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Solución de problemas

Usar hello sigue sugerencias toohelp solucionar los problemas que pueda surgir con el emulador de base de datos de Azure Cosmos hello:

- Si instala una nueva versión de hello emulador y está experimentando errores, asegúrese de que restablecer los datos. Puede restablecer los datos haciendo clic en icono de emulador de base de datos de Azure Cosmos hello en la bandeja del sistema de hello y, a continuación, haga clic en Restablecer datos... Si no se soluciona errores de hello, puede desinstalar y reinstalar la aplicación hello. Vea [desinstalar un emulador local hello](#uninstall) para obtener instrucciones.

- Si se bloquea el emulador de base de datos de Azure Cosmos hello, recopilar archivos de volcado de memoria de la carpeta c:\Users\user_name\AppData\Local\CrashDumps, comprimirlos y conéctelas correo electrónico tooan demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Si se producen bloqueos en CosmosDB.StartupEntryPoint.exe, ejecute hello siguiente comando desde un símbolo del sistema de administración:`lodctr /R` 

- Si se produce un problema de conectividad, [recopilar los archivos de seguimiento](#trace-files), comprimirlos y conéctelas correo electrónico tooan demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Si recibe un **servicio no disponible** de mensajes, hello emulador podría no ser correcta pila de red de tooinitialize Hola. Compruebe toosee si dispone de cliente segura de impulso de Hola o instalado, el cliente de redes de Juniper como sus controladores de filtro de red pueden provocar problemas de Hola. Desinstalando controladores de filtro de red de otros fabricantes normalmente corrige el problema de Hola.

### <a id="trace-files"></a>Recopilación de archivos de seguimiento

toocollect depuración seguimientos, ejecute hello siguientes comandos desde un símbolo del sistema administrativo:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Inspección Hola bandeja toomake seguro Hola programa sistema se ha cerrado, podría tardar un minuto. Puede también hacer clic **Exit** en la interfaz de usuario del emulador de base de datos de Azure Cosmos de Hola.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Reproduzca el problema de Hola. Si el Explorador de datos no funciona, sólo necesita toowait para tooopen de explorador hello para el error unos segundos toocatch Hola.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Navegue demasiado`%ProgramFiles%\Azure Cosmos DB Emulator` y busque el archivo de hello docdbemulator_000001.etl.
7. Enviar archivo .etl de hello junto con los pasos de reproducción demasiado[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) para la depuración.

### <a id="uninstall"></a>Desinstalar Hola emulador local

1. Salir de todas las instancias abiertas de hello emulador local haciendo clic en icono de emulador de base de datos de Azure Cosmos hello en la bandeja del sistema de hello y, a continuación, haga clic en salir. Puede tardar un minuto para tooexit de todas las instancias.
2. En el cuadro de búsqueda de Windows hello, escriba **aplicaciones y características** y haga clic en hello **aplicaciones y características (configuración del sistema)** resultado.
3. En la lista de Hola de aplicaciones, desplácese demasiado**emulador de base de datos de Azure Cosmos**, selecciónela, haga clic en **desinstalar**, a continuación, confirme y haga clic en **desinstalar** nuevo.
4. Cuando se desinstala la aplicación hello, navegue tooC:\Users\<usuario > carpeta hello \AppData\Local\CosmosDBEmulator y delete. 

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Instalado Hola emulador local
> * RAND Hola emulador en Docker para Windows
> * Ha autenticado solicitudes
> * Usar Hola Explorador de datos en hello emulador
> * Ha exportado certificados SSL
> * Llamado hello emulador desde la línea de comandos de Hola
> * Ha recopilado archivos de seguimiento

En este tutorial, ha aprendido cómo toouse Hola emulador local para el desarrollo local disponible. Ahora puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo tooexport certificados de SSL del emulador. 

> [!div class="nextstepaction"]
> [Exportar certificados de emulador de base de datos de Azure Cosmos Hola](local-emulator-export-ssl-certificates.md)
