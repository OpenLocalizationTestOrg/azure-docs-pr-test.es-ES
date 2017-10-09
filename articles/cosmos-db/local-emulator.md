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
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="82648-104">Usar hello Azure Cosmos DB emulador para desarrollo local y las pruebas</span><span class="sxs-lookup"><span data-stu-id="82648-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="82648-105"><strong>Archivos binarios</strong></span><span class="sxs-lookup"><span data-stu-id="82648-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="82648-106">Descargar MSI</span><span class="sxs-lookup"><span data-stu-id="82648-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="82648-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="82648-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="82648-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="82648-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="82648-109"><strong>Origen de Docker</strong></span><span class="sxs-lookup"><span data-stu-id="82648-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="82648-110">Github</span><span class="sxs-lookup"><span data-stu-id="82648-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="82648-111">Hello Azure Cosmos DB emulador proporciona un entorno local que emula Hola servicio de base de datos de Azure Cosmos para fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="82648-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="82648-112">Hola emulador de base de datos de Azure Cosmos puede desarrollar y probar su aplicación localmente, sin crear una suscripción de Azure o incurrir en los costos.</span><span class="sxs-lookup"><span data-stu-id="82648-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="82648-113">Cuando esté satisfecho con cómo funciona la aplicación en el emulador de base de datos de Azure Cosmos hello, puede cambiar una cuenta de base de datos de Azure Cosmos en nube de hello toousing.</span><span class="sxs-lookup"><span data-stu-id="82648-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="82648-114">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="82648-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="82648-115">Instalar Hola emulador</span><span class="sxs-lookup"><span data-stu-id="82648-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="82648-116">Hola ejecución emulador en Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="82648-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="82648-117">Autenticación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="82648-117">Authenticating requests</span></span>
> * <span data-ttu-id="82648-118">Uso de hello Explorador de datos en hello emulador</span><span class="sxs-lookup"><span data-stu-id="82648-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="82648-119">Exportación de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="82648-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="82648-120">Llamar a Hola emulador desde línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="82648-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="82648-121">Recopilación de archivos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="82648-121">Collecting trace files</span></span>

<span data-ttu-id="82648-122">Se recomienda introducción, inspeccionando Hola después de vídeo, donde se muestra cómo tooget partió hello Azure Cosmos DB emulador Kirill Gavrylyuk.</span><span class="sxs-lookup"><span data-stu-id="82648-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="82648-123">Tenga en cuenta que vídeo Hola hace referencia toohello emulador como Hola emulador de documentos, pero se ha cambiado el nombre de la propia herramienta de Hola Hola Azure Cosmos DB emulador desde punteando en vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="82648-124">Toda la información de vídeo hello es precisa para hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="82648-125">Cómo funciona la Hola emulador</span><span class="sxs-lookup"><span data-stu-id="82648-125">How hello Emulator works</span></span>
<span data-ttu-id="82648-126">Hola emulador de base de datos de Azure Cosmos proporciona una emulación de alta fidelidad del servicio de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="82648-127">Admite una funcionalidad idéntica a la de Azure Cosmos DB, incluida la compatibilidad con la creación y la consulta de documentos JSON, el aprovisionamiento y el escalado de colecciones y la ejecución de procedimientos y desencadenadores almacenados.</span><span class="sxs-lookup"><span data-stu-id="82648-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="82648-128">Puede desarrollar y probar las aplicaciones que usan el emulador de base de datos de Azure Cosmos hello e implementarlos tooAzure a escala global realizando simplemente una sola configuración cambiar toohello extremo de la conexión de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="82648-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="82648-129">Mientras se crea una emulación local de alta fidelidad del servicio de base de datos de Azure Cosmos real de hello, implementación de Hola de hello Azure Cosmos DB emulador es diferente del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="82648-130">Por ejemplo, hello Azure Cosmos DB emulador usa componentes del sistema operativo estándares, como sistema de archivos local de hello para la persistencia y la pila del protocolo HTTPS para la conectividad.</span><span class="sxs-lookup"><span data-stu-id="82648-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="82648-131">Esto significa que alguna funcionalidad que se basa en la infraestructura de Azure como replicación global, latencia de milisegundos de un solo dígito para lectura/escritura y niveles de coherencia de los no están disponibles a través de hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="82648-132">En este Hola Explorador de datos de tiempo en hello emulador solo admite la creación de hello de colecciones de API de documentos y MongoDB.</span><span class="sxs-lookup"><span data-stu-id="82648-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="82648-133">Hola Explorador de datos en el emulador de hello no admite actualmente la creación de hello de tablas y gráficos.</span><span class="sxs-lookup"><span data-stu-id="82648-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="82648-134">Requisitos del sistema</span><span class="sxs-lookup"><span data-stu-id="82648-134">System requirements</span></span>
<span data-ttu-id="82648-135">Hola emulador de base de datos de Azure Cosmos tiene Hola según los requisitos de hardware y software:</span><span class="sxs-lookup"><span data-stu-id="82648-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="82648-136">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="82648-136">Software requirements</span></span>
  * <span data-ttu-id="82648-137">Windows Server 2012 R2, Windows Server 2016 o Windows 10</span><span class="sxs-lookup"><span data-stu-id="82648-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="82648-138">Requisitos mínimos de hardware</span><span class="sxs-lookup"><span data-stu-id="82648-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="82648-139">2 GB DE RAM</span><span class="sxs-lookup"><span data-stu-id="82648-139">2 GB RAM</span></span>
  * <span data-ttu-id="82648-140">10 GB de espacio disponible en disco duro</span><span class="sxs-lookup"><span data-stu-id="82648-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="82648-141">Instalación</span><span class="sxs-lookup"><span data-stu-id="82648-141">Installation</span></span>
