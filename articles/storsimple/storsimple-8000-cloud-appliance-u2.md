---
title: "aaaStorSimple 3 de actualización de dispositivo en la nube | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate, implementar y administrar un dispositivo StorSimple de nube en una red virtual de Microsoft Azure. (Se aplica tooStorSimple Update 3 y posterior)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Implementación y administración de una instancia de StorSimple Cloud Appliance en Azure (Update 3 y versiones posteriores)

## <a name="overview"></a>Información general

Hola dispositivo de StorSimple 8000 Series en la nube es una capacidad adicional que se incluye con la solución de StorSimple de Microsoft Azure. Hola dispositivo de StorSimple en la nube se ejecuta en una máquina virtual en una red virtual de Microsoft Azure, y puede usarlo tooback seguridad y clonar datos desde los hosts.

Este artículo describe Hola proceso paso a paso toodeploy y administrar un dispositivo StorSimple de nube en Azure. Después de leer este artículo, habrá aprendido lo siguiente:

* Comprender cómo difiere el aparato de nube de hello de dispositivo físico de Hola.
* Ser capaz de toocreate y configurar el dispositivo de nube de Hola.
* Conecte el dispositivo de nube de toohello.
* Obtenga información acerca de cómo toowork con hello en la nube de dispositivo.

Este tutorial aplica tooall Hola aparatos de nube de StorSimple ejecuta Update 3 y versiones posteriores.

#### <a name="cloud-appliance-model-comparison"></a>Comparación de los modelos de dispositivo de nube

Hola dispositivo StorSimple de nube está disponible en dos modelos, una 8010 estándar (anteriormente conocido como Hola 1100) y una prima 8020 (introducida en Update 2). Hello en la tabla siguiente presenta una comparación de dos modelos de Hola.

| Modelo de dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacidad máxima** |30 TB |64 TB |
| **MV de Azure** |Standard_A3 (4 núcleos, 7 GB de memoria)| Standard_DS3 (4 núcleos, 14 GB de memoria)|
| **Disponibilidad en regiones** |Todas las regiones de Azure |Regiones de Azure que admiten Premium Storage y máquinas virtuales de Azure DS3<br></br>Use [esta lista](https://azure.microsoft.com/regions/services/) toosee si **máquinas virtuales > DS-series** y **almacenamiento > el almacenamiento en disco** están disponibles en su región. |
| **Tipo de almacenamiento** |Usa el almacenamiento estándar de Azure para discos locales <br></br> Obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento estándar](../storage/common/storage-create-storage-account.md) |Usa el almacenamiento premium de Azure para discos locales<sup>2</sup> <br></br>Obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md) |
| **Guía de la carga de trabajo** |Recuperación a nivel de elemento de archivos de copias de seguridad |Escenarios de desarrollo y pruebas de la nube <br></br>Baja latencia y cargas de trabajo de rendimiento más elevado<br></br>Dispositivo secundario para recuperación ante desastres |

<sup>1</sup> *anteriormente conocido como Hola 1100*.

<sup>2</sup> *ambos Hola 8010 y 8020 usar almacenamiento de Azure estándar para diferencia Hola Hola en la nube de nivel. solo se encuentra en la capa local de hello en dispositivo hello*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Diferencias de dispositivo de nube de hello de dispositivo físico de Hola

Hola aparato de nube de StorSimple es una versión exclusivamente en software de StorSimple que se ejecuta en un único nodo en una máquina Virtual de Microsoft Azure. dispositivo de nube de Hello es compatible con escenarios de recuperación ante desastres en el que el dispositivo físico no está disponible. aplicación de nube de Hello es adecuado para su uso en la recuperación de nivel de elemento de las copias de seguridad, recuperación ante desastres de local y los escenarios de desarrollo y pruebas de la nube.

#### <a name="differences-from-hello-physical-device"></a>Diferencias de dispositivo físico de Hola

