---
title: "administración de service Manager aaaStorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage dispositivo de StorSimple mediante el uso de hello en el servicio StorSimple Manager Hola portal de Azure clásico."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Usar hello StorSimple Manager servicio tooadminister el dispositivo de StorSimple
## <a name="overview"></a>Información general
Este artículo describe la interfaz de servicio de StorSimple Manager hello, incluyendo cómo tooconnect tooit, Hola distintas opciones disponibles y proporciona vínculos out toohello flujos de trabajo específicos que se pueden realizar a través de esta interfaz de usuario. Esta guía es aplicable tooboth; Hola StorSimple físico y el dispositivo virtual Hola.

Después de leer este artículo, aprenderá a:

* Conectar el servicio de administrador de tooStorSimple
* Navegue Hola UI del Administrador de StorSimple
* Administrar el dispositivo StorSimple mediante el servicio StorSimple Manager Hola

## <a name="connect-toostorsimple-manager-service"></a>Conectar el servicio de administrador de tooStorSimple
Hola el servicio StorSimple Manager se ejecuta en Microsoft Azure y conecta a los dispositivos de StorSimple toomultiple. Usar un portal clásico central de Microsoft Azure ejecuta en un explorador toomanage estos dispositivos. tooconnect toohello el servicio StorSimple Manager, Hola después.

