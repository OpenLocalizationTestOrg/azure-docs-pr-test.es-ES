---
title: aaaCreate una cuenta de lote en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un lote de Azure cuenta hello Azure toorun portal las cargas de trabajo paralelas a gran escala en la nube de Hola"
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
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="410b4-103">Crear una cuenta de lote con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="410b4-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="410b4-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="410b4-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="410b4-105">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="410b4-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="410b4-106">Obtenga información acerca de cómo toocreate un lote de Azure cuenta Hola [portal de Azure][azure_portal]y elija Propiedades de la cuenta de hello que se ajusten a su escenario de proceso.</span><span class="sxs-lookup"><span data-stu-id="410b4-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="410b4-107">Obtenga información acerca de dónde propiedades de cuenta importante de toofind como teclas de acceso y las direcciones URL de cuenta.</span><span class="sxs-lookup"><span data-stu-id="410b4-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="410b4-108">Para obtener información acerca de los escenarios y las cuentas por lotes, vea hello [Introducción a las funciones](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="410b4-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="410b4-109">Crear una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="410b4-109">Create a Batch account</span></span>

<span data-ttu-id="410b4-110">Usar Hola portal toocreate una cuenta de lote en uno de dos hello *modos de asignación del grupo*: **por lotes servicio** modo o versiones más recientes de hello **suscripción de usuario** modo, que requiere más configuración.</span><span class="sxs-lookup"><span data-stu-id="410b4-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="410b4-111">Para obtener información acerca de estos dos modos, vea hello [Introducción a las funciones](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="410b4-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="410b4-112">Para las características del modo de suscripción de usuario de hello, vea también hello [entrada de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="410b4-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="410b4-113">Modo de servicio de Batch</span><span class="sxs-lookup"><span data-stu-id="410b4-113">Batch service mode</span></span>



1. <span data-ttu-id="410b4-114">Inicie sesión en toohello [portal de Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="410b4-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="410b4-115">Haga clic en **Nuevo** > **Proceso** > **Servicio de Batch**.</span><span class="sxs-lookup"><span data-stu-id="410b4-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote de hello Marketplace][marketplace_portal]
3. <span data-ttu-id="410b4-117">Hola **nueva cuenta de lote** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="410b4-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="410b4-118">Ver una descripción de hello debajo de cada elemento de la hoja.</span><span class="sxs-lookup"><span data-stu-id="410b4-118">See hello descriptions below of each blade element.</span></span>

    ![Crear una cuenta de lote][account_portal]

    <span data-ttu-id="410b4-120">a.</span><span class="sxs-lookup"><span data-stu-id="410b4-120">a.</span></span> <span data-ttu-id="410b4-121">**Nombre de la cuenta**: nombre de cuenta de lote Hola que elija debe ser único dentro de la región de Azure donde se crea la cuenta de Hola Hola (vea **ubicación** a continuación).</span><span class="sxs-lookup"><span data-stu-id="410b4-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="410b4-122">nombre de la cuenta de Hello puede contener solo caracteres en minúsculas o números y debe ser 3 y 24 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="410b4-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="410b4-123">b.</span><span class="sxs-lookup"><span data-stu-id="410b4-123">b.</span></span> <span data-ttu-id="410b4-124">**Suscripción**: Hola suscripción en qué hello toocreate cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="410b4-125">Si tiene una sola suscripción, se selecciona de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="410b4-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="410b4-126">c.</span><span class="sxs-lookup"><span data-stu-id="410b4-126">c.</span></span> <span data-ttu-id="410b4-127">**Modo de asignación de grupo**: seleccione **Servicio Batch**.</span><span class="sxs-lookup"><span data-stu-id="410b4-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="410b4-128">c.</span><span class="sxs-lookup"><span data-stu-id="410b4-128">c.</span></span> <span data-ttu-id="410b4-129">**Grupo de recursos**: seleccione un grupo de recursos existente para la nueva cuenta de Batch, o bien cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="410b4-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="410b4-130">d.</span><span class="sxs-lookup"><span data-stu-id="410b4-130">d.</span></span> <span data-ttu-id="410b4-131">**Ubicación**: Hola región de Azure en qué hello toocreate cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="410b4-132">Solo las regiones de hello compatibles con su suscripción y el grupo de recursos se muestran como opciones.</span><span class="sxs-lookup"><span data-stu-id="410b4-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="410b4-133">e.</span><span class="sxs-lookup"><span data-stu-id="410b4-133">e.</span></span> <span data-ttu-id="410b4-134">**Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="410b4-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="410b4-135">Se recomienda su uso para la mayoría de las cuentas de Batch.</span><span class="sxs-lookup"><span data-stu-id="410b4-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="410b4-136">Consulte [Cuenta de Azure Storage vinculada](#linked-azure-storage-account) más adelante en este artículo para más información.</span><span class="sxs-lookup"><span data-stu-id="410b4-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="410b4-137">Haga clic en **crear** cuenta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="410b4-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="410b4-138">portal de Hello indica la implementación está en curso.</span><span class="sxs-lookup"><span data-stu-id="410b4-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="410b4-139">Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="410b4-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="410b4-140">Modo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="410b4-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="410b4-141">Permitir Azure Batch tooaccess suscripción hello (operación única)</span><span class="sxs-lookup"><span data-stu-id="410b4-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="410b4-142">Al crear la primera cuenta de lote en modo de suscripción de usuario, realizar Hola siguiendo los pasos tooregister su suscripción con el lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="410b4-143">(Si lo hizo anteriormente, omita la sección siguiente toohello.)</span><span class="sxs-lookup"><span data-stu-id="410b4-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="410b4-144">Inicie sesión en toohello [portal de Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="410b4-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="410b4-145">Haga clic en **más servicios** > **suscripciones**y haga clic en la suscripción de Hola que desee toouse para hello cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="410b4-146">Hola **suscripción** hoja, haga clic en **(de índices IAM) de control de acceso** > **agregar**.</span><span class="sxs-lookup"><span data-stu-id="410b4-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Control de acceso a la suscripción][subscription_access]

4. <span data-ttu-id="410b4-148">En hello **agregar permisos** hoja, seleccione hello **colaborador** rol, busque Hola API de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="410b4-149">Buscar cada una de estas cadenas hasta que encuentre Hola API:</span><span class="sxs-lookup"><span data-stu-id="410b4-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="410b4-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="410b4-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="410b4-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="410b4-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="410b4-152">Los inquilinos más recientes de Azure AD pueden utilizar este nombre.</span><span class="sxs-lookup"><span data-stu-id="410b4-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="410b4-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** es Id. de Hola para hello API de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="410b4-154">Una vez que encuentre Hola API de lote, selecciónelo y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="410b4-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Adición de permisos de Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="410b4-156">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="410b4-156">Create a key vault</span></span>
<span data-ttu-id="410b4-157">En el modo de suscripción de usuario, se requiere un almacén de claves de Azure que pertenece toothe mismo grupo de recursos como toobe de cuenta de lote Hola creado.</span><span class="sxs-lookup"><span data-stu-id="410b4-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="410b4-158">Asegúrese de que el grupo de recursos de hello está en una región donde es el proceso por lotes [disponibles](https://azure.microsoft.com/regions/services/) y que es compatible con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="410b4-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="410b4-159">Hola [portal de Azure][azure_portal], haga clic en **New** > **seguridad e identidad** > **el almacén de claves** .</span><span class="sxs-lookup"><span data-stu-id="410b4-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="410b4-160">Hola **crear el almacén de claves** hoja, escriba un nombre para el almacén de claves de Hola y crear un grupo de recursos en la región de Hola que desee para su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="410b4-161">Deje Hola restantes parámetros utilizando valores predeterminados, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="410b4-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="410b4-162">Crear una cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="410b4-162">Create a Batch account</span></span>

1. <span data-ttu-id="410b4-163">Hola [portal de Azure][azure_portal], haga clic en **New** > **proceso** > **elservicioporlotes**.</span><span class="sxs-lookup"><span data-stu-id="410b4-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote de hello Marketplace][marketplace_portal]
3. <span data-ttu-id="410b4-165">Hola **nueva cuenta de lote** hoja se muestra.</span><span class="sxs-lookup"><span data-stu-id="410b4-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="410b4-166">Ver una descripción de hello debajo de cada elemento de la hoja.</span><span class="sxs-lookup"><span data-stu-id="410b4-166">See hello descriptions below of each blade element.</span></span>

    ![Crear una cuenta de lote][account_portal_byos]

    <span data-ttu-id="410b4-168">a.</span><span class="sxs-lookup"><span data-stu-id="410b4-168">a.</span></span> <span data-ttu-id="410b4-169">**Nombre de la cuenta**: nombre de cuenta de lote Hola que elija debe ser único dentro de la región de Azure donde se crea la cuenta de Hola Hola (vea **ubicación** a continuación).</span><span class="sxs-lookup"><span data-stu-id="410b4-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="410b4-170">nombre de la cuenta de Hello puede contener solo caracteres en minúsculas o números y debe ser 3 y 24 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="410b4-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="410b4-171">b.</span><span class="sxs-lookup"><span data-stu-id="410b4-171">b.</span></span> <span data-ttu-id="410b4-172">**Suscripción**: si tiene más de una suscripción, seleccione la suscripción de Hola que ha registrado con hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="410b4-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="410b4-173">c.</span><span class="sxs-lookup"><span data-stu-id="410b4-173">c.</span></span> <span data-ttu-id="410b4-174">**Modo de asignación de grupo**: seleccione **Suscripción del usuario**.</span><span class="sxs-lookup"><span data-stu-id="410b4-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="410b4-175">d.</span><span class="sxs-lookup"><span data-stu-id="410b4-175">d.</span></span> <span data-ttu-id="410b4-176">**Almacén de claves**: almacén de claves de hello Select que creó para la cuenta de lote en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="410b4-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="410b4-177">También puede crear un nuevo almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="410b4-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="410b4-178">Después de seleccionar el almacén de hello, seleccione Hola casilla toogrant Azure Batch acceso toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="410b4-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="410b4-179">c.</span><span class="sxs-lookup"><span data-stu-id="410b4-179">c.</span></span> <span data-ttu-id="410b4-180">**Grupo de recursos**: grupo de recursos de hello Select en la que creó el almacén de claves Hola.</span><span class="sxs-lookup"><span data-stu-id="410b4-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="410b4-181">d.</span><span class="sxs-lookup"><span data-stu-id="410b4-181">d.</span></span> <span data-ttu-id="410b4-182">**Ubicación**: Hola región de Azure en la que creó el almacén de claves de Hola Hola cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="410b4-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="410b4-183">e.</span><span class="sxs-lookup"><span data-stu-id="410b4-183">e.</span></span> <span data-ttu-id="410b4-184">**Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="410b4-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="410b4-185">Se recomienda su uso para la mayoría de las cuentas de Batch.</span><span class="sxs-lookup"><span data-stu-id="410b4-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="410b4-186">Consulte [Cuenta de Almacenamiento de Azure vinculada](#linked-azure-storage-account) a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="410b4-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="410b4-187">Haga clic en **crear** cuenta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="410b4-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="410b4-188">portal de Hello indica la implementación está en curso.</span><span class="sxs-lookup"><span data-stu-id="410b4-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="410b4-189">Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="410b4-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="410b4-190">Visualización de propiedades de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="410b4-190">View Batch account properties</span></span>
<span data-ttu-id="410b4-191">Una vez que se ha creado la cuenta de hello, puede abrir hello **hoja de la cuenta de lote** tooaccess su configuración y las propiedades.</span><span class="sxs-lookup"><span data-stu-id="410b4-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="410b4-192">Puede tener acceso a todas las propiedades y configuración de la cuenta mediante el uso de menú de la izquierda Hola de hoja de cuenta de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="410b4-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Hoja Cuenta de Batch en el Portal de Azure][account_blade]

* <span data-ttu-id="410b4-194">**URL de la cuenta de lote**: al desarrollar una aplicación con hello [API de lote](batch-apis-tools.md#azure-accounts-for-batch-development), necesitará un tooaccess de dirección URL de la cuenta los recursos de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="410b4-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="410b4-195">Una URL de la cuenta de lote tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="410b4-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![Dirección URL de la cuenta de Batch en el portal][account_url]

* <span data-ttu-id="410b4-197">**Las claves de acceso** (modo de servicio por lotes): tooauthenticate acceso tooyour cuenta de lote de la aplicación, necesitará una clave de acceso de cuenta.</span><span class="sxs-lookup"><span data-stu-id="410b4-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="410b4-198">(Esta configuración no está disponible en el modo de suscripción de usuario, en el que se usa la autenticación de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="410b4-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="410b4-199">tooview o regenerar claves de acceso de su cuenta de lote, escriba `keys` en el menú de la izquierda hello **búsqueda** cuadro hoja de cuenta de lote de hello, a continuación, seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="410b4-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Claves de la cuenta de Lote en el Portal de Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="410b4-201">Cuenta de Almacenamiento de Azure vinculada</span><span class="sxs-lookup"><span data-stu-id="410b4-201">Linked Azure Storage account</span></span>

<span data-ttu-id="410b4-202">Opcionalmente, puede vincular un uso general tooyour de cuenta cuenta de lote de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="410b4-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="410b4-203">Hola [paquetes de aplicación](batch-application-packages.md) característica del lote utiliza el almacenamiento de blobs de Azure, igual hello [.NET de convenciones de archivo por lotes](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="410b4-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="410b4-204">Estas características opcionales le ayudará a implementar aplicaciones de Hola que se ejecutan las tareas por lotes y conservar los datos de Hola que generan.</span><span class="sxs-lookup"><span data-stu-id="410b4-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="410b4-205">Se recomienda crear una cuenta de Storage nueva para que la use exclusivamente su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="410b4-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Creación de una cuenta de almacenamiento de uso general][storage_account]

> [!NOTE]
> <span data-ttu-id="410b4-207">Lote de Azure admite actualmente solo Hola almacenamiento cuenta tipos de uso general.</span><span class="sxs-lookup"><span data-stu-id="410b4-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="410b4-208">Este tipo de cuenta se describe en el paso 5, [Crear una cuenta de almacenamiento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), de [Acerca de las cuentas de Azure Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="410b4-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="410b4-209">Tenga cuidado al volver a generar las claves de acceso de Hola de una cuenta de almacenamiento vinculada.</span><span class="sxs-lookup"><span data-stu-id="410b4-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="410b4-210">Volver a generar solo una clave de cuenta de almacenamiento y haga clic en **claves sincronización** en hello vinculado hoja de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="410b4-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="410b4-211">Espere cinco minutos tooallow Hola claves toopropagate toohello nodos de cálculo en los grupos, a continuación, volver a generar y sincronizar Hola otra clave si es necesario.</span><span class="sxs-lookup"><span data-stu-id="410b4-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="410b4-212">Si vuelve a generarlas claves en hello mismo tiempo, los nodos de proceso no será capaz de toosynchronize la clave y perderá la cuenta de almacenamiento de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="410b4-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="410b4-213">![Regeneración de claves de cuenta de almacenamiento][4]</span><span class="sxs-lookup"><span data-stu-id="410b4-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="410b4-214">Límites y cuotas del servicio Lote</span><span class="sxs-lookup"><span data-stu-id="410b4-214">Batch service quotas and limits</span></span>
<span data-ttu-id="410b4-215">Ten en cuenta que como con la suscripción de Azure y otro Azure servicios, ciertos [cuotas y límites](batch-quota-limit.md) tooBatch cuentas se aplican.</span><span class="sxs-lookup"><span data-stu-id="410b4-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="410b4-216">Las cuotas de actuales de una cuenta de lote aparecen en portal de hello en la cuenta de hello **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="410b4-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Cuotas de la cuenta de Lote en el Portal de Azure][quotas]



<span data-ttu-id="410b4-218">Además, muchas de estas cuotas pueden aumentarse simplemente con una solicitud de soporte técnico de producto gratuito enviada en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="410b4-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="410b4-219">Vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener más información sobre cómo aumentar la cuota se solicita.</span><span class="sxs-lookup"><span data-stu-id="410b4-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="410b4-220">Otras opciones de administración de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="410b4-220">Other Batch account management options</span></span>
<span data-ttu-id="410b4-221">Además toousing Hola portal de Azure, también puede crear y administrar cuentas de lote con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="410b4-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="410b4-222">Cmdlets de PowerShell de Batch</span><span class="sxs-lookup"><span data-stu-id="410b4-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="410b4-223">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="410b4-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="410b4-224">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="410b4-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="410b4-225">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="410b4-225">Next steps</span></span>
* <span data-ttu-id="410b4-226">Vea hello [Introducción a la característica por lotes](batch-api-basics.md) toolearn más información sobre características y conceptos del servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="410b4-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="410b4-227">artículo de Hola describe los recursos de proceso por lotes principales hello como grupos, los nodos de proceso, trabajos y tareas y proporciona una visión general de hello características del servicio que permiten la ejecución de la carga de trabajo de proceso a gran escala.</span><span class="sxs-lookup"><span data-stu-id="410b4-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="410b4-228">Información sobre conceptos básicos de Hola de desarrollar una aplicación habilitada por lotes con hello [biblioteca de cliente .NET de lote](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="410b4-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="410b4-229">Estos artículos de Introducción le guiará a través de una aplicación que usa Hola lote servicio tooexecute una carga de trabajo en varios nodos de ejecución e incluye el uso de almacenamiento de Azure para recuperación y almacenamiento provisional del archivo de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="410b4-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

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
