---
title: "Características de Azure AD Connect en la versión preliminar | Microsoft Docs"
description: "En este tema se describen más detenidamente las características que se encuentran en la versión preliminar en Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Más detalles sobre las características de vista previa
Este tema describe cómo toouse características actualmente en vista previa.

## <a name="group-writeback"></a>Escritura diferida de grupos
opción de Hola para reescritura de grupos de características opcionales permite toowriteback **grupos de Office 365** tooa bosque con Exchange instalado. Se trata de un grupo que siempre se controla en la nube de Hola. Si tiene Exchange local, a continuación, puede escribir nuevo estos grupos tooon local para que los usuarios con un buzón de Exchange local pueden enviar y recibir mensajes de correo electrónico de estos grupos.

Para obtener más información acerca de los grupos de Office 365 y cómo toouse les pueden encontrarse [aquí](http://aka.ms/O365g).

Este grupo de Office 365 se representará como un grupo de distribución en AD DS local. El servidor de Exchange local debe estar en la actualización acumulativa de Exchange 2013 8 (publicada en marzo de 2015) o Exchange 2016 toorecognize este nuevo tipo de grupo.

**Notas durante la vista previa de Hola**

* atributo de libreta de direcciones Hola actualmente no se rellena en la vista previa de Hola. Sin este atributo, grupo de hello no está visible en hello GAL. Hola toopopulate de manera más fácil este atributo es el cmdlet de PowerShell de Exchange de hello toouse `update-recipient`.
* Solo bosques con el esquema de Exchange Hola constituyen destinos válidos para los grupos. Si se ha detectado ningún cambio, a continuación, reescritura de grupos no es posible tooenable.
* Actualmente solo se admiten las implementaciones de organizaciones de Exchange de un solo bosque. Si tiene más de una organización de Exchange en local, a continuación, necesita una local GALSync solución para estos tooappear grupos en los otros bosques.
* característica de reescritura de grupos de Hello no controla los grupos de seguridad o grupos de distribución.

> [!NOTE]
> Un tooAzure de suscripción AD Premium es necesario para la reescritura de grupos.
> 
>

## <a name="user-writeback"></a>Reescritura de usuarios
> [!IMPORTANT]
> Hello característica de vista previa de reescritura de usuario se quitó en tooAzure de actualización de agosto de 2015 Hola AD Connect. Si la ha habilitado, debería deshabilitarla.
>
>

## <a name="next-steps"></a>Pasos siguientes
Continúe su [Instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