#### <a name="tooconnect-toohello-service"></a>servicio de toohello tooconnect
1. Navegue demasiado[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Con sus credenciales de cuenta de Microsoft, inicie sesión en el portal clásico de Microsoft Azure toohello (que se encuentra en hello superior derecha del panel de hello).
3. Desplácese hacia abajo Hola dejado el servicio StorSimple Manager Hola de navegación panel tooaccess.

## <a name="navigate-storsimple-manager-service-ui"></a>Navegar por la UI del servicio de Administrador de StorSimple
Hola jerarquía de navegación para el servicio de StorSimple Manager hello que en hello en la tabla siguiente se muestra interfaz de usuario.

* **StorSimple Manager** página de aterrizaje toma dispositivos de tooall aplicables de páginas de nivel de servicio de interfaz de usuario de toohello dentro de un servicio.
* **Dispositivos** página tarda un dispositivo específico de tooa aplicables de páginas de interfaz de usuario de toohello: nivel de dispositivo.
* **Contenedores de volúmenes** página tarda toohello página de volumen que muestra todos los volúmenes de hello asociados con un dispositivo.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>Jerarquía de navegación del servicio de Administrador de StorSimple
| Página de aterrizaje | Páginas de nivel de servicio | Páginas de nivel de dispositivo | Páginas de nivel de dispositivo |
| --- | --- | --- | --- |
| Servicio StorSimple Manager |Panel del servicio |Panel del dispositivo | |
| Dispositivos → |Supervisión | | |
| Catálogo de copias de seguridad |Contenedores de volúmenes→ |Volúmenes | |
| Configurar (servicio) |Directivas de copia de seguridad | | |
| Trabajos |Configurar (dispositivo) | | |
| Alertas |Mantenimiento | | |

![Vídeo disponible](./media/storsimple-manager-service-administration/Video_icon.png)**Vídeo disponible**

Haga clic en un vídeo que le guía a través de la interfaz de usuario de servicio de StorSimple Manager hello, toowatch [aquí](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>Administrar el dispositivo StorSimple mediante el servicio de Administrador de StorSimple
Hello tabla siguiente muestra un resumen de todas las tareas de administración comunes de Hola y flujos de trabajo complejos que se pueden realizar en hello UI del servicio StorSimple Manager. Estas tareas se organizan en función de las páginas de interfaz de usuario de hello en el que se inician.

Para obtener más información sobre cada flujo de trabajo, haga clic en hello procedimiento adecuado en la tabla de Hola.

#### <a name="storsimple-manager-workflows"></a>Flujos de trabajo del servicio de Administrador de StorSimple
| Si desea toodo esto... | Ir a página de interfaz de usuario de toothis... | Utilice este procedimiento. |
| --- | --- | --- |
| Crear un servicio</br>Eliminar un servicio</br>Obtener la clave de registro del servicio</br>Regenerar la clave de registro del servicio regenerar |Servicio StorSimple Manager |[Implementar un servicio del Administrador de StorSimple](storsimple-manage-service.md) |
| Cambiar la clave de cifrado de datos del servicio de Hola</br>Ver registros de operaciones de Hola |Servicio de Administrador de StorSimple → Panel |[Usar el panel de servicio del Administrador de StorSimple de Hola](storsimple-service-dashboard.md) |
| Desactivación de un dispositivo</br>Eliminar un dispositivo |Servicio de Administrador de StorSimple → Dispositivos |[Desactivar o eliminar un dispositivo](storsimple-deactivate-and-delete-device.md) |
| Obtener información sobre recuperación ante desastres y conmutación por error</br>Dispositivo físico de conmutación por error tooa</br>Dispositivo virtual de conmutación por error tooa</br>Recuperación ante desastres y continuidad empresarial (BCDR) |Servicio de Administrador de StorSimple → Dispositivos |[Conmutación por error y recuperación ante desastres para el dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md) |
| Enumerar copias de seguridad para un volumen</br>Seleccionar un conjunto de copia de seguridad</br>Eliminar un conjunto de copias de seguridad |Servicio de Administrador de StorSimple → Catálogo de copias de seguridad |[Administrar copias de seguridad](storsimple-manage-backup-catalog.md) |
| Clonar un volumen |Servicio de Administrador de StorSimple → Catálogo de copias de seguridad |[Clonar un volumen](storsimple-clone-volume.md) |
| Restaurar un conjunto de copias de seguridad |Servicio de Administrador de StorSimple → Catálogo de copias de seguridad |[Restaurar un conjunto de copias de seguridad](storsimple-restore-from-backup-set.md) |
| Acerca de las cuentas de almacenamiento</br>Agregar una cuenta de almacenamiento</br>Editar una cuenta de almacenamiento</br>Eliminar una cuenta de almacenamiento</br>Rotación de claves de las cuentas de almacenamiento |Servicio de Administrador de StorSimple → Configurar |[Administrar cuentas de almacenamiento](storsimple-manage-storage-accounts.md) |
| Acerca de las plantillas de ancho de banda</br>Agregar una plantilla de ancho de banda</br>Editar una plantilla de ancho de banda</br>Eliminar una plantilla de ancho de banda</br>Usar una plantilla de ancho de banda predeterminada</br>Crear una plantilla de ancho de banda para todo el día que comienza a una hora especificada |Servicio de Administrador de StorSimple → Configurar |[Administrar plantillas de ancho de banda](storsimple-manage-bandwidth-templates.md) |
| Acerca de los registros de control de acceso</br>Crear un registro de control de acceso</br>Editar un registro de control de acceso</br>Eliminar un registro de control de acceso |Servicio de Administrador de StorSimple → Configurar |[Administrar registros de control de acceso](storsimple-manage-acrs.md) |
| Ver detalles del trabajo</br>Cancelar un trabajo |Servicio StorSimple Manager → Trabajos |[Trabajos de administración](storsimple-manage-jobs.md) |
| Recibir notificaciones de alerta</br>Administrar alertas</br>Revisar alertas |Servicio de Administrador de StorSimple → Alertas |[Ver y administrar alertas de StorSimple](storsimple-manage-alerts.md) |
| Ver iniciadores conectados</br>Buscar el número de serie del dispositivo de Hola</br>Buscar el IQN de destino de Hola |Servicio de Administrador de StorSimple → Dispositivos → Panel |[Usar el panel de dispositivo de StorSimple de Hola](storsimple-device-dashboard.md) |
| Gráficos de supervisión de dispositivos |Servicio de Administrador de StorSimple → Dispositivos → Supervisión |[Supervisar su dispositivo StorSimple](storsimple-monitor-device.md) |
| Agregar un contenedor de volúmenes</br>Modificar un contenedor de volúmenes</br>Eliminar un contenedor de volúmenes |Servicio de Administrador de StorSimple → Dispositivos → Contenedores de volúmenes |[Administrar contenedores de volúmenes](storsimple-manage-volume-containers.md) |
| Agregar un volumen</br>Modificar un volumen</br>Desconectar un volumen</br>Eliminar un volumen</br>Supervisar un volumen |Servicio de Administrador de StorSimple → Dispositivos → Contenedores de volúmenes → Volúmenes |[Administrar volúmenes](storsimple-manage-volumes.md) |
| Modificar la configuración del dispositivo</br>Modificar la configuración del tiempo</br>Modificar la configuración de DNS.md</br>Configurar interfaces de red |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Modificar la configuración de dispositivo de su dispositivo StorSimple device](storsimple-modify-device-config.md) |
| Ver la configuración de proxy web |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Configurar el proxy web para el dispositivo](storsimple-configure-web-proxy.md) |
| Modificar la contraseña del administrador de dispositivos</br>Modificar la contraseña de Snapshot Manager de StorSimple |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Cambiar las contraseñas de StorSimple](storsimple-change-passwords.md) |
| Configuración de la administración remota |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Conectarse de forma remota el dispositivo de StorSimple tooyour](storsimple-remote-connect.md) |
| Configurar alertas |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Ver y administrar alertas de StorSimple](storsimple-manage-alerts.md) |
| Configurar CHAP para el dispositivo StorSimple |Servicio de Administrador de StorSimple → Dispositivos → Configurar |[Configurar CHAP para el dispositivo StorSimple](storsimple-configure-chap.md) |
| Agregar una directiva de copia de seguridad</br>Incorporación o modificación de una programación</br>Eliminación de una directiva de copia de seguridad</br>Creación de una copia de seguridad manual</br>Crear una directiva de copia de seguridad personalizada con varios programas y volúmenes |Servicio de Administrador de StorSimple → Dispositivos → Directivas de copia de seguridad |[Administrar directivas de copia de seguridad](storsimple-manage-backup-policies.md) |
| Detener los controladores de dispositivo</br>Reiniciar los controladores de dispositivo</br>Apagar los controladores de dispositivo</br>Restablecer los valores predeterminados del dispositivo toofactory</br>(Lo anterior es solo para dispositivos locales) |Servicio de Administrador de StorSimple → Dispositivos → Mantenimiento |[Administrar controladores de dispositivo StorSimple](storsimple-manage-device-controller.md) |
| Obtener información sobre los componentes de hardware de StorSimple</br>Supervisar el estado del hardware</br>(Lo anterior es solo para dispositivos locales) |Servicio de Administrador de StorSimple → Dispositivos → Mantenimiento |[Supervisar componentes de hardware](storsimple-monitor-hardware-status.md) |
| Crear un paquete de soporte |Servicio de Administrador de StorSimple → Dispositivos → Mantenimiento |[Crear y administrar paquetes de soporte técnico](storsimple-create-manage-support-package.md) |
| Instalación de actualizaciones de software |Servicio de Administrador de StorSimple → Dispositivos → Mantenimiento |[Actualizar su dispositivo](storsimple-update-device.md) |

## <a name="next-steps"></a>Pasos siguientes
Si experimenta problemas con el funcionamiento diario de hello de dispositivo de StorSimple o con cualquiera de sus componentes de hardware, consulte:

* [Solución de problemas de un dispositivo de StorSimple operativo](storsimple-troubleshoot-operational-device.md)
* [Utilizar los LED Indicadores de supervisión de StorSimple](storsimple-monitoring-indicators.md)

Si no se puede resolver problemas de Hola y necesita toocreate una solicitud de servicio, consulte demasiado[póngase en contacto con soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).

