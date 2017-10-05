---
title: "Creación de una cuenta de Batch en Azure Portal | Microsoft Docs"
description: Aprenda a crear una cuenta de Lote de Azure en el Portal de Azure para ejecutar cargas de trabajo paralelas a gran escala en la nube
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 520d1d42d35b25db1a35d4317e9eb616cf5de565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="730bb-103">Creación de una cuenta de Batch con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="730bb-103">Create a Batch account with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="730bb-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="730bb-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="730bb-105">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="730bb-106">Aprenda a crear una cuenta de Azure Batch en [Azure Portal][azure_portal] y seleccione las propiedades de cuenta más adecuadas para su escenario de proceso.</span><span class="sxs-lookup"><span data-stu-id="730bb-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="730bb-107">Aprenda dónde encontrar importantes propiedades de cuenta, como teclas de acceso y direcciones URL de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="730bb-107">Learn where to find important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="730bb-108">Para más información acerca de los escenarios y las cuentas de Batch, consulte la [descripción de las características](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="730bb-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="730bb-109">Crear una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="730bb-109">Create a Batch account</span></span>

<span data-ttu-id="730bb-110">Use el portal para crear una cuenta de Batch con uno de los dos *modos de asignación de grupo*: el modo de **servicio Batch** o el modo más reciente de **suscripción de usuario**, que requiere una mayor configuración.</span><span class="sxs-lookup"><span data-stu-id="730bb-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="730bb-111">Para más información sobre estos dos modos, consulte la [descripción de las características](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="730bb-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="730bb-112">Consulte también esta [entrada de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/) para más información sobre las características del modo de suscripción de usuario.</span><span class="sxs-lookup"><span data-stu-id="730bb-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="730bb-113">Modo de servicio de Batch</span><span class="sxs-lookup"><span data-stu-id="730bb-113">Batch service mode</span></span>



