---
title: "Explorador de almacenamiento de aaaConnect tooan suscripción de la pila de Azure"
description: "Obtenga información acerca de cómo tooconnect Exporer de almacenamiento tooan suscripción de la pila de Azure"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a><span data-ttu-id="34ecb-103">Conectar Explorador de almacenamiento tooan Azure pila suscripción</span><span class="sxs-lookup"><span data-stu-id="34ecb-103">Connect Storage Explorer tooan Azure Stack subscription</span></span>

<span data-ttu-id="34ecb-104">Explorador de almacenamiento de Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de la pila de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="34ecb-104">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="34ecb-105">Hay varias herramientas permiten toomove datos tooand pila del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="34ecb-105">There are several tools avaialble toomove data tooand from Azure Stack Storage.</span></span> <span data-ttu-id="34ecb-106">Para más información, consulte [Herramientas de transferencia de datos de Azure Stack Storage](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="34ecb-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="34ecb-107">En este artículo, aprenderá cómo tooconnect tooyour almacenamiento de Azure pila cuentas con el Explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="34ecb-107">In this article, you learn how tooconnect tooyour Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="34ecb-108">Si no ha instalado todavía el Explorador de Storage, [descárguelo](http://www.storageexplorer.com/) y hágalo.</span><span class="sxs-lookup"><span data-stu-id="34ecb-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="34ecb-109">Después de conectar tooyour suscripción de pila de Azure, puede usar hello [artículos Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork con los datos de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="34ecb-109">After you connect tooyour Azure Stack subscription, you can use hello [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="34ecb-110">Preparación de una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34ecb-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="34ecb-111">Necesitará tener acceso de escritorio de la máquina de host de toohello pila de Azure o una conexión VPN para la suscripción de Azure pila de explorador de almacenamiento tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="34ecb-111">You need access toohello Azure Stack host machine's desktop or a VPN connection for Storage Explorer tooaccess hello Azure Stack subscription.</span></span> <span data-ttu-id="34ecb-112">toolearn tooset seguridad un tooAzure de conexión VPN pila, vea [conectar tooAzure pila con VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="34ecb-112">toolearn how tooset up a VPN connection tooAzure Stack, see [Connect tooAzure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="34ecb-113">Para hello Kit de desarrollo de pila de Azure, necesita certificado de raíz de entidad emisora de tooexport Hola pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="34ecb-113">For hello Azure Stack Development Kit, you need tooexport hello Azure Stack authority root certificate.</span></span>

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a><span data-ttu-id="34ecb-114">tooexport y, a continuación, importar hello Azure pila certificado</span><span class="sxs-lookup"><span data-stu-id="34ecb-114">tooexport and then import hello Azure Stack certificate</span></span>

1. <span data-ttu-id="34ecb-115">Abra `mmc.exe` en un equipo de host de la pila de Azure, o en un equipo local con una tooAzure de conexión VPN pila.</span><span class="sxs-lookup"><span data-stu-id="34ecb-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection tooAzure Stack.</span></span> 

2. <span data-ttu-id="34ecb-116">En **archivo**, seleccione **agregar o quitar complemento**y, a continuación, agregue **certificados** toomanage **cuenta de equipo** de **Local Equipo**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** toomanage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="34ecb-117">En **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** busque **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Cargar certificado de raíz de hello Azure pila mediante mmc.exe][25]

4. <span data-ttu-id="34ecb-119">El certificado de Hola de menú contextual, seleccione **todas las tareas** > **exportar**y, a continuación, siga el certificado de Hola Hola instrucciones tooexport con **codificado en Base 64 X.509 (. CER)**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-119">Right-click hello certificate, select **All Tasks** > **Export**, and then follow hello instructions tooexport hello certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="34ecb-120">se usará en el paso siguiente de Hola Hola de certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="34ecb-120">hello exported certificate will be used in hello next step.</span></span>
5. <span data-ttu-id="34ecb-121">Inicie el Explorador de almacenamiento (versión preliminar), y si ve hello **conectar tooAzure almacenamiento** diálogo cuadro, cancele el proceso.</span><span class="sxs-lookup"><span data-stu-id="34ecb-121">Start Storage Explorer (Preview), and if you see hello **Connect tooAzure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="34ecb-122">En hello **editar** menú, seleccione demasiado**certificados SSL**y, a continuación, haga clic en **importar certificados**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-122">On hello **Edit** menu, point too**SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="34ecb-123">Utilice toofind del cuadro de diálogo de hello archivo selector y el certificado de hello abierto que exportó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="34ecb-123">Use hello file picker dialog box toofind and open hello certificate that you exported in hello previous step.</span></span>

    <span data-ttu-id="34ecb-124">Después de importar, son toorestart solicitada Explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="34ecb-124">After importing, you are prompted toorestart Storage Explorer.</span></span>

    ![Importar el certificado de hello en el Explorador de almacenamiento (versión preliminar)][27]

<span data-ttu-id="34ecb-126">Ahora está listo tooconnect suscripción de Azure pila tooan de explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="34ecb-126">Now you are ready tooconnect Storage Explorer tooan Azure Stack subscription.</span></span>

### <a name="tooconnect-an-azure-stack-subscription"></a><span data-ttu-id="34ecb-127">tooconnect una suscripción de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="34ecb-127">tooconnect an Azure Stack subscription</span></span>


1. <span data-ttu-id="34ecb-128">Una vez reiniciado el Explorador de almacenamiento (versión preliminar), seleccione hello **editar** menú y, a continuación, asegúrese de que **pila de Azure de destino** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="34ecb-128">After Storage Explorer (Preview) restarts, select hello **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="34ecb-129">Si no está seleccionada, selecciónela y, a continuación, reinicie el Explorador de almacenamiento para cambiar tootake efecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="34ecb-129">If it is not selected, select it, and then restart Storage Explorer for hello change tootake effect.</span></span> <span data-ttu-id="34ecb-130">Esta configuración es necesaria para obtener compatibilidad con el entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="34ecb-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![Comprobación de que Azure Stack de destino está activada][28]

7. <span data-ttu-id="34ecb-132">En el panel izquierdo de hello, seleccione **administrar cuentas de**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-132">In hello left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="34ecb-133">Que ha iniciado sesión tooare muestra todas las cuentas de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="34ecb-133">All hello Microsoft accounts that you are signed in tooare displayed.</span></span>

8. <span data-ttu-id="34ecb-134">tooconnect toohello cuenta de la pila de Azure, seleccione **agregar una cuenta**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-134">tooconnect toohello Azure Stack account, select **Add an account**.</span></span>

    ![Adición de una cuenta de Azure Stack][29]

9. <span data-ttu-id="34ecb-136">Hola **conectar tooAzure almacenamiento** cuadro de diálogo **entorno de Azure**, seleccione **entorno de pila de usar Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-136">In hello **Connect tooAzure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="34ecb-137">toosign con hello cuenta de pila de Azure que está asociado con al menos una suscripción activa de la pila de Azure, rellene hello **iniciar sesión en el entorno de pila tooAzure** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34ecb-137">toosign in with hello Azure Stack account that's associated with at least one active Azure Stack subscription, fill in hello **Sign in tooAzure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="34ecb-138">detalles de Hola para cada campo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="34ecb-138">hello details for each field are as follows:</span></span>

    * <span data-ttu-id="34ecb-139">**Nombre del entorno**: campo de hello puede personalizarse por usuario.</span><span class="sxs-lookup"><span data-stu-id="34ecb-139">**Environment name**: hello field can be customized by user.</span></span>
    * <span data-ttu-id="34ecb-140">**Punto de conexión de recurso ARM**: Hola ejemplos de puntos de conexión de recursos de Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="34ecb-140">**ARM resource endpoint**: hello samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="34ecb-141">Para operadores en la nube:</span><span class="sxs-lookup"><span data-stu-id="34ecb-141">For cloud operator:</span></span><br> <span data-ttu-id="34ecb-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="34ecb-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="34ecb-143">Para el inquilino:</span><span class="sxs-lookup"><span data-stu-id="34ecb-143">For tenant:</span></span><br> <span data-ttu-id="34ecb-144">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="34ecb-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="34ecb-145">**Identificador de inquilino**: opcional.</span><span class="sxs-lookup"><span data-stu-id="34ecb-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="34ecb-146">se asigna un valor de Hello solo cuando se debe especificar el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="34ecb-146">hello value is given only when hello directory must be specified.</span></span>

12. <span data-ttu-id="34ecb-147">Una vez que inicie sesión correctamente con una cuenta de la pila de Azure, panel izquierdo de Hola se rellena con las suscripciones de Azure pila Hola asociadas con esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="34ecb-147">After you successfully sign in with an Azure Stack account, hello left pane is populated with hello Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="34ecb-148">Seleccione las suscripciones de la pila de Azure de Hola que desee toowork con y, a continuación, seleccione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="34ecb-148">Select hello Azure Stack subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="34ecb-149">(Activando o desactivando hello **todas las suscripciones** alterna de casilla de verificación Seleccionar todos o ninguno de Hola muestran las suscripciones de la pila de Azure.)</span><span class="sxs-lookup"><span data-stu-id="34ecb-149">(Selecting or clearing hello **All subscriptions** check box toggles selecting all or none of hello listed Azure Stack subscriptions.)</span></span>

    ![Seleccione las suscripciones de Azure pila Hola después de rellenar el cuadro de diálogo del entorno de nube personalizada hello][30]  
    <span data-ttu-id="34ecb-151">panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure pila Hola seleccionado.</span><span class="sxs-lookup"><span data-stu-id="34ecb-151">hello left pane displays hello storage accounts associated with hello selected Azure Stack subscriptions.</span></span>

    ![Lista de cuentas de almacenamiento, incluidas las cuentas de suscripción de Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="34ecb-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34ecb-153">Next steps</span></span>
* [<span data-ttu-id="34ecb-154">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="34ecb-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="34ecb-155">Azure Stack Storage: Diferencias y consideraciones</span><span class="sxs-lookup"><span data-stu-id="34ecb-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="34ecb-156">toolearn más sobre el almacenamiento de Azure, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="34ecb-156">toolearn more about Azure Storage, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