Hello tabla siguiente muestran algunas diferencias clave entre hello de dispositivo de StorSimple en la nube y el dispositivo físico StorSimple Hola.

|  | Dispositivo físico | Dispositivo de nube |
| --- | --- | --- |
| **Ubicación** |Se encuentra en el centro de datos de Hola. |Se ejecuta en Azure. |
| **Interfaces de red** |Tiene seis interfaces de red: de DATA 0 a DATA 5. |Solo tiene una interfaz de red: DATA 0. |
| **Registro** |Registrado durante el paso de configuración inicial de Hola. |Registrado a través de una tarea independiente. |
| **Clave de cifrado de datos de servicio** |Volver a generar en el dispositivo físico de hello y, a continuación, actualizar dispositivo de hello en la nube con una clave nueva de Hola. |No se puede volver a generar de dispositivo de hello en la nube. |
| **Tipos de volúmenes admitidos** |Admite volúmenes conectados localmente y por niveles. |Admite solo volúmenes por niveles. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Requisitos previos para la aplicación de nube de Hola

Hello las secciones siguientes explica los requisitos previos de configuración de hello para el dispositivo de StorSimple en la nube. Antes de implementar una aplicación en la nube, revise las consideraciones de seguridad de hello para el uso de un dispositivo de nube.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Requisitos de Azure

Antes de que aprovisione el dispositivo de nube de hello, necesita hello toomake siguientes preparativos en el entorno de Azure:

