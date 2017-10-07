---
title: las implementaciones de PaaS aaaSecuring | Documentos de Microsoft
description: " Comprender las ventajas de seguridad de Hola de PaaS en comparación con otros modelos de servicio de nube y obtenga información acerca de las prácticas recomendadas para proteger la implementación de PaaS de Azure. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>Protección de implementaciones de PaaS

En este artículo se proporciona información que ayuda a:

- Comprender las ventajas de seguridad de Hola de hospedaje de aplicaciones en la nube de Hola
- Evaluar las ventajas de seguridad de Hola de plataforma como servicio (PaaS) en comparación con otros modelos de servicio de nube
- Cambiar el foco de la seguridad de un enfoque de tooan centrada en la red perimetral centrada en la identidad de seguridad
- Implementar recomendaciones generales de procedimientos recomendados de PaaS

## <a name="cloud-security-advantages"></a>Ventajas de seguridad en la nube
Hay toobeing de ventajas de seguridad en nube Hola. En un entorno local, las organizaciones probablemente tengan responsabilidades inadecuadas y recursos limitados disponibles tooinvest en seguridad, que crea un entorno donde los atacantes están tooexploit capaz de vulnerabilidades en todas las capas.

![Ventajas de seguridad de la era en la nube][1]

Las organizaciones está tooimprove capaz de sus tiempos de respuesta y la detección de amenazas mediante las capacidades de seguridad basada en la nube y la inteligencia de nube de un proveedor.  Al cambiar el proveedor de nube de responsabilidades toohello, las organizaciones pueden obtener más cobertura de seguridad, lo que les permite tooreallocate recursos de seguridad y las prioridades del negocio de tooother de presupuesto.

## <a name="division-of-responsibility"></a>División de responsabilidad
Es importante toounderstand división de Hola de responsabilidad entre usted y Microsoft. De forma local, poseen pila completa de hello, pero como mover en la nube toohello algunas responsabilidades transfiere tooMicrosoft. Hello responsabilidad matriz siguiente muestra las áreas de Hola de pila de hello en una implementación de IaaS, PaaS y SaaS que usted es responsable y es responsable de Microsoft.

![Zonas de responsabilidad][2]

Para todos los tipos de implementación de nube, es propietario de los datos y las identidades. Es responsables de proteger Hola de seguridad de los datos y las identidades de los recursos locales y Hola componentes en la nube que puede controlar (que varía según el tipo de servicio).

Responsabilidades que siempre se conservan por el usuario, independientemente del tipo hello de implementación son:

- Datos
- Puntos de conexión
- Cuenta
- administración de acceso

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Ventajas de seguridad de un modelo de servicio en la nube de PaaS
Usar Hola misma matriz de responsabilidad, echemos un vistazo ventajas de seguridad de Hola de una implementación de PaaS de Azure e implementarlos en local.

![Ventajas de seguridad de PaaS][3]

Empezando por la parte inferior de Hola de pila de hello, infraestructura física de hello, Microsoft mitiga los riesgos comunes y las responsabilidades. Dado que Hola nube de Microsoft se supervisa continuamente con Microsoft, es tooattack de disco duro. No tiene sentido para una Hola de toopursue atacante nube de Microsoft como un destino. A menos que el atacante de hello tiene una gran cantidad de dinero y recursos, el atacante hello es probablemente toomove en tooanother de destino.  

En el centro de Hola de pila de hello, no hay ninguna diferencia entre una implementación de PaaS y local. En el nivel de aplicación de Hola y capa de administración de acceso y la cuenta de hello, tendrá los riesgos similares. En la sección pasos siguiente de Hola de este artículo, le guiaremos toobest prácticas para eliminar o minimizar estos riesgos.

Hola parte superior de la pila de hello, gestión de datos y administración de derechos, realizar un riesgo que se puede mitigar mediante administración de claves. (La administración de claves se cubre en los procedimientos recomendados). Si bien la administración de claves es una responsabilidad adicional, tener áreas en una implementación de PaaS que ya no tienen toomanage por lo que puede cambiar la administración de recursos tookey.

Hola plataforma Windows Azure también proporciona protección frente a DDoS seguro mediante el uso de varias tecnologías basadas en red. Sin embargo, todos los tipos de métodos de protección contra ataques DDoS basados en red tienen sus límites por vínculo y por centro de datos. toohelp evitar el impacto de Hola de ataques de DDoS grandes, puede aprovechar las ventajas de capacidad de nube de Azure fundamental habilitar al usuario tooquickly y automáticamente escalada toodefend frente a ataques de DDoS. Lo veremos más detalles acerca de cómo puede hacer esto en Hola artículos de procedimientos recomendado.

## <a name="modernizing-hello-defenders-mindset"></a>Actitud modernizado Hola defender
Las implementaciones de PaaS conlleva un cambio en su toosecurity enfoque general. Desplazamiento de la necesidad de toocontrol todo usted mismo toosharing responsabilidad con Microsoft.

Otra diferencia importante entre PaaS y las implementaciones locales tradicionales, es una nueva vista de lo que define el perímetro de seguridad principal de Hola. Históricamente, perímetro de seguridad local principal Hola era la red y más local seguridad diseños uso Hola red como su pivot de seguridad principal. Para las implementaciones de PaaS, mejor se sirven teniendo en cuenta el perímetro de seguridad principal de identidad toobe Hola.

## <a name="identity-as-hello-primary-security-perimeter"></a>Identidad que el perímetro de seguridad principal de Hola
Uno de los cinco características fundamentales Hola de informática en nube es acceso amplio a redes, lo que hace centrada en la red pensando menos relevantes. objetivo de Hola de gran parte de la informática en nube es tooallow usuarios tooaccess recursos independientemente de su ubicación. Para la mayoría de los usuarios, su ubicación está sucediendo toobe en algún lugar Hola Internet.

