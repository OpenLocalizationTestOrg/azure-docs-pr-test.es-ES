---
title: "Introducción al Explorador de Storage (versión preliminar) | Microsoft Docs"
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="b128b-103">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b128b-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="b128b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b128b-104">Overview</span></span>
<span data-ttu-id="b128b-105">El Explorador de Azure Storage (versión preliminar) es una aplicación independiente que permite trabajar fácilmente con datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="b128b-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="b128b-106">En este artículo aprenderá las diferentes maneras de conectarse a cuentas de Azure Storage y de administrarlas.</span><span class="sxs-lookup"><span data-stu-id="b128b-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Explorador de almacenamiento de Microsoft Azure (versión preliminar)][15]

## <a name="prerequisites"></a><span data-ttu-id="b128b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b128b-108">Prerequisites</span></span>
* [<span data-ttu-id="b128b-109">Descargue e instale el Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b128b-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="b128b-110">Conexión a una cuenta de almacenamiento o servicio</span><span class="sxs-lookup"><span data-stu-id="b128b-110">Connect to a storage account or service</span></span>
<span data-ttu-id="b128b-111">El Explorador de Storage (versión preliminar) proporciona varias maneras de conectar con las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b128b-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="b128b-112">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="b128b-112">For example, you can:</span></span>
* <span data-ttu-id="b128b-113">Conectar con las cuentas de almacenamiento asociadas a las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b128b-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="b128b-114">Conectar con las cuentas de almacenamiento y los servicios que se comparten desde otras suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b128b-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="b128b-115">Conectar con el almacenamiento local, y administrarlo, mediante el Emulador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b128b-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="b128b-116">Además, puede trabajar con cuentas de almacenamiento en nubes de Azure globales y nacionales:</span><span class="sxs-lookup"><span data-stu-id="b128b-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="b128b-117">[Conexión a una suscripción de Azure](#connect-to-an-azure-subscription): administre los recursos de almacenamiento que pertenecen a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b128b-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="b128b-118">[Trabajo con el almacenamiento de desarrollo local](#work-with-local-development-storage): administre el almacenamiento local mediante el Emulador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b128b-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="b128b-119">[Conexión a almacenamiento externo](#attach-or-detach-an-external-storage-account): administre los recursos de almacenamiento que pertenecen a otra suscripción de Azure o que se encuentran en nubes de Azure nacionales mediante el nombre, la clave y los puntos de conexión de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b128b-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="b128b-120">[Asociación de una cuenta de almacenamiento mediante una SAS](#attach-storage-account-using-sas): administre recursos de almacenamiento que pertenecen a otra suscripción de Azure mediante una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="b128b-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="b128b-121">[Asociación de un servicio mediante una SAS](#attach-service-using-sas): administre un servicio de almacenamiento específico (contenedor de blobs, cola o tabla) que pertenece a otra suscripción de Azure mediante una SAS.</span><span class="sxs-lookup"><span data-stu-id="b128b-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="b128b-122">Conexión a una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="b128b-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="b128b-123">Si aún no tiene ninguna cuenta de Azure, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b128b-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="b128b-124">En el Explorador de almacenamiento (versión preliminar), seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b128b-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Configuración de la cuenta de Azure][0]

2. <span data-ttu-id="b128b-126">En el panel izquierdo se muestran todas las cuentas de Microsoft en las que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="b128b-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="b128b-127">Para conectarse a otra cuenta, seleccione **Agregar una cuenta** y siga las instrucciones para iniciar sesión con una cuenta de Microsoft que esté asociada a una suscripción activa de Azure por lo menos.</span><span class="sxs-lookup"><span data-stu-id="b128b-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b128b-128">Actualmente no se admite la conexión a una nube de Azure nacional (como Azure Alemania, Azure Government y Azure China mediante inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="b128b-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="b128b-129">Consulte la sección "Conexión a almacenamiento externo" para saber cómo conectarse a cuentas de Azure Storage nacionales.</span><span class="sxs-lookup"><span data-stu-id="b128b-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="b128b-130">Después de haber iniciado sesión correctamente con una cuenta de Microsoft, el panel izquierdo se llenará con las suscripciones de Azure asociadas a dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="b128b-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="b128b-131">Elija las suscripciones de Azure con las que desea trabajar y luego seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="b128b-132">(Al seleccionar **Todas las suscripciones** , se alterna entre todas o ninguna de las suscripciones de Azure que aparecen).</span><span class="sxs-lookup"><span data-stu-id="b128b-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Selección de suscripciones de Azure][3]  
    <span data-ttu-id="b128b-134">El panel izquierdo muestra ahora las cuentas de almacenamiento asociadas a las suscripciones de Azure seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="b128b-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Suscripciones de Azure seleccionadas][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="b128b-136">Conexión a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b128b-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="b128b-137">Para más información sobre cómo conectarse a una suscripción de Azure Stack, consulte [Conexión de Storage Explorer a una suscripción de Azure Stack](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="b128b-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="b128b-138">Trabajo con el almacenamiento de desarrollo local</span><span class="sxs-lookup"><span data-stu-id="b128b-138">Work with local development storage</span></span>
<span data-ttu-id="b128b-139">Con el Explorador de Storage (versión preliminar), puede trabajar con el almacenamiento local mediante el Emulador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b128b-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="b128b-140">Este enfoque le permite escribir código y realizar pruebas de almacenamiento sin necesidad de tener una cuenta de almacenamiento implementada en Azure (ya que el Emulador de Azure Storage emula dicha cuenta).</span><span class="sxs-lookup"><span data-stu-id="b128b-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="b128b-141">El Emulador de almacenamiento de Azure actualmente solo se admite para Windows.</span><span class="sxs-lookup"><span data-stu-id="b128b-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="b128b-142">En el panel izquierdo del Explorador de Storage (versión preliminar), expanda el nodo **Local and Attached (Local y asociados)** > **Cuentas de almacenamiento** > **(Desarrollo)**.</span><span class="sxs-lookup"><span data-stu-id="b128b-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nodo de desarrollo local][21]

2. <span data-ttu-id="b128b-144">Si aún no ha instalado el Emulador de Azure Storage, se le solicita que lo haga a través de una barra de información.</span><span class="sxs-lookup"><span data-stu-id="b128b-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="b128b-145">Si se muestra la barra de información, seleccione **Descargar la última versión** e instale el emulador.</span><span class="sxs-lookup"><span data-stu-id="b128b-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Mensaje para descargar el emulador de Almacenamiento de Azure][22]

3. <span data-ttu-id="b128b-147">Después de que el emulador se ha instalado, puede crear tablas, colas y blobs locales, y trabajar con ellos.</span><span class="sxs-lookup"><span data-stu-id="b128b-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="b128b-148">Para aprender a trabajar con cada tipo de cuenta de almacenamiento, seleccione uno de los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="b128b-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="b128b-149">Administración de recursos de Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b128b-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="b128b-150">Administración de recursos de almacenamiento de recurso compartido de archivos de Azure; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="b128b-151">Administración de recursos de Azure Queue Storage; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="b128b-152">Administración de recursos de Azure Table Storage; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="b128b-153">Conexión a almacenamiento externo</span><span class="sxs-lookup"><span data-stu-id="b128b-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="b128b-154">Con el Explorador de Storage (versión preliminar), puede conectarse a cuentas de almacenamiento externas, lo que facilita el uso compartido de las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b128b-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="b128b-155">En esta sección se explica cómo asociar (y desasociar) cuentas de almacenamiento externo.</span><span class="sxs-lookup"><span data-stu-id="b128b-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="b128b-156">Obtención de las credenciales de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b128b-156">Get the storage account credentials</span></span>
<span data-ttu-id="b128b-157">Para compartir una cuenta de almacenamiento externa, su propietario debe obtener primero las credenciales (nombre y clave de cuenta) de esta, y compartir dicha información con la persona que desea asociar a dicha cuenta (externa).</span><span class="sxs-lookup"><span data-stu-id="b128b-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="b128b-158">Puede obtener las credenciales de la cuenta de almacenamiento mediante el portal de Azure haciendo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b128b-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="b128b-159">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b128b-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b128b-160">Seleccione **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-160">Select **Browse**.</span></span>

3. <span data-ttu-id="b128b-161">Seleccione **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b128b-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="b128b-162">En la hoja **Cuentas de almacenamiento**, seleccione la cuenta de almacenamiento deseada.</span><span class="sxs-lookup"><span data-stu-id="b128b-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="b128b-163">En la hoja **Configuración** de la cuenta de almacenamiento elegida, seleccione **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="b128b-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Opción de teclas de acceso][5]

