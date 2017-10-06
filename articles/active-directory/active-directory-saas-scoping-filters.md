---
title: "aplicaciones de aaaProvisioning con filtros de ámbito | Documentos de Microsoft"
description: "Obtenga información acerca de cómo definir el ámbito toouse filtra los objetos de tooprevent en aplicaciones que admitan el aprovisionamiento automático de usuarios desde que se aprovisiona realmente si un objeto no satisface sus requisitos empresariales."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito
objetivo de Hola de esta sección es tooexplain cómo toouse ámbito filtra toodefine basado en atributos reglas que determinan qué usuarios aprovisiona toohello aplicación.

## <a name="clauses-and-scope-groups"></a>Cláusulas y grupos de ámbitos
![Filtro de ámbito][1] 

Los filtros de ámbito se definen mediante uno o varios **grupos de ámbitos**, y cada uno de ellos contiene una o varias **cláusulas**. cláusulas de hello toosee para un grupo de ámbito determinado, expándalo haciendo clic en hello flecha toohello a la izquierda del nombre de grupo de Hola.

A **cláusula** determina qué usuarios tienen permiso toopass a través de hello filtro de ámbito mediante la evaluación de atributos de cada usuario. Por ejemplo, tendrá una cláusula que requiere que "state" atributo igual Nueva York un usuario, por lo que solo los usuarios de Nueva York se aprovisionan en aplicación hello.

![Nombre del grupo de ámbito][2] 

Cada **grupo del ámbito** comienza con una obligatorio **cláusula**, tal y como se muestra en la captura de pantalla de hello anterior. Esta cláusula indica simplemente que el usuario Hola primero se debe asignar toohello aplicación antes de que se evalúa por los filtros de ámbito. Esta cláusula no puede eliminarse ni modificarse.

Puede agregar nuevas cláusulas o nuevos grupos de ámbito presionando el botón correspondiente de Hola. Puede asignar un nombre a cada grupo de ámbitos; para ello, edite la propiedad **Nombre del grupo de ámbitos** .

## <a name="how-scoping-filters-are-evaluated"></a>Evaluación de los filtros de ámbito
Durante el aprovisionamiento, probamos cada usuario asignado en su ámbito toodetermine filtros si ese usuario merece acceso toohello aplicación. Se puede considerar cada cláusula como una prueba que se debe pasar en orden para hello usuario tooavoid obtener filtran. 

Si tiene varios grupos de ámbito definidos, cada usuario debe superar al menos uno de ellos tooaccess aplicación hello. Dentro de cada grupo de ámbito, sin embargo, Hola usuario debe pasar cada cláusula toopass ese grupo de ámbito específico. 

En otras palabras, puede pensar en grupos de ámbito como o juntos, y se puede considerar las cláusulas de hello dentro de ellos como AND haría juntos. Por ejemplo, considere la posibilidad de hello siguiente filtro de ámbito:

![Nombre del grupo de ámbito][3]  

Según toothis filtro de ámbito, los usuarios deben cumplir los siguientes Hola criterios, toobe aprovisionado:

1. Deben estar asignados toohello aplicación.
2. Debe trabajar en el departamento de ingeniería de Hola
3. Deben trabajar en San Francisco o Canadá.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones](active-directory-saas-app-provisioning.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Escritura de expresiones para asignaciones de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
