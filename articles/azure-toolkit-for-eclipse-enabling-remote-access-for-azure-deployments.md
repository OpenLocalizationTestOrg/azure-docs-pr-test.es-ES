---
title: aaaEnabling acceso remoto para las implementaciones de Azure en Eclipse
description: "Obtenga información acerca de cómo tener acceso tooenable remoto para las implementaciones de Azure mediante Hola Kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="ff41c-103">Habilitación del acceso remoto para implementaciones de Azure en Eclipse</span><span class="sxs-lookup"><span data-stu-id="ff41c-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="ff41c-104">toohelp solucionar problemas de las implementaciones, puede habilitar y usar acceso remoto tooconnect toohello virtual machine hospeda la implementación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="ff41c-105">Hola funcionalidad de acceso remoto se basa en hello protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="ff41c-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="ff41c-106">Puede configurar el acceso remoto para la implementación después de que haya publicado tooAzure, o si está usando Eclipse con un sistema operativo Windows, puede configurar el acceso remoto antes de publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ff41c-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="ff41c-107">Tenga en cuenta que necesitará a un cliente de escritorio remoto que sea compatible con el sistema operativo en la máquina virtual de orden tooconnect tooyour de la implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff41c-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="ff41c-108">Cómo tooenable acceso remoto antes de implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="ff41c-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="ff41c-109">tooenable acceso remoto antes de implementar su aplicación tooAzure, deberá toobe ejecutarse Eclipse en Windows.</span><span class="sxs-lookup"><span data-stu-id="ff41c-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="ff41c-110">Hello siguiente imagen muestra hello **acceso remoto** cuadro de diálogo de propiedades utiliza tooenable el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="ff41c-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="ff41c-111">Hay dos Hola de toodisplay maneras **acceso remoto** cuadro de diálogo de propiedades:</span><span class="sxs-lookup"><span data-stu-id="ff41c-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="ff41c-112">Haga clic en hello **avanzadas** vínculo Hola **acceso remoto** sección de hello **publicar tooAzure** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff41c-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="ff41c-113">Abra hello **propiedades** cuadro de diálogo de su proyecto de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff41c-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="ff41c-114">Cuando crea un nuevo proyecto de implementación de Azure, el proyecto de hello no tendrá acceso remoto habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ff41c-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="ff41c-115">Sin embargo, puede habilitar fácilmente acceso remoto mediante la especificación de nombre de usuario de hello y una contraseña en hello **publicar tooAzure** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff41c-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="ff41c-116">contraseña de acceso remoto de Hola se cifra mediante certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="ff41c-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="ff41c-117">Si no usa proporcionar su propio certificado, cifrado de Hola se basa en un certificado autofirmado acompaña Hola complemento de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ff41c-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="ff41c-118">Este certificado autofirmado está en hello **cert** carpeta de su proyecto de Azure, almacenado como un archivo de certificado público (SampleRemoteAccessPublic.cer) y archivo de certificado como un intercambio de información Personal (PFX) () SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="ff41c-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="ff41c-119">Hola esta última contiene la clave privada de hello certificado de Hola y tiene una contraseña predeterminada, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="ff41c-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="ff41c-120">Sin embargo, puesto que esta contraseña es de dominio público, certificado predeterminado de hello debe usarse solo para el aprendizaje, no para una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="ff41c-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="ff41c-121">Tan distinto con fines de aprendizaje, cuando desee que las sesiones remotas de tooenabled para las implementaciones, se debe hacer clic en hello **avanzadas** vínculo Hola **publicar tooAzure** diálogo toospecify su propio certificado.</span><span class="sxs-lookup"><span data-stu-id="ff41c-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="ff41c-122">Tenga en cuenta que necesitará versión PFX de hello tooupload del servicio de tooyour hospedado de certificado de hello en hello Portal de administración de Azure, por lo que Azure pueda descifrar la contraseña de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff41c-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="ff41c-123">resto de Hola de tutorial de hello muestra cómo tener acceso tooenable remoto para un proyecto de implementación de Azure que se creó inicialmente con acceso remoto deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="ff41c-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="ff41c-124">Para los fines de este tutorial, vamos a crear un certificado autofirmado y su archivo .pfx tendrá una contraseña de su elección.</span><span class="sxs-lookup"><span data-stu-id="ff41c-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="ff41c-125">También tiene opción de hello del uso de un certificado emitido por una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="ff41c-126">¿Cómo tooenable acceso remoto después de haya implementado tooAzure</span><span class="sxs-lookup"><span data-stu-id="ff41c-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="ff41c-127">tooenable acceso remoto después de haber implementado tooAzure, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="ff41c-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="ff41c-128">Inicie sesión en el portal de administración de Azure de hello con su cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="ff41c-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="ff41c-129">En la lista de **Servicios en la nube**, seleccione el servicio en la nube que se implementó</span><span class="sxs-lookup"><span data-stu-id="ff41c-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="ff41c-130">En la página web del servicio en la nube hello, haga clic en hello **configurar** vínculo</span><span class="sxs-lookup"><span data-stu-id="ff41c-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="ff41c-131">En hello parte inferior de la página de configuración de hello, haga clic en hello **remoto** vínculo</span><span class="sxs-lookup"><span data-stu-id="ff41c-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="ff41c-132">Cuando aparezca el cuadro de diálogo emergente de hello:</span><span class="sxs-lookup"><span data-stu-id="ff41c-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="ff41c-133">Especificar Hola rol, que se desea acceso remoto tooenable</span><span class="sxs-lookup"><span data-stu-id="ff41c-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="ff41c-134">Haga clic en hello tooselect **habilitar Escritorio remoto** casilla de verificación</span><span class="sxs-lookup"><span data-stu-id="ff41c-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="ff41c-135">Especifique un nombre de usuario y una contraseña que desee toouse para acceso remoto</span><span class="sxs-lookup"><span data-stu-id="ff41c-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="ff41c-136">Seleccione Hola certificado toouse</span><span class="sxs-lookup"><span data-stu-id="ff41c-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="ff41c-137">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="ff41c-137">Click **OK**</span></span> 

