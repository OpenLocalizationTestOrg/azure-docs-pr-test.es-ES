---
title: el adaptador de StorSimple para SharePoint aaaInstall | Documentos de Microsoft
description: "Describe cómo tooinstall y configurar o quitar Hola el adaptador de StorSimple para SharePoint en una granja de servidores de SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Instalar y configurar Hola el adaptador de StorSimple para SharePoint
## <a name="overview"></a>Información general
Hola adaptador de StorSimple para SharePoint es un componente que le permite ofrecer almacenamiento flexible de Microsoft Azure StorSimple y granjas de servidores de tooSharePoint de protección de datos. Puede usar el contenido de objetos binarios grandes (BLOB) de hello adaptador toomove de hello SQL Server las bases de datos de contenido toohello StorSimple de Microsoft Azure en la nube dispositivo de almacenamiento híbrido.

Hello adaptador de StorSimple para SharePoint funciona como un proveedor de almacenamiento remoto de blobs (RBS) y utiliza Hola toostore de la característica de almacenamiento remoto de blobs de SQL Server contenido de SharePoint sin estructurar (en forma de Hola de BLOBs) en un servidor de archivos que está respaldado por un dispositivo de StorSimple.

> [!NOTE]
> Hola adaptador de StorSimple para SharePoint es compatible con almacenamiento de blobs de remoto (RBS) de SharePoint Server 2010. No admite el almacenamiento externo de blobs (EBS) de SharePoint Server 2010.


* Hola toodownload adaptador de StorSimple para SharePoint, vaya demasiado[adaptador de StorSimple para SharePoint] [ 1] Hola Microsoft Download Center.
* Para obtener información sobre la planeación de RBS y RBS limitaciones, vaya demasiado[decidir toouse RBS en SharePoint 2013] [ 2] o [planeación de RBS (SharePoint Server 2010)] [3].

