---
title: "Uso del complemento para máquinas subordinadas de Azure con Hudson Continuous Integration | Microsoft Docs"
description: "Describe cómo usar el complemento esclavo de Azure con Hudson Continuous Integration."
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
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="ac98c-103">Uso del complemento esclavo de Azure con Hudson Continuous Integration</span><span class="sxs-lookup"><span data-stu-id="ac98c-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="ac98c-104">El complemento esclavo de Azure para Hudson le permite aprovisionar los nodos subordinados en Azure cuando se ejecutan compilaciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="ac98c-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="ac98c-105">Instalación del complemento subordinado de Azure</span><span class="sxs-lookup"><span data-stu-id="ac98c-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="ac98c-106">En el panel de Hudson, haga clic en **Manage Hudson**(Administrar Hudson).</span><span class="sxs-lookup"><span data-stu-id="ac98c-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ac98c-107">En la página **Manage Hudson** (Administrar Hudson), haga clic en **Manage Plugins** (Administrar complementos).</span><span class="sxs-lookup"><span data-stu-id="ac98c-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="ac98c-108">Haga clic en la pestaña **Available** (Disponible).</span><span class="sxs-lookup"><span data-stu-id="ac98c-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="ac98c-109">Haga clic en **Buscar** y escriba **Azure** para limitar la lista de complementos pertinentes.</span><span class="sxs-lookup"><span data-stu-id="ac98c-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="ac98c-110">Si opta por desplazarse por la lista de complementos disponibles, encontrará el complemento para máquinas subordinadas de Azure en la sección **Cluster Management and Distributed Build** (Administración de clústeres y compilación distribuida) de la pestaña **Others** (Otros).</span><span class="sxs-lookup"><span data-stu-id="ac98c-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="ac98c-111">Active la casilla **Azure Slave Plugin**(Complemento esclavo de Azure).</span><span class="sxs-lookup"><span data-stu-id="ac98c-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="ac98c-112">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ac98c-112">Click **Install**.</span></span>
7. <span data-ttu-id="ac98c-113">Reinicie Hudson.</span><span class="sxs-lookup"><span data-stu-id="ac98c-113">Restart Hudson.</span></span>

<span data-ttu-id="ac98c-114">Ahora que está instalado el complemento, los siguientes pasos serían configurarlo con el perfil de suscripción de Azure y crear una plantilla que se usará en la creación de la máquina virtual para el nodo subordinado.</span><span class="sxs-lookup"><span data-stu-id="ac98c-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="ac98c-115">Configuración del complemento esclavo de Azure con el perfil de suscripción</span><span class="sxs-lookup"><span data-stu-id="ac98c-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="ac98c-116">Un perfil de suscripción, también conocido como configuración de publicación, es un archivo XML que contiene credenciales seguras y alguna información adicional que necesitará para trabajar con Azure en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ac98c-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="ac98c-117">Para configurar el complemento esclavo de Azure, necesitará:</span><span class="sxs-lookup"><span data-stu-id="ac98c-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="ac98c-118">Su id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="ac98c-118">Your subscription id</span></span>
* <span data-ttu-id="ac98c-119">Un certificado de administración para la suscripción</span><span class="sxs-lookup"><span data-stu-id="ac98c-119">A management certificate for your subscription</span></span>

<span data-ttu-id="ac98c-120">Estos se pueden encontrar en su [perfil de suscripción].</span><span class="sxs-lookup"><span data-stu-id="ac98c-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="ac98c-121">A continuación se muestra un ejemplo de un perfil de suscripción.</span><span class="sxs-lookup"><span data-stu-id="ac98c-121">Below is an example of a subscription profile.</span></span>

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

