---
title: aaaSign en instrucciones de hello Azure Toolkit for Eclipse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosign en Microsoft Azure mediante el uso de hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="b4f67-103">Azure inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="b4f67-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b4f67-104">Hello Azure Toolkit for Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4f67-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="b4f67-105">**Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f67-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="b4f67-106">**Automatizada** : cuando se usa este método, se creará un archivo de credenciales que contiene los datos de entidad de seguridad de servicio, después del cual puede usar el inicio de sesión de hello credenciales archivo tooautomatically en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f67-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="b4f67-107">Hello en hello las secciones siguientes se explica cómo toouse cada método.</span><span class="sxs-lookup"><span data-stu-id="b4f67-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="b4f67-108">Inicio de sesión en la cuenta de Azure de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="b4f67-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="b4f67-109">Hello pasos siguientes se ilustran cómo toosign en Azure bien especificando sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f67-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="b4f67-110">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b4f67-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="b4f67-111">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. <span data-ttu-id="b4f67-113">Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **Interactive**y, a continuación, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][I02]

1. <span data-ttu-id="b4f67-115">Cuando Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. <span data-ttu-id="b4f67-117">Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="b4f67-119">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva</span><span class="sxs-lookup"><span data-stu-id="b4f67-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="b4f67-120">Después de haber configurado los pasos de hello en la sección anterior de hello, aparecerá automáticamente la sesión de su cuenta de Azure cada vez que inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b4f67-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="b4f67-121">Sin embargo, si desea toosign fuera de su cuenta de Azure sin necesidad de reiniciar Eclipse, utilice Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="b4f67-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="b4f67-122">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="b4f67-124">Cuando Hola **Azure Sign Out** aparece el cuadro de diálogo, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="b4f67-126">Inicie sesión en su cuenta de Azure de forma automática y la creación de credenciales de un archivo toouse Hola futuras</span><span class="sxs-lookup"><span data-stu-id="b4f67-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="b4f67-127">Hello siguientes pasos le guiarán por la creación de un archivo de credenciales que contiene los datos de entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b4f67-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="b4f67-128">Una vez haya completado estos pasos, will Eclipse automáticamente uso Hola credenciales archivo tooautomatically inicio de sesión que en Azure cada vez que abra el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b4f67-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="b4f67-129">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b4f67-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="b4f67-130">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="b4f67-132">Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **automatizada**y, a continuación, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="b4f67-134">Cuando Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. <span data-ttu-id="b4f67-136">Cuando Hola **crear archivos de autenticación** aparece en el cuadro de diálogo, las suscripciones que desee toouse, elija el directorio de destino y, a continuación, haga clic en hello seleccione **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. <span data-ttu-id="b4f67-138">Hola **estado de creación de entidad de servicio** se mostrará el cuadro de diálogo y después de que los archivos se han creado correctamente, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. <span data-ttu-id="b4f67-140">Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="b4f67-142">Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="b4f67-144">Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática</span><span class="sxs-lookup"><span data-stu-id="b4f67-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="b4f67-145">Después de haber configurado los pasos de hello en la sección anterior de hello, hello Azure Toolkit iniciará sesión automáticamente en su cuenta de Azure cada vez que inicie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b4f67-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="b4f67-146">Sin embargo, toosign fuera de su cuenta de Azure e impiden que hello Azure Toolkit iniciar sesión automáticamente, un uso Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="b4f67-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="b4f67-147">En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. <span data-ttu-id="b4f67-149">Cuando Hola **Azure Sign Out** aparece el cuadro de diálogo, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="b4f67-151">Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente</span><span class="sxs-lookup"><span data-stu-id="b4f67-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="b4f67-152">Si cierre la sesión de Azure en Eclipse, necesitará tooreconfigure Hola Kit de herramientas de Azure para Eclipse toouse un archivo de credenciales que ha creado antes de poder firmar automáticamente en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f67-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="b4f67-153">Hello pasos siguientes le guiará por configurar hello Azure Toolkit toouse un archivo de credenciales existente.</span><span class="sxs-lookup"><span data-stu-id="b4f67-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="b4f67-154">Abra el proyecto con Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b4f67-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="b4f67-155">Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. <span data-ttu-id="b4f67-157">Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **automatizada**y, a continuación, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A02]

1. <span data-ttu-id="b4f67-159">Cuando Hola **Seleccionar archivo autenticado** aparece el cuadro de diálogo, seleccione un archivo de credenciales que creó anteriormente y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Cuadro de diálogo Iniciar sesión][A08]

1. <span data-ttu-id="b4f67-161">Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. <span data-ttu-id="b4f67-163">Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4f67-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="see-also"></a><span data-ttu-id="b4f67-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b4f67-165">See Also</span></span>
<span data-ttu-id="b4f67-166">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="b4f67-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="b4f67-167">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4f67-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b4f67-168">[What's New en hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4f67-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b4f67-169">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4f67-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b4f67-170">*Inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse (de este artículo)*</span><span class="sxs-lookup"><span data-stu-id="b4f67-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="b4f67-171">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4f67-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="b4f67-172">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b4f67-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b4f67-173">[What's New en hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b4f67-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b4f67-174">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b4f67-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b4f67-175">[Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b4f67-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b4f67-176">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b4f67-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="b4f67-177">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b4f67-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's New en hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

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
