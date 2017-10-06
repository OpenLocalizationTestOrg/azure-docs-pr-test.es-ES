---
title: "Preguntas más frecuentes de acceso condicional de Active Directory aaaAzure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre el acceso condicional en Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Preguntas más frecuentes sobre el acceso condicional de Azure Active Directory

## <a name="which-applications-work-with-conditional-access-policies"></a>¿Qué aplicaciones funcionan con directivas de acceso condicional?

Para obtener información sobre las aplicaciones que funcionan con directivas de acceso condicional, consulte [Aplicaciones y navegadores que usan reglas de acceso condicional en Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>¿Se aplican directivas de acceso condicional a usuarios de colaboración B2B o invitados?

Se exigen directivas a los usuarios de la colaboración de negocio a negocio (B2B), Sin embargo, en algunos casos, un usuario podría ser capaz de toosatisfy requisitos de la directiva de Hola. Por ejemplo, la organización de un usuario invitado podría no admitir la autenticación multifactor. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>¿Aplica también una directiva de SharePoint Online tooOneDrive para la empresa?

Sí. Una directiva de SharePoint Online tooOneDrive también aplica para la empresa.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>¿Por qué no se puede establecer una directiva en las aplicaciones cliente, como Word o Outlook?

Una directiva de acceso condicional establece los requisitos para obtener acceso a un servicio. Se aplica cuando se produce el servicio de autenticación toothat. Directiva de Hello no se establece directamente en una aplicación cliente. En su lugar, se aplica cuando un cliente llama a un servicio. Por ejemplo, una directiva establecida en SharePoint aplica tooclients llamando a SharePoint. Una directiva establecida en Exchange aplica tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>¿Aplica una directiva de acceso condicional tooservice cuentas?

Las directivas de acceso condicional aplican las cuentas de usuario de tooall. Aquí se incluyen las cuentas de usuario que se usan como cuentas de servicio. A menudo, una cuenta de servicio que se ejecuta desatendida no puede satisfacer los requisitos de Hola de una directiva de acceso condicional. Por ejemplo, se podría requerir una autenticación multifactor. Las cuentas de servicio se pueden excluir de una directiva mediante la configuración de administración de directivas de acceso condicional. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>¿Están disponibles las API Graph para configurar directivas de acceso condicional?

Actualmente no. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>¿Qué es la directiva de exclusión predeterminada de Hola para plataformas de dispositivos no compatibles?

Actualmente, las directivas de acceso condicional se aplican de forma selectiva a los usuarios de dispositivos iOS y Android. Las aplicaciones en otras plataformas de dispositivo, de forma predeterminada, no se ven afectadas por la directiva de acceso condicional de Hola para dispositivos iOS y Android. Un administrador de inquilinos puede elegir toooverride Hola directiva global toodisallow acceso toousers en plataformas que no son compatibles.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>¿Cómo funcionan las directivas de acceso condicional para Microsoft Teams?  

Microsoft Teams se basa principalmente en Exchange Online y SharePoint Online para los principales escenarios de productividad, como las reuniones, los calendarios y el uso compartido de archivos. Directivas de acceso condicional que se establecen para estas aplicaciones de nube aplican los equipos de tooMicrosoft cuando un usuario inicia sesión.

Microsoft Teams también se admite por separado como aplicación de nube en las directivas de acceso condicional de Azure Active Directory. Las directivas de entidad emisora de certificados que están establecidas para una aplicación de nube aplican los equipos de tooMicrosoft cuando un usuario inicia sesión.

Los clientes de escritorio de Microsoft Teams para Windows y Mac admiten la autenticación moderna. La autenticación moderna aporta en función de las aplicaciones cliente de Office de hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft en plataformas de inicio de sesión. 
