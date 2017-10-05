---
title: Lista de cuentas de almacenamiento de Azure
description: "Administrar la configuración de su cuenta de almacenamiento con el Kit de herramientas de Azure para Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="89410-103">Lista de cuentas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="89410-103">Azure Storage Account List</span></span>
<span data-ttu-id="89410-104">Las cuentas de almacenamiento de Azure permiten el uso de las ubicaciones de descarga para su JDK, el servidor de aplicaciones y los componentes arbitrarios, así como para almacenar el estado cuando se usa el almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="89410-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="89410-105">Eclipse mantiene una lista de cuentas de almacenamiento conocidas que están disponibles para sus proyectos en el área de trabajo de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="89410-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="89410-106">Para abrir el cuadro de diálogo **Cuentas de almacenamiento** que se usa para administrar esa lista, en Eclipse, haga clic en **Ventana**, en **Preferencias**, expanda **Azure** y luego haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="89410-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="89410-107">Lo siguiente muestra el cuadro de diálogo **Cuentas de almacenamiento** .</span><span class="sxs-lookup"><span data-stu-id="89410-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="89410-108">También se puede abrir este cuadro de diálogo desde un vínculo **Cuentas** en cuadros de diálogo que usan cuentas de almacenamiento, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="89410-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="89410-109">La pestaña **JDK** del cuadro de diálogo **Configuración del servidor**.</span><span class="sxs-lookup"><span data-stu-id="89410-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="89410-110">La pestaña **Servidor** del cuadro de diálogo **Configuración del servidor**.</span><span class="sxs-lookup"><span data-stu-id="89410-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="89410-111">El cuadro de diálogo **Agregar componente** .</span><span class="sxs-lookup"><span data-stu-id="89410-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="89410-112">El cuadro de diálogo de propiedades de **Almacenamiento en caché** .</span><span class="sxs-lookup"><span data-stu-id="89410-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="89410-113">Para importar sus cuentas de almacenamiento mediante un archivo de configuración de publicación</span><span class="sxs-lookup"><span data-stu-id="89410-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="89410-114">Dentro del cuadro de diálogo **Cuentas de almacenamiento**, haga clic en **Importar desde el archivo PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="89410-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="89410-115">(Omita este paso si ya ha guardado un archivo de configuración de publicación en su máquina local). En el cuadro de diálogo **Importar desde el archivo de suscripción**, haga clic en **Descargar archivo PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="89410-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="89410-116">Si todavía no ha iniciado sesión en su cuenta de Azure, se le solicitará que lo haga.</span><span class="sxs-lookup"><span data-stu-id="89410-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="89410-117">Después, se le solicitará que guarde un archivo de configuración de publicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="89410-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="89410-118">(Puede ignorar las instrucciones resultantes que se muestran en las páginas de inicio de sesión: se ofrecen por el portal de Azure y están pensadas para los usuarios de Visual Studio.) Guárdelo en su equipo local.</span><span class="sxs-lookup"><span data-stu-id="89410-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="89410-119">Todavía en el cuadro de diálogo **Importar información de suscripción**, haga clic en el botón **Examinar**, seleccione el archivo de configuración de publicación que guardó localmente anteriormente y luego haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="89410-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="89410-120">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Importar información de la suscripción**.</span><span class="sxs-lookup"><span data-stu-id="89410-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="89410-121">Para crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="89410-121">To create a new storage account</span></span>
1. <span data-ttu-id="89410-122">En el cuadro de diálogo **Cuentas de almacenamiento**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="89410-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="89410-123">En el cuadro de diálogo **Agregar cuenta de almacenamiento**, haga clic en **Nueva**.</span><span class="sxs-lookup"><span data-stu-id="89410-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="89410-124">En el cuadro de diálogo **Nueva cuenta de almacenamiento** , especifique los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="89410-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="89410-125">Nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-125">Storage account name.</span></span>

   * <span data-ttu-id="89410-126">Ubicación de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-126">Location of the storage account.</span></span>

   * <span data-ttu-id="89410-127">Descripción de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-127">Description of the storage account.</span></span>

   * <span data-ttu-id="89410-128">La suscripción a la que pertenece la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="89410-129">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Nueva cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="89410-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="89410-130">Se puede tardar unos minutos en crearse su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="89410-131">Una vez creada, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Agregar cuenta de almacenamiento** y se agregará la nueva cuenta de almacenamiento a la lista de cuentas de almacenamiento disponibles.</span><span class="sxs-lookup"><span data-stu-id="89410-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="89410-132">Para agregar una cuenta de almacenamiento existente a la lista</span><span class="sxs-lookup"><span data-stu-id="89410-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="89410-133">Si no dispone ya de una cuenta de almacenamiento de Azure, cree una siguiendo los pasosde la sección **Creación de una cuenta de almacenamiento nueva** que aparece anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89410-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="89410-134">(También puede crear una cuenta de almacenamiento nueva en el [Portal de administración de Azure][Azure Management Portal]).</span><span class="sxs-lookup"><span data-stu-id="89410-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="89410-135">En el cuadro de diálogo **Cuentas de almacenamiento**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="89410-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="89410-136">En el cuadro de diálogo **Agregar cuenta de almacenamiento**, especifique valores para **Nombre** y **Clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="89410-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="89410-137">El nombre de la cuenta y la clave de acceso deben ser para una cuenta de almacenamiento de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="89410-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="89410-138">Use la sección **Almacenamiento** del [Portal de administración de Azure][Azure Management Portal] para ver sus claves y nombres de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="89410-139">Su cuadro de diálogo **Agregar cuenta de almacenamiento** tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="89410-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="89410-140">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Agregar cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="89410-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="89410-141">Para modificar una cuenta de almacenamiento para que use una nueva clave de acceso</span><span class="sxs-lookup"><span data-stu-id="89410-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="89410-142">En el cuadro de diálogo **Cuentas de almacenamiento**, haga clic en la cuenta de almacenamiento que quiera editar y luego haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="89410-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="89410-143">En el cuadro de diálogo **Editar la clave de acceso de la cuenta de almacenamiento**, modifique el valor de la **Clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="89410-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="89410-144">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editar la clave de acceso de la cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="89410-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="89410-145">Para quitar una cuenta de almacenamiento de la lista mantenida en Eclipse</span><span class="sxs-lookup"><span data-stu-id="89410-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="89410-146">En el cuadro de diálogo **Cuentas de almacenamiento**, haga clic en la cuenta de almacenamiento que quiera editar y luego haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="89410-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="89410-147">Haga clic en **Aceptar** cuando se pregunte si quiere quitar la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89410-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="89410-148">Al quitar la cuenta de almacenamiento mediante el cuadro de diálogo **Cuentas de almacenamiento** solo se quita de la lista de cuentas de almacenamiento que se pueden ver en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="89410-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="89410-149">No elimina la cuenta de almacenamiento de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="89410-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="89410-150">Además, la cuenta de almacenamiento podría aparecer de nuevo en la lista después de que Eclipse vuelva a cargar los detalles de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="89410-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="89410-151">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="89410-151">See Also</span></span>
<span data-ttu-id="89410-152">[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89410-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="89410-153">[Instalación del Kit de herramientas de Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89410-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="89410-154">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89410-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="89410-155">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="89410-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