Hello resto de esta información general describe brevemente rol Hola de adaptador de StorSimple para SharePoint de Hola y Hola capacidad de SharePoint y los límites de rendimiento que debe tener en cuenta antes de instalar y configurar el adaptador de Hola. Después de revisar esta información, vaya demasiado[el adaptador de StorSimple para la instalación de SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin Configurar adaptador Hola.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Beneficios del adaptador de StorSimple para SharePoint
En un sitio de SharePoint, el contenido se almacena como datos BLOB no estructurados en una o más bases de datos de contenido. De forma predeterminada, estas bases de datos se hospedan en equipos que ejecutan SQL Server y que se encuentran en la granja de servidores de SharePoint de Hola. Los BLOBs pueden aumentar rápidamente de tamaño, consumiendo grandes cantidades de almacenamiento local. Por esta razón, es recomendable toofind solución de almacenamiento más económica y otro. SQL Server proporciona una tecnología denominada remoto almacenamiento BLOBs (RBS) que le permite almacenar el contenido de BLOB Hola sistema de archivos, fuera de la base de datos de SQL Server de Hola. Con RBS, BLOBs pueden residir en el sistema de archivos de hello en el equipo de Hola que ejecuta SQL Server o que puedan almacenarse en el sistema de archivos de hello en otro equipo del servidor.

RBS requiere que use un proveedor RBS, como Hola adaptador de StorSimple para SharePoint, tooenable RBS en SharePoint. Hola adaptador de StorSimple para SharePoint funciona con RBS, lo que le permite mover servidor tooa de BLOBs respaldada por el sistema de Microsoft Azure StorSimple Hola. Microsoft Azure StorSimple, a continuación, almacena datos BLOB de hello localmente o en la nube hello, según el uso. Los bLOBs que son muy activos (que normalmente se conoce tooas nivel 1 o datos activos) residen localmente. Los datos de archivo y de datos menos activos residen en nube de Hola. Después de habilitar RBS en una base de datos de contenido, cualquier contenido nuevo de BLOB creado en SharePoint se almacena en el dispositivo StorSimple hello y no está en la base de datos de contenido de Hola.

implementación de Microsoft Azure StorSimple Hola de RBS proporciona Hola siguientes ventajas:

* Por móvil BLOB tooa contenido servidor independiente, puede reducir Hola carga de consultas en SQL Server, lo que puede mejorar la capacidad de respuesta de SQL Server. 
* StorSimple de Azure usa el tamaño de los datos tooreduce desduplicación y la compresión.
* Azure StorSimple ofrece protección de datos en forma de Hola de local y en la nube. Además, si coloca Hola propia base de datos en el dispositivo StorSimple hello, hacer copias de seguridad base de datos de contenido de Hola y BLOBs juntos de forma coherente de bloqueo. (Solo se admite mover un dispositivo de toohello de base de datos de contenido de hello de dispositivo de la serie StorSimple 8000 Hola. Esta característica no se admite para la serie de hello 5000 o 7000.)
* StorSimple de Azure incorpora características de recuperación ante desastres, entre otras, la conmutación por error, la recuperación de archivos y volúmenes (incluida la recuperación de prueba), y la rápida restauración de los datos.
* Puede usar software de recuperación de datos, como Kroll Ontrack PowerControls, con las instantáneas de StorSimple BLOB tooperform nivel de elemento de recuperación de datos de contenido de SharePoint. (Este software de recuperación de datos se compra por separado).
* Hola adaptador de StorSimple para SharePoint conecta al portal de Administración Central de SharePoint de hello, permitiéndole toomanage toda la solución de SharePoint desde una ubicación central.

Mover el sistema de archivos BLOB toohello contenido puede proporcionar otros ahorros de costos y beneficios. Por ejemplo, usar RBS puede reducir la necesidad de Hola de almacenamiento de información de nivel 1 costoso y, porque reduce la base de datos de contenido de hello, RBS puede reducir el número de Hola de bases de datos necesarias en la granja de servidores de SharePoint de Hola. Sin embargo, otros factores, como los límites de tamaño de base de datos y la cantidad de Hola de contenido no sea de RBS, también pueden afectar a los requisitos de almacenamiento. Para obtener más información sobre los costos de Hola y ventajas de usar RBS, vea [planeación de RBS (SharePoint Foundation 2010)] [ 4] y [decidir toouse RBS en SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Límites de capacidad y rendimiento
Antes de considerar usar RBS en la solución de SharePoint, debe ser consciente de rendimiento de hello probado y límites de capacidad de SharePoint Server 2010 y SharePoint Server 2013 y cómo estos límites relacionan tooacceptable rendimiento. Para obtener más información, consulte [Restricciones y límites de software de SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Revise los siguientes de hello antes de configurar RBS:

* Asegúrese de que ese tamaño total de Hola de hello contenido (Hola el tamaño de una base de datos de contenido) más hello de los BLOBs externalizados asociados no superan el límite de tamaño RBS de hello compatible con SharePoint. Este límite es de 200 GB. 
  
    **base de datos de contenido de toomeasure y tamaño del BLOB**
  
  1. Ejecute esta consulta en hello WFE de Administración Central. Iniciar Hola Shell de administración de SharePoint y, a continuación, escriba Hola después de tamaño de Hola de tooget de comandos de Windows PowerShell de bases de datos de contenido de hello:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Este paso obtiene tamaño Hola de base de datos de contenido de hello en el disco de Hola.
  2. Ejecute una de las siguientes consultas SQL en SQL Management Studio en el cuadro de hello SQL server en cada base de datos de contenido de Hola y agregar Hola resultado toohello número obtenido en el paso 1.
     
     En las bases de datos de contenido de SharePoint 2013, escriba:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     En las bases de datos de contenido de SharePoint 2010, escriba:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Este paso obtiene tamaño Hola de hello BLOBs que se han externalizado.
* Se recomienda almacenar todo el contenido de BLOB y base de datos localmente en el dispositivo StorSimple Hola. dispositivo de StorSimple de Hello es un clúster de dos nodos para alta disponibilidad. Colocación de las bases de datos de contenido de Hola y BLOBs en el dispositivo StorSimple Hola proporciona alta disponibilidad.
  
    Use tradicional SQL Server migración mejores prácticas toomove Hola contenido de la base de datos toohello dispositivo StorSimple. Mover la base de datos de hello solo después de que todo el contenido BLOB de base de datos de hello ha sido movido toohello recurso compartido de archivos mediante RBS. Si decide que el dispositivo de StorSimple de toohello toomove Hola contenido de la base de datos, se recomienda que configurar el almacenamiento de contenido de la base de datos de hello en dispositivo hello como el volumen principal.
* En Microsoft Azure StorSimple, si usa volúmenes en capas, no hay ninguna manera tooguarantee que contenido almacenado localmente en el dispositivo StorSimple Hola no estará tooMicrosoft en capas de almacenamiento de nube de Azure. Por lo tanto, se recomienda usar volúmenes de StorSimple anclados localmente junto con RBS de SharePoint. Esto garantizará que todo el contenido BLOB permanece localmente en el dispositivo StorSimple hello y no ha movido tooMicrosoft Azure.
* Si no almacena las bases de datos de contenido de hello en dispositivo de StorSimple de hello, utilice tradicional SQL Server alta disponibilidad recomendaciones compatibles con RBS. La agrupación en clústeres de SQL Server admite RBS, mientras que la creación de reflejos de SQL Server no es compatible. 

> [!WARNING]
> Si no ha habilitado RBS, no se recomienda mover el dispositivo de StorSimple de toohello de hello contenido de la base de datos. Se trata de una configuración no probada.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Instalación del adaptador de StorSimple para SharePoint
Para poder instalar Hola el adaptador de StorSimple para SharePoint, debe configurar el dispositivo de StorSimple de Hola y asegúrese de que la granja de servidores de SharePoint de Hola y creación de instancias de SQL Server cumplen todos los requisitos previos. Este tutorial describen los requisitos de configuración, así como los procedimientos de instalación y actualización Hola el adaptador de StorSimple para SharePoint.

## <a name="configure-prerequisites"></a>Configuración de los requisitos previos
Para poder instalar Hola el adaptador de StorSimple para SharePoint, asegúrese de que el dispositivo de StorSimple de Hola y granja de servidores de SharePoint, la creación de instancias de SQL Server cumplen Hola siguiendo los requisitos previos.

### <a name="system-requirements"></a>Requisitos del sistema
Hola adaptador de StorSimple para SharePoint funciona con hello después de hardware y software:

* Sistema operativo compatible: Windows Server 2008 R2 SP1, Windows Server 2012 o Windows Server 2012 R2.
* Versiones de SharePoint compatibles: SharePoint Server 2010 o SharePoint Server 2013
* Versiones de SQL Server compatibles: SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition o SQL Server 2012 Enterprise Edition 
* Dispositivos StorSimple compatibles: serie StorSimple 8000, serie StorSimple 7000 o serie StorSimple 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Requisitos previos de configuración del dispositivo StorSimple
dispositivo de StorSimple de Hello es un dispositivo de bloque y como tal, requiere un servidor de archivos en el que se pueden hospedar datos Hola. Se recomienda usar un servidor independiente en lugar de un servidor existente de granja de servidores de SharePoint de Hola. Este servidor de archivos debe estar en Hola misma red de área local (LAN) como equipo de SQL Server de Hola que bases de datos de contenido de hello hosts.

> [!TIP]
> * Si configura la granja de servidores de SharePoint para lograr alta disponibilidad, debe implementar también servidor de archivos de Hola para alta disponibilidad.
> * Si no almacena datos de contenido de hello en dispositivo de StorSimple de hello, use procedimientos recomendados tradicionales de alta disponibilidad compatibles con RBS. La agrupación en clústeres de SQL Server admite RBS, mientras que la creación de reflejos de SQL Server no es compatible. 


Asegúrese de que el dispositivo de StorSimple está configurado correctamente y que toosupport de volúmenes correspondientes en la implementación de SharePoint están configurados y accesible desde el equipo de SQL Server. Vaya demasiado[implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md) si todavía no ha implementado ni configurado su dispositivo de StorSimple. Tenga en cuenta dirección IP de hello de dispositivo de StorSimple de hello; necesitará durante el adaptador de StorSimple para la instalación de SharePoint.

Además, asegúrese de que ese toobe de volumen de hello utilizado para la externalización de blobs cumple Hola según los requisitos:

* volumen de Hello debe formatearse con un tamaño de unidad de asignación de 64 KB.
* El front-end web (WFE) y servidores de aplicaciones deben ser capaz de tooaccess Hola a través de una ruta de acceso de convención de nomenclatura universal (UNC, Universal Naming Convention).
* granja de servidores de SharePoint de Hello debe ser configurado toowrite toohello volumen.

> [!NOTE]
> Después de instalar y configurar el adaptador de hello, toda la externalización de blobs debe pasar por dispositivo de StorSimple de hello (dispositivo Hola presentará Hola volúmenes tooSQL servidor y administrar niveles de almacenamiento de hello). No puede utilizar ningún otro destino para la externalización de BLOBs.


Si piensa toouse Administrador de instantáneas StorSimple tootake instantáneas de BLOB de Hola y de base de datos los datos, ser seguro tooinstall Administrador de instantáneas de StorSimple en el servidor de base de datos de Hola para que puedan utilizar hello tooimplement servicio SQL Writer Hola instantáneas de volumen de Windows Service (VSS).

> [!IMPORTANT]
> Administrador de instantáneas de StorSimple no admite Hola VSS Writer de SharePoint y no se puede tomar instantáneas coherentes con la aplicación de datos de SharePoint. En un escenario de SharePoint, el Administrador de instantáneas StorSimple proporciona solo copias de seguridad preparadas para bloqueos.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Requisitos previos de configuración de la granja de SharePoint
Asegúrese de que su granja de servidores de SharePoint está configurada correctamente, de la siguiente manera:

* Compruebe que la granja de servidores de SharePoint está en un estado correcto y compruebe Hola siguiente:
* Todos los servidores de aplicaciones registrados en la granja de servidores de Hola y WFE de SharePoint se ejecutan y se pueden hacer ping del servidor de hello en el que va a instalar Hola el adaptador de StorSimple para SharePoint.
* Hola servicio de temporizador de SharePoint (SPTimerV3 o SPTimerV4) se está ejecutando en cada servidor WFE y el servidor de aplicaciones.
* Tanto Hola servicio de temporizador de SharePoint y grupo de aplicaciones de IIS de hello en la que se ejecuta el sitio de Administración Central de SharePoint de Hola tengan privilegios administrativos.
* Asegúrese de que Internet Explorer Enhanced Security Context (IE ESC) está deshabilitado. Siga estos toodisable pasos ESC de Internet Explorer:
  
  1. Cierre todas las instancias de Internet Explorer.
  2. Inicie el administrador del servidor de Hola.
  3. En el panel izquierdo de hello, haga clic en **servidor Local**.
  4. En hello haga panel, a continuación demasiado**configuración de seguridad mejorada de Internet Explorer**, haga clic en **en**.
  5. En **Administradores**, haga clic en **Desactivar**.
  6. Haga clic en **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Requisitos previos del almacenamiento remoto de BLOBS (RBS)
Asegúrese de utilizar una versión compatible de SQL Server. Solamente hello versiones siguientes son compatible y puede toouse RBS:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

Los bLOBs pueden externalizarse en solo los volúmenes que Hola dispositivo StorSimple presenta tooSQL Server. No se admite ningún otro destino para la externalización de BLOBS.

Cuando se hayan completado todos los pasos de configuración de requisitos previos, vaya demasiado[Hola de instalar el adaptador de StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Instalar Hola el adaptador de StorSimple para SharePoint
Usar hello siguiendo los pasos tooinstall Hola el adaptador de StorSimple para SharePoint. Si va a reinstalar el software de hello, consulte [actualizar o reinstalar Hola el adaptador de StorSimple para SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). Hola tiempo necesario para la instalación de Hola depende número total de Hola de bases de datos de SharePoint en la granja de servidores de SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Configuración de RBS
Después de instalar Hola el adaptador de StorSimple para SharePoint, configure RBS según se describe en hello siguiendo el procedimiento.

> [!TIP]
> Hola adaptador de StorSimple para SharePoint se conecta a la página de Administración Central de SharePoint de Hola, lo que permite toobe RBS habilitada o deshabilitada en cada base de datos de contenido en la granja de servidores de SharePoint de Hola. Sin embargo, habilitar o deshabilitar RBS en la base de datos de contenido de hello provoca el restablecimiento de IIS, que, según la configuración de la granja de servidores, puede interrumpir temporalmente disponibilidad Hola de hello SharePoint front-end web (WFE). (Factores como el uso de Hola de un equilibrador de carga de front-end, la carga actual del servidor hello etc., pueden limitar o eliminar tal interrupción). tooprotect a los usuarios de una interrupción, se recomienda habilitar o deshabilitar RBS solo durante una ventana de mantenimiento planeada.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Configuración de la recolección de elementos no utilizados
Cuando se eliminan los objetos de un sitio de SharePoint, no se eliminan automáticamente de hello volumen del almacén de RBS. En su lugar, una asincrónica, programa de mantenimiento de segundo plano elimina los BLOBs huérfanos del almacén de archivos de Hola. Los administradores del sistema pueden programar este proceso toorun periódicamente o pueden iniciarlo cuando lo estimen necesario.

Este programa de mantenimiento (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) se instala automáticamente en todos los servidores WFE y servidores de aplicaciones de SharePoint al habilitar RBS. programa Hello se instala en hello ubicación siguiente: *unidad de arranque*: \Program almacenamiento remoto de blobs de SQL 10.50\Maintainer\

Para obtener información acerca de cómo configurar y usar el programa de mantenimiento de hello, consulte [mantener RBS en SharePoint Server 2013][8].

> [!IMPORTANT]
> programa del mantenedor de RBS Hello es consumen muchos recursos. Debe programarla toorun solo durante periodos de poca actividad en la granja de servidores de SharePoint de Hola.


### <a name="delete-orphaned-blobs-immediately"></a>Elimine los BLOBS huérfanos de inmediato
Si necesita toodelete huérfano BLOBs inmediatamente, puede usar Hola siguiendo las instrucciones. Tenga en cuenta que estas instrucciones son un ejemplo de cómo esto puede hacerse en un entorno de SharePoint 2013 con hello de los componentes siguientes:

* nombre de la base de datos de contenido de Hello es WSS_Content.
* nombre de SQL Server de Hello es SHRPT13 SQL12\SHRPT13.
* nombre de aplicación web de Hello es SharePoint-80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Actualizar o reinstalar Hola el adaptador de StorSimple para SharePoint
Usar hello siguiendo procedimientos tooupgrade SharePoint server y, a continuación, vuelva a instalar el adaptador de StorSimple para SharePoint o toosimply actualización o volver a instalar el adaptador de hello en una granja de servidores de SharePoint existente.

> [!IMPORTANT]
> Revisar Hola siguiente información antes de intentar tooupgrade el software de SharePoint y/o actualizar o reinstalar Hola el adaptador de StorSimple para SharePoint:
> 
> * Los archivos migrados previamente tooexternal almacenamiento mediante RBS no estarán disponible hasta que finalice la reinstalación de Hola y Hola característica RBS se vuelva a habilitar. toolimit usuario afectan, lleve a cabo cualquier actualización o reinstalación de una ventana de mantenimiento planeada.
> * tiempo de Hello necesario para hello actualización/reinstalación puede variar en función número total de Hola de bases de datos de SharePoint en la granja de servidores de SharePoint de Hola.
> * Una vez completada la actualización o reinstalación de hello, necesitará tooenable RBS para las bases de datos de contenido de Hola. Para obtener más información, vea [Configuración de RBS](#configure-rbs) .
> * Si va a configurar RBS para una granja de servidores de SharePoint que tiene un gran número de bases de datos (más de 200), Hola **Administración Central de SharePoint** página puede agotar el tiempo de espera. Si sucede esto, actualice la página de Hola. Esto no afecta el proceso de configuración de Hola.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Eliminación del adaptador de StorSimple para SharePoint
Hola procedimientos siguientes describe cómo toomove Hola BLOBs realizar copias de bases de datos de contenido de SQL Server toohello y, a continuación, desinstalación Hola el adaptador de StorSimple para SharePoint. 

> [!IMPORTANT]
> Tener toomove Hola BLOBs back-toohello contenidos las bases de datos antes de desinstalar el software del adaptador de Hola.


### <a name="before-you-begin"></a>Antes de empezar
Recopilar Hola siguiente información antes de mover datos de hello copia de bases de datos de contenido de SQL Server toohello y comenzar el proceso de eliminación de adaptador de hello:

* Hola nombres de todas las bases de datos de hello para el que RBS está habilitado
* ruta de acceso UNC de Hola de hello configurado el almacén de blobs

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Mover bases de datos de contenido de back-toohello de BLOBs de Hola
Antes de desinstalar el adaptador de StorSimple de hello para el software de SharePoint, debe migrar todos Hola BLOBs creados bases de datos de contenido de SQL Server externalizados toohello atrás. Si intentas hello toouninstall adaptador de StorSimple para SharePoint antes de mover todas Hola BLOBs back-toohello contenidos bases de datos, verá Hola siguiente mensaje de advertencia.

![Mensaje de advertencia](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove Hola BLOBs back-toohello contenidos las bases de datos
1. Descargar cada uno de los objetos de hello externalizado.
2. Abra hello **Administración Central de SharePoint** página y examinar demasiado**configuración del sistema**.
3. En **Azure StorSimple**, haga clic en **Configurar el adaptador de StorSimple**.
4. En hello **configurar el adaptador de StorSimple** página, haga clic en hello **deshabilitar** botón debajo de cada una de las bases de datos de contenido Hola que desea tooremove de almacenamiento de blobs externo. 
5. Eliminar objetos de Hola de SharePoint y, a continuación, cargarlos de nuevo.

Como alternativa, puede utilizar Microsoft hello` RBS Migrate()` cmdlet de PowerShell incluido con SharePoint. Para obtener más información, vea [migrar contenido dentro o fuera de RBS](https://technet.microsoft.com/library/ff628255.aspx).

Después de mover la base de datos de contenido de back-toohello de BLOBs de hello, vaya toohello siguiente paso: [adaptador Hola de desinstalación](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Desinstalar el adaptador de Hola
Después de mover Hola BLOBs back-toohello contenidos bases de datos SQL, utilice uno de hello sigue opciones toouninstall Hola el adaptador de StorSimple para SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>adaptador Hola de toouninstall de programa de instalación de toouse Hola
1. Use una cuenta con toolog de privilegios de administrador en el servidor de toohello web front-end (WFE).
2. Haga doble clic en el adaptador de StorSimple de hello para el programa de instalación de SharePoint. Hola Asistente para la instalación se inicia.
   
    ![Asistente para la instalación](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Haga clic en **Siguiente**. aparece Hola después de la página.
   
    ![Página de eliminación del Asistente para la instalación](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Haga clic en **quitar** tooselect proceso de eliminación de Hola. aparece Hola después de la página.
   
    ![Página de confirmación del Asistente para la instalación](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Haga clic en **quitar** eliminación de hello tooconfirm. Hola después de la página de progreso aparece.
   
    ![Página de progreso del Asistente para la instalación](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Cuando se complete la eliminación de hello, aparece la página de finalización de Hola. Haga clic en **finalizar** tooclose Hola Asistente para la instalación.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>adaptador hello toouninstall de toouse Hola el Panel de Control
1. Abra el Panel de Control de hello y, a continuación, haga clic en **programas y características**.
2. Seleccione **Adaptador de StorSimple para SharePoint** y luego haga clic en **Desinstalar**.

## <a name="next-steps"></a>Pasos siguientes
[Obtenga más información sobre StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
