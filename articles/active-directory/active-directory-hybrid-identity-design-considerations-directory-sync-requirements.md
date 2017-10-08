---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de sincronización de directorio | Documentos de Microsoft"
description: "Identificar qué requisitos son necesarios para la sincronización de todos los usuarios de hello entre on = local y en la nube para enterprise Hola."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Determinación de los requisitos de sincronización de directorios
Sincronización consiste en proporcionar a los usuarios una identidad en la nube de hello en función de su identidad local. Si no utilizará la cuenta sincronizada para la autenticación o autenticación federada, los usuarios de hello aún necesitarán toohave una identidad en la nube de Hola.  Esta identidad necesita toobe mantiene y actualiza periódicamente.  Hola actualizaciones pueden adoptar numerosas formas, de los cambios de toopassword de cambios de título.  

Inicio mediante la evaluación de las organizaciones de hello local de los requisitos de usuario y la solución de identidad. Esta evaluación es requisitos técnicos de hello toodefine importante acerca de cómo se se crean y mantienen en la nube de Hola identidades de usuario.  Para la mayoría de las organizaciones, Active Directory local y directorio local de Hola que los usuarios se sincronizarán desde, sin embargo en algunos casos esto no será el caso de hello.  

Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Tiene un bosque de AD único, múltiple o no tiene ninguno?
  
  * ¿Con cuántos directorios de Azure AD va a sincronizar?
    
    1. ¿Usará filtrado?
    2. ¿Tiene varios servidores de Azure AD Connect planeados?
* ¿Dispone actualmente de  una herramienta de sincronización local?
  
  * En caso afirmativo, ¿tienen sus usuarios una directorio virtual o integración de identidades?
* ¿Tiene cualquier otro directorio local que desea que toosynchronize (p. ej. directorio LDAP, base de datos de recursos humanos, etcetera)?
  * ¿Vas toobe hacer cualquier GALSync?
  * ¿Cuál es el estado actual de Hola de UPN en su organización? 
  * ¿Tiene un directorio diferente en el que se autentican los usuarios?
  * ¿Usa su organización Microsoft Exchange?
    * ¿Tienen previsto tener una implementación híbrida de Exchange?

Ahora que tiene una idea sobre los requisitos de sincronización, debe toodetermine qué herramienta es una toomeet correcta de hello estos requisitos.  Microsoft proporciona varias herramientas tooaccomplish directorio la integración y sincronización.  Vea hello [tabla de comparación de herramientas de integración de directorio de identidad híbrida](active-directory-hybrid-identity-design-considerations-tools-comparison.md) para obtener más información. 

Ahora que tiene los requisitos de sincronización y la herramienta Hola que realizará para su empresa, necesita que las aplicaciones de hello tooevaluate que utilizan estos servicios de directorio. Esta evaluación es importante toodefine Hola requisitos técnicos toointegrate estos nube toohello de aplicaciones. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Estas aplicaciones será toohello movida en la nube y usar Hola directory?
* ¿Hay atributos especiales que necesitan en la nube toohello toobe sincronizado por lo que pueden usar estas aplicaciones correctamente?
* ¿Será necesario estas aplicaciones toobe reescribirá tootake ventaja de autenticación en la nube?
* ¿Estas aplicaciones seguirán toolive local mientras los usuarios tener acceso a ellos mediante la identidad de nube de hello?

También debe toodetermine Hola seguridad requisitos y restricciones de sincronización de directorios. Esta evaluación es importante tooget una lista de los requisitos de Hola que se necesitará en orden toocreate y mantener las identidades del usuario en la nube de Hola. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Dónde se ubicarán los servidor de sincronización de hello?
* ¿Estará unido a un dominio?
* ¿Se encuentra el servidor de hello en una red restringida detrás de un firewall, como una red Perimetral?
  * ¿Será sincronización de toosupport de puertos de tooopen capaz de hello necesario firewall?
* ¿Tiene un plan de recuperación ante desastres para el servidor de sincronización de hello?
* ¿Tiene una cuenta con permisos correctos de Hola para todos los bosques que desee toosynch con?
  * Si su empresa no conoce la respuesta de Hola para esta pregunta, revise la sección de Hola "Permisos para la sincronización de contraseña" en el artículo hello [Hola instalar servicio de sincronización de Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) y determine si ya tiene un cuenta con estos permisos o si debe toocreate uno.
* ¿Si tiene sincronización de bosque múltiple es tooget pueda tooeach bosque de hello sincronización server?

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Determinar los requisitos de respuesta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) irá sobre las opciones de hello disponibles. Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Determinación de los requisitos de autenticación multifactor](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

