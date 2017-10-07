---
title: "dispositivo de StorSimple aaaDeploy en el Portal de administración pública | Documentos de Microsoft"
description: Describe los pasos de Hola y procedimientos recomendados para implementar dispositivos hello StorSimple Update 1 y el servicio en el portal de Azure Government Hola.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 3fe3648d-e0b6-4928-a2cb-8d3ccc50d62a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/17/2016
ms.author: v-sharos
ms.openlocfilehash: 045c838a28efc92d0f67ae3bab2a7393d1badc12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Implementar el dispositivo de StorSimple local en hello Portal de administración pública
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Información general
Página principal de implementación de dispositivos de tooMicrosoft StorSimple de Azure. Estos tutoriales de implementación aplican toohello StorSimple 8000 Series Update 1 software que se ejecute en hello Portal de administración pública de Azure. Esta serie de tutoriales se describe cómo tooconfigure dispositivo de StorSimple e incluye una lista de comprobación de configuración, requisitos previos de configuración y la configuración detallada pasos.

información Hello en estos tutoriales se supone que ha revisado precauciones de seguridad de hello y desempaquetar, racks y cablear el dispositivo StorSimple. Si aún necesita tooperform las tareas, comience con revisar hello [precauciones de seguridad](storsimple-safety.md). Dependiendo del modelo de dispositivo, a continuación, puede desempaquetar, montaje en bastidor y cable siguiendo las instrucciones de hello en:

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
| Lista de comprobación de la configuración de implementación. |Use esta lista de comprobación toogather y registro información previa tooand durante la implementación de Hola. |
| Requisitos previos de implementación. |Estos validar Hola entorno está listo para la implementación. |
|  | |
| **IMPLEMENTACIÓN PASO A PASO** |Estos pasos es necesario toodeploy dispositivo de StorSimple en producción. |
| Paso 1: Crear un nuevo servicio. |Configure la administración y el almacenamiento en la nube para el dispositivo StorSimple. Omita este paso si tiene un servicio existente para otros dispositivos StorSimple. |
| Paso 2: Obtener la clave de registro del servicio de Hola. |Use esta clave tooregister & conectar el dispositivo StorSimple con el servicio de administración de Hola. |
| Paso 3: Configurar y registrar dispositivo hello mediante Windows PowerShell para StorSimple. |Conectar red de tooyour de dispositivo de Hola y registrarlo con el programa de instalación de un saludo toocomplete Azure mediante servicio de administración de Hola. |
| Paso 4: Completar el programa de instalación mínima del dispositivo </br>Opcional: actualización del dispositivo StorSimple. |Toocomplete de servicio de administración de uso Hola Hola el programa de instalación de dispositivos y habilitar almacenamiento tooprovide. |
| Paso 5: Crear un contenedor de volúmenes. |Crear un contenedor de volúmenes de tooprovision. Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. |
| Paso 6: Crear un volumen. |Aprovisionar volúmenes de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. |
| Paso 7: Montar, inicializar y formatear un volumen.</br>Opcional: configurar MPIO. |Conectar el almacenamiento de iSCSI de toohello servidores proporcionado por dispositivo de Hola. También puede configurar que los servidores pueden tolerar vínculo, red y errores de interfaz de tooensure MPIO. |
| Paso 8: Realizar una copia de seguridad. |Configurar la tooprotect de directiva de copia de seguridad de los datos |
|  | |
| **OTROS PROCEDIMIENTOS** |Puede que tenga los procedimientos de toothese toorefer tal y como se implementa la solución. |
| Configurar una nueva cuenta de almacenamiento para el servicio de Hola. | |
| Utilice la consola serie del dispositivo de toohello tooconnect PuTTY. | |
| Búsqueda y aplicación de actualizaciones | |
| Obtener Hola IQN de un host de Windows Server. | |
| Crear una copia de seguridad manual. | |
| Configurar MPIO | |

