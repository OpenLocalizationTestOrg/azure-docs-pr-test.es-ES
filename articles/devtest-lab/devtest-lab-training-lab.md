---
title: aaaUse laboratorios de desarrollo y pruebas de Azure para el entrenamiento | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse laboratorios de desarrollo y pruebas de Azure para escenarios de aprendizaje."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Uso de Azure DevTest Labs para entrenamiento
Laboratorios de desarrollo y pruebas de Azure puede ser usado tooimplement muchos escenarios claves de prueba/toodev de suma. Uno de estos escenarios es tooset un laboratorio para el entrenamiento. Laboratorios de desarrollo y pruebas de Azure permite toocreate un laboratorio donde se pueden especificar plantillas personalizadas que cada aprendiz puede usar entornos de toocreate idénticos y aislado para el entrenamiento. Puede aplicar tooensure directivas que entornos de entrenamiento son aprendiz tooeach disponible solo cuando se necesiten y contienen suficientes recursos - como máquinas virtuales - necesarias para el entrenamiento de Hola. Por último, puede compartir fácilmente laboratorio Hola con prácticas, que puede tener acceso a un solo clic.

![Uso de DevTest Labs para entrenamiento](./media/devtest-lab-training-lab/devtest-lab-training.png)

Laboratorios de desarrollo y pruebas Azure cumple Hola según los requisitos que son necesarios tooconduct entrenamiento en cualquier entorno virtual: 

* Los aprendices no pueden ver las máquinas virtuales creadas por otros aprendices
* Cada máquina de entrenamiento debe ser idéntica
* Los aprendices pueden aprovisionar rápidamente sus entornos de entrenamiento
* Controlar los costos al garantizar que prácticas no pueden obtener más máquinas virtuales de las se necesitan para el entrenamiento de Hola y también apagar las máquinas virtuales cuando no está utilizando
* Compartir fácilmente el laboratorio de entrenamiento de hello con cada aprendiz
* Laboratorio de entrenamiento de Hola de reutilización y otra vez

En este artículo, aprenderá acerca de diversas características de laboratorios de desarrollo y pruebas de Azure que se pueden usar toomeet Hola descrito anteriormente requerimientos de capacitación y pasos detallados que puede seguir tooset un laboratorio para el entrenamiento.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Implementación de un entrenamiento con Azure DevTest Labs
1. **Cree el laboratorio de Hola** 
   
    Laboratorios son Hola punto inicial en los laboratorios de desarrollo y pruebas de Azure. Una vez que cree un laboratorio, puede realizar tareas tales como agregar laboratorio toohello de usuarios (prácticas), los costos de conjunto de directivas toocontrol, definen imágenes de máquina virtual que pueden crear rápidamente y mucho más.   
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de un laboratorio con Laboratorios de desarrollo y pruebas de Azure](devtest-lab-create-lab.md) |Obtenga información acerca de cómo toocreate un laboratorio de prácticas de desarrollo y pruebas de Azure de Hola portal de Azure. |
2. **Creación de máquinas virtuales de entrenamiento en cuestión de minutos mediante imágenes listas para usar de Marketplace e imágenes personalizadas** 
   
    Puede elegir imágenes prediseñadas desde una gran variedad de imágenes en hello Azure Marketplace y ponerlos a disposición de prácticas de hello en laboratorio Hola. Si imágenes prediseñadas hello no satisfacen sus necesidades, puede crear una imagen personalizada mediante la creación de un máquina virtual con una imagen listos para su uso de Azure Marketplace, instalar todo el software de Hola que necesita para el entrenamiento de Hola y conseguir un ahorro Hola VM como imagen personalizada en el laboratorio de Hola de laboratorio. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Configuración de imágenes de Azure Marketplace](devtest-lab-configure-marketplace-images.md) |Obtenga información acerca de cómo puede imágenes de Azure Marketplace de lista blanca de direcciones; hacer que estén disponibles para las imágenes de Hola de selección única que desee para el entrenamiento de Hola. |
   | [Creación de una imagen personalizada](devtest-lab-create-template.md) |Crear una imagen personalizada mediante la instalación previamente el software de Hola que necesitará para el entrenamiento de Hola para que prácticas pueden crear rápidamente una máquina virtual con una imagen personalizada hello. |
3. **Creación de plantillas reutilizables para las máquinas de entrenamiento** 
   
    Una fórmula de laboratorios de desarrollo y pruebas de Azure es que una lista de valores de propiedad predeterminados utiliza toocreate una máquina virtual. Puede crear una fórmula en el laboratorio de hello escogiendo una imagen, un tamaño de memoria virtual (una combinación de CPU y RAM) y una red virtual. Cada aprendiz puede ver fórmula hello en el laboratorio de Hola y usarlo toocreate una máquina virtual. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Administrar las fórmulas de laboratorios de desarrollo y pruebas toocreate máquinas virtuales](devtest-lab-manage-formulas.md) |Aprenda cómo crear una fórmula en el laboratorio seleccionando una imagen, un tamaño de máquina virtual (una combinación de CPU y RAM) y una red virtual. |
4. **Control de los costos**
   
    Azure laboratorios de desarrollo y pruebas permite tooset una directiva de hello laboratorio toospecify Hola número máximo de máquinas virtuales que se pueden crear mediante un aprendiz en laboratorio Hola. 
   
    Si se realiza el entrenamiento de día y desea toostop todas las máquinas virtuales de hello en un momento determinado del día de Hola y automáticamente reinícielos Hola siguiente día, puede fácilmente hacerlo por apagado automático de configuración y directivas en el laboratorio de Hola de inicio a automático. 
   
    Por último, una vez completado entrenamiento puede eliminar todas las máquinas virtuales de Hola de a la vez mediante la ejecución de un script de PowerShell único. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md) |Controlar los costos mediante el establecimiento de directivas en el laboratorio de Hola. |
   | [Eliminar el laboratorio de hello todas las máquinas virtuales con un script de PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Eliminar todas las prácticas de hello en una sola operación una vez completado el entrenamiento de Hola. |
5. **Compartir laboratorio Hola con cada aprendiz**
   
    Se puede acceder directamente a los laboratorios mediante un vínculo que puede compartir con los aprendices. Sus prácticas no incluso tienen toohave una cuenta de Azure, siempre tienen un [cuenta de Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Los aprendices no pueden ver las máquinas virtuales creadas por otros aprendices.  
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Agregar un laboratorio de prácticas tooa en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-add-devtest-user.md) |Use hello tooadd portal Azure prácticas tooyour entrenamiento laboratorio. |
   | [Agregar el laboratorio de prácticas toohello mediante un script de PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilice tooautomate PowerShell agregar laboratorio de prácticas tooyour entrenamiento. |
   | [Obtener un laboratorio de toohello de vínculo](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Aprenda cómo se puede acceder directamente a un laboratorio a través de un hipervínculo. |
6. **Volver a usar una y otra vez laboratorio Hola** 
   
    Puede automatizar la creación de laboratorio, incluida la configuración personalizada, crear una plantilla de administrador de recursos y utilizándolo laboratorios idénticos toocreate una y otra vez. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de un laboratorio mediante una plantilla de Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Cree laboratorios en Azure DevTest Labs mediante plantillas de Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

