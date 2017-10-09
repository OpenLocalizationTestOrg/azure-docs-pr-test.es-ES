---
title: aaaUpload una imagen personalizada para Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupload personalizado de la imagen de Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Carga de una imagen personalizada para RemoteApp de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Ahora que ha creado la imagen de plantilla personalizada o haya actualizado con los cambios, debe tooupload esa biblioteca de imágenes de imagen tooyour Azure RemoteApp. Siga estos pasos.

## <a name="before-you-start"></a>Antes de comenzar
1. Compruebe la imagen personalizada cumple hello [requisitos de la imagen](remoteapp-imagereqs.md) y [requisitos de la aplicación](remoteapp-appreqs.md).
2. Instalar hello [módulo Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Paso a paso sobre cómo imagen personalizada tooupload
1. Abra el Portal de administración de Azure y desplácese toohello página de RemoteApp.
2. En hello **imágenes de plantilla** , haga clic en **cargar** final Hola de página Hola.
3. Escriba un nombre descriptivo para la imagen y especifique la ubicación de la cuenta de hello almacenamiento. Asegúrese de ubicación de hello es hello misma ubicación que la colección RemoteApp o una ubicación donde desea toocreate uno.
4. Cuando se le solicite, descargue Hola script tooyour PC local.
5. Copiar parámetros del comando hello en el Portapapeles de tooyour de cuadro de texto de Hola.
6. Abra una ventana de Windows PowerShell con privilegios elevados.
7. De hello elevado de ventana de Windows PowerShell, vaya toohello mismo directorio donde descargó el script de Hola.
8. Hola pegar copia el comando y presione **ENTRAR**.
   
   se iniciará el proceso de carga de Hola y duración puede depender de muchos factores como la velocidad de la red y el tamaño de imagen de Hola
9. Si la carga no se realiza correctamente debido a la interrupción de la red o cosas como esta, puede reanudar siempre que se inició el proceso de carga de Hola. tooresume una carga, ejecutar script de Hola utilizando de nuevo Hola misma línea de comandos.

> [!WARNING]
> No modifique nunca script de carga de Hola. Comprobaciones específicas han sido implementado tooensure que Hola imagen cumple los requisitos de imagen hello y requisitos de la aplicación.
> 
> 

## <a name="common-problems"></a>Problemas comunes
* Asegúrese de que usa Windows PowerShell y no Azure PowerShell. Necesita módulo de PowerShell de Azure de hello tooinstall porque algunos módulos se necesitan durante el proceso de carga de Hola.
* Nunca modifican script hello, validaciones existen para su comodidad.
* Si el archivo de disco duro virtual de hello obtiene bloqueada durante la carga, copie el archivo hello o tooa nueva carga de ubicación e intente volver a moverlo. Es posible que algunos procesos de Windows impidan la carga.  

