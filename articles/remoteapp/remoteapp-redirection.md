---
title: "redirección de aaaUsing en Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de cómo redirección tooconfigure y el uso de RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Uso del redireccionamiento de RemoteApp de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Redirección de dispositivos permite a los usuarios interactuar con aplicaciones remotas mediante el equipo local de hello dispositivos tootheir adjunto, teléfono o tableta. Por ejemplo, si ha proporcionado Skype a través de RemoteApp de Azure, el usuario necesita cámara Hola instalado en su toowork PC con Skype. Esto también se aplica a las impresoras, altavoces, monitores y a una amplia gama de periféricos conectados mediante USB.

RemoteApp aprovecha la redirección de tooprovide de protocolo de escritorio remoto (RDP) y RemoteFX Hola.

## <a name="what-redirection-is-enabled-by-default"></a>¿Qué redireccionamiento está habilitado de manera predeterminada?
Cuando usas RemoteApp, Hola siguen las redirecciones está habilitada de forma predeterminada. información de Hello entre paréntesis indica la configuración de RDP Hola.

* Reproducir sonidos en el equipo local de hello (**reproducir en este equipo**). (audiomode:i:0)
* Captura de audio del equipo local de Hola y equipo remoto de envío toohello (**grabar desde este equipo**). (audiocapturemode:i:1)
* Imprimir en impresoras de toolocal (redirectprinters:i:1)
* Puertos COM (redirectcomports:i:1)
* Dispositivo de tarjeta inteligente (redirectsmartcards:i:1)
* Portapapeles (toocopy de capacidad y pegar) (redirectclipboard:i:1)
* Desactivar el suavizado de fuentes (permitir suavizado de fuentes: i:1)
* Redirigir todos los dispositivos Plug and Play compatibles. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>¿Qué otro redireccionamiento está disponible?
Existen dos opciones de redireccionamiento deshabilitadas de forma predeterminada:

* Redirección de unidad (asignación de unidad): unidades del equipo local se convierten en las unidades asignadas en la sesión remota de Hola. Esto permite guardar o abrir archivos desde las unidades locales mientras trabaja en una sesión remota de Hola.
* Redireccionamiento de USB: puede usar el equipo local del tooyour adjunto de dispositivos USB Hola dentro sesión remota de Hola.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Cambiar la configuración de redireccionamiento de RemoteApp
Puede cambiar configuración de redirección de dispositivos de Hola para una colección mediante Hola Microsoft Azure PowerShell con el SDK. Después de instalar Hola PowerShell nueva y SDK, configurarla primero toomanage su suscripción como se describe en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

A continuación, use un toohello similar de comando tooset Hola personalizado RDP propiedades siguientes:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Tenga en cuenta que  *`n*  se utiliza como delimitador entre las propiedades individuales.)

tooget una lista de qué propiedades RDP personalizadas configuradas, ejecute hello siguiente cmdlet. Tenga en cuenta que las propiedades personalizadas solo se muestran como resultados y no Hola propiedades predeterminadas:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Al establecer las propiedades personalizadas deben especificar todas las propiedades personalizadas cada vez; en caso contrario, valor de hello revierte toodisabled.   

### <a name="common-examples"></a>Ejemplos comunes
Usar hello después de la redirección de unidad de tooenable de cmdlet:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Usar este cmdlet tooenable redireccionamiento de USB y unidad:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Use este cmdlet toodisable uso compartido del Portapapeles:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Ser seguro toocompletely cerrar todos los usuarios de la colección de hello (y no solo desconectarlos) antes de probar los cambios de Hola. tooensure a los usuarios se registran completamente off, vaya toohello **sesiones** ficha en la colección de Hola Hola portal de Azure y cerrar todos los usuarios que están desconectados o está firmados. A veces puede tardar varios segundos antes de hello tooshow de las unidades locales en el Explorador de dentro de la sesión de Hola.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Cambie la configuración de redireccionamiento de USB en el cliente Windows
Si desea toouse redireccionamiento de USB en un equipo que se conecta tooRemoteApp, hay 2 acciones que deben toohappen. 1: el administrador necesita tooenable redireccionamiento de USB en el nivel de colección de hello mediante Azure PowerShell. 2 - en cada dispositivo en el que desea toouse redireccionamiento de USB, deberá tooenable una directiva de grupo que lo permita. Este paso será necesario toobe realiza para cada usuario que desea toouse redireccionamiento de USB.

> [!NOTE]
> El redireccionamiento USB con RemoteApp de Azure solo se admite en equipos Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Habilitar la redirección de USB para hello colección RemoteApp
Usar hello después de redireccionamiento de USB tooenable de cmdlet en el nivel de colección de hello:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Habilitar la redirección de USB para el equipo de cliente hello
configuración de redirección de tooconfigure USB en el equipo:

1. Hola abrir Editor de directivas de grupo Local (GPEDIT. MSC). (Ejecute gpedit.msc desde un símbolo del sistema de comando).
2. Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.
3. Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.
4. Seleccione **habilitado**y, a continuación, seleccione **administradores y usuarios en hello derechos de acceso de redirección de USB RemoteFX**.
5. Abra un símbolo del sistema con permisos administrativos y ejecute el siguiente comando de hello:
   
        gpupdate /force
6. Reinicie el equipo de Hola.

También puede utilizar toocreate de herramienta de administración de directivas de grupo de Hola y aplicar directiva de redirección de hello USB para todos los equipos del dominio:

1. Inicie sesión en el controlador de dominio de hello como administrador del dominio Hola.
2. Abra Hola consola de administración de directivas de grupo. (Haga clic en **Inicio > Herramientas administrativas > Administración de directivas de grupo**).
3. Navegue toohello dominio o unidad organizativa para la que desea que Directiva de hello toocreate.
4. Haga clic con el botón derecho en **Directiva de dominio predeterminada** y, a continuación, haga clic en **Editar**.
5. Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.
6. Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.
7. Seleccione **habilitado**y, a continuación, seleccione **administradores y usuarios en hello derechos de acceso de redirección de USB RemoteFX**.
8. Haga clic en **Aceptar**.  

