---
title: "administración de aaaRegion en la pila de Azure | Documentos de Microsoft"
description: "Introducción a la administración de regiones en Azure Stack."
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a>Administración de regiones en Azure Stack
Pila de Azure tiene el concepto de Hola de regiones, que son entidades lógicas que consta de los recursos de hardware de Hola que componen la infraestructura de Azure pila Hola. Dentro de la administración de la región, puede buscar todos los recursos que son necesario toosuccessfully funcionan del ciclo de vida de infraestructura de hello pila de Azure.

Hola Kit de desarrollo de pila de Azure es una implementación de un único nodo y es igual a una región. Si configura otra instancia del programa Hola Kit de desarrollo de pila de Azure en hardware independiente, esta instancia es una región diferente.

## <a name="information-available-through-hello-region-management-tile"></a>Información disponible a través del icono de administración de la región de Hola
Pila de Azure tiene un conjunto de capacidades de administración de región disponibles en hello **administración región** icono. Este icono es administrador de la nube de tooa disponible en panel predeterminado de hello en el portal del Administrador de Hola. A través de este icono, puede supervisar y actualizar su región de Azure Stack y sus componentes, que son específicos de cada región.

 ![icono de administración de región de Hola](media/azure-stack-manage-region/image1.png)

 Si hace clic en una región en el icono de administración de región de hello, puede tener acceso a Hola siguiente información:

  ![Descripción de los paneles en la hoja de administración de región de Hola](media/azure-stack-manage-region/image2.png)

1. **menú de recursos de Hello**. Aquí, puede tener acceso a áreas de administración de infraestructuras específicas y ver y administrar los recursos de inquilino como son las cuentas de almacenamiento y las redes virtuales.

2. **Alertas**. Este icono muestra las alertas de todo el sistema y proporciona detalles sobre cada una.

3. **Actualizaciones**. En este icono, puede ver la versión actual de Hola de su infraestructura de la pila de Azure.

4. **Proveedores de recursos**. Proveedores de recursos es Hola lugar toomanage Hola inquilino la funcionalidad que ofrece Hola componentes necesarios toorun pila de Azure. Cada proveedor de recursos viene con una experiencia administrativa. Esta experiencia puede incluir las alertas de proveedor específico de hello, métricas y otro proveedor de recursos de toohello específico de las capacidades de administración.
 
5. **Infrastructure roles** (Roles de infraestructura). Los roles de infraestructura son Hola componentes necesarios toorun pila de Azure. Solo roles de infraestructura de Hola que dependen de las alertas se muestran. Haciendo clic en un rol, puede ver alertas de hello asociadas con el rol específico de hello e instancias de rol de Hola donde se ejecuta este rol. Aunque hay Hola capacidad toostart, reiniciar, o cerrar una instancia de rol de infraestructura, realice **no** hacer esto en un entorno de kit de desarrollo. Estas opciones están diseñadas únicamente para un entorno de varios nodos, donde hay más de una instancia de rol por rol de infraestructura. Al reiniciar una instancia de rol (especialmente AzS-Xrp01) en el kit de desarrollo de hello provoca inestabilidad del sistema.

## <a name="next-steps"></a>Pasos siguientes
[Supervisar el estado y las alertas en Azure Stack](azure-stack-monitor-health.md)

[Administrar las actualizaciones en Azure Stack](azure-stack-updates.md)






