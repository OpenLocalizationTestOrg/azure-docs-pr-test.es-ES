---
title: "un paquete de soporte técnico de StorSimple aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo descifrar toocreate y editar un paquete de soporte para el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Crear y administrar paquetes de soporte técnico de StorSimple
## <a name="overview"></a>Información general
Un paquete de soporte técnico de StorSimple es un mecanismo fácil de usar que recopila todos los registros pertinentes tooassist Microsoft Support a solucionar los problemas del dispositivo StorSimple. Hello registros recopilados están cifrados y comprimidos.

Este tutorial incluye instrucciones paso a paso toocreate y administrar el paquete de soporte de Hola.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Crear y cargar un paquete de soporte en hello portal de Azure clásico
También puede crear y cargar un sitio de Microsoft Support de toohello de paquete de soporte técnico a través de hello **mantenimiento** página de servicio de Hola Hola portal de Azure clásico.

> [!NOTE]
> carga de Hello requiere una clave de paso de soporte técnico. El ingeniero de soporte técnico debe proporcionar este tooyou en un correo electrónico.
> 
> 

Un paquete de soporte cifrados y comprimidos (archivo .cab) es el sitio de soporte técnico de toohello creado y cargado. Ingeniero de soporte técnico de Hello, a continuación, puede recuperar este paquete desde el sitio de soporte técnico de Hola para solucionar el problema de Hola.

