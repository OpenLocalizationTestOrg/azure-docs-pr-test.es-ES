---
title: "¿aaaAzure RemoteApp - cómo ancho de banda de red y la calidad de experiencia de trabajo juntos? | Microsoft Docs"
description: "Obtenga información acerca de cómo puede afectar el ancho de banda de red en Azure RemoteApp a la calidad de la experiencia de los usuarios."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp: ¿cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Cuando se encuentre en hello [ancho de banda de red total](remoteapp-bandwidth.md) requerido para Azure RemoteApp, tenga en Hola de cuenta siguientes factores: estos forman parte de un sistema dinámico que impactos Hola experiencia global del usuario. 

* **Ancho de banda de red disponible y condiciones actuales de la red** -un conjunto de parámetros (pérdida, latencia y vibración) en hello igual de red en un momento dado puede afectar la aplicación de hello experiencia de transmisión por secuencias, lo que significa una experiencia global del usuario reducidos. ancho de banda de Hello disponible en la red es una función de congestión, pérdida aleatoria, la latencia porque todos estos parámetros afectan al mecanismo de control de congestión de hello, que a su vez controles Hola colisiones de tooavoid de velocidad de transmisión.  Por ejemplo, una red con pérdida de datos o con una latencia elevada realizará usuario Hola experimentar incorrecta incluso en una red con ancho de banda de 1000 MB. latencia y pérdida de Hello varían en función de número de Hola de usuarios que se encuentran en hello misma red y lo que hacen los usuarios (por ejemplo, ver vídeos, descargar o cargar archivos grandes, imprimir).
* **Escenario de uso** -experiencia de hello depende de qué Hola hacen los usuarios como usuarios, como un grupo en hello misma red. Por ejemplo, la lectura de una diapositiva requiere solo un toobe de marco único actualizado; Si el usuario de hello skims y se desplaza sobre el contenido de Hola de un documento de texto, que necesitan un número mayor de toobe fotogramas actualizado por segundo. Hola comunicación atrás y hacia delante toohello servidor en este escenario finalmente consumirá más ancho de banda de red. Considere también un ejemplo extremo: varios usuarios están viendo vídeos de alta definición (como, por ejemplo, con una resolución de 4K), realizando llamadas de conferencias HD, jugando a videojuegos en 3D o trabajando en sistemas CAD. Todo esto puede hacer que incluso una red con un ancho de banda muy alto sea prácticamente inservible.
* **Número de hello y resolución de pantallas de la pantalla** -más ancho de banda de red es necesario toofull actualización mayores pantallas a pantallas más pequeñas. tecnología subyacente de Hello hace un buen trabajo de codificación y transmitir sólo las regiones de Hola de pantallas de Hola que se han actualizado, pero una vez en cuando, pantalla completa de bienvenida necesita toobe actualizado. Cuando el usuario de hello tiene una pantalla de resolución superior (por ejemplo la resolución de 4K), esa actualización requiere más ancho de banda de red a una pantalla con una resolución inferior (por ejemplo, 1024x768px). Esta misma lógica se aplica si usa más de una pantalla de redireccionamiento. Ancho de banda debe tooincrease con número de Hola de pantallas.
* **Redirección del Portapapeles y dispositivos** : se trata de un problema no muy obvio, pero en muchos casos si un usuario almacena una gran parte del Portapapeles de toohello de datos, que tarda un poco de tiempo para que tootransfer de información de cliente de escritorio remoto de hello toohello servidor. experiencia de nivel inferior de Hello puede verse afectado por la experiencia de Hola de enviar el contenido del Portapapeles de hello en dirección ascendente. Hello mismo se aplica a la redirección de dispositivos - si un escáner o cámara web genera una gran cantidad de datos que necesita toobe envía toohello ascendente servidor, una impresora debe tooreceive un documento de gran tamaño o necesidades de almacenamiento local, toobe tooan disponibles aplicación en ejecución en hello en la nube toocopy un archivo de gran tamaño, los usuarios pueden notar fotogramas descartados o temporalmente "inmovilizado" vídeo debido a datos de hello necesarios para la redirección de dispositivos de hello está aumentando el ancho de banda de red de hello es necesario. 

Al evaluar sus necesidades de ancho de banda de red, asegúrese de tooconsider seguro todos estos factores funciona como un sistema.

Ahora, vuelva atrás toohello [artículo de ancho de banda de red principal](remoteapp-bandwidth.md), o se mueven en tootesting su [ancho de banda de red](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Más información
* [Calcular el uso del ancho de banda de red de Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - testing your network bandwidth usage with some common scenarios (Azure RemoteApp: probar su uso de ancho de banda de red con algunos escenarios comunes)](remoteapp-bandwidthtests.md)
* [Ancho de banda de red de Azure RemoteApp: directrices generales (si no puede probarlo usted mismo)](remoteapp-bandwidthguidelines.md)

