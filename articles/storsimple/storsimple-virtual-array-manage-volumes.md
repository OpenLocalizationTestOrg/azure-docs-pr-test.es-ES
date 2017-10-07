---
title: "volúmenes de aaaManage en StorSimple Virtual Array | Documentos de Microsoft"
description: "Hola, Administrador de dispositivos de StorSimple se describe y se explica cómo toouse se toomanage volúmenes en la matriz Virtual de StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Volúmenes de toomanage de servicio de administrador de dispositivos de StorSimple de uso en hello StorSimple Virtual Array

## <a name="overview"></a>Información general

Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar los volúmenes en la matriz Virtual de StorSimple.

Hola servicio Administrador de dispositivos de StorSimple es una extensión en hello portal de Azure que le permite administrar la solución de StorSimple de una única interfaz web. En los volúmenes y recursos compartidos de toomanaging de suma, puede usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar dispositivos, ver alertas y ver y administrar directivas de copia de seguridad y el catálogo de copia de seguridad de Hola.

## <a name="volume-types"></a>Tipos de volúmenes

Los volúmenes de StorSimple pueden ser:

* **Anclado localmente**: datos de estos volúmenes permanece en la matriz de hello en todo momento y no volcarse toohello en la nube.
* **En niveles**: datos de estos volúmenes pueden retrasar toohello en la nube. Cuando se crea un volumen en capas, aproximadamente el 10% del espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola. Por ejemplo, si ha aprovisionado un volumen de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos. A su vez, esto implica que si se ejecuta fuera de todo el espacio local en hello en dispositivo hello, no se puede aprovisionar un volumen en capas (porque Hola 10% necesarios en hello local nivel no estará disponible).

### <a name="provisioned-capacity"></a>Capacidad aprovisionada
Consulte toohello máxima capacidad aprovisionada para cada tipo de volumen en la tabla siguiente.

| **Identificador de límites**                                       | **Límite**     |
|------------------------------------------------------------|---------------|
| Tamaño mínimo de un volumen en capas                            | 500 GB        |
| Tamaño máximo de un volumen en capas                            | 5 TB          |
| Tamaño mínimo de un volumen anclado localmente                    | 50 GB         |
| Tamaño máximo de un volumen anclado localmente                    | 500 GB        |

## <a name="hello-volumes-blade"></a>hoja de volúmenes de Hola
Hola **volúmenes** menú en la hoja de resumen de servicio de StorSimple muestra la lista de Hola de volúmenes de almacenamiento en una matriz StorSimple y permitiéndole toomanage ellos.