1. <span data-ttu-id="730bb-114">Inicie sesión en [Azure Portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="730bb-114">Sign in to the [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="730bb-115">Haga clic en **Nuevo** > **Proceso** > **Servicio de Batch**.</span><span class="sxs-lookup"><span data-stu-id="730bb-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote en Marketplace][marketplace_portal]
3. <span data-ttu-id="730bb-117">Se muestra la hoja **Nueva cuenta de Lote** .</span><span class="sxs-lookup"><span data-stu-id="730bb-117">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="730bb-118">Consulte las descripciones siguientes de cada elemento de la hoja.</span><span class="sxs-lookup"><span data-stu-id="730bb-118">See the descriptions below of each blade element.</span></span>

    ![Crear una cuenta de lote][account_portal]

    <span data-ttu-id="730bb-120">a.</span><span class="sxs-lookup"><span data-stu-id="730bb-120">a.</span></span> <span data-ttu-id="730bb-121">**Nombre de la cuenta**: el nombre de la cuenta de Batch que elija debe ser único en la región de Azure en la que se crea cuenta (consulte **Ubicación** a continuación).</span><span class="sxs-lookup"><span data-stu-id="730bb-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="730bb-122">El nombre de la cuenta solo puede contener caracteres en minúsculas o números, y su longitud debe oscilar entre 3 y 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="730bb-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="730bb-123">b.</span><span class="sxs-lookup"><span data-stu-id="730bb-123">b.</span></span> <span data-ttu-id="730bb-124">**Suscripción**: la suscripción en la que se crea la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-124">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="730bb-125">Si tiene una sola suscripción, se selecciona de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="730bb-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="730bb-126">c.</span><span class="sxs-lookup"><span data-stu-id="730bb-126">c.</span></span> <span data-ttu-id="730bb-127">**Modo de asignación de grupo**: seleccione **Servicio Batch**.</span><span class="sxs-lookup"><span data-stu-id="730bb-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="730bb-128">c.</span><span class="sxs-lookup"><span data-stu-id="730bb-128">c.</span></span> <span data-ttu-id="730bb-129">**Grupo de recursos**: seleccione un grupo de recursos existente para la nueva cuenta de Batch, o bien cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="730bb-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="730bb-130">d.</span><span class="sxs-lookup"><span data-stu-id="730bb-130">d.</span></span> <span data-ttu-id="730bb-131">**Ubicación**: la región de Azure en la que se va a crear la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-131">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="730bb-132">Solo se muestran como opciones las regiones admitidas por su suscripción y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="730bb-132">Only the regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="730bb-133">e.</span><span class="sxs-lookup"><span data-stu-id="730bb-133">e.</span></span> <span data-ttu-id="730bb-134">**Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="730bb-135">Se recomienda su uso para la mayoría de las cuentas de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="730bb-136">Consulte [Cuenta de Azure Storage vinculada](#linked-azure-storage-account) más adelante en este artículo para más información.</span><span class="sxs-lookup"><span data-stu-id="730bb-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="730bb-137">Haga clic en **Crear** para crear la cuenta.</span><span class="sxs-lookup"><span data-stu-id="730bb-137">Click **Create** to create the account.</span></span>

   <span data-ttu-id="730bb-138">El portal indica que la implementación está en curso.</span><span class="sxs-lookup"><span data-stu-id="730bb-138">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="730bb-139">Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="730bb-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="730bb-140">Modo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="730bb-140">User subscription mode</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="730bb-141">Procedimiento para permitir que Azure Batch acceda a la suscripción (operación única)</span><span class="sxs-lookup"><span data-stu-id="730bb-141">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="730bb-142">Al crear la primera cuenta de Batch en modo de suscripción de usuario, realice los pasos siguientes para registrar la suscripción con Batch</span><span class="sxs-lookup"><span data-stu-id="730bb-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span></span> <span data-ttu-id="730bb-143">(si ya lo ha hecho anteriormente, vaya a la sección siguiente).</span><span class="sxs-lookup"><span data-stu-id="730bb-143">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="730bb-144">Inicie sesión en [Azure Portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="730bb-144">Sign in to the [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="730bb-145">Haga clic en **Más servicios** > **Suscripciones** y, a continuación, en la suscripción que desea usar para la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span></span>

3. <span data-ttu-id="730bb-146">En la hoja **Suscripción**, haga clic en **Control de acceso (IAM)** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="730bb-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Control de acceso a la suscripción][subscription_access]

4. <span data-ttu-id="730bb-148">En la hoja **Agregar permisos**, seleccione el rol **Colaborador** y busque Batch API.</span><span class="sxs-lookup"><span data-stu-id="730bb-148">On the **Add permissions** blade, select the **Contributor** role, search for the Batch API.</span></span> <span data-ttu-id="730bb-149">Busque cada una de estas cadenas hasta que encuentre la API:</span><span class="sxs-lookup"><span data-stu-id="730bb-149">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="730bb-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="730bb-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="730bb-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="730bb-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="730bb-152">Los inquilinos más recientes de Azure AD pueden utilizar este nombre.</span><span class="sxs-lookup"><span data-stu-id="730bb-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="730bb-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** es el identificador de Batch API.</span><span class="sxs-lookup"><span data-stu-id="730bb-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 

5. <span data-ttu-id="730bb-154">Una vez que encuentre Batch API, selecciónelo y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="730bb-154">Once you find the Batch API, select it and click **Save**.</span></span>

    ![Adición de permisos de Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="730bb-156">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="730bb-156">Create a key vault</span></span>
<span data-ttu-id="730bb-157">En el modo de suscripción de usuario, se requiere una instancia de Azure Key Vault que pertenezca al mismo grupo de recursos que la cuenta de Batch que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="730bb-157">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="730bb-158">Asegúrese de que el grupo de recursos se encuentre en una región en la que Batch esté [disponible](https://azure.microsoft.com/regions/services/) y que la suscripción admita.</span><span class="sxs-lookup"><span data-stu-id="730bb-158">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="730bb-159">En [Azure Portal][azure_portal], haga clic en **Nuevo** > **Seguridad e identidad** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="730bb-159">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="730bb-160">En la hoja **Crear Key Vault**, escriba un nombre para el almacén de claves y cree un grupo de recursos en la región que desee para su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-160">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="730bb-161">Deje los valores predeterminados para el resto de la configuración y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="730bb-161">Leave the remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="730bb-162">Crear una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="730bb-162">Create a Batch account</span></span>

1. <span data-ttu-id="730bb-163">En [Azure Portal][azure_portal], haga clic en **Nuevo** > **Compute** > **Servicio Batch**.</span><span class="sxs-lookup"><span data-stu-id="730bb-163">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote en Marketplace][marketplace_portal]
3. <span data-ttu-id="730bb-165">Se muestra la hoja **Nueva cuenta de Lote** .</span><span class="sxs-lookup"><span data-stu-id="730bb-165">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="730bb-166">Consulte las descripciones siguientes de cada elemento de la hoja.</span><span class="sxs-lookup"><span data-stu-id="730bb-166">See the descriptions below of each blade element.</span></span>

    ![Crear una cuenta de lote][account_portal_byos]

    <span data-ttu-id="730bb-168">a.</span><span class="sxs-lookup"><span data-stu-id="730bb-168">a.</span></span> <span data-ttu-id="730bb-169">**Nombre de la cuenta**: el nombre de la cuenta de Batch que elija debe ser único en la región de Azure en la que se crea cuenta (consulte **Ubicación** a continuación).</span><span class="sxs-lookup"><span data-stu-id="730bb-169">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="730bb-170">El nombre de la cuenta solo puede contener caracteres en minúsculas o números, y su longitud debe oscilar entre 3 y 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="730bb-170">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="730bb-171">b.</span><span class="sxs-lookup"><span data-stu-id="730bb-171">b.</span></span> <span data-ttu-id="730bb-172">**Suscripción**: si tiene varias suscripciones, seleccione la suscripción que haya registrado con el servicio de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-172">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span></span>

    <span data-ttu-id="730bb-173">c.</span><span class="sxs-lookup"><span data-stu-id="730bb-173">c.</span></span> <span data-ttu-id="730bb-174">**Modo de asignación de grupo**: seleccione **Suscripción del usuario**.</span><span class="sxs-lookup"><span data-stu-id="730bb-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="730bb-175">d.</span><span class="sxs-lookup"><span data-stu-id="730bb-175">d.</span></span> <span data-ttu-id="730bb-176">**Key Vault**: seleccione el almacén de claves que creó para la cuenta de Batch en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="730bb-176">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span></span> <span data-ttu-id="730bb-177">También puede crear un nuevo almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="730bb-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="730bb-178">Después de seleccionar el almacén, active la casilla para conceder a Azure Batch acceso al almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="730bb-178">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span></span>

    <span data-ttu-id="730bb-179">c.</span><span class="sxs-lookup"><span data-stu-id="730bb-179">c.</span></span> <span data-ttu-id="730bb-180">**Grupo de recursos**: seleccione el grupo de recursos en el que creó el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="730bb-180">**Resource group**: Select the resource group in which you  created the key vault.</span></span>

    <span data-ttu-id="730bb-181">d.</span><span class="sxs-lookup"><span data-stu-id="730bb-181">d.</span></span> <span data-ttu-id="730bb-182">**Ubicación**: la región de Azure en la que ha creado el almacén de claves para la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-182">**Location**: The Azure region in which you created the key vault for the Batch account.</span></span>

    <span data-ttu-id="730bb-183">e.</span><span class="sxs-lookup"><span data-stu-id="730bb-183">e.</span></span> <span data-ttu-id="730bb-184">**Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="730bb-185">Se recomienda su uso para la mayoría de las cuentas de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="730bb-186">Consulte [Cuenta de Almacenamiento de Azure vinculada](#linked-azure-storage-account) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="730bb-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="730bb-187">Haga clic en **Crear** para crear la cuenta.</span><span class="sxs-lookup"><span data-stu-id="730bb-187">Click **Create** to create the account.</span></span>

   <span data-ttu-id="730bb-188">El portal indica que la implementación está en curso.</span><span class="sxs-lookup"><span data-stu-id="730bb-188">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="730bb-189">Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="730bb-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="730bb-190">Visualización de propiedades de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-190">View Batch account properties</span></span>
<span data-ttu-id="730bb-191">Una vez creada la cuenta, puede abrir la **hoja de la cuenta de Lote** para acceder a sus propiedades y configuración.</span><span class="sxs-lookup"><span data-stu-id="730bb-191">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span></span> <span data-ttu-id="730bb-192">Puede tener acceso a todas las propiedades y configuración de la cuenta en el menú izquierdo de la hoja Cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-192">You can access all account settings and properties by using the left menu of the Batch account blade.</span></span>

![Hoja Cuenta de Batch en el Portal de Azure][account_blade]

* <span data-ttu-id="730bb-194">**URL cuenta de Batch**: al desarrollar una aplicación con las [API de Batch](batch-apis-tools.md#azure-accounts-for-batch-development), necesitará una dirección URL de la cuenta para acceder a los recursos de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-194">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL to access your Batch resources.</span></span> <span data-ttu-id="730bb-195">Una dirección URL de la cuenta de Batch tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="730bb-195">A Batch account URL has the following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![Dirección URL de la cuenta de Batch en el portal][account_url]

* <span data-ttu-id="730bb-197">**Claves de acceso** (modo de servicio de Batch): para autenticar el acceso a su cuenta de Batch desde su aplicación, necesitará una clave de acceso a la cuenta</span><span class="sxs-lookup"><span data-stu-id="730bb-197">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="730bb-198">(Esta configuración no está disponible en el modo de suscripción de usuario, en el que se usa la autenticación de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="730bb-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="730bb-199">Para ver o volver a generar las claves de acceso de la cuenta de Batch, escriba `keys` en el cuadro de **búsqueda** del menú de la izquierda, en la hoja de cuenta de Batch, y seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="730bb-199">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span></span>

    ![Claves de la cuenta de Lote en el Portal de Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="730bb-201">Cuenta de Almacenamiento de Azure vinculada</span><span class="sxs-lookup"><span data-stu-id="730bb-201">Linked Azure Storage account</span></span>

<span data-ttu-id="730bb-202">Existe la posibilidad de vincular una cuenta de Azure Storage de uso general a una cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-202">You can optionally link a general-purpose Azure Storage account to your Batch account.</span></span> <span data-ttu-id="730bb-203">La característica de [paquetes de aplicación](batch-application-packages.md) de Batch usa Azure Blob Storage, tal como hace la biblioteca [Batch File Conventions .NET](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="730bb-203">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="730bb-204">Estas características opcionales le ayudan a implementar las aplicaciones que ejecutan las tareas de Batch y a conservar los datos que generan.</span><span class="sxs-lookup"><span data-stu-id="730bb-204">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="730bb-205">Se recomienda crear una cuenta de Storage nueva para que la use exclusivamente su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="730bb-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Creación de una cuenta de almacenamiento de uso general][storage_account]

> [!NOTE]
> <span data-ttu-id="730bb-207">En la actualidad, Azure Batch solo admite el tipo de cuenta de Storage de uso general.</span><span class="sxs-lookup"><span data-stu-id="730bb-207">Azure Batch currently supports only the general-purpose Storage account type.</span></span> <span data-ttu-id="730bb-208">Este tipo de cuenta se describe en el paso 5, [Crear una cuenta de almacenamiento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), de [Acerca de las cuentas de Azure Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="730bb-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="730bb-209">Tenga cuidado al volver a generar las claves de acceso de una cuenta de Storage vinculada.</span><span class="sxs-lookup"><span data-stu-id="730bb-209">Be careful when regenerating the access keys of a linked Storage account.</span></span> <span data-ttu-id="730bb-210">Vuelva a generar solo una clave de la cuenta de almacenamiento y haga clic en **Sincronizar claves** en la hoja de la cuenta de almacenamiento vinculada.</span><span class="sxs-lookup"><span data-stu-id="730bb-210">Regenerate only one Storage account key and click **Sync Keys** on the linked Storage account blade.</span></span> <span data-ttu-id="730bb-211">Espere cinco minutos para que las claves se propaguen a los nodos de proceso de los grupos, y después vuelva a generar y sincronizar la otra clave si es necesario.</span><span class="sxs-lookup"><span data-stu-id="730bb-211">Wait five minutes to allow the keys to propagate to the compute nodes in your pools, then regenerate and synchronize the other key if necessary.</span></span> <span data-ttu-id="730bb-212">Si vuelve a generar las dos claves al mismo tiempo, los nodos de proceso no podrán sincronizar ninguna de las claves y perderán el acceso a la cuenta de Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="730bb-212">If you regenerate both keys at the same time, your compute nodes will not be able to synchronize either key, and they will lose access to the Storage account.</span></span>
>
>

<span data-ttu-id="730bb-213">![Regeneración de claves de cuenta de almacenamiento][4]</span><span class="sxs-lookup"><span data-stu-id="730bb-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="730bb-214">Límites y cuotas del servicio Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-214">Batch service quotas and limits</span></span>
<span data-ttu-id="730bb-215">Tenga en cuenta que como con su suscripción de Azure y otros servicios de Azure, se aplican ciertas [cuotas y límites](batch-quota-limit.md) a las cuentas de Lote.</span><span class="sxs-lookup"><span data-stu-id="730bb-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span></span> <span data-ttu-id="730bb-216">Las cuotas actuales de una cuenta de Lote aparecen en el portal en las **propiedades**de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="730bb-216">Current quotas for a Batch account appear in the portal in the account **Properties**.</span></span>

![Cuotas de la cuenta de Lote en el Portal de Azure][quotas]



<span data-ttu-id="730bb-218">Además, muchas de estas cuotas se pueden aumentar simplemente con una solicitud gratuita de soporte técnico de producto enviada en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="730bb-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span></span> <span data-ttu-id="730bb-219">Para más información sobre la solicitud de aumentos de cuotas, consulte [Cuotas y límites del servicio Lote de Azure](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="730bb-219">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="730bb-220">Otras opciones de administración de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-220">Other Batch account management options</span></span>
<span data-ttu-id="730bb-221">Además de usar el Portal de Azure, también puede crear y administrar cuentas de Lote con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="730bb-221">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span></span>

* [<span data-ttu-id="730bb-222">Cmdlets de PowerShell de Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="730bb-223">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="730bb-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="730bb-224">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="730bb-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="730bb-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="730bb-225">Next steps</span></span>
* <span data-ttu-id="730bb-226">Para más información acerca de los conceptos y las características del servicio de Batch, consulte la [descripción de las características de Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="730bb-226">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="730bb-227">El artículo describe los principales recursos de Lote como grupos, nodos de proceso, trabajos y tareas, y proporciona información general acerca de las características del servicio que permiten la ejecución de cargas de trabajo de proceso a gran escala.</span><span class="sxs-lookup"><span data-stu-id="730bb-227">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="730bb-228">Para conocer los aspectos básicos del desarrollo de una aplicación habilitada para Batch, consulte la [biblioteca de cliente de Batch para .NET](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="730bb-228">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="730bb-229">Estos artículos introductorios le guían a través de una aplicación activa que usa el servicio de Batch para ejecutar una carga de trabajo en varios nodos de proceso e incluye el uso de Azure Storage para el almacenamiento provisional y la recuperación del archivo de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="730bb-229">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regeneración de claves de cuenta de almacenamiento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
