---
title: acceso condicional de Active Directory aaaAzure | Documentos de Microsoft
description: "Usar el control de acceso condicional en Azure Active Directory toocheck para condiciones específicas al autenticar para tooapplications de acceso."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Acceso condicional en Azure Active Directory

En un mundo móvil en primer lugar, basado en la nube, Azure Active Directory permite toodevices de inicio de sesión único, las aplicaciones y servicios desde cualquier lugar. Con la proliferación de Hola de dispositivos (como BYOD), trabajan sin redes corporativas y aplicaciones de SaaS de terceros 3ª, profesionales de TI se enfrentan dos objetivos opuestos:

- Capacitar a toobe de los usuarios finales de hello productivo, donde y cuando
- Proteger los activos corporativos hello en cualquier momento

productividad tooimprove, Azure Active Directory proporciona a los usuarios con una amplia gama de opciones tooaccess los activos corporativos. Administración de acceso de la aplicación, con Azure Active Directory permite que solo tooensure *Hola personas* puede tener acceso a las aplicaciones. ¿Qué ocurre si desea toohave más control sobre cómo personas Hola obtiene acceso a los recursos en determinadas condiciones? ¿Qué ocurre si incluso tener las condiciones bajo el cual desea tooblock acceso toocertain aplicaciones incluso para hello *haga personas*? Por ejemplo, podría ser Aceptar automáticamente si personas Hola se obtiene acceso a determinadas aplicaciones desde una red de confianza; Sin embargo, no conviene ellos tooaccess estas aplicaciones desde una red que no confías. También puede abordar estas cuestiones mediante el acceso condicional.

Acceso condicional es una capacidad de Azure Active Directory que permite que los controles de tooenforce en tooapps de acceso de hello en su entorno basándose en condiciones específicas. Con los controles, o bien puede asociar acceso de toohello requisitos adicionales o puede bloquearla. implementación de Hola de acceso condicional se basa en las directivas. Un enfoque basado en directiva simplifica la experiencia de configuración porque sigue forma Hola que piensa sobre los requisitos de acceso.  

Normalmente, se definen los requisitos de acceso mediante las instrucciones que se basan en hello siguiente patrón:

![Control](./media/active-directory-conditional-access-azure-portal/10.png)

Cuando se reemplaza dos apariciones de Hola de "*esto*" con la información del mundo real, tiene un ejemplo de una instrucción de directiva que probablemente se parezca tooyou familiar:

*Cuando contratistas están tratando de tooaccess nuestras aplicaciones de nube desde las redes que no son de confianza, a continuación, bloquear el acceso.*

instrucción de directiva de Hello anterior destaca power Hola de acceso condicional. Si bien puede permitir contratistas toobasically tener acceso a las aplicaciones de nube (**que**), con el acceso condicional, también puede definir las condiciones bajo qué Hola sea posible el acceso (**cómo**).

En el contexto de Hola de acceso condicional de Azure Active Directory,

- "**Cuando esto sucede**" se denomina **declaración de condición**
- "**Entonces haga esto**" se denomina **controles**.

![Control](./media/active-directory-conditional-access-azure-portal/11.png)

combinación de Hola de una instrucción de condición con los controles representa una directiva de acceso condicional.

