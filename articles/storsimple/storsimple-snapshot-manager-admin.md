---
title: "administración de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Proporciona información general y vínculos toomore información acerca de las tareas de administración de administrador de instantáneas StorSimple soluciones y flujos de trabajo."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>Usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple

## <a name="overview"></a>Información general
Administrador de instantáneas StorSimple es un complemento de Microsoft Management Console (MMC) que simplifica la protección de datos y la administración de las copias de seguridad en un entorno de Microsoft Azure StorSimple. Con el Administrador de instantáneas de StorSimple, puede administrar datos de Microsoft Azure StorSimple en el centro de datos de Hola y en la nube de hello como una solución de almacenamiento de información integrada y, por tanto, lo que simplifica los procesos de copia de seguridad y reducen los costos.

consola de administración central de administrador de instantáneas StorSimple Hola le permite toocreate coherente, momento en copias de seguridad de local y datos en la nube. Por ejemplo, puede usar la consola de Hola para:

* Configurar, crear copias de seguridad y eliminar volúmenes.
* Configurar el volumen tooensure de grupos que la copia de seguridad de datos es coherente con la aplicación.
* Administrar directivas de copia de seguridad, con el fin de que las copias de seguridad de los datos se realicen según una programación predeterminada.
* Crear copias independientes de datos, que se pueden almacenar en la nube de Hola y usados para la recuperación ante desastres.

Este artículo proporcionan vínculos tootutorials que describen el Administrador de instantáneas StorSimple y cómo toouse se toocomplete las tareas de administración del sistema y los flujos de trabajo.

* Para obtener más información acerca de la arquitectura y los componentes de Administrador de instantáneas StorSimple, consulte [¿Qué es el Administrador de instantáneas StorSimple?](storsimple-what-is-snapshot-manager.md) 
* toodownload Administrador de instantáneas de StorSimple, vaya demasiado[página de descarga del Administrador de instantáneas StorSimple hello](https://www.microsoft.com/download/details.aspx?id=44220).
* Para ver los procedimientos de implementación del Administrador de instantáneas de StorSimple, vaya demasiado[implementar Administrador de instantáneas de StorSimple](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> No puede usar el Administrador de instantáneas StorSimple toomanage Microsoft Azure StorSimple Virtual matrices (también conocido como StorSimple virtuales dispositivos locales).


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>Tareas y flujos de trabajo de Administrador de instantáneas StorSimple
Puede usar hello toomonitor de administrador de instantáneas StorSimple y administrar trabajos de copia de seguridad actuales, programados y completados. Además, el Administrador de instantáneas StorSimple proporciona un catálogo de copias de seguridad too64 completado. Puede usar Hola catálogo toofind y restaurar volúmenes o archivos individuales. 

| IF desea tooDO THIS... | USE ESTE TUTORIAL... |
|:--- |:--- |
| Más información sobre Administrador de instantáneas StorSimple |[¿Qué es Administrador de instantáneas StorSimple? ](storsimple-what-is-snapshot-manager.md) |
| Instalar Administrador de instantáneas StorSimple<br>Reinstalar StorSimple Snapshot Manager<br>Quitar Administrador de instantáneas StorSimple |[Implementación de Administrador de instantáneas StorSimple](storsimple-snapshot-manager-deployment.md) |
| Usar los menús y las características de Administrador de instantáneas StorSimple:<ul><li>Barra de menús</li><li>Barra de herramientas</li><li>Panel de Ámbito</li><li>Panel de Resultados</li><li>Panel de Acciones</li><li>Métodos abreviados y navegación mediante el teclado</li></ul> |[Interfaz de usuario de Administrador de instantáneas StorSimple](storsimple-use-snapshot-manager.md) |
| Use Hola comunes MMC características incluidas en el Administrador de instantáneas de StorSimple:<ul><li>Ver</li><li>Nueva ventana desde aquí</li><li>Actualizar</li><li>Exportar lista</li><li>Ayuda</li></ul> |[Usar acciones del menú Hola MMC en el Administrador de instantáneas StorSimple](storsimple-snapshot-manager-mmc-menu.md) |
| Incorporación o remplazo de un dispositivo<br>Conexión de un dispositivo<br>Comprobación de los grupos de volúmenes importados<br>Actualización de los dispositivos conectados<br>Autenticar un dispositivo<br>Vista de detalles de dispositivo<br>Eliminación de una configuración de dispositivo<br>Cambiar una contraseña de dispositivo<br>Reemplazo de un dispositivo con errores<br> |[Use el Administrador de instantáneas StorSimple tooconnect y administrar dispositivos de StorSimple](storsimple-snapshot-manager-manage-devices.md) |
| Montaje de volúmenes<br>Ver información acerca de volúmenes<br>Eliminar un volumen<br>Volver a examinar volúmenes<br>Configuración y copia de seguridad de un volumen básico<br>Configurar y realizar copia de seguridad de un volumen reflejado dinámico |[Use el Administrador de instantáneas StorSimple tooview y administrar volúmenes](storsimple-snapshot-manager-manage-volumes.md) |
| Visualización de grupos de volúmenes<br>Crear un grupo de volúmenes<br>Realizar una copia de seguridad de un grupo de volúmenes<br>Editar un grupo de volúmenes<br>Eliminar un grupo de volúmenes |[Use el Administrador de instantáneas StorSimple toocreate y administrar grupos de volúmenes](storsimple-snapshot-manager-manage-volume-groups.md) |
| Creación de una directiva de copia de seguridad <br>Edición de una directiva de copia de seguridad<br>Eliminación de una directiva de copia de seguridad |[Use el Administrador de instantáneas StorSimple toocreate y administrar las directivas de copia de seguridad](storsimple-snapshot-manager-manage-backup-policies.md) |
| Ver y administrar los trabajos de copia de seguridad programados<br>Ver y administrar los trabajos de copia de seguridad recientes<br>Ver y administrar trabajos de copia de seguridad en ejecución en ese momento |[Use el Administrador de instantáneas StorSimple tooview y administrar los trabajos de copia de seguridad](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Restauración de un volumen<br>Clonación de un volumen o un grupo de volúmenes<br>Eliminación de una copia de seguridad<br>Recuperación de un archivo<br>Restaurar base de datos de administrador de instantáneas StorSimple Hola |[Catálogo de copia de seguridad de hello toomanage use el Administrador de instantáneas StorSimple](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Pasos siguientes
[Descarga de Administrador de instantáneas StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

