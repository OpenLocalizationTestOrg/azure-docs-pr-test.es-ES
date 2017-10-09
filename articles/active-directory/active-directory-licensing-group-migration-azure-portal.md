---
title: toomigrate aaaHow su tooa individuales de los usuarios con licencia de grupo en Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo tooswitch de usuario individual licencias licencia basada en toogroup con Azure Active Directory"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>¿Cómo tooadd licencia de grupo de usuarios tooa de licencia en Azure Active Directory

Tal vez tenga existente toousers de licencias implementados en organizaciones de Hola a través de "asignación directa;" es decir, usando scripts de PowerShell u otras licencias de usuario individual de tooassign de herramientas. Si desea que toostart con licencias toomanage licencias basadas en grupo en su organización, necesitará una migración plan tooseamlessly reemplazar las soluciones existentes con licencia basada en el grupo.

Hola tookeep de lo más importante en cuenta es que debe evitar una situación donde se producirá la licencia de migración basada en toogroup los usuarios pierdan temporalmente sus licencias asignadas actualmente. Cualquier proceso que puede provocar la eliminación de licencias debe ser evitar el riesgo de hello tooremove de los usuarios pierdan acceso tooservices y sus datos.

## <a name="recommended-migration-process"></a>Proceso de migración recomendado

1. Cuenta actualmente con un sistema de automatización (por ejemplo, PowerShell) que administra la asignación y la retirada de licencias de los usuarios. Deje que se ejecute de la forma habitual.

2. Crear un nuevo grupo de licencias (o decidir qué existente agrupa toouse) y asegúrese de que todos los necesarios a los usuarios se agregarán como miembros.

3. Asignar licencias de hello requerido grupos de toothose; el objetivo debe ser tooreflect Hola mismo estado licencias aplica toothose a los usuarios la automatización existente (por ejemplo, PowerShell).

4. Comprobar que licencias se han tooall aplicados a los usuarios en esos grupos. Esto puede hacerse mediante la comprobación de estado de procesamiento de hello en cada grupo y compruebe los registros de auditoría.

  - Puede realizar una revisión rápida de cada usuario observando los detalles de sus licencias. Verá que ha Hola mismo licencias asignadas "directamente" y "heredado" de grupos.

  - Puede ejecutar un script de PowerShell demasiado[Compruebe cómo se asignan las licencias toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Cuando hello misma licencia del producto es toohello usuario asignado directamente y a través de un grupo, se consume sólo una licencia de usuario Hola. Por lo tanto, no hay licencias adicionales son necesarios tooperform migración.

5. Compruebe si en algún grupo de usuarios aparece el estado de error, a fin de verificar que no se produzcan errores en las asignaciones de licencias. Para más información, vea [Identificación y resolución de problemas de licencias de un grupo](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Considere la posibilidad de quitar las asignaciones directas original Hola; Puede que desee toodo gradualmente, en "ondas", toomonitor Hola primero resultado en un subconjunto de usuarios.

  Podría omitir Hola originales asignaciones directas en los usuarios, pero cuando los usuarios de hello dejan sus grupos con licencia que aún conservarán licencia original hello, que es posiblemente no desea que desee.

## <a name="an-example"></a>Un ejemplo

Tenemos una organización con 1000 usuarios. Todos los usuarios necesitan la licencia de Enterprise Mobility + Security (EMS). 200 usuarios están en hello departamento de finanzas y requieren licencias de Office 365 Enterprise E3. Existe un script de PowerShell que se ejecuta a nivel local mediante la adición y retirada de licencias de usuarios a medida que se incorporan y que se van. Queremos que el script de Hola tooreplace con basado en el grupo de licencias para que licencias se administran automáticamente por Azure AD.

Este es el proceso de migración de hello pudo apariencia:

1. Utilizando hello Azure asigne portal Hola EMS licencia toohello **todos los usuarios** grupo en Azure AD. Asignar Hola E3 licencia toohello **departamento de finanzas** grupo que contiene todos los usuarios de hello necesario.

2. Confirme en cada grupo que se haya completado la asignación de licencia a todos los usuarios. Vaya toohello hoja para cada grupo, seleccione **licencias**y comprobar el estado de procesamiento de hello en parte superior de Hola de hello **licencias** hoja.

  - Buscar para tooconfirm "cambios de licencias más recientes han sido tooall aplicados a los usuarios" se ha completado el procesamiento.

  - Busque si hay alguna notificación en la parte superior sobre algún usuario cuya licencia no se haya podido asignar correctamente. ¿Se han agotado las licencias para algunos usuarios? ¿Algunos usuarios tienen SKU de licencias conflictivas que les impidan heredar las licencias de grupo?

3. Zona comprobar algunos tooverify de los usuarios que tienen Hola directa y licencias de grupo aplicadas. Vaya toohello hoja para un usuario, seleccione **licencias**y examinar el estado de Hola de licencias.

  - Esto es estado de usuario de hello esperada durante la migración:

      ![estado de usuario esperado](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Esto confirma que el usuario hello tiene licencias directa y heredadas. Se observa que tiene asignadas las licencias para **EMS** y **E3**.

  - Seleccione cada detalles de licencia tooshow acerca de los servicios de hello habilitado. Esto puede resultar toocheck usado si hello directa y activar licencias de grupo exactamente Hola mismo planes de servicio de usuario de Hola.

      ![comprobación de planes de servicio](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Después de confirmar que las licencias directas y de grupo son equivalentes, puede empezar a quitar a los usuarios las licencias directas. Puede probarlo quitándolos para usuarios individuales en el portal de hello y, a continuación, ejecutar toohave de scripts de automatización a quitan de forma masiva. Este es un ejemplo de Hola mismo usuario con licencias directa Hola quitado a través del portal de Hola. Tenga en cuenta que sufre ningún estado de la licencia de hello, pero no se vean las asignaciones directas.

  ![licencias directas quitadas](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de otros escenarios de administración de licencias a través de grupos, leer

* [Asignar licencias tooa grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [¿En qué consisten las licencias basadas en grupos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificación y resolución de problemas de licencias de un grupo en Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md) (Escenarios adicionales de licencias basadas en grupos de Azure Active Directory)
