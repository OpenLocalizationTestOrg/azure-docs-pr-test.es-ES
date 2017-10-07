---
title: "aaaManage cuenta de automatización de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo toomanage Hola configuración de la cuenta de automatización, como la renovación de certificados, eliminación y una configuración incorrecta."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Administración de la cuenta de Azure Automation
En algún momento antes de que expire su cuenta de automatización, necesitará toorenew Hola certificado. Si cree que Hola cuenta de ejecución está en peligro, puede eliminar y volver a crearla. Esta sección se describe cómo tooperform estas operaciones.

## <a name="self-signed-certificate-renewal"></a>Renovación de certificado autofirmado
certificado autofirmado de Hola que creó para la cuenta de ejecución de Hola expira un año a partir de la fecha de Hola de creación. Se puede renovar en cualquier momento antes de que expire. Cuando renovarlo, certificado válido de hello actual es retenido tooensure que los runbooks que se ponen en cola hasta o activamente ejecutándose y que autenticarse con hello cuenta de ejecución, no se afecta negativamente. certificado de Hello sigue siendo válido hasta la fecha de expiración.

> [!NOTE]
> Si ha configurado su toouse de cuenta automatización ejecutar como un certificado emitido por la entidad de certificación de empresa y use esta opción, certificado de empresa de Hola se reemplazará por un certificado autofirmado.

Hola toorenew certificados, Hola siguientes:

1. Hola portal de Azure, abrir cuenta de automatización de Hola.

2. En hello **cuenta de automatización** hoja en hello **cuenta propiedades** panel, en **configuración de la cuenta**, seleccione **cuentas de ejecución**.

    ![Panel de propiedades de la cuenta de Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta u Hola clásico cuenta de ejecución que desea toorenew Hola certificado.

4. En hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **renovar certificado**.

    ![Renovación del certificado para una cuenta de ejecución](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Mientras se que se va a renovar el certificado de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Eliminación de una cuenta de ejecución o de ejecución clásica
Esta sección se describe cómo toodelete y volver a crear una cuenta de ejecución o identificación clásico. Al realizar esta acción, se conserva Hola cuenta de automatización. Después de eliminar una cuenta de ejecución o identificación clásico, puede volver a crearla en hello portal de Azure.

1. Hola portal de Azure, abrir cuenta de automatización de Hola.

2. En hello **cuenta de automatización** hoja, en el panel de propiedades de cuenta hello, seleccione **cuentas de ejecución**.

3. En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta de ejecución de o clásico como la cuenta que desea toodelete. A continuación, en hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **eliminar**.

 ![Eliminación de una cuenta de ejecución](media/automation-manage-account/automation-account-delete-runas.png)

4. Mientras se está eliminando la cuenta de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

5. Después de que se ha eliminado la cuenta de hello, se puede volver a crear en hello **cuentas de ejecución** opción de creación de la hoja de propiedades seleccionando hello **ejecutar como cuenta de Azure**.

 ![Volver a crear Hola automatización de la cuenta de ejecución](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Error de configuración
Algunos elementos de configuración necesarios para toofunction de cuenta de identificación o identificación clásico Hola correctamente podrían se han eliminado o creó incorrectamente durante la instalación inicial. Hola elementos incluyen:

* Recurso de certificado
* Recurso de conexión
* Se ha quitado la cuenta de ejecución de rol de colaborador de Hola
* Entidad de servicio o aplicación en Azure AD

Hola anterior y otras instancias de una configuración incorrecta, Hola cuenta de automatización detecta Hola cambia y muestra un estado de *incompleta* en hello **cuentas de ejecución** hoja de propiedades para hello cuenta.

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Cuando se selecciona la cuenta de identificación de hello, Hola cuenta **propiedades** panel muestra hello mensaje de error siguiente:

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Rápidamente puede resolver estos problemas de la cuenta ejecutar como eliminar y volver a crear la cuenta de hello.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información acerca de las entidades de servicio, consulte demasiado[objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md).
* Para obtener más información sobre el Control de acceso basado en roles en automatización de Azure, consulte demasiado[control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md).
* Para obtener más información sobre los certificados y servicios de Azure, consulte demasiado[Introducción a los certificados para servicios en la nube](../cloud-services/cloud-services-certs-create.md).
