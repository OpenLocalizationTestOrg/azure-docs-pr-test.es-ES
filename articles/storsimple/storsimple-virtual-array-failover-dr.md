---
title: "aaaStorSimple Virtual Array ante desastres recuperación y el dispositivo de conmutación por error | Documentos de Microsoft"
description: "Más información acerca de cómo toofailover la matriz Virtual de StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Recuperación ante desastres y conmutación por error de dispositivos para la matriz virtual de StorSimple mediante Azure Portal

## <a name="overview"></a>Información general
Este artículo describe recuperación ante desastres de Hola para su Microsoft Azure StorSimple Virtual Array incluidos Hola detallada salta toofail matriz virtual tooanother. Una conmutación por error permite toomove los datos de un *origen* dispositivo en hello datacenter tooa *destino* dispositivo. Hello dispositivo de destino puede ser ubicado en hello misma o a una ubicación geográfica diferente. conmutación por error de dispositivo de Hello es para todo dispositivo de Hola. Durante la conmutación por error, cambian los datos de nube hello para el dispositivo de origen de hello toothat propiedad hello de dispositivo de destino.

Este artículo es aplicable tooStorSimple arreglos de discos virtuales solo. toofail a través de un dispositivo de la 8000 serie, vaya demasiado[dispositivo conmutación por error y recuperación ante desastres de su dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>Descripción de la recuperación ante desastres y la conmutación por error de dispositivos

En un escenario de recuperación ante desastres, dispositivo primario Hola deja de funcionar. En este escenario, puede mover los datos de nube de hello asociadas Hola error tooanother un dispositivo. Puede usar el dispositivo primario de hello como hello *origen* y especifique otro dispositivo como hello *destino*. Este proceso es que se hace referencia tooas hello *conmutación por error*. Durante la conmutación por error, Hola a todos los volúmenes o recursos compartidos de hello de dispositivo de origen Hola cambiar la propiedad y son transferidos toohello dispositivo de destino. No se permite ningún filtrado de datos de Hola.

Recuperación ante desastres se modelan como una restauración de todos los dispositivos con calor Hola mapa basados en niveles y de seguimiento. Un mapa térmico se define mediante la asignación de un toohello del valor de calor tomando como base de datos de lectura y escritura de patrones. Este calor asignar, a continuación, niveles de Hola menor calor datos fragmentos toohello en la nube primero manteniendo Hola calor alta (más usado) los fragmentos de datos en el nivel local Hola. Durante una recuperación ante desastres, StorSimple usa toorestore de mapa térmico de Hola y rehidratar datos Hola de nube de Hola. dispositivo de Hello captura todos los Hola volúmenes o recursos compartidos de copia de seguridad reciente Hola última (tal y como se determina internamente) y realiza una restauración de copia de seguridad. matriz virtual Hola orquesta todo proceso de recuperación ante desastres Hola.

> [!IMPORTANT]
> dispositivo de origen Hola se elimina al final de Hola de conmutación por error de dispositivo y, por tanto, no se admite una conmutación por recuperación.
> 
> 

Recuperación ante desastres se organiza a través de la característica de conmutación por error de dispositivo de Hola y se inicia desde hello **dispositivos** hoja. Esta hoja tabula todos los hello StorSimple dispositivos conectados tooyour dispositivo el servicio StorSimple Manager. Para cada dispositivo, puede ver el nombre descriptivo de hello, estado, capacidad de aprovisionamiento y máxima, tipo y modelo.

## <a name="prerequisites-for-device-failover"></a>Requisitos previos para la conmutación por error de un dispositivo

### <a name="prerequisites"></a>Requisitos previos

Para una conmutación por error de dispositivo, asegúrese de que Hola siguiendo los requisitos previos se cumplen:

* dispositivo de origen de Hello necesita toobe en un **desactivado** estado.
* Hello dispositivo de destino debe tooshow seguridad como **listo tooset seguridad** Hola portal de Azure. Aprovisionar una matriz virtual de destino de hello capacidad igual o superior. Utilizar tooconfigure de interfaz de usuario web local de Hola y registre correctamente matriz virtual de destino de Hola.
  
  > [!IMPORTANT]
  > No intente dispositivo virtual de tooconfigure Hola registrados a través del servicio Hola. Ninguna configuración de dispositivo debe realizarse a través del servicio Hola.
  > 
  > 
* dispositivo de destino de Hello no puede tener Hola mismo nombre como dispositivo de origen Hola.
* dispositivo de origen y destino Hello tiene toobe Hola el mismo tipo. Solo puede producir un error en una matriz virtual configurada como un servidor de archivos de tooanother de servidor de archivos. Hello mismo puede decirse de un servidor de iSCSI.
* Para un servidor de archivos de recuperación ante desastres, se recomienda que se une toohello de dispositivo de destino de hello mismo dominio como origen de Hola. Esta configuración garantiza que los permisos de recurso compartido de Hola se resuelven automáticamente. Solo Hola conmutación por error tooa dispositivo de destino en hello mismo dominio.
* dispositivos de destino disponibles Hola de DR son dispositivos que tienen Hola igual o mayor capacidad en comparación con el dispositivo de origen toohello. Hello dispositivos que están conectado tooyour servicio pero que no cumplen Hola criterios de espacio no están disponibles como dispositivos de destino.

### <a name="other-considerations"></a>Otras consideraciones

* Si es una conmutación por error planeada 
  
  * Se recomienda que realice todos los volúmenes de Hola o recursos compartidos en el dispositivo de origen Hola sin conexión.
  * Se recomienda que realice una copia de seguridad del dispositivo de hello y, a continuación, continúe con pérdida de datos de toominimize de conmutación por error de Hola. 
* Para una conmutación por error no planeada, dispositivo de hello usa datos de Hola de toorestore de copia de seguridad más recientes de Hola.

### <a name="device-failover-prechecks"></a>Comprobaciones previas a la conmutación por error de dispositivos

Antes de hello que comienza la recuperación ante desastres, dispositivo Hola realiza prechecks. Estas comprobaciones ayudan a garantizar que no se producirán errores cuando comience la recuperación ante desastres. Hola prechecks incluyen:

* Validando cuenta de almacenamiento de Hola.
* Comprobando la conectividad tooAzure de hello en la nube.
* Comprobando el espacio disponible en el dispositivo de destino de Hola.
* Comprobar si un volumen del dispositivo de origen del servidor iSCSI tiene:
  
  * Nombres de ACR válidos.
  * IQN válido (que no supere 220 caracteres).
  * Contraseñas CHAP válidas (entre 12 y 16 caracteres).

Si alguna de hello anterior prechecks no, no puede continuar con hello recuperación ante desastres. Resuelva esos problemas y vuelva a intentar la recuperación ante desastres.

Después de hello DR se ha completado correctamente, propiedad de Hola de los datos de nube de hello en dispositivo de origen de hello es transfieren toohello dispositivo de destino. dispositivo de origen de Hello, a continuación, ya no está disponible en el portal de Hola. Se ha bloqueado el acceso tooall Hola volúmenes o recursos compartidos en el dispositivo de origen de Hola y dispositivo de destino de hello pasa a estar activo.

> [!IMPORTANT]
> Si bien dispositivo Hola ya no está disponible, máquina virtual de Hola que ha aprovisionado en el sistema de host de Hola se siguen consumiendo recursos. Una vez completada correctamente Hola recuperación ante desastres, puede eliminar esta máquina virtual desde el sistema host.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Conmutar por error matriz virtual tooa

Se recomienda aprovisionar, configurar y registrar otra instancia de StorSimple Virtual Array con el servicio StorSimple Device Manager antes de ejecutar este procedimiento.

> [!IMPORTANT]
> 
> * No se puede conmutar de un dispositivo StorSimple 8000 series dispositivo tooa 1200 virtual.
> * Puede conmutar por error desde un dispositivo FIPS habilitada de tooanother de información de procesamiento estándar Federal (FIPS) habilitado dispositivo virtual o el dispositivo de FIPS no tooa implementado en el portal de administración pública Hola.


Realizar Hola siguiendo los pasos toorestore Hola dispositivo tooa destino dispositivo virtual StorSimple.

1. Crear y configurar un dispositivo de destino que cumpla hello [requisitos previos para la conmutación por error de dispositivo](#prerequisites). Completar configuración de dispositivo de Hola a través de la interfaz de usuario de web local de Hola y registrarla en servicio de administrador de dispositivos de StorSimple tooyour. Si crea un servidor de archivos, vaya toostep 1 de [configurado como servidor de archivos](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Si crea un servidor de iSCSI, vaya toostep 1 de [configurado como servidor de iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Desconecte los volúmenes o recursos compartidos sin conexión en el host de Hola. tootake Hola volúmenes o recursos compartidos sin conexión, consulte instrucciones de toohello específicas del sistema operativo de host de Hola. No ya está sin conexión, debe tootake todos Hola volúmenes o recursos compartidos sin conexión en el dispositivo de hello haciendo Hola siguiente.
   
    1. Vaya demasiado**dispositivos** hoja y seleccione el dispositivo.
   
    2. Vaya demasiado**configuración > Administrar > recursos compartidos** (o **configuración > Administrar > volúmenes**). 
   
    3. Seleccione un recurso compartido o un volumen, haga clic con el botón derecho y seleccione **Desconectar**. 
   
    4. Cuando se le pida confirmación, compruebe **entiendo impacto Hola de desconectar este recurso compartido.** 
   
    5. Haga clic en **Desconectar**.

3. En el servicio Administrador de dispositivos de StorSimple, vaya demasiado**Administración > dispositivos**. Hola **dispositivos** hoja, seleccione y haga clic en el dispositivo de origen.

4. En la hoja **Panel del dispositivo**, haga clic en **Desactivar**.

5. Hola **desactivar** hoja, se le solicitará confirmación. La desactivación de un dispositivo es un proceso *permanente* que no se puede deshacer. También es tootake recibir los recursos compartidos o volúmenes en hello host. Escriba tooconfirm de nombre de dispositivo de Hola y haga clic en **desactivar**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. inicia la desactivación de Hola. Recibirá una notificación después de desactivación de Hola se ha completado correctamente.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. En la página de dispositivos de hello, estado del dispositivo Hola ahora cambiar demasiado**desactivado**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. Hola **dispositivos** hoja, seleccione y haga clic en dispositivo de origen desactivado Hola para conmutación por error. 
9. Hola **panel del dispositivo** hoja, haga clic en **una conmutación por error**. 
10. Hola **conmutar por error dispositivo** hoja, Hola siguientes:
    
    1. campo de Hello de dispositivo de origen se rellena automáticamente. Tenga en cuenta tamaño total de datos de hello de dispositivo de origen Hola. tamaño de los datos Hola debe ser anterior a la capacidad disponible de hello en dispositivo de destino de Hola. Revise los detalles de hello asociados hello de dispositivo de origen como nombre de dispositivo, capacidad total y nombres de Hola de recursos compartidos de Hola que se conmuten por error.

    2. En la lista desplegable de Hola de dispositivos disponibles, elija un **dispositivo de destino**. Solo los dispositivos de Hola que tienen suficiente capacidad se muestran en la lista desplegable de Hola.

    3. Compruebe que **entiendo que esta operación se producirá un error en el dispositivo de destino de datos toohello**. 

    4. Haga clic en **Conmutación por error**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Se inicia un trabajo de conmutación por error y recibirá una notificación. Vaya demasiado**dispositivos > trabajos** conmutación por error de toomonitor Hola.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. Hola **trabajos** hoja, verá un trabajo de conmutación por error creado para el dispositivo de origen Hola. Este trabajo realiza hello prechecks de recuperación ante desastres.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Una vez prechecks Hola DR son correctas, trabajo de conmutación por error de hello generará los trabajos de restauración para cada recurso compartido o volumen que exista en el dispositivo de origen.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Después de hello conmutación por error completa, vaya toohello **dispositivos** hoja.
    
    1. Seleccione y haga clic en el dispositivo StorSimple Hola que se usó como dispositivo de destino de hello para el proceso de conmutación por error de Hola.
    2. Vaya demasiado**configuración > Administración > recursos compartidos** (o **volúmenes** si el servidor iSCSI). Hola **recursos compartidos** hoja, puede ver todos los recursos compartidos de hello (volúmenes) de dispositivo antiguo de Hola.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Necesitará demasiado[crear un alias DNS](https://support.microsoft.com/kb/168322) para que todas las aplicaciones que están tratando de Hola tooconnect puede obtener toohello redirigida nuevo dispositivo.

## <a name="errors-during-dr"></a>Errores durante la recuperación ante desastres

**Interrupción de la conectividad de la nube durante la recuperación ante desastres**

Si se interrumpe la conectividad de la nube de Hola después de la recuperación ante desastres se ha iniciado y antes de completar la restauración de dispositivo de hello, Hola DR se producirá un error. Recibirá una notificación de conmutación por error. dispositivo de destino de Hola para recuperación ante desastres está marcada como *inutilizable.* No se puede usar hello mismo dispositivo de destino para DRs futuras.

**No hay dispositivos de destino compatibles**

Si los dispositivos de destino disponibles hello no tiene suficiente espacio, verá un efecto de toohello de error que no hay ningún dispositivo de destino compatible.

**Errores de las comprobaciones previas**

Si no se cumple una de hello prechecks, verá errores anterior al cheque.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Recuperación ante desastres y continuidad empresarial (BCDR)

Un escenario de recuperación (BCDR) de desastres de continuidad de negocio se produce cuando Hola todo Azure centro de datos deja de funcionar. Esto puede afectar a su servicio de administrador de dispositivos de StorSimple y Hola asociadas dispositivos StorSimple.

Si hay dispositivos de StorSimple que se han registrado justo antes de que se produzca un desastre, estos dispositivos de StorSimple necesite toobe eliminado. Después de un desastre hello, puede volver a crear y configurar los dispositivos.

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple mediante la interfaz de usuario de web local hello](storsimple-ova-web-ui-admin.md).

