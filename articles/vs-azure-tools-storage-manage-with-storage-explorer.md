---
title: "aaaGet a trabajar con el Explorador de almacenamiento (versión preliminar) | Documentos de Microsoft"
description: "Administración de recursos de almacenamiento de Azure con el Explorador de almacenamiento (versión preliminar)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="8cf89-103">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8cf89-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="8cf89-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8cf89-104">Overview</span></span>
<span data-ttu-id="8cf89-105">Explorador de almacenamiento de Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="8cf89-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="8cf89-106">En este artículo, aprenderá Hola diversas formas de conectarse tooand administrar sus cuentas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Explorador de almacenamiento de Microsoft Azure (versión preliminar)][15]

## <a name="prerequisites"></a><span data-ttu-id="8cf89-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8cf89-108">Prerequisites</span></span>
* [<span data-ttu-id="8cf89-109">Descargue e instale el Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8cf89-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="8cf89-110">Conecte tooa cuenta de almacenamiento o servicio</span><span class="sxs-lookup"><span data-stu-id="8cf89-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="8cf89-111">Explorador de almacenamiento (versión preliminar) proporciona varias maneras de tooconnect toostorage cuentas.</span><span class="sxs-lookup"><span data-stu-id="8cf89-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="8cf89-112">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="8cf89-112">For example, you can:</span></span>
* <span data-ttu-id="8cf89-113">Conectar las cuentas de toostorage asociadas a las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="8cf89-114">Conectar toostorage cuentas y los servicios que se comparten desde otras suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="8cf89-115">Conectar tooand administrar el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="8cf89-116">Además, puede trabajar con cuentas de almacenamiento en nubes de Azure globales y nacionales:</span><span class="sxs-lookup"><span data-stu-id="8cf89-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="8cf89-117">[Conectar tooan suscripción de Azure](#connect-to-an-azure-subscription): administrar recursos de almacenamiento que pertenecen tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="8cf89-118">[Trabajar con almacenamiento de desarrollo local](#work-with-local-development-storage): administrar el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="8cf89-119">[Conectar almacenamiento tooexternal](#attach-or-detach-an-external-storage-account): administrar recursos de almacenamiento que pertenecen tooanother suscripción de Azure o que están bajo nubes Azure nacionales mediante nombre de la cuenta de almacenamiento de hello, claves y los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="8cf89-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="8cf89-120">[Asociar una cuenta de almacenamiento mediante una SAS](#attach-storage-account-using-sas): administrar recursos de almacenamiento que pertenecen tooanother suscripción de Azure utilizando una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="8cf89-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="8cf89-121">[Asociar un servicio mediante una SAS](#attach-service-using-sas): administrar un servicio de almacenamiento específica (contenedor de blob, cola o tabla) que pertenece tooanother suscripción de Azure mediante el uso de una SAS.</span><span class="sxs-lookup"><span data-stu-id="8cf89-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="8cf89-122">Conectar tooan suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="8cf89-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="8cf89-123">Si aún no tiene ninguna cuenta de Azure, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8cf89-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="8cf89-124">En el Explorador de almacenamiento (versión preliminar), seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Configuración de la cuenta de Azure][0]

2. <span data-ttu-id="8cf89-126">panel izquierdo de Hello muestra todas las cuentas de Microsoft de Hola que ha iniciado la sesión.</span><span class="sxs-lookup"><span data-stu-id="8cf89-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="8cf89-127">cuenta de tooconnect tooanother, seleccione **agregar una cuenta**y, a continuación, siga Hola instrucciones toosign con una cuenta de Microsoft que está asociada con al menos una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8cf89-128">Conexión toonational Azure (por ejemplo, Azure en Alemania, administración pública de Azure y Azure China a través de inicio de sesión) actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="8cf89-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="8cf89-129">Vea Hola "adjuntar o separar una cuenta de almacenamiento externo" sección para saber cómo las cuentas de almacenamiento de Azure de toonational tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8cf89-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="8cf89-130">Después de iniciar sesión correctamente con una cuenta de Microsoft, Hola izquierda panel se llena con hello Azure suscripciones asociadas a esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="8cf89-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="8cf89-131">Seleccione Hola suscripciones de Azure que desee toowork con y, a continuación, seleccione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="8cf89-132">(Seleccione **todas las suscripciones** alterna seleccionando todas o ninguna de hello muestran las suscripciones de Azure.)</span><span class="sxs-lookup"><span data-stu-id="8cf89-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Selección de suscripciones de Azure][3]  
    <span data-ttu-id="8cf89-134">panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure Hola seleccionado.</span><span class="sxs-lookup"><span data-stu-id="8cf89-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Suscripciones de Azure seleccionadas][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="8cf89-136">Conectar suscripción de Azure pila tooan</span><span class="sxs-lookup"><span data-stu-id="8cf89-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="8cf89-137">Para obtener información acerca de la suscripción de Azure pila tooan conexión, consulte [conectar Explorador de almacenamiento tooan suscripción de Azure pila](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="8cf89-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="8cf89-138">Trabajo con el almacenamiento de desarrollo local</span><span class="sxs-lookup"><span data-stu-id="8cf89-138">Work with local development storage</span></span>
<span data-ttu-id="8cf89-139">Con el Explorador de almacenamiento (vista previa), puede trabajar en el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="8cf89-140">Este enfoque le permite escribir código frente a y el almacenamiento de prueba sin necesidad de tener una cuenta de almacenamiento implementada en Azure, porque la cuenta de almacenamiento de hello está siendo emulado por hello emulador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="8cf89-141">Hola emulador de almacenamiento de Azure actualmente solo se admite para Windows.</span><span class="sxs-lookup"><span data-stu-id="8cf89-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="8cf89-142">En el panel izquierdo de hello del explorador de almacenamiento (versión preliminar), expanda hello **(locales y adjuntas)** > **cuentas de almacenamiento** > **(desarrollo)** nodo.</span><span class="sxs-lookup"><span data-stu-id="8cf89-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nodo de desarrollo local][21]

2. <span data-ttu-id="8cf89-144">Si aún no ha instalado Hola emulador de almacenamiento de Azure, son toodo solicitada por lo que a través de una barra de información.</span><span class="sxs-lookup"><span data-stu-id="8cf89-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="8cf89-145">Si se muestra la barra de información de hello, seleccione **descargue la versión más reciente de hello**y, a continuación, instalar el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Mensaje para descargar el emulador de Almacenamiento de Azure][22]

3. <span data-ttu-id="8cf89-147">Después de instala el emulador de hello, puede crear y trabajar con tablas, colas y blobs locales.</span><span class="sxs-lookup"><span data-stu-id="8cf89-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="8cf89-148">toolearn cómo escribe toowork con cada cuenta de almacenamiento, consulte uno de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="8cf89-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="8cf89-149">Administración de recursos de Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="8cf89-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="8cf89-150">Administración de recursos de almacenamiento de recurso compartido de archivos de Azure; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="8cf89-151">Administración de recursos de Azure Queue Storage; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="8cf89-152">Administración de recursos de Azure Table Storage; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="8cf89-153">Conexión a almacenamiento externo</span><span class="sxs-lookup"><span data-stu-id="8cf89-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="8cf89-154">Con el Explorador de almacenamiento (vista previa), puede asociar las cuentas de almacenamiento de tooexternal para que pueden compartirse fácilmente las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8cf89-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="8cf89-155">Esta sección se explica cómo tooattach too(and detach from) cuentas de almacenamiento externo.</span><span class="sxs-lookup"><span data-stu-id="8cf89-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="8cf89-156">Obtener las credenciales de cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="8cf89-156">Get hello storage account credentials</span></span>
<span data-ttu-id="8cf89-157">tooshare una cuenta de almacenamiento externo, el propietario de Hola de esa cuenta debe primero obtener credenciales de hello (nombre de cuenta y clave) para la cuenta de hello y, a continuación, compartir esa información con hello quien desea tooattach toothat (externo) cuenta.</span><span class="sxs-lookup"><span data-stu-id="8cf89-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="8cf89-158">Puede obtener credenciales de cuenta de almacenamiento de Hola a través del portal de Azure Hola haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="8cf89-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="8cf89-159">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8cf89-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8cf89-160">Seleccione **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-160">Select **Browse**.</span></span>

3. <span data-ttu-id="8cf89-161">Seleccione **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="8cf89-162">En hello **cuentas de almacenamiento** hoja, seleccione Hola deseado cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8cf89-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="8cf89-163">En hello **configuración** hoja para hello seleccionado cuenta de almacenamiento, seleccione **las claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Opción de teclas de acceso][5]

6. <span data-ttu-id="8cf89-165">En hello **las claves de acceso** hoja, Hola copia **nombre de la cuenta de almacenamiento** y **key1** valores para su uso al asociar la cuenta de almacenamiento de toohello.</span><span class="sxs-lookup"><span data-stu-id="8cf89-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Claves de acceso][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="8cf89-167">Asociar la cuenta de almacenamiento externa tooan</span><span class="sxs-lookup"><span data-stu-id="8cf89-167">Attach tooan external storage account</span></span>
<span data-ttu-id="8cf89-168">cuenta de almacenamiento externo de tooattach tooan, necesita la cuenta de hello nombre y clave.</span><span class="sxs-lookup"><span data-stu-id="8cf89-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="8cf89-169">Hola "Obtener credenciales de cuenta de hello almacenamiento" sección explica cómo tooobtain estos valores de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf89-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="8cf89-170">Sin embargo, en el portal de hello, clave de cuenta de hello se denomina **key1**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="8cf89-171">Por tanto, cuando el Explorador de almacenamiento (versión preliminar) solicita una clave de cuenta, escriba Hola **key1** valor.</span><span class="sxs-lookup"><span data-stu-id="8cf89-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="8cf89-172">En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. <span data-ttu-id="8cf89-174">Hola **conectar tooAzure almacenamiento** diálogo cuadro, especifique la clave de la cuenta de hello (hello **key1** valor de hello portal de Azure) y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8cf89-175">Puede escribir la cadena de conexión de almacenamiento de Hola desde una cuenta de almacenamiento en Azure nacional.</span><span class="sxs-lookup"><span data-stu-id="8cf89-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="8cf89-176">Por ejemplo, cuentas de almacenamiento de tooconnect tooAzure Alemania, escriba similar toohello siguiente de cadenas de conexión:</span><span class="sxs-lookup"><span data-stu-id="8cf89-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="8cf89-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="8cf89-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="8cf89-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="8cf89-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="8cf89-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="8cf89-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="8cf89-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8cf89-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="8cf89-181">Puede obtener la cadena de conexión de Hola de hello Azure portal Hola igual manera que se describe en Hola sección "Obtener credenciales de cuenta de almacenamiento de Hola".</span><span class="sxs-lookup"><span data-stu-id="8cf89-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. <span data-ttu-id="8cf89-183">Hola **adjuntar almacenamiento externo** cuadro de diálogo hello **nombre-cuenta** cuadro, escriba el nombre de cuenta de almacenamiento de hello, especifique cualquier otro valor deseado y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Cuadro de diálogo Attach External Storage (Asociar almacenamiento externo)][8]

4. <span data-ttu-id="8cf89-185">Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="8cf89-186">Seleccione si desea toochange nada, **volver** y vuelva a escribir la configuración de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="8cf89-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="8cf89-187">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-187">Select **Connect**.</span></span>

6. <span data-ttu-id="8cf89-188">Cuando está conectado correctamente, se muestra la cuenta de almacenamiento externo de hello con **(externo)** anexa toohello nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8cf89-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Resultado de conexión de cuenta de almacenamiento externo tooan][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="8cf89-190">Desasociación de una cuenta de almacenamiento externo</span><span class="sxs-lookup"><span data-stu-id="8cf89-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="8cf89-191">Haga clic en la cuenta de almacenamiento externo de Hola que desee toodetach y, a continuación, seleccione **separar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Opción para desasociar del almacenamiento][10]

2. <span data-ttu-id="8cf89-193">En el mensaje de confirmación de hello, seleccione **Sí** desasociación de hello tooconfirm de cuenta de almacenamiento externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="8cf89-194">Asociación de una cuenta de almacenamiento mediante una SAS</span><span class="sxs-lookup"><span data-stu-id="8cf89-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="8cf89-195">Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite Hola, Administrador de una suscripción de Azure conceder acceso temporal de cuenta de almacenamiento de tooa sin necesidad de credenciales de suscripción de Azure tooprovide.</span><span class="sxs-lookup"><span data-stu-id="8cf89-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="8cf89-196">tooillustrate este escenario, vamos a decir que ese UserA es un administrador de una suscripción de Azure y UserA desea tooallow UserB tooaccess cuenta de almacenamiento durante un tiempo limitado con permisos específicos:</span><span class="sxs-lookup"><span data-stu-id="8cf89-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="8cf89-197">UserA genera una SAS (que consta de cadena de conexión de Hola Hola cuenta de almacenamiento) de una hora específica período y con permisos de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="8cf89-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="8cf89-198">Recursos compartidos de UserA Hola SAS con persona hello (UserB, en nuestro ejemplo) que desea la cuenta de almacenamiento de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="8cf89-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="8cf89-199">UserB registrará el Explorador de almacenamiento (versión preliminar) tooattach toohello pertenece tooUserA mediante el uso de hello proporcionado SAS.</span><span class="sxs-lookup"><span data-stu-id="8cf89-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="8cf89-200">Obtener una SAS para la cuenta de hello que desea tooshare</span><span class="sxs-lookup"><span data-stu-id="8cf89-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="8cf89-201">En el Explorador de almacenamiento (vista previa), haga clic en la cuenta de almacenamiento de Hola que desee compartir y, a continuación, seleccione **obtener firma de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opción de menú contextual para obtener la SAS][13]

2. <span data-ttu-id="8cf89-203">Hola **firma de acceso compartido** diálogo cuadro, especifique el período de tiempo de Hola y los permisos que desee para la cuenta de hello y, a continuación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="8cf89-204">![Cuadro de diálogo Get SAS (Obtener SAS)][14]</span><span class="sxs-lookup"><span data-stu-id="8cf89-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="8cf89-205">Hola **firma de acceso compartido** cuadro de diálogo se abre y muestra hello SAS.</span><span class="sxs-lookup"><span data-stu-id="8cf89-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="8cf89-206">Siguiente toohello **cadena de conexión**, seleccione **copia** toocopy se toohello Portapapeles y, a continuación, seleccione **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="8cf89-207">Asociar cuenta toohello compartido mediante Hola SAS</span><span class="sxs-lookup"><span data-stu-id="8cf89-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="8cf89-208">En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. <span data-ttu-id="8cf89-210">Hola **conectar tooAzure almacenamiento** cuadro de diálogo, especifique la cadena de conexión de hello y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. <span data-ttu-id="8cf89-212">Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="8cf89-213">cambios de toomake, seleccione **volver**y, a continuación, escriba la configuración de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="8cf89-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="8cf89-214">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-214">Select **Connect**.</span></span>

5. <span data-ttu-id="8cf89-215">Después de que está conectado, se muestra la cuenta de almacenamiento de hello con **(SAS)** anexa el nombre de la cuenta de toohello que ha proporcionado.</span><span class="sxs-lookup"><span data-stu-id="8cf89-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Resultado de la cuenta de tooan conectados mediante el uso de SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="8cf89-217">Asociación de un servicio mediante una SAS</span><span class="sxs-lookup"><span data-stu-id="8cf89-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="8cf89-218">sección de "Adjuntar una cuenta de almacenamiento mediante una SAS" Hello explica cómo un administrador de suscripción de Azure puede conceder cuenta de almacenamiento de acceso temporal tooa generar y compartir una SAS Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8cf89-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="8cf89-219">De igual forma, se puede generar una SAS para un servicio específico (contenedor de blobs, cola o tabla) dentro de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8cf89-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="8cf89-220">Generar una SAS para el servicio de Hola que desea tooshare</span><span class="sxs-lookup"><span data-stu-id="8cf89-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="8cf89-221">En este contexto, un servicio puede ser un contenedor de blobs, una cola o una tabla.</span><span class="sxs-lookup"><span data-stu-id="8cf89-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="8cf89-222">Hola toogenerate SAS para un servicio de la lista, vea:</span><span class="sxs-lookup"><span data-stu-id="8cf89-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="8cf89-223">Obtener Hola SAS para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="8cf89-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="8cf89-224">Obtener Hola SAS para un recurso compartido de archivos: *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="8cf89-225">Obtener Hola SAS para una cola: *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="8cf89-226">Obtener Hola SAS para una tabla: *próximamente*</span><span class="sxs-lookup"><span data-stu-id="8cf89-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="8cf89-227">Asociar cuenta toohello compartido Hola de servicio mediante el uso de SAS</span><span class="sxs-lookup"><span data-stu-id="8cf89-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="8cf89-228">En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. <span data-ttu-id="8cf89-230">Hola **conectar tooAzure almacenamiento** cuadro de diálogo, especifique el URI de SAS de hello y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. <span data-ttu-id="8cf89-232">Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="8cf89-233">cambios de toomake, seleccione **volver**y, a continuación, escriba la configuración de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="8cf89-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="8cf89-234">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8cf89-234">Select **Connect**.</span></span>

5. <span data-ttu-id="8cf89-235">Una vez que se conecta, hello servicio recién conectado se muestra en hello **(servicio SAS)** nodo.</span><span class="sxs-lookup"><span data-stu-id="8cf89-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Resultado de adjuntar servicio tooa compartido mediante una SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="8cf89-237">Búsqueda de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8cf89-237">Search for storage accounts</span></span>
<span data-ttu-id="8cf89-238">Si tiene una larga lista de cuentas de almacenamiento, un toolocate de forma rápida una cuenta de almacenamiento concreta es toouse Hola búsqueda cuadro Hola parte superior del panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cf89-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="8cf89-239">Cuando escribe en el cuadro de búsqueda de hello, Hola panel izquierdo de las cuentas de almacenamiento de hello muestra que coinciden con el valor de búsqueda de Hola que ha especificado seguridad toothat punto.</span><span class="sxs-lookup"><span data-stu-id="8cf89-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="8cf89-240">Por ejemplo, una búsqueda para todo el almacenamiento de cuentas cuyo nombre contenga **tarcher** se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="8cf89-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Búsqueda de cuenta de almacenamiento][11]

## <a name="next-steps"></a><span data-ttu-id="8cf89-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8cf89-242">Next steps</span></span>
* [<span data-ttu-id="8cf89-243">Administración de recursos de Azure Blob Storage con el Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8cf89-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
