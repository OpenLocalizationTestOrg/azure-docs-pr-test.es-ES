---
title: "dispositivo de la serie StorSimple 8000 aaaDeploy en el portal de administración pública | Documentos de Microsoft"
description: Describe los pasos de Hola y procedimientos recomendados para implementar hello de dispositivo de la serie StorSimple 8000 ejecuta Update 3 y versiones posteriores y hello atender de hello portal de Azure Government.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: ea643cd59dcdf17482268d14c1348a3b5fb098b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Implementar el dispositivo de StorSimple local en el portal de administración pública Hola

## <a name="overview"></a>Información general
Página principal de implementación de dispositivos de tooMicrosoft StorSimple de Azure. Estos tutoriales de implementación aplican software toohello StorSimple 8000 Series de ejecución Update 3 o versiones posteriores en hello portal de Azure Government. En esta serie de tutoriales se describe se incluye una lista de comprobación de configuración, una lista los requisitos previos de configuración y los pasos de configuración detallados para su dispositivo StorSimple.

información Hello en estos tutoriales se supone que ha revisado precauciones de seguridad de hello y desempaquetar, racks y cablear el dispositivo StorSimple. Si aún necesita tooperform las tareas, comience con revisar hello [precauciones de seguridad](storsimple-safety.md). Siga instrucciones específico del dispositivo de hello toounpack, montaje en bastidor y cable del dispositivo.

* [Desempaquetado, montaje en bastidor y cableado del 8100](storsimple-8100-hardware-installation.md)
* [Desempaquetado, montaje en bastidor y cableado del 8600](storsimple-8600-hardware-installation.md)

Necesitará privilegios toocomplete Hola el programa de instalación y configuración de proceso del administrador. Se recomienda que revise la lista de comprobación de configuración de hello antes de empezar. proceso de implementación y configuración de Hello puede tardar algunos toocomplete de tiempo.

