---
title: "aaaManage tooAzure de acceso mediante roles de facturación | Documentos de Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Administrar la información de toobilling de acceso de Azure mediante control de acceso basado en roles

Puede conceder acceso a Azure toomembers de información de facturación de su equipo mediante la asignación de uno de hello después de suscripción de tooyour de roles de usuario: cuenta de administrador, Administrador de servicios, Coadministrador, propietario, Colaborador, lector y lector de facturación. Tendrían acceso toobilling información en hello [portal de Azure](https://portal.azure.com/), y pueden utilizar hello [API facturación](billing-usage-rate-card-overview.md) tooprogrammatically obtener facturas (una vez elegido-in) y obtener detalles de uso. Para más información sobre quién puede conceder roles y qué puede hacer cada rol, vea [Roles en Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Permitir que otros usuarios tooaccess facturas

Hello Administrador de la cuenta debe elegir utilizando hello [portal de Azure](https://portal.azure.com/) permitir acceso tooinvoices para otros usuarios y a través de API.

1. Como administrador de la cuenta de hello, seleccione su suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en portal de Azure.

1. Seleccione **facturas** y, a continuación, **acceso tooinvoices**.

    ![Captura de pantalla muestra cómo acceder toodelegate a tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Activar **en** acceso Hola seguido de guardar los cambios de hello, los usuarios de tooallow de suscripción roles con ámbito toodownload factura.

    ![Captura de pantalla muestra toodelegate desactivar acceso tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

La aceptación de permite el Administrador de servicios, Coadministrador, propietario, Colaborador, lector y lector de facturación en facturas de hello suscripción toodownload PDF en hello portal de Azure. Sin embargo, facturas anteriores a de 2016 diciembre son toohello única disponible Administrador de la cuenta por ahora.

Hola, Administrador de la cuenta también puede configurar facturas toohave enviadas a través del correo electrónico. más información, consulte toolearn [obtener la factura de correo electrónico](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Agregar rol de lector de facturación de los usuarios toohello

rol de lector de facturación de Hello tiene información de facturación de toosubscription de acceso de solo lectura en el portal de Azure y no tooservices de acceso, como las máquinas virtuales y las cuentas de almacenamiento. Asignar toosomeone de rol de lector de facturación Hola que necesita tener acceso a información de facturación de suscripción toohello pero no Hola capacidad toomanage Azure servicios. Este rol es adecuado para los usuarios de una organización que solo realizan la administración financiera y de costos para las suscripciones de Azure.

1. Seleccione la suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en portal de Azure.

1. Seleccione **Control de acceso (IAM)** y haga clic en **Agregar**.

    ![Captura de pantalla muestra IAM en la hoja de la suscripción de Hola](./media/billing-manage-access/select-iam.PNG)

1. Elija **facturación lector** en hello **seleccione un rol** página.

    ![Captura de pantalla muestra de facturación lector en la vista de la ventana emergente de Hola](./media/billing-manage-access/select-roles.PNG)

1. Escriba el correo electrónico de hello para el usuario de Hola que desee tooinvite, y después haga clic en **Aceptar** invitación de hello toosend.

    ![Captura de pantalla que muestra una persona tooenter tooinvite de correo electrónico](./media/billing-manage-access/add-user.PNG)

1. Siga las instrucciones en toolog de correo electrónico de invitación de hello en como un lector de facturación.

    ![Captura de pantalla que muestra qué Hola lector de facturación puede ver en el portal de Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> característica de lector de facturación de Hello está en vista previa y aún no admiten suscripciones de enterprise (EA) o nubes no globales.

## <a name="adding-users-tooother-roles"></a>Agregar usuarios tooother roles

Los usuarios de otros roles, como Propietario o Colaborador, pueden tener acceso no solo a la información de facturación, sino también a los servicios de Azure. estos roles, consulte el toomanage [agregar o cambiar roles de administrador de Azure que administran la suscripción de Hola o servicios](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>¿Quién puede acceder a hello [centro de cuentas de](https://account.windowsazure.com)?

Hola sólo administrador de la cuenta puede iniciar sesión en el centro de cuentas de toohello. Hola, Administrador de la cuenta es propietario legal de Hola de suscripción de Hola. De forma predeterminada, Hola quien inscrito o comprado Hola suscripción de Azure es hello Administrador de cuenta, a menos que hello [propiedad de la suscripción se ha transferido](billing-subscription-transfer.md) toosomebody else. Hola, Administrador de la cuenta puede crear suscripciones, cancelar suscripciones, cambiar dirección de facturación de Hola para una suscripción y administrar las directivas de acceso para la suscripción de Hola.

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.

Si tienes más preguntas, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.
