---
title: aaaProtect datos personales con controles de identidad y acceso de Azure | Documentos de Microsoft
description: Mediante el uso de Azure toohelp de controles de identidad y acceso a proteger sus datos personales
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory y Multi-Factor Authentication: protección de datos personales con controles de identidad y acceso

Este artículo proporciona información y procedimientos que puede usar datos personales tooprotect con los servicios y características de seguridad de autenticación de Azure Active Directory y varios factores.

## <a name="scenario"></a>Escenario

Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas. toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido 

la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola. Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global. También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones. línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.

Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes de la compañía de Hola ubicados en todo Hola a todos tienen acceso a recursos de empresa de toosome.

## <a name="problem-statement"></a>Declaración del problema

empresa Hola debe proteger la privacidad de Hola de datos personales de los clientes y empleados frente a atacantes buscando toouse en riesgo identidades toogain acceso. También deben asegurarse de que toopersonal de acceso a datos por los usuarios legítimos se restringe a solo aquellos que lo necesiten toodo sus trabajos.

## <a name="company-goal"></a>Objetivo de la empresa

objetivo de la compañía de Hello es tooensure que tienen acceso a datos toopersonal esté estrictamente controlado. Es fundamental que las identidades de los usuarios con acceso a los datos toopersonal protegerse con una autenticación segura. Una directiva de [privilegios mínimos] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) se debe aplicar para que los usuarios legítimos tengan único nivel de Hola de acceso que necesitan y nada más.

## <a name="solutions"></a>Soluciones

Microsoft Azure proporciona herramientas de administración de identidades y accesos toohelp control de las empresas que tenga acceso tooresources que contienen datos personales.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) administra las identidades y controla el acceso tooAzure así como otros locales y otros recursos de nube, datos y aplicaciones. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ayuda a número de administradores de Azure toominimize Hola de personas que tienen acceso toocertain información como datos personales. Les permite toodiscover, restrinja y supervise las identidades con privilegios y sus acceso tooresources y tooassign temporal, Just (JIT) derechos administrativos tooeligible usuarios. Asimismo, proporciona información sobre quién tiene privilegios administrativos de AAD.

las actividades de Hello implicadas el uso de AAD PIM incluyen:

- Habilitación de Privileged Identity Management para el directorio

- Usar importante información toosee del panel de administración de Privileged Identity Management de un vistazo

- Administración de identidades de hello con privilegios (administradores) agregando o quitando el rol de administradores permanentes ni aptos tooeach

- Configuración de activación de rol Hola

- Activación de roles

- Revisión de la actividad de un rol

#### <a name="how-do-i-enable-aad-pim"></a>¿Cómo se puede habilitar AAD PIM?

toostart usar PIM para su directorio, Hola siguientes:

1. Inicie sesión en toohello portal de Azure como administrador global de su directorio.

2. Si su organización tiene más de un directorio, seleccione el nombre de usuario en hello superior derecha del programa Hola a portal de Azure. Seleccione el directorio de Hola donde use AD Privileged Identity Management de Azure.

3. Seleccione **más servicios** y usar hello **filtro** toosearch de cuadro de texto para Azure AD Privileged Identity Management.

4. Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**. Hola aplicación Privileged Identity Management se abre.

