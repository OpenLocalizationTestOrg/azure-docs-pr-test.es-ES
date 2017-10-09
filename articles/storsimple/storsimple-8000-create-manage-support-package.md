---
title: paquete de soporte de aaaCreate un StorSimple 8000 series | Documentos de Microsoft
description: "Obtenga información acerca de cómo descifrar toocreate y editar un paquete de soporte para el dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="b31a5-103">Crear y administrar un paquete de soporte para la serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="b31a5-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="b31a5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b31a5-104">Overview</span></span>

<span data-ttu-id="b31a5-105">Un paquete de soporte técnico de StorSimple es un mecanismo fácil de usar que recopila todos los registros pertinentes tooassist Microsoft Support a solucionar los problemas del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b31a5-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="b31a5-106">Hello registros recopilados están cifrados y comprimidos.</span><span class="sxs-lookup"><span data-stu-id="b31a5-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="b31a5-107">Este tutorial incluye instrucciones paso a paso toocreate y administrar el paquete de soporte de hello para el dispositivo de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="b31a5-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="b31a5-108">Si está trabajando con una matriz Virtual de StorSimple, vaya demasiado[generar un paquete de registros](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="b31a5-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="b31a5-109">Crear un paquete de soporte</span><span class="sxs-lookup"><span data-stu-id="b31a5-109">Create a support package</span></span>

<span data-ttu-id="b31a5-110">En algunos casos, necesitará toomanually crear paquete de soporte de Hola a través de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b31a5-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b31a5-111">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31a5-111">For example:</span></span>

* <span data-ttu-id="b31a5-112">Si necesita información confidencial de tooremove desde el registro de los archivos anterior toosharing con Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="b31a5-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="b31a5-113">Si tiene dificultades para cargar el paquete Hola debido a problemas de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="b31a5-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="b31a5-114">Puede compartir su paquete de soporte generado manualmente con el servicio de soporte técnico de Microsoft mediante el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b31a5-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="b31a5-115">Realizar Hola siguiendo los pasos toocreate un paquete de soporte de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b31a5-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b31a5-116">toocreate un paquete de soporte de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b31a5-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b31a5-117">toostart una sesión de Windows PowerShell como administrador en el equipo remoto de Hola que ha utilizado el dispositivo de StorSimple de tooconnect tooyour, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b31a5-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="b31a5-118">En la sesión de Windows PowerShell de hello, conectar toohello consola SSAdmin del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b31a5-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="b31a5-119">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="b31a5-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="b31a5-120">En el cuadro de diálogo de Hola que se abre, escriba la contraseña de administrador del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b31a5-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="b31a5-121">es la contraseña predeterminada de Hello _Password1_.</span><span class="sxs-lookup"><span data-stu-id="b31a5-121">hello default password is _Password1_.</span></span>
     
      ![Cuadro de diálogo de credenciales de PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="b31a5-123">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b31a5-123">Select **OK**.</span></span>
   4. <span data-ttu-id="b31a5-124">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="b31a5-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="b31a5-125">En la sesión de Hola que se abre, escriba comando adecuado Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="b31a5-126">Para los recursos compartidos de red que están protegidos por contraseña, escriba:</span><span class="sxs-lookup"><span data-stu-id="b31a5-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="b31a5-127">Se le pedirá una contraseña, una carpeta compartida de la red de toohello ruta de acceso y una frase de contraseña (porque se cifra el paquete de soporte de hello).</span><span class="sxs-lookup"><span data-stu-id="b31a5-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="b31a5-128">A continuación, se crea un paquete de soporte en la carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="b31a5-129">Para los recursos compartidos que no están protegidas por contraseña, no es necesario hello `-Credential` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b31a5-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="b31a5-130">Escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31a5-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="b31a5-131">se creará el paquete de soporte técnico de Hola para ambos controladores en la carpeta compartida de red especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="b31a5-132">Es un archivo comprimido cifrado que puede enviarse tooMicrosoft soporte técnico para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="b31a5-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="b31a5-133">Para obtener más información, consulte [Ponerse en contacto con el soporte técnico de Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b31a5-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="b31a5-134">Hola parámetros del cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="b31a5-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="b31a5-135">Puede usar Hola parámetros con el cmdlet Export-HcsSupportPackage Hola siguientes.</span><span class="sxs-lookup"><span data-stu-id="b31a5-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="b31a5-136">Parámetro</span><span class="sxs-lookup"><span data-stu-id="b31a5-136">Parameter</span></span> | <span data-ttu-id="b31a5-137">Obligatorio/opcional</span><span class="sxs-lookup"><span data-stu-id="b31a5-137">Required/Optional</span></span> | <span data-ttu-id="b31a5-138">Description</span><span class="sxs-lookup"><span data-stu-id="b31a5-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="b31a5-139">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b31a5-139">Required</span></span> |<span data-ttu-id="b31a5-140">Utilice tooprovide Hola ubicación de carpeta compartida en la red de hello en qué Hola se coloca el paquete de soporte.</span><span class="sxs-lookup"><span data-stu-id="b31a5-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="b31a5-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b31a5-141">Required</span></span> |<span data-ttu-id="b31a5-142">Use tooprovide una frase de contraseña toohelp cifrar paquete de soporte de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="b31a5-143">Opcional</span><span class="sxs-lookup"><span data-stu-id="b31a5-143">Optional</span></span> |<span data-ttu-id="b31a5-144">Usar credenciales de acceso de toosupply Hola carpeta compartida de red.</span><span class="sxs-lookup"><span data-stu-id="b31a5-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="b31a5-145">Opcional</span><span class="sxs-lookup"><span data-stu-id="b31a5-145">Optional</span></span> |<span data-ttu-id="b31a5-146">Paso de confirmación de la frase de contraseña de cifrado de hello con uso tooskip.</span><span class="sxs-lookup"><span data-stu-id="b31a5-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="b31a5-147">Opcional</span><span class="sxs-lookup"><span data-stu-id="b31a5-147">Optional</span></span> |<span data-ttu-id="b31a5-148">Usar toospecify en un directorio *ruta de acceso* en qué soporte Hola se coloca el paquete.</span><span class="sxs-lookup"><span data-stu-id="b31a5-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="b31a5-149">valor predeterminado de Hello es [nombre de dispositivo]-[fecha y hora actuales:aaaa-mm-dd-hh-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="b31a5-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="b31a5-150">Opcional</span><span class="sxs-lookup"><span data-stu-id="b31a5-150">Optional</span></span> |<span data-ttu-id="b31a5-151">Especificar como **clúster** toocreate (valor predeterminado) un paquete de soporte para ambos controladores.</span><span class="sxs-lookup"><span data-stu-id="b31a5-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="b31a5-152">Si desea toocreate un paquete solo para el controlador actual de hello, especifique **controlador**.</span><span class="sxs-lookup"><span data-stu-id="b31a5-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="b31a5-153">Editar un paquete de soporte</span><span class="sxs-lookup"><span data-stu-id="b31a5-153">Edit a support package</span></span>

<span data-ttu-id="b31a5-154">Una vez que haya generado un paquete de soporte, deberá información confidencial de tooedit Hola paquete tooremove.</span><span class="sxs-lookup"><span data-stu-id="b31a5-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="b31a5-155">Esto puede incluir nombres de volúmenes, direcciones IP de dispositivos y nombres de copia de seguridad de archivos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="b31a5-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b31a5-156">Solo pueden editarse los paquetes de soporte generados a través de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b31a5-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b31a5-157">No se puede editar un paquete creado en hello portal de Azure con el servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b31a5-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="b31a5-158">tooedit un paquete de soporte antes de cargarlo en el sitio de Microsoft Support hello, descifrar primero el paquete de soporte de hello, editar archivos de hello y, a continuación, volver a cifrarlos.</span><span class="sxs-lookup"><span data-stu-id="b31a5-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="b31a5-159">Realizar pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b31a5-160">tooedit un paquete de soporte de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b31a5-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b31a5-161">Generar un paquete de soporte técnico como se ha descrito anteriormente, en [toocreate un paquete de soporte de Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b31a5-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="b31a5-162">[Descargar el script de Hola](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente en el cliente.</span><span class="sxs-lookup"><span data-stu-id="b31a5-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="b31a5-163">Importe el módulo de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="b31a5-164">Especifique la carpeta local Hola ruta de acceso toohello en la que descargó el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="b31a5-165">módulo de hello tooimport, escriba:</span><span class="sxs-lookup"><span data-stu-id="b31a5-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="b31a5-166">Todos los archivos de hello están *.aes* archivos que están comprimidos y cifrados.</span><span class="sxs-lookup"><span data-stu-id="b31a5-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="b31a5-167">toodecompress y descifrar archivos, escriba:</span><span class="sxs-lookup"><span data-stu-id="b31a5-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="b31a5-168">Tenga en cuenta que las extensiones de archivo real de hello ahora se muestran para todos los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="b31a5-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Edición del paquete de soporte](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="b31a5-170">Cuando se le pide Hola frase de contraseña, escriba la frase de contraseña de Hola que utilizó cuando creó el paquete de soporte de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="b31a5-171">Busque la carpeta toohello que contiene los archivos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="b31a5-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="b31a5-172">Porque los archivos de registro de hello ahora están descomprimidos y descifrar, que tienen extensiones de archivo original.</span><span class="sxs-lookup"><span data-stu-id="b31a5-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="b31a5-173">Modifique estos archivos tooremove cualquier información específica del cliente, como nombres de volúmenes y direcciones IP de dispositivo y guardar archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="b31a5-174">Hola cerrar archivos toocompress con gzip y cifrarlos con AES-256.</span><span class="sxs-lookup"><span data-stu-id="b31a5-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="b31a5-175">Se trata de la velocidad y la seguridad para transferir el paquete de soporte de Hola a través de una red.</span><span class="sxs-lookup"><span data-stu-id="b31a5-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="b31a5-176">toocompress y cifrar los archivos, escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31a5-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edición del paquete de soporte](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="b31a5-178">Cuando se le solicite, proporcione una frase de contraseña para el paquete de soporte modificado Hola.</span><span class="sxs-lookup"><span data-stu-id="b31a5-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="b31a5-179">Escriba Hola nueva frase de contraseña, por lo que puede compartir con Microsoft Support cuando se solicita.</span><span class="sxs-lookup"><span data-stu-id="b31a5-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="b31a5-180">Ejemplo: Edición de archivos de un paquete de soporte en un recurso compartido protegido por contraseña</span><span class="sxs-lookup"><span data-stu-id="b31a5-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="b31a5-181">Hola de ejemplo siguiente muestra cómo toodecrypt, editar y volver a cifrar un paquete de soporte.</span><span class="sxs-lookup"><span data-stu-id="b31a5-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="b31a5-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b31a5-182">Next steps</span></span>

* <span data-ttu-id="b31a5-183">Obtenga información acerca de hello [la información recopilada en el paquete de soporte de Hola](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="b31a5-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="b31a5-184">Obtenga información acerca de cómo demasiado[paquetes de compatibilidad de uso y el dispositivo los registros tootroubleshoot la implementación de dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b31a5-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="b31a5-185">Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b31a5-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

