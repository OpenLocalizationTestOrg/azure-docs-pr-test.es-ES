---
title: un servicio de dividir-combinar aaaDeploy | Documentos de Microsoft
description: "División y combinación con las herramientas de Base de datos elástica"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="b844e-103">Implemente un servicio de división y combinación</span><span class="sxs-lookup"><span data-stu-id="b844e-103">Deploy a split-merge service</span></span>
<span data-ttu-id="b844e-104">herramienta Dividir-combinar de Hello permite mover datos entre bases de datos particionadas.</span><span class="sxs-lookup"><span data-stu-id="b844e-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="b844e-105">Consulte [Mover datos entre bases de datos en la nube escaladas horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="b844e-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="b844e-106">Descargar los paquetes de saludo dividir-combinar</span><span class="sxs-lookup"><span data-stu-id="b844e-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="b844e-107">Descargar Hola versión más reciente de NuGet desde [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="b844e-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="b844e-108">Abra un símbolo del sistema y desplácese directorio toohello donde descargó nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="b844e-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="b844e-109">descarga de Hello incluye commmands de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b844e-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="b844e-110">Descargue el paquete de división y combinación más reciente de hello en el directorio actual de hello con hello comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b844e-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="b844e-111">Hola archivos se colocan en un directorio denominado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** donde *x.x.xxx.x* refleja el número de versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="b844e-112">Buscar archivos de servicio de dividir-combinar de hello en hello **content\splitmerge\service** subdirectorio, Hola dividir-combinar PowerShell (y los scripts y archivos .dll de cliente necesario) en hello **content\splitmerge\powershell** subdirectorio.</span><span class="sxs-lookup"><span data-stu-id="b844e-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b844e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b844e-113">Prerequisites</span></span>
1. <span data-ttu-id="b844e-114">Crear una base de datos de la base de datos de SQL Azure que se usará como base de datos de estado de la división y combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="b844e-115">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b844e-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b844e-116">Cree una nueva **Base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="b844e-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="b844e-117">Asigne un nombre de base de datos de Hola y cree un nuevo administrador y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="b844e-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="b844e-118">Estar seguro de nombre de hello toorecord y la contraseña para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="b844e-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="b844e-119">Asegúrese de que el servidor de base de datos de SQL Azure permite tooit tooconnect de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="b844e-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b844e-120">En portal Hola Hola **configuración del Firewall**, asegúrese de que hello **permitir acceso a servicios de tooAzure** opción se establece demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="b844e-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="b844e-121">Haga clic en hello "Guardar" icono.</span><span class="sxs-lookup"><span data-stu-id="b844e-121">Click hello "save" icon.</span></span>
   
   ![Servicios permitidos][1]
