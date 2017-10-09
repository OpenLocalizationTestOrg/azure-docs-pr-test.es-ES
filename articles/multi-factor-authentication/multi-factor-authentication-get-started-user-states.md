---
title: "aaaMicrosoft Estados de usuario de autenticación multifactor de Azure"
description: "Obtenga información sobre los estados de usuario en Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>¿Cómo toorequire verificacion de un usuario o grupo

Existen dos enfoques para exigir la verificación en dos pasos. Hola primera opción es tooenable cada usuario individual para Azure Multi-factor Authentication (MFA). Cuando los usuarios se habilitan de forma individual, siempre realizan la verificación en dos pasos (con algunas excepciones, como cuando inician sesión desde direcciones IP de confianza o si se recuerda Hola característica de dispositivos está activado). Hola segunda opción es tooset una directiva de acceso condicional que requiere la verificación en dos pasos en determinadas condiciones.

>[!TIP] 
>Elija uno de estos métodos toorequire verificacion, no ambos. La habilitación de un usuario para Azure MFA invalida las directivas de acceso condicional.

## <a name="which-option-is-right-for-you"></a>Cuál es la opción adecuada para usted

**Habilitar MFA de Azure mediante el cambio de estado de usuario** es Hola enfoque tradicional para exigir la verificación en dos pasos. Funciona para ambos MFA de Azure en la nube de Hola y el servidor de MFA de Azure. Todos los usuarios de Hola que permiten tener Hola misma experiencia, que es tooperform verificacion cada vez que inicien sesión. La habilitación de un usuario invalida las directivas de acceso condicional que pudieran afectar a dicho usuario. 

