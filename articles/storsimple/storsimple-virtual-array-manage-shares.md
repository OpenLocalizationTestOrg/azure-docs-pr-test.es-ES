---
title: recursos compartidos de StorSimple Virtual Array aaaManage | Documentos de Microsoft
description: "Hola, Administrador de dispositivos de StorSimple se describe y se explica cómo toouse se toomanage los recursos compartidos de la matriz Virtual de StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Usar recursos compartidos toomanage de servicio de administrador de dispositivos de StorSimple de hello en hello StorSimple Virtual Array

## <a name="overview"></a>Información general

Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar recursos compartidos en la matriz Virtual de StorSimple.

Hola servicio Administrador de dispositivos de StorSimple es una extensión en hello portal de Azure que le permite administrar la solución de StorSimple de una única interfaz web. En volúmenes y recursos compartidos de toomanaging de suma, puede usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar dispositivos, ver las alertas, administrar directivas de copia de seguridad y administrar el catálogo de copia de seguridad de Hola.

## <a name="share-types"></a>Tipos de recursos compartidos

Los recursos compartidos de StorSimple pueden ser de uno de los siguientes tipos:

* **Anclado localmente**: datos de estos recursos compartidos permanece en la matriz de hello en todo momento y no volcarse toohello en la nube.
* **En niveles**: datos de estos recursos compartidos pueden retrasar toohello en la nube. Cuando se crea un recurso compartido en capas, aproximadamente el 10% del espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola. Por ejemplo, si ha aprovisionado a un recurso compartido de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos. A su vez, esto implica que si se ejecuta fuera de todo el espacio local en hello en dispositivo hello, no se puede aprovisionar un recurso compartido en capas (porque Hola 10% necesarios en hello local nivel no estará disponible).

### <a name="provisioned-capacity"></a>Capacidad aprovisionada

Consulte toohello máxima capacidad aprovisionada para cada tipo de recurso compartido en la tabla siguiente.

| **Identificador de límites** | **Límite** |
| --- | --- |
| Tamaño mínimo de un recurso compartido en capas |500 GB |
| Tamaño máximo de un recurso compartido en capas |20 TB |
| Tamaño mínimo de un recurso compartido anclado localmente |50 GB |
| Tamaño máximo del recurso compartido anclado localmente |2 TB |

## <a name="hello-shares-blade"></a>hoja de recursos compartidos de Hola

Hola **recursos compartidos** menú en la hoja de resumen de servicio de StorSimple muestra la lista de Hola de recursos compartidos de almacenamiento en una matriz StorSimple y permitiéndole toomanage ellos.

