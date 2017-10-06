---
title: "las fórmulas de aaaManage en toocreate de laboratorios de desarrollo y pruebas de Azure VM | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupdate y quite las fórmulas de laboratorios de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="6a8ed-103">Administración de fórmulas de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6a8ed-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="6a8ed-104">Este artículo se explica cómo toocreate una fórmula de una base (imagen personalizada, una imagen de Marketplace u otra fórmula) o en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="6a8ed-105">Este artículo también le guía a través de la administración de las fórmulas existentes.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="6a8ed-106">Creación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="6a8ed-106">Create a formula</span></span>
<span data-ttu-id="6a8ed-107">Cualquier persona con laboratorios de desarrollo y pruebas *usuarios* permisos es capaz de toocreate las máquinas virtuales usando una fórmula como base.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="6a8ed-108">Hay dos maneras de toocreate fórmulas:</span><span class="sxs-lookup"><span data-stu-id="6a8ed-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="6a8ed-109">Desde una base - utilice cuando desee toodefine todas las características de Hola de fórmula de saludo.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="6a8ed-110">En un laboratorio existente VM - Utilice esta opción cuando desee toocreate una fórmula basado en valores de hello de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="6a8ed-111">Para obtener más información sobre cómo agregar usuarios y permisos, consulte [Adición de propietarios y usuarios en Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="6a8ed-112">Creación de una fórmula desde una base</span><span class="sxs-lookup"><span data-stu-id="6a8ed-112">Create a formula from a base</span></span>
<span data-ttu-id="6a8ed-113">Hola pasos le guiará a través de proceso de Hola de creación de una fórmula de una imagen personalizada, una imagen de Marketplace u otra fórmula.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="6a8ed-114">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="6a8ed-115">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="6a8ed-116">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="6a8ed-117">En la hoja del laboratorio de hello, seleccione **fórmulas (reutilizables bases)**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="6a8ed-119">En hello **fórmulas** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Agregar una fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="6a8ed-121">En hello **elegir una base de** hoja, base de Hola seleccione (imagen personalizada, una imagen de Marketplace o fórmula) desde el que se usará de fórmula de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Lista base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="6a8ed-123">En hello **crear fórmula** hoja, especifique Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="6a8ed-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="6a8ed-124">**Nombre de fórmula** : escriba un nombre para la fórmula.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="6a8ed-125">Este valor se muestra en la lista de Hola de imágenes de base cuando se crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="6a8ed-126">nombre de Hola se valida como escribe, y si no es válido, un mensaje indica los requisitos de Hola para un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="6a8ed-127">**Descripción** : escriba una descripción significativa para la fórmula.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="6a8ed-128">Este valor está disponible desde el menú contextual de la fórmula de hello cuando se crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="6a8ed-129">**Nombre de usuario**: escriba un nombre de usuario al que se concederán privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="6a8ed-130">**Contraseña** : escriba - o seleccione en la lista desplegable de hello - un valor que está asociado con el secreto de hello (contraseña) que quiere toouse de usuario especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="6a8ed-131">Para obtener más información acerca de los secretos de hello, consulte [laboratorios de desarrollo y pruebas de Azure: almacén secreto Personal](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="6a8ed-132">**Tipo de disco de máquina virtual** : especifique cualquier unidad de disco duro (unidad de disco duro) o si se permite tooindicate SSD (unidad de estado sólido) qué almacenamiento es el tipo de disco para las máquinas virtuales de hello aprovisionadas usando esta imagen base.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="6a8ed-133">** Máquina Virtual de tamaño **: seleccione uno de los elementos de hello predefinido que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello VM toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="6a8ed-134">**Artefactos** -tooopen seleccione hello **agregar artefactos** hoja, en el que seleccione y configure los artefactos de Hola que desea que la imagen base de tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="6a8ed-135">Para obtener más información sobre los artefactos, vea [Administración de artefactos de máquina virtual en Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="6a8ed-136">**Configuración avanzada** -tooopen seleccione hello **avanzadas** hoja donde configurar Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="6a8ed-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="6a8ed-137">**Red virtual** -especificar Hola deseada de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="6a8ed-138">**Subred** -especificar la subred de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="6a8ed-139">**Configuración de dirección IP** -especificar si desea que Hola Public, Private o compartido direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="6a8ed-140">Para obtener más información sobre las direcciones IP compartidas, consulte [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Direcciones IP compartidas en Azure DevTest Labs).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="6a8ed-141">**Hacer que esta máquina claimable** -realizar una máquina "claimable" significa que se le no asignará la propiedad en tiempo de presentación de la creación.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="6a8ed-142">En su lugar, los usuarios del laboratorio será máquina de hello tootake capaz de propiedad ("notificaciones") en la hoja del laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="6a8ed-143">**Imagen** : este campo muestra el nombre de imagen base Hola que ha seleccionado en la hoja de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="6a8ed-145">Seleccione **crear** toocreate fórmula de saludo.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="6a8ed-146">Cuando se ha creado la fórmula de hello, muestra en lista Hola Hola **fórmulas** hoja.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="6a8ed-147">Creación de una fórmula desde una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6a8ed-147">Create a formula from a VM</span></span>
<span data-ttu-id="6a8ed-148">Hello pasos siguientes guiarán a través del proceso de Hola de creación de una fórmula basada en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a8ed-149">toocreate una fórmula de una máquina virtual, Hola VM debe haber creado después del 30 de marzo de 2016.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="6a8ed-150">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6a8ed-151">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="6a8ed-152">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="6a8ed-153">En el laboratorio de hello **Introducción** hoja, VM Hola seleccione desde el que desea fórmula de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Máquinas virtuales de laboratorios](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="6a8ed-155">En la hoja de la máquina virtual de hello, seleccione **crear fórmula (base reutilizable)**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="6a8ed-157">En hello **crear fórmula** hoja, escriba una **nombre** y **descripción** para la nueva fórmula.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Hoja Crear fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="6a8ed-159">Seleccione **Aceptar** toocreate fórmula de saludo.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="6a8ed-160">Modificación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="6a8ed-160">Modify a formula</span></span>
<span data-ttu-id="6a8ed-161">toomodify una fórmula, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6a8ed-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="6a8ed-162">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6a8ed-163">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="6a8ed-164">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="6a8ed-165">En la hoja del laboratorio de hello, seleccione **fórmulas (reutilizables bases)**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="6a8ed-167">En hello **fórmulas de laboratorio** hoja, fórmula Seleccione Hola desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="6a8ed-168">En hello **actualizar fórmula** hoja, edite el Hola deseado y seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="6a8ed-169">Eliminación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="6a8ed-169">Delete a formula</span></span>
<span data-ttu-id="6a8ed-170">toodelete una fórmula, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6a8ed-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="6a8ed-171">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6a8ed-172">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="6a8ed-173">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="6a8ed-174">En el laboratorio de hello **configuración** hoja, seleccione **fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="6a8ed-176">En hello **fórmulas de laboratorio** hoja, seleccione Hola puntos suspensivos toohello derecha de la fórmula de hello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="6a8ed-178">En el menú contextual de la fórmula de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Menú contextual de fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="6a8ed-180">Seleccione **Sí** cuadro de diálogo de confirmación de eliminación de toohello.</span><span class="sxs-lookup"><span data-stu-id="6a8ed-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6a8ed-181">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="6a8ed-181">Related blog posts</span></span>
* [<span data-ttu-id="6a8ed-182">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="6a8ed-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="6a8ed-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a8ed-183">Next steps</span></span>
<span data-ttu-id="6a8ed-184">Una vez haya creado una fórmula para usarla al crear una máquina virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="6a8ed-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