6. <span data-ttu-id="b128b-165">En la hoja **Claves de acceso**, copie los valores de **Nombre de cuenta de almacenamiento** y **key1** para usarlos en la conexión a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b128b-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Claves de acceso][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="b128b-167">Asociación de una cuenta de almacenamiento externo</span><span class="sxs-lookup"><span data-stu-id="b128b-167">Attach to an external storage account</span></span>
<span data-ttu-id="b128b-168">Para la asociación a una cuenta de almacenamiento externa, se necesitan el nombre y la clave de la misma.</span><span class="sxs-lookup"><span data-stu-id="b128b-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="b128b-169">En la sección "Obtención de las credenciales de la cuenta de almacenamiento" se explica cómo obtener estos valores desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b128b-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="b128b-170">Sin embargo, en el portal, la clave de cuenta se denomina **key1**.</span><span class="sxs-lookup"><span data-stu-id="b128b-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="b128b-171">Por tanto, cuando el Explorador de Storage (versión preliminar) solicite una clave de cuenta, escriba el valor **key1**.</span><span class="sxs-lookup"><span data-stu-id="b128b-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="b128b-172">En el Explorador de almacenamiento (versión preliminar), seleccione **Connect to Azure storage**(Conectar con el almacenamiento de Azure).</span><span class="sxs-lookup"><span data-stu-id="b128b-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opción de conexión a Almacenamiento de Azure][23]