<span data-ttu-id="ac98c-122">Una vez que tiene el perfil de suscripción, siga estos pasos para configurar el complemento esclavo de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac98c-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="ac98c-123">En el panel de Hudson, haga clic en **Manage Hudson**(Administrar Hudson).</span><span class="sxs-lookup"><span data-stu-id="ac98c-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ac98c-124">Haga clic en **Configure System**(Configurar sistema).</span><span class="sxs-lookup"><span data-stu-id="ac98c-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="ac98c-125">Desplácese hacia abajo en la página para encontrar la sección **Cloud** (Nube).</span><span class="sxs-lookup"><span data-stu-id="ac98c-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="ac98c-126">Haga clic en **Add new cloud > Microsoft Azure** (Agregar nueva nube > Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="ac98c-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![agregar nube nueva][add new cloud]
   
    <span data-ttu-id="ac98c-128">Se mostrarán los campos donde debe especificar los detalles de suscripción.</span><span class="sxs-lookup"><span data-stu-id="ac98c-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![configurar perfil][configure profile]
5. <span data-ttu-id="ac98c-130">Copie el certificado de administración y el id. de suscripción del perfil de suscripción y péguelos en los campos correspondientes.</span><span class="sxs-lookup"><span data-stu-id="ac98c-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="ac98c-131">Al copiar el certificado de administración y el identificador de suscripción, **no** incluya las comillas que delimitan los valores.</span><span class="sxs-lookup"><span data-stu-id="ac98c-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="ac98c-132">Haga clic en **Verify configuration**(Comprobar configuración).</span><span class="sxs-lookup"><span data-stu-id="ac98c-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="ac98c-133">Cuando se compruebe que la configuración es correcta, haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="ac98c-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="ac98c-134">Configuración de una plantilla de máquina virtual para el complemento esclavo de Azure</span><span class="sxs-lookup"><span data-stu-id="ac98c-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="ac98c-135">Una plantilla de máquina virtual define los parámetros que usará el complemento para crear un nodo subordinado en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac98c-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="ac98c-136">En los pasos siguientes crearemos plantilla para una VM de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ac98c-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="ac98c-137">En el panel de Hudson, haga clic en **Manage Hudson**(Administrar Hudson).</span><span class="sxs-lookup"><span data-stu-id="ac98c-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ac98c-138">Haga clic en **Configure System**(Configurar sistema).</span><span class="sxs-lookup"><span data-stu-id="ac98c-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="ac98c-139">Desplácese hacia abajo en la página para encontrar la sección **Cloud** (Nube).</span><span class="sxs-lookup"><span data-stu-id="ac98c-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="ac98c-140">Dentro de la sección **Cloud** (Nube), busque **Add Azure Virtual Machine Template** (Agregar plantilla de máquina virtual de Azure) y haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="ac98c-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![agregar plantilla de vm][add vm template]
5. <span data-ttu-id="ac98c-142">Especifique un nombre de servicio en la nube en el campo **Name** (Nombre).</span><span class="sxs-lookup"><span data-stu-id="ac98c-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="ac98c-143">Si el nombre que especifique se refiere a un servicio en la nube existente, la máquina virtual se aprovisionará en dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="ac98c-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="ac98c-144">De lo contrario, Azure creará uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="ac98c-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="ac98c-145">En el campo **Description** (Descripción), escriba el texto que describe la plantilla que está creando.</span><span class="sxs-lookup"><span data-stu-id="ac98c-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="ac98c-146">Esta información es solo para fines documentales y no se usa en el aprovisionamiento de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="ac98c-147">En el campo **Labels** (Etiquetas), escriba **linux**.</span><span class="sxs-lookup"><span data-stu-id="ac98c-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="ac98c-148">Esta etiqueta se usa para identificar la plantilla que está creando y posteriormente para hacer referencia a la plantilla al crear un trabajo de Hudson.</span><span class="sxs-lookup"><span data-stu-id="ac98c-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="ac98c-149">Seleccione una región donde se creará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="ac98c-150">Seleccione el tamaño adecuado de la máquina.</span><span class="sxs-lookup"><span data-stu-id="ac98c-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="ac98c-151">Especifique una cuenta de almacenamiento donde se creará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="ac98c-152">Asegúrese de que se encuentra en la misma región que el servicio en la nube que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="ac98c-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="ac98c-153">Si desea crear nuevo almacenamiento, puede dejar este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="ac98c-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="ac98c-154">El tiempo de retención especifica el número de minutos antes de que Hudson elimine un subordinado inactivo.</span><span class="sxs-lookup"><span data-stu-id="ac98c-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="ac98c-155">Deje el valor predeterminado de 60.</span><span class="sxs-lookup"><span data-stu-id="ac98c-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="ac98c-156">En **Usage**(Uso), seleccione la condición adecuada de uso de este nodo subordinado.</span><span class="sxs-lookup"><span data-stu-id="ac98c-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="ac98c-157">Por ahora, seleccione **Utilize this node as much as possible**(Usar este nodo tanto como sea posible).</span><span class="sxs-lookup"><span data-stu-id="ac98c-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="ac98c-158">En este punto, su formulario sería parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac98c-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![configuración de plantilla][template config]
13. <span data-ttu-id="ac98c-160">En **Image Family or Id** (Familia o identificador de imagen), debe especificar la imagen de sistema que se instalará en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="ac98c-161">Puede seleccionar de una lista de familias de imagen o especificar una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="ac98c-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="ac98c-162">Si desea seleccionar de una lista de familias de imagen, escriba el primer carácter (distingue mayúsculas de minúsculas) del nombre de familia de imagen.</span><span class="sxs-lookup"><span data-stu-id="ac98c-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="ac98c-163">Por ejemplo, al escribir **U** aparecerá una lista de familias de Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="ac98c-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="ac98c-164">Una vez que seleccione de la lista, Jenkins usará la versión más reciente de esa imagen de sistema de esa familia al aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![lista de familias de SO][OS family list]
    
     <span data-ttu-id="ac98c-166">Si tiene una imagen personalizada que desea usar en su lugar, escriba su nombre.</span><span class="sxs-lookup"><span data-stu-id="ac98c-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="ac98c-167">Los nombres de imagen personalizada no se muestran en una lista, por lo que debe asegurarse de escribir el nombre correctamente.</span><span class="sxs-lookup"><span data-stu-id="ac98c-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="ac98c-168">Para este tutorial, escriba **U** para que aparezca una lista de imágenes de Ubuntu y seleccione **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="ac98c-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="ac98c-169">Para **Launch method** (Método de inicio), seleccione **SSH**.</span><span class="sxs-lookup"><span data-stu-id="ac98c-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="ac98c-170">Copie el siguiente script y péguelo en el campo **Init script** (Script de inicialización).</span><span class="sxs-lookup"><span data-stu-id="ac98c-170">Copy the script below and paste in the **Init script** field.</span></span>
    
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
    
     <span data-ttu-id="ac98c-171">El **script de inicialización** se ejecutará después de crearse la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="ac98c-172">En este ejemplo, el script instala Java, git y ant.</span><span class="sxs-lookup"><span data-stu-id="ac98c-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="ac98c-173">En los campos **Username** (Nombre de usuario) y **Password** (Contraseña), escriba los valores preferidos para la cuenta de administrador que se creará en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac98c-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="ac98c-174">Haga clic en **Verify Template** (Comprobar plantilla) para comprobar si los parámetros especificados son válidos.</span><span class="sxs-lookup"><span data-stu-id="ac98c-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="ac98c-175">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="ac98c-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="ac98c-176">Creación de un trabajo de Hudson que se ejecuta en un nodo subordinado en Azure</span><span class="sxs-lookup"><span data-stu-id="ac98c-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="ac98c-177">En esta sección, creará una tarea de Hudson que se ejecutará en un nodo subordinado en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac98c-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="ac98c-178">En el panel de Hudson, haga clic en **New Job**(Nuevo trabajo).</span><span class="sxs-lookup"><span data-stu-id="ac98c-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="ac98c-179">Escriba un nombre para el trabajo que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="ac98c-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="ac98c-180">Para el tipo de trabajo, seleccione **Build a free-style software job**(Crear un trabajo de software de estilo libre).</span><span class="sxs-lookup"><span data-stu-id="ac98c-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="ac98c-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ac98c-181">Click **OK**.</span></span>
5. <span data-ttu-id="ac98c-182">En la página de configuración del trabajo, seleccione **Restrict where this project can be run**(Restringir dónde se puede ejecutar este proyecto).</span><span class="sxs-lookup"><span data-stu-id="ac98c-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="ac98c-183">Seleccione **Node and label menu** (Menú de nodo y etiqueta) y seleccione **linux** (esta etiqueta se especificó al crear la plantilla de máquina virtual en la sección anterior).</span><span class="sxs-lookup"><span data-stu-id="ac98c-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="ac98c-184">En la sección **Build** (Compilar), haga clic en **Add build step** (Agregar paso de compilación) y seleccione **Execute shell** (Ejecutar shell).</span><span class="sxs-lookup"><span data-stu-id="ac98c-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="ac98c-185">Edite el siguiente script; para ello, sustituya **{your github account name}**, **{your project name}** y **{your project directory}** por los valores adecuados y pegue el script editado en el área de texto que aparece.</span><span class="sxs-lookup"><span data-stu-id="ac98c-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="ac98c-186">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="ac98c-186">Click on **Save**.</span></span>
10. <span data-ttu-id="ac98c-187">En el panel de Hudson, busque el trabajo que acaba de crear y haga clic en icono **Schedule a build** (Programar una compilación).</span><span class="sxs-lookup"><span data-stu-id="ac98c-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="ac98c-188">Hudson creará luego un nodo subordinado con la plantilla que creó en la sección anterior y ejecutará el script especificado en el paso de compilación de esta tarea.</span><span class="sxs-lookup"><span data-stu-id="ac98c-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac98c-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac98c-189">Next Steps</span></span>
<span data-ttu-id="ac98c-190">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="ac98c-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="ac98c-191">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="ac98c-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="ac98c-192">[perfil de suscripción]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="ac98c-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