> [!NOTE]
> información sobre la implementación de Hello StorSimple publicada en el sitio Web de Microsoft Azure Hola aplica tooStorSimple 8000 series solo a los dispositivos. Para obtener información completa acerca de los dispositivos de la serie de hello 7000, vaya a: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Para obtener información de implementación de 7000 serie, vea hello [Guía de inicio rápido de StorSimple System](http://onlinehelp.storsimple.com/111_Appliance/).


## <a name="deployment-steps"></a>Pasos de implementación
Realice estos pasos tooconfigure el dispositivo StorSimple y conéctelo tooyour servicio de administrador de dispositivos de StorSimple. Además toohello requiere pasos, hay pasos opcionales y los procedimientos que puede necesitar toocomplete durante la implementación de Hola. instrucciones de implementación paso a paso de Hello indican cuándo se debe realizar en cada uno de estos pasos opcionales.

| Paso | Description |
| --- | --- |
| **REQUISITOS PREVIOS** |Es necesario toobe completado como preparación para la implementación de las próximas Hola. |
| [Lista de comprobación de la configuración de implementación](#deployment-configuration-checklist) |Use esta lista de comprobación toogather y registro información previa tooand durante la implementación de Hola. |
| [Requisitos previos de implementación](#deployment-prerequisites) |Estos validar ese Hola entorno está listo para la implementación. |
|  | |
| **IMPLEMENTACIÓN PASO A PASO** |Estos pasos es necesario toodeploy dispositivo de StorSimple en producción. |
| [Paso 1: Crear un nuevo servicio](#step-1-create-a-new-service) |Configure la administración y el almacenamiento en la nube para el dispositivo StorSimple. *Omita este paso si tiene un servicio existente para otros dispositivos StorSimple*. |
| [Paso 2: Obtener la clave de registro del servicio de Hola](#step-2-get-the-service-registration-key) |Use esta clave tooregister y conecte el dispositivo StorSimple con el servicio de administración de Hola. |
| [Paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Conectar red de tooyour de dispositivo de Hola y registrarlo con el programa de instalación de un saludo toocomplete Azure mediante servicio de administración de Hola. |
| [Paso 4: Completar el programa de instalación mínima del dispositivo de Hola](#step-4-complete-minimum-device-setup) </br>Opcional: actualización del dispositivo StorSimple. |Toocomplete de servicio de administración de uso Hola Hola el programa de instalación de dispositivos y habilitar almacenamiento tooprovide. |
| [Paso 5: Crear un contenedor de volúmenes](#step-5-create-a-volume-container) |Crear un contenedor de volúmenes de tooprovision. Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. |
| [Paso 6: Crear un volumen](#step-6-create-a-volume) |Aprovisionar volúmenes de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. |
| [Paso 7: Montar, inicializar y formatear un volumen](#step-7-mount-initialize-and-format-a-volume) </br>Opcional: configurar MPIO. |Conectar el almacenamiento de iSCSI de toohello servidores proporcionado por dispositivo de Hola. Opcionalmente, configure tooensure MPIO que los servidores pueden tolerar vínculo, red y errores de interfaz. |
| [Paso 8: Realizar una copia de seguridad](#step-8-take-a-backup) |Configurar la tooprotect de directiva de copia de seguridad de los datos |
|  | |
| **OTROS PROCEDIMIENTOS** |Puede que tenga los procedimientos de toothese toorefer tal y como se implementa la solución. |
| [Configurar una nueva cuenta de almacenamiento para el servicio de Hola](#configure-a-new-storage-account-for-the-service) | |
| [Usar la consola serie del dispositivo de toohello tooconnect PuTTY](#use-putty-to-connect-to-the-device-serial-console) | |
| [Búsqueda y aplicación de actualizaciones](#scan-for-and-apply-updates) | |
| [Obtener Hola IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host) | |
| [Crear una copia de seguridad manual](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>Lista de comprobación de la configuración de implementación
Antes de implementar el dispositivo StorSimple, necesitará software de toocollect información tooconfigure hello en el dispositivo. Preparar parte de esta información antes de tiempo ayudará a agilizar el proceso de Hola de implementación de dispositivo de StorSimple de hello en su entorno. Descargue y use este detalles de la configuración de la lista de comprobación toonote Hola que implementa el dispositivo.

[Descargar la lista de comprobación de la configuración de implementación de StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Requisitos previos de implementación
Hello las secciones siguientes explica los requisitos previos de configuración de hello para el servicio de administrador de dispositivos de StorSimple y el dispositivo de StorSimple.

### <a name="for-hello-storsimple-device-manager-service"></a>Para hello servicio Administrador de dispositivos de StorSimple
Antes de comenzar, asegúrese de que:

* Tiene una cuenta Microsoft con credenciales de acceso.
* Tiene una cuenta de almacenamiento de Microsoft Azure con credenciales de acceso.
* Su suscripción de Microsoft Azure está habilitada para hello servicio Administrador de dispositivos de StorSimple. La suscripción se debe adquirir mediante hello [contrato Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Tener acceso a software de emulación de tooterminal, como PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Para dispositivos de hello en el centro de datos de Hola
Antes de configurar el dispositivo de hello, asegúrese de:

* El dispositivo viene completamente desempaquetado, montado en un bastidor y totalmente cableado para alimentación, red y acceso serie, tal como se describe en:
  
  * [Desempaquetado, montaje en bastidor y cableado del dispositivo 8100](storsimple-8100-hardware-installation.md)
  * [Desempaquetado, montaje en bastidor y cableado del dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Para la red de hello en el centro de datos de Hola
Antes de comenzar, asegúrese de que:

* Hello puertos en el firewall de centro de datos son tooallow abierto para el tráfico de iSCSI y nube tal y como se describe en [requisitos de red para el dispositivo StorSimple](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>IMPLEMENTACIÓN PASO A PASO
Usar hello siguiendo las instrucciones paso a paso toodeploy el dispositivo StorSimple en el centro de datos de Hola.

## <a name="step-1-create-a-new-service"></a>Paso 1: Crear un nuevo servicio
El servicio de Administrador de dispositivos de StorSimple puede administrar varios dispositivos StorSimple. Realizar Hola siguiendo los pasos toocreate una nueva instancia de hello servicio Administrador de dispositivos de StorSimple.

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> Si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio, deberá toocreate al menos una cuenta de almacenamiento después de haber creado correctamente un servicio. Dicha cuenta de almacenamiento se usará al crear un contenedor de volúmenes.
> 
> * Si no ha creado una cuenta de almacenamiento automáticamente, vaya demasiado[configurar una nueva cuenta de almacenamiento para el servicio de hello](#configure-a-new-storage-account-for-the-service) para obtener instrucciones detalladas.
> * Si ha habilitado la creación automática de Hola de una cuenta de almacenamiento, vaya demasiado[paso 2: clave de registro del servicio de Get hello](#step-2-get-the-service-registration-key).


## <a name="step-2-get-hello-service-registration-key"></a>Paso 2: Obtener la clave de registro del servicio de Hola
Después de hello servicio Administrador de dispositivos de StorSimple está en funcionamiento, deberá clave de registro del servicio de tooget Hola. Esta clave es tooregister usado y conectar el servicio de toohello de dispositivos de StorSimple.

Realizar Hola siguiendo los pasos en el portal de administración pública de Hola.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple
Usar Windows PowerShell para StorSimple toocomplete Hola la instalación inicial de su dispositivo StorSimple como se explica en hello siguiendo el procedimiento. Necesitará toocomplete de software de emulación de terminales toouse este paso. Para obtener más información, consulte [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Paso 4: Completar el programa de instalación mínima del dispositivo 
Para la configuración mínima del dispositivo de hello del dispositivo StorSimple, es necesario:

* Proporcione un nombre descriptivo para el dispositivo.
* Establecer zona horaria del dispositivo Hola.
* Asignar direcciones IP fijas controladores de hello tooboth.

Realizar Hola siguiendo los pasos de configuración mínima del dispositivo de hello Azure Government toocomplete portal Hola.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>Paso 5: Crear un contenedor de volúmenes
Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. Deberá toocreate un contenedor de volumen para poder empezar a aprovisionar volúmenes en el dispositivo StorSimple.

Realizar pasos de hello gobierno portal toocreate un contenedor de volúmenes de Hola.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Paso 6: Crear un volumen
Después de crear un contenedor de volumen, puede aprovisionar un volumen de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. Realizar pasos de hello gobierno portal toocreate un volumen de Hola.

> [!IMPORTANT]
> StorSimple Device Manager solo puede crear volúmenes con aprovisionamiento fino.  Sin embargo, no se pueden crear volúmenes aprovisionados parcialmente.

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Paso 7: Montar, inicializar y formatear un volumen
Siga estos pasos en el host de Windows Server.

> [!IMPORTANT]
> * Hola alta disponibilidad de la solución de StorSimple, recomendamos que configure MPIO en su tooconfiguring anteriores de servidores (opcional) de host iSCSI. Configuración de MPIO en servidores host se asegurará de que los servidores de hello pueden tolerar un vínculo, red o errores de interfaz.
> * Para MPIO y iSCSI instalación y configuración de las instrucciones en el host de Windows Server, vaya demasiado[configurar MPIO para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md). Éstos también incluirá Hola pasos toomount, inicializar y formatear volúmenes de StorSimple.
> * Para MPIO y iSCSI instalación y configuración de las instrucciones en un host Linux, vaya demasiado[configurar MPIO para el host de StorSimple Linux](storsimple-configure-mpio-on-linux.md)

Si decide no tooconfigure MPIO, llevar a cabo Hola siguiendo los pasos toomount, inicializar y dar formato a los volúmenes de StorSimple en un host de Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Paso 8: Realizar una copia de seguridad
Las copias de seguridad proporcionan seguridad para los volúmenes a partir de un momento específico y mejoran la capacidad de recuperación al mismo tiempo que reducen los tiempos de restauración. Puede realizar dos tipos de copia de seguridad en el dispositivo StorSimple: instantáneas locales e instantáneas en la nube. Cada uno de estos tipos de copia de seguridad puede ser **Programada** o **Manual**.

Realizar pasos de hello gobierno portal toocreate copias de seguridad programadas de Hola.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

Puede realizar una copia de seguridad manual en cualquier momento. Para conocer los procedimientos, vaya demasiado[crear una copia de seguridad manual](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurar una nueva cuenta de almacenamiento para el servicio de Hola
Se trata de un paso opcional que necesite tooperform únicamente si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio. Una cuenta de almacenamiento de Microsoft Azure es toocreate requiere un contenedor de volúmenes de StorSimple.

Si necesita una cuenta de almacenamiento de Azure en una región distinta de toocreate, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) para obtener instrucciones paso a paso.

Realizar Hola pasos descritos en el portal de administración pública de hello, en hello **servicio de administrador de dispositivos de StorSimple** página.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Usar la consola serie del dispositivo de toohello tooconnect PuTTY
tooconnect tooWindows PowerShell para StorSimple, necesita toouse software de emulación de terminales, como PuTTY. Puede usar PuTTY cuando acceda a los dispositivos de hello directamente a través de la consola serie de Hola o al abrir una sesión de telnet desde un equipo remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Búsqueda y aplicación de actualizaciones
La actualización del dispositivo puede tardar entre varias horas. Para obtener pasos detallados acerca de cómo tooinstall Hola actualización más reciente, vaya demasiado[instalar actualización 4](storsimple-8000-install-update-4.md).

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obtener Hola IQN de un host de Windows Server
Realizar Hola siguiendo los pasos tooget Hola iSCSI nombre completo (IQN) de un host de Windows que ejecuta Windows Server® 2012.

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Crear una copia de seguridad manual
Realizar Hola siguiendo los pasos indicados en hello gobierno portal toocreate una copia de seguridad manual a petición para un solo volumen en el dispositivo StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Pasos siguientes
* Configure un [dispositivo virtual](storsimple-8000-cloud-appliance-u2.md).
* Hola de uso [servicio de administrador de dispositivos de StorSimple](storsimple-8000-manager-service-administration.md) toomanage el dispositivo StorSimple.

