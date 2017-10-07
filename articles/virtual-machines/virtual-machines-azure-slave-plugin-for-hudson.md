---
title: "aaaHow toouse hello Azure esclavo complemento con integración continua Hudson | Documentos de Microsoft"
description: "Describe cómo toouse hello Azure subordinado complemento con integración continua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="7f36d-103">¿Cómo toouse hello Azure subordinado complemento con integración continua Hudson</span><span class="sxs-lookup"><span data-stu-id="7f36d-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="7f36d-104">Hello Azure esclavo complemento para Hudson permite nodos de tooprovision esclavo en Azure cuando ejecuta distribuida compila.</span><span class="sxs-lookup"><span data-stu-id="7f36d-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="7f36d-105">Instalar hello Azure esclavo complemento</span><span class="sxs-lookup"><span data-stu-id="7f36d-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="7f36d-106">En el panel de Hudson hello, haga clic en **administrar Hudson**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="7f36d-107">Hola **administrar Hudson** página, haga clic en **administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="7f36d-108">Haga clic en hello **disponible** ficha.</span><span class="sxs-lookup"><span data-stu-id="7f36d-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="7f36d-109">Haga clic en **búsqueda** y tipo **Azure** toolimit Hola lista toorelevant complementos.</span><span class="sxs-lookup"><span data-stu-id="7f36d-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="7f36d-110">Si decide tooscroll a través de la lista de Hola de complementos disponibles, encontrará hello Azure esclavo complemento en hello **administración del clúster y distribuidas compilar** sección Hola **otros** ficha.</span><span class="sxs-lookup"><span data-stu-id="7f36d-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="7f36d-111">Casilla de Hola de **Azure esclavo complemento**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="7f36d-112">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-112">Click **Install**.</span></span>
7. <span data-ttu-id="7f36d-113">Reinicie Hudson.</span><span class="sxs-lookup"><span data-stu-id="7f36d-113">Restart Hudson.</span></span>

<span data-ttu-id="7f36d-114">Ahora se instala dicho complemento hello, pasos de Hola sería tooconfigure Hola complemento con el perfil de suscripción de Azure y toocreate una plantilla que se utilizará en la creación de hello VM para el nodo de esclavo Hola.</span><span class="sxs-lookup"><span data-stu-id="7f36d-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="7f36d-115">Configurar hello Azure esclavo complemento con el perfil de suscripción</span><span class="sxs-lookup"><span data-stu-id="7f36d-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="7f36d-116">Un perfil de suscripción, también denominados tooas configuración de publicación, es un archivo XML que contiene credenciales seguras e información adicional que necesitará toowork con Azure en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="7f36d-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="7f36d-117">Hola tooconfigure Azure esclavo complemento, debe:</span><span class="sxs-lookup"><span data-stu-id="7f36d-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="7f36d-118">Su id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="7f36d-118">Your subscription id</span></span>
* <span data-ttu-id="7f36d-119">Un certificado de administración para la suscripción</span><span class="sxs-lookup"><span data-stu-id="7f36d-119">A management certificate for your subscription</span></span>

<span data-ttu-id="7f36d-120">Estos se pueden encontrar en su [perfil de suscripción].</span><span class="sxs-lookup"><span data-stu-id="7f36d-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="7f36d-121">A continuación se muestra un ejemplo de un perfil de suscripción.</span><span class="sxs-lookup"><span data-stu-id="7f36d-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="7f36d-122">Una vez que tenga su perfil de suscripción, siga estos Hola de tooconfigure pasos Azure esclavo de complemento.</span><span class="sxs-lookup"><span data-stu-id="7f36d-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="7f36d-123">En el panel de Hudson hello, haga clic en **administrar Hudson**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="7f36d-124">Haga clic en **Configure System**(Configurar sistema).</span><span class="sxs-lookup"><span data-stu-id="7f36d-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="7f36d-125">Desplácese hacia abajo Hola de hello página toofind **nube** sección.</span><span class="sxs-lookup"><span data-stu-id="7f36d-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="7f36d-126">Haga clic en **Add new cloud > Microsoft Azure** (Agregar nueva nube > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="7f36d-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![agregar nube nueva][add new cloud]
   
    <span data-ttu-id="7f36d-128">Esto mostrará los campos de hello en las que necesite tooenter los detalles de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="7f36d-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![configurar perfil][configure profile]
