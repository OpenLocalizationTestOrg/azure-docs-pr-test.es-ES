---
title: "Habilitación del acceso remoto para implementaciones de Azure en Eclipse"
description: "Obtenga información sobre cómo habilitar el acceso remoto para las implementaciones de Azure mediante el kit de herramientas de Azure para Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="ec185-103">Habilitación del acceso remoto para implementaciones de Azure en Eclipse</span><span class="sxs-lookup"><span data-stu-id="ec185-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="ec185-104">Para facilitar la solución de problemas de las implementaciones, puede habilitar y usar el acceso remoto para conectarse a la máquina virtual que hospeda la implementación.</span><span class="sxs-lookup"><span data-stu-id="ec185-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="ec185-105">La funcionalidad de acceso remoto se basa en el protocolo de Escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="ec185-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="ec185-106">Puede configurar el acceso remoto para la implementación después de publicarlo en Azure, o bien, si usa Eclipse con un sistema operativo Windows, puede configurar el acceso remoto antes de publicar en Azure.</span><span class="sxs-lookup"><span data-stu-id="ec185-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="ec185-107">Tenga en cuenta que necesitará a un cliente de Escritorio remoto que sea compatible con el sistema operativo para conectarse a la máquina virtual de su implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="ec185-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="ec185-108">Habilitación del acceso remoto antes de implementar en Azure</span><span class="sxs-lookup"><span data-stu-id="ec185-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="ec185-109">Para habilitar el acceso remoto antes de implementar la aplicación en Azure, tiene que ejecutarse Eclipse en Windows.</span><span class="sxs-lookup"><span data-stu-id="ec185-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="ec185-110">La imagen siguiente muestra el cuadro de diálogo de propiedades **Remote Access** (Acceso remoto) que se usa para habilitar el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="ec185-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="ec185-111">Hay dos maneras de mostrar el cuadro de diálogo de propiedades **Remote Access** :</span><span class="sxs-lookup"><span data-stu-id="ec185-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="ec185-112">Haga clic en el vínculo **Advanced** (Propiedades avanzadas) en la sección **Remote Access** (Acceso remoto) del cuadro de diálogo **Publish to Azure** (Publicar en Azure).</span><span class="sxs-lookup"><span data-stu-id="ec185-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="ec185-113">Abra el cuadro de diálogo **Properties** (Propiedades) del proyecto de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec185-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="ec185-114">Cuando cree un proyecto de implementación de Azure, el proyecto no tendrá el acceso remoto habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ec185-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="ec185-115">Pero, puede habilitar fácilmente el acceso remoto especificando el nombre de usuario y la contraseña en el cuadro de diálogo **Publish to Azure** .</span><span class="sxs-lookup"><span data-stu-id="ec185-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="ec185-116">La contraseña de acceso remoto se cifra mediante certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="ec185-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="ec185-117">Si no especifica su propio certificado, el cifrado se basa en un certificado autofirmado que se suministra con el complemento de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ec185-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="ec185-118">Este certificado autofirmado se encuentra en la carpeta **cert** del proyecto de Azure, almacenado como archivo de certificado público (SampleRemoteAccessPublic.cer) y como archivo de certificado de intercambio de información personal (PFX) (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="ec185-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="ec185-119">El segundo contiene la clave privada para el certificado y tiene una contraseña de forma predeterminada, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="ec185-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="ec185-120">Pero, puesto que esta contraseña es de dominio público, el certificado predeterminado solo debe usarse con fines de aprendizaje, no para una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="ec185-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="ec185-121">Así pues, si sus fines no son de aprendizaje, cuando quiera habilitar sesiones remotas para sus implementaciones, debe hacer clic en el vínculo **Advanced** (Propiedades avanzadas) del cuadro de diálogo **Publish to Azure** (Publicar en Azure) para especificar su propio certificado.</span><span class="sxs-lookup"><span data-stu-id="ec185-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="ec185-122">Tenga en cuenta que tendrá que cargar la versión PFX del certificado en el servicio hospedado dentro del Portal de administración de Azure, para que Azure pueda descifrar la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="ec185-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="ec185-123">El resto del tutorial muestra cómo habilitar el acceso remoto para un proyecto de implementación de Azure que se creó inicialmente con el acceso remoto deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="ec185-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="ec185-124">Para los fines de este tutorial, vamos a crear un certificado autofirmado y su archivo .pfx tendrá una contraseña de su elección.</span><span class="sxs-lookup"><span data-stu-id="ec185-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="ec185-125">También tiene la opción de usar un certificado emitido por una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="ec185-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="ec185-126">Habilitación del acceso remoto después de haber implementado en Azure</span><span class="sxs-lookup"><span data-stu-id="ec185-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="ec185-127">Para habilitar el acceso remoto después de haber implementado en Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ec185-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="ec185-128">Inicie sesión en el Portal de administración de Azure con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec185-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="ec185-129">En la lista de **Servicios en la nube**, seleccione el servicio en la nube que se implementó</span><span class="sxs-lookup"><span data-stu-id="ec185-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="ec185-130">En la página web del servicio en la nube, haga clic en el vínculo **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="ec185-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="ec185-131">En la parte inferior de la página de configuración, haga clic en el vínculo **Remoto** .</span><span class="sxs-lookup"><span data-stu-id="ec185-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="ec185-132">Cuando aparezca el cuadro de diálogo emergente:</span><span class="sxs-lookup"><span data-stu-id="ec185-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="ec185-133">Especifique el rol para el que desea habilitar el acceso remoto</span><span class="sxs-lookup"><span data-stu-id="ec185-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="ec185-134">Haga clic en la casilla **Habilitar Escritorio remoto** para seleccionarla.</span><span class="sxs-lookup"><span data-stu-id="ec185-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="ec185-135">Especifique un nombre de usuario y la contraseña que quiere usar apara el acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="ec185-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="ec185-136">Seleccione el certificado que va a usar.</span><span class="sxs-lookup"><span data-stu-id="ec185-136">Select the certificate to use</span></span>

