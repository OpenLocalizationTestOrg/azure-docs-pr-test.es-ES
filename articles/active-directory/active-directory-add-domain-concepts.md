---
title: "información general de aaaConceptual de nombres de dominio personalizado en Azure Active Directory | Documentos de Microsoft"
description: "Explica el marco conceptual de hello para el uso de nombres de dominio personalizado en Azure Active directory, incluida la federación para el inicio de sesión único"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Información general conceptual de nombres de dominio personalizado en Azure Active Directory
Un nombre de dominio puede ser un identificador importante para muchos recursos de directorio, como parte de:

* Un nombre de usuario o una dirección de correo electrónico de un usuario
* dirección de Hola para un grupo
* URI del Id. de aplicación de Hello para una aplicación

Un recurso en Azure Active Directory (Azure AD) puede incluir un nombre de dominio que ya se comprobó toobe propiedad de directorio de Hola que contiene recursos de Hola. Solo los administradores globales pueden realizar tareas de administración de Azure AD.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo toomanage los nombres de dominio en el centro de administración de hello Azure AD, consulte [administrar nombres de dominio personalizado en Azure Active Directory](active-directory-domains-manage-azure-portal.md).

Los nombres de dominio en Azure AD son únicos globalmente. Un nombre de dominio personalizado puede utilizarlo un único inquilino de Azure AD a la vez. Si un directorio de Azure AD ha comprobado un nombre de dominio, ningún otro directorio de Azure AD puede comprobar o usar ese mismo nombre de dominio.

## <a name="initial-and-custom-domain-names"></a>Nombres de dominio personalizados e iniciales
Cada nombre de dominio en Azure AD es un nombre de dominio inicial o un nombre de dominio personalizado.

Cada Azure AD incluye un nombre de dominio inicial en hello formulario contoso.onmicrosoft.com. Este nombre de dominio de nivel tercer, en este ejemplo, "contoso.onmicrosoft.com", se estableció cuando se creó el directorio de hello, normalmente por Hola, administrador que creó el directorio de Hola. no se modificará ni eliminará el nombre de dominio inicial de Hola para un directorio. nombre de dominio inicial de Hello, aunque es totalmente funcional, está pensado principalmente toobe utilizado como un mecanismo de arranque hasta que un nombre de dominio personalizado se comprueba.

En la mayoría de los entornos de producción, un directorio tiene al menos un dominio personalizado comprobado, por ejemplo, "contoso.com", y es ese dominio personalizado que está tooend visible a los usuarios. Un nombre de dominio personalizado es un nombre de dominio que pertenece a la organización que lo utiliza (por ejemplo, "contoso.com") para fines como el alojamiento de su sitio web. Este nombre de dominio es familiar tooemployees porque es parte del nombre de usuario de Hola que use toosign en la red corporativa de toohello o toosend y recuperar el correo electrónico.

Antes de que se puede utilizar Azure AD, nombre de dominio personalizado de hello debe ser directorio tooyour agregado y comprobado.

## <a name="verified-and-unverified-domain-names"></a>Nombres de dominio comprobados y no comprobados
nombre de dominio inicial de Hola para un directorio implícitamente se evalúa como comprobado por Azure AD. Cuando un administrador agrega un tooan de nombre de dominio personalizado Azure AD, inicialmente se encuentra en un estado no comprobado. Azure AD no permitirá cualquier toouse de recursos de directorio un nombre de dominio no comprobado. Esto garantiza que solo un directorio puede usar un nombre de dominio en particular, y que organización hello usa el nombre de dominio de hello realmente posee ese nombre de dominio.

Azure AD comprueba la propiedad de un nombre de dominio, busque una entrada determinada en el archivo de zona de servicio (de dominio DNS) en nombre de dominio de Hola para nombre de dominio de Hola. propiedad tooverify de un nombre de dominio, un administrador obtiene Hola DNS entrada de Azure AD que Azure AD buscará y agrega ese archivo de zona DNS de toohello de entrada para el nombre de dominio de Hola. archivo de zona DNS de Hello es mantenido por el registrador de nombres de dominio de Hola para ese dominio. Hola pasos tooverify un dominio se muestran en el artículo de Hola para [agregar un directorio de Azure AD tooyour de dominio personalizado](active-directory-add-domain.md).

Agregar un archivo de zona DNS toohello de entrada para el nombre de dominio de hello no afecta a otros servicios de dominio, como correo electrónico o la de alojamiento web.

## <a name="federated-and-managed-domain-names"></a>Nombres de dominio federados y administrados
Un nombre de dominio personalizado en Azure AD pueden ser usuarios de toogive configurado un inicio de sesión federado experiencia entre su Active Directory en local y Azure AD. Configurar un dominio para la federación necesita actualiza tooprivileged recursos en Azure AD y también tooyour Windows Server Active Directory. La configuración de un dominio federado debe realizarse desde Azure AD Connect o con PowerShell. Federar un dominio personalizado no se puede iniciar desde el portal de Azure clásico Hola. [Vea este vídeo toolearn sobre la configuración de AD FS para el inicio de sesión de usuario con Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Los dominios que no están federados a veces se denominan dominios administrados. dominio inicial de Hola para un directorio de Azure AD implícitamente se evalúa como un dominio administrado.

## <a name="primary-domain-names"></a>Nombres de dominio principales
nombre de dominio principal para un directorio Hello es nombre de dominio de Hola que está preseleccionada como valor predeterminado de Hola para parte del nombre de usuario de hello, hello 'dominio' cuando un administrador crea un nuevo usuario en hello [portal de Azure](https://portal.azure.com/), o en otro portal como el portal de administración de Office 365 Hola o portal de Microsoft Intune Hola. Un directorio puede tener solo un nombre de dominio principal. Un administrador puede cambiar toobe de nombre de dominio principal de hello cualquier dominio personalizado comprobado que no es federada o toohello inicial del dominio.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Nombres de dominio en Azure AD y otros servicios Microsoft Online Services
El nombre de dominio debe comprobarse en Azure AD antes de poder ser utilizado por otros servicios Microsoft Online Services, como Exchange Online, SharePoint Online e Intune. Normalmente, estos otros servicios requieren un tooadd administrador una o más entradas DNS que son toohello determinado del servicio.

Una aplicación web de Azure usa su propio mecanismo tooverify la propiedad de un dominio. El dominio debe comprobarse para su uso con Azure AD, incluso si se ha hecho anteriormente para que lo utilice una aplicación web de Azure en una suscripción que depende de dicha instancia de Azure AD. Una aplicación web de Azure puede utilizar un nombre de dominio que se ha comprobado en un directorio distinto del directorio de Hola que protege la aplicación web de hello.

## <a name="managing-domain-names"></a>Administración de nombres de dominio
Pueden completar las tareas de administración de dominios de portal de Azure clásico de Hola y de PowerShell. Muchas tareas pueden realizarse mediante la API de Azure AD Graph Hola.

* [Utilización de nombres de dominio personalizados para simplificar la experiencia de inicio de sesión de los usuarios](active-directory-add-domain.md)
* [Administración de dominios en hello portal de Azure clásico](active-directory-add-manage-domain-names.md)
* [Usar nombres de dominio de toomanage de PowerShell de Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Usar nombres de dominio de hello Azure AD Graph API toomanage en Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

