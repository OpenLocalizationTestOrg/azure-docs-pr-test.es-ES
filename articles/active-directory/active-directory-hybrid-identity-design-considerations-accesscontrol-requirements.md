---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de control de acceso | Documentos de Microsoft"
description: "Portadas Hola pilares de identidad y los requisitos de acceso de identificación de los recursos para los usuarios en un entorno híbrido."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Determinación de los requisitos de control de acceso para la solución de identidad híbrida
Cuando se está diseñando una organización su solución de identidad híbrida también pueden usar esta oportunidad tooreview acceder a los requisitos para los recursos de Hola que están organizando toomake estén disponibles para los usuarios. acceso a datos de Hello entre todos los cuatro pilares de identidad, que son:

* Administración
* Autenticación
* Autorización
* Auditoría

secciones de Hola que sigue cubrirá autenticación y autorización con más detalle, administración y auditoría forman parte del ciclo de vida de identidad híbrida de Hola. Lea [Determinación de las tareas de administración de identidad híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) para más información acerca de estas funcionalidades.

> [!NOTE]
> Lectura [Hola cuatro pilares de la identidad - Identity Management Hola edad de TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) para obtener más información acerca de cada una de esas columnas.
> 
> 

## <a name="authentication-and-authorization"></a>Autenticación y autorización
Hay escenarios diferentes para la autenticación y autorización, estos escenarios tendrá requisitos específicos que deben cumplirse mediante la solución de identidad híbrida de Hola que empresa hello es tooadopt continuo. Escenarios que implican tooBusiness de negocio (B2B) comunicación puede agregar un desafío adicional para los administradores de TI ya que necesitan tooensure que el método de autenticación y autorización de hello, utilizado por la organización de hello puede comunicarse con sus socios comerciales. Durante la Hola diseñar el proceso para los requisitos de autenticación y autorización, asegúrese de respuestas a esa Hola siguientes preguntas:

* ¿Su organización va a autenticar y autorizar solamente a los usuarios ubicados en su sistema de administración de identidades?
  * ¿Existen planes para escenarios B2B?
  * En caso afirmativo, ¿ya sabe qué protocolos (SAML, OAuth, Kerberos, Tokens o certificados) le puede tooconnect usa dos empresas?
* ¿Solución de identidad híbrida de Hola que se van tooadopt admite estos protocolos?

Otro tooconsider punto importante es donde se ubicarán los repositorios de autenticación de Hola que utilizarán los usuarios y socios y Hola modelo administrativo toobe usa. Considere la posibilidad de hello siguientes dos opciones principales:

* Centralizado: en este Hola modelo las credenciales del usuario, las directivas y administración pueden ser centralizado en un entorno local o en la nube de Hola.
* Híbrido: en este Hola de modelo las credenciales del usuario, las directivas y administración será centralizado en un entorno local y se replica de una en la nube de Hola.

Qué modelo de su organización adopte varían los requerimientos del negocio tootheir correspondiente, que le interese hello tooanswer después preguntas tooidentify donde residen sistema de administración de identidades de Hola y Hola toouse de modo de administrador:

* ¿Su organización cuenta actualmente con administración de identidades local?
  * En caso afirmativo, ¿piensan tookeep él?
  * ¿Hay algún requisito de cumplimiento o normativa que su organización debe seguir que indica dónde debe residir sistema de administración de identidades de hello?
* ¿Su organización utiliza un inicio de sesión único para aplicaciones que se encuentran en local o en la nube de hello?
  * ¿En caso afirmativo, la adopción de un modelo de identidad híbrida Hola afecta este proceso?

## <a name="access-control"></a>Control de acceso
Mientras que la autenticación y autorización son datos core elementos tooenable acceso toocorporate mediante la validación del usuario, también es de nivel de hello toocontrol importante de acceso que estos usuarios tendrán y nivel de Hola de administradores de acceso tendrá sobre Hola recursos que administran. La solución de identidad híbrida debe ser capaz de tooprovide acceso granular tooresources, delegación y el control de acceso base del rol. Asegúrese de que Hola siguiente pregunta se responden en relación con el control de acceso:

* ¿La compañía tiene más de un usuario con privilegios elevados toomanage su sistema de identidad?
  * ¿Si Sí, cada usuario necesita Hola mismo nivel de acceso?
* ¿Sería necesario toodelegate acceso toousers toomanage específico recursos de la empresa?
  * En caso afirmativo, ¿con qué frecuencia sucede esto?
* ¿La compañía necesita capacidades de control de acceso de toointegrate entre local y la nube recursos?
* ¿La compañía necesita toolimit acceso tooresources según las condiciones de toosome?
* ¿La compañía tiene cualquier aplicación que necesita recursos de toosome de acceso de control personalizado?
  * ¿En caso afirmativo, dónde se ubican las aplicaciones (local o en la nube de hello)?
  * ¿En caso afirmativo, donde están los recursos de destino encuentra (local o en la nube de hello)?

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Definir la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Hola opciones disponibles y las ventajas y desventajas de cada opción.  Las respuestas que obtenga  partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Determinación de los requisitos de respuesta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

