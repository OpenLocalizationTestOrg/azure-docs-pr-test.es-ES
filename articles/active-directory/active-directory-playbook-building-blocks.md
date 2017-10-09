---
title: "Active Directory de prueba de concepto bloques de creación de guía aaaAzure | Documentos de Microsoft"
description: "Exploración e implementación rápida de escenarios de administración de identidades y acceso"
services: active-directory
keywords: "azure active directory, guía, prueba de concepto, PoC"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Guía de prueba de concepto de Azure Active Directory: bloques de creación

## <a name="catalog-of-roles"></a>Catálogo de roles

| Rol | Descripción | Responsabilidad de la prueba de concepto (POC) |
| --- | --- | --- |
| **Equipo de arquitectura de identidad/desarrollo** | Este equipo suele ser Hola uno que diseña soluciones de hello, implementa prototipos, las unidades de aprobaciones y finalmente entrega toooperations | Proporcionan entornos hello y evaluar escenarios distintos de Hola Hola que desde la perspectiva de facilidad de uso de Hola |
| **Equipo de operaciones de identidad locales** | Administra Hola identidad diferentes orígenes locales: bosques de Active Directory, directorios LDAP, sistemas de recursos humanos y proveedores de identidades de federación. | Proporcionar acceso a los recursos locales tooon necesitan para hello escenarios de prueba de concepto.<br/>Debe estar tan poco implicado como sea posible.|
| **Propietarios técnicos de aplicaciones** | Propietarios de técnicos de hello en la nube diferentes aplicaciones y servicios que se integrarán con Azure AD | Proporcionan información detallada sobre las aplicaciones de SaaS (potencialmente instancias de prueba). |
| **Administrador global de Azure AD** | Administra la configuración de hello Azure AD | Proporcione las credenciales de servicio de sincronización de tooconfigure Hola. Normalmente Hola el mismo equipo que la arquitectura de identidad durante la prueba de concepto pero independiente durante la fase de operaciones de Hola|
| **Equipo de base de datos** | Propietarios de infraestructura de la base de datos de Hola | Proporcionar acceso de entorno de tooSQL (AD FS o Azure AD Connect) para preparados escenario concreto.<br/>Debe estar tan poco implicado como sea posible. |
| **Equipo de red** | Propietarios de infraestructura de red de Hola | Proporcionan acceso necesario Hola a nivel de red para la sincronización de hello orígenes de datos de servidores tooproperly acceso hello y servicios en la nube (reglas de firewall, puertos abiertos, las reglas de IPSec etcetera.) |
| **Equipo de seguridad** | Define la estrategia de seguridad de hello, analiza los informes de seguridad de varios orígenes y sigue a través conclusiones. | Proporciona escenarios de evaluación de la seguridad del destino. |

## <a name="common-prerequisites-for-all-building-blocks"></a>Requisitos previos comunes para todos los bloques de creación.

A continuación se proporcionan algunos requisitos previos necesarios para cualquier prueba de concepto con Azure AD Premium.