2. <span data-ttu-id="b128b-174">En el cuadro de diálogo **Connect to Azure storage** (Conectar con Azure Storage), especifique la clave de cuenta (el valor **key1** del portal de Azure) y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b128b-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b128b-175">Puede escribir la cadena de conexión de almacenamiento desde una cuenta de almacenamiento en una nube de Azure nacional.</span><span class="sxs-lookup"><span data-stu-id="b128b-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="b128b-176">Por ejemplo, para conectarse a las cuentas de almacenamiento de Azure Alemania, escriba cadenas de conexión similares a las siguientes:</span><span class="sxs-lookup"><span data-stu-id="b128b-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="b128b-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="b128b-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="b128b-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="b128b-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="b128b-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="b128b-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="b128b-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="b128b-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="b128b-181">Puede obtener la cadena de conexión desde el portal de Azure tal y como se describe en la sección "Obtención de las credenciales de la cuenta de almacenamiento".</span><span class="sxs-lookup"><span data-stu-id="b128b-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Cuadro de diálogo Connect to Azure storage (Conectar con Azure Storage)][24]

3. <span data-ttu-id="b128b-183">En el cuadro de diálogo **Attach External Storage** (Asociar almacenamiento externo), escriba el nombre de la cuenta de almacenamiento en el cuadro **Nombre de la cuenta**, especifique los demás valores deseados y luego seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b128b-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Cuadro de diálogo Attach External Storage (Asociar almacenamiento externo)][8]

4. <span data-ttu-id="b128b-185">En el cuadro de diálogo **Connection Summary** (Resumen de conexiones), compruebe la información.</span><span class="sxs-lookup"><span data-stu-id="b128b-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b128b-186">Si desea cambiar algo, seleccione **Atrás** y vuelva a escribir la configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="b128b-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="b128b-187">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-187">Select **Connect**.</span></span>

6. <span data-ttu-id="b128b-188">Una vez conectado correctamente, se muestra la cuenta de almacenamiento externa con el texto **(Externa)** junto al nombre de esta.</span><span class="sxs-lookup"><span data-stu-id="b128b-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Resultado de la conexión a una cuenta de almacenamiento externo][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="b128b-190">Desasociación de una cuenta de almacenamiento externo</span><span class="sxs-lookup"><span data-stu-id="b128b-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="b128b-191">Haga clic con el botón derecho en la cuenta de almacenamiento externa que desea desconectar y luego seleccione **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Opción para desasociar del almacenamiento][10]

