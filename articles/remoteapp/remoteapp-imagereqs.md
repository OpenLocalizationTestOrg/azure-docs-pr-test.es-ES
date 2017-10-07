---
title: requisitos de imagen de RemoteApp aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de los requisitos de Hola para crear toobe de imágenes que se usa con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Requisitos para las imágenes Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure utiliza un toohost de imagen de Windows Server 2012 R2 en todos los programas de Hola que desee tooshare con los usuarios. toocreate una imagen personalizada, puede empezar con una imagen existente o [crear una nueva](remoteapp-create-custom-image.md).

> [!TIP]
> ¿Sabía que su proporciona de suscripción de Azure RemoteApp en que acceso tooa de imagen de Windows Server 2012 R2 Hola Galería de máquinas virtuales de Azure puede usar toocreate en su propia imagen de plantilla? [Compruébelo](remoteapp-image-on-azurevm.md).  
> 
> 

requisitos de Hello para la imagen de Hola que se pueden cargar para su uso con Azure RemoteApp son:

* Las aplicaciones personalizadas no almacenan datos localmente en la imagen de Hola. Estas imágenes no tienen estado y solo deben contener aplicaciones.
* imagen de Hello no contiene datos que se pueden perder.
* tamaño de la imagen de Hello debe ser un múltiplo de MB. Si intentas tooupload una imagen que no es un múltiplo exacto, se producirá un error en la carga de Hola.
* tamaño de la imagen de Hello debe ser 127 GB o menor.
* Debe estar en un archivo VHD (los archivos VHDX no se admiten actualmente).
* Hola VHD no debe ser una máquina virtual de generación 2.
* Hola VHD puede ser de tamaño fijo o de expansión dinámica. Un disco duro virtual de expansión dinámica se recomienda porque toma menos tooAzure tooupload de tiempo que un archivo de disco duro virtual de tamaño fijo.
* disco de Hello debe inicializarse con estilo de partición de registro de arranque maestro (MBR) Hola. no se admite el estilo de partición GPT (tabla) de particiones GUID Hola.
* Hola VHD debe contener una única instalación de Windows Server 2012 R2. Puede contener varios volúmenes, pero uno de ellos con una instalación de Windows.
* deben estar instalados el rol de Host de sesión de escritorio remoto (RDSH) de Hola y la característica experiencia de escritorio de Hola.
* rol de agente de conexión a Escritorio remoto de Hello debe *no* instalarse.
* Sistema de archivos cifrados (EFS) de Hello debe deshabilitarse.
* Hello imagen debe estar preparada con Sysprep mediante parámetros de hello **/oobe /generalize /shutdown** (no usar hello **/mode: VM** parámetro).
* No se admite la carga de su VHD desde una cadena de instantáneas.

Consulte [Creación de una imagen de Azure RemoteApp](remoteapp-imageoptions.md) para obtener más información sobre la creación de imágenes para Azure RemoteApp.

