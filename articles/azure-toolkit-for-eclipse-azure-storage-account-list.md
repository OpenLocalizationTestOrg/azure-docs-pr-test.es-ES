---
title: aaaAzure lista de cuentas de almacenamiento
description: "Administrar la configuración de la cuenta de almacenamiento mediante Hola Kit de herramientas de Azure para Eclipse"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="e01ec-103">Lista de cuentas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e01ec-103">Azure Storage Account List</span></span>
<span data-ttu-id="e01ec-104">Almacenamiento de Azure cuentas permiten descargar toobe de ubicaciones que se usa para el JDK, servidor de aplicaciones y componentes arbitrarios, así como para almacenar el estado cuando se usa el almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="e01ec-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="e01ec-105">Eclipse mantiene una lista de cuentas de almacenamiento conocidas que son proyectos tooyour disponible en el área de trabajo de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e01ec-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="e01ec-106">Hola tooopen **cuentas de almacenamiento** cuadro de diálogo, que es usado toomanage que enumeran, en Eclipse, haga clic en **ventana**, haga clic en **preferencias**, expanda **Azure** y, a continuación, haga clic en **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="e01ec-107">siguiente Hello muestra hello **cuentas de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="e01ec-108">También se puede abrir este cuadro de diálogo desde un **cuentas** vínculo en los cuadros de diálogo que utilizan cuentas de almacenamiento, como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e01ec-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="e01ec-109">Hola **JDK** ficha de hello **configuración del servidor** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="e01ec-110">Hola **Server** ficha de hello **configuración del servidor** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="e01ec-111">Hola **Agregar componente** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="e01ec-112">Hola **Caching** cuadro de diálogo Propiedades.</span><span class="sxs-lookup"><span data-stu-id="e01ec-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="e01ec-113">tooimport el almacenamiento de cuentas con un archivo de configuración de publicación</span><span class="sxs-lookup"><span data-stu-id="e01ec-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="e01ec-114">Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **importar desde el archivo de configuración de publicación**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="e01ec-115">(Omita este paso si ya ha guardado un equipo local tooyour del archivo de publicación configuración). Hola **Import Subscription Information** cuadro de diálogo, haga clic en **Download PUBLISH-SETTINGS File**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="e01ec-116">Si no ha iniciado ya sesión en su cuenta de Azure, es posible que toolog solicitada en.</span><span class="sxs-lookup"><span data-stu-id="e01ec-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="e01ec-117">A continuación, se le pedirá una Azure toosave archivo de configuración de publicación.</span><span class="sxs-lookup"><span data-stu-id="e01ec-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="e01ec-118">(Puede omitir instrucciones de hello resultante que se muestra en las páginas de inicio de sesión de hello - se proporcionan por hello portal de Azure y están pensadas para usuarios de Visual Studio.) Guárdelo tooyour de equipo local.</span><span class="sxs-lookup"><span data-stu-id="e01ec-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="e01ec-119">Aún en hello **Import Subscription Information** cuadro de diálogo, haga clic en hello **examinar** button, seleccione Hola publicar el archivo de configuración que ha guardado localmente anteriormente y, a continuación, haga clic en **abrir**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="e01ec-120">Haga clic en **Aceptar** tooclose hello **Import Subscription Information** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="e01ec-121">toocreate una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e01ec-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="e01ec-122">Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="e01ec-123">Dentro de hello **agregar una cuenta de almacenamiento** cuadro de diálogo, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="e01ec-124">Dentro de hello **nueva cuenta de almacenamiento** cuadro de diálogo, especifique los valores siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="e01ec-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="e01ec-125">Nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e01ec-125">Storage account name.</span></span>

   * <span data-ttu-id="e01ec-126">Ubicación de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ec-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="e01ec-127">Descripción de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ec-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="e01ec-128">cuenta de almacenamiento de Hello suscripción toowhich Hola pertenece.</span><span class="sxs-lookup"><span data-stu-id="e01ec-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="e01ec-129">Haga clic en **Aceptar** tooclose hello **nueva cuenta de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="e01ec-130">Puede tardar varios minutos para su toobe de cuenta de almacenamiento creado.</span><span class="sxs-lookup"><span data-stu-id="e01ec-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="e01ec-131">Después de crearla, haga clic en **Aceptar** tooclose hello **agregar una cuenta de almacenamiento** cuadro de diálogo y la nueva cuenta de almacenamiento se agregarán toohello lista de cuentas de almacenamiento disponible.</span><span class="sxs-lookup"><span data-stu-id="e01ec-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="e01ec-132">tooadd una lista de toohello de cuenta de almacenamiento existente</span><span class="sxs-lookup"><span data-stu-id="e01ec-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="e01ec-133">Si ya tiene un almacenamiento de Azure de la cuenta, cree una forma Hola pasos enumeran en hello **toocreate una nueva sección de la cuenta de almacenamiento** anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e01ec-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="e01ec-134">(O bien, puede crear una nueva cuenta de almacenamiento en hello [Portal de administración de Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="e01ec-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="e01ec-135">Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="e01ec-136">Dentro de hello **agregar una cuenta de almacenamiento** cuadro de diálogo, especifique los valores de **nombre** y **clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="e01ec-137">clave de acceso y nombre de la cuenta de Hello debe ser para una cuenta de almacenamiento de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="e01ec-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="e01ec-138">Hola de uso **almacenamiento** sección de hello [Portal de administración de Azure] [ Azure Management Portal] tooview nombres y claves de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e01ec-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="e01ec-139">Su **agregar una cuenta de almacenamiento** cuadro de diálogo tendrá un aspecto similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="e01ec-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="e01ec-140">Haga clic en **Aceptar** tooclose hello **agregar una cuenta de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="e01ec-141">toomodify un toouse de cuenta de almacenamiento una nueva clave de acceso</span><span class="sxs-lookup"><span data-stu-id="e01ec-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="e01ec-142">Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en la cuenta de almacenamiento de Hola que desee tooedit y, a continuación, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="e01ec-143">Dentro de hello **editar la clave de acceso de la cuenta de almacenamiento** cuadro de diálogo Modificar hello **clave de acceso** valor.</span><span class="sxs-lookup"><span data-stu-id="e01ec-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="e01ec-144">Haga clic en **Aceptar** tooclose hello **editar la clave de acceso de la cuenta de almacenamiento** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e01ec-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="e01ec-145">tooremove mantiene de una cuenta de almacenamiento de la lista de hello en Eclipse</span><span class="sxs-lookup"><span data-stu-id="e01ec-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="e01ec-146">Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en la cuenta de almacenamiento de Hola que desee tooedit y, a continuación, haga clic en **quitar**.</span><span class="sxs-lookup"><span data-stu-id="e01ec-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="e01ec-147">Haga clic en **Aceptar** cuando tooremove solicitada Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e01ec-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="e01ec-148">Quitar la cuenta de almacenamiento de Hola a través de hello **cuentas de almacenamiento** cuadro de diálogo solo quita de la lista de Hola de cuentas de almacenamiento pueden visualizar en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e01ec-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="e01ec-149">No quita la cuenta de almacenamiento de Hola desde su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ec-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="e01ec-150">Además, cuenta de almacenamiento de hello podría aparecer de nuevo en la lista después de que Eclipse vuelva a cargar los detalles de Hola de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e01ec-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="e01ec-151">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e01ec-151">See Also</span></span>
<span data-ttu-id="e01ec-152">[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e01ec-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="e01ec-153">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e01ec-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="e01ec-154">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e01ec-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="e01ec-155">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="e01ec-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
