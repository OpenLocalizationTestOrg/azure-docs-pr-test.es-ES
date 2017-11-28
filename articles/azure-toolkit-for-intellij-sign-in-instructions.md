---
title: instrucciones de aaaSign para hello Azure Toolkit para IntelliJ | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosign en tooMicrosoft Azure mediante el uso de Hola Kit de herramientas de Azure para IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="5dfad-103">Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5dfad-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="5dfad-104">Hello Azure Toolkit for IntelliJ proporciona dos métodos para iniciar sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="5dfad-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="5dfad-105">**Interactivo**: escriba sus credenciales de Azure cada vez que inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfad-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="5dfad-106">**Automatizada**: crear un archivo de credenciales que puede usar el inicio de sesión de tooautomatically en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfad-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="5dfad-107">Hello siguientes secciones se describen cómo toouse cada método.</span><span class="sxs-lookup"><span data-stu-id="5dfad-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="5dfad-108">Iniciar sesión en tooyour cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="5dfad-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="5dfad-109">toosign en tooAzure bien especificando sus credenciales de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5dfad-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="5dfad-110">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfad-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="5dfad-111">Haga clic en **herramientas**, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando de inicio de sesión en Azure IntelliJ Hola][I01]

3. <span data-ttu-id="5dfad-113">Hola **inicio de sesión en Azure** ventana, seleccione **Interactive**y, a continuación, haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![inicio de sesión de Azure en ventana Hello con interactivo seleccionado][I02]

4. <span data-ttu-id="5dfad-115">Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![cuadro de diálogo de inicio de sesión de Azure de Hola][I03]

5. <span data-ttu-id="5dfad-117">Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![cuadro de diálogo Seleccionar suscripciones Hola][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="5dfad-119">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="5dfad-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="5dfad-120">Después de haber configurado la cuenta mediante el uso de hello pasos anteriores, se cerrará sesión automáticamente en su cuenta de Azure cada vez que inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfad-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="5dfad-121">Sin embargo, si desea que toosign fuera de su cuenta de Azure *sin* reiniciar IntelliJ IDEA, Hola después.</span><span class="sxs-lookup"><span data-stu-id="5dfad-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="5dfad-122">En la IDEA de IntelliJ, en hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **Azure Sign Out**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hola comando IntelliJ el inicio de sesión de Azure Out][L01]

2. <span data-ttu-id="5dfad-124">Hola **Azure Sign Out** ventana de confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![ventana Hello Azure Sign Out confirmación][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="5dfad-126">Iniciar sesión en tooyour cuenta de Azure automáticamente</span><span class="sxs-lookup"><span data-stu-id="5dfad-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="5dfad-127">Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio.</span><span class="sxs-lookup"><span data-stu-id="5dfad-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="5dfad-128">Después de completar este proceso, Eclipse usa Hola credenciales archivo tooautomatically inicio de sesión que de tooAzure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="5dfad-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="5dfad-129">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfad-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="5dfad-130">En hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando de inicio de sesión en Azure IntelliJ Hola][A01]

3. <span data-ttu-id="5dfad-132">Hola **inicio de sesión en Azure** ventana, seleccione **automatizada**y, a continuación, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A02]

4. <span data-ttu-id="5dfad-134">Hola **cuadro de diálogo de inicio de sesión de Azure** ventana, escriba sus credenciales de Azure y, a continuación, haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![cuadro de diálogo de inicio de sesión de Azure de Hola][A03]

5. <span data-ttu-id="5dfad-136">Hola **crear archivos de autenticación** (ventana), las suscripciones de hello select que desee toouse, elija el directorio de destino y, a continuación, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![ventana de Hello crear archivos de autenticación][A04]

6. <span data-ttu-id="5dfad-138">Hola **estado de creación de entidad de servicio** cuadro de diálogo, después de que los archivos se han creado correctamente, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Hola, cuadro de diálogo de estado de creación de entidad de servicio][A05]

7. <span data-ttu-id="5dfad-140">Hola **inicio de sesión en Azure** ventana, haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

8. <span data-ttu-id="5dfad-142">Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![cuadro de diálogo Seleccionar suscripciones Hola][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="5dfad-144">Cierre de sesión de la cuenta de Azure después de haber iniciado sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="5dfad-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="5dfad-145">Después de haber configurado la cuenta mediante el uso de hello pasos anteriores, hello Azure Toolkit inicia automáticamente la sesión en tooyour cuenta de Azure cada vez que inicie IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfad-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="5dfad-146">Sin embargo, toosign fuera de su cuenta de Azure y evitar hello Azure Toolkit de iniciar sesión automáticamente, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5dfad-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="5dfad-147">En la IDEA de IntelliJ, en hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **Azure Sign Out**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hola comando IntelliJ el inicio de sesión de Azure Out][L01]

2. <span data-ttu-id="5dfad-149">Hola **Azure Sign Out** ventana de confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![ventana Hello Azure Sign Out confirmación][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="5dfad-151">Inicie sesión en tooyour cuenta de Azure automáticamente mediante un archivo de credenciales existente</span><span class="sxs-lookup"><span data-stu-id="5dfad-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="5dfad-152">Si cierre la sesión de su cuenta de Azure cuando se utiliza la IDEA de IntelliJ, debe utilizar un inicio de sesión de tooautomatically de archivo de credenciales existente en toohello cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dfad-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="5dfad-153">Hola tooconfigure Kit de herramientas de Azure para Eclipse toouse un archivo de credenciales existente, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5dfad-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="5dfad-154">Abra el proyecto con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfad-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="5dfad-155">En hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![comando de inicio de sesión en Azure IntelliJ Hola][A01]

3. <span data-ttu-id="5dfad-157">Hola **inicio de sesión en Azure** ventana, seleccione **automatizada**y, a continuación, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A02]

4. <span data-ttu-id="5dfad-159">Hola **Seleccionar archivo de autenticación** cuadro de diálogo, seleccione un archivo de credenciales creado anteriormente y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![cuadro de diálogo Seleccionar archivo de autenticación de Hola][A08]

5. <span data-ttu-id="5dfad-161">Hola **inicio de sesión en Azure** ventana, haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A06]

6. <span data-ttu-id="5dfad-163">Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5dfad-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![cuadro de diálogo Seleccionar suscripciones Hola][A07]

## <a name="next-steps"></a><span data-ttu-id="5dfad-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5dfad-165">Next steps</span></span>
<span data-ttu-id="5dfad-166">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="5dfad-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="5dfad-167">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5dfad-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5dfad-168">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5dfad-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5dfad-169">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5dfad-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5dfad-170">[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5dfad-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5dfad-171">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5dfad-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="5dfad-172">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5dfad-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5dfad-173">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5dfad-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5dfad-174">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5dfad-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5dfad-175">*Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ* (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="5dfad-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="5dfad-176">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5dfad-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="5dfad-177">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5dfad-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

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