Una vez que se ha configurado AD Privileged Identity Management de Azure, consulte hoja de navegación de hello cada vez que abra la aplicación hello.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Para obtener más información e instrucciones sobre cómo empezar a trabajar con AAD PIM, consulte [Comenzar a usar Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Control de acceso basado en rol de Azure

[Role-Based Access Control de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ayuda a administradores de Azure a administrar acceso a los recursos tooAzure habilitando Hola concesión de acceso basado en rol asignado del usuario de Hola. Puede separar los derechos dentro de un equipo y solo Hola cantidad de acceso toousers, grupos y aplicaciones que necesitan tooperform sus trabajos de concesiones.

Se puede conceder acceso basado en roles toousers mediante Hola portal de Azure, Azure herramientas de línea de comandos o las API de administración de Azure.

Para obtener más información acerca de conceptos básicos de RBAC de Azure, consulte [empezar a trabajar con Control de acceso basado en roles en hello Portal de Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>¿Cómo se puede administrar RBAC de Azure con PowerShell?

Puede usar cmdlets de PowerShell toomanage RBAC de Azure, incluidos Hola después de las tareas de administración:

- Lista de roles

- Consulta de quién ha accedido

- Conceder acceso

- Quitar acceso

- Crear un rol personalizado

- Acciones Get para un proveedor de recursos

- Modificación de un rol personalizado

- Eliminación de un rol personalizado

- Lista de roles personalizados

Para obtener instrucciones sobre cómo toomanage RBAC de Azure con PowerShell, vea [administrar Role-based Access con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[La autenticación multifactor Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) es una solución de comprobación de dos pasos que le ayuda a proteger acceso toodata y las aplicaciones, al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).

toodeploy MFA en hello nube de Azure, necesita toofirst habilitarlo y, a continuación, activar la verificación en dos pasos para los usuarios.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>¿Cómo habilito toouse Azure MFA?

Si los usuarios tienen licencias que incluyen la autenticación multifactor de Azure, no hay nada que necesite toodo tooturn en Azure MFA. De lo contrario, deberá toocreate un proveedor de autenticación multifactor en su directorio. toodo, siga estos pasos:

1. Seleccione **Active Directory** en hello Azure portal clásico (iniciado sesión como administrador).

2. Seleccione **Proveedores de Multi-Factor Authentication.**

3. Seleccione **Nuevo** y, a continuación, en **App Services,** seleccione **Proveedor de Multi-Factor Authentication.**

4. Seleccione **Creación rápida.**

5. Rellene el campo de nombre de Hola y seleccione un modelo de uso (por autenticación o por usuario habilitado).

6. Designar un directorio con qué hello está asociado el proveedor de MFA.

7. Haga clic en hello **crear** botón.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Para obtener más instrucciones sobre cómo toomanage el proveedor de autenticación multifactor, consulte [introducción con un proveedor de autenticación multifactor de Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>¿Cómo se puede activar la verificación en dos pasos para los usuarios?

Puede exigir la verificación en dos pasos para todos los inicios de sesión, o puede crear verificacion de toorequire de directivas de acceso condicional sólo cuando se dan condiciones específicas.

Habilitar MFA de Azure mediante el cambio de estado de usuario es el enfoque tradicional de Hola para exigir la verificación en dos pasos. Todos los usuarios de Hola que habilitar tendrán Hola verificación en dos pasos de mismo requisito tooperform cada vez que inicien sesión. La habilitación de un usuario invalida las directivas de acceso condicional que pudieran afectar a dicho usuario.

Habilitar Azure MFA con una directiva de acceso condicional es un enfoque más flexible para exigir la verificación en dos pasos. Puede crear directivas de acceso condicional que se aplican toogroups, así como los usuarios individuales. Los grupos de alto riesgo pueden recibir más restricciones que los grupos de bajo riesgo o bien la verificación en dos pasos puede ser necesaria solo para aplicaciones de alto riesgo en la nube y omitida para las de bajo riesgo. Sin embargo, el acceso condicional es una característica de pago de Azure Active Directory.

Hola tooenable MFA cambiando el estado de usuario siguientes:

1. Inicie sesión en toohello portal de Azure como administrador.
2. Vaya demasiado**Azure Active Directory \> usuarios y grupos \> todos los usuarios**.
3. Seleccione **Multi-Factor Authentication**.
4. Buscar usuario de Hola que quiere tooenable de MFA de Azure. Puede que necesite toochange Hola vista en la parte superior de Hola.
5. Compruebe Hola cuadro siguiente toohello del nombre de usuario.
6. En hello derecha, bajo pasos rápidos, elija **habilitar**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Confirme la selección en la ventana emergente de Hola que se abre.  Los usuarios para los que se ha habilitado MFA le preguntará hello tooregister próxima vez que inicie sesión.

tooenable MFA de Azure con una directiva de acceso condicional, Hola siguientes:

1. Inicie sesión en toohello portal de Azure como administrador.

2. Vaya demasiado**Azure Active Directory \> acceso condicional**.

3. Seleccione **Nueva directiva**.

4. En **Asignaciones**, seleccione **Usuarios y grupos**. Hola de uso **Include** y **excluir** pestañas toospecify qué usuarios y grupos serán administrada por directiva Hola.

5. En **Asignaciones**, seleccione **Aplicaciones en la nube.** Elija demasiado**incluyen todas las aplicaciones de nube**.
6.  En **Controles de acceso**, seleccione **Conceder**. Seleccione **Requerir autenticación multifactor**.
7.  Activar **habilitar Directiva de** demasiado**en** y, a continuación, seleccione **guardar**.

Para obtener información sobre cómo tooset de configuración de MFA de Azure de tooconfigure las alertas de fraude, se crea una omisión por única vez, usar mensajes de voz personalizados, configurar el almacenamiento en caché, especificar direcciones IP de confianza, crear contraseñas de aplicación, habilitar la autenticación Multifactor para dispositivos que los usuarios de confianza y seleccione teniendo en cuenta métodos de comprobación, vea [configurar configuración de Azure Multi-factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Pasos siguientes

- [Protección del acceso con privilegios en Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Preguntas más frecuentes relacionadas con Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Solución de problemas del control de acceso basado en rol](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
