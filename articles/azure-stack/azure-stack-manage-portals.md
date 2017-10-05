---
title: "Usar los portales de administración y de usuarios en Azure Stack | Microsoft Docs"
description: "Aprenda las diferencias entre los portales de administración y de usuarios en Azure Stack."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 066de8278d1ef4406cde837da4c7c65304854383
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-administrator-and-user-portals-in-azure-stack"></a>Usar los portales de administración y de usuarios en Azure Stack

Hay dos portales en Azure Stack: el portal de administración y el portal de usuarios (también llamado portal de *inquilinos*). Los portales se apoyan en instancias independientes de Azure Resource Manager.

En la tabla siguiente se muestra cómo conectarse a los portales y a los puntos de conexión de Resource Manager en un entorno de Azure Stack Development Kit.

|  Portal | URL del portal | URL del punto de conexión de Resource Manager |   
| -------- | ------------- | ------- |  
| Administrador | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| Usuario | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

## <a name="the-administrator-portal"></a>El portal de administración

El portal de administración permite que un operador de nube realice tareas administrativas y operativas. Un operador de nube puede hacer cosas como las siguientes:
* Supervisar el estado y las alertas.
* Administrar la capacidad.
* Rellenar el Marketplace.
* Crear planes y ofertas.
* Crear suscripciones para los inquilinos.

Un operador de nube también puede crear recursos, como máquinas virtuales, redes virtuales y cuentas de almacenamiento.

 ![El portal de administración](media/azure-stack-manage-portals/image1.png)

 ## <a name="the-user-portal"></a>El portal de usuarios

 El portal de usuarios no proporciona acceso a cualquiera de las funcionalidades administrativas u operativas del portal de administración. En el portal de usuarios, un usuario puede suscribirse a las ofertas públicas y utilizar los servicios que están disponibles a través de dichas ofertas.

  ![El portal de usuarios](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a>Comportamiento de la suscripción
 
 Asegúrese de comprender las siguientes diferencias entre el comportamiento de la suscripción en los dos portales.

 Portal de administración:
* Hay solo una suscripción que está disponible en el portal de administración. Esta suscripción es la *suscripción de proveedor predeterminada*. No se puede agregar ninguna otra suscripción para usarla en el portal de administración.
* Como operador de nube, puede agregar suscripciones para los usuarios (incluido usted mismo) desde el portal de administración. Los usuarios (incluido usted) pueden tener acceso a estas suscripciones y usarlas desde el portal de usuarios.

  >[!NOTE]
  Debido a la separación de Azure Resource Manager, las suscripciones no se cruzan de un portal a otro. Por ejemplo, si, como operador de nube, inicia sesión en el portal de usuarios, no puede tener acceso a la suscripción de proveedor predeterminada. Por lo tanto, no tiene acceso a las funciones administrativas. Puede crear suscripciones para sí mismo a partir de ofertas públicas, pero se le considerará un usuario inquilino.

Portal de usuarios:
* En el portal de usuarios, una cuenta puede tener varias suscripciones.

  >[!NOTE]
  En el entorno del kit de desarrollo, si un usuario inquilino pertenece al mismo directorio que el operador de nube, no se le impide iniciar sesión en el portal de administración. Sin embargo, no tiene acceso a ninguna de las funciones administrativas. Además, no puede agregar suscripciones ni acceder a las ofertas disponibles en el portal de usuarios.

## <a name="next-steps"></a>Pasos siguientes

[Conexión a Azure Stack](azure-stack-connect-azure-stack.md)

[Administración de regiones en Azure Stack](azure-stack-region-management.md)
