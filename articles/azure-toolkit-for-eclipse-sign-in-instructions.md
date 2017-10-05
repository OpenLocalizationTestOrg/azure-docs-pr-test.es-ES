---
title: "Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse | Microsoft Docs"
description: "Obtenga información sobre cómo iniciar sesión en Microsoft Azure utilizando el Kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9ef28-103">Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="9ef28-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="9ef28-104">El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="9ef28-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="9ef28-105">**Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef28-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="9ef28-106">**Automatizado**: al utilizar este método, se creará un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Después, podrá utilizar el archivo de credenciales para iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef28-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="9ef28-107">Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.</span><span class="sxs-lookup"><span data-stu-id="9ef28-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="9ef28-108">Inicio de sesión en la cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="9ef28-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="9ef28-109">En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef28-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="9ef28-110">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ef28-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9ef28-111">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. <span data-ttu-id="9ef28-113">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][I02]

1. <span data-ttu-id="9ef28-115">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. <span data-ttu-id="9ef28-117">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="9ef28-119">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="9ef28-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="9ef28-120">Después de haber configurado los pasos en la sección anterior, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ef28-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="9ef28-121">Sin embargo, si desea cerrar sesión de su cuenta de Azure sin tener que reiniciar Eclipse, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9ef28-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="9ef28-122">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="9ef28-124">Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="9ef28-126">Inicio de sesión en su cuenta de Azure de forma automática y creación de un archivo de credenciales para utilizarlo en el futuro</span><span class="sxs-lookup"><span data-stu-id="9ef28-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="9ef28-127">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9ef28-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="9ef28-128">Cuando finalice estos pasos, Eclipse usará automáticamente el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9ef28-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="9ef28-129">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ef28-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9ef28-130">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="9ef28-132">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="9ef28-134">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. <span data-ttu-id="9ef28-136">Cuando se muestre el cuadro de diálogo **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. <span data-ttu-id="9ef28-138">Se mostrará el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio) y, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. <span data-ttu-id="9ef28-140">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="9ef28-142">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="9ef28-144">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="9ef28-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="9ef28-145">Después de haber configurado los pasos en la sección anterior, el kit de herramientas de Azure cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ef28-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="9ef28-146">Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9ef28-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="9ef28-147">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="9ef28-149">Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="9ef28-151">Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente</span><span class="sxs-lookup"><span data-stu-id="9ef28-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="9ef28-152">Si cierra la sesión de Azure al utilizar Eclipse, debe volver a configurar el kit de herramientas de Azure para Eclipse con el fin de usar un archivo de credenciales ya creado antes de poder iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef28-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="9ef28-153">Los siguientes pasos lo guiarán a través del proceso de configuración del kit de herramientas de Azure para usar un archivo de credenciales existente.</span><span class="sxs-lookup"><span data-stu-id="9ef28-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="9ef28-154">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9ef28-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9ef28-155">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="9ef28-157">Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="9ef28-159">Cuando se muestra el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales que creó anteriormente y, luego, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A08]

1. <span data-ttu-id="9ef28-161">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="9ef28-163">Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9ef28-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="see-also"></a><span data-ttu-id="9ef28-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9ef28-165">See Also</span></span>
<span data-ttu-id="9ef28-166">Para más información acerca de los kits de herramientas de Azure para los IDE de Java, vea los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="9ef28-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="9ef28-167">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9ef28-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9ef28-168">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9ef28-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9ef28-169">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9ef28-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9ef28-170">*Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse* (este artículo)</span><span class="sxs-lookup"><span data-stu-id="9ef28-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="9ef28-171">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9ef28-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="9ef28-172">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9ef28-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9ef28-173">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9ef28-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9ef28-174">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9ef28-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9ef28-175">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9ef28-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9ef28-176">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9ef28-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="9ef28-177">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="9ef28-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="9ef28-178">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="9ef28-179">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="9ef28-180">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9ef28-181">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9ef28-182">[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="9ef28-183">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="9ef28-184">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="9ef28-185">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="9ef28-186">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9ef28-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="9ef28-187">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="9ef28-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="9ef28-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="9ef28-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
