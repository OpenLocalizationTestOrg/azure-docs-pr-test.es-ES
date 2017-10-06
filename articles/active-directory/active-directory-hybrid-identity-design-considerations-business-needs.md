---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de identidad | Documentos de Microsoft"
description: "Identificar necesidades empresariales de la compañía de Hola que ocasionarán toodefine requisitos de hello para el diseño de identidad híbrida de Hola."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Determinación de los requisitos de identidad para la solución de identidad híbrida
Hola primer paso para diseñar una solución de identidad híbrida es toodetermine requisitos de Hola para los valore de Hola que se puede aprovechar esta solución.  Identidad híbrida comienza como una función de soporte (es compatible con todas las demás soluciones de nube al proporcionar autenticación) y continúa tooprovide nuevas e interesantes capacidades que desbloquear nuevas cargas de trabajo para los usuarios.  Estas cargas de trabajo o los servicios que desea tooadopt para los usuarios determinará los requisitos de hello para el diseño de identidad híbrida de Hola.  Estos servicios y las cargas de trabajo necesitan identidad híbrida de tooleverage tanto de forma local y en la nube de Hola.  

Necesita toogo estos aspectos clave de hello business toounderstand ¿qué es un requisito ahora y planes de la empresa de Hola para hello futuras. Si no tiene visibilidad Hola de estrategia a largo plazo de hello para el diseño de identidad híbrida, lo más probable es que la solución no sea escalable como Hola empresa necesite crecer y cambiar.   T el diagrama siguiente muestra un ejemplo de un híbrido identidad hello y arquitectura de las cargas de trabajo que se está Desbloqueando para los usuarios. Esto es simplemente un ejemplo de todas las posibilidades nuevo de Hola que se pueden desbloquear y ofrece una estrategia de identidad híbrida sólido. 