![Hoja Volúmenes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Un volumen se compone de una serie de atributos:

* **Nombre del volumen** : un nombre descriptivo que debe ser únicos y ayuda a identificar el volumen de Hola.
* **Estado** : puede estar conectado o desconectado. Si un volumen está sin conexión, no es visible tooinitiators (servidores) que se permiten acceso toouse Hola volumen.
* **Tipo de** : indica si el volumen de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.
* **Capacidad** : especifica la cantidad de Hola de datos que se usan como toohello en comparación con la cantidad total de datos que se pueden almacenar por el iniciador de hello (servidor).
* **Copia de seguridad** : en el caso de hello StorSimple Virtual Array, se habilitan automáticamente todos los volúmenes de copia de seguridad.
* **Hosts conectados** – especifica iniciadores de hello (servidores) que se permiten acceso toothis volumen.

![Detalles de volúmenes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:

* Agregar un volumen
* Modificar un volumen
* Desconectar un volumen
* Eliminar un volumen

## <a name="add-a-volume"></a>Agregar un volumen

1. En la hoja de resumen de hello StorSimple servicio, haga clic en **+ agregar volumen** de barra de comandos de Hola. Esto abrirá hello **agregar volumen** hoja.
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. Hola **agregar volumen** hoja, Hola siguientes:
   
   * Hola **nombre del volumen** , a continuación, escriba un nombre único para su volumen. nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.
   * Hola **tipo** lista desplegable lista, especifique si toocreate una **"en capas"** o **anclado localmente** volumen. Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Volumen anclado localmente**. Para todos los demás datos, seleccione volumen **en capas**.
   * Hola **capacidad** , especifique el tamaño de hello del volumen de Hola. Un volumen en capas debe tener entre 500 GB y 5 TB, mientras que un volumen anclado localmente debe oscilar entre 50 GB y 500 GB.
   * * Haga clic en **hosts conectados**, seleccione un acceso control registro (ACR) correspondiente toohello iniciador iSCSI que desee tooconnect toothis volumen y, a continuación, haga clic en **seleccione**.
3. tooadd un nuevo host conectado, haga clic en **agregar nueva**, escriba un nombre de host de Hola y su iSCSI (IQN) nombre completo y, a continuación, haga clic en **agregar**.
   
    ![Agregar volumen](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Cuando haya terminado de configurar el volumen, haga clic en **Crear**. Se creará un volumen con hello especificado configuración y verá una notificación durante la creación correcta de Hola de Hola igual. De forma predeterminada, copia de seguridad se habilitarán para volumen Hola.
5. tooconfirm que Hola volumen estaba se creó correctamente, vaya toohello **volúmenes** hoja. Debería ver los volúmenes de Hola que aparecen.
   
    ![Creación de volumen correcta](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Modificar un volumen

Modificar un volumen cuando necesita toochange Hola hosts que tienen acceso a los volúmenes de Hola. Hello otros atributos de un volumen no se puede modificar una vez que se ha creado el volumen de Hola.

#### <a name="toomodify-a-volume"></a>toomodify un volumen

1. De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría toomodify.
2. **Seleccione** Hola volumen y haga clic en **hosts conectados** tooview Hola host conectado actualmente y modifíquelo tooa otro servidor.
   
    ![Modificación del volumen](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Guarde los cambios haciendo clic en hello **guardar** barra de comandos. Se aplicará la configuración especificada y verá una notificación.

## <a name="take-a-volume-offline"></a>Desconectar un volumen

Puede que necesite tootake un volumen sin conexión cuando piensa toomodify lo o delete. Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura. Necesitará tootake Hola volumen sin conexión en el host de hello, así como en el dispositivo de Hola.

#### <a name="tootake-a-volume-offline"></a>tootake un volumen sin conexión

1. Asegúrese de que volumen hello en cuestión no está en uso antes de desconectarlo.
2. Desconecte volumen hello en el host de hello primero. Esto elimina cualquier riesgo potencial de daños en los datos en el volumen de Hola. Para obtener pasos específicos, consulte las instrucciones de toohello para el sistema operativo host.
3. Después de volumen de hello en el host de hello está sin conexión, desconecte el volumen de hello en la matriz de hello sin conexión mediante la realización de hello pasos:
   
   * De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría tootake sin conexión.
   * **Seleccione** Hola volumen y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **desconectar**.
     
        ![Volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Revise la información de Hola Hola **desconectar** hoja y confirmar la aceptación de operación de Hola. Haga clic en **desconectar** volumen tootake Hola. Verá una notificación de Hola la operación en curso.
   * tooconfirm que el volumen de hello correctamente se dejó sin conexión, vaya toohello **volúmenes** hoja. Debería ver estado de saludo del volumen de hello como sin conexión.
     
       ![Confirmación de volumen desconectado](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Eliminar un volumen

> [!IMPORTANT]
> Puede eliminar un volumen solo si está desconectado.
> 
> 

Completar Hola siguiendo los pasos toodelete un volumen.

#### <a name="toodelete-a-volume"></a>toodelete un volumen

1. De hello **volúmenes** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el volumen que le gustaría toodelete.
2. **Seleccione** Hola volumen y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **eliminar**.
   
    ![Eliminar volumen](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Comprobar el estado de saludo del volumen de Hola que desea toodelete. Si desea toodelete de volumen de hello no está desconectado, dejarlo pasos hello en primer lugar, siguiente sin conexión [desconectar un volumen](#take-a-volume-offline).
4. Cuando se le pida confirmación en hello **eliminar** hoja, acepte la confirmación de Hola y haga clic en **eliminar**. volumen de Hola se eliminará y Hola **volúmenes** hoja mostrará la lista de hello actualizado de volúmenes dentro de la matriz virtual Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[clonar un volumen de StorSimple](storsimple-virtual-array-clone.md).

