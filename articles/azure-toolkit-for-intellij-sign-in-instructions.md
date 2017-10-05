---
title: "Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ | Microsoft Docs"
description: "Obtenga información sobre cómo iniciar sesión en Microsoft Azure con el kit de herramientas de Azure para IntelliJ."
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="18590-103">Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="18590-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="18590-104">El kit de herramientas de Azure para IntelliJ proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="18590-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="18590-105">**Interactivo**: escriba sus credenciales de Azure cada vez que inicie sesión su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="18590-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="18590-106">**Automatizado**: cree un archivo de credenciales que puede usar para iniciar sesión automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="18590-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="18590-107">Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.</span><span class="sxs-lookup"><span data-stu-id="18590-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="18590-108">Inicio de sesión en la cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="18590-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="18590-109">En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure:</span><span class="sxs-lookup"><span data-stu-id="18590-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="18590-110">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="18590-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="18590-111">Haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="18590-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][I01]

3. <span data-ttu-id="18590-113">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="18590-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Interactivo seleccionado][I02]

4. <span data-ttu-id="18590-115">Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="18590-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

5. <span data-ttu-id="18590-117">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18590-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="18590-119">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="18590-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="18590-120">Después de haber configurado la cuenta con los pasos anteriores, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="18590-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="18590-121">Sin embargo, si desea cerrar sesión de su cuenta de Azure *sin* tener que reiniciar IntelliJ IDEA, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="18590-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="18590-122">En IntelliJ IDEA, haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Cierre de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="18590-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![El comando de cierre de sesión en Azure IntelliJ][L01]

2. <span data-ttu-id="18590-124">En la ventana confirmación **Cierre de sesión en Microsoft Azure**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="18590-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![La ventana de confirmación Cierre de sesión en Microsoft Azure][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="18590-126">Inicio sesión en la cuenta de Azure de forma automática</span><span class="sxs-lookup"><span data-stu-id="18590-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="18590-127">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio.</span><span class="sxs-lookup"><span data-stu-id="18590-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="18590-128">Cuando finalice este proceso, Eclipse usará el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="18590-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="18590-129">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="18590-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="18590-130">En el menú **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="18590-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][A01]

3. <span data-ttu-id="18590-132">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="18590-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A02]

4. <span data-ttu-id="18590-134">En la ventana **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="18590-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![El cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

5. <span data-ttu-id="18590-136">En la ventana **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="18590-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![La ventana Create authentication files (Crear archivos de autenticación)][A04]

6. <span data-ttu-id="18590-138">En el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio), una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18590-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![El cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

7. <span data-ttu-id="18590-140">En la ventana **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="18590-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

8. <span data-ttu-id="18590-142">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18590-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="18590-144">Cierre de sesión de la cuenta de Azure después de haber iniciado sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="18590-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="18590-145">Después de haber configurado la cuenta con los pasos anteriores, el kit de herramientas de Azure iniciará sesión automáticamente en su cuenta de Azure cada vez que reinicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="18590-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="18590-146">Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="18590-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="18590-147">En IntelliJ IDEA, haga clic en **Herramientas**, seleccione **Azure** y, luego, haga clic en **Cierre de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="18590-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![El comando de cierre de sesión en Azure IntelliJ][L01]

2. <span data-ttu-id="18590-149">En la ventana confirmación **Cierre de sesión en Microsoft Azure**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="18590-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![La ventana de confirmación Cierre de sesión en Microsoft Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="18590-151">Inicio de sesión en su cuenta de Azure de forma automática mediante un archivo de credenciales</span><span class="sxs-lookup"><span data-stu-id="18590-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="18590-152">Si cierra la sesión de su cuenta de Azure mientras utiliza IntelliJ IDEA, debe usar un archivo de credenciales para iniciar sesión automáticamente en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="18590-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="18590-153">Para configurar el kit de herramientas de Azure para que Eclipse use un archivo de credenciales, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="18590-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="18590-154">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="18590-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="18590-155">En el menú **Herramientas**, seleccione **Azure** y, luego, haga clic en **Inicio de sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="18590-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![El comando de inicio de sesión en Azure IntelliJ][A01]

3. <span data-ttu-id="18590-157">En la ventana **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="18590-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A02]

4. <span data-ttu-id="18590-159">En el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales creado anteriormente y, luego, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="18590-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![El cuadro de diálogo Select Authentication File (Seleccionar archivo de autenticación)][A08]

5. <span data-ttu-id="18590-161">En la ventana **Inicio de sesión en Microsoft Azure**, haga clic en **Iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="18590-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![La ventana Inicio de sesión en Microsoft Azure con el modo Automatizado seleccionado][A06]

6. <span data-ttu-id="18590-163">En el cuadro de diálogo **Seleccionar suscripciones**, elija las suscripciones que desea usar y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18590-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="next-steps"></a><span data-ttu-id="18590-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18590-165">Next steps</span></span>
<span data-ttu-id="18590-166">Para más información acerca de los kits de herramientas de Azure para los IDE de Java, vea los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="18590-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="18590-167">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="18590-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="18590-168">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="18590-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="18590-169">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="18590-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="18590-170">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="18590-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="18590-171">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="18590-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="18590-172">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="18590-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="18590-173">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="18590-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="18590-174">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="18590-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="18590-175">*Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ* (este artículo)</span><span class="sxs-lookup"><span data-stu-id="18590-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="18590-176">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="18590-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="18590-177">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="18590-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="18590-178">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="18590-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="18590-179">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="18590-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="18590-180">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="18590-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="18590-181">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="18590-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="18590-182">[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="18590-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="18590-183">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="18590-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="18590-184">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="18590-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="18590-185">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="18590-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="18590-186">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="18590-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="18590-187">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="18590-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="18590-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="18590-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
