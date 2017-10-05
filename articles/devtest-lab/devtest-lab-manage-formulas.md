---
title: "Administración de fórmulas de Azure DevTest Labs para crear máquinas virtuales | Microsoft Docs"
description: "Información sobre cómo actualizar y quitar las fórmulas de Azure DevTest Labs"
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
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="d0b16-103">Administración de fórmulas de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d0b16-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="d0b16-104">En este artículo se explica cómo crear una fórmula a partir de una base (una imagen personalizada, una imagen de Marketplace u otra fórmula) o una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d0b16-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="d0b16-105">Este artículo también le guía a través de la administración de las fórmulas existentes.</span><span class="sxs-lookup"><span data-stu-id="d0b16-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="d0b16-106">Creación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="d0b16-106">Create a formula</span></span>
<span data-ttu-id="d0b16-107">Cualquier usuario con permisos de *usuarios* de DevTest Labs puede crear máquinas virtuales tomando una fórmula como base.</span><span class="sxs-lookup"><span data-stu-id="d0b16-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="d0b16-108">Hay dos maneras de crear fórmulas:</span><span class="sxs-lookup"><span data-stu-id="d0b16-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="d0b16-109">Desde una base: use esta forma cuando desee definir todas las características de la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="d0b16-110">Desde una máquina virtual de laboratorio existente: use esta forma cuando desee crear una fórmula basada en la configuración de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d0b16-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="d0b16-111">Para obtener más información sobre cómo agregar usuarios y permisos, consulte [Adición de propietarios y usuarios en Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="d0b16-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="d0b16-112">Creación de una fórmula desde una base</span><span class="sxs-lookup"><span data-stu-id="d0b16-112">Create a formula from a base</span></span>
<span data-ttu-id="d0b16-113">Los siguientes pasos le guiarán por el proceso de creación de una fórmula a partir de una imagen personalizada, una imagen de Marketplace u otra fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="d0b16-114">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0b16-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="d0b16-115">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="d0b16-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="d0b16-116">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="d0b16-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="d0b16-117">En la hoja del laboratorio, seleccione **Fórmulas (bases reutilizables)**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="d0b16-119">En la hoja **Fórmulas**, seleccione **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Agregar una fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="d0b16-121">En la hoja **Elegir una base** , seleccione la base (imagen personalizada, imagen de Marketplace o fórmula) a partir de la cual quiere crear la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Lista base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="d0b16-123">En la hoja **Crear fórmula** , especifique los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="d0b16-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="d0b16-124">**Nombre de fórmula** : escriba un nombre para la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="d0b16-125">Este valor se mostrará en la lista de imágenes base al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0b16-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="d0b16-126">El nombre se valida a medida que lo escribe y, si no es válido, un mensaje le indicará los requisitos para un nombre válido.</span><span class="sxs-lookup"><span data-stu-id="d0b16-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="d0b16-127">**Descripción** : escriba una descripción significativa para la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="d0b16-128">Este valor está disponible desde el menú contextual de la fórmula al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0b16-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="d0b16-129">**Nombre de usuario**: escriba un nombre de usuario al que se concederán privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="d0b16-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="d0b16-130">**Contraseña** : escriba, o seleccione en la lista desplegable, un valor que esté asociado con el secreto (contraseña) que desee usar para el usuario especificado.</span><span class="sxs-lookup"><span data-stu-id="d0b16-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="d0b16-131">Para obtener más información sobre los secretos, consulte [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/) (Azure DevTest Labs: almacén personal de secretos).</span><span class="sxs-lookup"><span data-stu-id="d0b16-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="d0b16-132">**Virtual machine disk type** (Tipo de disco de máquina virtual): especifique cualquier HDD (unidad de disco duro) o SSD (unidad de estado sólido) para indicar qué tipo de disco de almacenamiento se permite para las máquinas virtuales que se aprovisionan con esta imagen base.</span><span class="sxs-lookup"><span data-stu-id="d0b16-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="d0b16-133">** Tamaño de la máquina virtual**: seleccione uno de los elementos predefinidos que especifican los núcleos del procesador, el tamaño de RAM y el tamaño de la unidad de disco duro de la máquina virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="d0b16-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="d0b16-134">**Artefactos**: seleccione esta opción para abrir la hoja **Agregar artefactos**, donde podrá seleccionar y configurar los artefactos que quiere agregar a la imagen base.</span><span class="sxs-lookup"><span data-stu-id="d0b16-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="d0b16-135">Para obtener más información sobre los artefactos, vea [Administración de artefactos de máquina virtual en Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0b16-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="d0b16-136">**Configuración avanzada**: seleccione esta opción para abrir la hoja **Avanzado**, donde podrá configurar las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="d0b16-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="d0b16-137">**Red virtual** : especifique la red virtual que desee.</span><span class="sxs-lookup"><span data-stu-id="d0b16-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="d0b16-138">**Subred** : especifique la subred deseada.</span><span class="sxs-lookup"><span data-stu-id="d0b16-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="d0b16-139">**Configuración de dirección IP**: especifique si desea direcciones IP públicas, privadas o compartidas.</span><span class="sxs-lookup"><span data-stu-id="d0b16-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="d0b16-140">Para obtener más información sobre las direcciones IP compartidas, consulte [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Direcciones IP compartidas en Azure DevTest Labs).</span><span class="sxs-lookup"><span data-stu-id="d0b16-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="d0b16-141">**Make this machine claimable** (Poder reclamar esta máquina): poder reclamar una máquina significa que no se podrá asignar la propiedad durante su creación.</span><span class="sxs-lookup"><span data-stu-id="d0b16-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="d0b16-142">En su lugar, los usuarios del laboratorio podrán asumir su propiedad ("reclamar") de la máquina en la hoja del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="d0b16-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="d0b16-143">**Imagen** : este campo muestra el nombre de la imagen base que seleccionó en la hoja anterior.</span><span class="sxs-lookup"><span data-stu-id="d0b16-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="d0b16-145">Seleccione **Crear** para crear la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="d0b16-146">Cuando se ha creado la fórmula, se muestra en la lista de la hoja **Fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="d0b16-147">Creación de una fórmula desde una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d0b16-147">Create a formula from a VM</span></span>
<span data-ttu-id="d0b16-148">Los siguientes pasos le guiarán a través del proceso de creación de una fórmula basada en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d0b16-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0b16-149">Para crear una fórmula desde una máquina virtual, la máquina virtual debe haberse creado después del 30 de marzo de 2016.</span><span class="sxs-lookup"><span data-stu-id="d0b16-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="d0b16-150">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0b16-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0b16-151">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="d0b16-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="d0b16-152">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="d0b16-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="d0b16-153">En la hoja **Información general** del laboratorio, seleccione la máquina virtual desde la que desee crear la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Máquinas virtuales de laboratorios](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="d0b16-155">En la hoja de la máquina virtual, seleccione **Crear fórmula (base reutilizable)**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="d0b16-157">En la hoja **Crear fórmula**, escriba un **Nombre** y una **Descripción** para la nueva fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Hoja Crear fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="d0b16-159">Seleccione **Aceptar** para crear la fórmula.</span><span class="sxs-lookup"><span data-stu-id="d0b16-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="d0b16-160">Modificación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="d0b16-160">Modify a formula</span></span>
<span data-ttu-id="d0b16-161">Para modificar una fórmula, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d0b16-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="d0b16-162">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0b16-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0b16-163">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="d0b16-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="d0b16-164">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="d0b16-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="d0b16-165">En la hoja del laboratorio, seleccione **Fórmulas (bases reutilizables)**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="d0b16-167">En la hoja **Lab formulas** (Fórmulas de laboratorio), seleccione la fórmula que quiere modificar.</span><span class="sxs-lookup"><span data-stu-id="d0b16-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="d0b16-168">En la hoja **Update formula** (Actualizar fórmula), realice las modificaciones deseadas y seleccione **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="d0b16-169">Eliminación de una fórmula</span><span class="sxs-lookup"><span data-stu-id="d0b16-169">Delete a formula</span></span>
<span data-ttu-id="d0b16-170">Para eliminar una fórmula, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d0b16-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="d0b16-171">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0b16-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0b16-172">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="d0b16-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="d0b16-173">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="d0b16-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="d0b16-174">En la hoja **Configuración** del laboratorio, seleccione **Fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="d0b16-176">En la hoja **Lab formulas** (Fórmulas de laboratorio), seleccione los puntos suspensivos a la derecha de la fórmula que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="d0b16-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="d0b16-178">En el menú contextual de la fórmula, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d0b16-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Menú contextual de fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="d0b16-180">Seleccione **Sí** en el cuadro de diálogo de confirmación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="d0b16-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="d0b16-181">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="d0b16-181">Related blog posts</span></span>
* [<span data-ttu-id="d0b16-182">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="d0b16-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="d0b16-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0b16-183">Next steps</span></span>
<span data-ttu-id="d0b16-184">Cuando haya creado una fórmula para usarla al crear una máquina virtual, el siguiente paso consiste en [agregar una máquina virtual al laboratorio](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0b16-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

