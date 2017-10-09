---
title: grupo de tooa aaaAssign licencias en Azure Active Directory | Documentos de Microsoft
description: "¿Cómo tooassign licencias toousers mediante el Administrador de licencias del grupo de Active Directory de Azure"
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
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Asignar licencias toousers por su pertenencia a grupo en Azure Active Directory

Este artículo le guiará a través de la asignación de grupo de tooa de licencias de productos de los usuarios de Azure Active Directory (Azure AD) y, a continuación, comprobar que está licencia correctamente.

En este ejemplo, el inquilino de hello contiene un grupo de seguridad llamado **departamento de recursos humanos**. Este grupo incluye a todos los miembros del departamento de recursos humanos de hello (aproximadamente 1000 usuarios). Desea que todo departamento de tooassign Office 365 Enterprise E3 licencias toohello. Hola servicio Yammer Enterprise que se incluye en el producto de hello debe deshabilitarse temporalmente hasta que el departamento de Hola se toostart listo usarlo. También puede toodeploy Enterprise Mobility + Security licencias toohello mismo grupo de usuarios.

> [!NOTE]
> Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia de usuario de tooa, Administrador de hello tiene propiedad de ubicación de uso de toospecify hello en usuario Hola.

> Para la asignación de licencias del grupo, los usuarios sin especificar una ubicación de uso heredará ubicación hello del directorio de Hola. Si hay usuarios en varias ubicaciones, se recomienda establecer siempre ubicación de uso como parte de su flujo de creación de usuario en Azure AD (por ejemplo, mediante la conexión de AAD configuración) - que se asegurará de resultado de hello de asignación de licencias siempre es correcto y los usuarios no reciben servicios en ubicaciones que no están permitidos.

## <a name="step-1-assign-hello-required-licenses"></a>Paso 1: Asignar licencias de hello necesario

