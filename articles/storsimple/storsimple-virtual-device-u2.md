---
title: dispositivo virtual aaaStorSimple Update 2 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate, implementar y administrar un dispositivo StorSimple virtual en una red virtual de Microsoft Azure. (Se aplica tooStorSimple Update 2)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Implementar y administrar un dispositivo virtual StorSimple en Azure
## <a name="overview"></a>Información general
dispositivo virtual de Hello StorSimple 8000 series es una capacidad adicional que se incluye con la solución de StorSimple de Microsoft Azure. dispositivo virtual StorSimple de Hola se ejecuta en una máquina virtual en una red virtual de Microsoft Azure, y puede usarlo tooback seguridad y clonar datos desde los hosts. Este tutorial se describe cómo toodeploy y administrar un dispositivo virtual en Azure y es aplicable tooall dispositivos virtuales Hola ejecutando la versión de software Update 2 e inferior.

#### <a name="virtual-device-model-comparison"></a>Comparación del modelo de dispositivo virtual
Hola StorSimple dispositivo virtual está disponible en dos modelos, una 8010 estándar (anteriormente conocido como Hola 1100) y una prima 8020 (introducida en Update 2). Una comparación de dos modelos de Hola se tabulan a continuación.

| Modelo de dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacidad máxima** |30 TB |64 TB |
| **MV de Azure** |Standard_A3 (4 núcleos, 7 GB de memoria) |Standard_DS3 (4 núcleos, 14 GB de memoria) |
| **Compatibilidad de versión** |Ejecuta las versiones previas a la actualización 2 o posterior |Ejecuta las versiones de la actualización 2 o posterior |
| **Disponibilidad en regiones** |Todas las regiones de Azure |Todas las regiones de Azure que admiten Premium Storage y máquinas virtuales de Azure DS3<br></br> Use [esta lista](https://azure.microsoft.com/en-us/regions/services) toosee si *máquinas virtuales > DS-series* y *almacenamiento > el almacenamiento en disco* están disponibles en su región. |
| **Tipo de almacenamiento** |Usa el almacenamiento estándar de Azure para discos locales <br></br> Obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento estándar](../storage/common/storage-create-storage-account.md) |Usa el almacenamiento premium de Azure para discos locales<sup>2</sup> <br></br>Obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md) |
| **Guía de la carga de trabajo** |Recuperación a nivel de elemento de archivos de copias de seguridad |Escenarios de desarrollo y pruebas en la nube, baja latencia, mayores cargas de trabajo de rendimiento  <br></br>Dispositivo secundario para recuperación ante desastres |

<sup>1</sup> *anteriormente conocido como Hola 1100*.

<sup>2</sup> *ambos Hola 8010 y 8020 usar almacenamiento de Azure estándar para diferencia Hola Hola en la nube de nivel. solo se encuentra en la capa local de hello en dispositivo hello*.

En este artículo se describe Hola proceso paso a paso de la implementación de un dispositivo virtual StorSimple de Azure. Después de leer este artículo, habrá aprendido lo siguiente:

* Comprender cómo difiere el dispositivo virtual hello de dispositivo físico de Hola.
* Ser capaz de toocreate y configure el dispositivo virtual Hola.
* Conecte el dispositivo virtual toohello.
* Obtenga información acerca de cómo toowork con dispositivo virtual Hola.

Este tutorial aplica tooall Hola dispositivos virtuales de StorSimple ejecutan la actualización 2 y versiones posteriores.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Diferencias de dispositivo virtual de hello de dispositivo físico de Hola
dispositivo virtual StorSimple de Hello es una versión exclusivamente en software de StorSimple que se ejecuta en un único nodo en una máquina Virtual de Microsoft Azure. Hola dispositivo virtual admite la recuperación ante desastres en el que el dispositivo físico no está disponible y es adecuado para su uso en la recuperación de nivel de elemento desde copias de seguridad, recuperación ante desastres, local dev en la nube y escenarios de prueba.

#### <a name="differences-from-hello-physical-device"></a>Diferencias de dispositivo físico de Hola
Hello tabla siguiente muestran algunas diferencias clave entre el dispositivo virtual StorSimple Hola y el dispositivo físico StorSimple Hola.

