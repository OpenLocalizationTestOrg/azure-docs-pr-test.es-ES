---
title: "Use los agentes de máquina virtual de Azure para la integración continua con Jenkins."
description: "Agentes de máquina virtual de Azure como servidores subordinados de Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="367b2-103">Use los agentes de máquina virtual de Azure para la integración continua con Jenkins.</span><span class="sxs-lookup"><span data-stu-id="367b2-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="367b2-104">Esta guía de inicio rápido muestra cómo usar el complemento de agentes de máquina virtual de Azure para Jenkins para crear un agente de Linux (Ubuntu) a petición en Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="367b2-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="367b2-105">Prerequisites</span></span>

<span data-ttu-id="367b2-106">Para completar esta guía de inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="367b2-106">To complete this quickstart:</span></span>

* <span data-ttu-id="367b2-107">Si no dispone de un servidor maestro de Jenkins, puede empezar con la [plantilla de solución](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="367b2-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="367b2-108">Consulte [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si no dispone de una entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="367b2-109">Instalación del complemento de agentes de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="367b2-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="367b2-110">Si empieza a partir de la [plantilla de solución](install-jenkins-solution-template.md), el complemento de agentes de máquina virtual de Azure se instala en el servidor maestro de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="367b2-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="367b2-111">En caso contrario, instale el complemento **Agentes de máquina virtual de Azure** desde dentro del panel de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="367b2-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="367b2-112">Configuración del complemento</span><span class="sxs-lookup"><span data-stu-id="367b2-112">Configure the plugin</span></span>

* <span data-ttu-id="367b2-113">En el panel de Jenkins, haga clic en **Manage Jenkins (Administrar Jenkins) -> Configure System (Configurar sistema) ->**.</span><span class="sxs-lookup"><span data-stu-id="367b2-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="367b2-114">Desplácese hasta la parte inferior de la página y busque la sección con la lista desplegable **Add new cloud** (Agregar una nube nueva).</span><span class="sxs-lookup"><span data-stu-id="367b2-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="367b2-115">En el menú, seleccione **Microsoft Azure VM Agents** (Agentes de máquina virtual de Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="367b2-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="367b2-116">Seleccione una cuenta existente de la lista desplegable de credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="367b2-117">Para agregar una nueva **entidad de servicio de Microsoft Azure,** escriba los siguientes valores: Id. de suscripción, Id. de cliente, secreto de cliente y punto de conexión de token de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="367b2-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Credenciales de Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="367b2-119">Haga clic en **Verify configuration** (Comprobar configuración) para asegurarse de que la configuración del perfil es correcta.</span><span class="sxs-lookup"><span data-stu-id="367b2-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="367b2-120">Guarde la configuración y continúe con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="367b2-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="367b2-121">Configuración de plantilla</span><span class="sxs-lookup"><span data-stu-id="367b2-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="367b2-122">Configuración general</span><span class="sxs-lookup"><span data-stu-id="367b2-122">General configuration</span></span>
<span data-ttu-id="367b2-123">A continuación, configure una plantilla para utilizarla para definir a un agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="367b2-124">Haga clic en **Add** (Agregar) para agregar una plantilla.</span><span class="sxs-lookup"><span data-stu-id="367b2-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="367b2-125">Proporcione un nombre para la nueva plantilla.</span><span class="sxs-lookup"><span data-stu-id="367b2-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="367b2-126">Para la etiqueta, escriba "ubuntu".</span><span class="sxs-lookup"><span data-stu-id="367b2-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="367b2-127">Esta etiqueta se usa durante la configuración del trabajo.</span><span class="sxs-lookup"><span data-stu-id="367b2-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="367b2-128">Seleccione la región deseada en el control de cuadro combinado.</span><span class="sxs-lookup"><span data-stu-id="367b2-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="367b2-129">Seleccione el tamaño de máquina virtual deseado.</span><span class="sxs-lookup"><span data-stu-id="367b2-129">Select the desired VM size.</span></span>
* <span data-ttu-id="367b2-130">Especifique el nombre de cuenta de Azure Storage o déjelo en blanco y use el nombre predeterminado "jenkinsarmst".</span><span class="sxs-lookup"><span data-stu-id="367b2-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="367b2-131">Especifique el tiempo de retención en minutos.</span><span class="sxs-lookup"><span data-stu-id="367b2-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="367b2-132">Esta opción define el número de minutos que Jenkins debe esperar antes de eliminar automáticamente un agente inactivo.</span><span class="sxs-lookup"><span data-stu-id="367b2-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="367b2-133">También puede especificar 0 si no desea que los agentes inactivos se eliminen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="367b2-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![Configuración general](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="367b2-135">Configuración de imagen</span><span class="sxs-lookup"><span data-stu-id="367b2-135">Image configuration</span></span>

<span data-ttu-id="367b2-136">Para crear un agente de Linux (Ubuntu), seleccione **Image reference** (Referencia de imagen) y utilice la configuración siguiente como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="367b2-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="367b2-137">Vaya a [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) para obtener las imágenes más recientes compatibles con Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="367b2-138">Image Publisher (Publicador de imagen): Canonical</span><span class="sxs-lookup"><span data-stu-id="367b2-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="367b2-139">Image Offer (Oferta de imagen): UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="367b2-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="367b2-140">Image Sku (SKU de imagen): 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="367b2-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="367b2-141">Image version (Versión de imagen): la más reciente</span><span class="sxs-lookup"><span data-stu-id="367b2-141">Image version: latest</span></span>
* <span data-ttu-id="367b2-142">OS Type (Tipo de sistema operativo): Linux</span><span class="sxs-lookup"><span data-stu-id="367b2-142">OS Type: Linux</span></span>
* <span data-ttu-id="367b2-143">Launch method (Método de inicio): SSH</span><span class="sxs-lookup"><span data-stu-id="367b2-143">Launch method: SSH</span></span>
* <span data-ttu-id="367b2-144">Proporcione unas credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="367b2-144">Provide an admin credentials</span></span>
* <span data-ttu-id="367b2-145">Para el script de inicialización de la máquina virtual, escriba:</span><span class="sxs-lookup"><span data-stu-id="367b2-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuración de imagen](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="367b2-147">Haga clic en **Verify Template** (Comprobar plantilla) para comprobar la configuración.</span><span class="sxs-lookup"><span data-stu-id="367b2-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="367b2-148">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="367b2-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="367b2-149">Creación de un trabajo en Jenkins</span><span class="sxs-lookup"><span data-stu-id="367b2-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="367b2-150">En el panel de Jenkins, haga clic en **New Item**(Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="367b2-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="367b2-151">Escriba un nombre y seleccione **Freestyle project** (Proyecto de estilo libre) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="367b2-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="367b2-152">En la pestaña **General**, seleccione "Restrict where project can be run" (Restringir donde se pueda ejecutar el proyecto) y escriba "ubuntu" en la expresión de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="367b2-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="367b2-153">Ahora verá "ubuntu" en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="367b2-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="367b2-154">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="367b2-154">Click **Save**.</span></span>

![Configurar un proyecto](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="367b2-156">Compilación de un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="367b2-156">Build your new project</span></span>

* <span data-ttu-id="367b2-157">Vuelva al panel de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="367b2-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="367b2-158">Haga clic con el botón derecho en el nuevo trabajo que creó y, a continuación, haga clic en **Build now** (Compilar ahora).</span><span class="sxs-lookup"><span data-stu-id="367b2-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="367b2-159">Se inicia una compilación.</span><span class="sxs-lookup"><span data-stu-id="367b2-159">A build is kicked off.</span></span> 
* <span data-ttu-id="367b2-160">Una vez completada la compilación, vaya a **Console output** (Salida de consola).</span><span class="sxs-lookup"><span data-stu-id="367b2-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="367b2-161">Allí puede ver que la compilación se realizó de forma remota en Azure.</span><span class="sxs-lookup"><span data-stu-id="367b2-161">You see that the build was performed remotely on Azure.</span></span>

![Salida de consola](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="367b2-163">Referencia</span><span class="sxs-lookup"><span data-stu-id="367b2-163">Reference</span></span>

* <span data-ttu-id="367b2-164">Vídeo de Azure Friday: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Integración continua con Jenkins mediante agentes de máquina virtual de Azure)</span><span class="sxs-lookup"><span data-stu-id="367b2-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="367b2-165">Opciones de configuración e información de soporte técnico: [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) (Wiki del complemento Jenkins de agente de máquina virtual de Azure)</span><span class="sxs-lookup"><span data-stu-id="367b2-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

