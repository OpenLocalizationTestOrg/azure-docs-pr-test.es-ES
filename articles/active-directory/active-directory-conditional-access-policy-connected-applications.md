---
title: directivas de acceso condicional basado en dispositivos de Azure Active Directory de aaaConfigure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las directivas de acceso condicional basado en dispositivos de Azure Active Directory tooconfigure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Configuración de directivas de acceso condicional basadas en dispositivos de Azure Active Directory

Con el [acceso condicional de Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), puede ajustar el modo en que los usuarios autorizados pueden tener acceso a sus recursos. Por ejemplo, limitar los dispositivos tootrusted Hola access toocertain recursos. Una directiva de acceso condicional que requiere un dispositivo de confianza se conoce también como directiva de acceso condicional basada en dispositivos.

Este tema proporciona información sobre cómo condicional basado en dispositivos de tooconfigure tener acceso a las directivas de aplicaciones Azure conectada a AD. 


## <a name="before-you-begin"></a>Antes de empezar

El acceso condicional basado en dispositivos une el **acceso condicional de Azure AD** y la **administración de dispositivos de Azure AD**. Si no está familiarizado con una de estas áreas aún, debe leer Hola siguientes temas, en primer lugar:

- **[Acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -este tema proporciona información general y conceptual de instrucción condicional acceso y Hola terminología relacionada.

- **[Administración de toodevice de introducción en Azure Active Directory](device-management-introduction.md)**  -en este tema se ofrece una visión general de hello diversas opciones que tooconnect dispositivos con Azure AD. 


## <a name="trusted-devices"></a>Dispositivos de confianza

En un mundo móvil en primer lugar, basado en la nube, Azure Active Directory permite toodevices de inicio de sesión único, las aplicaciones y servicios desde cualquier lugar. Para determinados recursos en su entorno, conceder acceso de usuarios deseados toohello podrían no ser suficientemente buenos. Además toohello usuarios deseados, también podría necesitar que un dispositivo de confianza toobe utiliza tooaccess un recurso. En su entorno, puede definir lo que un dispositivo de confianza se basa en Hola siguientes componentes:

- Hola [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) en un dispositivo
- Si un dispositivo es compatible
- Si un dispositivo está unido a un dominio 

Hola [plataformas de dispositivos](active-directory-conditional-access-azure-portal.md#device-platforms) se caracteriza por sistema operativo de Hola que se ejecuta en el dispositivo. En la directiva de acceso condicional basado en el dispositivo, puede limitar el acceso toocertain recursos toospecific plataformas de dispositivos.



En una directiva de acceso condicional basado en el dispositivo, puede requerir toobe de dispositivos de confianza marcado como compatible.

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Los dispositivos se pueden marcar como cumplen los requisitos de directorio Hola por:

- Intune 
- Un sistema de administración de dispositivos móviles de terceros integrado con Azure AD  

Solo los dispositivos que están conectado tooAzure AD se pueden marcar como conformes. tooconnect un tooAzure dispositivo Active Directory, deberá Hola siguientes opciones: 

- Registrado en Azure AD
- Unido a Azure AD
- Híbrido unido a Azure AD

    ![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Si tiene una superficie de Active Directory (AD) local, podría considerar dispositivos que no están conectado tooAzure AD pero toobe tooyour combinadas AD de confianza.

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Pasos siguientes

Antes de configurar una directiva de acceso condicional basado en el dispositivo en su entorno, debe Eche un vistazo a hello [las prácticas recomendadas para el acceso condicional en Azure Active Directory](active-directory-conditional-access-best-practices.md).