![Control](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Controles

En una directiva de acceso condicional, los controles definen qué es lo que debe suceder cuando se ha satisfecho una declaración de condición.  
Con controles, puede bloquear el acceso o permitir el acceso con requisitos adicionales.
Cuando se configura una directiva que permite el acceso, deberá tooselect al menos uno de los requisitos.   

### <a name="grant-controls"></a>Controles de concesión
implementación actual de Hola de Azure Active Directory permite hello tooconfigure según los requisitos de control de concesión:

![Control](./media/active-directory-conditional-access-azure-portal/05.png)

- **Multi-factor Authentication**: pude exigir autenticación fuerte mediante la autenticación multifactor. Como proveedor, puede usar la autenticación multifactor de Azure o un proveedor de autenticación multifactor de terceros, en combinación con Active Directory Federation Services (AD FS). Utilizar la autenticación multifactor le ayuda a proteger los recursos de que se obtiene acceso por un usuario no autorizado que podría haber obtenido acceso toohello credenciales de un usuario válido.

- **Dispositivo compatible con** -puede establecer directivas de acceso condicional en el nivel de dispositivo de Hola. Es posible configurar la directiva tooonly Habilitar equipos que son compatibles o dispositivos móviles que están inscritos en una tooaccess de administración de dispositivos móviles de recursos de su organización. Por ejemplo, puede usar Intune toocheck el cumplimiento de dispositivos y, a continuación, notificarlo tooAzure AD para la aplicación cuando el usuario de hello intenta tooaccess una aplicación. Para obtener instrucciones detalladas sobre cómo toouse Intune tooprotect aplicaciones y datos, vea [proteger aplicaciones y datos con Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). También puede usar la protección de datos de tooenforce de Intune para dispositivos perdidos o robados. Para obtener más información, consulte [Ayudar a proteger los datos con el borrado selectivo o completo mediante Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Dispositivo unido a un dominio** : puede requerir dispositivo Hola usaron tooconnect tooAzure Active Directory toobe Unidos al dominio tooyour Active Directory (AD) local. Esta directiva aplica tooWindows escritorios, equipos portátiles y tabletas de empresa. 

Si tiene varios controles seleccionados, también puede configurar si todos ellos son necesarios al procesarse su directiva.

![Control](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Controles de sesión
Los controles de sesión permiten limitar la experiencia desde una aplicación en la nube. controles de la sesión de Hola se aplican mediante aplicaciones de nube y se basan en información adicional proporcionada por la aplicación de Azure AD toohello acerca de la sesión de Hola.

![Control](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Usar restricciones que exige la aplicación
Puede usar este control toorequire Azure AD toopass Hola información toohello en la nube del dispositivo. Esto ayuda a aplicación de nube de hello saber si el usuario de hello procede de un dispositivo compatible o Unidos a un dominio. Este control está actualmente solo se admiten con SharePoint como aplicación de hello en la nube. SharePoint utiliza Hola dispositivo información tooprovide que los usuarios una experiencia completa o limitada, según el estado del dispositivo de Hola.
toolearn más información acerca de cómo toorequire limitado el acceso con SharePoint, vaya [aquí](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Declaración de condición

sección anterior de Hola presenta toosupported opciones tooblock o restringir el acceso a los recursos tooyour en forma de controles. En una directiva de acceso condicional, definir criterios de Hola que deben toobe cumplen para su toobe controles aplicado en forma de una instrucción de condición.  

Puede incluir Hola siguiendo las asignaciones en la instrucción de condición:

![Control](./media/active-directory-conditional-access-azure-portal/07.png)


- **Que** -en muchos casos, desea que los controles toobe aplica tooa conjunto de usuarios específico. En una instrucción de condición, puede definir este conjunto mediante la selección de usuarios de Hola y la directiva se aplica a los grupos. Si es necesario, también puede eximir un conjunto de usuarios de su directiva si los excluye explícitamente.  
Al seleccionar los usuarios y grupos, definir ámbito Hola de usuarios que se aplica la directiva.    

    ![Control](./media/active-directory-conditional-access-azure-portal/08.png)



- **Qué**: normalmente, hay determinadas aplicaciones que se ejecutan en el entorno que requieren más atención que otras, desde la perspectiva de la protección. Esto afecta a, por ejemplo, las aplicaciones que tienen acceso a los datos toosensitive.
Al seleccionar las aplicaciones de nube, definir ámbito de saludo de la directiva se aplica a las aplicaciones de nube. Si es necesario, también puede excluir explícitamente un conjunto de aplicaciones de su directiva.

    ![Control](./media/active-directory-conditional-access-azure-portal/09.png)


- **¿Cómo** : mientras se lleva a cabo acceso tooyour aplicaciones en condiciones que puede controlar, podría existen necesidad de imponer controles adicionales en cómo las aplicaciones de nube no son obtenerse acceso a los usuarios. Sin embargo, cosas podrían ser diferentes si se realiza acceso tooyour las aplicaciones de nube, por ejemplo, en redes que no son de confianza o dispositivos que no son compatibles. En una instrucción de condición, puede definir determinadas condiciones de acceso que tienen requisitos adicionales de cómo se realiza el acceso tooyour aplicaciones.

    ![Condiciones](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Condiciones

En la implementación actual de Hola de Azure Active Directory, puede definir condiciones Hola siguientes áreas:

- Riesgo de inicio de sesión
- Plataformas de dispositivo
- Ubicaciones
- Aplicaciones cliente

![Condiciones](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Riesgo de inicio de sesión

Un riesgo de inicio de sesión es un objeto que se usa por la probabilidad de hello tootrack de Azure Active Directory que no ha realizado un intento de inicio de sesión propietario legítimo de Hola de una cuenta de usuario. En este objeto, probabilidad de hello (alto, medio o bajo) se almacena en un formato de un atributo denominado [nivel de riesgo de inicio de sesión](active-directory-reporting-risk-events.md#risk-level). El objeto se genera durante un inicio de sesión de un usuario si Azure Active Directory ha detectado riesgos de inicio de sesión. Para más información, consulte la sección sobre los [inicios de sesión peligrosos](active-directory-identityprotection.md#risky-sign-ins).  
Puede utilizar el nivel de riesgo de inicio de sesión de hello calculado como condición en una directiva de acceso condicional. 

![Condiciones](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Plataformas de dispositivo

plataforma de dispositivo de Hola se caracteriza por sistema operativo de Hola que se ejecuta en el dispositivo:

- Android
- iOS
- Windows Phone
- Windows
- macOS (versión preliminar). 

![Condiciones](./media/active-directory-conditional-access-azure-portal/02.png)

Puede definir las plataformas de dispositivos de Hola que se incluyen, así como las plataformas de dispositivos que están exentos de una directiva.  
plataformas de dispositivos de toouse en la directiva de hello, primer Hola cambio configurar alterna demasiado**Sí**y, a continuación, seleccione todos o directiva de Hola de plataformas de dispositivos individuales se aplica a. Si selecciona plataformas de dispositivos individuales, directiva de hello tiene solo un impacto en estas plataformas. En este caso, plataformas de tooother admitida inicios de sesión no se ven afectadas por la directiva de Hola.


### <a name="locations"></a>Ubicaciones

Hello ubicación se identifica por dirección IP de Hola de cliente hello usaron tooconnect tooAzure Active Directory. Esta condición requiere toobe familiarizado con **denominada ubicaciones** y **MFA IP de confianza**.  

**Denominada ubicaciones** es una característica de Azure Active Directory que permite los intervalos de direcciones IP toolabel de confianza en su organización. En su entorno, puede usar ubicaciones con nombre en el contexto de hello de la detección de Hola de [el riesgo de eventos](active-directory-reporting-risk-events.md) , así como acceso condicional. Para más información sobre cómo configurar ubicaciones con nombre en Azure Active Directory, vea [Ubicaciones con nombre en Azure Active Directory](active-directory-named-locations.md).

número de Hola de ubicaciones que puede configurar está restringido por tamaño Hola del objeto relacionado de hello en Azure AD. Puede configurar:
 
 - Una ubicación con nombre con los intervalos de IP too500
 - Un máximo de 60 ubicaciones con nombre (vista previa) con un intervalo IP asignada tooeach de ellos 


**IP de confianza de MFA** es una característica de la autenticación multifactor que permite toodefine confianza intervalos de direcciones IP que representa la intranet local de su organización. Cuando se configura un condiciones de ubicación, IP de confianza le permite toodistinguish entre las conexiones realizadas desde la red de su organización y todas las demás ubicaciones. Para más información, vea [IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Puede incluir todas las ubicaciones o todas las direcciones IP de confianza y puede excluir todas las direcciones IP de confianza.

![Condiciones](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Aplicación cliente

aplicación de cliente de Hello puede ser en una aplicación Hola nivel genérico (explorador web, aplicaciones móviles, cliente de escritorio) ha utilizado tooconnect tooAzure Active Directory o puede seleccionar específicamente Exchange Active Sync.  
Autenticación heredado hace referencia tooclients con la autenticación básica como clientes de Office más antiguos que no usan la autenticación moderna. El acceso condicional no se admite actualmente con la autenticación heredada.

![Condiciones](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Escenarios comunes

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exigir autenticación multifactor para las aplicaciones

Muchos entornos tienen las aplicaciones que requieren un mayor nivel de protección que Hola otros usuarios.
Esto sucede, por ejemplo, hello para aplicaciones que tienen acceso a los datos toosensitive.
Si desea tooadd otro nivel de protección toothese aplicaciones, puede configurar una directiva de acceso condicional que requiere la autenticación multifactor cuando los usuarios tienen acceso a estas aplicaciones.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exigir autenticación multifactor para el acceso desde redes que no son de confianza

Este escenario es similar toohello anterior porque agrega un requisito para la autenticación multifactor.
Sin embargo, Hola principal diferencia es condición Hola para este requisito.  
Mientras se estaba foco Hola del escenario anterior hello en aplicaciones con acceso a los datos toosensitve, Hola de este escenario es ubicaciones de confianza.  
En otras palabras, podría tener un requisito de autenticación multifactor si un usuario accede a una aplicación desde una red que no es de confianza.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Solo los dispositivos de confianza pueden acceder a servicios de Office 365

Si usa Intune en su entorno, inmediatamente puede comenzar a usar la interfaz de directiva de acceso condicional de Hola Hola consola de Azure.

Muchos clientes de Intune usa tooensure de acceso condicional que solo los dispositivos de confianza pueden tener acceso a servicios de Office 365. Esto significa que los dispositivos móviles inscriben con Intune y cumplan los requisitos de directiva de cumplimiento de normas y que los equipos con Windows son tooan Unidos a un dominio de local. Una importante mejora es que no haya tooset Hola misma directiva para cada uno de los servicios de hello Office 365.  Cuando se crea una nueva directiva, configure hello en la nube aplicaciones tooinclude cada de las aplicaciones de Office 365 Hola que desee tooprotect con el acceso condicional.

## <a name="next-steps"></a>Pasos siguientes

Si desea tooknow tooconfigure una directiva de acceso condicional, vea [empezar a trabajar con el acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Si está listo tooconfigure directivas de acceso condicional para su entorno, vea hello [las prácticas recomendadas para el acceso condicional en Azure Active Directory](active-directory-conditional-access-best-practices.md). 
