---
title: "aaaTest tooAzure de conmutación por error de Site Recovery | Documentos de Microsoft"
description: "Obtenga información acerca de cómo ejecutar una conmutación por error de prueba de tooAzure local"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Probar la conmutación por error tooAzure en Site Recovery



Este artículo proporciona información y las instrucciones para realizar una conmutación por error de prueba o una exploración de recuperación ante desastres de máquinas virtuales y servidores físicos están protegidas con Site Recovery con Azure como sitio de recuperación de Hola.

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Conmutación por error de prueba es ejecutar toovalidate la estrategia de replicación o realizar una exploración de recuperación ante desastres sin pérdida de datos o el tiempo de inactividad. Realizar una conmutación por error de prueba no tiene ningún efecto en la replicación en curso de Hola o en el entorno de producción. La conmutación por error de prueba puede hacerse en una máquina virtual o en un [plan de recuperación](site-recovery-create-recovery-plans.md). Al activar una conmutación por error de prueba, debe prueba de toowhich de red toospecify Hola conectaría máquinas virtuales. Una vez que se desencadena una conmutación por error de prueba, puede seguir el progreso en hello **trabajos** página.  


## <a name="supported-scenarios"></a>Escenarios admitidos
Se admite la conmutación por error en todos los escenarios de implementación distinto de [tooAzure de sitio de VMware heredado](site-recovery-vmware-to-azure-classic-legacy.md). Conmutación por error de prueba tampoco se admite cuando la máquina virtual ha se ha conmutado por error tooAzure.  


## <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
Este procedimiento describe cómo toorun una conmutación por error de prueba para una recuperación del plan. O bien también puede ejecutar la conmutación por error de prueba para un único equipo mediante el uso de la opción adecuada de hello en él.

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Seleccione **Recovery Plans** > *nombreDePlanDeRecuperación*. Haga clic en **Probar conmutación por error**.
1. Seleccione un **punto de recuperación** toofailover a. Puede usar uno de hello siguientes opciones:
    1.  **Procesar más reciente**: esta opción se conmuta todas las máquinas virtuales de hello recuperación plan toohello último punto de recuperación que ya ha sido procesado por el servicio de Site Recovery. Cuando realiza una conmutación por error de prueba de una máquina virtual, también se muestra la marca de tiempo de punto de recuperación procesada más reciente de Hola. Si realiza una conmutación por error de un plan de recuperación, puede ir de máquina virtual de tooindividual y mirar **puntos de recuperación más reciente** icono tooget esta información. A medida que se empleó ningún tiempo tooprocess Hola datos sin procesar, esta opción proporciona una opción de conmutación por error bajo RTO (objetivo de tiempo de recuperación).
    1.  **Más reciente coherente con la aplicación**: esta opción se conmuta todas las máquinas virtuales Hola plan toohello más reciente aplicación coherente recuperación del punto de recuperación que ya ha sido procesado por el servicio de recuperación del sitio. Cuando realiza una conmutación por error de prueba de una máquina virtual, también se muestra la marca de tiempo del último punto de recuperación coherente con la aplicación hello. Si realiza una conmutación por error de un plan de recuperación, puede ir de máquina virtual de tooindividual y mirar **puntos de recuperación más reciente** icono tooget esta información.
    1.  **Última**: esta opción procesa primero todos los datos de Hola que se ha enviado tooSite recuperación servicio toocreate un punto de recuperación para cada máquina virtual antes de conmutar a tooit. Esta opción proporciona Hola menor RPO (objetivo de punto de recuperación) como máquina de virtual Hola creada después de conmutación por error tendrá todos los datos de Hola que se ha replicado tooSite el servicio de recuperación cuando se activó la conmutación por error de Hola.
    1.  **Latest multi-VM processed** (Últimas máquinas virtuales procesadas): esta opción solo está disponible para planes de recuperación que tienen al menos una máquina virtual con la coherencia para varias máquinas virtuales activada. Punto de máquinas virtuales que forman parte de una replicación grupo conmutación por error toohello recuperación más reciente comunes varias VM coherente. Otra máquinas virtuales conmutación por error tootheir más reciente procesado punto de recuperación.  
    1.  **Latest multi-VM app-consistent** (Últimas máquinas virtuales coherentes con la aplicación): esta opción solo está disponible para planes de recuperación que tienen al menos una máquina virtual con la coherencia para varias máquinas virtuales activada. Máquinas virtuales que forman parte de una replicación de grupo de conmutación por error toohello más reciente varias VM coherentes con la aplicación de punto de recuperación común. Otra máquinas virtuales conmutación por error tootheir más reciente coherente con la aplicación el punto de recuperación. 
    1.  **Personalizado**: si está realizando la conmutación por error de prueba de una máquina virtual, puede usar este punto de recuperación concreto de opción toofailover tooa.