Algunos componentes que forman parte de la arquitectura de identidad híbrida de Hola![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Determinación de las necesidades empresariales
Cada empresa tendrá requisitos diferentes, aunque estas empresas forman parte del programa Hola mismo sector, requisitos de hello empresariales reales pueden variar. Puede seguir aprovechando las prácticas recomendadas del sector de hello, pero en última instancia es necesidades empresariales de la compañía de Hola que ocasionarán toodefine requisitos de hello para el diseño de identidad híbrida de Hola. 

Asegúrese de que el siguiente de hello tooanswer preguntas tooidentify su empresa debe:

* ¿Su empresa busca toocut costos operativos de TI?
* ¿Su empresa busca los recursos de nube toosecure (aplicaciones de SaaS, infraestructura)?
* ¿Compañía buscando toomodernize el departamento de TI?
  * ¿Son los usuarios más exigentes y móviles TI toocreate excepciones en el tipo de recursos diferentes de tráfico tooaccess DMZ tooallow diferente?
  * ¿La compañía tiene aplicaciones heredadas que sea necesario toobe publicado toothese moderna usuarios pero que no sean toorewrite fácil?
  * ¿Necesita tooaccomplish todas estas tareas y de su empresa colocarlo bajo control en hello mismo tiempo?
* ¿Es su empresa busca las identidades de los usuarios de toosecure y reducir los riesgos aunando las nuevas herramientas que aprovechen la experiencia de Hola de Azure seguridad experiencia local de Microsoft?
* ¿Es su empresa intentar tooget rid de hello temida "externas" cuentas de forma local y moverlos toohello en la nube que ya no son una amenaza inactiva dentro de su entorno local?

## <a name="analyze-on-premises-identity-infrastructure"></a>Análisis de la infraestructura de identidad local
Ahora que tiene una idea con respecto a los requisitos empresariales de su empresa, debe tooevaluate su infraestructura de identidad local. Esta evaluación es importante para definir Hola requisitos técnicos toointegrate su sistema de la administración de identidad con nube toohello del solución de actual identidad. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Qué soluciones de autenticación y autorización usa su empresa localmente? 
* ¿Su empresa tiene actualmente servicios locales de sincronización?
* ¿Su empresa usa proveedores de identidades (IdP) de terceros?

También necesita toobe consciente de los servicios de nube de Hola que su compañía puede tener. Realizar una integración actual de evaluación toounderstand Hola con SaaS, ¿IaaS o PaaS modelos en el entorno es muy importante. Asegúrese de que hello tooanswer después preguntas durante esta evaluación:

* ¿Tiene la compañía alguna integración con un proveedor de servicios en la nube?
* En caso afirmativo, ¿qué servicios se utilizan?
* ¿Está esta integración actualmente en producción o se trata de una prueba piloto?

> [!NOTE]
> Si no tiene una asignación precisa de todas las aplicaciones y servicios en la nube, puede usar la herramienta de Cloud App Discovery de Hola. Esta herramienta puede proporcionar al departamento de TI visibilidad en la estructura empresarial de la organización y las aplicaciones de nube del consumidor. Que resulta más fácil que nunca toodiscover instantáneas TI de su organización, incluidos los detalles sobre los patrones de uso y los usuarios que acceden a aplicaciones en la nube. vea tooget iniciado [Cloud app discovery de](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Evaluación de los requisitos de integración de identidades
A continuación, hay requisitos de integración de identidad de tooevaluate Hola. Esta evaluación es requisitos técnicos de hello toodefine importante para cómo se autenticarán los usuarios, el aspecto de presencia de la organización de hello en la nube de hello, la organización de hello permitirá autorización y la experiencia del usuario hello es continuo toobe. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Su organización va a usar la federación, la autenticación estándar o ambas?
* ¿Es la federación un requisito?  Debido a los siguientes hello:
  * SSO basado en Kerberos
  * Su empresa tiene una aplicación local (ya sea generada internamente o de terceros) que usa SAML o capacidades de federación similares.
  * MFA mediante tarjetas inteligentes. RSA SecurID, etc.
  * Reglas de acceso de cliente que abordan preguntas Hola siguientes:
    1. ¿Puedo bloquear todos los acceso externo tooOffice 365 basado en dirección IP de Hola de cliente hello?
    2. ¿Puedo bloquear todos los acceso externo tooOffice 365, excepto Exchange ActiveSync?
    3. ¿Puedo bloquear todos los acceso externo tooOffice 365, excepto en aplicaciones basadas en explorador (OWA, SPO)
    4. ¿Puedo bloquear todos los acceso externo tooOffice 365 para los miembros de grupos específicos de AD
* Consideraciones de seguridad o auditoría
* Inversión ya existente en la autenticación federada
* ¿El nombre que utilizará nuestra organización para el dominio en la nube de hello?
* ¿La organización hello tiene un dominio personalizado?
  1. ¿Es dicho dominio público y fácilmente comprobable a través de DNS?
  2. ¿Si no lo es, a continuación, tiene un dominio público que pueden ser utilizado tooregister un UPN alternativo en Active Directory?
* ¿Son identificadores de usuario de hello coherente para la representación en la nube? 
* ¿Organización hello tiene aplicaciones que requieren integración con los servicios en la nube?
* ¿Organización de hello tiene varios dominios y todos ellos, se utilizará la autenticación estándar o federada?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Evaluación de las aplicaciones que se ejecutan en el entorno
Ahora que tiene una idea con respecto a su local y la nube de infraestructura, necesitas que las aplicaciones de Hola de tooevaluate que se ejecutan en estos entornos. Esta evaluación es importante toodefine Hola requisitos técnicos toointegrate estos sistema de administración de identidades de las aplicaciones toohello en la nube. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Dónde residirán las aplicaciones?
* ¿Los usuarios van a acceder a aplicaciones locales?  ¿En la nube de hello? ¿O en ambos entornos?
* ¿Son existen planes de cargas de trabajo de aplicación existente de tootake hello y moverlos toohello en la nube?
* ¿Existen planes toodevelop nuevas aplicaciones que se encuentran de forma local o en hello en la nube que usarán la autenticación de nube?

## <a name="evaluate-user-requirements"></a>Evaluación de los requisitos del usuario
También tiene requisitos de usuario de tooevaluate Hola. Esta evaluación es pasos de hello toodefine importante que será necesaria para de incorporación y ayudan a los usuarios que hagan el cambio en la nube toohello. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Los usuarios van a acceder a las aplicaciones de forma local?
* ¿Los usuarios tengan acceso a las aplicaciones de nube de hello?
* ¿Cómo los usuarios normalmente tootheir de inicio de sesión en entorno local?
* ¿Cómo se a los usuarios iniciar sesión toohello en la nube?

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Determinar los requisitos de respuesta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) irá Hola opciones disponibles y las ventajas e inconvenientes de cada opción.  Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Determinación de los requisitos de sincronización de directorios](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