5. <span data-ttu-id="7f36d-130">Copie el certificado de administración y el Id. de suscripción Hola de su perfil de suscripción y péguelos en los campos correspondientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f36d-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="7f36d-131">Cuando se copian el certificado de administración y el Id. de suscripción hello, **no** incluidas Hola comillas que delimitan los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="7f36d-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="7f36d-132">Haga clic en **Verify configuration**(Comprobar configuración).</span><span class="sxs-lookup"><span data-stu-id="7f36d-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="7f36d-133">Cuando se comprobó correctamente la configuración de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="7f36d-134">Configurar una plantilla de máquina virtual para hello Azure esclavo complemento</span><span class="sxs-lookup"><span data-stu-id="7f36d-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="7f36d-135">Una plantilla de máquina virtual define parámetros Hola Hola complemento utilizará toocreate un nodo subordinado en Azure.</span><span class="sxs-lookup"><span data-stu-id="7f36d-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="7f36d-136">Hola pasos se podrá crear plantilla para una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7f36d-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="7f36d-137">En el panel de Hudson hello, haga clic en **administrar Hudson**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="7f36d-138">Haga clic en **Configure System**(Configurar sistema).</span><span class="sxs-lookup"><span data-stu-id="7f36d-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="7f36d-139">Desplácese hacia abajo Hola de hello página toofind **nube** sección.</span><span class="sxs-lookup"><span data-stu-id="7f36d-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="7f36d-140">Dentro de hello **nube** sección, busque **Agregar plantilla de máquina Virtual de Azure** y haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="7f36d-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![agregar plantilla de vm][add vm template]
5. <span data-ttu-id="7f36d-142">Especifique un nombre de servicio de nube en hello **nombre** campo.</span><span class="sxs-lookup"><span data-stu-id="7f36d-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="7f36d-143">Si se especifica el nombre de Hola hace referencia tooan existente de servicio en la nube, se aprovisionará Hola VM en ese servicio.</span><span class="sxs-lookup"><span data-stu-id="7f36d-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="7f36d-144">De lo contrario, Azure creará uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="7f36d-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="7f36d-145">Hola **descripción** , a continuación, escriba el texto que describe la plantilla de Hola que está creando.</span><span class="sxs-lookup"><span data-stu-id="7f36d-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="7f36d-146">Esta información es solo para fines documentales y no se usa en el aprovisionamiento de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="7f36d-147">Hola **etiquetas** , escriba **linux**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="7f36d-148">Esta etiqueta es tooidentify usado Hola plantilla que está creando y es la plantilla de Hola de tooreference posteriormente usado cuando se crea un trabajo Hudson.</span><span class="sxs-lookup"><span data-stu-id="7f36d-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="7f36d-149">Seleccione una región donde se creará Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="7f36d-150">Seleccione el tamaño de VM apropiado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f36d-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="7f36d-151">Especifique una cuenta de almacenamiento donde se creará Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="7f36d-152">Asegúrese de que se encuentra en hello misma región que el servicio de nube de Hola que vamos a usar.</span><span class="sxs-lookup"><span data-stu-id="7f36d-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="7f36d-153">Si desea que el nuevo toobe de almacenamiento creado, puede dejar este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="7f36d-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="7f36d-154">Tiempo de retención especifica Hola minutos antes de Hudson elimina a un esclavo inactivo.</span><span class="sxs-lookup"><span data-stu-id="7f36d-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="7f36d-155">Dejarlo en el valor predeterminado de Hola de 60.</span><span class="sxs-lookup"><span data-stu-id="7f36d-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="7f36d-156">En **uso**, seleccione Hola condición adecuada cuando se usará este nodo subordinado.</span><span class="sxs-lookup"><span data-stu-id="7f36d-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="7f36d-157">Por ahora, seleccione **Utilize this node as much as possible**(Usar este nodo tanto como sea posible).</span><span class="sxs-lookup"><span data-stu-id="7f36d-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="7f36d-158">En este momento, el formulario sería toothis similar:</span><span class="sxs-lookup"><span data-stu-id="7f36d-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![configuración de plantilla][template config]
13. <span data-ttu-id="7f36d-160">En **familia de imagen o identificador** tiene toospecify qué imagen de sistema se instalará en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="7f36d-161">Puede seleccionar de una lista de familias de imagen o especificar una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="7f36d-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="7f36d-162">Si desea tooselect en una lista de familias de imagen, escriba Hola primer carácter (distingue mayúsculas de minúsculas) del nombre de familia de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f36d-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="7f36d-163">Por ejemplo, al escribir **U** aparecerá una lista de familias de Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="7f36d-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="7f36d-164">Una vez que selecciona en la lista de Hola, Jenkins usará versión más reciente de Hola de esa imagen de sistema de esa familia al aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![lista de familias de SO][OS family list]
    
     <span data-ttu-id="7f36d-166">Si tiene una imagen personalizada que desee toouse en su lugar, escriba el nombre de Hola de esa imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="7f36d-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="7f36d-167">Nombres de imagen personalizada no se muestran en una lista por lo que tendrá tooensure que Hola nombre está escrito correctamente.</span><span class="sxs-lookup"><span data-stu-id="7f36d-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="7f36d-168">Para este tutorial, escriba **U** toobring una lista de imágenes de Ubuntu y seleccione **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="7f36d-169">Para **Launch method** (Método de inicio), seleccione **SSH**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="7f36d-170">Copie el siguiente script de Hola y pegue en hello **Init script** campo.</span><span class="sxs-lookup"><span data-stu-id="7f36d-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="7f36d-171">Hola **Init script** se ejecutará después de Hola se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="7f36d-172">En este ejemplo, el script de Hola instala ant, Java y git.</span><span class="sxs-lookup"><span data-stu-id="7f36d-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="7f36d-173">Hola **nombre de usuario** y **contraseña** campos, escriba los valores preferidos para cuenta de administrador de Hola que se creará en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f36d-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="7f36d-174">Haga clic en **comprobar plantilla** toocheck si los parámetros de hello especificados son válidos.</span><span class="sxs-lookup"><span data-stu-id="7f36d-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="7f36d-175">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="7f36d-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="7f36d-176">Creación de un trabajo de Hudson que se ejecuta en un nodo subordinado en Azure</span><span class="sxs-lookup"><span data-stu-id="7f36d-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="7f36d-177">En esta sección, creará una tarea de Hudson que se ejecutará en un nodo subordinado en Azure.</span><span class="sxs-lookup"><span data-stu-id="7f36d-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="7f36d-178">En el panel de Hudson hello, haga clic en **nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="7f36d-179">Escriba un nombre para el trabajo de Hola que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="7f36d-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="7f36d-180">Para el tipo de trabajo de hello, seleccione **crear un trabajo de estilo libre software**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="7f36d-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-181">Click **OK**.</span></span>