<span data-ttu-id="82648-142">Puede descargar e instalar hello Azure Cosmos DB emulador de hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="82648-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="82648-143">tooinstall, configurar y ejecutar el emulador de base de datos de Azure Cosmos hello, debe tener privilegios administrativos en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="82648-144">Ejecución en Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="82648-144">Running on Docker for Windows</span></span>

<span data-ttu-id="82648-145">Hola emulador de Azure Cosmos DB se puede ejecutar en Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="82648-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="82648-146">Hola emulador no funciona en Docker para Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="82648-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="82648-147">Una vez que tenga [Docker para Windows](https://www.docker.com/docker-windows) instalado, se puede extraer de imagen del emulador Hola de Docker Hub ejecutando el siguiente comando desde el shell de favoritos de Hola (cmd.exe, PowerShell, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="82648-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="82648-148">imagen de hello toostart, ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="82648-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="82648-149">respuesta de Hello tiene un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="82648-149">hello response looks similar toohello following:</span></span>

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

<span data-ttu-id="82648-150">Cierre Hola shell interactiva cuando se ha iniciado el emulador de hello va contenedor del emulador de apagado Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="82648-151">Use punto de conexión de Hola y de clave maestra en el de respuesta de hello en el cliente e importe el certificado SSL de hello en el host.</span><span class="sxs-lookup"><span data-stu-id="82648-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="82648-152">Hola tooimport certificado SSL, Hola siguiente desde un símbolo del sistema de administración:</span><span class="sxs-lookup"><span data-stu-id="82648-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="82648-153">Iniciar el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="82648-153">Start hello Emulator</span></span>

<span data-ttu-id="82648-154">Hola toostart emulador de base de datos de Azure Cosmos, seleccione el botón de inicio de Hola o presione la tecla de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="82648-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="82648-155">Comience a escribir **emulador de base de datos de Azure Cosmos**y seleccione Hola emulador de lista de Hola de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82648-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Seleccione Hola o presionen Hola Windows clave de inicio, comience a escribir ** Azure Cosmos DB emulador ** y seleccione Hola emulador de lista de Hola de aplicaciones](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="82648-157">Cuando se ejecuta el emulador de hello, verá un icono en el área de notificación de barra de tareas de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="82648-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Notificación en la barra de tareas del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="82648-159">Hola emulador de base de datos de Azure Cosmos de forma predeterminada se ejecuta en máquina local de hello ("localhost") escuchando en el puerto 8081.</span><span class="sxs-lookup"><span data-stu-id="82648-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="82648-160">Hello Azure Cosmos DB emulador instala predeterminado toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="82648-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="82648-161">También puede iniciar y detener el emulador de Hola desde Hola de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="82648-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="82648-162">Vea la [referencia de la herramienta de la línea de comandos](#command-line) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="82648-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="82648-163">Inicio del Explorador de datos</span><span class="sxs-lookup"><span data-stu-id="82648-163">Start Data Explorer</span></span>

<span data-ttu-id="82648-164">Cuando se inicia el emulador de base de datos de Azure Cosmos Hola abrirá automáticamente Hola Explorador de datos de base de datos de Azure Cosmos en el explorador.</span><span class="sxs-lookup"><span data-stu-id="82648-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="82648-165">dirección de Hello aparecerá como [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="82648-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="82648-166">Si cerrar Hola explorador y desearía toore abierto más adelante, puede abrir dirección URL de hello en el explorador o iniciarlo desde hello Azure Cosmos DB emulador en el icono de la Bandeja de Windows hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="82648-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Iniciador del Explorador de datos del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="82648-168">Búsqueda de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="82648-168">Checking for updates</span></span>
<span data-ttu-id="82648-169">En el Explorador de datos se indica si hay una nueva actualización disponible para descarga.</span><span class="sxs-lookup"><span data-stu-id="82648-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="82648-170">Datos que se crean en una versión de hello Azure Cosmos DB emulador no está garantizados toobe accesible cuando se usa una versión diferente.</span><span class="sxs-lookup"><span data-stu-id="82648-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="82648-171">Si necesita toopersist los datos para a largo plazo de hello, se recomienda que almacene esos datos en una cuenta de base de datos de Azure Cosmos, en lugar de hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="82648-172">Autenticación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="82648-172">Authenticating requests</span></span>
<span data-ttu-id="82648-173">Al igual que con la base de datos de Azure Cosmos en nube de hello, todas las solicitudes que se realizan con hello Azure Cosmos DB emulador deben autenticarse.</span><span class="sxs-lookup"><span data-stu-id="82648-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="82648-174">Hola emulador de base de datos de Azure Cosmos admite una cuenta única fija y una clave de autenticación conocido para la autenticación de clave maestra.</span><span class="sxs-lookup"><span data-stu-id="82648-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="82648-175">Esta cuenta y clave son Hola únicas credenciales permitidas para su uso con hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="82648-176">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="82648-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="82648-177">clave maestra de Hello admitido hello Azure Cosmos DB emulador está pensado para uso únicamente con el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="82648-178">No puede usar su cuenta de base de datos de Azure Cosmos de producción y la clave con hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="82648-179">Si ha iniciado el emulador de hello con hello opción/Key, a continuación, usar la clave de hello generado en lugar de "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="82648-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="82648-180">Además, al igual que el servicio de base de datos de Azure Cosmos, hello Azure Cosmos DB emulador Hola admite solo una comunicación segura mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="82648-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="82648-181">Emulador en ejecución hello en una red local</span><span class="sxs-lookup"><span data-stu-id="82648-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="82648-182">Puede ejecutar el emulador de hello en una red local.</span><span class="sxs-lookup"><span data-stu-id="82648-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="82648-183">tooenable acceso a la red, especifique la opción de /AllowNetworkAccess hello en hello [línea de comandos](#command-line-syntax), que también requiere que especifique/Key = key_string o/keyfile = nombre_archivo.</span><span class="sxs-lookup"><span data-stu-id="82648-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="82648-184">Puede usar /GenKeyFile = nombre_archivo toogenerate un archivo con una clave aleatoria por adelantado.</span><span class="sxs-lookup"><span data-stu-id="82648-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="82648-185">A continuación, puede pasar dicho demasiado/KeyFile = nombre_archivo o/Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="82648-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="82648-186">acceso a la red tooenable Hola Hola usuario debe cerrar el emulador de Hola y eliminar el directorio de datos del emulador de hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="82648-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="82648-187">Desarrollar con hello emulador</span><span class="sxs-lookup"><span data-stu-id="82648-187">Developing with hello Emulator</span></span>
<span data-ttu-id="82648-188">Una vez que haya hello Azure Cosmos DB emulador que se ejecute en el escritorio, puede usar cualquier admite [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) o hello [API de REST de base de datos de Azure Cosmos](/rest/api/documentdb/) toointeract con hello emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="82648-189">Hola emulador de base de datos de Azure Cosmos también incluye un explorador de datos integrados que le permite crear colecciones hello documentos y MongoDB APIs y ver y editar documentos sin escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="82648-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="82648-190">Si usas [base de datos de Azure Cosmos compatibilidad con el protocolo para MongoDB](mongodb-introduction.md), use Hola después de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="82648-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="82648-191">También puede usar herramientas existentes como [estudio de DocumentDB](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="82648-192">También puede migrar datos entre hello Azure Cosmos DB emulador y el servicio de base de datos de Azure Cosmos hello mediante hello [herramienta de migración de datos de base de datos de Azure Cosmos](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="82648-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="82648-193">Si ha iniciado el emulador de hello con hello opción/Key, a continuación, usar la clave de hello generado en lugar de "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="82648-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="82648-194">Mediante el emulador de base de datos de Azure Cosmos hello, de forma predeterminada, puede crear colecciones de una única partición too25 o 1 colección particionada.</span><span class="sxs-lookup"><span data-stu-id="82648-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="82648-195">Para obtener más información acerca de cómo cambiar este valor, consulte [establecer valor de hello PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="82648-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="82648-196">Exportar el certificado SSL de Hola</span><span class="sxs-lookup"><span data-stu-id="82648-196">Export hello SSL certificate</span></span>

<span data-ttu-id="82648-197">Lenguajes .NET y en tiempo de ejecución use Hola almacén de certificados de Windows toosecurely conectan emulador local de base de datos de Azure Cosmos toohello.</span><span class="sxs-lookup"><span data-stu-id="82648-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="82648-198">Otros lenguajes tienen sus propios métodos de administración y uso de certificados.</span><span class="sxs-lookup"><span data-stu-id="82648-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="82648-199">Java utiliza su propio [almacén de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), mientras que Python utiliza [contenedores de sockets](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="82648-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="82648-200">En orden tooobtain un toouse de certificado con los idiomas y tiempo de ejecución que no se integra con el almacén de certificados de Windows hello, será necesario tooexport mediante el Administrador de certificados de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="82648-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="82648-201">Puede iniciarlo, ejecute certlm.msc o siga las instrucciones paso a paso de hello en [exportar hello Azure Cosmos DB emulador certificados](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="82648-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="82648-202">Una vez que se ejecuta el Administrador de certificados de hello, certificados personales de hello abrir tal y como se muestra a continuación y exportación Hola certificado con el nombre descriptivo de Hola "DocumentDBEmulatorCertificate" como archivo X.509 (.cer) codificado en BASE 64.</span><span class="sxs-lookup"><span data-stu-id="82648-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificado SSL del emulador local de Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="82648-204">certificado X.509 de Hello puede importarse al almacén de certificados de Java de hello siguiendo las instrucciones de hello en [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="82648-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="82648-205">Una vez que se importa el certificado de hello en el almacén de certificados de hello, aplicaciones de Java y MongoDB será toohello tooconnect capaz de emulador de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="82648-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="82648-206">Cuando se conecte toohello emulador del SDK de Node.js y Python, deshabilitar la comprobación de SSL.</span><span class="sxs-lookup"><span data-stu-id="82648-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="82648-207"><a id="command-line"></a>Referencia de la herramienta de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="82648-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="82648-208">Desde la ubicación de instalación de hello, puede usar toostart de línea de comandos de Hola y detener el emulador de hello, configurar las opciones y realizar otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="82648-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="82648-209">Sintaxis de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="82648-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="82648-210">lista de hello tooview de opciones, tipo `CosmosDB.Emulator.exe /?` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="82648-211"><strong>Opción</strong></span><span class="sxs-lookup"><span data-stu-id="82648-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="82648-212"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="82648-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="82648-213"><strong>Comando</strong></span><span class="sxs-lookup"><span data-stu-id="82648-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="82648-214"><strong>Argumentos</strong></span><span class="sxs-lookup"><span data-stu-id="82648-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-215">[Sin argumentos]</span><span class="sxs-lookup"><span data-stu-id="82648-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="82648-216">Se inicia hello Azure Cosmos DB emulador con la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="82648-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="82648-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="82648-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-218">[Ayuda]</span><span class="sxs-lookup"><span data-stu-id="82648-218">[Help]</span></span></td>
  <td><span data-ttu-id="82648-219">Muestra una lista de hello admite argumentos de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="82648-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="82648-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="82648-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="82648-221">Shutdown</span></span></td>
  <td><span data-ttu-id="82648-222">Se cierra hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="82648-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="82648-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="82648-224">DataPath</span></span></td>
  <td><span data-ttu-id="82648-225">Especifica la ruta de acceso de hello en los archivos de datos de toostore.</span><span class="sxs-lookup"><span data-stu-id="82648-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="82648-226">El valor predeterminado es %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="82648-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="82648-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="82648-228">&lt;datapath&gt;: una ruta accesible</span><span class="sxs-lookup"><span data-stu-id="82648-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-229">Port</span><span class="sxs-lookup"><span data-stu-id="82648-229">Port</span></span></td>
  <td><span data-ttu-id="82648-230">Especifica toouse de número de puerto de hello para el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="82648-231">El valor predeterminado es 8081.</span><span class="sxs-lookup"><span data-stu-id="82648-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="82648-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="82648-233">&lt;port&gt;: número de puerto sencillo</span><span class="sxs-lookup"><span data-stu-id="82648-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="82648-234">MongoPort</span></span></td>
  <td><span data-ttu-id="82648-235">Especifica el puerto número toouse de hello para la compatibilidad de MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="82648-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="82648-236">El valor predeterminado es 10255.</span><span class="sxs-lookup"><span data-stu-id="82648-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="82648-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="82648-238">&lt;mongoport&gt;: número de puerto sencillo</span><span class="sxs-lookup"><span data-stu-id="82648-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="82648-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="82648-240">Especifica hello toouse de puertos para la conectividad directa.</span><span class="sxs-lookup"><span data-stu-id="82648-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="82648-241">Los valores predeterminados son 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="82648-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="82648-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="82648-243">&lt;directports&gt;: una lista delimitada por comas de 4 puertos</span><span class="sxs-lookup"><span data-stu-id="82648-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-244">Clave</span><span class="sxs-lookup"><span data-stu-id="82648-244">Key</span></span></td>
  <td><span data-ttu-id="82648-245">Clave de autorización para el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="82648-246">Clave debe ser Hola codificación de base 64 de un vector de 64 bytes.</span><span class="sxs-lookup"><span data-stu-id="82648-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="82648-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="82648-248">&lt;clave&gt;: las claves deben ser Hola codificación de base 64 de un vector de 64 bits</span><span class="sxs-lookup"><span data-stu-id="82648-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="82648-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="82648-250">Especifica que el comportamiento de limitación de velocidad de solicitudes está habilitado.</span><span class="sxs-lookup"><span data-stu-id="82648-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="82648-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="82648-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="82648-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="82648-253">Especifica que el comportamiento de limitación de velocidad de solicitudes está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="82648-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="82648-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="82648-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="82648-255">NoUI</span></span></td>
  <td><span data-ttu-id="82648-256">No mostrar el emulador de hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="82648-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="82648-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="82648-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="82648-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="82648-259">No muestra el Explorador de documentos en el inicio.</span><span class="sxs-lookup"><span data-stu-id="82648-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="82648-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="82648-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="82648-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="82648-262">Especifica el número máximo de Hola de las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="82648-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="82648-263">Vea [cambiar número de Hola de colecciones](#set-partitioncount) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="82648-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="82648-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="82648-265">&lt;partitioncount&gt;: número máximo de colecciones de una sola partición permitidas.</span><span class="sxs-lookup"><span data-stu-id="82648-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="82648-266">El valor predeterminado es 25.</span><span class="sxs-lookup"><span data-stu-id="82648-266">Default is 25.</span></span> <span data-ttu-id="82648-267">El máximo permitido es 250.</span><span class="sxs-lookup"><span data-stu-id="82648-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="82648-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="82648-269">Especifica el número predeterminado de Hola de particiones para una colección con particiones.</span><span class="sxs-lookup"><span data-stu-id="82648-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="82648-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="82648-271">El valor predeterminado de &lt;defaultpartitioncount&gt; es 25.</span><span class="sxs-lookup"><span data-stu-id="82648-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="82648-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="82648-273">Permite tener acceso a toohello emulador a través de una red.</span><span class="sxs-lookup"><span data-stu-id="82648-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="82648-274">También debe pasar/key =&lt;key_string&gt; o/keyfile =&lt;file_name&gt; tooenable acceso a la red.</span><span class="sxs-lookup"><span data-stu-id="82648-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="82648-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="82648-276">o</span><span class="sxs-lookup"><span data-stu-id="82648-276">or</span></span><br><br><span data-ttu-id="82648-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="82648-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="82648-279">No ajuste las reglas de firewall cuando se utiliza /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="82648-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="82648-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="82648-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="82648-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="82648-282">Generar una nueva clave de autorización y guarde el archivo especificado toohello.</span><span class="sxs-lookup"><span data-stu-id="82648-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="82648-283">clave de Hello generado se puede utilizar con opciones / keyfile u Hola/Key.</span><span class="sxs-lookup"><span data-stu-id="82648-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="82648-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;ruta al archivo tookey&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-285">Coherencia</span><span class="sxs-lookup"><span data-stu-id="82648-285">Consistency</span></span></td>
  <td><span data-ttu-id="82648-286">Establezca el nivel de coherencia de hello predeterminado para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="82648-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="82648-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="82648-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="82648-288">&lt;coherencia&gt;: valor debe ser uno de los siguientes hello [niveles de coherencia](consistency-levels.md): sesión segura, Eventual o BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="82648-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="82648-289">valor predeterminado de Hello es la sesión.</span><span class="sxs-lookup"><span data-stu-id="82648-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="82648-290">?</span><span class="sxs-lookup"><span data-stu-id="82648-290">?</span></span></td>
  <td><span data-ttu-id="82648-291">Mostrar mensaje de Ayuda de saludo.</span><span class="sxs-lookup"><span data-stu-id="82648-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="82648-292">Diferencias entre hello Azure Cosmos DB emulador y base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="82648-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="82648-293">Dado que hello Azure Cosmos DB emulador proporciona un entorno emulado ejecutando en una estación de trabajo de desarrollador local, hay algunas diferencias de funcionalidad entre emulador hello y una cuenta de base de datos de Azure Cosmos en nube de hello:</span><span class="sxs-lookup"><span data-stu-id="82648-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="82648-294">Hola emulador de base de datos de Azure Cosmos admite solo una cuenta única fija y una clave maestra conocida.</span><span class="sxs-lookup"><span data-stu-id="82648-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="82648-295">Regeneración de claves no es posible en hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="82648-296">Hello Azure Cosmos DB emulador no es un servicio escalable y no será compatible con un gran número de colecciones.</span><span class="sxs-lookup"><span data-stu-id="82648-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="82648-297">Hello Azure Cosmos DB emulador no simular diferentes [niveles de coherencia de base de datos de Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="82648-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="82648-298">Hello Azure Cosmos DB emulador no simular [varias regiones replicación](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="82648-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="82648-299">Hello Azure Cosmos DB emulador no admite invalidaciones de cuota de servicio de Hola que están disponibles en el servicio de base de datos de Azure Cosmos hello (por ejemplo, límites de tamaño del documento, colección particionada mayor almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="82648-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="82648-300">Como la copia de hello Azure Cosmos DB emulador no puede ser una toodate con los cambios más recientes de hello con el servicio de base de datos de Azure Cosmos hello, inicie [programador de capacidad de la base de datos de Azure Cosmos](https://www.documentdb.com/capacityplanner) rendimiento de producción de estimación de tooaccurately (RUs) necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82648-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="82648-301"><a id="set-partitioncount"></a>Cambiar el número de Hola de colecciones</span><span class="sxs-lookup"><span data-stu-id="82648-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="82648-302">De forma predeterminada, puede crear colecciones de una única partición too25 o 1 colección con particiones mediante hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="82648-303">Mediante la modificación de hello **PartitionCount** valor, puede crear colecciones de una única partición too250 o 10 colecciones con particiones o cualquier combinación de dos que no superan los 250 único Hola particiones (donde 1 dividida colección = 25 colección de una sola partición).</span><span class="sxs-lookup"><span data-stu-id="82648-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="82648-304">Si intentas toocreate una colección después de que se superó el número de partición actual de hello, emulador Hola produce una excepción ServiceUnavailable, con el siguiente mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="82648-305">número de hello toochange de colecciones disponibles toohello emulador de base de datos de Azure Cosmos, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="82648-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="82648-306">Eliminar todos los datos de Azure Cosmos DB emulador locales con el botón secundario hello **emulador de base de datos de Azure Cosmos** icono de bandeja del sistema de hello y, a continuación, haga clic en **restablecer datos...** .</span><span class="sxs-lookup"><span data-stu-id="82648-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="82648-307">Elimine todos los datos del emulador en la carpeta C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="82648-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="82648-308">Salir de todas las instancias abiertas con el botón secundario hello **emulador de base de datos de Azure Cosmos** icono de bandeja del sistema de hello y, a continuación, haga clic en **Exit**.</span><span class="sxs-lookup"><span data-stu-id="82648-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="82648-309">Puede tardar un minuto para tooexit de todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="82648-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="82648-310">Instalar la versión más reciente de hello del programa Hola a [emulador de base de datos de Azure Cosmos](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="82648-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="82648-311">Inicie el emulador de hello con hello PartitionCount marca estableciendo un valor < = 250.</span><span class="sxs-lookup"><span data-stu-id="82648-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="82648-312">Por ejemplo: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="82648-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="82648-313">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="82648-313">Troubleshooting</span></span>

<span data-ttu-id="82648-314">Usar hello sigue sugerencias toohelp solucionar los problemas que pueda surgir con el emulador de base de datos de Azure Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="82648-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="82648-315">Si instala una nueva versión de hello emulador y está experimentando errores, asegúrese de que restablecer los datos.</span><span class="sxs-lookup"><span data-stu-id="82648-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="82648-316">Puede restablecer los datos haciendo clic en icono de emulador de base de datos de Azure Cosmos hello en la bandeja del sistema de hello y, a continuación, haga clic en Restablecer datos...</span><span class="sxs-lookup"><span data-stu-id="82648-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="82648-317">Si no se soluciona errores de hello, puede desinstalar y reinstalar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="82648-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="82648-318">Vea [desinstalar un emulador local hello](#uninstall) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="82648-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="82648-319">Si se bloquea el emulador de base de datos de Azure Cosmos hello, recopilar archivos de volcado de memoria de la carpeta c:\Users\user_name\AppData\Local\CrashDumps, comprimirlos y conéctelas correo electrónico tooan demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="82648-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="82648-320">Si se producen bloqueos en CosmosDB.StartupEntryPoint.exe, ejecute hello siguiente comando desde un símbolo del sistema de administración:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="82648-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="82648-321">Si se produce un problema de conectividad, [recopilar los archivos de seguimiento](#trace-files), comprimirlos y conéctelas correo electrónico tooan demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="82648-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="82648-322">Si recibe un **servicio no disponible** de mensajes, hello emulador podría no ser correcta pila de red de tooinitialize Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="82648-323">Compruebe toosee si dispone de cliente segura de impulso de Hola o instalado, el cliente de redes de Juniper como sus controladores de filtro de red pueden provocar problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="82648-324">Desinstalando controladores de filtro de red de otros fabricantes normalmente corrige el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="82648-325"><a id="trace-files"></a>Recopilación de archivos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="82648-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="82648-326">toocollect depuración seguimientos, ejecute hello siguientes comandos desde un símbolo del sistema administrativo:</span><span class="sxs-lookup"><span data-stu-id="82648-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="82648-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="82648-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="82648-328">Inspección Hola bandeja toomake seguro Hola programa sistema se ha cerrado, podría tardar un minuto.</span><span class="sxs-lookup"><span data-stu-id="82648-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="82648-329">Puede también hacer clic **Exit** en la interfaz de usuario del emulador de base de datos de Azure Cosmos de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="82648-330">Reproduzca el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-330">Reproduce hello problem.</span></span> <span data-ttu-id="82648-331">Si el Explorador de datos no funciona, sólo necesita toowait para tooopen de explorador hello para el error unos segundos toocatch Hola.</span><span class="sxs-lookup"><span data-stu-id="82648-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="82648-332">Navegue demasiado`%ProgramFiles%\Azure Cosmos DB Emulator` y busque el archivo de hello docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="82648-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="82648-333">Enviar archivo .etl de hello junto con los pasos de reproducción demasiado[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) para la depuración.</span><span class="sxs-lookup"><span data-stu-id="82648-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="82648-334"><a id="uninstall"></a>Desinstalar Hola emulador local</span><span class="sxs-lookup"><span data-stu-id="82648-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="82648-335">Salir de todas las instancias abiertas de hello emulador local haciendo clic en icono de emulador de base de datos de Azure Cosmos hello en la bandeja del sistema de hello y, a continuación, haga clic en salir.</span><span class="sxs-lookup"><span data-stu-id="82648-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="82648-336">Puede tardar un minuto para tooexit de todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="82648-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="82648-337">En el cuadro de búsqueda de Windows hello, escriba **aplicaciones y características** y haga clic en hello **aplicaciones y características (configuración del sistema)** resultado.</span><span class="sxs-lookup"><span data-stu-id="82648-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="82648-338">En la lista de Hola de aplicaciones, desplácese demasiado**emulador de base de datos de Azure Cosmos**, selecciónela, haga clic en **desinstalar**, a continuación, confirme y haga clic en **desinstalar** nuevo.</span><span class="sxs-lookup"><span data-stu-id="82648-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="82648-339">Cuando se desinstala la aplicación hello, navegue tooC:\Users\<usuario > carpeta hello \AppData\Local\CosmosDBEmulator y delete.</span><span class="sxs-lookup"><span data-stu-id="82648-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="82648-340">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82648-340">Next steps</span></span>

<span data-ttu-id="82648-341">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="82648-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82648-342">Instalado Hola emulador local</span><span class="sxs-lookup"><span data-stu-id="82648-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="82648-343">RAND Hola emulador en Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="82648-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="82648-344">Ha autenticado solicitudes</span><span class="sxs-lookup"><span data-stu-id="82648-344">Authenticated requests</span></span>
> * <span data-ttu-id="82648-345">Usar Hola Explorador de datos en hello emulador</span><span class="sxs-lookup"><span data-stu-id="82648-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="82648-346">Ha exportado certificados SSL</span><span class="sxs-lookup"><span data-stu-id="82648-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="82648-347">Llamado hello emulador desde la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="82648-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="82648-348">Ha recopilado archivos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="82648-348">Collected trace files</span></span>

<span data-ttu-id="82648-349">En este tutorial, ha aprendido cómo toouse Hola emulador local para el desarrollo local disponible.</span><span class="sxs-lookup"><span data-stu-id="82648-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="82648-350">Ahora puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo tooexport certificados de SSL del emulador.</span><span class="sxs-lookup"><span data-stu-id="82648-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="82648-351">Exportar certificados de emulador de base de datos de Azure Cosmos Hola</span><span class="sxs-lookup"><span data-stu-id="82648-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