![Hoja Recursos compartidos](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Un recurso compartido se compone de una serie de atributos:

* **Nombre del recurso compartido** : un nombre descriptivo que debe ser únicos y ayuda a identificar el recurso compartido de Hola.
* **Estado** : puede estar conectado o desconectado. Si un recurso compartido está desconectado, los usuarios del recurso compartido de hello no estarán tooaccess capaz de él.
* **Tipo de** : indica si el recurso compartido de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.
* **Capacidad** : especifica la cantidad de Hola de datos que se usan como toohello en comparación con la cantidad total de datos que pueden almacenarse en el recurso compartido de Hola.
* **Descripción** – una configuración opcional que ayuda a describir el recurso compartido de Hola.
* **Permisos** -Hola NTFS permisos toohello recurso compartido que se pueden administrar a través del explorador de Windows.
* **Copia de seguridad** : en el caso de hello StorSimple Virtual Array, se habilitan automáticamente todos los recursos compartidos para copia de seguridad.

![Detalles del recurso compartido](./media/storsimple-virtual-array-manage-shares/share-details.png)

Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:

* Agregar un recurso compartido
* Modificación de un recurso compartido
* Desconexión de un recurso compartido
* Eliminación de un recurso compartido

## <a name="add-a-share"></a>Agregar un recurso compartido

1. En la hoja de resumen de hello StorSimple servicio, haga clic en **+ recurso compartido de agregar** de barra de comandos de Hola. Esto abrirá hello **recurso compartido de agregar** hoja.

    ![Incorporación de un recurso compartido](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. Hola **recurso compartido de agregar** hoja, Hola siguientes:
   
    1. Hola **nombre de recurso compartido** , escriba un nombre único para el recurso compartido. nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.

    2. Opcional **descripción** para el recurso compartido de Hola. Descripción de Hello le ayudará a identificar los propietarios del recurso compartido de Hola.

    3. Hola **tipo** lista desplegable lista, especifique si toocreate una **"en capas"** o **anclado localmente** compartir. Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Recurso compartido anclado localmente**. Para todos los demás datos, seleccione **Recurso compartido en capas**.

    4. Hola **capacidad** , especifique el tamaño de Hola de recurso compartido de Hola. Un recurso compartido en capas debe tener entre 500 GB y 20 TB, y uno anclado localmente debe tener entre 50 GB y 2 TB.

    5. Hola **establezca predeterminados todos los permisos** , a continuación, asignar Hola permisos toohello, usuario o grupo de Hola que tenga acceso a este recurso compartido. Especifique Hola nombre de usuario de Hola o grupo de usuarios de hello en  _john@contoso.com_  formato. Se recomienda usar un tooaccess de privilegios de administrador de usuario grupo (en lugar de un solo usuario) tooallow estos recursos compartidos. Después de haber asignado permisos de hello aquí, a continuación, puede usar estos permisos toomodify del explorador de archivos.
3. Cuando haya terminado de configurar el recurso compartido, haga clic en **Crear**. Se creará un recurso compartido con hello especificado configuración y verá una notificación. De forma predeterminada, copia de seguridad se habilitará para el recurso compartido de Hola.
4. tooconfirm que Hola recurso compartido estaba se creó correctamente, vaya toohello **recursos compartidos** hoja. Debería ver Hola compartir enumeradas.
   
    ![Creación de un recurso compartido correcta](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Modificación de un recurso compartido

Modificar un recurso compartido cuando necesite descripción de hello toochange del recurso compartido de Hola. Ninguna otra propiedad de recurso compartido puede modificarse una vez creado el recurso compartido de Hola.

#### <a name="toomodify-a-share"></a>toomodify un recurso compartido

1. De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el recurso compartido que le gustaría toomodify.
2. **Seleccione** Hola descripción actual del recurso compartido tooview hello y modificarlo.
3. Guarde los cambios haciendo clic en hello **guardar** barra de comandos. Se aplicará la configuración especificada y verá una notificación.
   
    ![ Editar recurso compartido](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Desconexión de un recurso compartido

Puede que necesite tootake sin conexión un recurso compartido si tiene previsto toomodify lo o delete. Cuando un recurso compartido está desconectado, no está disponible para el acceso de lectura y escritura. Necesitará tootake Hola recursos compartidos sin conexión en el host de hello, así como en el dispositivo de Hola.

#### <a name="tootake-a-share-offline"></a>tootake un recurso compartido sin conexión

1. Asegúrese de que ese recurso compartido de hello en cuestión no está en uso antes de desconectarlo.
2. Quitarle participación de hello en la matriz de hello sin conexión mediante la realización de hello pasos:
   
    1. De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en qué Hola reside el recurso compartido que le gustaría tootake sin conexión.

    2. **Seleccione** recurso compartido de Hola y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **desconectar**.
     
        ![Recurso compartido sin conexión](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Revise la información de Hola Hola **desconectar** hoja y confirmar la aceptación de operación de Hola. Haga clic en **desconectar** compartir de hello tootake sin conexión. Verá una notificación de Hola la operación en curso.

    4. tooconfirm que Hola recurso compartido se realizó correctamente sin conexión, vaya toohello **recursos compartidos** hoja. Debería ver estado de saludo del recurso compartido de hello como sin conexión.

## <a name="delete-a-share"></a>Eliminación de un recurso compartido

> [!IMPORTANT]
> Puede eliminar un recurso compartido solo si está desconectado.


Hola completa siguiendo los pasos toodelete un recurso compartido.

#### <a name="toodelete-a-share"></a>toodelete un recurso compartido

1. De hello **recursos compartidos** establecer en la hoja de resumen de servicio de StorSimple de hello, seleccione Hola matriz virtual en el recurso compartido de hello desea toodelete reside.
2. **Seleccione** recurso compartido de Hola y haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **eliminar**.
   
    ![Eliminación del recurso compartido](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Comprobar el estado de saludo del recurso compartido de Hola que desea toodelete. Si desea toodelete de recurso compartido de hello no está desconectado, desconéctelo primero. Siga los pasos de hello en [poner sin conexión un recurso compartido de](#take-a-share-offline).
4. Cuando se le pida confirmación en hello **eliminar** hoja, acepte la confirmación de Hola y haga clic en **eliminar**. recurso compartido de Hola se eliminará y Hola **recursos compartidos** hoja muestra la lista de hello actualizado de recursos compartidos dentro de la matriz virtual Hola.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[clonar un recurso compartido de StorSimple](storsimple-virtual-array-clone.md).