2. <span data-ttu-id="b128b-193">En el mensaje de confirmación, seleccione **Sí** para confirmar la desasociación de la cuenta de almacenamiento externa.</span><span class="sxs-lookup"><span data-stu-id="b128b-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="b128b-194">Asociación de una cuenta de almacenamiento mediante una SAS</span><span class="sxs-lookup"><span data-stu-id="b128b-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="b128b-195">Una [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite al administrador de una suscripción de Azure conceder acceso temporal a una cuenta de almacenamiento sin tener que proporcionar las credenciales de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b128b-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="b128b-196">Para ilustrar este escenario, supongamos que el Usuario A es administrador de una suscripción de Azure y desea permitir que el Usuario B acceda a una cuenta de almacenamiento durante un tiempo limitado con determinados permisos:</span><span class="sxs-lookup"><span data-stu-id="b128b-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="b128b-197">El Usuario A genera una SAS (que consiste en una cadena de conexión para la cuenta de almacenamiento) durante un período de tiempo específico y con los permisos deseados.</span><span class="sxs-lookup"><span data-stu-id="b128b-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="b128b-198">El Usuario A comparte la SAS con la persona que desea tener acceso a la cuenta de almacenamiento (en nuestro ejemplo el Usuario B).</span><span class="sxs-lookup"><span data-stu-id="b128b-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="b128b-199">El Usuario B usa el Explorador de Storage (versión preliminar) para conectarse a la cuenta que pertenece al Usuario A, con la SAS proporcionada.</span><span class="sxs-lookup"><span data-stu-id="b128b-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="b128b-200">Obtención de una SAS para la cuenta que se desea compartir</span><span class="sxs-lookup"><span data-stu-id="b128b-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="b128b-201">En el Explorador de Storage (versión preliminar), haga clic con el botón derecho en la cuenta de almacenamiento que quiere compartir y seleccione **Get Shared Access Signature**(Obtener firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="b128b-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opción de menú contextual para obtener la SAS][13]

2. <span data-ttu-id="b128b-203">En el cuadro de diálogo **Firma de acceso compartido**, especifique el período y los permisos que desee para la cuenta y luego seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b128b-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="b128b-204">![Cuadro de diálogo Get SAS (Obtener SAS)][14]</span><span class="sxs-lookup"><span data-stu-id="b128b-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="b128b-205">Se abre el cuadro de diálogo **Firma de acceso compartido**, que muestra la SAS.</span><span class="sxs-lookup"><span data-stu-id="b128b-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="b128b-206">Junto a la **cadena de conexión**, seleccione **Copiar** para copiarla en el Portapapeles y, a continuación, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="b128b-207">Conexión a la cuenta compartida mediante la SAS</span><span class="sxs-lookup"><span data-stu-id="b128b-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="b128b-208">En el Explorador de almacenamiento (versión preliminar), seleccione **Connect to Azure storage**(Conectar con el almacenamiento de Azure).</span><span class="sxs-lookup"><span data-stu-id="b128b-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opción de conexión a Almacenamiento de Azure][23]

2. <span data-ttu-id="b128b-210">En el cuadro de diálogo **Connect to Azure storage** (Conectar con Azure Storage), especifique la cadena de conexión y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b128b-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Cuadro de diálogo Connect to Azure storage (Conectar con Azure Storage)][24]

3. <span data-ttu-id="b128b-212">En el cuadro de diálogo **Connection Summary** (Resumen de conexiones), compruebe la información.</span><span class="sxs-lookup"><span data-stu-id="b128b-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b128b-213">Para realizar cambios, seleccione **Atrás** y luego escriba los valores de configuración deseados.</span><span class="sxs-lookup"><span data-stu-id="b128b-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="b128b-214">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-214">Select **Connect**.</span></span>