Hello en la ilustración siguiente se muestra cómo ha evolucionado perímetro de seguridad de Hola desde un perímetro de la identidad de la red perimetral tooan. La seguridad se hace menos sobre defiende la red y más información sobre defiende los datos, así como administrar la seguridad de Hola de sus aplicaciones y los usuarios. Hola principal diferencia es que desea que la empresa del toowhat más de cerca de toopush seguridad tooyour importante.

![La identidad como el nuevo perímetro de seguridad][4]

Inicialmente, los servicios PaaS en Azure (por ejemplo, los roles web y Azure SQL) ofrecían poca o ninguna defensa para el perímetro de red tradicional. Se entiende que propósito del elemento de hello era toobe expuesta toohello Internet (rol web) y que la autenticación proporciona Hola nuevo perímetro (por ejemplo, BLOB o SQL Azure).

Prácticas recomendadas de seguridad modernas suponga que adversario Hola ha infringido el perímetro de la red de Hola. Por lo tanto, las prácticas de defensa moderna han movido tooidentity. Las organizaciones deben establecer un perímetro de seguridad basado en identidades con autenticación sólida e higiene de autorización (procedimientos recomendados).

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Recomendaciones para administrar el perímetro de la identidad de Hola

Principios y patrones de perímetro de la red de hello han estado disponibles durante décadas. En cambio, sector de hello tiene relativamente menos experiencia con el uso de identidad como perímetro de seguridad principal de Hola. Dicho esto, se han acumulado suficiente experiencia tooprovide algunas recomendaciones generales que se ha comprobado en el campo de Hola y aplican tooalmost todos los servicios de PaaS.

siguiente Hola resume un toomanaging de enfoque prácticas recomendada generales el perímetro de una identidad.

- **No pierda sus claves o las credenciales** protección de claves y credenciales es esencial toosecure implementaciones de PaaS. La pérdida de claves y credenciales es un problema común. Una buena solución es una solución centralizada de toouse donde se pueden almacenar claves y secretos en módulos de seguridad de hardware (HSM). Azure proporciona un HSM en la nube de hello con [el almacén de claves de Azure](../key-vault/key-vault-whatis.md).
- **No coloque las credenciales y otros secretos en el código fuente o GitHub** Hola sólo lo que es peor algo de perder las credenciales y las claves es tener un tercero no autorizado obtuviera acceso a toothem. Los atacantes son tootake puede aprovechar las claves de bot tecnologías toofind y secretos almacenados en repositorios de código, como GitHub. No coloque las claves ni los secretos en estos repositorios públicos de código fuente.
- **Proteja las interfaces de administración de máquinas virtuales en servicios híbridos IaaS y PaaS** Los servicios IaaS y PaaS se ejecutan en máquinas virtuales (VM). Según el tipo de saludo del servicio, existen varias interfaces de administración que le permiten tooremote administrar estas máquinas virtuales directamente. Se pueden usar protocolos de administración remota como el [Protocolo Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), el [Protocolo de escritorio remoto (RDP)](https://support.microsoft.com/kb/186607) y [PowerShell remoto](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting). En general, se recomienda que no habilita el acceso remoto directo tooVMs de hello Internet. Si están disponibles, debe usar enfoques alternativos como el uso de una red privada virtual en una red virtual de Azure. Si no hay enfoques alternativos disponibles, asegúrese de utilizar frases de contraseña complejas y, si está disponible, la autenticación en dos fases (como [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).
- **Use plataformas sólidas de autenticación y autorización**

  - Use identidades federadas en Azure AD en lugar de tiendas de usuarios personalizadas. Cuando se usa identidades federadas, aprovechar un enfoque basado en la plataforma y delegar la administración de Hola de socios de tooyour identidades autorizados. Un enfoque de identidad federada es especialmente importante en escenarios cuando finalizan los empleados y que debe toobe información refleja a través de varias identidades y autorización sistemas.
  - Use los mecanismos de autenticación y autorización proporcionados en la plataforma en lugar del código personalizado. motivo de Hello es que desarrollar código de autenticación personalizado puede ser propenso a errores. La mayoría de los desarrolladores de software no sean expertos en seguridad y toobe poco probable que tenga en cuenta los matices de Hola y Hola últimos avances autenticación y autorización. El código comercial (por ejemplo, de Microsoft) suele revisarse de manera amplia a efectos de seguridad.
  - Use Multi-factor Authentication. La autenticación multifactor es hello actual estándar para la autenticación y autorización, porque evita puntos débiles de seguridad de hello inherentes a tipos de nombre de usuario y la contraseña de autenticación. Interfaces de administración de Azure (portal remoto o PowerShell) de acceso a tooboth hello y toocustomer servicios orientados al debe diseñarse y configurados toouse [Azure la autenticación multifactor (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Use los protocolos de autenticación estándar, como OAuth2 y Kerberos. Estos protocolos se han sometido a revisiones exhaustivas del mismo nivel y posiblemente se implementen como parte de las bibliotecas de la plataforma a efectos de autenticación y autorización.

## <a name="next-steps"></a>Pasos siguientes
Este artículo se centra en las ventajas de seguridad que ofrece una implementación de PaaS de Azure. A continuación, conozca los procedimientos recomendados para proteger las soluciones móviles y web de PaaS. Se empieza por Azure App Service, Azure SQL Database y Azure SQL Data Warehouse. Artículos sobre procedimientos recomendados para otros servicios de Azure estén disponibles, se proporcionará vínculos en hello lista siguiente:

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database y Azure SQL Data Warehouse](security-paas-applications-using-sql.md)
- Almacenamiento de Azure
- Azure REDIS Cache
- Bus de servicio
- Firewall de aplicaciones web

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
