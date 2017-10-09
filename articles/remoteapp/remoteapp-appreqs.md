---
title: requisitos de aaaApp de Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información sobre los requisitos de Hola para las aplicaciones que desea toouse en Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Requisitos de aplicaciones
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Azure RemoteApp admite el streaming de aplicaciones Windows de 32 o 64 bits desde una imagen de Windows Server 2012 R2. La mayoría de las aplicaciones Windows de 32 o 64 bits se ejecutan "tal cual" en el entorno de Azure RemoteApp (Servicios de Escritorio remoto antes conocido como Terminal Services). Sin embargo, hay una diferencia entre ejecutar y ejecutar bien; algunas aplicaciones funcionan correctamente y su rendimiento es adecuado, mientras que otras no. Hola siguiente información proporciona una guía para desarrollar aplicaciones en un entorno de servicios de escritorio remoto y probar la compatibilidad de tooensure.

Sugerencia: estamos trabajando en la creación de algunos ejemplos prácticos de aplicaciones para usted. Verá algunos temas nuevos en los que se analiza el uso de Microsoft Access, QuickBooks y App-V en RemoteApp.

## <a name="requirements"></a>Requisitos
Estos tres requisitos, si se siguen, ayudarán a sus aplicaciones a ejecutarse bien en RemoteApp:

1. Las aplicaciones que todos los cumplen [requisitos de certificación para aplicaciones de escritorio de Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) y seguirán demasiado[directrices de programación de servicios de escritorio remoto](https://msdn.microsoft.com/library/aa383490.aspx) tendrá compatibilidad completa con RemoteApp.
2. Las aplicaciones nunca deberían almacenar datos localmente en la imagen de Hola o instancias de RemoteApp que se pueden perder.  Después de crear una colección de RemoteApp, instancias de Hola se clonan y no tienen estados y solo deben contener las aplicaciones. Almacenar datos en un origen externo o en el perfil de usuario de Hola.
3. Las imágenes personalizadas nunca deben contener datos que se puedan perder.  

## <a name="testing-your-apps"></a>Prueba de las aplicaciones
Use estas aplicaciones de tootesting de pasos:

1. Instale Windows Server 2012 R2 y su aplicación
2. Habilite Escritorio remoto
3. Cree dos cuentas de usuario, UserA y UserB, agregar ambos grupo de seguridad de usuario cuentas toohello escritorio remoto.
4. Comprobar la compatibilidad de la sesión mediante el establecimiento de dos toohello de sesiones RDS simultáneas PC al iniciar la aplicación hello.
5. Valide el comportamiento de la aplicación

## <a name="application-development-guidelines"></a>Instrucciones para el desarrollo de aplicaciones
Usar hello siguiendo las directrices para desarrollar aplicaciones de RemoteApp.

### <a name="multiple-users"></a>Varios usuarios
* La instalación de una [aplicación para un único usuario ](https://msdn.microsoft.com/library/aa380661.aspx)puede crear problemas en un entorno de varios usuarios.
* Las aplicaciones deben [almacenar información específica del usuario](https://msdn.microsoft.com/library/aa383452.aspx) en ubicaciones específicas del usuario, por separado de información global que aplica a los usuarios de tooall.
* RemoteApp usa varios [espacios de nombres para objetos de kernel](https://msdn.microsoft.com/library/aa382954.aspx); un espacio de nombres global lo usan principalmente los servicios en aplicaciones cliente/servidor.
* No es seguro tooassume que Hola nombre_equipo o hello [dirección IP](https://msdn.microsoft.com/library/aa382942.aspx) toohello asignado equipo están asociados con un solo usuario dado que varios usuarios pueden haber iniciado sesión al mismo tiempo tooa Host de sesión de escritorio remoto (RD Session Servidor de host).

### <a name="performance"></a>Rendimiento
* Deshabilitar [efectos gráficos](https://msdn.microsoft.com/library/aa380822.aspx) antes de agregar el tooRemoteApp de aplicación.
* disponibilidad de toomaximize CPU para todos los usuarios, o bien deshabilitar [tareas en segundo plano ](https://msdn.microsoft.com/library/aa380665.aspx) o crear tareas en segundo plano eficaz que no son de gran cantidad de recursos.
* Debe ajustar y equilibrar el [uso de subprocesos](https://msdn.microsoft.com/library/aa383520.aspx) de la aplicación en un entorno de varios usuarios y procesadores.
* toooptimize rendimiento, es recomendable para las aplicaciones demasiado[detectar](https://msdn.microsoft.com/library/aa380798.aspx) si está ejecutando en una sesión de cliente.