Realizar Hola pasos de hello toocreate portal clásico un paquete de soporte.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate un paquete de soporte en hello portal de Azure clásico
1. Seleccione **Dispositivos** > **Mantenimiento**.
2. Hola **paquete de soporte** sección, seleccione **crear y cargar paquete de soporte**.
3. Hola **crear y cargar paquete de soporte** diálogo cuadro, Hola siguientes:
   
    ![Creación de un paquete de soporte](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * Hola **clave de paso de soporte técnico** texto cuadro, escriba la clave de paso de Hola. El ingeniero de soporte técnico de Microsoft debe enviar este tooyou de clave de paso por correo electrónico.
   * Seleccione casilla hello tooprovide tooautomatically consentimiento carga compatibilidad Hola paquete Microsoft Support toohello sitio.
   * Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Creación manual de un paquete de soporte
En algunos casos, necesitará toomanually crear paquete de soporte de Hola a través de Windows PowerShell para StorSimple. Por ejemplo:

* Si necesita información confidencial de tooremove desde el registro de los archivos anterior toosharing con Microsoft Support.
* Si tiene dificultades para cargar el paquete Hola debido a problemas de tooconnectivity.

Puede compartir su paquete de soporte generado manualmente con el servicio de soporte técnico de Microsoft mediante el correo electrónico. Realizar Hola siguiendo los pasos toocreate un paquete de soporte de Windows PowerShell para StorSimple.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate un paquete de soporte de Windows PowerShell para StorSimple
1. toostart una sesión de Windows PowerShell como administrador en el equipo remoto de Hola que ha utilizado el dispositivo de StorSimple de tooconnect tooyour, escriba Hola siguiente comando:
   
    `Start PowerShell`
2. En la sesión de Windows PowerShell de hello, conectar toohello consola SSAdmin del dispositivo:
   
   * En hello símbolo del sistema, escriba:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * En el cuadro de diálogo de Hola que se abre, escriba la contraseña de administrador del dispositivo. contraseña de Hello predeterminada es:
     
      `Password1`
     
      ![Cuadro de diálogo de credenciales de PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Seleccione **Aceptar**.
   * En hello símbolo del sistema, escriba:
     
      `Enter-PSSession $MS`
3. En la sesión de Hola que se abre, escriba comando adecuado Hola.
   
   * Para los recursos compartidos de red que están protegidos por contraseña, escriba:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Se le pedirá una contraseña, una carpeta compartida de la red de toohello ruta de acceso y una frase de contraseña (porque se cifra el paquete de soporte de hello). A continuación, se crea un paquete de soporte en la carpeta especificada de Hola.
   * Para los recursos compartidos que no están protegidas por contraseña, no es necesario hello `-Credential` parámetro. Escriba Hola siguiente:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       se creará el paquete de soporte técnico de Hola para ambos controladores en la carpeta compartida de red especificado de Hola. Es un archivo comprimido cifrado que puede enviarse tooMicrosoft soporte técnico para solucionar problemas. Para obtener más información, consulte [Ponerse en contacto con el soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Hola parámetros del cmdlet Export-HcsSupportPackage
Puede usar Hola parámetros con el cmdlet Export-HcsSupportPackage Hola siguientes.

| Parámetro | Obligatorio/opcional | Description |
| --- | --- | --- |
| `-Path` |Obligatorio |Utilice tooprovide Hola ubicación de carpeta compartida en la red de hello en qué Hola se coloca el paquete de soporte. |
| `-EncryptionPassphrase` |Obligatorio |Use tooprovide una frase de contraseña toohelp cifrar paquete de soporte de Hola. |
| `-Credential` |Opcional |Usar credenciales de acceso de toosupply Hola carpeta compartida de red. |
| `-Force` |Opcional |Paso de confirmación de la frase de contraseña de cifrado de hello con uso tooskip. |
| `-PackageTag` |Opcional |Usar toospecify en un directorio *ruta de acceso* en qué soporte Hola se coloca el paquete. valor predeterminado de Hello es [nombre de dispositivo]-[fecha y hora actuales:aaaa-mm-dd-hh-mm-ss]. |
| `-Scope` |Opcional |Especificar como **clúster** toocreate (valor predeterminado) un paquete de soporte para ambos controladores. Si desea toocreate un paquete solo para el controlador actual de hello, especifique **controlador**. |

## <a name="edit-a-support-package"></a>Editar un paquete de soporte
Una vez que haya generado un paquete de soporte, deberá información confidencial de tooedit Hola paquete tooremove. Esto puede incluir nombres de volúmenes, direcciones IP de dispositivos y nombres de copia de seguridad de archivos de registro de hello.

> [!IMPORTANT]
> Solo pueden editarse los paquetes de soporte generados a través de Windows PowerShell para StorSimple. No se puede editar un paquete creado en hello portal de Azure clásico con el servicio StorSimple Manager.
> 
> 

tooedit un paquete de soporte antes de cargarlo en el sitio de Microsoft Support hello, descifrar primero el paquete de soporte de hello, editar archivos de hello y, a continuación, volver a cifrarlos. Realizar pasos de Hola.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit un paquete de soporte de Windows PowerShell para StorSimple
1. Generar un paquete de soporte técnico como se ha descrito anteriormente, en [toocreate un paquete de soporte de Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Descargar el script de Hola](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente en el cliente.
3. Importe el módulo de Windows PowerShell de Hola. Especifique la carpeta local Hola ruta de acceso toohello en la que descargó el script de Hola. módulo de hello tooimport, escriba:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Todos los archivos de hello están *.aes* archivos que están comprimidos y cifrados. toodecompress y descifrar archivos, escriba:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Tenga en cuenta que las extensiones de archivo real de hello ahora se muestran para todos los archivos de saludo.
   
    ![Edición del paquete de soporte](./media/storsimple-create-manage-support-package/IC750706.png)
5. Cuando se le pide Hola frase de contraseña, escriba la frase de contraseña de Hola que utilizó cuando creó el paquete de soporte de Hola.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Busque la carpeta toohello que contiene los archivos de registro de hello. Porque los archivos de registro de hello ahora están descomprimidos y descifrar, que tienen extensiones de archivo original. Modifique estos archivos tooremove cualquier información específica del cliente, como nombres de volúmenes y direcciones IP de dispositivo y guardar archivos de Hola.
7. Hola cerrar archivos toocompress con gzip y cifrarlos con AES-256. Se trata de la velocidad y la seguridad para transferir el paquete de soporte de Hola a través de una red. toocompress y cifrar los archivos, escriba Hola siguiente:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edición del paquete de soporte](./media/storsimple-create-manage-support-package/IC750707.png)
8. Cuando se le solicite, proporcione una frase de contraseña para el paquete de soporte modificado Hola.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Escriba Hola nueva frase de contraseña, por lo que puede compartir con Microsoft Support cuando se solicita.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Ejemplo: Edición de archivos de un paquete de soporte en un recurso compartido protegido por contraseña
Hola de ejemplo siguiente muestra cómo toodecrypt, editar y volver a cifrar un paquete de soporte.

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

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[paquetes de compatibilidad de uso y el dispositivo los registros tootroubleshoot la implementación de dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

