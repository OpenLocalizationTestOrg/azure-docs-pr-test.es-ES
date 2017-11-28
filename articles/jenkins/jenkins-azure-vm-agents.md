---
title: "aaaUse agentes de máquina virtual de Azure para la integración continua con Jenkins."
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
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="a9d86-103">Use los agentes de máquina virtual de Azure para la integración continua con Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a9d86-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="a9d86-104">Este tutorial rápido muestra cómo toouse Hola agentes de máquina virtual de Azure Jenkins complemento toocreate un agente de Linux (Ubuntu) a petición en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d86-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9d86-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a9d86-105">Prerequisites</span></span>

<span data-ttu-id="a9d86-106">toocomplete este tutorial rápido:</span><span class="sxs-lookup"><span data-stu-id="a9d86-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="a9d86-107">Si no dispone de un patrón Jenkins, puede empezar con hello [plantilla de solución](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="a9d86-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="a9d86-108">Consulte demasiado[crear una entidad de seguridad de servicio de Azure con Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si ya no dispone de una entidad de seguridad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d86-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="a9d86-109">Instalación del complemento de agentes de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a9d86-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="a9d86-110">Si inicia desde hello [plantilla de solución](install-jenkins-solution-template.md), complemento de hello Azure VM Agent está instalado en master de hello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a9d86-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="a9d86-111">En caso contrario, instalar hello **agentes de máquina virtual de Azure** complemento desde dentro del panel de hello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a9d86-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="a9d86-112">Configurar el complemento de Hola</span><span class="sxs-lookup"><span data-stu-id="a9d86-112">Configure hello plugin</span></span>

* <span data-ttu-id="a9d86-113">En el panel de Jenkins hello, haga clic en **Jenkins administrar -> configurar el sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="a9d86-114">Desplácese toohello inferior de la página de Hola y busque la sección de hello con lista desplegable de hello **agregar nueva nube**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="a9d86-115">En el menú de hello, seleccione **agentes de máquina virtual de Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="a9d86-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="a9d86-116">Seleccione una cuenta existente de lista desplegable de hello las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d86-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="a9d86-117">tooadd un nuevo **entidad de servicio de Microsoft Azure,** escriba Hola siguientes valores: Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a9d86-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Credenciales de Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="a9d86-119">Haga clic en **Compruebe la configuración de** toomake que esa configuración de perfil de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="a9d86-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="a9d86-120">Guardar configuración de Hola y continuar toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="a9d86-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="a9d86-121">Configuración de plantilla</span><span class="sxs-lookup"><span data-stu-id="a9d86-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="a9d86-122">Configuración general</span><span class="sxs-lookup"><span data-stu-id="a9d86-122">General configuration</span></span>
<span data-ttu-id="a9d86-123">A continuación, configure una plantilla para uso toodefine un agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d86-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="a9d86-124">Haga clic en **agregar** tooadd una plantilla.</span><span class="sxs-lookup"><span data-stu-id="a9d86-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="a9d86-125">Proporcione un nombre para la nueva plantilla.</span><span class="sxs-lookup"><span data-stu-id="a9d86-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="a9d86-126">Para la etiqueta de hello, escriba "ubuntu."</span><span class="sxs-lookup"><span data-stu-id="a9d86-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="a9d86-127">Esta etiqueta se usa durante la configuración del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9d86-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="a9d86-128">Seleccionar región deseada Hola de cuadro combinado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9d86-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="a9d86-129">Seleccione Hola había deseado tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9d86-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="a9d86-130">Especifique el nombre de cuenta de almacenamiento de Azure de Hola o dejarlo nombre predeterminado de hello toouse en blanco "jenkinsarmst."</span><span class="sxs-lookup"><span data-stu-id="a9d86-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="a9d86-131">Especifique el tiempo de retención de hello en minutos.</span><span class="sxs-lookup"><span data-stu-id="a9d86-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="a9d86-132">Esta opción define el número de Hola de minutos que Jenkins puede esperar antes de eliminar automáticamente un agente inactivo.</span><span class="sxs-lookup"><span data-stu-id="a9d86-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="a9d86-133">Especifique 0 si no desea toobe agentes inactivo elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a9d86-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Configuración general](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="a9d86-135">Configuración de imagen</span><span class="sxs-lookup"><span data-stu-id="a9d86-135">Image configuration</span></span>

<span data-ttu-id="a9d86-136">toocreate un agente de Linux (Ubuntu), seleccione **referencia de imagen** y use Hola siguiente configuración como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9d86-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="a9d86-137">Consulte demasiado[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) para hello Azure más reciente admite imágenes.</span><span class="sxs-lookup"><span data-stu-id="a9d86-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="a9d86-138">Image Publisher (Publicador de imagen): Canonical</span><span class="sxs-lookup"><span data-stu-id="a9d86-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="a9d86-139">Image Offer (Oferta de imagen): UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="a9d86-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="a9d86-140">Image Sku (SKU de imagen): 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="a9d86-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="a9d86-141">Image version (Versión de imagen): la más reciente</span><span class="sxs-lookup"><span data-stu-id="a9d86-141">Image version: latest</span></span>
* <span data-ttu-id="a9d86-142">OS Type (Tipo de sistema operativo): Linux</span><span class="sxs-lookup"><span data-stu-id="a9d86-142">OS Type: Linux</span></span>
* <span data-ttu-id="a9d86-143">Launch method (Método de inicio): SSH</span><span class="sxs-lookup"><span data-stu-id="a9d86-143">Launch method: SSH</span></span>
* <span data-ttu-id="a9d86-144">Proporcione unas credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="a9d86-144">Provide an admin credentials</span></span>
* <span data-ttu-id="a9d86-145">Para el script de inicialización de la máquina virtual, escriba:</span><span class="sxs-lookup"><span data-stu-id="a9d86-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuración de imagen](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="a9d86-147">Haga clic en **comprobar plantilla** configuración de tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="a9d86-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="a9d86-148">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="a9d86-149">Creación de un trabajo en Jenkins</span><span class="sxs-lookup"><span data-stu-id="a9d86-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="a9d86-150">En el panel de Jenkins hello, haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="a9d86-151">Escriba un nombre y seleccione **Freestyle project** (Proyecto de estilo libre) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="a9d86-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="a9d86-152">Hola **General** ficha, seleccione "Restringir donde se puede ejecutar el proyecto" y escriba "ubuntu" en la expresión de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="a9d86-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="a9d86-153">Ahora verá "ubuntu" en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9d86-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="a9d86-154">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-154">Click **Save**.</span></span>

![Configurar un proyecto](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="a9d86-156">Compilación de un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="a9d86-156">Build your new project</span></span>

* <span data-ttu-id="a9d86-157">Volver atrás toohello Jenkins panel.</span><span class="sxs-lookup"><span data-stu-id="a9d86-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="a9d86-158">Nuevo trabajo de Hola de menú contextual que ha creado, a continuación, haga clic en **compila ahora**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="a9d86-159">Se inicia una compilación.</span><span class="sxs-lookup"><span data-stu-id="a9d86-159">A build is kicked off.</span></span> 
* <span data-ttu-id="a9d86-160">Una vez completada la compilación de hello, vaya demasiado**salida de consola**.</span><span class="sxs-lookup"><span data-stu-id="a9d86-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="a9d86-161">Verá que compilación Hola se realizó de forma remota en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d86-161">You see that hello build was performed remotely on Azure.</span></span>

![Salida de consola](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="a9d86-163">Referencia</span><span class="sxs-lookup"><span data-stu-id="a9d86-163">Reference</span></span>

* <span data-ttu-id="a9d86-164">Vídeo de Azure Friday: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Integración continua con Jenkins mediante agentes de máquina virtual de Azure)</span><span class="sxs-lookup"><span data-stu-id="a9d86-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="a9d86-165">Opciones de configuración e información de soporte técnico: [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) (Wiki del complemento Jenkins de agente de máquina virtual de Azure)</span><span class="sxs-lookup"><span data-stu-id="a9d86-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

