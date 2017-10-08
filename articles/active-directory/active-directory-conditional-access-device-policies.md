---
title: directivas de dispositivo de aaaAzure Active Directory acceso condicional para servicios de Office 365 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toohelp de directivas de dispositivo de acceso condicional de tooprovision proteger los recursos corporativos, manteniendo tooservices de cumplimiento y el acceso de usuario."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Directivas de dispositivos de acceso condicional de Active Directory para servicios de Office 365

Acceso condicional requiere toowork de varias partes. Implica un usuario con autenticación multifactor, un dispositivo autenticado y un dispositivo compatible, entre otros factores. En este artículo, se centra principalmente en condiciones basado en dispositivos que su organización puede utilizar toohelp controlar acceso tooOffice 365 services. 

Los usuarios corporativos desean tooaccess Office 365 servicios como Exchange y SharePoint Online en el trabajo o escuela desde sus dispositivos personales. Desea Hola acceso toobe segura. Puede aprovisionar acceso condicional dispositivo directivas toohelp Asegúrese de los recursos corporativos más seguros, al conceder acceso tooservices para los usuarios que usen dispositivos compatibles. Puede establecer directivas de acceso condicional tooOffice 365 en el portal de acceso condicional de Microsoft Intune Hola.

Azure Active Directory (Azure AD) exige acceso condicional directivas toohelp un acceso seguro tooOffice 365 los servicios. Puede crear una directiva de acceso condicional que impida que un usuario que tenga un dispositivo no compatible pueda obtener acceso a un servicio de Office 365. usuario de Hello debe cumplir las directivas de dispositivo de la compañía toohello antes de que se concede acceso toohello servicio. Como alternativa, puede crear una directiva que requiere que los usuarios tooenroll su tooan de acceso de dispositivos toogain servicio de Office 365. Las directivas pueden ser usuarios tooall aplicados en una organización, o que estén limitadas tooa algunos grupos de destino. Puede agregar más directivas de tooa de grupos de destino con el tiempo.

Un requisito previo para aplicar directivas de dispositivos es que los usuarios deben registrar sus dispositivos con el servicio de registro de dispositivos de hello Azure AD. Puede optar por tooturn en la autenticación multifactor para dispositivos que registrar con hello servicio de registro de dispositivo de Azure AD. Se recomienda la autenticación multifactor para hello servicio de registro de dispositivo de Azure Active Directory. Cuando la autenticación multifactor está activada, los usuarios que registren sus dispositivos con hello servicio de registro de dispositivo de Azure AD deben someterse para la autenticación de segundo factor.

## <a name="how-does-a-conditional-access-policy-work"></a>¿Cómo funcionan las directivas de acceso condicional?

Cuando un usuario solicita acceso tooan servicio de Office 365 desde una plataforma de dispositivos compatibles, Azure AD autentica usuarios de Hola y dispositivos de Hola. Concede acceso toohello servicio de Azure AD solo si el usuario de hello cumple la directiva toohello establecida para el servicio de Hola. Los usuarios en los dispositivos que no están inscritos reciben instrucciones sobre cómo tooenroll y se convierten en tooaccess compatible con servicios de Office 365. Los usuarios de dispositivos iOS y Android es necesario tooenroll sus dispositivos mediante el uso de la aplicación de Portal de empresa Intune hello. Cuando un usuario inscribe un dispositivo, Hola dispositivo está registrado con Azure AD y se ha inscrito para el cumplimiento de normas y la administración de dispositivos. Debe usar el servicio de registro de dispositivo de hello Azure AD con Microsoft Intune para la administración de dispositivos móviles para los servicios de Office 365. Inscripción de dispositivos es necesaria para los usuarios tooaccess servicios de Office 365 cuando se aplican las directivas de dispositivo.

Cuando un usuario inscribe correctamente un dispositivo, el dispositivo de hello sea de confianza. Azure AD proporciona a las aplicaciones de toocompany de acceso de inicio de sesión único de usuario de hello autenticado. Azure AD impone un acceso condicional directiva toogrant tooa servicio de acceso no solo Hola Hola usuario solicita acceso, pero cada vez que lo utiliza Hola renueva una solicitud de acceso. usuario de Hola se deniega acceso tooservices cuando se cambien las credenciales de inicio de sesión, Hola dispositivo se pierde o es robado o no se cumplen condiciones de Hola de directiva de hello en tiempo de saludo de solicitud para la renovación.

## <a name="deployment-considerations"></a>Consideraciones de la implementación

Deben utilizar dispositivos tooregister de servicio de registro de dispositivo de hello Azure AD.

Cuando los usuarios locales va toobe autenticado, los servicios de federación de Active Directory (AD FS) (versión 1.0 y versiones posteriores) es necesario. Se produce un error en la autenticación multifactor para unirse al área de trabajo al proveedor de identidades de hello no es capaz de la autenticación multifactor. Por ejemplo, no puede usar la autenticación multifactor con AD FS 2.0. Asegúrese de que Hola local de AD FS funciona con la autenticación multifactor, y que es un método de autenticación multifactor válida en su lugar antes de activar la autenticación multifactor para el servicio de registro de dispositivo de Azure AD de Hola. Por ejemplo, AD FS en Windows Server 2012 R2 tiene capacidades de autenticación multifactor. También debe establecer un método de autenticación válido adicionales (la autenticación multifactor) en el servidor de AD FS Hola antes de activar la autenticación multifactor para el servicio de registro de dispositivo de hello Azure AD. Para obtener más información sobre los métodos de autenticación multifactor admitidos en AD FS, consulte [Configurar los métodos de autenticación adicional de AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Pasos siguientes

*   Para respuestas toocommon preguntas, consulte [acceso condicional de Azure Active Directory preguntas más frecuentes sobre](active-directory-conditional-faqs.md).