**Habilitar Azure MFA con una directiva de acceso condicional** es un enfoque más flexible para exigir la verificación en dos pasos. Solo funciona para Azure MFA en la nube de hello, sin embargo, y el acceso condicional es un [característica de Azure Active Directory de pago](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Puede crear directivas de acceso condicional que se aplican toogroups, así como los usuarios individuales. Los grupos de alto riesgo pueden recibir más restricciones que los grupos de bajo riesgo o bien la verificación en dos pasos puede ser necesaria solo para aplicaciones de alto riesgo en la nube y omitida para las de bajo riesgo. 

Estas dos opciones solicitar tooregister de los usuarios para saludo de la autenticación multifactor Azure primera vez que inicien sesión después de activar los requisitos de Hola. Ambas opciones también funcionan con hello configurable [configuración de autenticación multifactor de Azure](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Habilitar Azure MFA mediante el cambio de estado del usuario

Cuentas de usuario de la autenticación multifactor Azure tienen Hola después de tres estados distintos:

| Estado | Descripción | Aplicaciones que no son de explorador afectadas |
|:---:|:---:|:---:|
| Disabled |estado de Hello predeterminado para un usuario nuevo no inscrito Azure la autenticación multifactor (MFA). |No |
| habilitado |usuario de Hola se ha inscrito en Azure MFA, pero no se ha registrado. Estarán Hola solicitadas tooregister próxima vez que inicie sesión. |No.  Se siguen toowork hasta que se complete el proceso de registro de hello. |
| Aplicado |usuario de Hola se ha inscrito y ha completado el proceso de registro de hello para Azure MFA. |Sí.  Las aplicaciones requieren contraseñas de aplicación. |

Estado de un usuario refleja si un administrador ha inscrito ellos en Azure MFA, y si ha completado el proceso de registro de hello.

Todos los usuarios comienzan con el estado *Deshabilitado*. Cuando inscribe usuarios en Azure MFA, cambia a *Habilitado*. Cuando los usuarios habilitados iniciar sesión y completar el proceso de registro de hello, su estado cambia demasiado*aplica*.  

### <a name="view-hello-status-for-a-user"></a>Ver el estado de Hola para un usuario

Hola de uso después de pasos tooaccess Hola página donde puede ver y administrar los Estados de usuario:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Vaya demasiado**Azure Active Directory** > **usuarios y grupos** > **todos los usuarios**.
3. Seleccione **Multi-Factor Authentication**.
   Seleccione ![Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Se abre una nueva página, que muestra los Estados de usuario de hello.
   ![Estado de usuario de Multi-Factor Authentication (captura de pantalla)](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Cambiar estado de Hola para un usuario

1. Usar hello delante de la página de usuarios de la autenticación multifactor de pasos tooget toohello.
2. Buscar usuario de Hola que quiere tooenable de MFA de Azure. Puede que necesite toochange Hola vista en la parte superior de Hola. 
   ![Búsqueda de usuario (captura de pantalla)](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Compruebe el nombre de tootheir de hello cuadro siguiente.
4. En hello derecha, bajo pasos rápidos, elija **habilitar** o **deshabilitar**.
   ![Habilitación del usuario seleccionado (captura de pantalla)](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Habilitado* a los usuarios cambian automáticamente demasiado*aplica* cuando registre para Azure MFA. No debe cambiar manualmente tooenforced de estado de usuario de Hola. 

5. Confirme la selección en la ventana emergente de Hola que se abre. 

Después de habilitar los usuarios, debe notificarlos por correo electrónico. Indicar que se le pedirá hello tooregister próxima vez que inicie sesión. Además, si su organización utiliza aplicaciones sin explorador que no son compatibles con la autenticación moderna, deberán toocreate contraseñas de aplicación. También puede incluir un vínculo tooour [Guía del usuario final de Azure MFA](./end-user/multi-factor-authentication-end-user.md) toohelp a empezar a trabajar.

### <a name="use-powershell"></a>Uso de PowerShell
toochange Hola usuario estado estado utilizando [PowerShell de Azure AD](/powershell/azure/overview), cambiar `$st.State`. Hay tres estados posibles:

* habilitado
* Aplicado
* Disabled  

No se mueven a los usuarios directamente toohello *forzado* estado. Aplicaciones basadas en el explorador no dejará de funcionar porque el usuario hello no ha pasado a través del registro MFA y obtenido una [contraseña de aplicación](multi-factor-authentication-whats-next.md#app-passwords). 

Uso de PowerShell es una buena opción si necesita toobulk permitiendo a los usuarios. Cree un script de PowerShell que recorre en iteración una lista de usuarios y los habilita:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Aquí tiene un ejemplo:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Habilitar Azure MFA con una directiva de acceso condicional

El acceso condicional es una característica de pago de Azure Active Directory, con muchas opciones de configuración posibles. Estos pasos describe una manera de toocreate una directiva. Para más información, consulte [Acceso condicional en Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Vaya demasiado**Azure Active Directory** > **acceso condicional**.
3. Seleccione **Nueva directiva**.
4. En **Asignaciones**, seleccione **Usuarios y grupos**. Hola de uso **Include** y **excluir** pestañas toospecify qué usuarios y grupos serán administrada por directiva Hola.
5. En **Asignaciones**, seleccione **Aplicaciones en la nube**. Elija tooinclude **todas las aplicaciones de la nube**.
6. En **Controles de acceso**, seleccione **Conceder**. Seleccione **Requerir autenticación multifactor**.
7. Activar **habilitar Directiva de** demasiado**en** y, a continuación, seleccione **guardar**.

Hello otras opciones de directiva de acceso condicional de hello permiten toospecify exactamente cuándo debe exigirse la verificación en dos pasos. Por ejemplo, podría realizar una directiva que indica: cuando contratistas intentan tooaccess nuestra aplicación de compras desde las redes que no se confía en los dispositivos que no están unidos a un dominio, requieren verificación en dos pasos. 

## <a name="next-steps"></a>Pasos siguientes

- Obtenga sugerencias sobre hello [las prácticas recomendadas para el acceso condicional](../active-directory/active-directory-conditional-access-best-practices.md)

- Administrar la configuración de Multi-Factor Authentication de [los usuarios y sus dispositivos](multi-factor-authentication-manage-users-and-devices.md)