1. Seleccione un **red virtual de Azure**: proporcione una red virtual de Azure donde se debería crear máquinas virtuales de prueba de Hola. Máquinas virtuales de prueba toocreate en una subred del mismo nombre de intentos de recuperación de sitio y usar Hola IP misma que la proporcionada en **proceso y red** configuración de máquina virtual de Hola. Si la subred del mismo nombre no está disponible en hello red virtual de Azure proporcionado para la conmutación por error de prueba, máquina virtual de prueba se crea en la primera subred de hello alfabéticamente. Si la misma IP no está disponible en la subred de hello, la máquina virtual tiene otra dirección IP disponible en la subred de Hola. Consulte esta sección para obtener [más información](#creating-a-network-for-test-failover).
1. Si está conmuta tooAzure y está habilitado el cifrado de datos, en **clave de cifrado** certificado Hola seleccione emitido cuando habilita el cifrado de datos durante la instalación del proveedor. Puede omitir este paso si no ha habilitado el cifrado en la máquina virtual de Hola.
1. Realizar el seguimiento de progreso de la conmutación por error en hello **trabajos** ficha. Debe ser toosee capaz de máquina de réplica de prueba de Hola Hola portal de Azure.
1. tooinitiate una conexión RDP en la máquina virtual de hello, necesitará demasiado[agregar una ip pública](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) en hello interfaz de red de hello conmutado por máquina virtual. Si conmuta por máquina virtual de tooa clásico, deberá demasiado[agregar un punto de conexión](../virtual-machines/windows/classic/setup-endpoints.md) en el puerto 3389
1. Una vez que haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas** registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Esto elimina máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.


> [!TIP]
> Máquinas virtuales de prueba toocreate en una subred del mismo nombre de intentos de recuperación de sitio y usar Hola IP misma que la proporcionada en **proceso y red** configuración de máquina virtual de Hola. Si la subred del mismo nombre no está disponible en hello red virtual de Azure proporcionado para la conmutación por error de prueba, máquina virtual de prueba se crea en la primera subred de hello alfabéticamente. Si IP de destino de hello forma parte de hello elegido subred, recuperación de sitio intenta toocreate Hola prueba de conmutación por error máquina virtual a través Hola IP de destino. Si IP de destino de hello no forma parte de hello elegido subred máquina virtual de conmutación por error de prueba se crea con cualquier dirección IP disponible en hello elegido subred.
>
>

## <a name="test-failover-job"></a>Trabajo de conmutación por error de prueba

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Cuando se desencadena una conmutación por error de prueba, se realizan estos pasos:

1. Comprobación de los requisitos previos: en este paso se garantiza que se cumplen todas las condiciones necesarias para la conmutación por error.
1. Conmutación por error: Este paso procesa los datos de Hola y sea listo para que se puede crear una máquina virtual de Azure fuera de ella. Si ha elegido **más reciente** punto de recuperación, este paso crea un punto de recuperación de datos de Hola que se ha enviado el servicio toohello.
1. Inicio: En este paso se crea una máquina virtual de Azure utilizando los datos de hello procesados en el paso anterior de Hola.

## <a name="time-taken-for-failover"></a>Tiempo necesario para la conmutación por error

En algunos casos, conmutación por error de máquinas virtuales requiere un paso adicional intermedio que normalmente tarda aproximadamente 8 too10 minutos toocomplete. Estos casos son los siguientes:

* Máquinas virtuales VMware usando una versión de servicio de movilidad anterior a 9,8 hello
* Servidores físicos
* Máquinas virtuales de VMware Linux
* Máquinas virtuales Hyper-V protegidas como servidores físicos
* Máquinas virtuales de VMware donde los siguientes controladores no están presentes como controladores de arranque
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* Máquinas virtuales de VMware que no tienen el servicio DHCP habilitado independientemente de si usan direcciones IP estáticas o DHCP

En hello todos los demás casos este paso intermedio no es necesaria y tiempo Hola de conmutación por error de hello es notablemente inferior.


## <a name="creating-a-network-for-test-failover"></a>Creación de una red para conmutación por error de prueba
Se recomienda que, cuando realiza una conmutación por error de prueba elija una red que está aislada de la red de sitio de recuperación de producción que proporcionó en **proceso y red** configuración de máquina virtual de Hola. De forma predeterminada, cualquier red virtual que se cree en Azure está aislada de otras redes. Esta red debe imitar la red de producción:

1. Red de prueba debe tener el mismo número de subredes que en la red de producción y con el mismo nombre que las subredes de hello en la red de producción de hello.
1. Debe usar la red de prueba Hola mismo intervalo IP que el de la red de producción.
1. Hola de actualización DNS de red de prueba como Hola IP que asignó como destino IP para hello DNS máquinas virtuales de hello **proceso y red** configuración. Examine la sección [Consideraciones sobre la conmutación por error de prueba para Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obtener más información.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Red de producción de tooa de conmutación por error de prueba en el sitio de recuperación
Se recomienda que, cuando realiza una conmutación por error de prueba elija una red que es diferente de la red de sitio de recuperación de producción que proporcionó en **proceso y red** configuración de máquina virtual de Hola. Sin embargo, si realmente desea conectividad de red de tooend toovalidate final en un error a través de la máquina virtual, tenga en cuenta Hola siguientes puntos:

1. Asegúrese de que la máquina virtual principal Hola está apagado cuando realiza una conmutación por error de prueba de Hola. Si no lo hace, habrá dos máquinas virtuales con hello misma identidad que se ejecuta en hello en la misma red en hello mismo tiempo y que puede provocar la tooundesired consecuencias.
1. Se perderán los cambios realizados en máquinas virtuales de hello prueba de conmutación por error cuando se limpieza Hola conmutación por error máquinas virtuales. Estos cambios no serán máquina virtual principal de toohello atrás replicada.
1. Esta forma de realizar pruebas conduce tooa tiempo de inactividad de la aplicación de producción. Los usuarios de aplicación Hola se deben plantear toonot de la aplicación de Hola de uso al explorar Hola recuperación ante desastres está en curso.  



## <a name="prepare-active-directory-and-dns"></a>Preparación de Active Directory y DNS
toorun una conmutación por error de prueba para probar la aplicación, necesitará una copia del entorno de Active Directory de producción de hello en el entorno de prueba. Examine la sección [Consideraciones sobre la conmutación por error de prueba para Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obtener más información.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Preparar tooconnect tooAzure las máquinas virtuales después de la conmutación por error

Si desea que tooconnect tooAzure máquinas virtuales mediante RDP después de la conmutación por error, asegúrese de que hello las acciones que se resumen en la tabla de Hola.

**Conmutación por error** | **Ubicación** | **Acciones**
--- | --- | ---
**Máquina virtual de Azure que ejecuta Windows** | En la máquina local antes de la conmutación por error | tooaccess Hola VM de Azure sobre Hola internet, habilitar RDP, asegúrese de que TCP y UDP reglas se agregan para hello **público**, y que se permita RDP en **Firewall de Windows** > **permitido Aplicaciones**, para todos los perfiles.<br/><br/> tooaccess a través de una conexión de sitio a sitio, habilitar RDP en la máquina de Hola y asegúrese de que está permitido RDP en hello **Firewall de Windows** -> **permite aplicaciones y características** para  **Dominio y Private** redes.<br/><br/>  Asegúrese de que Directiva de SAN del sistema operativo Hola se establece demasiado**OnlineAll**. [Más información](https://support.microsoft.com/kb/3031135).<br/><br/> Asegúrese de que no hay Windows actualizaciones pendientes en la máquina virtual de hello cuando se desencadenan una conmutación por error. Actualización de Windows puede comenzar cuando la conmutación por error y no será capaz de toologin toohello virtual machine hasta que se complete la actualización de Hola. <br/><br/>
**Máquina virtual de Azure que ejecuta Windows** | En la máquina virtual de Azure después de la conmutación por error | Para una máquina virtual clásica, [agregar un extremo público](../virtual-machines/windows/classic/setup-endpoints.md) para hello protocolo RDP (puerto 3389)<br/><br/>  En el caso de una máquina virtual de Resource Manager, [añada una dirección IP pública](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) a la máquina virtual.<br/><br/> Hola reglas del grupo de seguridad de red en hello conmutado por error máquinas virtuales y hello toowhich de subred de Azure está conectado, necesita puerto RDP de las conexiones entrante de tooallow toohello.<br/><br/> Para una máquina virtual del Administrador de recursos, también puede comprobar **diagnósticos de arranque** toolook en una captura de pantalla de máquina virtual de Hola<br/><br/> Si no puede conectarse, compruebe que Hola VM se esté ejecutando y, a continuación, consulte estos [sugerencias para solucionar problemas](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Máquina virtual de Azure que ejecuta Linux** | En la máquina local antes de la conmutación por error | Asegúrese de que ese servicio de Secure Shell en hello Azure VM Hola se establece toostart automáticamente en el arranque del sistema.<br/><br/> Compruebe que las reglas de firewall permiten a un tooit de conexión SSH.
**Máquina virtual de Azure que ejecuta Linux** | Máquina virtual de Azure después de la conmutación por error | Hola reglas del grupo de seguridad de red en hello conmutado por error máquinas virtuales y hello toowhich de subred de Azure está conectado, es necesario tooallow conexiones toohello SSH el puerto entrante.<br/><br/> Para una máquina virtual clásica, [agregar un extremo público](../virtual-machines/windows/classic/setup-endpoints.md) debe crearse en las conexiones entrantes de tooallow en hello SSH (puerto TCP 22 de forma predeterminada).<br/><br/> En el caso de una máquina virtual de Resource Manager, [añada una dirección IP pública](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) a la máquina virtual.<br/><br/> Para una máquina virtual del Administrador de recursos, también puede comprobar **diagnósticos de arranque** toolook en una captura de pantalla de máquina virtual de Hola<br/><br/>



## <a name="next-steps"></a>Pasos siguientes
Después de ejecutar correctamente una conmutación por error de prueba, puede intentar realizar una [conmutación por error](site-recovery-failover.md).