5. <span data-ttu-id="b128b-215">Después de conectarse, la cuenta de almacenamiento se muestra con **(SAS)** anexada al nombre de cuenta que ha proporcionado.</span><span class="sxs-lookup"><span data-stu-id="b128b-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![Resultado de conectarse a una cuenta mediante SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="b128b-217">Asociación de un servicio mediante una SAS</span><span class="sxs-lookup"><span data-stu-id="b128b-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="b128b-218">En la sección "Asociación de una cuenta de almacenamiento mediante una SAS" se explica cómo el administrador de una suscripción de Azure puede conceder acceso temporal a una cuenta de almacenamiento mediante la generación y el uso compartido de una SAS para dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="b128b-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="b128b-219">De igual forma, se puede generar una SAS para un servicio específico (contenedor de blobs, cola o tabla) dentro de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b128b-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="b128b-220">Generación de una SAS para el servicio que se desea compartir</span><span class="sxs-lookup"><span data-stu-id="b128b-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="b128b-221">En este contexto, un servicio puede ser un contenedor de blobs, una cola o una tabla.</span><span class="sxs-lookup"><span data-stu-id="b128b-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="b128b-222">Para generar la SAS para un servicio enumerado, consulte:</span><span class="sxs-lookup"><span data-stu-id="b128b-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="b128b-223">Get the SAS for a blob container (Obtención de la SAS para un contenedor de blobs)</span><span class="sxs-lookup"><span data-stu-id="b128b-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="b128b-224">Obtención de la SAS para un recurso compartido de archivos; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="b128b-225">Obtención de la SAS para una cola; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="b128b-226">Obtención de la SAS para una tabla; *próximamente*</span><span class="sxs-lookup"><span data-stu-id="b128b-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="b128b-227">Conexión al servicio de la cuenta de almacenamiento mediante la SAS</span><span class="sxs-lookup"><span data-stu-id="b128b-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="b128b-228">En el Explorador de almacenamiento (versión preliminar), seleccione **Connect to Azure storage**(Conectar con el almacenamiento de Azure).</span><span class="sxs-lookup"><span data-stu-id="b128b-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opción de conexión a Almacenamiento de Azure][23]

2. <span data-ttu-id="b128b-230">En el cuadro de diálogo **Connect to Azure storage** (Conectar con Azure Storage), especifique el identificador URI de SAS y luego seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b128b-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Cuadro de diálogo Connect to Azure storage (Conectar con Azure Storage)][24]

3. <span data-ttu-id="b128b-232">En el cuadro de diálogo **Connection Summary** (Resumen de conexiones), compruebe la información.</span><span class="sxs-lookup"><span data-stu-id="b128b-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b128b-233">Para realizar cambios, seleccione **Atrás** y luego escriba los valores de configuración deseados.</span><span class="sxs-lookup"><span data-stu-id="b128b-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="b128b-234">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="b128b-234">Select **Connect**.</span></span>

5. <span data-ttu-id="b128b-235">Una vez conectado, el servicio aparecerá en el nodo **(Service SAS)** [(SAS de servicio)].</span><span class="sxs-lookup"><span data-stu-id="b128b-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Resultado de la conexión a un servicio compartido mediante una SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="b128b-237">Búsqueda de cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b128b-237">Search for storage accounts</span></span>
<span data-ttu-id="b128b-238">Si tiene una larga lista de cuentas de almacenamiento, puede usar el cuadro de búsqueda en la parte superior del panel izquierdo para encontrar rápidamente una cuenta de almacenamiento concreta.</span><span class="sxs-lookup"><span data-stu-id="b128b-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="b128b-239">A medida que vaya escribiendo en el cuadro de búsqueda, el panel izquierdo mostrará solo las cuentas de almacenamiento que coincidan con el valor de búsqueda que haya escrito hasta ese momento.</span><span class="sxs-lookup"><span data-stu-id="b128b-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="b128b-240">Por ejemplo, en la pantalla siguiente se muestra una búsqueda de todas las cuentas de almacenamiento cuyo nombre contenga **tarcher**:</span><span class="sxs-lookup"><span data-stu-id="b128b-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Búsqueda de cuenta de almacenamiento][11]

## <a name="next-steps"></a><span data-ttu-id="b128b-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b128b-242">Next steps</span></span>
* [<span data-ttu-id="b128b-243">Administración de recursos de Azure Blob Storage con el Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b128b-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
