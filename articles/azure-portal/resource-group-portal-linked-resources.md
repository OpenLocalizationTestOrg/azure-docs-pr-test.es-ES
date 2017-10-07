---
title: "aaaRelated y recursos vinculados en hello icono Galería"
description: "Obtenga información acerca de los recursos vinculados y relacionados que se muestran en la Galería de mosaico de Hola de portal de vista previa de Hola."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a>Recursos relacionados y vinculados en la Galería de mosaico de Hola
Galería de mosaico de Hello permite toofind mosaicos para un recurso determinado y arrástrelos hasta la hoja actual. Con la Galería de mosaico de hello, puede crear vistas de administración que abarcan los recursos. Cualquier recurso especificado, hello relacionado con recursos incluyen todos los recursos de hello en su grupo de recursos y todos los recursos que se vinculan tooor del recurso de Hola.

## <a name="linked-resources-in-resource-manager"></a>Recursos vinculados en Resource Manager
Vinculación es una característica del programa Hola a Administrador de recursos.  Le permite toodeclare relaciones entre los recursos incluso si no residen en hello mismo grupo de recursos. La vinculación no influye en hello en tiempo de ejecución de los recursos, ningún impacto sobre la facturación y ningún impacto en el acceso basado en roles.  Es simplemente un mecanismo que se pueden usar relaciones de toorepresent para que las herramientas como la Galería de mosaico de hello puede proporcionar una administración enriquecido experimentan.  Las herramientas pueden inspeccionar vínculos de hello mediante vínculos de hello API y proporcionar experiencias de administración de relaciones personalizado también. 

## <a name="how-do-i-link-my-resources"></a>¿Cómo puedo vincular mis recursos?
Al crear recursos a través del portal de Hola o mediante la implementación de una plantilla a través de Azure PowerShell o CLI de Azure, se crean automáticamente vínculos de algunos de los recursos dependientes. Mediante programación puede vincular recursos mediante hello [API de REST de recursos vinculados](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Pasos siguientes
* Si necesita una plantillas de administrador de recursos de toowriting de introducción, consulte [crear plantillas](../azure-resource-manager/resource-group-authoring-templates.md).
* toounderstand más acerca de cómo trabajar con grupos de recursos a través del portal de hello, consulte [Using Hola toomanage portal Azure de los recursos de Azure](../azure-resource-manager/resource-group-portal.md).