| Requisito previo | Recursos |
| --- | --- |
| Inquilino de Azure AD definido con una suscripción válida a Azure | [Cómo inquilino tooget Azure Active Directory](active-directory-howto-tenant.md)<br/>**Nota:** si ya tiene un entorno con licencias de Azure AD Premium, puede obtener una suscripción de límite cero desplazándose toohttps://aka.ms/accessaad <br/>Más información en https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ and https://technet.microsoft.com/library/dn832618.aspx. |
| Dominios definidos y verificados | [Agregar un tooAzure de nombre de dominio personalizado Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Nota:** algunas cargas de trabajo, como Power BI podría haber aprovisionado un inquilino de azure AD en hello cubre. toocheck si un dominio determinado es tooa asociado inquilino, vaya toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Si obtiene una respuesta correcta, a continuación, el dominio de hello ya está asignado a tooa inquilino y asumir podría ser necesarios. En ese caso, póngase en contacto con Microsoft para más información. Más información acerca de las opciones de adquisición de hello en: [¿qué es la suscripción de autoservicio de Azure?](active-directory-self-service-signup.md) |
| Prueba de Azure AD Premium o EMS habilitada | [Azure Active Directory Premium gratis durante un mes](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Asignó licencias de Azure AD Premium o EMS tooPoC usuarios | [Obtención de una licencia para usted y sus usuarios en Azure Active Directory.](active-directory-licensing-get-started-azure-portal.md) |
| Credenciales de administrador global de Azure AD | [Asignación de roles de administrador en Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Opcional pero muy recomendado: entorno de laboratorio paralelo como reserva | [Requisitos previos de Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Sincronización de directorios: Sincronización de hash de contraseñas (PHS) y nueva instalación

Aproximación tiempo tooComplete: una hora de menos de 1.000 usuarios de prueba de concepto

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Servidor tooRun Azure AD Connect | [Requisitos previos de Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Dirigirse a usuarios de prueba de concepto, Hola mismo dominio y parte de un grupo de seguridad y la unidad organizativa | [Instalación personalizada de Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD conectarse características que necesitan Hola se identifican la prueba de concepto | [Conexión de Active Directory con Azure Active Directory: Configuración de características de sincronización](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Tener las credenciales necesarias para entornos locales y en la nube  | [Azure AD Connect: cuentas y permisos](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Descargar la versión más reciente de Hola de Azure AD Connect | [Descarga de Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Instalar Azure AD Connect con ruta de acceso más sencillo de hello: Express <br/>1. Tiempo de ciclo de sincronización de toohello destino OU toominimize Hola de filtro<br/>2. Elija el conjunto de destinos de usuarios en el grupo local de Hola.<br/>3. Implementar características de hello necesarios por Hola otros temas de prueba de concepto | [Azure AD Connect: Instalación personalizada: Filtrado por dominio y unidad organizativa](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Instalación personalizada: Filtrado de sincronización basado en grupos](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integración de las identidades locales con Azure Active Directory: Configuración de características de sincronización](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Abrir hello Azure AD Connect interfaz de usuario y ver los perfiles de hello ejecutando completado (importación, sincronización y exportación) | [Azure AD Connect Sync: Programador](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Abra hello [portal de administración de Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), vaya toohello hoja de "Todos los usuarios", Agregar columna de "Origen de autoridad" y vea que aparecen los usuarios de hello, marcado correctamente como procedente de "Windows Server AD" | [Portal de administración de Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Consideraciones

1. Examine las consideraciones de seguridad de Hola de sincronización de hash de contraseña [aquí](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Si la sincronización de hash de contraseña para los usuarios de producción piloto definitivamente no es posible, considere la posibilidad de hello siguientes alternativas:
   * Crear usuarios de prueba en el dominio de producción de hello. Asegúrese de que no sincronizar ninguna otra cuenta.
   * Mover tooan UAT entorno
2.  Si desea que la federación toopursue, merece la pena los costos de hello toounderstand asociada a una solución federada local de proveedor de identidades más allá de la prueba de concepto de Hola y medida que contra Hola ventajas que está buscando:
    * Está en la ruta crítica de Hola para que tengan toodesign para lograr alta disponibilidad
    * Es un servicio local necesita toocapacity plan
    * Es un servicio local necesita toomonitor/mantener/patch

Más información: [Información acerca de la identidad de Office 365 y Azure Active Directory: Identidad federada](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Personalización de marca

Aproximación tiempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Activos (imágenes, logotipos, etcetera); Para la mejor visualización realizar seguro activos de hello tiene Hola tamaños recomendado. | [Agregar marcas tooyour página de inicio de sesión en hello Azure Active Directory de empresa](active-directory-branding-custom-signon-azure-portal.md) |
| Opcional: Si el entorno de hello tiene un servidor ADFS, tener acceso a tema de toohello server toocustomize web | [Personalización de inicio de sesión del usuario de FS AD](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Experiencia de inicio de sesión de cliente equipo tooperform del usuario final |  |
| Opcional: Dispositivos móviles toovalidate experiencia |  |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Vaya tooAzure AD Portal de administración | [Portal de administración de Azure AD: Personalización de marca de empresa](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Cargar activos de hello de la página de inicio de sesión de hello (logotipo héroe, logotipo pequeño, etiquetas, etcetera). Opcionalmente, si tiene AD FS, alinear Hola mismo activos con páginas de inicio de sesión ADFS | [Agregar marcas tooyour inicio de sesión y páginas de Panel de acceso de empresa: elementos personalizables](active-directory-add-company-branding.md) |
| Espere unos minutos para toofully surten efecto de cambio de Hola |  |
| Inicie sesión con hello POC usuario credencial toohttps://myapps.microsoft.com |  |
| Confirmar Hola apariencia y funcionamiento en explorador | [Agregar marcas tooyour inicio de sesión y páginas de Panel de acceso de empresa](active-directory-add-company-branding.md) |
| Si lo desea, confirme Hola apariencia y funcionamiento en otros dispositivos |  |

### <a name="considerations"></a>Consideraciones

Si Hola antiguo apariencia y funcionamiento permanece después de la personalización de hello, a continuación, vaciar la memoria caché de cliente del explorador de Hola y vuelva a intentar la operación de Hola.

## <a name="group-based-licensing"></a>Licencias basadas en grupos

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Todos los usuarios de prueba de concepto forman parte de un grupo de seguridad (en la nube o local) | [Creación de un grupo y adición de miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Vaya toolicenses hoja en el Portal de administración de Azure AD | [Portal de administración de Azure AD: Licencias](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Asigne el grupo de seguridad de hello licencias toohello con usuarios de prueba de concepto. | [Asignar a licencias tooa grupo de usuarios en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Consideraciones

En el caso de los problemas, vaya demasiado[escenarios, limitaciones y problemas conocidos con el uso de grupos de licencias toomanage en Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Configuración de SSO federado en SaaS

Aproximación tiempo tooComplete: 60 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Probar el entorno de hello aplicación SaaS disponible. En esta guía, se utiliza ServiceNow como ejemplo.<br/>Se recomienda encarecidamente toouse una fricción de toominimize de instancia de prueba sobre cómo desplazarse por las asignaciones y calidad de los datos existentes. | Vaya toohttps://developer.servicenow.com/app.do#! / home proceso de hello toostart de obtener una instancia de prueba |
| Consola de administración de ServiceNow de toohello de acceso de administrador | [Tutorial: Integración de Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Conjuntos de usuarios tooassign Hola aplicación de destino. Se recomienda un grupo de seguridad que contenga los usuarios de prueba de concepto de Hola. <br/>Si no es posible crear el grupo de hello, a continuación, asignar a usuarios de hello toodirectly toohello aplicación para prueba de concepto de hello | [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Compartir actores de tooall tutorial Hola desde Microsoft Documentation  | [Tutorial: Integración de Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Establecer una reunión de trabajo y siga los pasos del tutorial Hola con cada actor. | [Tutorial: Integración de Azure Active Directory con ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Asigne Hola aplicación toohello grupo identificado en hello requisitos previos. Si prueba de concepto de hello tenga acceso condicional en su ámbito de hello, puede volver a visitar que más adelante y agregar MFA y similares. <br/>Tenga en cuenta que esto activará Hola proceso de aprovisionamiento (si está configurado) |  [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Creación de un grupo y adición de miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Utilizar tooadd de Portal de administración de Azure AD ServiceNow aplicación de galería| [Portal de administración de AD Azure: Aplicaciones empresariales](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Novedades sobre la administración de aplicaciones empresariales en Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| En la hoja "Inicio de sesión único" de la aplicación ServiceNow, habilite "Inicio de sesión basado en SAML". |  |
| Rellene los campos "URL de inicio de sesión" e "Identificador" con la dirección URL de ServiceNow.<br/>Casilla de verificación Hola demasiado "activar un nuevo certificado"<br/>y haga clic en Guardar configuración. |  |
| Hoja de "Configurar ServiceNow" abrir en parte inferior de Hola de hello panel tooview personalizar instrucciones tooconfigure ServiceNow |  |
| Siga las instrucciones tooconfigure ServiceNow |  |
| En la hoja "Aprovisionamiento" de la aplicación ServiceNow, habilite el aprovisionamiento "Automático". | [Administración de aplicaciones empresariales en el nuevo portal de Azure Hola de aprovisionamiento de cuentas de usuario](active-directory-enterprise-apps-manage-provisioning.md) |
| Espere unos minutos mientras se completa el aprovisionamiento.  Hola mientras tanto, puede comprobar en hello aprovisionamiento informes |  |
| Inicie sesión en toohttps://myapps.microsoft.com/ como un usuario de prueba que tiene acceso | [¿Qué es hello Panel de acceso?](active-directory-saas-access-panel-introduction.md) |
| Haga clic en el icono de hello para la aplicación hello que acaba de crear. Confirme el acceso |  |
| Si lo desea, puede comprobar los informes de uso de aplicación Hola. Tenga en cuenta que hay cierta latencia, por lo que necesita toowait cierto tráfico de hello toosee de tiempo en los informes de Hola. | [Informes de actividad de inicio de sesión en el portal de Azure Active Directory hello: uso de las aplicaciones administradas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Consideraciones

1. Anteriormente [Tutorial](active-directory-saas-servicenow-tutorial.md) hace referencia a la experiencia de administración de Azure AD tooold. Pero la prueba de concepto se basa en la experiencia [Inicio rápido](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away).
2. Si la aplicación de destino de hello no está presente en la Galería de hello, puede usar "Traiga su propia aplicación". Más información: [Novedades sobre la administración de aplicaciones empresariales en Azure Active Directory: Incorporación de aplicaciones personalizadas desde un solo lugar](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Configuración de SSO con contraseña en SaaS

Aproximación tiempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Entorno de prueba para las aplicaciones SaaS. HipChat y Twitter son ejemplos de SSO de contraseña. Para cualquier otra aplicación, necesita dirección URL exacta de Hola de página de hello con el formulario de inicio de sesión de html. | [Twitter en Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat en Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Cuentas para aplicaciones de Hola de prueba. | [Registro en Twitter](https://twitter.com/signup?lang=en)<br/>[Registro gratuito: HipChat](https://www.hipchat.com/sign_up) |
| Conjuntos de usuarios tooassign Hola aplicación de destino. Se recomienda a los usuarios Hola de contenidos de grupo de seguridad. | [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Hola de toodeploy extensión del Panel de acceso de Internet Explorer, Chrome o Firefox para el equipo de tooa de acceso Administrador local | [Extensión Access Panel para IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensión Access Panel para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensión Access Panel para Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Instalar extensión de explorador Hola | [Extensión Access Panel para IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensión Access Panel para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensión Access Panel para Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configuración de una aplicación de la galería | [Novedades de la administración de aplicaciones de empresa en Azure Active Directory: Galería de aplicaciones nuevas y mejoradas de Hola](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configure la contraseña de SSO. | [Administración de inicio de sesión único para aplicaciones empresariales en el nuevo portal de Azure hello: inicio de sesión basado en contraseña en](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Asignar Hola aplicación toohello grupo identificado en hello requisitos previos | [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Inicie sesión en toohttps://myapps.microsoft.com/ como un usuario de prueba que tiene acceso |  |
| Haga clic en el icono de hello para la aplicación hello que acaba de crear. | [¿Qué es hello Panel de acceso?: SSO basado en contraseña sin proporcionar identidad](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Proporcionar credenciales de aplicación Hola | [¿Qué es hello Panel de acceso?: SSO basado en contraseña sin proporcionar identidad](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Cierre el explorador Hola e inicio de sesión de repetición Hola. Este tema usuario Hola debería ver la aplicación de toohello de acceso sin problemas. |  |
| Si lo desea, puede comprobar los informes de uso de aplicación Hola. Tenga en cuenta que hay cierta latencia, por lo que necesita toowait cierto tráfico de hello toosee de tiempo en los informes de Hola. | [Informes de actividad de inicio de sesión en el portal de Azure Active Directory hello: uso de las aplicaciones administradas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Consideraciones

Si la aplicación de destino de hello no está presente en la Galería de hello, puede usar "Traiga su propia aplicación". Más información: [Novedades sobre la administración de aplicaciones empresariales en Azure Active Directory: Incorporación de aplicaciones personalizadas desde un solo lugar](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenga en hello cuenta según los requisitos:
   * La aplicación debe tener una dirección URL de inicio de sesión conocida.
   * página de inicio de sesión de Hello debe contener un formulario HTML con uno más campos de texto que las extensiones del explorador Hola pueden rellenar de forma automática. En hello mínimo, debe contener username y password.

## <a name="saas-shared-accounts-configuration"></a>Configuración de cuentas compartidas de SaaS

Aproximación tiempo tooComplete: 30 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Hola lista de aplicaciones de destino y Hola exactas inicio de sesión en las direcciones URL antes de tiempo. Por ejemplo, puede usar Twitter. | [Twitter en Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Registro en Twitter](https://twitter.com/signup?lang=en) |
| Credenciales compartidas para esta aplicación SaaS. | [Uso compartido de cuentas con Azure AD](active-directory-sharing-accounts.md)<br/>[Azure AD automated password roll-over for Facebook, Twitter and LinkedIn now in preview! Enterprise Mobility and Security Blog (Versión preliminar de la sustitución automatizada de contraseñas de Azure AD para Facebook, Twitter y LinkedIn: Blog de seguridad y movilidad empresarial)] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Las credenciales de al menos dos miembros del equipo que tendrá acceso a Hola misma cuenta. Deben formar parte de un grupo de seguridad. | [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Hola de toodeploy extensión del Panel de acceso de Internet Explorer, Chrome o Firefox para el equipo de tooa de acceso Administrador local | [Extensión Access Panel para IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensión Access Panel para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensión Access Panel para Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Instalar extensión de explorador Hola | [Extensión Access Panel para IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensión Access Panel para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensión Access Panel para Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configuración de una aplicación de la galería | [Novedades de la administración de aplicaciones de empresa en Azure Active Directory: Galería de aplicaciones nuevas y mejoradas de Hola](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configure la contraseña de SSO. | [Administración de inicio de sesión único para aplicaciones empresariales en el nuevo portal de Azure hello: inicio de sesión basado en contraseña en](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Asignar Hola aplicación toohello grupo identificado en hello requisitos previos durante la asignación de credenciales | [Asignar una aplicación de empresa de tooan de usuario o grupo en Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Inicie sesión como distintos usuarios de esa aplicación de acceso como hello **mismas compartida cuenta.**  |  |
| Si lo desea, puede comprobar los informes de uso de aplicación Hola. Tenga en cuenta que hay cierta latencia, por lo que necesita toowait cierto tráfico de hello toosee de tiempo en los informes de Hola. | [Informes de actividad de inicio de sesión en el portal de Azure Active Directory hello: uso de las aplicaciones administradas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Consideraciones

Si la aplicación de destino de hello no está presente en la Galería de hello, puede usar "Traiga su propia aplicación". Más información: [Novedades sobre la administración de aplicaciones empresariales en Azure Active Directory: Incorporación de aplicaciones personalizadas desde un solo lugar](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenga en hello cuenta según los requisitos:
   * La aplicación debe tener una dirección URL de inicio de sesión conocida.
   * página de inicio de sesión de Hello debe contener un formulario HTML con uno más campos de texto que las extensiones del explorador Hola pueden rellenar de forma automática. En hello mínimo, debe contener username y password.

## <a name="app-proxy-configuration"></a>Configuración de proxy de aplicación

Aproximación tooComplete de tiempo: 20 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Una suscripción Basic o Premium a Microsoft Azure AD y un directorio de Azure AD del que sea administrador global. | [Ediciones de Azure Active Directory](active-directory-editions.md) |
| Una aplicación web hospedada que desearía tooconfigure para el acceso remoto a local |  |
| Un servidor que ejecute Windows Server 2012 R2 o Windows 8.1 o posterior, en el que puede instalar Hola conector del Proxy de aplicación | [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md) |
| Si hay un firewall en la ruta de acceso de hello, asegúrese de que está abierto, por lo que Hola que conector podrá efectuar HTTPS (TCP) solicita toohello Proxy de aplicación | [Habilita el Proxy de aplicación en hello portal de Azure: requisitos previos del Proxy de aplicación](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Si su organización usa proxy toohello tooconnect de servidores de internet, realice un vistazo a Hola blog post trabajar con servidores de proxy local existente para detalles acerca de cómo tooconfigure ellos | [Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Instalar un conector en el servidor de Hola | [Habilita el Proxy de aplicación en hello portal de Azure: instalar y registrar Hola conector](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Publicar aplicación de hello local en Azure AD como una aplicación de Proxy de aplicación | [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md) |
| Asigne usuarios de prueba. | [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD: Adición de un usuario de prueba](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Si lo desea, configure una experiencia de inicio de sesión único para los usuarios. | [Provisión de inicio de sesión único mediante el proxy de aplicación de Azure AD](application-proxy-sso-azure-portal.md) |
| Probar la aplicación debe iniciar sesión en el portal de tooMyApps como usuario asignado | https://myapps.microsoft.com |

### <a name="considerations"></a>Consideraciones

1. Aunque se recomienda colocar el conector de hello en su red corporativa, hay casos en que verán un mejor rendimiento colocándolo en la nube de Hola. Más información: [Consideraciones sobre la topología de red al utilizar el Proxy de aplicación de Azure Active Directory](application-proxy-network-topology-considerations.md)
2. Para más detalles de seguridad y cómo esto proporciona una solución de acceso remoto especialmente seguro manteniendo únicamente las conexiones salientes, consulte [Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el Proxy de aplicación de Azure AD](application-proxy-security-considerations.md).

## <a name="generic-ldap-connector-configuration"></a>Configuración genérica del conector LDAP

Aproximación tiempo tooComplete: 60 minutos

> [!IMPORTANT]
> Se trata de una configuración avanzada que requiere cierta familiaridad con FIM o MIM. Si se usa en producción, se recomienda plantear las preguntas sobre esta configuración a través del [soporte técnico Premier](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Azure AD Connect instalado y configurado | Bloque de creación: [Sincronización de directorios: sincronización de hash de contraseñas](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Cumplir los requisitos de la instancia de ADLDS | [Referencia técnica de conector LDAP genérico: información general de hello conector LDAP genérico](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Lista de las cargas de trabajo que los usuarios usan y atributos asociados a ellas. | [Azure AD Connect sync: atributos sincronizados tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Incorporación del conector LDAP genérico | [Referencia técnica del conector de LDAP genérico: Creación de un nuevo conector](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Cree perfiles de ejecución para el conector creado (importación completa, importación diferencial, sincronización completa, sincronización diferencial y exportación). | [Create a Management Agent Run Profile](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx) (Creación de un perfil de ejecución del agente de administración)<br/> [Uso de conectores con hello Azure AD Connect Sync Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Ejecute el perfil de importación completa y verifique que hay objetos en el espacio del conector. | [Search for a Connector Space Object](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx) (Búsqueda de un objeto en el espacio del conector)<br/>[Uso de conectores con hello Azure AD Connect Sync Service Manager: espacio de conector de búsqueda](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Cree reglas de sincronización para que los objetos del metaverso tengan los atributos necesarios para las cargas de trabajo. | [Azure AD Connect sync: las prácticas recomendadas para cambiar la configuración predeterminada de hello: cambia tooSynchronization reglas](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect Sync: conocimiento del aprovisionamiento declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect Sync: conocimiento de expresiones de aprovisionamiento declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Inicie el ciclo de sincronización completa. | [Azure AD Connect sync: programador: iniciar el programador de Hola](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| En caso de problemas, soluciónelos. | [Solucionar problemas de un objeto que no se han sincronizado tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Compruebe que LDAP usuario puede iniciar sesión y tener acceso a la aplicación hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Consideraciones

> [!IMPORTANT]
> Se trata de una configuración avanzada que requiere cierta familiaridad con FIM o MIM. Si se usa en producción, se recomienda plantear las preguntas sobre esta configuración a través del [soporte técnico Premier](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Grupos: propiedad delegada

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Aplicación de SaaS (SSO federado o SSO de contraseña) ya configurado | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) |
| Se identifica el grupo de nube que se asigna la aplicación de access toohello en #1 | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) <br/>[Creación de un grupo y adición de miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Las credenciales para el propietario del grupo Hola están disponibles | [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md) |
| Se ha identificado las credenciales para hello información trabajo accediendo a aplicaciones de Hola | [¿Qué es hello Panel de acceso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Identificar el grupo de Hola que se ha concedido acceso toohello aplicación y configurar propietario Hola de determinado grupo| [Administrar la configuración de Hola para un grupo en Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Inicie sesión como propietario del grupo de hello, vea Hola la pertenencia de grupo en la ficha grupos del panel de acceso | [Página de administración de grupos de Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Agregar el trabajador de la información de hello desea tootest |  |
| Inicie sesión como trabajador de la información de hello, confirme el mosaico de hello está disponible | [¿Qué es hello Panel de acceso?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Consideraciones

Si la aplicación hello tiene habilitado el aprovisionamiento, podría necesitar toowait unos minutos para hello aprovisionamiento toocomplete antes de acceder a la aplicación hello como trabajador de la información de Hola.

## <a name="saas-and-identity-lifecycle"></a>Ciclo de vida de identidad y SaaS

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Aplicación de SaaS (SSO federado o SSO de contraseña) ya configurado | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) |
| Se identifica el grupo de nube que se asigna la aplicación de access toohello en #1 | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) <br/>[Creación de un grupo y adición de miembros en Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Se ha identificado las credenciales para hello información trabajo accediendo a aplicaciones de Hola | [¿Qué es hello Panel de acceso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Quitar usuario Hola de aplicación Hola de hello grupo se asigna demasiado| [Administración de la pertenencia a grupos de los usuarios del inquilino de Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Espere unos minutos para la cancelación del aprovisionamiento. | [Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory: ¿Cómo funciona el aprovisionamiento automático?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| En una sesión independiente del explorador, inicie sesión como portal de hello información trabajo toomy aplicaciones y confirme ese icono es que faltan | http://myapps.microsoft.com |


### <a name="considerations"></a>Consideraciones

Extrapolar tooleavers de escenario de prueba de concepto de Hola o escenarios de baja por ausencia. Si el usuario de hello obtiene deshabilitado en AD local o quitado, ya no es una manera toolog en toohello aplicación SaaS.

## <a name="self-service-access-tooapplication-management"></a>En sí mismo tooApplication administración de acceso al servicio

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Identificar a los usuarios de prueba de concepto que soliciten acceso toohello aplicaciones, como parte del grupo de seguridad de Hola | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) |
| Aplicación de destino implementada. | Bloque de creación: [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Vaya tooEnterprise hoja de aplicaciones en Portal de administración de Azure AD | [Portal de administración de AD Azure: Aplicaciones empresariales](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Configure la aplicación a partir de los requisitos previos con autoservicio. | [Novedades de la administración de aplicaciones de empresa en Azure Active Directory: Configuración del acceso a aplicaciones en modo autoservicio](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Inicie sesión como portal de aplicaciones de hello información trabajo toomy | http://myapps.microsoft.com |
| Tenga en cuenta "+ Agregar aplicación" botón en operaciones de página Hola. Usar tooget acceso toohello aplicación |  |

### <a name="considerations"></a>Consideraciones

aplicaciones de Hello elegidas pueden tener requisitos, el aprovisionamiento va inmediatamente toohello aplicación podría causar algunos errores. Si la aplicación hello elegido admite el aprovisionamiento con azure ad y se configura, debería usar esta opción como un oportunidad tooshow Hola todo flujo trabajar tooend final. Consulte el bloque de creación de hello para [configuración de SSO federado SaaS](#saas-federated-sso-configuration) recomendaciones adicionales

## <a name="self-service-password-reset"></a>Restablecimiento de contraseñas de autoservicio

Aproximación tiempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Habilitar la administración de contraseñas de autoservicio en el inquilino. | [Restablecimiento de contraseña de Azure Active Directory para administradores de TI](active-directory-passwords.md) |
| Habilitar las contraseñas de toomanage de reescritura de contraseña desde el entorno local. Tenga en cuenta que esto requiere versiones específicas de Azure AD Connect | [Requisitos previos de escritura diferida de contraseñas](active-directory-passwords-writeback.md) |
| Identificar a los usuarios de prueba de concepto de Hola que usará esta funcionalidad y asegúrese de que son miembros de un grupo de seguridad. los usuarios de Hello deben ser la capacidad de no administradores toofully showcase Hola | [Personalizar: Administración de Azure AD contraseñas: restringir acceso toopassword restablecimiento](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Navegue tooAzure AD Portal de administración: restablecimiento de contraseña | [Portal de administración de Azure AD: Restablecimiento de contraseñas](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Determinar la directiva de restablecimiento de contraseña de Hola. Con fines de prueba de concepto, puede utilizar la llamada de teléfono y preguntas y respuestas. Se recomienda tooenable registro toobe necesaria en el registro en el panel de tooaccess |  |
| Cierre sesión e iníciela como un trabajador de información. |  |
| Proporcionar datos de autoservicio de restablecimiento de contraseña de hello como configurado por el paso 2 | http://aka.ms/ssprsetup |
| Explorador de hello cerrar |  |
| Empezar el proceso de inicio de sesión de hello como trabajador de la información de hello usado en el paso 4 |  |
| Hola de restablecimiento de contraseña | [Actualización de su propia contraseña: restablecimiento de mi contraseña](active-directory-passwords-update-your-own-password.md) |
| Intente iniciar sesión con su nueva contraseña tooAzure AD, así como los recursos locales tooon |  |

### <a name="considerations"></a>Consideraciones

1. Si actualiza hello Azure AD Connect va toocause fricción, a continuación, considere el uso con cuentas en la nube o realizar una demostración en un entorno independiente
2. los administradores de Hello tienen una directiva diferente y usando Hola, administrador contraseña de cuenta de hello tooreset podría alterar las Hola prueba de concepto y llevan a confusión. Asegúrese de que utilizar una operación de restablecimiento de usuario normal cuenta tootest Hola


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure Multi-Factor Authentication con llamadas de teléfono

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Identificar a los usuarios de prueba de concepto que usarán MFA  |  |
| Teléfono con una buena cobertura de el desafío de MFA  | [¿Qué es Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Navegue demasiado hoja "Usuarios y grupos" en el Portal de administración de Azure AD | [Portal de administración de Azure AD: Usuarios y grupos](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Elija la hoja "Todos los usuarios". |  |
| En la barra elegir el botón "La autenticación multifactor" superior de Hola | Dirección URL directa para el portal de Azure MFA: https://aka.ms/mfaportal. |
| En la configuración de "Usuario" Hola, seleccione los usuarios de prueba de concepto de Hola y habilitarlas para MFA | [Estados de usuario en Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Inicie sesión como usuario de prueba de concepto de Hola y recorrido a través del proceso de prueba de Hola  |  |

### <a name="considerations"></a>Consideraciones

1. Hola PoC pasos de este bloque de creación se establece explícitamente MFA para un usuario en todos los inicios de sesión. Hay otras herramientas como el acceso condicional y la protección de identidad que interactúan con MFA en otros escenarios. Esto tendrá un aspecto tooconsider al pasar de la prueba de concepto tooproduction.
2. pasos de prueba de concepto de Hello en este bloque de creación explícitamente usa llamadas de teléfono como método MFA para expedience Hola. Tal y como se realiza la transición de tooproduction de prueba de concepto, se recomienda usar aplicaciones como hello [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) como el segundo factor siempre que sea posible.
Más información: [Estándar DRAFT NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Acceso condicional de MFA para aplicaciones SaaS

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Identificar la directiva de Hola de tootarget de los usuarios de prueba de concepto. Estos usuarios deben estar en una directiva de acceso condicional de seguridad grupo tooscope Hola | [Configuración de SSO federado en SaaS](#saas-federated-sso-configuration) |
| Aplicación de SaaS ya está configurado |  |
| Los usuarios de prueba de concepto ya están asignados toohello aplicación |  |
| Usuario de prueba de concepto de toohello credenciales están disponibles |  |
| El usuario de prueba de concepto está registrado para MFA Uso de un teléfono con una buena cobertura | http://aka.ms/ssprsetup |
| Dispositivo de red interna de Hola. Dirección IP configurada en el intervalo de dirección interna de Hola | Localice la dirección IP: https://www.bing.com/search?q=what%27s+my+ip |
| Dispositivo de red externa hello (puede ser un teléfono mediante red móvil del transportista hello) |  |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Vaya tooAzure AD Portal de administración: hoja de acceso condicional | [Portal de administración de Azure AD: Acceso condicional](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Cree una directiva de acceso condicional:<br/>- Usuarios de prueba de concepto de destino en "Usuarios y grupos".<br/>- Aplicación de prueba de concepto de destino en "Aplicaciones en la nube".<br/>- Coloque todas las ubicaciones, excepto las de confianza, en "Condiciones" -> "Ubicaciones" **Nota:** Las IP de confianza se configuran en el [Portal MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx).<br/>- Requiere Multi-Factor Authentication en "Conceder". | [Introducción al acceso condicional en Azure Active Directory: Pasos de la configuración de la directiva](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Acceda a la aplicación desde la red corporativa. | [Empezar a trabajar con el acceso condicional en Azure Active Directory: probar directiva Hola](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Acceda a la aplicación desde la red pública. | [Empezar a trabajar con el acceso condicional en Azure Active Directory: probar directiva Hola](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Consideraciones

Si está utilizando la federación, puede usar Hola de hello local proveedor de identidades (IdP) toocommunicate interna/externa estado de la red corporativa con notificaciones. Esta técnica se puede utilizar sin tener toomanage Hola lista de direcciones IP que podría ser tooassess complejos y administrar en grandes organizaciones. En que la instalación, necesita la cuenta para el escenario de "red móvil" hello (es decir, un usuario registro desde la red interna de Hola y mientras ha iniciado sesión conmutadores ubicaciones como una cafetería) y asegúrese de que comprenda las implicaciones de Hola. Obtener más información: [Protección de recursos en la nube con Azure Multi-Factor Authentication y AD FS: Direcciones IP de confianza para usuarios federados](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

Aproximación tiempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Identificar Hola, administrador global que se va a formar parte del programa Hola a prueba de concepto para PIM | [Comenzar a usar Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Identificar Hola, administrador global que se convertirá en Administrador de seguridad de Hola | [Comenzar a usar Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Rol administrativo diferente en Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Opcional: Confirmar si los administradores globales de hello tienen correo electrónico tener acceso a las notificaciones de correo electrónico de tooexercise de PIM | [¿Qué es Azure AD Privileged Identity Management?: configurar opciones de activación de rol de Hola](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Toohttps://portal.azure.com inicio de sesión como un administrador global (GA) y la hoja PIM de arranque Hola. Hola administrador Global que realiza este paso es visible como administrador de seguridad de Hola.  Vamos a llamar a este actor GA1. | [Utilizando el Asistente para la seguridad de hello en Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Hola, administrador global de identificar y moverlos desde tooeligible permanente. Debe ser un administrador independiente desde Hola utilizó en el paso 1 para mayor claridad. Vamos a llamar a este actor GA2. | [AD Privileged Identity Management de Azure: ¿Cómo tooadd o quitar un rol de usuario](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[¿Qué es Azure AD Privileged Identity Management?: configurar opciones de activación de rol de Hola](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Ahora, inicie sesión como toohttps://portal.azure.com GA2 y pruebe a cambiar "Configuración de usuario". Tenga en cuenta que algunas opciones aparecen atenuadas. | |
| En una nueva pestaña en hello misma sesión como el paso 3, navegue toohttps://portal.azure.com ahora y agregar Hola PIM hoja toohello panel. | [¿Cómo tooactivate o desactivar los roles en Azure AD Privileged Identity Management: Agregar aplicación de hello Privileged Identity Management](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Rol de administrador Global de solicitud de activación toohello | [¿Cómo tooactivate o desactivar los roles en Azure AD Privileged Identity Management: activar un rol](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Tenga en cuenta que si GA2 nunca se registró para MFA, será necesario registrarse para Azure MFA. |  |
| Volver atrás toohello ficha original en el paso 3 y haga clic en el botón de actualización de hello en el Explorador de Hola. Tenga en cuenta que ahora tiene acceso toochange "Configuración de usuario" | |
| Opcionalmente, si los administradores globales tienen correo electrónico habilitado, puede comprobar GA1 y de GA2 Bandeja de entrada y ver Hola notificación de rol Hola se activa |  |
| 8 Compruebe el historial de auditoría de Hola y observar la elevación de hello informe tooconfirm Hola de GA2 se muestra. | [¿Qué es Azure AD Privileged Identity Management?: Revisión de la actividad de un rol](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Consideraciones

Esta funcionalidad forma parte de Azure AD Premium P2 y EMS E5.

## <a name="discovering-risk-events"></a>Detección de eventos de riesgo

Aproximación tooComplete de tiempo: 20 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Dispositivo con el explorador Tor descargado e instalado | [Descarga del explorador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Inicio de sesión de acceso tooPOC usuario toodo Hola | [Azure Active Directory Identity Protection playbook (Guía de Azure Active Directory Identity Protection)](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Abra el explorador Tor | [Descarga del explorador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Inicie sesión en toohttps://myapps.microsoft.com con hello cuenta de usuario de prueba de concepto | [Guía de Azure Active Directory Identity Protection: Simulación de eventos de riesgo](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Espere 5-7 minutos. |  |
| Inicie sesión como un administrador global toohttps://portal.azure.com y abra una hoja de protección de la identidad de Hola | https://aka.ms/aadipgetstarted |
| Hoja de eventos de riesgo de hello abierto. Debería ver una entrada en "Inicios de sesión desde direcciones IP anónimas".  | [Guía de Azure Active Directory Identity Protection: Simulación de eventos de riesgo](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Consideraciones

Esta funcionalidad forma parte de Azure AD Premium P2 y EMS E5.

## <a name="deploying-sign-in-risk-policies"></a>Implementación de directivas de riesgo de inicio de sesión

Aproximación tiempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Dispositivo con el explorador Tor descargado e instalado | [Descarga del explorador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Acceso como un inicio de sesión de prueba de concepto usuario toodo hello en las pruebas |  |
| Usuario de prueba de concepto registrado en MFA. Asegúrese de que toouse un teléfono con una buena cobertura | Bloque de creación: [Azure Multi-Factor Authentication con llamadas de teléfono](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Inicie sesión como un toohttps://portal.azure.com administrador global y abra la hoja de protección de la identidad de Hola | https://aka.ms/aadipgetstarted |
| Habilite una directiva de inicio de sesión de riesgo de la manera siguiente:<br/>- Asignado a: usuario de prueba de concepto<br/>- Condiciones: inicio de sesión de riesgo medio o superior (el inicio de sesión en desde una ubicación anónima se considera un nivel de riesgo medio)<br/>- Controles: requiere MFA | [Guía de Azure Active Directory Identity Protection: Riesgo de inicio de sesión](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Abra el explorador Tor | [Descarga del explorador Tor](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Inicie sesión en toohttps://myapps.microsoft.com con hello cuenta de usuario de prueba de concepto |  |
| Hola aviso desafío MFA | [Experiencias de inicio de sesión con Azure AD Identity Protection: Recuperación de inicios de sesión peligrosos](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Consideraciones

Esta funcionalidad forma parte de Azure AD Premium P2 y EMS E5. toolearn más acerca de los eventos de riesgo, visite: [eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Configuración de autenticación basada en certificados

Aproximación toocomplete de tiempo: 20 minutos

### <a name="pre-requisites"></a>Requisitos previos

| Requisito previo | Recursos |
| --- | --- |
| Dispositivos con certificado de usuario aprovisionado (Windows, iOS o Android) de Enterprise PKI | [Implementar certificados de usuario](https://msdn.microsoft.com/library/cc770857.aspx) |
| Dominio de Azure AD federado con ADFS | [Azure AD Connect y la federación](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Información general de Servicios de certificados de Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Para dispositivos iOS, tener instalada la aplicación Microsoft Authenticator | [Introducción a la aplicación de Microsoft Authenticator hello](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Pasos

| Paso | Recursos |
| --- | --- |
| Habilite la Autenticación de certificados en ADFS. | [Configurar directivas de autenticación: tooconfigure principal autenticación globalmente en Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Opcional: Habilite la autenticación de certificados en Azure AD para los clientes de Exchange Active Sync. | [Introducción a la autenticación basada en certificados de Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Navegue tooAccess Panel y autenticarse con el certificado de usuario | https://myapps.microsoft.com |

### <a name="considerations"></a>Consideraciones

toolearn sobre advertencias de esta implementación, visite: [ADFS: autenticación de certificado con Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Debe mantenerse la posesión del certificado de usuario. Mediante la administración de dispositivos o con PIN en el caso de las tarjetas inteligentes.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
