---
title: aaaRestore un volumen de copia de seguridad de la serie StorSimple 8000 | Documentos de Microsoft
description: "Explica cómo toouse Hola toorestore de catálogo de copia de seguridad de servicio de administrador de dispositivos de StorSimple un volumen de StorSimple de un conjunto de copia de seguridad."
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
ms.workload: TBD
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restaurar un volumen de StorSimple de un conjunto de copia de seguridad

## <a name="overview"></a>Información general

Este tutorial describe la operación de restauración Hola realizada en un dispositivo de la serie 8000 de StorSimple utilizando un conjunto de copia de seguridad existente. Hola de uso **catálogo de copia de seguridad** hoja toorestore un volumen de una variable local o copia de seguridad en la nube. Hola **catálogo de copia de seguridad** hoja muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o automatizadas. operación de restauración de Hola de un conjunto de copia de seguridad pone en línea el volumen de hello inmediatamente mientras se descargan los datos en segundo plano de Hola.

Una restauración de toostart método alternativo es toogo demasiado**dispositivos > [dispositivo] > volúmenes**. Hola **volúmenes** hoja, seleccione un volumen, el menú contextual hello tooinvoke y, a continuación, seleccione **restaurar**.

## <a name="before-you-restore"></a>Antes de restaurar

Antes de iniciar una restauración, revise Hola después advertencias:

* **Debe desconectar el volumen de Hola** : desconectar el volumen hello en ambos host Hola y Hola dispositivo antes de iniciar la operación de restauración de Hola. Aunque la operación de restauración de hello pone automáticamente en línea el volumen de hello en dispositivo hello, manualmente se debe poner en línea el dispositivo de hello en el host de Hola. Puede poner en línea el volumen de hello en host Hola tan pronto como volumen de hello está en línea en el dispositivo de Hola. (No es necesario toowait hasta que finalice la operación de restauración de Hola.) Para conocer los procedimientos, vaya demasiado[desconectar un volumen](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **El tipo de volumen después de la restauración** : volúmenes eliminados se restauran en función de tipo de hello en la instantánea de hello; es decir, los volúmenes que se han anclado localmente se restaurarán como volúmenes anclados localmente y se restauran los volúmenes que estaban en niveles como volúmenes en capas.

    Para los volúmenes existentes, tipo de uso actual de Hola de volumen de hello reemplaza tipo hello que se almacena en la instantánea de Hola. Por ejemplo, si restaura un volumen desde una instantánea tomada cuando el tipo de volumen Hola se interconectan y que el tipo de volumen es ahora localmente anclado (vence tooa operación de conversión que se realizó), volumen de Hola se restaurará como un volumen anclado localmente. De forma similar, si un volumen anclado localmente existente se expande y posteriormente se restaura desde una instantánea más antigua cuidada al volumen de hello es más pequeño, hello volumen restaurado retendrá tamaño expandido actual de Hola.

    No se puede convertir un volumen de un volumen de volumen en capas tooa anclado localmente o desde un tooa volumen anclado localmente en niveles de volumen mientras se está restaurando el volumen de Hola. Espere hasta que finalice la operación de restauración de hello y, a continuación, puede convertir al tipo de tooanother del volumen de Hola. Para obtener información sobre cómo convertir un volumen, consulte demasiado[cambiar el tipo de volumen hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **tamaño del volumen Hello se refleja una en volumen de hello restaurar** : ésta es una consideración importante si va a restaurar un volumen anclado localmente que se ha eliminado (porque ya están completamente aprovisionados volúmenes anclados localmente). Asegúrese de que haya espacio suficiente antes de intentar toorestore un volumen anclado localmente que se haya eliminado anteriormente.

* **No se puede expandir un volumen mientras se está restaurando** : espere a que termine antes de intentar volumen de hello tooexpand operación de restauración de Hola. Para obtener información sobre la expansión de un volumen, consulte demasiado[modificar un volumen](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **Puede realizar una copia de seguridad mientras restaurar un volumen local** : para procedimientos vaya demasiado[usar directivas de copia de seguridad toomanage del servicio de administrador de dispositivos de StorSimple de hello](storsimple-8000-manage-backup-policies-u2.md).

* **Puede cancelar una operación de restauración** : si se cancela el trabajo de restauración de hello, a continuación, el volumen de Hola se revertirá toohello estado que tenía antes de que inició la operación de restauración de Hola. Para conocer los procedimientos, vaya demasiado[cancelar un trabajo](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Cómo funciona la restauración

Para los dispositivos que ejecutan Update 4 o una versión posterior, se implementa una restauración basada en el mapa térmico. Como Hola host solicita tooaccess datos llegan a dispositivo de hello, estas solicitudes se realiza el seguimiento y se crea un mapa térmico. Tasa de solicitud alta da como resultado los fragmentos de datos con mayor térmico mientras que la tasa de solicitud menor traduce toochunks con calor inferior. Debe tener acceso a Hola datos al menos dos veces toobe marcados como _activa_. Un archivo que se modifica también se marca como _activo_. Una vez que se inicia la restauración de hello, hidratación proactivo de datos se produce en función de mapa térmico de Hola. Para las versiones anteriores a la actualización 4, Hola se descargan datos durante la restauración que se basa en el acceso solo.

Hola después advertencias aplica restores basados en tooheatmap:

* El seguimiento basado en el mapa térmico solo se habilita para los volúmenes en capa; los volúmenes anclados localmente no son compatibles.

* No se admite la restauración basadas en el mapa térmico al clonar un dispositivo de tooanother volumen. 

* Si hay una restauración en contexto y existe una instantánea local para hello toobe de volumen restaurado en dispositivo hello, a continuación, no se rehidratar (como los datos ya están disponibles localmente). 

* De forma predeterminada, cuando se restaura, hello rehidratación trabajos se inician que rehidratar proactivamente datos basándose en el mapa térmico de Hola. 

En la actualización 4, cmdlets de Windows PowerShell puede ser usado tooquery rehidratación trabajos en ejecución, cancelar un trabajo de rehidratación y obtener el estado de Hola de trabajo de rehidratación de Hola.

* `Get-HcsRehydrationJob`-Este cmdlet obtiene estado Hola de trabajo de rehidratación Hola. Se desencadena un solo trabajo de rehidratación para un volumen.

* `Set-HcsRehydrationJob`-Este cmdlet permite toopause, detener, reanudar el trabajo de rehidratación de hello, si rehidratación Hola está en curso.

Para obtener más información sobre los cmdlets de rehidratación, vaya demasiado[referencia de cmdlet de Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Normalmente, con la rehidratación automática, se espera que el rendimiento de lectura transitorio sea superior. Hola magniutde real de mejoras depende de varios factores como el patrón de acceso, la renovación de datos y el tipo de datos. 

toocancel un trabajo de rehidratación, puede usar el cmdlet de PowerShell de Hola. Si lo desea trabajos rehidratación de toopermanently disable para todos Hola restauraciones futuras, [póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>¿Cómo toouse Hola catálogo de copia de seguridad

Hola **catálogo de copia de seguridad** hoja proporciona una consulta que le ayuda a toonarrow la selección de conjunto de copia de seguridad. Puede filtrar Hola conjuntos de copia que se recuperan en función de hello parámetros siguientes:

* **El intervalo de tiempo** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.
* **Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.
* **Directiva de copia de seguridad** o **volumen** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.

Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:

* **Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.
* **Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube. Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola. Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.
* **Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.
* **Crear en** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola. 
* **Volúmenes** -Hola número de volúmenes asociados con el conjunto de copia de seguridad de Hola.
* **Inicia** : las copias de seguridad de Hola se pueden iniciar automáticamente según la programación de tooa o manualmente por el usuario. (Puede usar copias de seguridad de tooschedule de una directiva de copia de seguridad. Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad interactiva o a petición.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Cómo toorestore su volumen de StorSimple desde una copia de seguridad

Puede usar hello **catálogo de copia de seguridad** toorestore hoja su volumen de StorSimple desde una copia de seguridad específica. Tenga en cuenta, sin embargo, que restaurar un volumen volverá al estado toohello Hola volumen en que estaba cuando se realizó la copia de seguridad de Hola. Se perderán los datos que se agregaron después de la operación de copia de seguridad de Hola.

> [!WARNING]
> Restaurar a partir de una copia de seguridad sustituirá los volúmenes existentes de copia de seguridad de Hola Hola. Esto puede provocar la pérdida de Hola de los datos que se escriben después de que se realizó la copia de seguridad de Hola.


### <a name="toorestore-your-volume"></a>toorestore el volumen
1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **catálogo de copia de seguridad**.

2. Seleccione una copia de seguridad de la siguiente manera:
   
   1. Especifique el intervalo de tiempo de Hola.
   2. Seleccionar dispositivo apropiados de Hola.
   3. En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.
   4. Haga clic en **aplicar** tooexecute esta consulta.

    Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.
   
    ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Expandir tooview Hola asociado volúmenes de hello conjunto de copia de seguridad. Estos volúmenes deben realizarse sin conexión en el host de Hola y el dispositivo antes de que pueda restaurarlos al completo. Obtener acceso a los volúmenes de hello en hello **volúmenes** hoja de su dispositivo y, a continuación, Hola de seguimiento de los pasos de [desconectar un volumen](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ellos sin conexión.
   
   > [!IMPORTANT]
   > Asegúrese de que haya desconectado Hola volúmenes en el host de hello en primer lugar, antes de poner sin conexión los volúmenes de hello en dispositivo Hola. Si no se realiza sin conexión los volúmenes de hello en el host de hello, pudieron causar daños toodata.
   
4. Desplácese atrás toohello **catálogo de copia de seguridad** pestaña y seleccione un conjunto de copia de seguridad. Haga clic en y, a continuación, desde el menú contextual de hello, seleccione **restaurar**.

    ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Se le pedirá confirmación. Hola de revisión restaura la información y, a continuación, active la casilla de verificación de confirmación de Hola.
   
    ![Página de confirmación](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Haga clic en **Restaurar**. Este comando inicia un trabajo de restauración que se puede ver mediante el acceso a hello **trabajos** página.

    ![Página de confirmación](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Una vez completada la restauración de hello, compruebe que el contenido de Hola de los volúmenes se reemplaza por volúmenes de copia de seguridad de Hola.


## <a name="if-hello-restore-fails"></a>Si restaura Hola se produce un error

Recibirá una alerta si Hola restaurar operación provocará un error por cualquier motivo. Si esto ocurre, la actualización de hello lista de reserva tooverify que Hola copia de seguridad sigue siendo válida. Si la copia de seguridad de hello es válido y se restaura desde la nube de hello, problemas de conectividad podrían estar causando problema Hola.

Hola toocomplete la operación de restauración, desconecte el volumen hello en el host de Hola y vuelva a intentar la operación de restauración de Hola. Tenga en cuenta que el proceso de restauración de los datos de volumen de toohello las modificaciones que se realizaron durante el saludo se perderá.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[StorSimple administrar volúmenes](storsimple-8000-manage-volumes-u2.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