<span data-ttu-id="ff41c-138">Verá un mensaje que indica que el cambio de configuración está en curso, lo que puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="ff41c-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="ff41c-139">Cuando haya finalizado el cambio de configuración de hello, siga los pasos de Hola Hola **toolog de forma remota** sección más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ff41c-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="ff41c-140">El proceso tooenable de acceso remoto en el paquete</span><span class="sxs-lookup"><span data-stu-id="ff41c-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="ff41c-141">En el panel del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto y haga clic en **Properties**(Propiedades).</span><span class="sxs-lookup"><span data-stu-id="ff41c-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="ff41c-142">Hola **propiedades** cuadro de diálogo, expanda **Azure** en el panel izquierdo de Hola y haga clic en **acceso remoto**.</span><span class="sxs-lookup"><span data-stu-id="ff41c-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="ff41c-143">Hola **acceso remoto** cuadro de diálogo, asegúrese de **habilitar todos los roles tooaccept conexiones a Escritorio remoto con estas credenciales de inicio de sesión** está activada.</span><span class="sxs-lookup"><span data-stu-id="ff41c-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="ff41c-144">Especifique un nombre de usuario para hello conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ff41c-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="ff41c-145">Especifique y confirme la contraseña de hello para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff41c-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="ff41c-146">valores de nombre y la contraseña de la usuario de Hello establecidos en este cuadro de diálogo se utilizará al realizar una conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ff41c-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="ff41c-147">(Tenga en cuenta que se trata de una contraseña independiente de su contraseña PFX).</span><span class="sxs-lookup"><span data-stu-id="ff41c-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="ff41c-148">Especifique la fecha de expiración de hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff41c-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="ff41c-149">Haga clic en **New** toocreate un nuevo certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="ff41c-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="ff41c-150">(Como alternativa, puede seleccionar un certificado desde el área de trabajo o sistema de archivos a través de hello **área de trabajo** o **FileSystem** botones, respectivamente, pero para los fines de este tutorial vamos a crear un nuevo certificado.)</span><span class="sxs-lookup"><span data-stu-id="ff41c-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="ff41c-151">Hola **nuevo certificado** cuadro de diálogo, especifique y confirme la contraseña de Hola que usará para el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="ff41c-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="ff41c-152">Acepte el valor Hola proporcionado para **nombre (CN)**, o usar un nombre personalizado.</span><span class="sxs-lookup"><span data-stu-id="ff41c-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="ff41c-153">Especifique Hola ruta de acceso y nombre de archivo donde se guardará el nuevo certificado de hello, en formato .cer.</span><span class="sxs-lookup"><span data-stu-id="ff41c-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="ff41c-154">En este paso y el paso siguiente de hello, podría utilizar hello **cert** carpeta de su proyecto de Azure, pero está libre toochoose otra ubicación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="ff41c-155">Para los fines de este tutorial, usaremos **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="ff41c-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="ff41c-156">(Crear hello **c:\mycert** tooproceeding anteriores de carpeta, o utilice una carpeta existente si lo desea.)</span><span class="sxs-lookup"><span data-stu-id="ff41c-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="ff41c-157">Especifique Hola ruta de acceso y nombre de archivo donde se guardará un nuevo certificado hello y su clave privada, en formato .pfx.</span><span class="sxs-lookup"><span data-stu-id="ff41c-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="ff41c-158">Para los fines de este tutorial, usaremos **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="ff41c-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="ff41c-159">Su **nuevo certificado** diálogo debe tener un aspecto similar siguiente toohello (actualizar las rutas de acceso de carpeta de hello si no usó **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="ff41c-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="ff41c-160">Haga clic en **Aceptar** tooclose hello **nuevo certificado** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff41c-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="ff41c-161">Su **acceso remoto** cuadro de diálogo debe tener un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="ff41c-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="ff41c-162">Haga clic en **Aceptar** tooclose hello **acceso remoto** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff41c-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="ff41c-163">Recompilar la aplicación, con hello generar el conjunto de toocloud de implementación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="ff41c-164">toolog de forma remota</span><span class="sxs-lookup"><span data-stu-id="ff41c-164">toolog in remotely</span></span>
<span data-ttu-id="ff41c-165">Una vez que la instancia de rol está lista, puede registrar de forma remota en la máquina virtual de toohello que hospeda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="ff41c-166">Si está usando Eclipse en Windows y Hola seleccionado se **iniciar escritorio remoto en implementar** opción durante la tooAzure de implementación, aparecerá una pantalla de inicio de sesión de conexión a Escritorio remoto cuando se inicia la implementación.</span><span class="sxs-lookup"><span data-stu-id="ff41c-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="ff41c-167">Cuando se le pida Hola nombre de usuario y contraseña, escriba los valores de hello que especificó para el usuario remoto hello y será capaz de toolog en.</span><span class="sxs-lookup"><span data-stu-id="ff41c-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="ff41c-168">Toolog de otra manera de forma remota es a través de hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de administración de Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="ff41c-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="ff41c-169">Dentro de hello **servicios en la nube** vista de hello portal de administración de Azure, haga clic en el servicio de nube, haga clic en **instancias**, haga clic en una instancia específica y, a continuación, haga clic en hello **conectar**botón.</span><span class="sxs-lookup"><span data-stu-id="ff41c-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="ff41c-170">Hola **conectar** botón se muestra como siguiente de hello en la barra de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="ff41c-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="ff41c-171">Tras hacer clic en hello **conectar** botón, podrá tooopen solicitada un archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="ff41c-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="ff41c-172">Abra el archivo hello y siga las indicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff41c-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="ff41c-173">(Podría guardar este equipo local tooyour de archivo y, a continuación, ejecutar archivo hello haciendo doble clic en él tooremote registro en tooyour máquina virtual sin necesidad de toofirst vaya portal de administración de Hola.)</span><span class="sxs-lookup"><span data-stu-id="ff41c-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="ff41c-174">Cuando se le pida Hola nombre de usuario y contraseña, escriba los valores de hello que especificó para el usuario remoto hello y será capaz de toolog en.</span><span class="sxs-lookup"><span data-stu-id="ff41c-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="ff41c-175">Si se encuentra en un sistema operativo, es necesario toouse un cliente de escritorio remoto que sea compatible con el sistema operativo y siga Hola pasos tooconfigure que el cliente con la configuración de hello en el archivo RDP de Hola que ha descargado.</span><span class="sxs-lookup"><span data-stu-id="ff41c-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="ff41c-176">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ff41c-176">See Also</span></span>
<span data-ttu-id="ff41c-177">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ff41c-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="ff41c-178">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ff41c-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="ff41c-179">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ff41c-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="ff41c-180">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="ff41c-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
