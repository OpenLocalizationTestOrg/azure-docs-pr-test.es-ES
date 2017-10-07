---
title: "prácticas recomendadas de RemoteApp aaaAzure | Documentos de Microsoft"
description: "Prácticas recomendadas para configurar y usar RemoteApp de Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Prácticas recomendadas para configurar y usar RemoteApp de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) para obtener más información.
> 
> 

Hola siguiente información puede ayudarle a configurar y usar Azure RemoteApp productiva.

## <a name="connectivity"></a>Conectividad
* Utilice siempre la versión de cliente más reciente de Hola. El uso de clientes anteriores podría producir problemas de conectividad y otras experiencias degradadas. Habilitar las actualizaciones de la aplicación automática para el dispositivo garantizará que el cliente más reciente Hola siempre se instala.
* Utilice siempre hello más estable y confiable internet conexión disponible tooyou.  
* Use solo las conexiones proxy admitidas para obtener un rendimiento óptimo de conectividad.  no se admite el proxy de SOCKS Hola.

## <a name="applications"></a>Aplicaciones
* Guarde y cierre las aplicaciones de RemoteApp cuando haya terminado con la aplicación hello. No cierre la aplicación hello podrían dar lugar a pérdida de datos.
* Valide las aplicaciones personalizadas antes de usarlas en RemoteApp de Azure. Esto incluye garantizar funcionan en una plataforma de múltiples sesiones y no consumen recursos innecesarios como la memoria y CPU que podría privar a otro usuario de hello misma colección. Para obtener información, descargue y revise hello [prácticas recomendadas de compatibilidad de aplicaciones para servicios de escritorio remoto](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuración y administración
* Mantenga las imágenes de plantilla seguridad toodate, instalar las actualizaciones de software y otras correcciones críticas según sea necesario. Esto garantiza que como Azure RemoteApp auto-escalas toomeet la capacidad, cada instancia se han modificado.  
* Asegúrese de que su implementación de Servicios de federación de Active Directory (AD FS) es segura y confiable. En caso contrario, es posible que se produzca un error en las autenticaciones de cliente, con lo que se impedirá que los usuarios accedan a RemoteApp de Azure.
* Configurar imágenes de plantilla con características, roles o aplicaciones instaladas, de manera que no tengan estado. No deben confiar en todas las instancias de máquinas virtuales de hello en un servicio de RemoteApp no estaba en un estado persistente.
  * Almacenar todos los datos de usuario en otro servicio de toohello externo de ubicaciones de almacenamiento, o perfiles de usuario, como OneDrive o recursos compartidos de archivos local.
  * Almacén de datos compartidos en servicio de toohello externo de ubicaciones de almacenamiento, como OneDrive o recursos compartidos de archivos local.
  * Configure las opciones de todo el sistema en la imagen de la plantilla de hello en lugar de en las máquinas virtuales individuales en un servicio.
  * Deshabilitar las actualizaciones de software automáticas para las aplicaciones publicadas: en su lugar aplicarlas manualmente toohello imagen de plantilla y probarlas antes de implementar desde plantilla Hola.

