---
title: "Azure Active Directory Domain Services: Habilitación de la delegación restringida de kerberos | Microsoft Docs"
description: "En este artículo se explica cómo habilitar la delegación restringida de kerberos en dominios administrados de Azure Active Directory Domain Services."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Configuración de la delegación restringida de kerberos (KCD) en un dominio administrado
Muchas aplicaciones necesitan recursos tooaccess en contexto de saludo del usuario de Hola. Active Directory admite un mecanismo denominado "delegación de kerberos", que posibilita este caso de uso. Además, puede restringir la delegación para que sólo recursos específicos son accesibles en el contexto de Hola de usuario de Hola. Los dominios administrados de Azure AD Domain Services son diferentes de los tradicionales de Active Directory, puesto que se bloquean de forma más segura.

Este artículo muestra cómo tooconfigure kerberos había restringida la delegación en un dominio administrado de los servicios de dominio de AD de Azure.

## <a name="kerberos-constrained-delegation-kcd"></a>Delegación restringida de kerberos (KCD)
La delegación de Kerberos permite una tooimpersonate cuenta recursos de tooaccess principal (por ejemplo, un usuario) de seguridad de otro. Considere la posibilidad de una aplicación web que tiene acceso a una API de back-end web en el contexto de Hola de un usuario. En este ejemplo, hello aplicación web (que se ejecuta en el contexto de Hola de una cuenta de servicio o una cuenta de equipo) suplanta a Hola usuario al tener acceso a recursos de hello (API de back-end web). La delegación de Kerberos es insegura porque no restringe Hola Hola recursos suplantando la cuenta puede tener acceso a en contexto de saludo del usuario de Hola.

Delegación limitada de Kerberos (KCD) restringe Hola servidor especificado de servicios y recursos toowhich Hola puede actuar en nombre de Hola de un usuario. KCD tradicionales requiere tooconfigure de privilegios de administrador de dominio una cuenta de dominio para un servicio y restringe tooa único dominio de cuenta de hello.

Asimismo, tiene algunos problemas inherentes. En versiones anteriores del sistema operativo donde el administrador del dominio de hello configurado servicio Hola, Administrador de servicios de Hola no tenía ningún tooknow de manera útil qué servicios front-end delegada toohello servicios de recurso que poseían. Y cualquier servicio front-end que podía delegar tooa el servicio de recursos representaba un punto de ataque potencial. Si se pone en peligro un servidor que hospeda un servicio front-end y estaba configurado toodelegate tooresource services, servicios de recurso de hello también podían verse comprometidos.

> [!NOTE]
> En un dominio administrado de Azure AD Domain Services, no tiene privilegios de administrador de dominios. Por lo tanto, **la KCD tradicional no se puede configurar en un dominio administrado**. Use la KCD basada en recursos, como se describe en este artículo. Este mecanismo también es más seguro.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Delegación restringida de kerberos basada en recursos
En Windows Server 2012 R2 y Windows Server 2012, se ha transferido delegación de hello capacidad tooconfigure limitada para servicio de Hola desde Administrador de servicios de toohello de administrador de dominio de Hola. De esta manera, el administrador del servicio back-end de hello puede permitir o denegar servicios front-end. Este modelo se conoce como **delegación restringida de kerberos basada en recursos**.

La KCD basada en recursos se configura mediante PowerShell. Usar Set-ADComputer de Hola o los cmdlets Set-ADUser, dependiendo de si Hola suplantando la cuenta es una cuenta de equipo o una cuenta de servicio o cuenta de usuario.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Configuración de la KCD basada en recursos para una cuenta de equipo de un dominio administrado
Suponga que tiene una aplicación web que se ejecuta en el equipo de hello ' contoso100-webapp.contoso100.com'. Necesita recursos de hello tooaccess (una API web que se ejecutan en ' contoso100-api.contoso100.com') en el contexto de Hola de usuarios del dominio. Este es el procedimiento para configurar la KCD basada en recursos para este escenario.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Configuración de la KCD basada en recursos para una cuenta de usuario de un dominio administrado
Suponga que tiene una aplicación web que se ejecuta como una cuenta de servicio 'appsvc' y necesita recursos de hello tooaccess (una API web que se ejecuta como una cuenta de servicio: 'backendsvc') en el contexto de Hola de usuarios del dominio. Este es el procedimiento para configurar la KCD basada en recursos para este escenario.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Introducción a la delegación limitada de kerberos](https://technet.microsoft.com/library/jj553400.aspx)
