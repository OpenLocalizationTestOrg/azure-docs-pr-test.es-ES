---
title: "aaaNever almacén de datos confidenciales en imágenes personalizadas para Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de las instrucciones de Hola para almacenar datos en imágenes personalizadas en Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Nunca almacene información confidencial en imágenes personalizadas
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Si hospeda su propia aplicación en Azure RemoteApp, Hola primer paso es toocreate una imagen personalizada. Utilizamos ese instancias de máquina virtual de toocreate de imagen personalizada que atienden a sus aplicaciones, usuarios de tooyour. imagen personalizada Hello debe contener sólo las aplicaciones y datos confidenciales nunca que se pueden perder, como bases de datos SQL, archivos de personal o archivos de datos especiales como los archivos de la empresa de QuickBooks. Todos los datos confidenciales deben residir externo tooAzure RemoteApp en un servidor de archivos, otra máquina virtual de Azure, o en SQL Azure. imagen de Hello debe solo host Hola la aplicación que se conecta el origen de datos de toohello y muestra los datos de Hola. Consulte [Requisitos para las imágenes Azure RemoteApp](remoteapp-imagereqs.md) para obtener más información. 

toounderstand ¿por qué no debería almacenar datos confidenciales, debe toounderstand cómo funciona RemoteApp de Azure. Cuando se crea o actualiza una colección, entre bastidores de hello varios clones o copias de la imagen de Hola se crean. Estas instancias de máquina virtual son réplicas exactas de imagen personalizada de hello; Cuando los usuarios inician aplicaciones son tooone conectado de estas instancias de máquina virtual. Pero no se garantiza hello misma instancia y no es importante porque son no persistentes. Hola instancias de máquina virtual aplicaciones de hospedaje hello no son persistentes y pueden ser destruido o eliminado en función, por ejemplo, durante la actualización de la colección. 

Una vez que se aprovisiona la colección de Hola y los usuarios inician toohello conectar máquinas virtuales, datos de usuario están persistentes y proteger porque se guarda en un almacenamiento independiente dentro de un disco duro virtual que llamamos una [disco de perfil de usuario (UPD)](remoteapp-upd.md), que es el perfil de usuario de Hola c:\Users\<userprofile >. Cuando se inicia una aplicación, se monta y se tratan como un perfil de usuario local por sistema operativo de Hola Hola UPD. Obtenga más información sobre cómo [Azure RemoteApp guarda la configuración y los datos de usuario](remoteapp-upd.md).

Datos de ejemplo que no deben residir en la imagen de hello:

* Datos compartidos para los usuarios tooaccess
* Base de datos SQL o Base de datos QuickBooks
* Todos los datos en D:\

Datos de ejemplo que pueden residir en hello predeterminado perfil toobe se copian en UPD de todos los usuarios:

* Archivos de configuración por usuario
* Scripts que los usuarios tendrían que conservar en el UPD

Puntos clave:

* No almacene nunca datos confidenciales que se pueden perder en la imagen de hello al crear una imagen personalizada.
* Los datos confidenciales siempre deben residir en un servidor de archivos independiente, separar de la máquina virtual de Azure, en nube hello y las instancias VM externo siempre toohello hospedar sus aplicaciones en Azure RemoteApp. 
* Datos de usuario se guardan y se conserva en el disco de perfil de usuario (UDP) de Hola

