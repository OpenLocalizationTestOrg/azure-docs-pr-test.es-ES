---
title: "Introducción al administrador de datos de Azure StorSimple aaaMicrosoft | Documentos de Microsoft"
description: "Proporciona información general de hello servicio de administrador de datos de StorSimple (vista previa privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Información general sobre el servicio StorSimple Data Manager (versión preliminar privada)

## <a name="overview"></a>Información general

StorSimple de Microsoft Azure es una solución de almacenamiento de nube híbrida que direcciones Hola complejidades de los datos no estructurados que suelen estar asociadas con recursos compartidos de archivos. StorSimple usa almacenamiento en la nube como solución local de una extensión de hello y automáticamente de capas de datos a través de un almacenamiento local hello y almacenamiento en la nube. Integra la protección de datos, con local e instantáneas en la nube, elimina la necesidad de Hola de una infraestructura de almacenamiento desorganizados. Archivado y recuperación ante desastres también es sin problemas con la nube de hello actúa como una ubicación fuera del sitio.

Servicios de transformación de datos de Hola que estamos incorporando en este documento, se permite tooseamlessly acceso hello StorSimple datos en la nube de Hola. Este servicio proporciona datos de las API tooextract de StorSimple y presentar tooother Azure servicios en formatos que pueden utilizarse con facilidad. formatos de Hello admitidos en esta versión preliminar son blobs de Azure y los activos de servicios multimedia de Azure. Esta transformación permite tooeasily conectar servicios como datos de toooperate de servicios multimedia de Azure, HDInsight de Azure, aprendizaje automático de Azure y búsqueda de Azure en el dispositivo de StorSimple 8000 series local.

A continuación se muestra un diagrama de bloques de alto nivel que lo ilustra.

![Diagrama de alto nivel](./media//storsimple-data-manager-overview/high-level-diagram.png)

En este documento se explica cómo puede suscribirse a una versión preliminar privada de este servicio. También se explica cómo puede usar esta aplicación de servicio toowrite que usan datos de StorSimple y otros servicios de Azure en la nube de Hola.

## <a name="sign-up-for-data-manager-preview"></a>Suscripción para una versión preliminar de Data Manager
Antes de registrarse para el servicio de administrador de datos de hello, revise Hola siguiendo los requisitos previos.

### <a name="prerequisites"></a>Requisitos previos

En este ejercicio se supone que dispone de:
* una suscripción a Azure activa
* acceso tooa registrado el dispositivo de StorSimple 8000 series
* todos los Hola claves asociadas con el dispositivo de la serie StorSimple 8000 Hola.

### <a name="sign-up"></a>Suscripción

Hola, Administrador de datos de StorSimple está en vista previa privada. Lleve a cabo Hola siguiendo los pasos toosign para disfrutar de una vista previa privada de este servicio:

1.  Inicie sesión en hello portal de Azure con la extensión de administrador de datos de StorSimple de hello en: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Utilice la toolog las credenciales de Azure en.

2.  Haga clic en hello  **+**  toocreate icono un servicio. Haga clic en **almacenamiento** y, a continuación, haga clic en **vea todos los** en la hoja de Hola que se abre.

    ![Buscar icono de StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Verá el icono de administrador de datos de StorSimple de Hola.

    ![Seleccionar icono de StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Haga clic en el icono de StorSimple Data Manager y, después, en **Create** (Crear). Seleccione la suscripción de Hola que desee tooenable de vista previa privada de hello y, a continuación, haga clic en **suscribirme!**

    ![Suscribirme](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Este modo envía una solicitud tooonboard. Dicha incorporación se realizará lo antes posible. Una vez habilitada la suscripción, ya se puede crear un servicio StorSimple Data Manager.

6. tooeasily tener acceso a servicio de administrador de datos de StorSimple de hello, haga clic en toopin de icono de estrella de Hola tooyour favoritos.

    ![Acceder a StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Pasos siguientes

[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).
