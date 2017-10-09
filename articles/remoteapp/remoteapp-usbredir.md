---
title: "aaaHow ¿redirigir dispositivos USB en Azure RemoteApp? | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse redirección de dispositivos USB en Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Redireccionamiento de los dispositivos USB en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Redirección de dispositivos permite a los usuarios usar tableta o equipo de hello USB dispositivos tootheir conectados con aplicaciones de hello en Azure RemoteApp. Por ejemplo, si comparte Skype a través de Azure RemoteApp, los usuarios necesitan toobe pueda toouse sus cámaras de dispositivo.

Antes de seguir adelante, asegúrese de leer información de redirección de USB hello en [mediante el redireccionamiento de Azure RemoteApp](remoteapp-redirection.md). Sin embargo recomienda Hola nusbdevicestoredirect:s: * no funcionará para cámaras web USB y podrían no funcionar para algunas impresoras USB o dispositivos multifuncionales de USB. Por cuestiones de diseño y por motivos de seguridad, Administrador de RemoteApp de Azure de Hola tiene tooenable redirección GUID de clase de dispositivo o Id. de instancia de dispositivo antes de que los usuarios pueden usar los dispositivos.

Aunque en este artículo se habla sobre la redirección de cámara web, puede usar un similar enfoque tooredirect las impresoras USB y otros dispositivos USB multifuncionales que no se redirigen por hello **nusbdevicestoredirect:s:*** comando.

## <a name="redirection-options-for-usb-devices"></a>Opciones de redireccionamiento de dispositivos USB
RemoteApp de Azure utiliza mecanismos muy similares para redirigir dispositivos USB como disponibles los Hola servicios de escritorio remoto. Hello tecnología subyacente le permite elegir método de redirección correcto de Hola para un determinado dispositivo, hello tooget lo mejor de ambos alto nivel y redirección de dispositivos USB RemoteFX mediante hello **usbdevicestoredirect:s:** comando. Hay cuatro elementos toothis comando:

| Orden de procesamiento | Parámetro | Description |
| --- | --- | --- |
| 1 |* |Selecciona todos los dispositivos que no se recogen mediante el redireccionamiento de alto nivel. Nota: por diseño, * no funciona para las cámaras web USB. |
| {GUID de clase de dispositivo} |Selecciona todos los dispositivos que coinciden con hello especificada la clase de instalación de dispositivos. | |
| USB\InstanceID |Selecciona un dispositivo USB especificado para hello tiene el identificador de instancia. | |
| 2 |-USB\Instance ID |Quita la configuración de redirección de hello de dispositivo especificado Hola. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Redirigir un dispositivo USB mediante el uso de GUID de la clase de dispositivo Hola
Hay dos formas de clase de dispositivo de hello toofind GUID que se puede usar para la redirección. 

Hola primera opción es hello toouse [tooVendors disponible de clases definidas dispositivo el programa de instalación](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Seleccionar clase de Hola que más se asemeje al equipo local de hello dispositivo toohello adjunto. Para las cámaras digitales, podría ser una clase de dispositivo de creación de imágenes o una clase de dispositivo de captura de vídeo. Necesitará toodo algunos experimentación con Hola dispositivo clases toofind Hola correcta de la clase GUID que funciona con hello localmente adjunta dispositivo USB (en nuestro cámara web de hello mayúsculas).

Una manera mejor o segunda opción hello, es toofollow estos dispositivos específicos de pasos toofind Hola GUID de clase:

1. Abra el Administrador de dispositivos de hello, busque dispositivo Hola que se redirigirán y haga clic en y, a continuación, abra las propiedades de Hola.
   ![Abra el Administrador de dispositivos de Hola](./media/remoteapp-usbredir/ra-devicemanager.png)
2. En hello **detalles** ficha, elija la propiedad de hello **Guid de la clase**. valor de Hola que aparece es hello GUID de clase de ese tipo de dispositivo.
   ![Propiedades de la cámara](./media/remoteapp-usbredir/ra-classguid.png)
3. Usar dispositivos de tooredirect de valor de Guid de clase de Hola que coinciden con él.

Por ejemplo:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Puede combinar varias redirecciones de dispositivo en hello mismo cmdlet. Por ejemplo: tooredirect de almacenamiento local y un puerto USB web cámara, cmdlet tiene el siguiente aspecto:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Al establecer la redirección de dispositivos por GUID de clase se redirigen todos los dispositivos que coinciden con la que la clase GUID de hello especificado colección. Por ejemplo, si hay varios equipos en la red local de Hola que tengan Hola mismo cámaras web USB, puede ejecutar un cmdlet único tooredirect todas hello web cámaras.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Redirigir un dispositivo USB mediante el uso de Id. de instancia de dispositivo de Hola
Si desea un control más minucioso y redirección de toocontrol por dispositivo, puede usar hello **USB\InstanceID** parámetro de redirección.

parte más difícil de Hola de este método detecta el identificador de dispositivo instancia Hola USB. Tendrá necesita acceso a toohello equipo y el dispositivo USB específico de Hola. A continuación, siga estos pasos:

1. Habilitar la redirección de dispositivos de hello en la sesión de escritorio remoto tal como se describe en [¿cómo puedo usar mi dispositivos y recursos en una sesión de escritorio remoto?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Abra una conexión a Escritorio remoto y haga clic en **Mostrar opciones**.
3. Haga clic en **Guardar como** toosave Hola conexión tooan RDP archivo de configuración actual.  
    ![Guardar la configuración de Hola como un archivo RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Elija un nombre de archivo y una ubicación, por ejemplo MyConnection.rdp y PC\Documents este y guarde el archivo hello.
5. Abra hello MyConnection.rdp archivo utilizando un editor de texto y buscar Id. de instancia de hello de dispositivo de hello desea tooredirect.

Ahora puede utilizar Id. de instancia de Hola Hola siguiente cmdlet:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Permítanos ayudarle
¿Sabía que en suma toorating este artículo y realizar comentarios hacia abajo, a continuación, puede realizar cambios toohello artículo? ¿Falta algo? ¿Algo no es correcto? ¿Algo de lo que he escrito es simplemente confuso? Desplazarse hacia arriba y haga clic en **editar en GitHub** toomake cambios - los procederán toous para su revisión y, a continuación, una vez que se aprueban en ellos, podrá ver los cambios y mejoras aquí.