## <a name="deployment-configuration-checklist"></a>Lista de comprobación de la configuración de implementación
Hola después de la lista de comprobación de configuración de implementación describe la información de Hola que necesita toocollect antes y después de configurar software hello en el dispositivo StorSimple. Preparar parte de esta información antes de tiempo ayudará a agilizar el proceso de Hola de implementación de dispositivo de StorSimple de hello en su entorno. Use esta lista de comprobación tooalso tome nota detalles de configuración de Hola que implementa el dispositivo.

| Fase | Parámetro | Detalles | Valores |
| --- | --- | --- | --- |
| **Cablear el dispositivo** |Acceso serie |Configuración inicial del dispositivo |Sí/No |
|  | | | |
| **Configurar y registrar el dispositivo** |Configuración de red de Data 0 |Dirección IP de Data 0:</br>Máscara de subred:</br>Puerta de enlace:</br>Servidor DNS principal:</br>Servidor NTP principal:</br>IP de servidor proxy web/FQDN (opcional):</br>Puerto de proxy web: | |
| &nbsp; |Contraseña de administrador de dispositivo |La contraseña debe contener entre 8 y 15 caracteres en minúscula, mayúscula, numéricos y especiales. | |
| &nbsp; |Contraseña para StorSimple Snapshot Manager |La contraseña debe contener entre 14 o 15 caracteres en minúscula, mayúscula, numéricos y especiales. | |
| &nbsp; |Clave de registro del servicio |Esta clave se genera a partir de hello portal de Azure. | |
| &nbsp; |Clave de cifrado de datos de servicio |Esta clave se crea cuando el dispositivo de hello está registrado con el servicio de administración de Hola a través de hello Windows PowerShell para StorSimple. Copie esta clave y guárdela en un lugar seguro, | |
|  | | | |
| **Completar la instalación mínima del dispositivo** |Nombre descriptivo para el dispositivo |Se trata de un nombre descriptivo para el dispositivo de Hola. | |
| &nbsp; |Zona horaria |El dispositivo usará esta zona horaria para todas las operaciones programadas. | |
| &nbsp; |Servidor DNS secundario |Es una configuración obligatoria. | |
| &nbsp; |Interfaz de red: IP fijas del controlador Data 0. |Estas direcciones IP debe ser enrutable toohello Internet.</br>Dirección IP fija del controlador 0:</br>Dirección IP fija del controlador 1: | |
|  | | | |
| **Configuración adicional de la interfaz de red** |Interfaz de red: Data 1</br>Si habilita el iSCSI, no configure Hola puerta de enlace. |Propósito: nube/iSCSI/no se usa</br>Dirección IP:</br>Máscara de subred:</br>Puerta de enlace: | |
| &nbsp; |Interfaz de red: Data 2</br>Si habilita el iSCSI, no configure Hola puerta de enlace. |Propósito: nube/iSCSI/no se usa</br>Dirección IP:</br>Máscara de subred:</br>Puerta de enlace: | |
| &nbsp; |Interfaz de red: Data 3</br>Si habilita el iSCSI, no configure Hola puerta de enlace. |Propósito: nube/iSCSI/no se usa</br>Dirección IP:</br>Máscara de subred:</br>Puerta de enlace: | |
| &nbsp; |Interfaz de red: Data 4</br>Si habilita el iSCSI, no configure Hola puerta de enlace. |Propósito: nube/iSCSI/no se usa</br>Dirección IP:</br>Máscara de subred:</br>Puerta de enlace: | |
| &nbsp; |Interfaz de red: Data 5</br>Si habilita el iSCSI, no configure Hola puerta de enlace. |Propósito: nube/iSCSI/no se usa</br>Dirección IP:</br>Máscara de subred:</br>Puerta de enlace: | |
|  | | | |
| **Crear un contenedor de volúmenes** |Nombre del contenedor de volúmenes: |Nombre de contenedor de Hola | |
| &nbsp; |Cuenta de almacenamiento de Azure: |Almacenamiento cuenta acceso y nombre de clave tooassociate con este contenedor de volúmenes | |
| &nbsp; |Clave de cifrado de almacenamiento en la nube: |Clave de cifrado para el almacenamiento en cada contenedor. | |
|  | | | |
| **Crear un volumen** |Detalles de cada volumen |Nombre del volumen: | |
| &nbsp; |&nbsp; |Tamaño | |
| &nbsp; |&nbsp; |Tipo de uso: | |
| &nbsp; |&nbsp; |Nombre ACR: | |
| &nbsp; |&nbsp; |Directiva de copia de seguridad predeterminada: | |
|  | | | |
| **Montar, inicializar y formatear un volumen** |Detalles de cada servidor host conectando toohello almacenamiento |Nombre de Windows Server: | |
| &nbsp; |&nbsp; |IQN de Windows Server: | |
| &nbsp; |&nbsp; |Nombre de volumen de Windows Server: | |
| &nbsp; |&nbsp; |Letra de unidad o punto de montaje de NTFS: | |