6. <span data-ttu-id="ec185-137">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="ec185-137">Click **OK**</span></span> 

<span data-ttu-id="ec185-138">Verá un mensaje que indica que el cambio de configuración está en curso, lo cual puede tardar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="ec185-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="ec185-139">Cuando el cambio en la configuración se haya completado, siga los pasos de la sección **Para iniciar sesión de manera remota** más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ec185-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="ec185-140">Habilitación del acceso remoto en el paquete</span><span class="sxs-lookup"><span data-stu-id="ec185-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="ec185-141">En el panel del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto y haga clic en **Properties**(Propiedades).</span><span class="sxs-lookup"><span data-stu-id="ec185-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="ec185-142">En el cuadro de diálogo **Properties** (Propiedades), expanda **Azure** en el panel izquierdo y haga clic en **Remote Access** (Acceso remoto).</span><span class="sxs-lookup"><span data-stu-id="ec185-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="ec185-143">En el cuadro de diálogo **Remote Access** (Acceso remoto), asegúrese de que la opción **Enable all roles to accept Remote Desktop Connections with these login credentials** (Habilitar todos los roles para aceptar las conexiones a Escritorio remoto con estas credenciales de inicio de sesión) está activada.</span><span class="sxs-lookup"><span data-stu-id="ec185-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="ec185-144">Especifique un nombre de usuario para la conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ec185-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="ec185-145">Especifique y confirme la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="ec185-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="ec185-146">Los valores de nombre de usuario y contraseña de usuario establecidos en este cuadro de diálogo se utilizarán al realizar una conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="ec185-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="ec185-147">(Tenga en cuenta que se trata de una contraseña independiente de su contraseña PFX).</span><span class="sxs-lookup"><span data-stu-id="ec185-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="ec185-148">Especifique la fecha de caducidad para la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="ec185-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="ec185-149">Haga clic en **New** (Nuevo) para crear un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="ec185-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="ec185-150">(Como alternativa, puede seleccionar un certificado desde el área de trabajo o el sistema de archivos mediante los botones **Workspace** (Área de trabajo) o **FileSystem** (Sistema de archivos), respectivamente, pero para fines de este tutorial vamos a crear un certificado).</span><span class="sxs-lookup"><span data-stu-id="ec185-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="ec185-151">En el cuadro de diálogo **New Certificate** (Nuevo certificado), especifique y confirme la contraseña que utilizará para el archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="ec185-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="ec185-152">Acepte el valor proporcionado para **Name (CN)**(Nombre (CN)) o use un nombre personalizado.</span><span class="sxs-lookup"><span data-stu-id="ec185-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="ec185-153">Especifique la ruta de acceso y el nombre de archivo donde se guardará el nuevo certificado en formato .cer.</span><span class="sxs-lookup"><span data-stu-id="ec185-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="ec185-154">Para este paso y el siguiente, puede usar la carpeta **cert** de su proyecto de Azure, pero tiene la posibilidad de elegir otra ubicación.</span><span class="sxs-lookup"><span data-stu-id="ec185-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="ec185-155">Para los fines de este tutorial, usaremos **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="ec185-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="ec185-156">(Cree la carpeta **c:\mycert** antes de continuar, o utilice una carpeta existente si lo desea).</span><span class="sxs-lookup"><span data-stu-id="ec185-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="ec185-157">Especifique la ruta de acceso y el nombre de archivo donde se guardará el nuevo certificado y su clave privada en formato .pfx.</span><span class="sxs-lookup"><span data-stu-id="ec185-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="ec185-158">Para los fines de este tutorial, usaremos **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="ec185-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="ec185-159">El cuadro de diálogo **New Certificate** (Nuevo certificado) debe ser similar al siguiente (actualice las rutas de acceso de la carpeta si no utilizó **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="ec185-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="ec185-160">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo **New Certificate** (Nuevo certificado).</span><span class="sxs-lookup"><span data-stu-id="ec185-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="ec185-161">El cuadro de diálogo **Remote Access** (Acceso remoto) debería ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec185-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="ec185-162">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo **Remote Access** (Acceso remoto).</span><span class="sxs-lookup"><span data-stu-id="ec185-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="ec185-163">Recompile la aplicación, con la compilación establecida para su implementación en la nube.</span><span class="sxs-lookup"><span data-stu-id="ec185-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="ec185-164">Para iniciar sesión de manera remota</span><span class="sxs-lookup"><span data-stu-id="ec185-164">To log in remotely</span></span>
<span data-ttu-id="ec185-165">Cuando la instancia de rol esté lista, podrá iniciar sesión de manera remota en la máquina virtual que hospeda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec185-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="ec185-166">Si usa Eclipse en Windows y ha seleccionado la opción **Start remote desktop on deploy** (Iniciar escritorio remoto al implementar) durante la implementación en Azure, se abrirá una pantalla de inicio de sesión de conexión a Escritorio remoto cuando se inicie la implementación.</span><span class="sxs-lookup"><span data-stu-id="ec185-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="ec185-167">Cuando se le pida el nombre de usuario y la contraseña, escriba los valores que especificó para el usuario remoto y podrá iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ec185-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="ec185-168">Otra manera de iniciar sesión de manera remota es a través del <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de administración de Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="ec185-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="ec185-169">Dentro de la vista **Cloud Services** del Portal de administración de Azure, haga clic en el servicio en la nube, en **Instancias**, en una instancia específica y luego en el botón**Conectar**.</span><span class="sxs-lookup"><span data-stu-id="ec185-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="ec185-170">El botón **Conectar** aparece del modo siguiente en la barra de comandos:</span><span class="sxs-lookup"><span data-stu-id="ec185-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="ec185-171">Tras hacer clic en el botón **Conectar** , se le pedirá que abra un archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="ec185-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="ec185-172">Abra el archivo y siga las indicaciones.</span><span class="sxs-lookup"><span data-stu-id="ec185-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="ec185-173">(También puede guardar este archivo en el equipo local y luego ejecutarlo haciendo doble clic en él para iniciar sesión de manera remota en la máquina virtual sin necesidad de ir primero al Portal de administración).</span><span class="sxs-lookup"><span data-stu-id="ec185-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="ec185-174">Cuando se le pida el nombre de usuario y la contraseña, escriba los valores que especificó para el usuario remoto y podrá iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ec185-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="ec185-175">Si se encuentra en un sistema operativo distinto de Windows, deberá usar un cliente de Escritorio remoto que sea compatible con el sistema operativo y seguir los pasos para configurar ese cliente con los valores del archivo RDP que descargó.</span><span class="sxs-lookup"><span data-stu-id="ec185-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="ec185-176">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ec185-176">See Also</span></span>
<span data-ttu-id="ec185-177">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec185-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="ec185-178">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec185-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="ec185-179">[Instalación del Kit de herramientas de Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec185-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="ec185-180">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="ec185-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
