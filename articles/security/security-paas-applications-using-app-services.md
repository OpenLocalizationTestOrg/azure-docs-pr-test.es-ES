---
title: "aaaSecuring PaaS web y aplicaciones móviles con servicios de aplicaciones de Azure | Documentos de Microsoft"
description: " Obtenga información sobre los procedimientos recomendados de seguridad de Azure App Services para proteger las aplicaciones web y móviles PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Protección de aplicaciones web y móviles PaaS con Azure App Services

En este artículo se expone una colección de procedimientos recomendados de seguridad de [Azure App Services](https://azure.microsoft.com/services/app-service/) para proteger las aplicaciones web y móviles PaaS. Estas prácticas recomendadas se derivan de nuestra experiencia con Azure y experiencias de Hola de clientes como usted mismo.

## <a name="azure-app-services"></a>Azure App Services
[Servicios de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) es una oferta de PaaS que le permite crear aplicaciones móviles para cualquier plataforma o dispositivo y web y conéctese toodata en cualquier lugar, en la nube de Hola o de forma local. Servicios de aplicaciones incluye web hello y capacidades de dispositivos móviles que previamente se han entregado por separado como sitios Web de Azure y servicios móviles de Azure. También incluye nuevas funcionalidades para automatizar procesos empresariales y hospedar las API en la nube. Como un único servicio integrado, servicios de aplicaciones ofrece un amplio conjunto de capacidades escenarios tooweb, móviles y la integración.

toolearn más información, consulte información general sobre [aplicaciones móviles](../app-service-mobile/app-service-mobile-value-prop.md) y [aplicaciones Web](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Prácticas recomendadas

Al usar App Services, siga estos procedimientos recomendados:

- [Autenticación mediante Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). App Services proporciona un servicio de OAuth 2.0 para el proveedor de identidades. OAuth 2.0 se centra en la sencillez del desarrollador del cliente y ofrece flujos de autorización específicos de aplicaciones web, aplicaciones de escritorio y teléfonos móviles. Azure AD usa OAuth 2.0 tooenable que tooauthorize acceso toomobile y las aplicaciones web.
- Restringir el acceso en función de hello necesidad tooknow y principios de seguridad de privilegios mínimos. Restringir el acceso es fundamental para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos. Control de acceso basado en roles (RBAC) puede ser usado tooassign permisos toousers, grupos y aplicaciones en un ámbito determinado. vea toolearn más acerca de cómo conceder a los usuarios tener acceso a tooapplications, [Introducción a administración de acceso](../active-directory/role-based-access-control-what-is.md).
- Protección de las claves. No importa la calidad de la seguridad si pierde las claves de suscripción. El Almacén de claves de Azure ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Mediante el uso de Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .PFX y contraseñas) a través del uso de claves que están protegidas por módulos de seguridad de hardware (HSM). Para tener mayor seguridad, puede importar o generar las claves en HSM. Vea [el almacén de claves de Azure](../key-vault/key-vault-whatis.md) toolearn más. También puede usar el almacén de claves toomanage sus certificados TLS con renovación automática.
- Restricción de las direcciones IP de origen entrantes. [App Services Environment](../app-service-web/app-service-app-service-environment-intro.md) tiene una característica de integración de la red virtual que ayuda a restringir las direcciones IP de origen entrantes mediante grupos de seguridad de red (NSG). Si no está familiarizado con las redes virtuales de Azure (redes virtuales), esto es una funcionalidad que permite tooplace muchos de los recursos de Azure en una red enrutable no internet que usted controla el acceso a. más información, consulte toolearn [integre su aplicación con una red Virtual de Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Pasos siguientes
En este artículo se introdujo tooa colección de prácticas recomendadas de seguridad de servicios de aplicaciones para proteger sus PaaS web y aplicaciones móviles. toolearn más acerca de cómo proteger las implementaciones de PaaS, vea:

- [Protección de implementaciones de PaaS](security-paas-deployments.md)
- [Protección de aplicaciones web y móviles PaaS con Azure SQL Database y SQL Data Warehouse](security-paas-applications-using-sql.md)
