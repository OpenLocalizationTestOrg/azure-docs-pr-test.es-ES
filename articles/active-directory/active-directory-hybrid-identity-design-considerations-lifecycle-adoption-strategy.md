---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar la estrategia de adopción de ciclo de vida de identidades híbridas | Documentos de Microsoft"
description: "Ayuda a definir las tareas de administración de identidad Hola híbrida según toohello opciones disponibles para cada fase del ciclo de vida."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Determinación de la estrategia de adopción de ciclo de vida de identidad híbrida
En esta tarea, definirá la estrategia de administración de identidades de Hola para sus híbrida identidad solución toomeet Hola requisitos empresariales que usted definió en [determinar las tareas de administración de identidad híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine Hola híbrida identidad las tareas de administración según toohello ciclo de vida de identidad to-end presentado anteriormente en este paso, tendrá opciones de hello tooconsider disponibles para cada fase del ciclo de vida.

## <a name="access-management-and-provisioning"></a>Aprovisionamiento y administración del acceso
Con una solución de administración de acceso de cuenta buena, su organización puede realizar un seguimiento con precisión quién tiene acceso toowhat información a través de la organización de Hola.

El control de acceso es una función crucial en un sistema centralizado de aprovisionamiento de único punto. Además de proteger la información confidencial, los controles de acceso exponen las cuentas existentes que tengan autorizaciones no aprobadas o que ya no sean necesarias. toocontrol cuentas obsoleta, Hola aprovisionamiento información del sistema vínculos cuenta junto con información autorizada sobre usuarios de hello propietarios de cuentas de Hola. Información de identidad de usuario autorizado normalmente se mantiene en las bases de datos de Hola y directorios de recursos humanos.

Las cuentas en las empresas de TI sofisticadas incluir cientos de parámetros que definen las entidades de Hola y estos detalles pueden controlarse mediante el sistema de suministro. Los usuarios nuevos pueden identificarse con datos de hello proporcionada por usted desde el origen de autoridad de Hola. capacidad de aprobación de solicitud de acceso de Hello inicia los procesos de Hola que aprobación (o rechazan) de recursos de aprovisionamiento para ellos.

| Fase de administración del ciclo de vida | Local | Nube | Híbrida |
| --- | --- | --- | --- |
| Aprovisionamiento y administración de cuentas |Mediante el uso de rol de servidor de servicios de dominio de Active Directory® (AD DS) de hello, puede crear una infraestructura escalable, segura y administrable para la administración de usuarios y recursos y proporcionan compatibilidad para aplicaciones habilitadas para directorio, como Microsoft® Exchange Server. <br><br> [Puede aprovisionar grupos en AD DS a través de un administrador de identidad.](https://technet.microsoft.com/library/ff686261.aspx) <br>[Puede aprovisionar usuarios en AD DS.](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Los administradores pueden usar recursos de tooshared de acceso de usuario de access control toomanage por motivos de seguridad. En Active Directory, se administra el control de acceso a nivel de objeto de Hola por establecer distintos niveles de acceso, o los permisos, tooobjects, como Control total, escritura, lectura o sin acceso. El control de acceso en Active Directory define cómo los distintos usuarios pueden usar objetos de Active Directory. De forma predeterminada, los permisos en objetos de Active Directory se establecen toohello de configuración más segura. |Tiene una cuenta para todos los usuarios que tendrán acceso a un servicio de nube de Microsoft toocreate. También puede cambiar las cuentas de usuario o eliminarlas cuando ya no sean necesarias. De forma predeterminada, los usuarios no tienen permisos de administrador, pero puede asignárselos si lo desea. Para obtener más información, consulte [Creación o edición de usuarios en Azure AD](active-directory-create-users.md). <br><br> Dentro de Azure Active Directory, una de las características principales de hello es Hola capacidad toomanage acceso tooresources. Estos recursos pueden formar parte del directorio de hello, como en caso de hello toomanage de objetos de permisos a través de roles en el directorio de Hola o recursos de directorio de toohello externo, como las aplicaciones de SaaS, servicios de Azure y los sitios de SharePoint o local recursos. <br><br> En hello solución de administración de acceso de center de Azure Active Directory es el grupo de seguridad de Hola. propietario del recurso de Hello (o el Administrador de hello del directorio de hello) puede asignar a un grupo tooprovide un determinados recursos de toohello derecho de acceso que poseen. los miembros de Hello del grupo de Hola se proporcionará acceso de Hola y el propietario del recurso de hello puede delegar la lista de miembros de Hola Hola toomanage derecho de una persona: por ejemplo, un administrador de departamento o un administrador del departamento de soporte técnico de toosomeone de grupo<br> <br> Administrar grupos de Hello en el tema de Azure AD proporciona más información acerca de cómo administrar el acceso a través de grupos. |Extender las identidades de Active Directory en la nube de Hola a través de la sincronización y la federación |

## <a name="role-based-access-control"></a>Control de acceso basado en rol
Control de acceso basado en roles (RBAC) usa roles y aprovisionamiento de directivas tooevaluate, probar y aplicar los procesos empresariales y las reglas para conceder acceso toousers. Claves administradores crear directivas de aprovisionamiento y asignar los usuarios tooroles y que definen conjuntos de tooresources de derechos para estos roles. RBAC extiende Hola identidad solución toouse basada en software procesos de administración de y reducir la interacción manual del usuario en proceso de aprovisionamiento de Hola.
RBAC de Azure AD permite la cantidad de hello empresa toorestrict Hola de las operaciones que un usuario individual puede realizar una vez que se tiene acceso tooAzure Portal de administración. Mediante RBAC toocontrol acceso toohello portal, los administradores de TI el acceso del delegado de entidad emisora de certificados mediante Hola después de la administración del acceso enfoques:

* **Asignación de roles basado en grupos**: puede asignar acceso tooAzure AD grupos que se pueden sincronizar desde su Active Directory local. Esto le permite tooleverage hello las inversiones existentes que su organización ha realizado en las herramientas y los procesos de administración de grupos. También puede utilizar la característica de administración de grupos delegados Hola de Azure AD Premium.
* **Aproveche integrada en roles de Azure**: puede utilizar los tres roles: tooensure propietario, Colaborador y lector, que los usuarios y grupos tienen permiso toodo sólo hello las tareas que necesitan toodo sus trabajos.
* **Acceso granular tooresources**: puede asignar toousers de roles y grupos para una suscripción determinada, grupo de recursos o un recurso de Azure individual como un sitio Web o una base de datos. De esta manera, puede asegurarse de que los usuarios tengan acceso a los recursos hello tooall que necesitan y no tooresources de acceso que no es necesario toomanage.

## <a name="provisioning-and-other-customization-options"></a>Aprovisionamiento y otras opciones de personalización
El equipo puede usar toodecide de planes y los requisitos de negocios cuánto soluciones de identidad toocustomize Hola. Por ejemplo, una gran empresa podría requerir un plan de implementación por fases para flujos de trabajo y adaptadores personalizados que se base en una escala de tiempo para aprovisionar de forma incremental aplicaciones que se usan ampliamente en diversas zonas del mundo. Puede proporcionar otro plan de personalización para dos o más toobe aplicaciones aprovisionado en toda la organización, y después de realizar pruebas correcta. Se puede personalizar la interacción de la aplicación de usuario y procedimientos para el aprovisionamiento de recursos pueden ser modificada tooaccommodate automatizada de aprovisionamiento.

Puede cancelar el aprovisionamiento de tooremove un servicio o componente. Por ejemplo, la cancelación del aprovisionamiento de una cuenta significa que la cuenta de hello se elimina de un recurso.

modelo híbrido de Hola de aprovisionamiento de recursos combina la solicitud y enfoques basada en roles, que son compatibles con Azure AD. Un subconjunto de los empleados o sistemas administrados, una empresa que sea mejor acceso tooautomate con la asignación basada en roles. Un negocio también podría controlar todas las demás solicitudes de acceso o excepciones por medio de un modelo basado en solicitudes. Puede que algunas empresas comiencen con la asignación manual y evolucionen hacia un modelo híbrido, con la intención de llegar a una implementación totalmente basada en roles en el futuro.

Otras compañías resultará muy poco práctico para negocios motivos tooachieve completa basada en roles aprovisionar y un enfoque híbrido de destino como un objetivo deseado. Todavía otras compañías podrían darse por satisfecho con aprovisionamiento solo basado en la solicitud y no desea tooinvest esfuerzo adicional toodefine y administrar directivas de aprovisionamiento automatizadas, basada en roles.

## <a name="license-management"></a>Administración de licencias
Administración de licencias basadas en grupos en Azure AD permite a los administradores asignar el grupo de seguridad de los usuarios tooa y Azure AD automáticamente asigna licencias de los miembros de hello tooall del grupo de Hola. Si un usuario posteriormente se agregan a o quitar del grupo de hello, una licencia se automáticamente asignada o se quitará según corresponda.

Puede usar los grupos que sincronice desde un AD local o que administre en Azure AD. Este emparejamiento con Azure AD premium sin intervención del Administrador de grupo de administración puede delegar fácilmente licencia asignación toohello adecuado toma de decisiones. Puede estar seguro de que los problemas como los conflictos de licencias y la falta de datos de ubicación se solucionarán automáticamente.

## <a name="self-regulating-user-administration"></a>Administración de usuarios autorregulada
Cuando su organización inicia tooprovision recursos a través de todas las organizaciones internas, implementar la capacidad de administración de usuarios autorregula Hola. Puede obtener ventajas de Hola y ventajas de aprovisionamiento de usuarios a través de límites de la organización. En este entorno, un cambio en el estado de un usuario se refleja automáticamente en los derechos de acceso en las diversas ubicaciones geográficas y a través de los límites de la organización. Puede reducir los costos de aprovisionamiento y simplificar los procesos de aprobación y acceso de Hola. implementación de Hello es consciente de posibilidades Hola de implementación del control de acceso basado en roles para la administración de acceso de extremo a extremo en su organización. Puede reducir los costos administrativos mediante procedimientos automatizados para regular el aprovisionamiento de usuarios. Puede mejorar la seguridad mediante la automatización de la aplicación de directivas de seguridad, así como optimizar y centralizar la administración del ciclo de vida de usuario y el aprovisionamiento de recursos para grandes grupos de usuarios.

> [!NOTE]
> Para obtener más información, consulte Configuración de Azure AD para la administración del acceso a la aplicación de autoservicio.
> 
> 

Los servicios de Azure AD basados en licencias (basados en derechos) funcionan mediante la activación de una suscripción en el inquilino del servicio/directorio de Azure AD. Una vez Hola suscripción está activa funcionalidades del servicio Hola administradas por los administradores del servicio de directorio/y utilizados por los usuarios con licencia. Consulte ¿Cómo funcionan las licencias de Azure AD? para obtener más información.
Integración con otros proveedores

Azure Active Directory proporciona el inicio de sesión único en y mejorado toothousands de seguridad de acceso de aplicación de las aplicaciones de SaaS y las aplicaciones web locales. Para obtener una lista detallada de la Galería de aplicaciones de Azure Active Directory para las aplicaciones SaaS compatibles, consulte la lista de compatibilidad de federación de Active Directory de Azure: proveedores de identidades de terceros que pueden ser utilizado tooimplement inicio de sesión único

## <a name="define-synchronization-management"></a>Definición de la administración de sincronización
La integración de directorios locales con Azure AD hace que los usuarios sean más productivos al proporcionar una identidad común para acceder tanto a los recursos en la nube como a los locales. Con esta integración, usuarios y organizaciones pueden sacar provecho de siguientes hello:

* Las organizaciones pueden proporcionar a los usuarios con una identidad híbrida común entre locales o servicios en la nube usando Windows Server Active Directory y, a continuación, conectando tooAzure Active Directory.
* Los administradores pueden proporcionar acceso condicional basado en el recurso de la aplicación, dispositivo e identidad de usuario, ubicación de red y autenticación multifactor.
* Los usuarios pueden aprovechar su identidad común a través de cuentas en Azure AD tooOffice 365, Intune, aplicaciones SaaS y aplicaciones de otros fabricantes.
* Los desarrolladores pueden crear aplicaciones que aprovechan el modelo de identidad común de hello, integración de aplicaciones en Active Directory local o en Azure para aplicaciones basadas en la nube

Hello en la ilustración siguiente se incluye un ejemplo de una vista de alto nivel del proceso de sincronización de identidades.

![](./media/hybrid-id-design-considerations/identitysync.png)

Proceso de sincronización de identidades

Revisar Hola tabla toocompare Hola sincronización opciones siguientes:

| Opción de administración de sincronización | Ventajas | Desventajas |
| --- | --- | --- |
| Basada en la sincronización (a través de DirSync o AADConnect) |Usuarios y grupos se sincronizan desde una ubicación local y la nube. <br>  **Control de directivas**: directivas de cuenta se pueden establecer a través de Active Directory, lo cual proporciona directivas de contraseñas de hello administrador Hola capacidad toomanage, estación de trabajo, las restricciones, controles de bloqueo y otros elementos, sin necesidad de tooperform adicional tareas en nube de Hola.  <br>  **Control de acceso**: puede restringir el acceso toohello servicio en la nube para que Servicios de hello pueden obtenerse a través de hello entorno corporativo, servidores en línea, o ambos. <br>  Reduce las llamadas de soporte técnico: si los usuarios tienen menos tooremember de contraseñas, son tooforget menos probabilidad de ellos. <br>  Seguridad: Información de identidades de usuario están protegidas porque todos los servidores de Hola y servicios que se utilizan en el inicio de sesión único, se controlan y controlan de forma local. <br>  Compatibilidad con la autenticación segura: puede utilizar autenticación firme (también denominada autenticación en dos fases) al servicio de nube de Hola. Sin embargo, si usa la autenticación sólida, debe emplear el inicio de sesión único. | |
| Basada en la federación (a través de AD FS) |Habilitada por el servicio de token de seguridad (STS). Al configurar un acceso de inicio de sesión único de STS tooprovide con un servicio de nube de Microsoft, creará una confianza federada entre su STS local y el dominio federado Hola que haya especificado en el inquilino de Azure AD. <br> Permite a los usuarios finales hello toouse mismo conjunto de recursos de credenciales tooobtain acceso toomultiple <br>los usuarios finales no tiene toomaintain varios conjuntos de credenciales. Sin embargo, los usuarios de hello tienen tooprovide su credenciales tooeach uno de hello participantes recursos., B2B y B2C escenarios admitidos. |Requiere personal especializado para implementar y mantener servidores AD FS locales dedicados. Hay restricciones en el uso de Hola de autenticación segura si tiene previsto toouse AD FS para tu STS. Para obtener más información, consulte la página sobre la [configuración de opciones avanzadas de AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Para obtener más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

