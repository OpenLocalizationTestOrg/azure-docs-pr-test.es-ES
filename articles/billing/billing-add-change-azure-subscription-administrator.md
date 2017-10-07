---
title: "aaaAdd o cambiar roles de suscripción de administración de Azure | Documentos de Microsoft"
description: "Describe cómo tooadd o cambiar Coadministrador de Azure, el Administrador de servicios y el Administrador de la cuenta"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Agregar o cambiar los roles de administrador de Azure que administran la suscripción de Hola o servicios
Puede cambiar hello Azure administrador que administra su suscripción de Azure o administra hello Azure servicios usados en su suscripción. tooview información de facturación de Azure y administrar suscripciones, debe iniciar sesión en toohello [centro de cuentas de](https://account.windowsazure.com/Home/Index) como Hola Administrador de la cuenta. 

## <a name="add-an-admin-for-a-subscription"></a>Adición de un administrador para una suscripción
Puede agregar un administrador de Azure en hello portal de Azure o en hello portal de Azure clásico.

**Portal de Azure**

tooadd alguien como administrador para una suscripción en hello portal de Azure, se les da el rol de propietario de Hola. rol de propietario de Hello solo puede administrar los recursos de hello en la suscripción de Hola que asignó. No tiene acceso con privilegios tooother suscripciones. Hola propietarios agregar a través de hello [portal de Azure](https://portal.azure.com) no puede administrar recursos en hello [portal de Azure clásico](https://manage.windowsazure.com).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, seleccione **suscripción** > *Hola suscripción que quiere Hola admin tooaccess*.

    ![Captura de pantalla que muestra la suscripción seleccionada](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. En la hoja de la suscripción de hello, seleccione **(de índices IAM) de control de acceso**.
4. Seleccione **Agregar** > **Rol** > **Propietario**. Escriba la dirección de correo electrónico de saludo del usuario de Hola que desee tooadd como propietario, el usuario seleccione hello y, a continuación, seleccione **guardar**.

    ![Captura de pantalla que muestra el rol de propietario de hello seleccionado](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Si desea que cuenta de propietario de hello tooadd como Coadministrador, Hola **(de índices IAM) de control de acceso** página, haga clic en usuario de hello y, a continuación, seleccione **agregar como Coadministrador**. Esta característica ahora está disponible en el [Portal de vista previa de Azure](https://preview.portal.azure.com/). 

     ![Captura de pantalla donde se agrega el coadministrador](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Necesitará usuario de "Propietario" hello tooadd como Coadministrador si es usuario de hello necesario toomanage Hola servicios de Azure en [portal de Azure clásico](https://manage.windowsazure.com/).

    permiso de tooremove Hola Coadministrador, haga clic en usuario de "administrador" hello y, a continuación, seleccione **quitar al Coadministrador**.

    ![Captura de pantalla donde se quita el coadministrador](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Portal de Azure clásico**

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/).
2. En el panel de navegación de hello, seleccione **configuración**> **administradores**> **agregar**. </br>

    ![Captura de pantalla que muestra cómo tooget toohello Agregar botón](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Escriba la dirección de correo electrónico de Hola de persona Hola que desea tooadd como Coadministrador y suscripción hello, a continuación, seleccione que desea Hola tooaccess de coadministrador.</br>

    ![Captura de pantalla que muestra una suscripción seleccionada ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Hola siguiente dirección de correo electrónico se pueden agregar como Coadministrador:

* **Cuenta Microsoft** (anteriormente Windows Live Id) </br>
  Puede usar un toosign Account Microsoft tooall orientados al consumidor productos de Microsoft y servicios de nube, como Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone y Xbox LIVE.
* **Organizational account**</br>
  Una cuenta de organización es una cuenta que se crea en Azure Active Directory. dirección de la cuenta organizativa de Hello tiene este formato:

    usuario@&lt;su dominio&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Cambio del administrador de servicios de una suscripción
Hola sólo administrador de la cuenta puede cambiar Hola Administrador de servicios para una suscripción.

1. Inicie sesión en demasiado[centro de cuentas de Azure](https://account.windowsazure.com/subscriptions) mediante el uso de hello Administrador de la cuenta.
2. Seleccione la suscripción de hello desea toochange.
3. En el lado derecho de hello, seleccione **Editar suscripción** detalles. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. Hola **Administrador de servicios** cuadro, escriba la dirección de correo electrónico de Hola de hello nuevo administrador de servicios. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Cambiar el Administrador de la cuenta de hello
la propiedad tootransfer de hello tooanother de Azure cuenta, consulte [transferir la propiedad de una suscripción de Azure](billing-subscription-transfer.md).

Se recomienda encarecidamente que no elimine o cambie el nombre de la dirección de correo electrónico del Administrador de la cuenta de hello. Puede ver el comportamiento inesperado y no deseado con hello cuenta de Azure. No puede ser capaz de tooAzure inicio de sesión con esa cuenta, realizar cambios toohello cuenta o administrar los recursos con esa cuenta. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Hola de comprobación de administrador de la cuenta de suscripción de Hola
Si no está seguro de que sea administrador de la cuenta de hello para la suscripción, utilice Hola siguiendo los pasos toofind out.

  1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
  2. En el menú del concentrador hello, seleccione **suscripción**.
  3. Seleccione Hola suscripción que desee toocheck y, a continuación, busque en **configuración**.
  4. Seleccione **Propiedades**. Administrador de la cuenta de suscripción de Hola Hola se muestra en hello **Administrador de la cuenta** cuadro.  

## <a name="types-of-azure-admin-accounts"></a>Tipos de cuentas de administrador de Azure
 Cuenta de administrador, Administrador de servicios y Coadministrador son tres tipos de Hola de roles de administrador de Microsoft Azure. Hello siguiente tabla describe Hola diferencia entre estas tres funciones administrativas.

| Rol administrativo | Límite | Description |
| --- | --- | --- |
| Administrador de cuenta (AA) |1 por cuenta de Azure |Esto es persona de Hola que suscribirse a o comprar suscripciones de Azure y es tooaccess autorizados hello [centro de cuentas de](https://account.windowsazure.com/Home/Index) y realizar varias tareas de administración. Estos incluyen el toocreate capaz de suscripciones, cancelar suscripciones, cambiar la facturación de Hola para una suscripción y cambiar Hola Administrador de servicios. |
| Administrador de servicios (SA) |1 por cada suscripción de Azure |Este rol es servicios autorizados toomanage Hola [portal de Azure](https://portal.azure.com). De forma predeterminada, para una suscripción nueva, Hola, Administrador de la cuenta es también hello Administrador de servicios. |
| Coadministrador (CA) en hello [portal de Azure clásico](https://manage.windowsazure.com) |200 por suscripción |Este rol tiene Hola mismo privilegios de acceso como Hola Administrador de servicios, pero no se puede cambiar la asociación de Hola de directorios de tooAzure de suscripciones. |

Azure basada en roles de Active Directory Access Control (RBAC) permite a los usuarios toobe toomultiple funciones de agregado. Para más información, consulte [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Limitaciones y restricciones de las cuentas de administrador
* Cada suscripción está asociada a un directorio de Azure AD (también conocido como Hola directorio predeterminado). Hola toofind suscripción Hola de directorio predeterminado está asociado, vaya toohello [portal de Azure clásico](https://manage.windowsazure.com/), seleccione **configuración** > **suscripciones**. Compruebe Hola de toofind de Id. de suscripción de hello directorio predeterminado.
* Si ha iniciado la sesión Account de Microsoft, solo puede agregar otros Accounts de Microsoft o a los usuarios en el directorio predeterminado de hello como Coadministrador.
* Si inició sesión con una cuenta de organización, puede agregar otras cuentas de organización de su organización como coadministrador. Por ejemplo, abby@contoso.com puede agregar a bob@contoso.com como administrador de servicios o coadministrador, pero no puede agregar a john@notcontoso.com a menos que john@notcontoso.com se encuentre en el directorio predeterminado. Usuarios que han iniciado sesión con cuentas de la organización pueden continuar a los usuarios de tooadd Account de Microsoft como servicio de administrador o Coadministrador.
* Ahora que es posible toosign en tooAzure con una cuenta profesional, incluimos Hola cambios tooService administrador y requisitos de la cuenta de administrador:

  | Método de inicio de sesión | ¿Desea agregar cuentas Microsoft o usuarios del directorio predeterminado como coadministrador o administrador de servicios? | ¿Agregar cuenta profesional en hello misma organización como entidad emisora de certificados o SA? | ¿Desea agregar una cuenta de organización en una organización diferente a la del coadministrador o administrador de servicios? |
  | --- | --- | --- | --- |
  |  Cuenta Microsoft |Sí |No |No |
  |  Cuenta de organización |Sí |Sí |No |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Más información sobre el control de acceso a los recursos y Active Directory
* toolearn más información acerca de cómo se controla el acceso a los recursos en Microsoft Azure, consulte [descripción de acceso a los recursos en Azure](../active-directory/active-directory-understanding-resource-access.md).
* Si desea más información sobre Azure Active Directory, consulte [Asociación de las suscripciones de Azure con Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) y [Asignación de roles de administrador en Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.
