---
title: datos de usuario de aaaMigrate de RemoteApp de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate los datos de usuario dentro y fuera de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>¿Cómo toomigrate datos dentro y fuera de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Puede usar muchas distintas herramientas y métodos tootransfer [datos de usuario](remoteapp-upd.md) dentro y fuera de Azure RemoteApp. Estos son algunos métodos:

* Copiar y pegar mediante el uso compartido del Portapapeles
* Copiar archivos y datos de servidor de archivos de tooa
* Copie los archivos tooOneDrive para la empresa a través de un explorador
* Copiar archivos mediante redirección

> [!NOTE]
> No se puede habilitar hello OneDrive para los agentes de sincronización de negocio o un consumidor - [no se admiten](remoteapp-onedrive.md) en Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Uso de copiar y pegar en el Explorador de archivos
Copiar y pegar mediante el Portapapeles de hello está habilitada en las implementaciones de RemoteApp [predeterminada](remoteapp-redirection.md). Gracias a esto, los usuarios pueden copiar archivos entre su equipo local y aplicaciones de RemoteApp. A menudo, a través de curso normal de Hola de uso de aplicaciones de RemoteApp, los usuarios han guardado archivos UPD tootheir - mover que datos de RemoteApp están fáciles:

1. [Publique el Explorador de archivos como aplicación](remoteapp-publish.md) en una colección de RemoteApp. (tenga en cuenta que se trata de una tarea administrativa).
2. Dirigir la aplicación de explorador de archivos de los usuarios toolaunch Hola publicada y toouse que toocopy y pegue los archivos en su UPD y fuera de ella.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Cargar archivos y servidor de archivos de datos tooa mediante la copia de archivos de red estándar
A menudo las organizaciones usar datos generales de toostore de servidores de archivos. Si conoce el nombre del servidor de Hola o ubicación, los usuarios pueden examinar Hola red local para el servidor de hello y, a continuación, copie sus archivos, igual que hicieron anteriormente. Nuevo podrá desea toopublish tooRemoteApp de explorador de archivos y, a continuación, compartirlo con los usuarios.

> [!NOTE]
> servidor de archivos de Hello debe estar en la red enrutable Hola que RemoteApp se implementó en.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Copie los archivos tooOneDrive para la empresa
Aunque no se puede habilitar hello OneDrive para el agente de sincronización de negocios en RemoteApp, puede seguir copiar archivos desde su tooOneDrive UPD para la empresa a través de un explorador. 

1. Publicar tooRemoteApp del explorador de archivos y, a continuación, indicar a los usuarios tooaccess Hola archivos a través de esa aplicación. 
2. Es más fáciles archivos tootransfer si están comprimidos, por lo que los usuarios deben crear un archivo .zip que todos los de hello archivos toomove tooOneDrive contiene para la empresa.
3. Pida el portal de usuarios toogo toohello Office 365 y, a continuación, vaya tooOneDrive y cargar el archivo .zip de Hola.

## <a name="copy-files-by-using-drive-redirection"></a>Copia de archivos mediante la redirección de unidades
Si ha habilitado la [redirección de unidades](remoteapp-redirection.md), ya ha creado una unidad asignada para los usuarios. En este caso, puede sus archivos en la unidad de hello redirigido zip y, a continuación, guardarlos tootheir PC local.

## <a name="how-administrators-can-export-data"></a>Cómo pueden exportar datos los administradores

Administra para Azure RemoteApp puede exportar todos los discos de perfil de usuario (UDP) para todas las colecciones dentro de un almacenamiento con PowerShell de Azure de suscripción tooAzure cmdlet Export-AzureRemoteAppUserDisk.  No hay ninguna capacidad tooselect individuales UPD.  Cuando se ejecuta el comando de PowerShell de hello, cada disco de usuario podrá tener un 50gb de tamaño de disco fijo y almacenamiento tooAzure exportado.  Los costos del almacenamiento de Azure se cobrarán inmediatamente para este almacenamiento.  Al ejecutar este comando Asegúrese de no hay ninguna sesión de exportación de hello en caso contrario se producirá un error.

Los UPD para las implementaciones de Azure RemoteApp unidas a un dominio solo pueden usarse de nuevo en una implementación de RDS; las implementaciones no unidas a un dominio no se pueden usar.  Si estos discos se utilizará en una implementación de RDS se recomienda toouse nuestro [scripts automatizados](https://github.com/arcadiahlyy/aramigration) que se exporte, convertir e importar Hola del UPD en una implementación de RDS.