|  | Dispositivo físico | Dispositivo virtual |
| --- | --- | --- |
| **Ubicación** |Se encuentra en el centro de datos de Hola. |Se ejecuta en Azure. |
| **Interfaces de red** |Tiene seis interfaces de red: de DATA 0 a DATA 5. |Solo tiene una interfaz de red: DATA 0. |
| **Registro** |Registrado durante el paso de configuración de Hola. |Registrado a través de una tarea independiente. |
| **Clave de cifrado de datos de servicio** |Volver a generar en el dispositivo físico de hello y, a continuación, actualizar dispositivo virtual Hola con una clave nueva Hola. |No se puede volver a generar de dispositivo virtual Hola. |

## <a name="prerequisites-for-hello-virtual-device"></a>Requisitos previos para el dispositivo virtual Hola
Hello las secciones siguientes explican los requisitos previos de configuración de hello para el dispositivo virtual StorSimple. Toodeploying anterior un dispositivo virtual, revise hello [consideraciones de seguridad para usar un dispositivo virtual](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Requisitos de Azure
Antes de aprovisionar dispositivo virtual hello, necesita hello toomake siguientes preparativos en el entorno de Azure:

* Dispositivo virtual de hello, [configurar una red virtual en Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Si usa Almacenamiento premium, tiene que crear una red virtual en una región de Azure que admita dicho almacenamiento. regiones de almacenamiento Premium de Hello son regiones que corresponden fila toohello para *el almacenamiento en disco* en la lista de Hola de [servicios de Azure por región](https://azure.microsoft.com/en-us/regions/services).
* Es aconsejable toouse Hola servidor DNS proporcionada por Azure en lugar de especificar su propio nombre del servidor DNS. Si el nombre del servidor DNS no es válido o si el servidor DNS de hello no tooresolve capaz de las direcciones IP correctamente, se producirá un error en la creación de hello de dispositivo virtual Hola.
* Punto a sitio y sitio a sitio son opcionales, pero no obligatorios. Si lo desea, puede configurar estas opciones para escenarios más avanzados.
* Puede crear [máquinas virtuales de Azure](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (servidores de host) en red virtual de Hola que puede usar los volúmenes de hello expuestos por el dispositivo virtual Hola. Estos servidores deben cumplir Hola según los requisitos:                             

  * Estar en máquinas virtuales de Windows o Linux con el software iSCSI Initiator instalado.
  * Se ejecuta en hello misma red virtual como dispositivo virtual Hola.
  * Ser capaz de tooconnect toohello iSCSI destino del dispositivo virtual de Hola a través de la dirección IP interna de hello de dispositivo virtual Hola.
* Asegúrese de que haya habilitado la compatibilidad para iSCSI y nube tráfico en hello misma red virtual.

#### <a name="storsimple-requirements"></a>Requisitos de StorSimple
Asegúrese de hello después de servicio de StorSimple de Azure de tooyour de actualizaciones antes de crear un dispositivo virtual:

* Agregar [accedan a los registros de control](storsimple-manage-acrs.md) para hello las máquinas virtuales que se van toobe servidores de host para el dispositivo virtual.
* Use un [cuenta de almacenamiento](storsimple-manage-storage-accounts.md#add-a-storage-account) Hola misma región que el dispositivo virtual Hola. Las cuentas de almacenamiento en regiones diferentes pueden causar un bajo rendimiento. Puede usar una cuenta estándar o Premium almacenamiento con el dispositivo virtual Hola. Para obtener más información acerca de cómo toocreate una [cuenta de almacenamiento estándar](../storage/common/storage-create-storage-account.md) o un [cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md)
* Usar una cuenta de almacenamiento diferentes para la creación de dispositivo virtual de hello uno utilizado para los datos. Utilizando la misma cuenta de almacenamiento puede causar un bajo rendimiento de Hola.

Asegúrese de que haya Hola siguiente información antes de comenzar:

* Cuenta del Portal de Azure clásico con credenciales de acceso.
* Una copia de la clave de cifrado de datos de servicio de hello de dispositivo físico.

## <a name="create-and-configure-hello-virtual-device"></a>Crear y configurar el dispositivo virtual Hola
Antes de realizar estos procedimientos, asegúrese de que se ha cumplido hello [requisitos previos para el dispositivo virtual hello](#prerequisites-for-the-virtual-device).

Una vez haya creado una red virtual, configurar un servicio de StorSimple Manager y registrado el dispositivo StorSimple físico con el servicio de hello, puede usar hello siguiendo los pasos toocreate y configurar un dispositivo virtual StorSimple.

### <a name="step-1-create-a-virtual-device"></a>Paso 1: Creación de un dispositivo virtual
Realizar Hola siguiendo los pasos toocreate Hola virtual el dispositivo StorSimple.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Si se produce un error en la creación de hello de dispositivo virtual de hello en este paso, puede que no tenga conectividad toohello Internet. Para obtener más información, consulte demasiado[para solucionar problemas de conectividad de Internet](#troubleshoot-internet-connectivity-errors) al crear un dispositivo virtual.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Paso 2: Configurar y registrar un dispositivo virtual Hola
Antes de iniciar este procedimiento, asegúrese de que tiene una copia de la clave de cifrado de datos del servicio de Hola. Hello clave de cifrado de datos de servicio se creó al configurar el primer dispositivo de StorSimple y estaban toosave siguiendo las instrucciones en una ubicación segura. Si no tiene una copia de la clave de cifrado de datos del servicio de hello, debe ponerse en contacto con Microsoft Support para obtener ayuda.

Realizar Hola siguiendo los pasos tooconfigure y registrar su dispositivo virtual StorSimple.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Paso 3: Opciones de configuración de dispositivo (opcional) modificar Hola
Hello siguiente sección describen opciones de configuración de dispositivo de hello necesarios para el dispositivo virtual StorSimple Hola si desea toouse CHAP, Administrador de instantáneas StorSimple o cambiar la contraseña de administrador de dispositivos de Hola.

#### <a name="configure-hello-chap-initiator"></a>Configurar el iniciador CHAP Hola
Este parámetro contiene las credenciales de Hola que el dispositivo virtual (destino) espera de iniciadores de hello (servidores) que están tratando de volúmenes de hello tooaccess. Hola iniciadores proporcionarán un nombre de usuario y una tooidentify de contraseña CHAP por sí mismos tooyour dispositivo durante la autenticación. Para obtener instrucciones detalladas, vaya demasiado[configurar CHAP para el dispositivo](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurar el destino CHAP Hola
Este parámetro contiene las credenciales de Hola que el dispositivo virtual que se usa cuando un iniciador habilitado para CHAP solicita la autenticación mutua o bidireccional. El dispositivo virtual usará un nombre de usuario de CHAP inverso y tooidentify contraseña CHAP inverso propio toohello iniciador durante este proceso de autenticación. Tenga en cuenta que los valores de destino de CHAP son valores globales. Cuando se aplican estos últimos, todos los Hola volúmenes conectados toohello almacenamiento virtual dispositivo va a usar la autenticación CHAP. Para obtener instrucciones detalladas, vaya demasiado[configurar CHAP para el dispositivo](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurar la contraseña de administrador de instantáneas StorSimple Hola
Software de administrador de instantáneas StorSimple reside en el host de Windows y permite a los administradores toomanage copias de seguridad del dispositivo de StorSimple en forma de Hola de local y en la nube.

> [!NOTE]
> Dispositivo virtual de hello, el host de Windows es una máquina virtual de Azure.
>
>

Al configurar un dispositivo en el Administrador de instantáneas StorSimple Hola, se le pedirá tooprovide Hola tooauthenticate de dirección y la contraseña de la IP del dispositivo StorSimple el dispositivo de almacenamiento. Para obtener instrucciones detalladas, vaya demasiado[contraseña de administrador de instantáneas de StorSimple configurar](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Cambiar contraseña de administrador de dispositivo de Hola
Cuando se usa tooaccess de interfaz de Windows PowerShell de Hola Hola dispositivo virtual, será necesario tooenter una contraseña de administrador de dispositivos. Por seguridad Hola de los datos, es necesario toochange esta contraseña antes de dispositivo virtual Hola puede utilizarse. Para obtener instrucciones detalladas, vaya demasiado[Configurar contraseña de administrador](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Conectarse de forma remota dispositivos virtuales toohello
Dispositivo virtual de tooyour de acceso remoto a través de la interfaz de Windows PowerShell de hello no está habilitado de forma predeterminada. Necesita tooenable administración remota en el dispositivo virtual hello en primer lugar y, a continuación, habilitarlo en cliente de Hola que será usado tooaccess el dispositivo virtual.

tooconnect de proceso de dos pasos Hola remotamente se detalla a continuación.

### <a name="step-1-configure-remote-management"></a>Paso 1: Configuración de la administración remota
Realizar Hola siguiendo los pasos tooconfigure de administración remota para su dispositivo virtual StorSimple.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Paso 2: Obtener acceso remoto a dispositivo virtual Hola
Después de haber habilitado la administración remota en la página de configuración de dispositivo de StorSimple de hello, puede usar Windows PowerShell remoting tooconnect toohello dispositivo virtual desde otra máquina virtual dentro de hello misma red virtual; Por ejemplo, puede conectarse desde la máquina virtual que ha configurado y usado tooconnect iSCSI de host de Hola. En la mayoría de las implementaciones, ya habrá abierto un punto de conexión público tooaccess su host de máquina virtual que puede utilizar para tener acceso a dispositivo virtual Hola.

> [!WARNING]
> **Para mayor seguridad, recomendamos encarecidamente que use HTTPS al conectarse a los puntos de conexión de toohello y, a continuación, eliminar los puntos de conexión de hello después de haber completado la sesión remota de PowerShell.**
>
>

Debe seguir los procedimientos de hello en [conecta de forma remota el dispositivo de StorSimple tooyour](storsimple-remote-connect.md) tooset el acceso remoto del dispositivo virtual.

## <a name="connect-directly-toohello-virtual-device"></a>Conectar directamente el dispositivo virtual toohello
También puede conectar directamente toohello de dispositivo virtual. Si desea que tooconnect directamente toohello dispositivo virtual desde otro equipo fuera de la red virtual de Hola o entorno de Microsoft Azure Hola exterior, necesita toocreate extremos adicionales tal como se describe en hello siguiendo el procedimiento.

Realizar Hola siguiendo los pasos toocreate un extremo público en el dispositivo virtual Hola.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

Se recomienda que se conecte desde otra máquina virtual dentro de hello mismo virtual porque esta práctica minimiza el número de Hola de extremos públicos de la red virtual de la red. Cuando utiliza este método, que simplemente conecte la máquina virtual de toohello a través de una sesión de escritorio remoto y, a continuación, configure esa máquina virtual para su uso como lo haría con cualquier otro cliente de Windows en una red local. No es necesario el número de puerto público de hello tooappend porque ya se conocerá el puerto de Hola.

## <a name="work-with-hello-storsimple-virtual-device"></a>Trabajar con el dispositivo virtual StorSimple Hola
Ahora que ha creado y configurado el dispositivo virtual StorSimple hello, está listo toostart trabajar con él. Puede trabajar con contenedores de volúmenes, volúmenes y las directivas de copia de seguridad en un dispositivo virtual como haría en un dispositivo físico de StorSimple; Hola única diferencia es que debe asegurarse de que selecciona el dispositivo virtual hello de la lista de dispositivos de toomake. Consulte demasiado[usar hello StorSimple Manager servicio toomanage un dispositivo virtual](storsimple-manager-service-administration.md) para conocer los procedimientos paso a paso de hello las tareas de administración de varios para dispositivo virtual Hola.

Hello siguientes secciones describen algunas de las diferencias de Hola que encontrará al trabajar con el dispositivo virtual Hola.

### <a name="maintain-a-storsimple-virtual-device"></a>Mantenimiento de un dispositivo virtual de StorSimple
Dado que es un dispositivo solo de software, mantenimiento de dispositivo virtual hello es mínimo cuando compara toomaintenance dispositivo físico de Hola. Tener Hola siguientes opciones:

* **Las actualizaciones de software** : puede ver la fecha de hello última actualización de software de hello, junto con los mensajes de estado de actualización. Puede usar hello **buscar actualizaciones** situado en parte inferior de Hola de hello página tooperform un análisis manual si desea toocheck si hay nuevas actualizaciones. Si hay actualizaciones disponibles, haga clic en **instalar actualizaciones** tooinstall. Dado que hay solo una única interfaz de dispositivo virtual de hello, esto significa que habrá una ligera interrupción del servicio cuando se aplican las actualizaciones. dispositivo virtual Hola se apagará y se reinicie (si es necesario) tooapply las actualizaciones que se han liberado. Para un procedimiento paso a paso, vaya demasiado[actualizar el dispositivo](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Paquete de soporte** : puede crear y cargar un toohelp de paquete de soporte técnico de Microsoft Support solucionar problemas con el dispositivo virtual. Para un procedimiento paso a paso, vaya demasiado[crear y administrar un paquete de soporte](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Cuentas de almacenamiento para un dispositivo virtual
Las cuentas de almacenamiento se crean para su uso por el servicio StorSimple Manager hello, dispositivo virtual hello y dispositivo físico de Hola. Al crear las cuentas de almacenamiento, se recomienda que use una región identificador en hello Nombre_descriptivo toohelp asegurarse de esa región Hola sea coherente a lo largo de todos los componentes de sistema de Hola de. Para un dispositivo virtual, es importante que todos los componentes de Hola Hola mismos problemas de rendimiento de tooprevent de región.

Para un procedimiento paso a paso, vaya demasiado[agregar una cuenta de almacenamiento](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Desactivación de un dispositivo virtual de StorSimple
La desactivación de un dispositivo virtual elimina Hola VM y los recursos de hello creados en el aprovisionamiento. Después de dispositivo virtual Hola está desactivada, no se puede restaurar el estado anterior de tooits. Antes de desactivar el dispositivo virtual hello, realizar toostop seguro o eliminar los clientes y hosts que dependen de él.

La desactivación de un dispositivo virtual resultado Hola siguientes acciones:

* se quitó el dispositivo virtual de Hola.
* disco de SO de Hola y discos de datos creados para dispositivo virtual Hola se quitan.
* servicio hospedado de Hola y red virtual creados durante el aprovisionamiento se conservan. Si no los utiliza, debe eliminarlos manualmente.
* Instantáneas en la nube creadas para el dispositivo virtual Hola se conservan.

Para un procedimiento paso a paso, vaya demasiado[desactivar y eliminar el dispositivo de StorSimple](storsimple-deactivate-and-delete-device.md).

Tan pronto como dispositivo virtual Hola se muestra como desactivado en la página del servicio de administrador de StorSimple de hello, puede eliminar el dispositivo virtual Hola de lista de dispositivos en hello **dispositivos** página.

### <a name="start-stop-and-restart-a-virtual-device"></a>Inicio, detención y reinicio de un dispositivo virtual
A diferencia de dispositivo físico de StorSimple de hello, no hay ningún energía o apagado toopush de botón en un dispositivo virtual StorSimple. Sin embargo, puede haber ocasiones donde necesita toostop y reinicie el dispositivo virtual Hola. Por ejemplo, algunas actualizaciones pueden requerir ese Hola que VM puede reinicia el proceso de actualización de toofinish Hola. la manera más fácil de Hola para toostart, detenga y reinicie un dispositivo virtual es toouse Hola consola de administración de máquinas virtuales.

Cuando se examina en la consola de administración de hello, el estado del dispositivo virtual de hello es **ejecutando** ya que se inicia de forma predeterminada después de crearlo. Puede iniciar, detener y reiniciar una máquina virtual en cualquier momento.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Restablecer valores predeterminados de toofactory
Si decide que desea toostart sobre con su dispositivo virtual, basta con desactivarlo y eliminarlo y, a continuación, cree uno nuevo. Al igual que cuando se restablece el dispositivo físico, el nuevo dispositivo virtual no tendrán las actualizaciones instaladas; por lo tanto, asegúrese de toocheck seguro para las actualizaciones antes de usarlo.

## <a name="fail-over-toohello-virtual-device"></a>Conmutar por error toohello de dispositivo virtual
Recuperación ante desastres (DR) es uno de los escenarios de clave de Hola que Hola StorSimple dispositivo virtual se diseñó para. En este escenario, Hola dispositivo StorSimple físico o todo centro de datos podría no estar disponible. Afortunadamente, puede usar las operaciones toorestore dispositivo virtual en una ubicación alternativa. Durante la recuperación ante desastres, contenedores de volúmenes de Hola Hola dispositivo de origen cambia la propiedad y transfieren toohello del dispositivo virtual. Hello requisitos previos de DR son que dispositivo virtual Hola se ha creado y configurado, todos los volúmenes de Hola Hola contenedor de volumen estén sin conexión y contenedor de volúmenes de hello tiene asociada una instantánea en la nube.

> [!NOTE]
> * Cuando se usa un dispositivo virtual como dispositivo secundaria Hola para recuperación ante desastres, tenga en cuenta que Hola 8010 tiene 30 TB de almacenamiento estándar y 8020 tiene 64 TB de almacenamiento Premium. Hola mayor capacidad 8020 dispositivo virtual puede ser más adecuada para un escenario de recuperación ante desastres.
> * No se puede conmutación por error o clonar desde un dispositivo que ejecuta actualizar 2 dispositivos tooa ejecutando 1 de anteriores a la actualización software. Sin embargo puede producir un error en un dispositivo que ejecuta Update 2 tooa dispositivo ejecuta Update 1 (1.1 o 1.2)
>
>

Para un procedimiento paso a paso, vaya demasiado[dispositivo virtual de conmutación por error tooa](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Apague o elimine el dispositivo virtual Hola
Si ha configurado anteriormente y usa un StorSimple virtual dispositivo pero ahora desea toostop acumular cargas para su uso, puede apagar el dispositivo virtual Hola. Apagar el dispositivo virtual hello no elimina su sistema operativo o discos de datos en el almacenamiento. Detiene la acumulación de cargas de su suscripción, pero seguirán cargas de almacenamiento Hola OS y discos de datos.

Si elimina o apagar el dispositivo virtual hello, aparecerá como **Offline** en página de dispositivos de Hola de hello el servicio StorSimple Manager. Puede elegir toodeactivate o eliminar dispositivos de hello si también desea toodelete copias de seguridad de hello creadas por dispositivo virtual Hola. Para más información, consulte [Desactivación y eliminación de un dispositivo de StorSimple](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Solucionar errores de conexión a Internet
Durante la creación de hello de un dispositivo virtual, si no hay ningún toohello de conectividad de Internet, el paso de creación de hello se producirá un error. tootroubleshoot si el error de hello es debido a la conectividad a Internet, realizar Hola pasos de hello portal de Azure clásico:

1. Cree una máquina virtual de Windows Server 2012 en Azure. Debe usar esta máquina virtual Hola la misma cuenta de almacenamiento, red virtual y subred que usa el dispositivo virtual. Si ya tiene un servicio de host de Windows Server en Azure mediante Hola la misma cuenta de almacenamiento, red virtual y subred, también se puede utilizar conectividad a Internet tootroubleshoot Hola.
2. Registro remoto en máquina virtual de hello creado en hello anterior paso.
3. Abra una ventana de comandos dentro de la máquina virtual de hello (Win + R y, después, escriba `cmd`).
4. Ejecute hello después cmd en el símbolo del sistema de Hola.

    `nslookup windows.net`
5. Si `nslookup` se produce un error, a continuación, error de conectividad de Internet impide el dispositivo virtual Hola al registrar el servicio StorSimple Manager toohello.
6. Realizar cambios de hello necesario tooyour tooensure de red virtual que Hola dispositivo virtual es capaz de tooaccess sitios de Azure, como "windows.net".

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar hello StorSimple Manager servicio toomanage un dispositivo virtual](storsimple-manager-service-administration.md).
* Comprender cómo demasiado[restaurar un volumen de StorSimple a partir de un conjunto de copia de seguridad](storsimple-restore-from-backup-set.md).
