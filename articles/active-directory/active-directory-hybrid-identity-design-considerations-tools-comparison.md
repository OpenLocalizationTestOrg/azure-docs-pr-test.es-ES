---
title: "Identidades híbridas: comparación de las herramientas para la integración de directorios | Microsoft Docs"
description: "Esta es la página proporciona una tabla completa que compara Hola diversas herramientas de integración de directorio que pueden usarse para la integración de directorio."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Identidades híbridas: comparación de las herramientas para la integración de directorios de identidades híbridas
Durante años de hello herramientas de integración de directorio de hello tienen crecido y evolucionado.  Este documento es toohelp proporcionan una vista consolidada de estas herramientas y una comparación de características de Hola que están disponibles en cada uno de ellos.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect incorpora componentes de Hola y la funcionalidad que anteriormente se publicó como Dirsync y AAD Sync. Estas herramientas ya no se lanzan individualmente y se incluirán todas las futuras mejoras en actualizaciones tooAzure AD conectarse, para que siempre sepa dónde tooget Hola funcionalidad más reciente.
> 
> DirSync y Sincronización de Azure AD están en desuso. Puede encontrar más información [aquí](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Usar hello sigue clave para cada una de las tablas de Hola.

●  = Ya disponible  
FR = versión futura  
PP = En versión preliminar pública  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud sincronización local
| Característica | Azure Active Directory Connect | Servicios de sincronización de Azure Active Directory (Sincronización de AAD) | Herramienta de sincronización de Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Conectar toosingle bosque de AD local |● |● |● |● |● |
| Conectar toomultiple bosques de AD locales |● |● | |● |● |
| Conectar toomultiple organizaciones de Exchange local |● | | | | |
| Conectar el directorio LDAP de toosingle local |VF | | |● |● |
| Conectar directorios LDAP de toomultiple locales |VF | | |● |● |
| Conectar tooon local AD y directorios LDAP locales |VF | | |● |● |
| Conectar sistemas de toocustom (es decir, SQL, Oracle, MySQL, etcetera) |VF | | |● |● |
| Sincronización de atributos definidos por el cliente (extensiones de directorio) |● | | | | |
| Conectar tooon local HR (es decir, SAP, Oracle eBusiness, PeopleSoft) |VF | | |● |● |
| Es compatible con las reglas de sincronización de FIM y los conectores para el aprovisionamiento de sistemas locales de tooon. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Sincronización de tooOn local en la nube
| Característica | Azure Active Directory Connect | Servicios de sincronización de Azure Active Directory | Herramienta de sincronización de Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Escritura diferida de dispositivos |● | |● | | |
| Escritura diferida de atributos (para la implementación híbrida de Exchange) |● |● |● |● |● |
| Escritura diferida de objetos de grupos |● | | | | |
| Escritura diferida de contraseñas (desde autoservicio de restablecimiento de contraseña [SSPR] y cambio de contraseña) |● |● | | | |

## <a name="authentication-feature-support"></a>Compatibilidad con características de autenticación
| Característica | Azure Active Directory Connect | Servicios de sincronización de Azure Active Directory | Herramienta de sincronización de Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Sincronización de contraseñas para bosque de AD local |● |● |● | | |
| Sincronización de contraseñas para varios bosques de AD locales |● |● | | | |
| Inicio de sesión único con federación |● |● |● |● |● |
| Escritura diferida de contraseñas (desde SSPR y cambio de contraseña) |● |● | | | |

## <a name="set-up-and-installation"></a>Configuración e instalación
| Característica | Azure Active Directory Connect | Servicios de sincronización de Azure Active Directory | Herramienta de sincronización de Azure Active Directory (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Admite la instalación de un controlador de dominio |● |● |● | |
| Admite la instalación con SQL Express |● |● |● | |
| Actualización sencilla desde DirSync |● | | | |
| Localización de administración UX tooWindows idiomas de servidor |● |● |● | |
| Localización del usuario final UX tooWindows idiomas de servidor | | | |● |
| Compatibilidad con Windows Server 2008 y Windows Server 2008 R2 |● para sincronización, no para federación |● |● |● |
| Compatibilidad con Windows Server 2012 y Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtrado y configuración
| Característica | Azure Active Directory Connect | Servicios de sincronización de Azure Active Directory | Herramienta de sincronización de Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtrar según dominios y unidades organizativas |● |● |● |● |● |
| Filtrar según valores de atributo de los objetos |● |● |● |● |● |
| Permitir que el conjunto mínimo de toobe de atributos sincronizado (MinSync) |● |● | | | |
| Permitir toobe de plantillas de servicio diferente aplicada para flujos de atributos |● |● | | | |
| Permitir la eliminación de atributos del flujo de AD tooAzure AD |● |● | | | |
| Permitir personalización avanzada para flujos de atributo |● |● | |● |● |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

