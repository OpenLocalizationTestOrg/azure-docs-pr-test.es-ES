---
title: una imagen de Azure RemoteApp aaaCreate | Documentos de Microsoft
description: "Obtener información sobre opciones de hello disponibles para la creación de imágenes para Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Creación de una imagen de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure utiliza imágenes toohold Hola aplicaciones que se comparten con los usuarios. (Tomamos la imagen y usar las máquinas virtuales de toocreate - que el acceso a los usuarios de hello cuando inician sesión en Azure RemoteApp.) toocreate una colección de RemoteApp de Azure con su elección de las aplicaciones, ya sea en la nube o híbridas, primero debe crear una imagen con esas aplicaciones instaladas. A continuación, cree una recopilación que use esa imagen, asignar a usuarios colección toohello y publicar los usuarios toothose de aplicaciones.

Tiene varias opciones para crear o utilizar imágenes. Hola básica [requisito](remoteapp-imagereqs.md) para una imagen que ejecutan Windows Server 2012 R2 y tiene instalado el rol de Host de sesión de escritorio remoto (RDSH) de Hola. La forma de conseguir esto es lo que resulta interesante.

Tiene las siguientes opciones cuando se trata de tooimages de Hola:

* Puede importar y utilizar una [imagen basada en una máquina virtual de Azure](remoteapp-image-on-azurevm.md). Esto es una buena opción para aplicaciones de línea de negocio que requieren una configuración personalizada. Puede personalizar hello toowork de imagen para la aplicación hello.
* Puede [crear y cargar una imagen personalizada](remoteapp-create-custom-image.md). Esto es apropiado si ya tiene una imagen que se utiliza para la implementación local de Servicios de Escritorio remoto.
* Puede usar uno de hello [imágenes de plantilla](remoteapp-images.md) incluido en su suscripción de RemoteApp. Estas imágenes se crean y mantenido por el equipo de RemoteApp de Hola y contienen algunas aplicaciones estándares (por ejemplo, hello Office suite) que puede hacer que los usuarios de tooyour disponible. Tenga en cuenta que esa imagen de Office 365 Pro Plus Hola sola puede usarse en un entorno de producción.

Independientemente de dónde obtener la imagen o cómo crear, es conveniente que comprenden hello toomake [requisitos de la aplicación](remoteapp-appreqs.md) tooensure que la aplicación funciona bien en RemoteApp. A continuación, el paso siguiente de hello es toocreate una [nube](remoteapp-create-cloud-deployment.md) o [híbrida](remoteapp-create-hybrid-deployment.md) colección.

