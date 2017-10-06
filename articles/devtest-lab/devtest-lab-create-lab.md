---
title: "aaaCreate un laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Creación de un laboratorio en Azure DevTest Labs para máquinas virtuales"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Creación de un laboratorio con Laboratorios de desarrollo y pruebas de Azure
Una práctica de laboratorios de desarrollo y pruebas de Azure es la infraestructura de Hola que abarca el proceso de un grupo de recursos, como máquinas virtuales (VM), que permite una mejor administrar esos recursos especificando los límites y cuotas. Este artículo le guiará por el proceso de Hola de creación de un laboratorio mediante Hola portal de Azure.

## <a name="prerequisites"></a>Requisitos previos
toocreate un laboratorio, debe:

* Una suscripción de Azure. toolearn acerca de las opciones de compra de Azure, consulte [cómo toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) o [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). Debe ser propietario de Hola de laboratorio de hello suscripción toocreate Hola.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Pasos toocreate un laboratorio de prácticas de desarrollo y pruebas de Azure
Hola siguientes pasos muestra cómo toouse Hola toocreate portal Azure un laboratorio de prácticas de desarrollo y pruebas de Azure. 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. En menú principal de hello en el lado izquierdo de hello, seleccione **más servicios** (final Hola de hello lista).

    ![Opción del menú Más servicios](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. En lista de hello de servicios disponibles, **laboratorios de desarrollo y pruebas**.
1. En hello **laboratorios de desarrollo y pruebas** hoja, seleccione **agregar**.
   
    ![Incorporación de un laboratorio](./media/devtest-lab-create-lab/add-lab-button.png)

1. En hello **crear un laboratorio de desarrollo y pruebas** hoja:
   
    1. Escriba un **nombre de laboratorio** para laboratorio nuevo Hola.
    2. Seleccione hello **suscripción** tooassociate con laboratorio Hola.
    3. Seleccione un **ubicación** en el laboratorio de hello toostore.
    4. Seleccione **apagado automático** toospecify si desea tooenable - y definir parámetros de Hola para - Hola automática apagar de máquinas virtuales del laboratorio Hola todos los. Hello apagado automático es principalmente un ahorro de costos característica mediante el cual puede especificar cuándo desea Hola VM tooautomatically apagarse. Puede cambiar la configuración de cierre automáticamente después de crear el laboratorio de hello siguiendo los pasos de Hola que se describen en el artículo de hello, [administrar todas las directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Seleccione **tooDashboard Pin** si desea un acceso directo de hello tooappear de laboratorio en el panel del portal Hola.
    6. Seleccione **opciones de automatización** tooget Azure Resource Manager plantillas para la automatización de la configuración. 
    7. Seleccione **Crear**. Después de seleccionar **crear**, hello **laboratorios de desarrollo y pruebas** muestra hoja. Puede supervisar Hola estado del proceso de creación de laboratorio de hello, inspeccionando hello **notificaciones** área. Una vez completado, actualización Hola página toosee Hola recién creado del laboratorio lista Hola de laboratorios.  
    
    ![Creación de una hoja de laboratorio](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez que haya creado el laboratorio, incluimos algunos tooconsider de pasos siguiente:

* [Laboratorio de acceso seguro tooa](devtest-lab-add-devtest-user.md).
* [Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)
* [Creación de una plantilla de laboratorio](devtest-lab-create-template.md)
* [Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)
* [Agregar una máquina virtual con el laboratorio de artefactos tooa](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