* Asegúrese de que tiene un dispositivo físico StorSimple 8000 series (modelo 8100 o 8600) implementado y en ejecución en el centro de datos. Registrar este dispositivo con Hola mismo servicio de administrador de dispositivos de StorSimple que piensa toocreate un dispositivo de StorSimple en la nube para.
* Para el dispositivo de la nube de hello, [configurar una red virtual en Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Si usa Almacenamiento premium, tiene que crear una red virtual en una región de Azure que admita dicho almacenamiento. regiones de almacenamiento Premium de Hello son regiones que corresponden fila toohello para almacenamiento en disco en hello [lista de servicios de Azure por región](https://azure.microsoft.com/regions/services/).
* Se recomienda que realice Hola servidor DNS proporcionada por Azure en lugar de especificar su propio nombre del servidor DNS. Si el nombre del servidor DNS no es válido o si el servidor DNS de hello no tooresolve capaz de las direcciones IP correctamente, se produce un error en la creación de hello de dispositivo de hello en la nube.
* Punto a sitio y sitio a sitio son opcionales, pero no obligatorios. Si lo desea, puede configurar estas opciones para escenarios más avanzados.
* Puede crear [máquinas virtuales de Azure](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (servidores de host) en red virtual de Hola que puede usar los volúmenes de hello expuestos por dispositivo de hello en la nube. Estos servidores deben cumplir Hola según los requisitos:

  * Estar en máquinas virtuales de Windows o Linux con el software iSCSI Initiator instalado.
  * Se ejecuta en hello misma red virtual como dispositivo de hello en la nube.
  * Ser capaz de tooconnect toohello iSCSI destino del dispositivo de nube Hola a través de la dirección IP interna de hello de dispositivo de la nube de Hola.
  * Asegúrese de que haya habilitado la compatibilidad para iSCSI y nube tráfico en hello misma red virtual.

#### <a name="storsimple-requirements"></a>Requisitos de StorSimple

Asegúrese de hello después el servicio de administrador de dispositivos de StorSimple de tooyour de actualizaciones antes de crear un dispositivo de nube:

* Agregar [accedan a los registros de control](storsimple-8000-manage-acrs.md) para máquinas virtuales de Hola que son servidores de host de curso toobe hello para el dispositivo en la nube.
* Use un [cuenta de almacenamiento](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) Hola misma región que el dispositivo de hello en la nube. Las cuentas de almacenamiento en regiones diferentes pueden causar un bajo rendimiento. Puede usar una cuenta estándar o Premium almacenamiento con dispositivo de hello en la nube. Para obtener más información acerca de cómo toocreate una [cuenta de almacenamiento estándar](../storage/common/storage-create-storage-account.md) o un [cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md)
* Usar una cuenta de almacenamiento diferentes para la creación de dispositivo de nube de hello uno utilizado para los datos. Utilizando la misma cuenta de almacenamiento puede causar un bajo rendimiento de Hola.

Asegúrese de que haya Hola siguiente información antes de comenzar:

* Su cuenta del portal de Azure con credenciales de acceso.
* Una copia de la clave de cifrado de datos de servicio de hello de dispositivo físico registrado toohello servicio de administrador de dispositivos de StorSimple.

## <a name="create-and-configure-hello-cloud-appliance"></a>Crear y configurar el dispositivo de hello en la nube

Antes de realizar estos procedimientos, asegúrese de que se ha cumplido hello [requisitos previos para la aplicación de nube de hello](#prerequisites-for-the-cloud-appliance).

Realizar Hola siguiendo los pasos toocreate un dispositivo de StorSimple en la nube.

### <a name="step-1-create-a-cloud-appliance"></a>Paso 1: Creación de un dispositivo de nube

Realizar Hola siguiendo los pasos toocreate Hola dispositivo de StorSimple en la nube.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Si se produce un error en la creación de hello de dispositivo de la nube de hello en este paso, puede que no tenga conectividad toohello Internet. Para obtener más información, consulte demasiado[para solucionar problemas de conectividad de Internet](#troubleshoot-internet-connectivity-errors) al crear una aplicación de nube.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Paso 2: Configurar y registrar el dispositivo de hello en la nube

Antes de iniciar este procedimiento, asegúrese de que tiene una copia de la clave de cifrado de datos del servicio de Hola. la clave de cifrado de datos del servicio de Hola se crea cuando se registra el primer dispositivo físico de StorSimple con hello servicio Administrador de dispositivos de StorSimple. Estaban toosave siguiendo las instrucciones en una ubicación segura. Si no tiene una copia de la clave de cifrado de datos del servicio de hello, debe ponerse en contacto con Microsoft Support para obtener ayuda.

Realizar Hola siguiendo los pasos tooconfigure y registrar su dispositivo de StorSimple en la nube.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Paso 3: Opciones de configuración de dispositivo (opcional) modificar Hola

Hello siguiente sección describen opciones de configuración de dispositivo de hello necesarios para hello de dispositivo de StorSimple en la nube si desea toouse CHAP, Administrador de instantáneas StorSimple o cambiar la contraseña de administrador de dispositivos de Hola.

#### <a name="configure-hello-chap-initiator"></a>Configurar el iniciador CHAP Hola

Este parámetro contiene las credenciales de Hola que su dispositivo en la nube (destino) espera de iniciadores de hello (servidores) que están tratando de volúmenes de hello tooaccess. iniciadores de Hello proporcionan un nombre de usuario y una tooidentify de contraseña CHAP por sí mismos tooyour dispositivo durante la autenticación. Para obtener instrucciones detalladas, vaya demasiado[configurar CHAP para el dispositivo](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurar el destino CHAP Hola

Este parámetro contiene las credenciales de Hola que su dispositivo en la nube que se usa cuando un iniciador habilitado para CHAP solicita la autenticación mutua o bidireccional. El dispositivo en la nube usa un nombre de usuario de CHAP inverso y tooidentify contraseña CHAP inverso propio toohello iniciador durante este proceso de autenticación.

> [!NOTE]
> Los valores de configuración de destino de CHAP son valores globales. Cuando se aplica esta configuración, todos los volúmenes de hello conectan autenticación de toohello en la nube dispositivo use CHAP.

Para obtener instrucciones detalladas, vaya demasiado[configurar CHAP para el dispositivo](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurar la contraseña de administrador de instantáneas StorSimple Hola

Software de administrador de instantáneas StorSimple reside en el host de Windows y permite a los administradores toomanage copias de seguridad del dispositivo de StorSimple en forma de Hola de local y en la nube.

> [!NOTE]
> Para el dispositivo de la nube de hello, el host de Windows es una máquina virtual de Azure.

Al configurar un dispositivo en el Administrador de instantáneas StorSimple Hola, le preguntarán tooprovide Hola tooauthenticate de dirección y la contraseña de la IP del dispositivo StorSimple el dispositivo de almacenamiento. Para obtener instrucciones detalladas, vaya demasiado[contraseña de administrador de instantáneas de StorSimple configurar](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Cambiar contraseña de administrador de dispositivo de Hola

Cuando usas tooaccess de interfaz de Windows PowerShell de Hola Hola aparato de nube, estás tooenter requiere una contraseña de administrador de dispositivos. Para la seguridad de Hola de los datos, debe cambiar esta contraseña para poder usar el dispositivo de hello en la nube. Para obtener instrucciones detalladas, vaya demasiado[Configurar contraseña de administrador](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Conectarse de forma remota toohello dispositivo de nube

Dispositivo de nube tooyour de acceso remoto a través de la interfaz de Windows PowerShell de hello no está habilitado de forma predeterminada. Debe habilitar la administración remota en el dispositivo en la nube de hello en primer lugar, y en hello cliente usa aparato de nube tooaccess Hola.

Hola siguiendo el procedimiento de dos pasos describe cómo tooconnect remotamente tooyour en la nube dispositivo.

### <a name="step-1-configure-remote-management"></a>Paso 1: Configuración de la administración remota

Realizar Hola siguiendo los pasos tooconfigure de administración remota para su dispositivo de StorSimple en la nube.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Paso 2: Obtener acceso remoto a dispositivo de hello en la nube

Después de habilitar la administración remota en el dispositivo de hello en la nube, use tooconnect toohello dispositivo de Windows PowerShell remoting desde otra máquina virtual dentro de hello misma red virtual. Por ejemplo, puede conectarse desde la máquina virtual que ha configurado y usado tooconnect iSCSI de host de Hola. En la mayoría de las implementaciones, se abrirá un punto de conexión público tooaccess su host de máquina virtual que puede utilizar para tener acceso a dispositivo de hello en la nube.

> [!WARNING]
> **Para mayor seguridad, recomendamos encarecidamente que use HTTPS al conectarse a los puntos de conexión de toohello y, a continuación, eliminar los puntos de conexión de hello después de haber completado la sesión remota de PowerShell.**

Debe seguir los procedimientos de hello en [conecta de forma remota el dispositivo de StorSimple tooyour](storsimple-8000-remote-connect.md) tooset el acceso remoto para su dispositivo en la nube.

## <a name="connect-directly-toohello-cloud-appliance"></a>Conéctese directamente toohello dispositivo de nube

También puede conectar directamente toohello dispositivo de nube. tooconnect directamente el dispositivo desde otro equipo fuera de la nube toohello Hola red virtual o el entorno de Microsoft Azure Hola exterior, debe crear extremos adicionales.

Realizar Hola siguiendo los pasos toocreate un extremo público en el dispositivo de hello en la nube.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

Se recomienda que se conecte desde otra máquina virtual dentro de hello mismo virtual porque esta práctica minimiza el número de Hola de extremos públicos de la red virtual de la red. En este caso, conectar la máquina virtual de toohello a través de una sesión de escritorio remoto y, a continuación, configure esa máquina virtual para su uso como lo haría con cualquier otro cliente de Windows en una red local. No es necesario el número de puerto público de hello tooappend porque ya se conoce el puerto de Hola.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Trabajar con hello de dispositivo de StorSimple en la nube

Ahora que ha creado y configurado hello de dispositivo de StorSimple en la nube, está listo toostart trabajar con él. Puede trabajar con contenedores de volúmenes, volúmenes y directivas de copia de seguridad en un dispositivo de nube tal y como haría en un dispositivo físico de StorSimple. Hola única diferencia es que debe asegurarse de que selecciona el dispositivo de nube de hello de la lista de dispositivos de toomake. Consulte demasiado[usar toomanage de servicio de administrador de dispositivos de StorSimple Hola un dispositivo de nube](storsimple-8000-manager-service-administration.md) para conocer los procedimientos paso a paso de hello las tareas de administración distintos para aplicación de nube de Hola.

Hello siguientes secciones describen algunas de las diferencias de hello que encuentre al trabajar con el dispositivo de hello en la nube.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Mantenimiento de StorSimple Cloud Appliance

Dado que es un dispositivo solo de software, mantenimiento de dispositivo de la nube de hello es mínimo cuando compara toomaintenance dispositivo físico de Hola.

No se puede actualizar un dispositivo en la nube. Usar versión más reciente de Hola de software toocreate un nuevo dispositivo en la nube.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Cuentas de almacenamiento para un dispositivo de nube

Las cuentas de almacenamiento se crean para su uso por hello servicio Administrador de dispositivos de StorSimple, por dispositivo de nube de Hola y por dispositivo físico de Hola. Al crear las cuentas de almacenamiento, se recomienda usar un identificador regional nombre descriptivo de Hola. Esto ayuda a asegurarse de que esa región Hola sea coherente a lo largo de todos los componentes de sistema de Hola de. Para un dispositivo en la nube, es importante que todos los componentes de hello están en hello mismos problemas de rendimiento de tooprevent de región.

Para un procedimiento paso a paso, vaya demasiado[agregar una cuenta de almacenamiento](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Desactivación de StorSimple Cloud Appliance

Al desactivar un dispositivo de nube, Hola eliminan Hola VM y los recursos de hello creados en el aprovisionamiento. Después de dispositivo de la nube de hello está desactivada, no se puede restaurar el estado anterior de tooits. Antes de desactivar el dispositivo de nube de hello, realizar toostop seguro o eliminar los clientes y hosts que dependen de él.

La desactivación de un dispositivo de nube genera Hola siguientes acciones:

* se quita el dispositivo de Hello en la nube.
* disco de SO de Hola y discos de datos creados para el dispositivo de nube de Hola se quitan.
* servicio hospedado de Hola y red virtual creados durante el aprovisionamiento se conservan. Si no los utiliza, debe eliminarlos manualmente.
* Instantáneas en la nube creadas para el dispositivo de nube de Hola se conservan.

Para un procedimiento paso a paso, vaya demasiado[desactivar y eliminar el dispositivo de StorSimple](storsimple-8000-deactivate-and-delete-device.md).

Tan pronto como dispositivo de hello en la nube se muestra como desactivado en el módulo de servicio del Administrador de dispositivos de StorSimple de hello, puede eliminar dispositivo de nube de Hola de lista de dispositivos en hello **dispositivos** hoja.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Inicio, detención y reinicio de un dispositivo de nube
A diferencia de dispositivo físico de StorSimple de hello, no hay ningún energía o apagado toopush de botón en una aplicación de nube de StorSimple. Sin embargo, puede haber ocasiones donde necesita toostop y reinicie el dispositivo de hello en la nube.

Hola la manera más fácil para toostart, detenga y reinicie que está en un dispositivo de nube a través de la hoja de servicio de máquinas virtuales de Hola. Servicio de máquina Virtual de hello go. En la lista Hola de máquinas virtuales, identificar dispositivo Hola VM de nube de tooyour correspondiente (mismo nombre) y haga clic en nombre de la máquina virtual de Hola. Cuando se examina en la hoja de la máquina virtual, estado de dispositivo de hello en la nube es **ejecutando** ya que se inicia de forma predeterminada después de crearlo. Puede iniciar, detener y reiniciar una máquina virtual en cualquier momento.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Restablecer valores predeterminados de toofactory
Si decide que desea toostart sobre con su dispositivo en la nube, desactivar y eliminar y, a continuación, cree uno nuevo.

## <a name="fail-over-toohello-cloud-appliance"></a>Conmutar por error toohello dispositivo de nube
Recuperación ante desastres (DR) es uno de hello escenarios clave que hello de dispositivo de StorSimple en la nube se diseñó para. En este escenario, Hola dispositivo StorSimple físico o todo centro de datos no estén disponible. Afortunadamente, puede usar una operación de toorestore de dispositivo de nube en una ubicación alternativa. Durante la recuperación ante desastres, contenedores de volúmenes de hello de dispositivo de origen Hola cambiar la propiedad y son toohello transfieren aparato de nube.

requisitos previos de Hola para recuperación ante desastres son:

* dispositivo de nube de Hello creada y configurada.
* Todos los volúmenes de Hola Hola contenedor de volumen están sin conexión.
* contenedor de volúmenes de Hola que conmutar por error, tiene asociada una instantánea en la nube.

> [!NOTE]
> * Cuando se usa un dispositivo de nube como dispositivo secundaria Hola para recuperación ante desastres, tenga en cuenta que Hola 8010 tiene 30 TB de almacenamiento estándar y 8020 tiene 64 TB de almacenamiento Premium. Hola mayor capacidad 8020 nube dispositivo puede ser más adecuada para un escenario de recuperación ante desastres.

Para un procedimiento paso a paso, vaya demasiado[conmutar por dispositivo de nube tooa](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Eliminar dispositivo de hello en la nube
Si ha configurado y usado un dispositivo de StorSimple en la nube pero ahora desea toostop acumular cargas para su uso, debe detener la aplicación de nube de Hola. Dispositivo de nube Hola deteniendo desasigna Hola VM. De esta forma dejan de acumularse cargos en su suscripción. discos de datos y cargas de almacenamiento Hola Hola OS sin embargo continuará.

se cobra toostop Hola a todos, debe eliminar dispositivo de hello en la nube. toodelete Hola copias de seguridad creadas por dispositivo de hello en la nube, puede desactivar o eliminar dispositivos de Hola. Para más información, consulte [Desactivación y eliminación de un dispositivo de StorSimple](storsimple-8000-deactivate-and-delete-device.md).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Solucionar errores de conexión a Internet
Durante la creación de hello de un dispositivo de nube, si no hay ningún toohello de conectividad de Internet, el paso de creación de hello produce un error. errores de conectividad de Internet tootroubleshoot, lleve a cabo Hola pasos de hello portal de Azure:

1. [Creación de una máquina virtual con Windows Server 2012 en Azure](/articles/virtual-machines/windows/quick-create-portal.md). Debe usar esta máquina virtual Hola la misma cuenta de almacenamiento, red virtual y subred porque usada por el dispositivo en la nube. Si hay una existente host de Windows Server en Azure mediante Hola la misma cuenta de almacenamiento y red virtual, subred, también se puede utilizar conectividad a Internet tootroubleshoot Hola.
2. Registro remoto en máquina virtual de hello creado en hello anterior paso.
3. Abra una ventana de comandos dentro de la máquina virtual de hello (Win + R y, después, escriba `cmd`).
4. Ejecute hello después cmd en el símbolo del sistema de Hola.

    `nslookup windows.net`
5. Si `nslookup` se produce un error, a continuación, error de conectividad de Internet está impidiendo que el dispositivo de nube de hello al registrar el servicio de administrador de dispositivos de StorSimple toohello.
6. Realizar cambios de hello necesario tooyour tooensure de red virtual que Hola aparato de nube es capaz de tooaccess sitios de Azure como _windows.net_.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar toomanage de servicio de administrador de dispositivos de StorSimple Hola un dispositivo de nube](storsimple-8000-manager-service-administration.md).
* Comprender cómo demasiado[restaurar un volumen de StorSimple a partir de un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).
