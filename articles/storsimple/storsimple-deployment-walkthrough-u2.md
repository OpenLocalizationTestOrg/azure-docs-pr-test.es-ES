---
title: "aaaDeploy el dispositivo de StorSimple (actualización 2) | Documentos de Microsoft"
description: "Describe los pasos de Hola y prácticas recomendadas para implementar el servicio y el dispositivo de hello StorSimple Update 2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: 5906cc3c41f03c426905ef91be37852608ae9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a>Implementar el dispositivo StorSimple local (Actualización 2)
> [!div class="op_single_selector"]
> * [Actualización 2 y posteriores ](storsimple-deployment-walkthrough-u2.md)
> * [Actualización 1](storsimple-deployment-walkthrough-u1.md)
> * [Versión: disponibilidad general](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Información general
Página principal de implementación de dispositivos de tooMicrosoft StorSimple de Azure. Estos tutoriales de implementación aplican tooStorSimple 8000 Series Update 2. En esta serie de tutoriales se describe se incluye una lista de comprobación de configuración, requisitos previos de configuración y los pasos de configuración detallados para su dispositivo StorSimple.

información Hello en estos tutoriales se supone que ha revisado precauciones de seguridad de hello y desempaquetar, racks y cablear el dispositivo StorSimple. Si aún necesita tooperform las tareas, comience con revisar hello [precauciones de seguridad](storsimple-safety.md). Siga las instrucciones específicas de hello dispositivo toounpack, montaje en bastidor y cable del dispositivo.

* [Desempaquetado, montaje en bastidor y cableado del 8100](storsimple-8100-hardware-installation.md)
* [Desempaquetado, montaje en bastidor y cableado del 8600](storsimple-8600-hardware-installation.md)

Necesitará privilegios toocomplete Hola el programa de instalación y configuración de proceso del administrador. Se recomienda que revise la lista de comprobación de configuración de hello antes de empezar. proceso de implementación y configuración de Hello puede tardar algunos toocomplete de tiempo.

> [!NOTE]
> información sobre la implementación de Hello StorSimple publicada en el sitio Web de Microsoft Azure Hola aplica tooStorSimple 8000 series solo a los dispositivos. Para obtener información completa acerca de los dispositivos de la serie de hello 7000, vaya a: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Para obtener información de implementación de 7000 serie, vea hello [Guía de inicio rápido de StorSimple System](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Pasos de implementación
Realice estos pasos tooconfigure el dispositivo StorSimple y conéctelo tooyour el servicio StorSimple Manager. Además toohello requiere pasos, hay pasos opcionales y los procedimientos que puede que necesite durante la implementación de Hola. instrucciones de implementación paso a paso de Hello indican cuándo se debe realizar en cada uno de estos pasos opcionales.

| Paso | Description |
| --- | --- |
| **REQUISITOS PREVIOS** |Es necesario toobe completado como preparación para la implementación de las próximas Hola. |
| [Lista de comprobación de la configuración de implementación](#deployment-configuration-checklist) |Use esta lista de comprobación toogather y registro información previa tooand durante la implementación de Hola. |
| [Requisitos previos de implementación](#deployment-prerequisites) |Estos validar Hola entorno está listo para la implementación. |
|  | |
| **IMPLEMENTACIÓN PASO A PASO** |Estos pasos es necesario toodeploy dispositivo de StorSimple en producción. |
| [Paso 1: Crear un nuevo servicio](#step-1-create-a-new-service) |Configure la administración y el almacenamiento en la nube para el dispositivo StorSimple. *Omita este paso si tiene un servicio existente para otros dispositivos StorSimple*. |
| [Paso 2: Obtener la clave de registro del servicio de Hola](#step-2-get-the-service-registration-key) |Use esta clave tooregister & conectar el dispositivo StorSimple con el servicio de administración de Hola. |
| [Paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Conectar red de tooyour de dispositivo de Hola y registrarlo con el programa de instalación de un saludo toocomplete Azure mediante servicio de administración de Hola. |
| [Paso 4: Completar la instalación mínima del dispositivo](#step-4-complete-minimum-device-setup)</br>[Opcional: actualización del dispositivo StorSimple](#scan-for-and-apply-updates) |Toocomplete de servicio de administración de uso Hola Hola el programa de instalación de dispositivos y habilitar almacenamiento tooprovide. |
| [Paso 5: Crear un contenedor de volúmenes](#step-5-create-a-volume-container) |Crear un contenedor de volúmenes de tooprovision. Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. |
| [Paso 6: Crear un volumen](#step-6-create-a-volume) |Aprovisionar volúmenes de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. |
| [Paso 7: Montar, inicializar y formatear un volumen](#step-7-mount-initialize-and-format-a-volume)</br>[Opcional: configurar MPIO](storsimple-configure-mpio-windows-server.md) |Conectar el almacenamiento de iSCSI de toohello servidores proporcionado por dispositivo de Hola. También puede configurar que los servidores pueden tolerar error de vínculo, la red y la interfaz de tooensure MPIO. |
| [Paso 8: Realizar una copia de seguridad](#step-8-take-a-backup) |Configurar la tooprotect de directiva de copia de seguridad de los datos |
|  | |
| **OTROS PROCEDIMIENTOS** |Puede que tenga los procedimientos de toothese toorefer tal y como se implementa la solución. |
| [Configurar una nueva cuenta de almacenamiento para el servicio de Hola](#configure-a-new-storage-account-for-the-service) | |
| [Usar la consola serie del dispositivo de toohello tooconnect PuTTY](#use-putty-to-connect-to-the-device-serial-console) | |
| [Obtener Hola IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host) | |
| [Crear una copia de seguridad manual](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a>Lista de comprobación de la configuración de implementación
Antes de implementar el dispositivo, necesitará software de toocollect información tooconfigure hello en el dispositivo StorSimple. Preparar parte de esta información antes de tiempo ayudará a agilizar el proceso de Hola de implementación de dispositivo de StorSimple de hello en su entorno. Descargue y use este toonote de lista de comprobación profundidad los detalles de configuración de Hola que implementa el dispositivo.

* [Descargar la lista de comprobación de la configuración de implementación de StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Requisitos previos de implementación
Hola siguientes secciones explica los requisitos previos de configuración de hello para el servicio StorSimple Manager y el dispositivo de StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Para el servicio StorSimple Manager Hola
Antes de comenzar, asegúrese de que:

* Tiene una cuenta Microsoft con credenciales de acceso.
* Tiene una cuenta de almacenamiento de Microsoft Azure con credenciales de acceso.
* Su suscripción de Microsoft Azure está habilitada para el servicio StorSimple Manager Hola. La suscripción se debe adquirir mediante hello [contrato Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Tener acceso a software de emulación de tooterminal, como PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Para dispositivos de hello en el centro de datos de Hola
Antes de configurar el dispositivo de hello, asegúrese de que el dispositivo está totalmente desempaquetar, montado en un bastidor y todos los cables de alimentación, red y acceso serie según se describe en:

* [Desempaquetado, montaje en bastidor y cableado del dispositivo 8100](storsimple-8100-hardware-installation.md)
* [Desempaquetado, montaje en bastidor y cableado del dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Para la red de hello en el centro de datos de Hola
Antes de comenzar, asegúrese de que:

* Hello puertos en el firewall de centro de datos son tooallow abierto para el tráfico de iSCSI y nube tal y como se describe en [requisitos de red para el dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>IMPLEMENTACIÓN PASO A PASO
Usar hello siguiendo las instrucciones paso a paso toodeploy el dispositivo StorSimple en el centro de datos de Hola.

## <a name="step-1-create-a-new-service"></a>Paso 1: Crear un nuevo servicio
El servicio de Administrador de StorSimple puede administrar varios dispositivos de StorSimple. Realizar Hola siguiendo los pasos toocreate una nueva instancia del servicio de StorSimple Manager Hola.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio, deberá toocreate al menos una cuenta de almacenamiento después de haber creado correctamente un servicio. Dicha cuenta de almacenamiento se usará al crear un contenedor de volúmenes. 
> 
> * Si no ha creado una cuenta de almacenamiento automáticamente, vaya demasiado[configurar una nueva cuenta de almacenamiento para el servicio de hello](#configure-a-new-storage-account-for-the-service) para obtener instrucciones detalladas. 
> * Si ha habilitado la creación automática de Hola de una cuenta de almacenamiento, vaya demasiado[paso 2: clave de registro del servicio de Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Paso 2: Obtener la clave de registro del servicio de Hola
Después de hello el servicio StorSimple Manager está en funcionamiento, deberá clave de registro del servicio de tooget Hola. Esta clave es tooregister usado y conecte el dispositivo StorSimple con el servicio de Hola.

Realizar Hola pasos de hello Portal de administración.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple
Usar Windows PowerShell para StorSimple toocomplete Hola la instalación inicial de su dispositivo StorSimple como se explica en hello siguiendo el procedimiento. Necesitará toocomplete de software de emulación de terminales toouse este paso. Para obtener más información, consulte [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Paso 4: Completar el programa de instalación mínima del dispositivo 
Para la configuración mínima del dispositivo de hello del dispositivo StorSimple, es necesario: 

* Configurar el servidor DNS secundario de Hola.
* Habilitar iSCSI en al menos una interfaz de red.
* Asignar direcciones IP fijas controladores de hello tooboth.

Realizar Hola siguiendo los pasos de configuración mínima del dispositivo de hello Portal de administración toocomplete Hola.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Paso 5: Crear un contenedor de volúmenes
Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. Deberá toocreate un contenedor de volumen para poder empezar a aprovisionar volúmenes en el dispositivo StorSimple. 

Realizar Hola siguiendo los pasos en el Portal de administración de hello toocreate un contenedor de volúmenes.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Paso 6: Crear un volumen
Después de crear un contenedor de volumen, puede aprovisionar un volumen de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. Realizar Hola siguiendo los pasos en el Portal de administración de hello toocreate un volumen.

> [!IMPORTANT]
> StorSimple Manager puede crear tanto volúmenes con aprovisionamiento fino como completo. Sin embargo, no se pueden crear volúmenes aprovisionados parcialmente. 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Paso 7: Montar, inicializar y formatear un volumen
Hola pasos se realiza en el host de Windows Server. 

> [!IMPORTANT]
> * Hola alta disponibilidad de la solución de StorSimple, recomendamos que configure MPIO en su tooconfiguring anteriores de servidores (opcional) de host iSCSI. Configuración de MPIO en servidores host se asegurará de que los servidores de hello pueden tolerar un vínculo, red o errores de interfaz.
> * Para MPIO y iSCSI instalación y configuración de las instrucciones en el host de Windows Server, vaya demasiado[configurar MPIO para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md). Éstos también incluirá Hola pasos toomount, inicializar y formatear volúmenes de StorSimple.
> * Para MPIO y iSCSI instalación y configuración de las instrucciones en un host Linux, vaya demasiado[configurar MPIO para el host de StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Si decide no tooconfigure MPIO, llevar a cabo Hola siguiendo los pasos toomount, inicializar y dar formato a los volúmenes de StorSimple en un host de Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Paso 8: Realizar una copia de seguridad
Las copias de seguridad proporcionan seguridad para los volúmenes a partir de un momento específico y mejoran la capacidad de recuperación al mismo tiempo que reducen los tiempos de restauración. Puede realizar dos tipos de copia de seguridad en el dispositivo StorSimple: instantáneas locales e instantáneas en la nube. Cada uno de estos tipos de copia de seguridad puede ser **Programada** o **Manual**. 

Realizar Hola siguiendo los pasos en el Portal de administración de hello toocreate una copia de seguridad programada.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Puede realizar una copia de seguridad manual en cualquier momento. Para conocer los procedimientos, vaya demasiado[crear una copia de seguridad manual](#create-a-manual-backup). 

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurar una nueva cuenta de almacenamiento para el servicio de Hola
Se trata de un paso opcional que necesite tooperform únicamente si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio. Una cuenta de almacenamiento de Microsoft Azure es toocreate requiere un contenedor de volúmenes de StorSimple.

Si necesita una cuenta de almacenamiento de Azure en una región distinta de toocreate, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) para obtener instrucciones paso a paso.

Realizar Hola pasos de hello Portal de administración, en hello **el servicio StorSimple Manager** página.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Usar la consola serie del dispositivo de toohello tooconnect PuTTY
tooconnect tooWindows PowerShell para StorSimple, necesita toouse software de emulación de terminales, como PuTTY. Puede usar PuTTY cuando acceda a los dispositivos de hello directamente a través de la consola serie de Hola o al abrir una sesión de telnet desde un equipo remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Búsqueda y aplicación de actualizaciones
La actualización del dispositivo puede tardar entre varias horas. Realizar Hola siguiendo los pasos tooscan para y aplicar las actualizaciones en el dispositivo.
<!--can take 1-4 hours--> 

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate el dispositivo
1. En el dispositivo de hello **inicio rápido** página, haga clic en **dispositivos**. Seleccione el dispositivo físico de hello, haga clic en **mantenimiento** y, a continuación, haga clic en **examinar actualizaciones**.  
2. Se crea un tooscan de trabajo si hay actualizaciones disponibles. Si hay actualizaciones disponibles, Hola **examinar actualizaciones** cambia demasiado**instalar actualizaciones**. Haga clic en **Instalar actualizaciones**. 
3. Se creará un trabajo de actualización. Supervisar el estado de saludo de la actualización desplazándose demasiado**trabajos**.
   
   > [!NOTE]
   > Cuando se inicia el trabajo de actualización de hello, inmediatamente muestra el estado de hello como 50 por ciento. estado de Hello cambia por ciento too100 solo después de trabajo de actualización de hello esté completando. No hay ningún estado en tiempo real para el proceso de actualización de Hola.
   > 
   > 
4. Una vez se actualizó correctamente el dispositivo de hello, habilitar interfaces de red Data 2 y Data 3 si éstos se han deshabilitado.

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obtener Hola IQN de un host de Windows Server
Realizar Hola siguiendo los pasos tooget Hola iSCSI nombre completo (IQN) de un host de Windows que ejecuta Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Crear una copia de seguridad manual
Realizar Hola siguiendo los pasos indicados en hello Portal de administración toocreate a petición copia de seguridad manual de un único volumen en el dispositivo StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>Pasos siguientes
* Configure un [dispositivo virtual](storsimple-virtual-device-u2.md).
* Hola de uso [el servicio StorSimple Manager](storsimple-manager-service-administration.md) toomanage dispositivo StorSimple.

