---
title: "Implementación de un servicio de división y combinación | Microsoft Docs"
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
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="4bf5f-103">Implemente un servicio de división y combinación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-103">Deploy a split-merge service</span></span>
<span data-ttu-id="4bf5f-104">La herramienta de división y combinación permite mover los datos entre bases de datos particionadas.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="4bf5f-105">Consulte [Mover datos entre bases de datos en la nube escaladas horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="4bf5f-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="4bf5f-106">Descarga de los paquetes de División y combinación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="4bf5f-107">Descargue la última versión de NuGet desde [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="4bf5f-108">Abra un símbolo del sistema y vaya al directorio al que descargó nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="4bf5f-109">La descarga incluye comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="4bf5f-110">Descargue el paquete de División y combinación más reciente en el directorio actual con el comando que aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="4bf5f-111">Los archivos están ubicados en un directorio llamado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** , donde *x.x.xxx.x* refleja el número de la versión.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="4bf5f-112">Busque los archivos del servicio de división y combinación en el subdirectorio **content\splitmerge\service** y los scripts de Powershell de división y combinación (y las .dll de cliente necesarias) en el subdirectorio **content\splitmerge\powershell**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bf5f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4bf5f-113">Prerequisites</span></span>
1. <span data-ttu-id="4bf5f-114">Cree una base de datos de Base de datos SQL de Azure que se usará como la base de datos de estado de división y combinación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="4bf5f-115">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4bf5f-116">Cree una nueva **Base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="4bf5f-117">Asigne un nombre a la base de datos y cree un nuevo administrador y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="4bf5f-118">Asegúrese de anotar el nombre y la contraseña para usarlos más adelante.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="4bf5f-119">Asegúrese de que el servidor de Base de datos SQL de Azure permite que los servicios de Azure se conecten a él.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="4bf5f-120">En el portal, en **Configuración de firewall**, asegúrese de que la opción **Permitir el acceso a servicios de Azure** esté establecida en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="4bf5f-121">Haga clic en el icono de "guardar".</span><span class="sxs-lookup"><span data-stu-id="4bf5f-121">Click the "save" icon.</span></span>
   
   ![Servicios permitidos][1]
3. <span data-ttu-id="4bf5f-123">Cree una cuenta de almacenamiento de Azure que se usará para la salida de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="4bf5f-124">Vaya al Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-124">Go to the Azure Portal.</span></span> <span data-ttu-id="4bf5f-125">En la barra de la izquierda, haga clic en **Nuevo**, en **Datos + almacenamiento** y en **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="4bf5f-126">Cree un servicio en la nube de Azure que contendrá el servicio de División y combinación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="4bf5f-127">Vaya al Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-127">Go to the Azure Portal.</span></span> <span data-ttu-id="4bf5f-128">En la barra de la izquierda, haga clic en **Nuevo**, en **Proceso**, en **Servicio en la nube** y en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="4bf5f-129">Configuración del servicio de división y combinación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="4bf5f-130">Configuración del servicio División y combinación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="4bf5f-131">En la carpeta donde ha descargado los ensamblados de división y combinación, cree una copia del archivo **ServiceConfiguration.Template.cscfg** que se suministra junto a **SplitMergeService.cspkg** y cámbiele el nombre por **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="4bf5f-132">Abra **ServiceConfiguration.cscfg** en un editor de texto como Visual Studio que permite validar las entradas como el formato de las huellas digitales de certificados.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="4bf5f-133">Cree una nueva base de datos o elija una base de datos existente que sirva como la base de datos de estado para las operaciones de división y combinación y recupere la cadena de conexión de esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="4bf5f-134">En este momento, la base de datos de estado debe usar la intercalación latina (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="4bf5f-135">Para obtener más información, vea [Nombre de intercalación de Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="4bf5f-136">Con Base de datos SQL de Azure, la cadena de conexión suele tener el formato:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="4bf5f-137">Escriba esta cadena de conexión en el archivo cscfg en las secciones de roles **SplitMergeWeb** y **SplitMergeWorker** en la configuración de ElasticScaleMetadata.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="4bf5f-138">Para el rol **SplitMergeWorker**, escriba una cadena de conexión válida en Azure Storage para la configuración **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="4bf5f-139">Configuración de seguridad</span><span class="sxs-lookup"><span data-stu-id="4bf5f-139">Configure security</span></span>
<span data-ttu-id="4bf5f-140">Para obtener instrucciones detalladas para configurar la seguridad del servicio, consulte [Configuración de seguridad de división y combinación](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="4bf5f-141">Para fines de una simple implementación de prueba para este tutorial, se realizará un conjunto mínimo de pasos de configuración para configurar y ejecutar el servicio.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="4bf5f-142">Estos pasos solo habilitan la máquina/cuenta que los ejecuta para comunicarse con el servicio.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="4bf5f-143">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="4bf5f-143">Create a self-signed certificate</span></span>
<span data-ttu-id="4bf5f-144">Cree un directorio nuevo y desde este directorio ejecute el siguiente comando usando una ventana de [Símbolo del sistema para desarrolladores para Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) :</span><span class="sxs-lookup"><span data-stu-id="4bf5f-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="4bf5f-145">Se le pedirá que escriba una contraseña para proteger la clave privada.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="4bf5f-146">Escriba una contraseña segura y confírmela.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="4bf5f-147">Luego se le pedirá que escriba nuevamente la contraseña.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="4bf5f-148">Haga clic en **Sí** al final para importarla al almacén Raíz de Entidades de certificación de confianza.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="4bf5f-149">Creación de un archivo PFX</span><span class="sxs-lookup"><span data-stu-id="4bf5f-149">Create a PFX file</span></span>
<span data-ttu-id="4bf5f-150">Ejecute el siguiente comando desde la misma ventana donde se ejecutó makecert; use la misma contraseña que usó para crear el certificado:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="4bf5f-151">Importación del certificado de cliente al almacén Personal</span><span class="sxs-lookup"><span data-stu-id="4bf5f-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="4bf5f-152">En el Explorador de Windows, haga doble clic en **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="4bf5f-153">En el **Asistente para importar certificados**, seleccione **Usuario actual** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="4bf5f-154">Confirme la ruta del archivo y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="4bf5f-155">Escriba la contraseña, deje activada la opción **Incluir todas las propiedades extendidas** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="4bf5f-156">Deje activada la opción **Seleccionar automáticamente el almacén de certificados…** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="4bf5f-157">Haga clic en **Finalizar** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="4bf5f-158">Carga del archivo PFX al servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="4bf5f-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="4bf5f-159">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4bf5f-160">Seleccione **Servicios en la nube**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="4bf5f-161">Seleccione el servicio en la nube que creó anteriormente para el servicio División y combinación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="4bf5f-162">Haga clic en **Certificados** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="4bf5f-163">Haga clic en **Cargar** en la barra inferior.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="4bf5f-164">Seleccione el archivo PFX y escriba la misma contraseña anterior.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="4bf5f-165">Una vez realizado, copie la huella digital del certificado desde la entrada nueva en la lista.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="4bf5f-166">Actualizar el archivo de configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="4bf5f-166">Update the service configuration file</span></span>
<span data-ttu-id="4bf5f-167">Pegue la huella digital del certificado copiada anteriormente en el atributo de huella digital/valor de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="4bf5f-168">Para el rol de trabajo:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="4bf5f-169">Para el rol web:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="4bf5f-170">Tenga en cuenta que para las implementaciones de producción se deben usar certificados independientes para la CA, para cifrado, el certificado de servidor y los certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="4bf5f-171">Para obtener instrucciones detalladas al respecto, consulte [Configuración de seguridad](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="4bf5f-172">Implementación del servicio</span><span class="sxs-lookup"><span data-stu-id="4bf5f-172">Deploy your service</span></span>
1. <span data-ttu-id="4bf5f-173">Vaya al [Portal de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4bf5f-174">Haga clic en la pestaña **Servicios en la nube** que aparece a la izquierda y seleccione el servicio en la nube que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="4bf5f-175">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="4bf5f-176">Elija el entorno de ensayo y, a continuación, haga clic en **Cargar una nueva implementación de ensayo**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Ensayo][3]
5. <span data-ttu-id="4bf5f-178">En el cuadro de diálogo, escriba una etiqueta de implementación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="4bf5f-179">Para "Paquete" y "Configuración", haga clic en "Desde local" y elija el archivo **SplitMergeService.cspkg** y el archivo .cscfg que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="4bf5f-180">Asegúrese de que la casilla de verificación con la etiqueta **Implementar aunque uno o varios roles contengan una sola instancia esté activada** .</span><span class="sxs-lookup"><span data-stu-id="4bf5f-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="4bf5f-181">Presione el botón de verificación que aparece en la esquina inferior derecha para comenzar la implementación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="4bf5f-182">Tenga en cuenta que puede tardar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-182">Expect it to take a few minutes to complete.</span></span>

   ![Cargar][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="4bf5f-184">Solución de problemas de la implementación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="4bf5f-185">Si el rol web no puede ponerse en línea, probablemente haya un problema con la configuración de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="4bf5f-186">Compruebe que SSL esté configurado como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="4bf5f-187">Si el rol de trabajo no puede ponerse en línea, pero el rol web sí, probablemente se trate de un problema al conectarse a la base de datos de estado que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="4bf5f-188">Asegúrese de que la cadena de conexión en el archivo .cscfg esté correcta.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="4bf5f-189">Compruebe que existan el servidor y la base de datos y de que el identificador de usuario y la contraseña estén correctos.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="4bf5f-190">En el caso de Base de datos SQL de Azure, la cadena de conexión debe tener el formato:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="4bf5f-191">Asegúrese de que el nombre del servidor no comience por **https://**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="4bf5f-192">Asegúrese de que el servidor de Base de datos SQL de Azure permite que los servicios de Azure se conecten a él.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="4bf5f-193">Para ello, abra https://manage.windowsazure.com, haga clic en "Bases de datos SQL" a la izquierda, haga clic en "Servidores" en la parte superior y, a continuación, seleccione su servidor.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="4bf5f-194">Haga clic en **Configurar** en la parte superior para asegurarse de que el valor **Servicios de Microsoft Azure** esté establecido en "Sí".</span><span class="sxs-lookup"><span data-stu-id="4bf5f-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="4bf5f-195">(Consulte la sección Requisitos previos al principio de este artículo).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="4bf5f-196">Prueba de la implementación del servicio</span><span class="sxs-lookup"><span data-stu-id="4bf5f-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="4bf5f-197">Conexión con un explorador web</span><span class="sxs-lookup"><span data-stu-id="4bf5f-197">Connect with a web browser</span></span>
<span data-ttu-id="4bf5f-198">Determine el extremo web de su servicio División y combinación.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="4bf5f-199">Para averiguar esto, vaya al Portal de Azure clásico, seleccione el **Panel** de su servicio en la nube y busque en **Dirección URL del sitio** en el lado derecho.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="4bf5f-200">Reemplace **http://** por **https://**, dado que la configuración de seguridad predeterminada deshabilita el punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="4bf5f-201">Cargue la página de esta dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="4bf5f-202">Pruebas con scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bf5f-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="4bf5f-203">Puede probar la implementación y su entorno si ejecuta los scripts de PowerShell de ejemplo incluidos.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="4bf5f-204">Los archivos de script incluidos son:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-204">The script files included are:</span></span>

1. <span data-ttu-id="4bf5f-205">**SetupSampleSplitMergeEnvironment.ps1** : configura una capa de datos de prueba para División y combinación (consulte la tabla que aparece a continuación para ver una descripción detallada).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="4bf5f-206">**ExecuteSampleSplitMerge.ps1** : ejecuta operaciones de prueba en la capa de datos de prueba (consulte la tabla que aparece a continuación para ver una descripción detallada).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="4bf5f-207">**GetMappings.ps1**: script de muestra de nivel superior que imprime el estado actual de las asignaciones de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="4bf5f-208">**ShardManagement.psm1**: script auxiliar que incluye la API de ShardManagement.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="4bf5f-209">**SqlDatabaseHelpers.psm1**: script auxiliar para crear y administrar bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="4bf5f-210">Archivo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bf5f-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="4bf5f-211">Pasos</span><span class="sxs-lookup"><span data-stu-id="4bf5f-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="4bf5f-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="4bf5f-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="4bf5f-213">Crea una base de datos del administrador de mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="4bf5f-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="4bf5f-214">Crea dos bases de datos de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="4bf5f-215">Crea un mapa de particiones para esas bases de datos (elimina todo mapa de particiones existente en esas bases de datos).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="4bf5f-216">Crea una pequeña tabla de ejemplo en las particiones y rellena la tabla en una de las particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="4bf5f-217">Declara la SchemaInfo para la tabla particionada.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="4bf5f-218">Archivo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bf5f-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="4bf5f-219">Pasos</span><span class="sxs-lookup"><span data-stu-id="4bf5f-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="4bf5f-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="4bf5f-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="4bf5f-221">Envía una solicitud de división al front-end web del servicio división-combinación, que divide la mitad de los datos entre la primera partición y la segunda.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="4bf5f-222">Sondea el front-end web para ver el estado de la solicitud de división y espera hasta que se complete la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="4bf5f-223">Envía una solicitud de combinación al front-end del servicio División y combinación, que mueve los datos desde la segunda partición de vuelta a la primera partición.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="4bf5f-224">Sondea el front-end web para ver el estado de la solicitud de combinación y espera hasta que se complete la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="4bf5f-225">Uso de PowerShell para comprobar la implementación</span><span class="sxs-lookup"><span data-stu-id="4bf5f-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="4bf5f-226">Abra una nueva ventana de PowerShell y vaya al directorio al que descargó el paquete División y combinación y, a continuación, vaya al directorio "powershell".</span><span class="sxs-lookup"><span data-stu-id="4bf5f-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="4bf5f-227">Cree un servidor de base de datos SQL de Azure (o elija un servidor existente) en el que se crearán las particiones y el administrador de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4bf5f-228">el script SetupSampleSplitMergeEnvironment.ps1 crea todas estas bases de datos en el mismo servidor de manera predeterminada para que el script sea simple.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="4bf5f-229">Esta no es una restricción del servicio División y combinación mismo.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="4bf5f-230">Se requerirá un inicio de sesión de autenticación de SQL con acceso de lectura/escritura a las bases de datos para que el servicio División y combinación mueva los datos y actualice el mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="4bf5f-231">Debido a que el servicio División y combinación se ejecuta en la nube, actualmente no es compatible con Autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="4bf5f-232">Asegúrese de que el servidor SQL de Azure esté configurado para permitir el acceso desde la dirección IP dela máquina que ejecuta estos scripts.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="4bf5f-233">Puede encontrar esta configuración en Servidor SQL de Azure / Configuración / Direcciones IP permitidas.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="4bf5f-234">Ejecute el script SetupSampleSplitMergeEnvironment.ps1 para crear el entorno de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="4bf5f-235">Ejecutar este script eliminará toda estructura de datos de administrador del mapa de particiones existente en la base de datos del administrador de mapa de particiones y las particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="4bf5f-236">Puede ser útil volver a ejecutar el script si desea volver a inicializar las particiones o el mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="4bf5f-237">Línea de comandos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="4bf5f-238">Ejecute el script Getmappings.ps1 para ver las asignaciones que existen actualmente en el entorno de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="4bf5f-239">Ejecute el script ExecuteSampleSplitMerge.ps1 para ejecutar una operación de división (moviendo la mitad de los datos de la primera partición a la segunda partición) y luego una operación de combinación (moviendo los datos de vuelta a la primera partición).</span><span class="sxs-lookup"><span data-stu-id="4bf5f-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="4bf5f-240">Si configuró SSL y dejó deshabilitado el extremo http, asegúrese de usar el extremo https://.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="4bf5f-241">Línea de comandos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="4bf5f-242">Si recibe el siguiente error, es muy probable que se trate de un problema con el certificado de su extremo web.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="4bf5f-243">Intente conectarse al extremo web con el explorador web de su preferencia y revise si hay un error en el certificado.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="4bf5f-244">Si está correcto, el resultado debiera verse de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="4bf5f-245">Experimente con otros tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-245">Experiment with other data types!</span></span> <span data-ttu-id="4bf5f-246">Todos estos scripts tienen un parámetro -ShardKeyType opcional que le permite especificar el tipo de clave.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="4bf5f-247">El valor predeterminado es Int32, pero también puede especificar Int64, Guid o Binary.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="4bf5f-248">Creación de solicitudes</span><span class="sxs-lookup"><span data-stu-id="4bf5f-248">Create requests</span></span>
<span data-ttu-id="4bf5f-249">El servicio se puede utilizar mediante la interfaz de usuario web o importando y utilizando el módulo de PowerShell SplitMerge.psm1 que enviará sus solicitudes a través del rol web.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="4bf5f-250">El servicio puede mover los datos de las tablas particionadas y de las tablas de referencia.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="4bf5f-251">Una tabla particionada tiene una columna de clave de particionamiento y distintos datos de fila en cada partición.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="4bf5f-252">Una tabla de referencia no está particionada, por lo que contiene los mismos datos de fila en cada partición.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="4bf5f-253">Las tablas de referencia son útiles para los datos que no cambian con frecuencia y que se usan para UNIRSE con tablas particionadas en consultas.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="4bf5f-254">Para realizar una operación de división y combinación, debe declarar las tablas particionadas y las tablas de referencia que desea mover.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="4bf5f-255">Esto se realiza con la API **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="4bf5f-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="4bf5f-256">Esta API está en el espacio de nombres **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** .</span><span class="sxs-lookup"><span data-stu-id="4bf5f-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="4bf5f-257">Para cada tabla particionada, cree un objeto **ShardedTableInfo** que describa el nombre del esquema principal de la tabla (opcional, se define de manera predeterminada en "dbo"), el nombre de la tabla y el nombre de la columna de esa tabla que contiene la clave de particionamiento.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="4bf5f-258">Para cada tabla de referencia, cree un objeto **ReferenceTableInfo** que describa el nombre del esquema principal de la tabla (opcional, se define de manera predeterminada en "dbo") y el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="4bf5f-259">Agregue los objetos TableInfo anteriores a un nuevo objeto **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="4bf5f-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="4bf5f-260">Obtenga una referencia a un objeto **ShardMapManager** y llame a **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="4bf5f-261">Agregue **SchemaInfo** a **SchemaInfoCollection** y proporcione el nombre del mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="4bf5f-262">Es posible ver un ejemplo de esto en el script SetupSampleSplitMergeEnvironment.ps1.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="4bf5f-263">El servicio División y combinación no crea la base de datos de destino (o esquema para cualquier tabla de la base de datos) por usted.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="4bf5f-264">Deben crearse previamente antes de enviar una solicitud al servicio.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4bf5f-265">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="4bf5f-265">Troubleshooting</span></span>
<span data-ttu-id="4bf5f-266">Es posible que cuando ejecute los scripts de ejemplo de PowerShell vea el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="4bf5f-267">Este error significa que el certificado SSL no está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="4bf5f-268">Siga las instrucciones que aparecen en la sección "Conexión con un explorador web".</span><span class="sxs-lookup"><span data-stu-id="4bf5f-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="4bf5f-269">Si no se pueden enviar solicitudes, verá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4bf5f-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="4bf5f-270">En este caso, compruebe el archivo de configuración, en particular la configuración de **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="4bf5f-271">Este error normalmente indica que el rol de trabajo no pudo inicializar correctamente la base de datos de metadatos la primera vez.</span><span class="sxs-lookup"><span data-stu-id="4bf5f-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