3. <span data-ttu-id="b844e-123">Cree una cuenta de almacenamiento de Azure que se usará para la salida de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b844e-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="b844e-124">Vaya toohello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b844e-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="b844e-125">En la barra de la izquierda hello, haga clic en **New**, haga clic en **datos + almacenamiento**, a continuación, **almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b844e-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="b844e-126">Cree un servicio en la nube de Azure que contendrá el servicio de División y combinación.</span><span class="sxs-lookup"><span data-stu-id="b844e-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="b844e-127">Vaya toohello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b844e-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="b844e-128">En la barra de la izquierda hello, haga clic en **New**, a continuación, **proceso**, **servicio de nube**, y **crear**.</span><span class="sxs-lookup"><span data-stu-id="b844e-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="b844e-129">Configuración del servicio de división y combinación</span><span class="sxs-lookup"><span data-stu-id="b844e-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="b844e-130">Configuración del servicio División y combinación</span><span class="sxs-lookup"><span data-stu-id="b844e-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="b844e-131">En carpeta de Hola donde descargó los ensamblados de hello dividir-combinar, cree una copia del programa Hola a **ServiceConfiguration.Template.cscfg** archivo que publicó junto con **SplitMergeService.cspkg** y cambie su nombre **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="b844e-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="b844e-132">Abra **ServiceConfiguration.cscfg** en un editor de texto como Visual Studio que valida las entradas como formato de Hola de huellas digitales de certificado.</span><span class="sxs-lookup"><span data-stu-id="b844e-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="b844e-133">Crear una nueva base de datos o elija un tooserve de base de datos existente como base de datos de estado de Hola para las operaciones de combinación de división y recuperar la cadena de conexión de Hola de esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="b844e-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="b844e-134">En este momento, base de datos de estado de hello debe usar intercalación latina hello (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="b844e-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="b844e-135">Para obtener más información, vea [Nombre de intercalación de Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="b844e-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="b844e-136">Con la base de datos de SQL Azure, cadena de conexión de hello normalmente tiene el formato de hello:</span><span class="sxs-lookup"><span data-stu-id="b844e-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="b844e-137">Escriba esta cadena de conexión en el archivo cscfg de hello en ambos hello **SplitMergeWeb** y **SplitMergeWorker** secciones de rol en la configuración de ElasticScaleMetadata Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="b844e-138">Para hello **SplitMergeWorker** rol, escriba un almacenamiento de tooAzure de cadena de conexión válida para hello **WorkerRoleSynchronizationStorageAccountConnectionString** configuración.</span><span class="sxs-lookup"><span data-stu-id="b844e-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="b844e-139">Configuración de seguridad</span><span class="sxs-lookup"><span data-stu-id="b844e-139">Configure security</span></span>
<span data-ttu-id="b844e-140">Para obtener instrucciones detalladas tooconfigure Hola la seguridad del servicio de hello, consulte toohello [dividir-combinar la configuración de seguridad](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b844e-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="b844e-141">Por motivos de Hola de una implementación de prueba sencilla para este tutorial, un conjunto mínimo de configuración pasos serán realiza servicio de hello tooget activos y en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="b844e-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="b844e-142">Estos pasos habilitan solo Hola una máquina/cuenta ejecutarlas toocommunicate con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b844e-143">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="b844e-143">Create a self-signed certificate</span></span>
<span data-ttu-id="b844e-144">Crear un nuevo directorio y desde este Hola execute de directorio después de comando mediante un [símbolo del sistema para desarrolladores de Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) ventana:</span><span class="sxs-lookup"><span data-stu-id="b844e-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="b844e-145">Se le pedirá una clave privada de contraseña tooprotect Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="b844e-146">Escriba una contraseña segura y confírmela.</span><span class="sxs-lookup"><span data-stu-id="b844e-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="b844e-147">A continuación, se pedirá Hola contraseña toobe utilizado después de una vez más.</span><span class="sxs-lookup"><span data-stu-id="b844e-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="b844e-148">Haga clic en **Sí** en hello final tooimport se toohello almacén de raíz de las entidades de certificación de confianza.</span><span class="sxs-lookup"><span data-stu-id="b844e-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="b844e-149">Creación de un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="b844e-149">Create a PFX file</span></span>
<span data-ttu-id="b844e-150">Ejecutar Hola siguiente comando de hello misma ventana donde se ejecutó makecert; Use Hola misma contraseña usa toocreate Hola certificado:</span><span class="sxs-lookup"><span data-stu-id="b844e-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="b844e-151">Importar el certificado de cliente de hello en el almacén personal de Hola</span><span class="sxs-lookup"><span data-stu-id="b844e-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="b844e-152">En el Explorador de Windows, haga doble clic en **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="b844e-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="b844e-153">Hola **Asistente para importar certificados** seleccione **usuario actual** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b844e-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="b844e-154">Confirmar la ruta de acceso de archivo de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b844e-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="b844e-155">Escriba la contraseña hello, deje **incluyen todas las propiedades extendidas** activada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b844e-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="b844e-156">Deje **almacén de certificados de hello seleccionar automáticamente [...]**  activada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b844e-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="b844e-157">Haga clic en **Finalizar** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b844e-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="b844e-158">Cargar el servicio de nube de hello PFX archivo toohello</span><span class="sxs-lookup"><span data-stu-id="b844e-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="b844e-159">Vaya toohello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b844e-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b844e-160">Seleccione **Servicios en la nube**.</span><span class="sxs-lookup"><span data-stu-id="b844e-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="b844e-161">Seleccione servicio de nube de Hola que creó anteriormente para el servicio de dividir y combinar Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="b844e-162">Haga clic en **certificados** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="b844e-163">Haga clic en **cargar** en la barra de la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="b844e-164">Seleccione el archivo PFX de hello y escriba Hola misma contraseña anterior.</span><span class="sxs-lookup"><span data-stu-id="b844e-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="b844e-165">Una vez completado, copie huella digital del certificado Hola de nueva entrada de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="b844e-166">Archivo de configuración de servicio de actualización Hola</span><span class="sxs-lookup"><span data-stu-id="b844e-166">Update hello service configuration file</span></span>
<span data-ttu-id="b844e-167">Pegue la huella digital del certificado Hola copiado anteriormente en el atributo/valor de huella digital de Hola de estos valores.</span><span class="sxs-lookup"><span data-stu-id="b844e-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="b844e-168">Para el rol de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="b844e-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b844e-169">Para el rol de hello web:</span><span class="sxs-lookup"><span data-stu-id="b844e-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b844e-170">Tenga en cuenta que para las implementaciones de producción se deben usar certificados independientes para hello entidad emisora de certificados para el cifrado, Hola certificado de servidor y certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="b844e-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="b844e-171">Para obtener instrucciones detalladas al respecto, consulte [Configuración de seguridad](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b844e-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="b844e-172">Implementación del servicio</span><span class="sxs-lookup"><span data-stu-id="b844e-172">Deploy your service</span></span>
1. <span data-ttu-id="b844e-173">Vaya toohello [portal de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b844e-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b844e-174">Haga clic en hello **servicios en la nube** ficha Hola izquierda y seleccione servicio de nube de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b844e-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="b844e-175">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="b844e-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="b844e-176">Elija el entorno de ensayo de hello, a continuación, haga clic en **cargue una nueva implementación de ensayo**.</span><span class="sxs-lookup"><span data-stu-id="b844e-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Ensayo][3]
5. <span data-ttu-id="b844e-178">En el cuadro de diálogo de hello, escriba una etiqueta de implementación.</span><span class="sxs-lookup"><span data-stu-id="b844e-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="b844e-179">Para "Paquete" y "Configuration", haga clic en 'Desde Local' y elija hello **SplitMergeService.cspkg** archivo y el archivo de .cscfg que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b844e-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="b844e-180">Asegurarse de esa casilla de hello **implementar aunque uno o varios roles contengan una sola instancia** está activada.</span><span class="sxs-lookup"><span data-stu-id="b844e-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="b844e-181">Pulse el botón de TIC de hello en la implementación de hello inferior derecho toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="b844e-182">Esperar tootake toocomplete unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b844e-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Cargar][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="b844e-184">Solucionar problemas de implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="b844e-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="b844e-185">Si su rol web se produce un error toocome en línea, es probable que un problema con la configuración de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="b844e-186">Compruebe que Hola que SSL está configurado como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b844e-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="b844e-187">Si se produce un error en el rol de trabajo toocome en línea, pero su rol web se realiza correctamente, es más probable es que un problema de conexión de base de datos de estado de toohello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b844e-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="b844e-188">Asegúrese de que la cadena de conexión de hello en su .cscfg es preciso.</span><span class="sxs-lookup"><span data-stu-id="b844e-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="b844e-189">Compruebe que existen bases de datos y servidor hello, y que los Id. de usuario de Hola y contraseña son correctos.</span><span class="sxs-lookup"><span data-stu-id="b844e-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="b844e-190">Base de datos de SQL Azure, cadena de conexión de hello debería tener Hola forma:</span><span class="sxs-lookup"><span data-stu-id="b844e-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="b844e-191">Asegúrese de no comienza con ese nombre de servidor hello **https://**.</span><span class="sxs-lookup"><span data-stu-id="b844e-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="b844e-192">Asegúrese de que el servidor de base de datos de SQL Azure permite tooit tooconnect de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="b844e-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b844e-193">toodo, abra https://manage.windowsazure.com, haga clic en "Bases de datos de SQL" en hello izquierda, haga clic en "Servidores" en la parte superior de Hola y seleccione el servidor.</span><span class="sxs-lookup"><span data-stu-id="b844e-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="b844e-194">Haga clic en **configurar** en hello principales y asegúrese de que hello **servicios de Azure** opción se establece demasiado "Sí".</span><span class="sxs-lookup"><span data-stu-id="b844e-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="b844e-195">(Consulte los requisitos previos de hello en parte superior de Hola de este artículo).</span><span class="sxs-lookup"><span data-stu-id="b844e-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="b844e-196">Probar la implementación del servicio Hola</span><span class="sxs-lookup"><span data-stu-id="b844e-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="b844e-197">Conexión con un explorador web</span><span class="sxs-lookup"><span data-stu-id="b844e-197">Connect with a web browser</span></span>
<span data-ttu-id="b844e-198">Determinar el punto de conexión de hello web del servicio en la combinación de división.</span><span class="sxs-lookup"><span data-stu-id="b844e-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="b844e-199">Puede encontrar esto en hello Portal clásico de Azure por van toohello **panel** de servicio en la nube y mira **dirección URL del sitio** en el lado derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="b844e-200">Reemplace **http://** con **https://** puesto que la configuración de seguridad predeterminada de hello deshabilita el extremo de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="b844e-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="b844e-201">Página de Hola de carga para esta dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="b844e-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="b844e-202">Pruebas con scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b844e-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="b844e-203">implementación de Hola y el entorno se pueden probar mediante la ejecución de scripts de PowerShell de ejemplo de Hola incluido.</span><span class="sxs-lookup"><span data-stu-id="b844e-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="b844e-204">archivos de script de Hola incluidos son:</span><span class="sxs-lookup"><span data-stu-id="b844e-204">hello script files included are:</span></span>

1. <span data-ttu-id="b844e-205">**SetupSampleSplitMergeEnvironment.ps1** : configura una capa de datos de prueba para División y combinación (consulte la tabla que aparece a continuación para ver una descripción detallada).</span><span class="sxs-lookup"><span data-stu-id="b844e-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="b844e-206">**ExecuteSampleSplitMerge.ps1** -ejecuta operaciones de prueba en pruebas de hello (vea la tabla siguiente para obtener una descripción detallada) de nivel de datos</span><span class="sxs-lookup"><span data-stu-id="b844e-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="b844e-207">**GetMappings.ps1** : nivel superior script que imprima el estado actual de Hola de asignaciones de particiones de Hola de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b844e-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="b844e-208">**ShardManagement.psm1** -script de aplicación auxiliar que ajusta Hola ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="b844e-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="b844e-209">**SqlDatabaseHelpers.psm1**: script auxiliar para crear y administrar bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b844e-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b844e-210">Archivo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b844e-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="b844e-211">Pasos</span><span class="sxs-lookup"><span data-stu-id="b844e-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="b844e-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="b844e-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="b844e-213">Crea una base de datos del administrador de mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="b844e-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b844e-214">Crea dos bases de datos de particiones.</span><span class="sxs-lookup"><span data-stu-id="b844e-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b844e-215">Crea un mapa de particiones para esas bases de datos (elimina todo mapa de particiones existente en esas bases de datos).</span><span class="sxs-lookup"><span data-stu-id="b844e-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b844e-216">Crea una tabla pequeña muestra de las particiones de Hola y rellena la tabla de hello en una de las particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="b844e-217">Declara hello SchemaInfo para tabla particionada Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b844e-218">Archivo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b844e-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="b844e-219">Pasos</span><span class="sxs-lookup"><span data-stu-id="b844e-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="b844e-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="b844e-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="b844e-221">Envía un división solicitud toohello dividir-combinar servicio front-end web, que divide los datos de hello mitad de partición segundo de hello primera partición toohello.</span><span class="sxs-lookup"><span data-stu-id="b844e-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b844e-222">Sondeos hello web front-end para dividir el estado de la solicitud y espera hasta que se complete la solicitud de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b844e-223">Envía un combinación solicitud toohello dividir-combinar servicio front-end web, que mueve los datos de Hola de particiones primera de hello segunda partición toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="b844e-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b844e-224">Sondeos Hola front-end web para el estado de solicitud de combinación de Hola y espera hasta que se complete la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="b844e-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="b844e-225">Usar PowerShell tooverify la implementación</span><span class="sxs-lookup"><span data-stu-id="b844e-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="b844e-226">Abra una nueva ventana de PowerShell, navegue directorio toohello donde descargó el paquete de división y combinación de hello y, a continuación, navegue al directorio de "powershell" Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="b844e-227">Crear un servidor de base de datos de SQL Azure (o elija un servidor existente) donde se creará el Administrador de mapa de particiones de Hola y particiones.</span><span class="sxs-lookup"><span data-stu-id="b844e-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b844e-228">Hola SetupSampleSplitMergeEnvironment.ps1 script crea todas estas bases de datos en hello mismo servidor por script de Hola de tookeep predeterminado simple.</span><span class="sxs-lookup"><span data-stu-id="b844e-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="b844e-229">Esto no es una restricción de hello dividir-combinar servicio propio.</span><span class="sxs-lookup"><span data-stu-id="b844e-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="b844e-230">Un inicio de sesión de autenticación de SQL con toohello de acceso de lectura/escritura que bases de datos serán necesarios para hello dividir-combinar datos de toomove del servicio y actualizar el mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="b844e-231">Puesto que Hola dividir-combinar servicio se ejecuta en la nube de hello, no admite actualmente la autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="b844e-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="b844e-232">Asegúrese de que hello Azure SQL server está configurado tooallow acceso de la dirección IP de Hola de máquina de hello ejecutando estas secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="b844e-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="b844e-233">Puede encontrar esta opción en el servidor de SQL Azure Hola / configuration / direcciones IP permitidas.</span><span class="sxs-lookup"><span data-stu-id="b844e-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="b844e-234">Ejecutar el entorno de ejemplo de Hola SetupSampleSplitMergeEnvironment.ps1 script toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="b844e-235">Ejecutar este script se borran los datos de administración de mapa de particiones existentes estructuras en la base de datos de administrador de mapa de particiones de Hola y particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="b844e-236">Es posible script de Hola toorerun útil si desea inicializar toore mapa de particiones de Hola o particiones.</span><span class="sxs-lookup"><span data-stu-id="b844e-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="b844e-237">Línea de comandos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b844e-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="b844e-238">Ejecute hello Getmappings.ps1 tooview Hola asignaciones de scripts que existen actualmente en el entorno de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="b844e-239">Ejecute hello ExecuteSampleSplitMerge.ps1 script tooexecute una operación de división (mover los datos de hello mitad particiones segunda de hello primera partición toohello) y, a continuación, una operación de combinación (mover datos de hello volver a la primera partición de hello).</span><span class="sxs-lookup"><span data-stu-id="b844e-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="b844e-240">Si ha configurado SSL y deshabilita el punto de conexión del http Hola izquierdo, asegúrese de que usa el punto de conexión de hello https:// en su lugar.</span><span class="sxs-lookup"><span data-stu-id="b844e-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="b844e-241">Línea de comandos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b844e-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="b844e-242">Si recibes hello debajo de error, más probable es que es un problema con el certificado del extremo de la Web.</span><span class="sxs-lookup"><span data-stu-id="b844e-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="b844e-243">Intente conectarse de punto de conexión de toohello Web con su explorador Web favorito y compruebe si hay un error de certificado.</span><span class="sxs-lookup"><span data-stu-id="b844e-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="b844e-244">Si se ha realizado correctamente, la salida de hello debe ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b844e-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="b844e-245">Experimente con otros tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="b844e-245">Experiment with other data types!</span></span> <span data-ttu-id="b844e-246">Todas estas secuencias de toman un parámetro de - ShardKeyType opcional que le permite el tipo de clave toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="b844e-247">valor predeterminado de Hello es Int32, pero también puede especificar Int64, Guid o binario.</span><span class="sxs-lookup"><span data-stu-id="b844e-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="b844e-248">Creación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="b844e-248">Create requests</span></span>
<span data-ttu-id="b844e-249">servicio de Hello puede usarse mediante la interfaz de usuario web de Hola o importar y utilizar el módulo de PowerShell SplitMerge.psm1 Hola que vaya a enviar las solicitudes a través de rol web de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="b844e-250">servicio de Hello puede mover los datos en tablas particionadas y tablas de referencia.</span><span class="sxs-lookup"><span data-stu-id="b844e-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="b844e-251">Una tabla particionada tiene una columna de clave de particionamiento y distintos datos de fila en cada partición.</span><span class="sxs-lookup"><span data-stu-id="b844e-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="b844e-252">Una tabla de referencia no está particionada así que contiene Hola mismo fila de datos en cada partición.</span><span class="sxs-lookup"><span data-stu-id="b844e-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="b844e-253">Tablas de referencia son útiles para los datos que no cambian con frecuencia y es tooJOIN usado con tablas particionadas en las consultas.</span><span class="sxs-lookup"><span data-stu-id="b844e-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="b844e-254">En orden tooperform una operación de combinación de división, debe declarar tablas particionadas hello y tablas de referencia que desee toohave movido.</span><span class="sxs-lookup"><span data-stu-id="b844e-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="b844e-255">Esto se logra con hello **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="b844e-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="b844e-256">Esta API está en hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b844e-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="b844e-257">Para cada tabla particionada, cree un **ShardedTableInfo** objeto que describe el nombre del esquema de la tabla de hello primario (opcional, valor predeterminado es demasiado "dbo"), Hola nombre de la tabla y Hola nombre de columna de la tabla que contiene la clave de particionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="b844e-258">Para cada tabla de referencia, cree una **ReferenceTableInfo** objeto que describe el nombre del esquema de la tabla de hello primario (opcional, valor predeterminado es demasiado "dbo") y el nombre de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="b844e-259">Agregar Hola anteriormente TableInfo objetos tooa nueva **SchemaInfo** objeto.</span><span class="sxs-lookup"><span data-stu-id="b844e-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="b844e-260">Obtener una referencia tooa **ShardMapManager** objeto y llame a **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="b844e-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="b844e-261">Agregar hello **SchemaInfo** toohello **SchemaInfoCollection**, proporcionando el nombre de asignación de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b844e-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="b844e-262">Un ejemplo de esto puede verse en hello SetupSampleSplitMergeEnvironment.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="b844e-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="b844e-263">Hola servicio dividir-combinar no crea bases de datos de destino de hello (o esquema de tablas de base de datos de hello) automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b844e-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="b844e-264">Se deben crear previamente antes de enviar un servicio de toohello de solicitud.</span><span class="sxs-lookup"><span data-stu-id="b844e-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b844e-265">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b844e-265">Troubleshooting</span></span>
<span data-ttu-id="b844e-266">Cuando se ejecuta scripts de powershell de ejemplo de Hola, puede ver Hola mensaje siguiente:</span><span class="sxs-lookup"><span data-stu-id="b844e-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="b844e-267">Este error significa que el certificado SSL no está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b844e-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="b844e-268">Siga las instrucciones de hello en la sección 'Conectar con un explorador web'.</span><span class="sxs-lookup"><span data-stu-id="b844e-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="b844e-269">Si no se pueden enviar solicitudes, verá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b844e-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="b844e-270">En este caso, compruebe el archivo de configuración, en configuración de hello determinado para **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b844e-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="b844e-271">Este error suele indicar que ese rol de trabajo hello no pudo inicializar correctamente base de datos de metadatos de Hola por primera vez.</span><span class="sxs-lookup"><span data-stu-id="b844e-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