## <a name="deployment-prerequisites"></a>Requisitos previos de implementación
Hola siguientes secciones explica los requisitos previos de configuración de hello para el servicio StorSimple Manager y el dispositivo de StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Para el servicio StorSimple Manager Hola
Antes de comenzar, asegúrese de que:

* Tiene una cuenta Microsoft con credenciales de acceso.
* Tiene una cuenta de almacenamiento de Microsoft Azure con credenciales de acceso.
* Su suscripción de Microsoft Azure está habilitada para el servicio StorSimple Manager Hola. La suscripción se debe adquirir mediante hello [contrato Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Tener acceso a software de emulación de tooterminal, como PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Para dispositivos de hello en el centro de datos de Hola
Antes de configurar el dispositivo de hello, asegúrese de:

* El dispositivo viene completamente desempaquetado, montado en un bastidor y totalmente cableado para alimentación, red y acceso serie, tal como se describe en:
  
  * [Desempaquetado, montaje en bastidor y cableado del dispositivo 8100](storsimple-8100-hardware-installation.md)
  * [Desempaquetado, montaje en bastidor y cableado del dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Para la red de hello en el centro de datos de Hola
Antes de comenzar, asegúrese de que:

* Hello puertos en el firewall de centro de datos son tooallow abierto para el tráfico de iSCSI y nube tal y como se describe en [requisitos de red para el dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>IMPLEMENTACIÓN PASO A PASO
Usar hello siguiendo las instrucciones paso a paso toodeploy el dispositivo StorSimple en el centro de datos de Hola.

## <a name="step-1-create-a-new-service"></a>Paso 1: Crear un nuevo servicio
El servicio de Administrador de StorSimple puede administrar varios dispositivos de StorSimple. Realizar Hola siguiendo los pasos toocreate una nueva instancia del servicio de StorSimple Manager Hola.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio, deberá toocreate al menos una cuenta de almacenamiento después de haber creado correctamente un servicio. Dicha cuenta de almacenamiento se usará al crear un contenedor de volúmenes.
> 
> * Si no ha creado una cuenta de almacenamiento automáticamente, vaya demasiado[configurar una nueva cuenta de almacenamiento para el servicio de hello](#configure-a-new-storage-account-for-the-service) para obtener instrucciones detalladas.
> * Si ha habilitado la creación automática de Hola de una cuenta de almacenamiento, vaya demasiado[paso 2: clave de registro del servicio de Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Paso 2: Obtener la clave de registro del servicio de Hola
Después de hello el servicio StorSimple Manager está en funcionamiento, deberá clave de registro del servicio de tooget Hola. Esta clave es tooregister usado y conectar el servicio de toohello de dispositivos de StorSimple.

Realizar Hola pasos de hello Portal de administración pública.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple
Usar Windows PowerShell para StorSimple toocomplete Hola la instalación inicial de su dispositivo StorSimple como se explica en hello siguiendo el procedimiento. Necesitará toocomplete de software de emulación de terminales toouse este paso. Para obtener más información, consulte [consola serie del dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Paso 4: Completar el programa de instalación mínima del dispositivo 
Para la configuración mínima del dispositivo de hello del dispositivo StorSimple, es necesario:

* Configurar el servidor DNS secundario de Hola.
* Habilitar iSCSI en al menos una interfaz de red.
* Asignar direcciones IP fijas controladores de hello tooboth.

Realizar Hola siguiendo los pasos de configuración mínima del dispositivo de hello Portal gobierno toocomplete Hola.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Paso 5: Crear un contenedor de volúmenes
Un contenedor de volumen tiene cuenta de almacenamiento, el ancho de banda y la configuración de cifrado para todos los volúmenes de hello contenidos en ella. Deberá toocreate un contenedor de volumen para poder empezar a aprovisionar volúmenes en el dispositivo StorSimple.

Realizar pasos de hello Portal gobierno toocreate un contenedor de volúmenes de Hola.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Paso 6: Crear un volumen
Después de crear un contenedor de volumen, puede aprovisionar un volumen de almacenamiento en el dispositivo de StorSimple de Hola para los servidores. Realizar pasos de hello Portal gobierno toocreate un volumen de Hola.

> [!IMPORTANT]
> Azure StorSimple solo puede crear volúmenes con aprovisionamiento fino.  No es posible crear volúmenes total o parcialmente aprovisionados en un sistema de Azure StorSimple.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Paso 7: Montar, inicializar y formatear un volumen
Siga estos pasos en el host de Windows Server.

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

Realizar pasos de hello Portal gobierno toocreate copias de seguridad programadas de Hola.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Puede realizar una copia de seguridad manual en cualquier momento. Para conocer los procedimientos, vaya demasiado[crear una copia de seguridad manual](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurar una nueva cuenta de almacenamiento para el servicio de Hola
Se trata de un paso opcional que necesite tooperform únicamente si no ha habilitado la creación automática de Hola de una cuenta de almacenamiento con el servicio. Una cuenta de almacenamiento de Microsoft Azure es toocreate requiere un contenedor de volúmenes de StorSimple.

Si necesita una cuenta de almacenamiento de Azure en una región distinta de toocreate, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) para obtener instrucciones paso a paso.

Realizar Hola pasos de hello Portal de administración pública en hello **el servicio StorSimple Manager** página.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Usar la consola serie del dispositivo de toohello tooconnect PuTTY
tooconnect tooWindows PowerShell para StorSimple, necesita toouse software de emulación de terminales, como PuTTY. Puede usar PuTTY cuando acceda a los dispositivos de hello directamente a través de la consola serie de Hola o al abrir una sesión de telnet desde un equipo remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Búsqueda y aplicación de actualizaciones
La actualización del dispositivo puede tardar entre varias horas. Realizar Hola siguiendo los pasos tooscan para y aplicar las actualizaciones en el dispositivo.

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

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obtener Hola IQN de un host de Windows Server
Realizar Hola siguiendo los pasos tooget Hola iSCSI nombre completo (IQN) de un host de Windows que ejecuta Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Crear una copia de seguridad manual
Realizar Hola siguiendo los pasos indicados en hello Portal gobierno toocreate a petición copia de seguridad manual de un único volumen en el dispositivo StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Configurar MPIO
E/S de múltiples rutas (MPIO) es una característica opcional y no está instalada de forma predeterminada en Windows Server. Se debe instalar como una característica a través del Administrador del servidor. Para obtener instrucciones de instalación de MPIO, vaya demasiado[configurar MPIO para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).

Para obtener instrucciones de instalación de MPIO para un dispositivo de StorSimple tooa conectado host de Linux, vaya demasiado[configurar MPIO para el host de Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> No se admite MPIO en un dispositivo virtual de StorSimple.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Configure un [dispositivo virtual](storsimple-virtual-device-u2.md).
* Hola de uso [el servicio StorSimple Manager](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage dispositivo StorSimple.