1. Inicie sesión en toohello [ **portal de Azure** ](https://portal.azure.com) con una cuenta de administrador. licencias de toomanage, cuenta de hello debe ser un administrador de cuenta de usuario o rol de administrador global.

2. Seleccione **más servicios** en Hola panel de navegación izquierdo y, a continuación, seleccione **Azure Active Directory**. Puede agregar este tooFavorites hoja o anclar toohello panel del portal.

3. En hello **Azure Active Directory** hoja, seleccione **licencias**. Se abrirá una hoja, donde puede ver y administrar todos los productos con licencia de inquilino de Hola.

4. En **todos los productos**, seleccione Office 365 Enterprise E3 y Enterprise Mobility + Security seleccionando los nombres de producto de Hola. la asignación de hello toostart, seleccione **asignar** princip Hola de hoja de Hola.

   ![Todos los productos, asignar licencias](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. En hello **asignar licencias** hoja, haga clic en **usuarios y grupos** tooopen hello **usuarios y grupos** hoja. Busque el nombre del grupo de hello *departamento de recursos humanos*, seleccione el grupo de hello y, a continuación, ser seguro tooconfirm haciendo clic en **seleccione** final Hola de hoja de Hola.

   ![Selección de un grupo](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. En hello **asignar licencias** hoja, haga clic en **opciones de asignación (opcionales)**, que muestra todos los planes de servicio incluidos en hello dos productos que se ha seleccionado anteriormente. Buscar **Yammer Enterprise** y activarlo **desactivar** toodisable que dan servicio de licencia del producto Hola. Confirme pulsando **Aceptar** final Hola de **opciones de asignación**.

   ![Opciones de asignación](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. asignación de hello toocomplete, en hello **asignar licencias** hoja, haga clic en **asignar** final Hola de hoja de Hola.

8. Se muestra una notificación en la esquina superior derecha de Hola que muestra el estado de Hola y el resultado del proceso de Hola. Si el grupo de toohello de asignación de hello no se pudo completar (por ejemplo, debido a licencias ya existentes en el grupo de hello), haga clic en detalles de tooview de hello notificación de error de Hola.

Ahora, hemos especificado una plantilla de licencia para el grupo de departamento de recursos humanos de Hola. Un proceso en segundo plano en Azure AD se ha iniciado tooprocess todos los miembros existentes de ese grupo. Esta operación inicial podría tardar algún tiempo, dependiendo del tamaño actual de hello del grupo de Hola. En el paso siguiente de hello, se podrá describen cómo tooverify ese proceso Hola finalizó y determinar si atención adicional es necesario tooresolve problemas.

> [!NOTE]
> Puede iniciar Hola la misma asignación de una ubicación alternativa: **usuarios y grupos** en Azure AD. Vaya demasiado**Azure Active Directory** > **usuarios y grupos** > **todos los grupos de**. A continuación, busque el grupo de hello, selecciónelo y vaya toohello **licencias** Hola de ficha **asignar** botón encima de la hoja de hello abre una hoja de asignación de licencias de Hola.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Paso 2: Comprobar que ha finalizado la asignación inicial de Hola

1. Vaya demasiado**Azure Active Directory** > **usuarios y grupos** > **todos los grupos de**. A continuación, busque hello **departamento de recursos humanos** grupo al que se han asignado licencias.

2. En hello **departamento de recursos humanos** hoja de grupo, seleccione **licencias**. Esto le permite confirmar rápidamente si licencias se han asignado totalmente toousers y si hay errores que deban toolook en. Hola siguiente información está disponible:

   - Lista de licencias de producto que están asignados a toohello grupo. Seleccione un servicios específicos de Hola de tooshow de entrada que se han habilitado y toomake cambia.

   - Estado de la última modificación de licencia de Hola que se realizaron toohello grupo (si se están procesando los cambios de Hola o si ha terminado el procesamiento de todos los miembros de usuario).

   - Información sobre los usuarios que están en un estado de error porque licencias no se pudo asignar toothem.

   ![Opciones de asignación](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Encontrará información más detallada sobre el procesamiento de licencias en **Azure Active Directory** > **Usuarios y grupos** > *nombre de grupo* > **Registros de auditoría**. Tenga en cuenta Hola siguientes actividades:

   - Actividad: **empezar a aplicar grupo basado licencia toousers**. Esto se registra cuando el sistema de hello recoge el cambio de asignación de licencias de hello en grupo de Hola y aplicarlo a tooall miembros de usuario se inicia. Contiene información sobre el cambio de Hola que se realizó.

   - Actividad: **finalizar aplicar toousers de licencia de grupo basado**. Esto se registra al sistema de hello finaliza el procesamiento de todos los usuarios en el grupo de Hola. Contiene un resumen de cuántos usuarios se han procesado correctamente y el número de usuarios a los que no se pudieron asignar las licencias de grupo.

   [Lea esta sección](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn más información acerca de cómo los registros de auditoría pueden ser cambios de tooanalyze usado realizados por basado en el grupo de licencias.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Paso 3: Comprobación y resolución de problemas de licencias

1. Vaya demasiado**Azure Active Directory** > **usuarios y grupos** > **todos los grupos de**y encontrar Hola **departamento de recursos humanos**grupo al que se han asignado licencias.
2. En hello **departamento de recursos humanos** hoja de grupo, seleccione **licencias**. notificación de Hello encima de la hoja de hello muestra que hay 10 usuarios que no se pudo asignar licencias a. Al hacer clic en ella, se abre una lista con todos los usuarios en estado de error de licencia para este grupo.
3. Hola **no se pudo asignaciones** columna nos indica que no se pudieron asignar los usuarios de toohello ambas licencias de producto. Hola **principales motivo error** columna contiene causa Hola de error de Hola. En este caso, es **Planes de servicio en conflicto**.

   ![Asignaciones erróneas](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Seleccione un saludo de tooopen usuario **licencias** hoja. Esta hoja muestra todas las licencias que están asignadas actualmente toohello usuario. En este ejemplo, usuario de hello tiene licencia de Office 365 Enterprise E1 Hola que se heredó de hello **usuarios quiosco** grupo. Esto está en conflicto con una licencia de hello E3 que Hola tooapply sistema probado de hello **departamento de recursos humanos** grupo. Como resultado, ninguno de licencias de Hola de ese grupo se ha asignado a toohello usuario.

   ![Ver las licencias de un usuario](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve este conflicto, eliminar al usuario Hola de hello **usuarios quiosco** grupo. Una vez que Azure AD procese cambio hello, Hola **departamento de recursos humanos** licencias se han asignado correctamente.

   ![Licencia asignada correctamente](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de la característica de hello establecido para la administración de licencias a través de grupos, vea Hola siguientes artículos:

* [¿En qué consisten las licencias basadas en grupos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificación y resolución de problemas de licencias de un grupo en Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Cómo toomigrate individuales autoriza el uso de los usuarios según toogroup licencias en Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md) (Escenarios adicionales de licencias basadas en grupos de Azure Active Directory)
