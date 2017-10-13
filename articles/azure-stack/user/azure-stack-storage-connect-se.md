---
title: "Conexión del Explorador de Storage a una suscripción de Azure Stack"
description: "Aprenda a conectar el Explorador de Storage a una suscripción de Azure Stack"
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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: c7e6d70148d39fd74f6409a0a239833f8e9f7614
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription"></a><span data-ttu-id="3175a-103">Conexión del Explorador de Storage a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3175a-103">Connect Storage Explorer to an Azure Stack subscription</span></span>

<span data-ttu-id="3175a-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="3175a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="3175a-105">El Explorador de Azure Storage (versión preliminar) es una aplicación independiente que permite trabajar fácilmente con datos de Azure Stack Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="3175a-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3175a-106">Hay varias herramientas disponibles para mover datos hacia Azure Stack Storage y desde este.</span><span class="sxs-lookup"><span data-stu-id="3175a-106">There are several tools avaialble to move data to and from Azure Stack Storage.</span></span> <span data-ttu-id="3175a-107">Para más información, consulte [Herramientas de transferencia de datos de Azure Stack Storage](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="3175a-107">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="3175a-108">En este artículo, aprenderá a conectarse a sus cuentas de Azure Stack Storage mediante el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="3175a-108">In this article, you learn how to connect to your Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="3175a-109">Si no ha instalado todavía el Explorador de Storage, [descárguelo](http://www.storageexplorer.com/) y hágalo.</span><span class="sxs-lookup"><span data-stu-id="3175a-109">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="3175a-110">Después de conectarse a su suscripción de Azure Stack, puede usar los [artículos sobre el Explorador de Azure Storage](../../vs-azure-tools-storage-manage-with-storage-explorer.md) para trabajar con los datos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-110">After you connect to your Azure Stack subscription, you can use the [Azure Storage Explorer articles](../../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="3175a-111">Preparación de una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3175a-111">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="3175a-112">Necesita acceder al escritorio de la máquina del host de Azure Stack o una conexión VPN para que el Explorador de Storage pueda acceder de forma remota a la suscripción de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-112">You need access to the Azure Stack host machine's desktop or a VPN connection for Storage Explorer to access the Azure Stack subscription.</span></span> <span data-ttu-id="3175a-113">Para más información sobre cómo configurar una conexión VPN a Azure Stack, consulte [Conexión a Azure Stack con VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="3175a-113">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="3175a-114">Para Azure Stack Development Kit, debe exportar el certificado raíz de la entidad de certificación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-114">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span></span>

### <a name="to-export-and-then-import-the-azure-stack-certificate"></a><span data-ttu-id="3175a-115">Exportación y posterior importación del certificado de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3175a-115">To export and then import the Azure Stack certificate</span></span>

1. <span data-ttu-id="3175a-116">Abra `mmc.exe` en una máquina host de Azure Stack o una máquina local con una conexión VPN a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-116">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span></span> 

2. <span data-ttu-id="3175a-117">En **archivo**, seleccione **agregar o quitar complemento**y, a continuación, agregue **certificados** para administrar **mi cuenta de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3175a-117">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **My user account**.</span></span>



3. <span data-ttu-id="3175a-118">En **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** busque **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="3175a-118">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Carga del certificado raíz de Azure Stack a través de mmc.exe][25]

4. <span data-ttu-id="3175a-120">Haga clic con el botón derecho en el certificado, seleccione **Todas las tareas** > **Exportar** y luego siga las instrucciones para exportar el certificado con **X.509 (.CER) codificado en base 64**.</span><span class="sxs-lookup"><span data-stu-id="3175a-120">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="3175a-121">Se usará el certificado exportado en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="3175a-121">The exported certificate will be used in the next step.</span></span>
5. <span data-ttu-id="3175a-122">Inicie el Explorador de Storage (versión preliminar) y, si ve el cuadro de diálogo **Conectar a Azure Storage**, cancélelo.</span><span class="sxs-lookup"><span data-stu-id="3175a-122">Start Storage Explorer (Preview), and if you see the **Connect to Azure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="3175a-123">En el menú **Editar**, seleccione **Certificados SSL** y, luego, haga clic en **Importar certificados**.</span><span class="sxs-lookup"><span data-stu-id="3175a-123">On the **Edit** menu, point to **SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="3175a-124">Use el cuadro de diálogo del selector de archivos para buscar y abrir el certificado que exportó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="3175a-124">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span></span>

    <span data-ttu-id="3175a-125">Después de la importación, se le pedirá que reinicie el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="3175a-125">After importing, you are prompted to restart Storage Explorer.</span></span>

    ![Importe el certificado en el Explorador de Storage (versión preliminar)][27]

<span data-ttu-id="3175a-127">Ahora ya está listo para conectar el Explorador de Storage a una suscripción de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-127">Now you are ready to connect Storage Explorer to an Azure Stack subscription.</span></span>

### <a name="to-connect-an-azure-stack-subscription"></a><span data-ttu-id="3175a-128">Conexión a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3175a-128">To connect an Azure Stack subscription</span></span>


1. <span data-ttu-id="3175a-129">Después de que se reinicie el Explorador de Storage (versión preliminar), seleccione el menú **Editar** y luego asegúrese de que esté seleccionada la opción **Target Azure Stack** (Azure Stack de destino).</span><span class="sxs-lookup"><span data-stu-id="3175a-129">After Storage Explorer (Preview) restarts, select the **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="3175a-130">Si no está seleccionada, selecciónela y luego reinicie el Explorador de Storage para que el cambio surta efecto.</span><span class="sxs-lookup"><span data-stu-id="3175a-130">If it is not selected, select it, and then restart Storage Explorer for the change to take effect.</span></span> <span data-ttu-id="3175a-131">Esta configuración es necesaria para obtener compatibilidad con el entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3175a-131">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![Comprobación de que Azure Stack de destino está activada][28]

7. <span data-ttu-id="3175a-133">En el panel izquierdo, seleccione **Administrar cuentas**.</span><span class="sxs-lookup"><span data-stu-id="3175a-133">In the left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="3175a-134">Se muestran todas las cuentas de Microsoft en las que haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="3175a-134">All the Microsoft accounts that you are signed in to are displayed.</span></span>

8. <span data-ttu-id="3175a-135">Para conectarse a la cuenta de Azure Stack, seleccione **Agregar una cuenta**.</span><span class="sxs-lookup"><span data-stu-id="3175a-135">To connect to the Azure Stack account, select **Add an account**.</span></span>

    ![Adición de una cuenta de Azure Stack][29]

9. <span data-ttu-id="3175a-137">En el cuadro de diálogo **Conectar a Azure Storage**, en el **entorno de Azure**, seleccione **Use Azure Stack Environment** (Usar entorno de Azure Stack) y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3175a-137">In the **Connect to Azure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="3175a-138">Para iniciar sesión con la cuenta de Azure Stack que está asociada a una suscripción de Azure Stack activa por lo menos, rellene el cuadro de diálogo **Sign in to Azure Stack Environment** (Iniciar sesión en un entorno de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="3175a-138">To sign in with the Azure Stack account that's associated with at least one active Azure Stack subscription, fill in the **Sign in to Azure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="3175a-139">Los detalles de cada campo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3175a-139">The details for each field are as follows:</span></span>

    * <span data-ttu-id="3175a-140">**Environment name** (Nombre del entorno): el usuario puede personalizar este campo.</span><span class="sxs-lookup"><span data-stu-id="3175a-140">**Environment name**: The field can be customized by user.</span></span>
    * <span data-ttu-id="3175a-141">**ARM resource endpoint** (Punto de conexión de recurso de ARM): los ejemplos de los puntos de conexión de recursos de Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="3175a-141">**ARM resource endpoint**: The samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="3175a-142">Para operadores en la nube:</span><span class="sxs-lookup"><span data-stu-id="3175a-142">For cloud operator:</span></span><br> <span data-ttu-id="3175a-143">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3175a-143">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="3175a-144">Para el inquilino:</span><span class="sxs-lookup"><span data-stu-id="3175a-144">For tenant:</span></span><br> <span data-ttu-id="3175a-145">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3175a-145">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="3175a-146">**Identificador de inquilino**: opcional.</span><span class="sxs-lookup"><span data-stu-id="3175a-146">**Tenant Id**: Optional.</span></span> <span data-ttu-id="3175a-147">Se asigna un valor solo si se debe especificar el directorio.</span><span class="sxs-lookup"><span data-stu-id="3175a-147">The value is given only when the directory must be specified.</span></span>

12. <span data-ttu-id="3175a-148">Después de iniciar sesión correctamente con una cuenta de Azure Stack, el panel izquierdo se llena con las suscripciones de Azure Stack asociadas a dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="3175a-148">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="3175a-149">Seleccione las suscripciones de Azure Stack con la que quiere trabajar y luego seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="3175a-149">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="3175a-150">(Al activar o desactivar la casilla **Todas las suscripciones**, se alterna entre seleccionar todas o ninguna de las suscripciones de Azure Stack que aparecen).</span><span class="sxs-lookup"><span data-stu-id="3175a-150">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

    ![Selección de las suscripciones de Azure Stack después de rellenar el cuadro de diálogo Custom Cloud Environment (Entorno personalizado en la nube)][30]  
    <span data-ttu-id="3175a-152">El panel izquierdo muestra ahora las cuentas de almacenamiento asociadas a las suscripciones de Azure Stack seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="3175a-152">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![Lista de cuentas de almacenamiento, incluidas las cuentas de suscripción de Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="3175a-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3175a-154">Next steps</span></span>
* [<span data-ttu-id="3175a-155">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="3175a-155">Get started with Storage Explorer (Preview)</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="3175a-156">Azure Stack Storage: Diferencias y consideraciones</span><span class="sxs-lookup"><span data-stu-id="3175a-156">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="3175a-157">Para más información sobre Azure Storage, consulte [Introducción a Microsoft Azure Storage](../../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3175a-157">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