5. <span data-ttu-id="7f36d-182">En la página de configuración del trabajo de hello, seleccione **restringir donde se puede ejecutar este proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="7f36d-183">Seleccione **menú de nodo y la etiqueta** y seleccione **linux** (se especifica esta etiqueta cuando se crea la plantilla de máquina virtual de hello en la sección anterior de hello).</span><span class="sxs-lookup"><span data-stu-id="7f36d-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="7f36d-184">Hola **generar** sección, haga clic en **agregar el paso de compilación** y seleccione **ejecutar shell**.</span><span class="sxs-lookup"><span data-stu-id="7f36d-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="7f36d-185">Editar Hola siguiente secuencia de comandos, reemplazando **{su nombre de cuenta de github}**, **{el nombre del proyecto}**, y **{el directorio del proyecto}** con los valores adecuados y pegue Hola Editar script Hola área de texto que aparece.</span><span class="sxs-lookup"><span data-stu-id="7f36d-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="7f36d-186">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="7f36d-186">Click on **Save**.</span></span>
10. <span data-ttu-id="7f36d-187">En Hola panel Hudson, busque el trabajo de Hola que acaba de crear y haga clic en hello **programar una compilación** icono.</span><span class="sxs-lookup"><span data-stu-id="7f36d-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="7f36d-188">Hudson después creará un nodo subordinado con plantilla Hola creado en la sección anterior de Hola y ejecutar script de Hola que especificó en el paso de compilación de Hola para esta tarea.</span><span class="sxs-lookup"><span data-stu-id="7f36d-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f36d-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f36d-189">Next Steps</span></span>
<span data-ttu-id="7f36d-190">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="7f36d-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[perfil de suscripción]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

