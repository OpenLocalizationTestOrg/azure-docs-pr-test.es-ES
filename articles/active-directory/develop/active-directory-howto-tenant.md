---
title: aaaHow tooget un inquilino de Azure AD | Documentos de Microsoft
description: "¿Cómo tooget un Azure Active Directory de inquilinos para registrar y generar aplicaciones."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Cómo inquilino tooget Azure Active Directory
En Azure Active Directory (Azure AD), un [inquilino](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) es un representante de una organización.  Es una instancia dedicada de hello servicio de Azure AD que una organización recibe y posee cuando suscribe a un servicio de nube de Microsoft como Office 365, Microsoft Intune o Azure.  Cada inquilino de Azure AD es distinto e independiente de los demás inquilinos de Azure AD.  

Un inquilino aloja a usuarios hello en una empresa y Hola información acerca de ellos, sus contraseñas, los datos de perfil de usuario, permisos y así sucesivamente.  También contiene grupos, aplicaciones y otra información relativa tooan organización y su seguridad.

tooallow toosign de los usuarios de Azure AD en tooyour aplicación, debe registrar la aplicación en un inquilino de su elección.  La publicación de una aplicación en un inquilino de Azure AD es **totalmente gratis**.  De hecho, la mayoría de programadores creará varios inquilinos y aplicaciones para fines de experimentación, desarrollo, almacenamiento provisional y prueba.  Las organizaciones que se suscriban a y usen su aplicación, opcionalmente, pueden elegir toopurchase licencias si lo desean tootake aprovechar las características de directorios avanzada.

Por lo tanto, ¿cómo obtiene un inquilino de Azure AD?  Hello proceso podría ser un poco diferente si es:

* [Dispone de una suscripción de Office 365 existente](#use-an-existing-office-365-subscription)
* [Tiene una suscripción de Azure asociada a una cuenta Microsoft](#use-an-msa-azure-subscription)
* [Dispone de una suscripción de Azure existente asociada a una cuenta organizativa](#use-an-organizational-azure-subscription)
* [Que no tenga ninguno de hello anterior "&" desea toostart desde el principio](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Uso de una suscripción de Office 365 existente
Si dispone de una suscripción a Office 365, ya tiene un inquilino de Azure AD. Puede iniciar sesión toohello [portal de Azure](https://portal.azure.com) con su O365 cuenta y empezar a usar Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Uso de una suscripción de MSA Azure
Si se ha registrado anteriormente en una suscripción de Azure con una cuenta Microsoft individual, ya dispone de un inquilino.  Cuando inicia una sesión toohello [Portal de Azure](https://portal.azure.com), se registrará automáticamente en el inquilino de tooyour predeterminado. Está libre toouse vea este inquilino que caben - pero puede que desee toocreate una cuenta de administrador de organización.

toodo por lo tanto, siga estos pasos.  Como alternativa, puede desea toocreate un nuevo inquilino y crear un administrador en ese inquilino siguiendo un proceso similar.

1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com) con su cuenta individual
2. Navegar por la sección de "Azure Active Directory" toohello del portal de hello (se encuentra en la barra de navegación izquierdo de hello, en **más servicios**)
3. Se debe sesión automáticamente en toohello "Directorio predeterminado", si no puede cambiar directorios haciendo clic en el nombre de cuenta en la esquina superior derecha de Hola.
4. De hello **tareas rápidas** sección, elija **agregar un usuario**.
5. En Hola Agregar formulario de usuario, proporcione Hola detalles siguientes:

   * Nombre: (elija un valor apropiado)
   * Nombre de usuario: (elija un nombre de usuario para este administrador)
   * Perfil: (rellene los valores adecuados para el nombre, nombre de último, puesto que ocupa y departamento hello)
   * Rol: administrador global
6. Cuando se hayan completado Hola Agregar formulario de usuario y recibir una contraseña temporal para el usuario administrativo nuevo de Hola Hola, ser seguro toorecord esta contraseña ya que será necesario toologin con este nuevo usuario en la contraseña de orden toochange Hola. También puede enviar contraseña hello toohello usuario directamente, con un correo electrónico alternativo.
7. Haga clic en **crear** nuevo usuario de toocreate Hola.
8. contraseña temporal toochange hello, inicie sesión en [https://login.microsoftonline.com](https://login.microsoftonline.com) con este nuevo usuario de la cuenta y cambiar la contraseña de hello cuando se solicita.

## <a name="use-an-organizational-azure-subscription"></a>Uso de una suscripción de Azure organizativa
Si se ha registrado anteriormente en una suscripción de Azure con la cuenta organizativa, ya dispone de un inquilino.  Hola [Portal de Azure](https://portal.azure.com), debería encontrar un inquilino al navegar demasiado "Más servicios" y "Azure Active Directory."  Son toouse libre este inquilino como ver ajustarse.

## <a name="start-from-scratch"></a>Comienzo desde cero
Si todo de hello anterior es un texto incomprensible tooyou, no se preocupe.  Basta con que visite [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign en Azure con una nueva organización.  Una vez que ha completado el proceso de hello, tendrá su propio inquilino de Azure AD con nombre de dominio de hello que eligió durante el inicio de sesión de seguridad.  Hola [Portal de Azure](https://portal.azure.com), puede encontrar el inquilino desplazándose demasiado "Azure Active Directory" en NAV de hello izquierdo.

Como parte del proceso de Hola de suscribirse a Azure, será necesario tooprovide detalles de tarjeta de crédito.  Puede continuar con confianza: no se le cobrará por publicar aplicaciones en Azure AD o crear nuevos inquilinos.
