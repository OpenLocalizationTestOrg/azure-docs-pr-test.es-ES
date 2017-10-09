---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - definir la estrategia de protección de datos | Documentos de Microsoft"
description: "Estrategia de protección de datos de hello definirá para sus híbrida identidad solución toomeet Hola requisitos empresariales que ha definido."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Definición de una estrategia de protección de datos para soluciones de identidad híbrida
En esta tarea, definirá la estrategia de protección de datos de Hola para sus híbrida identidad solución toomeet Hola requisitos empresariales que usted definió en:

* [Determinación de los requisitos de protección de datos](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Determinación de los requisitos de administración de contenido](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Determinación de los requisitos de control de acceso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Determinación de los requisitos de respuesta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Definición de las opciones de protección de datos
Como se explicó en [Determinación de los requisitos de sincronización de directorios](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), Microsoft Azure AD puede sincronizar con los Servicios de dominio de Active Directory  (AD DS) ubicados localmente. Esta integración permite a las credenciales de usuario de las organizaciones tooleverage Azure AD tooverify al tratar de tooaccess los recursos corporativos. Esto puede hacerse para ambos escenarios: datos en rest local y en la nube Hola.  Toodata de acceso de Azure AD requiere autenticación del usuario a través de un servicio de token de seguridad (STS).

Una vez autenticado, nombre de entidad de seguridad de usuario (UPN) de hello es de lectura de token de autenticación de Hola y Hola replica la partición y el contenedor correspondiente se determina el dominio del usuario toohello. Obtener información sobre la existencia del usuario de hello, el estado habilitado y la función se utiliza por toodetermine de sistema de autorización de hello si inquilino de destino de hello acceso solicitado toohello está autorizado para este usuario en esta sesión. Determinadas acciones autorizados (específicamente, crear usuario, restablecer la contraseña) crear una pista de auditoría que se puede usar un inquilino esfuerzos de cumplimiento de normas de administrador toomanage o investigaciones.

Migración de datos de su centro de datos local en el almacenamiento de Azure a través de una conexión a Internet no siempre es factible debido toodata volumen, la disponibilidad de ancho de banda u otras consideraciones. Hola [servicio de importación y exportación de almacenamiento de Azure](../storage/common/storage-import-export-service.md) proporciona una opción basada en hardware para colocar/recuperar grandes volúmenes de datos de almacenamiento de blobs. Le permite toosend [cifrada con BitLocker](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) unidades de disco duro directamente tooan centro de datos de Azure donde operadores en la nube permite cargar la cuenta de almacenamiento de hello contenido tooyour o puede descargar el tooyour de datos de Azure unidades tooreturn tooyou. Solo los discos cifrados se aceptan para este proceso (con una clave de BitLocker generada por el servicio durante la instalación de trabajo de Hola Hola). Hola BitLocker se proporciona la clave tooAzure por separado, lo que proporciona fuera de banda clave compartida.

Puesto que los datos en tránsito pueden tener lugar en distintos escenarios, también es tooknow pertinente que utiliza Microsoft Azure [redes virtuales](https://azure.microsoft.com/documentation/services/virtual-network/) tráfico de inquilinos tooisolate del resto, que emplea medidas como host - y -nivel de invitado los servidores de seguridad, filtrado de paquetes IP, el bloqueo de puertos y extremos HTTPS. Sin embargo, también se cifran la mayoría de las comunicaciones internas de Azure, incluida las de infraestructura con infraestructura e infraestructura con cliente (local). Otro escenario importante consiste en las comunicaciones de hello en centros de datos de Azure; Microsoft administra tooassure de redes que ninguna máquina virtual puede suplantar o espiar las direcciones IP de Hola de otro. TLS/SSL se utiliza al obtener acceso a bases de datos SQL o almacenamiento de Azure, o cuando se conecta a servicios de tooCloud. En este caso, el Administrador de cliente de hello es responsable de obtener un certificado TLS/SSL e implementarla tootheir la infraestructura de inquilinos. Mover entre las máquinas virtuales de tráfico de datos en Hola misma implementación o a través de protocolos de comunicación cifrada como HTTPS, SSL/TLS u otras personas se pueden proteger entre los inquilinos en una sola implementación a través de la red Virtual de Microsoft Azure.

Según como haya respondido a las preguntas de hello en [determinar los requisitos de protección de datos](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), debe ser capaz de toodetermine cómo desea tooprotect los datos y cómo la solución de identidad híbrida de hello le ayudará en el que. tabla de Hello muestra opciones de hello compatibles con Azure que están disponibles para cada escenario de protección de datos.

| Opciones de protección de datos | En reposo en la nube de Hola | En reposo localmente | En tránsito |
| --- | --- | --- | --- |
| Cifrado BitLocker de unidades |X |X | |
| Bases de datos de SQL Server tooencrypt |X |X | |
| Cifrado de VM a VM | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Lectura [cumplimiento por característica](https://azure.microsoft.com/support/trust-center/services/) en [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow más acerca de las certificaciones de Hola que sea compatible con cada servicio de Azure.
> Dado que las opciones de hello para la protección de datos usan un enfoque multicapa, comparación entre esas opciones no son aplicables para esta tarea. Asegúrese de que se aprovechan todas las opciones disponibles para cada estado que Hola datos estarán.
>
>

## <a name="define-content-management-options"></a>Definición de las opciones de administración de contenido
Una ventaja de usar Azure AD toomanage una infraestructura de identidad híbrida es que el proceso de hello es totalmente transparente desde la perspectiva del usuario final Hola. usuario de Hello intentará tooaccess un recurso compartido, Hola recurso requiere la autenticación, usuario Hola tendrá toosend un tooAzure de solicitud de autenticación AD en orden tooobtain Hola símbolo (token) y tener acceso a recursos de Hola. Todo este proceso se produce en segundo plano, sin interacción del usuario. También es posible toogrant permiso tooa [grupo](active-directory-manage-groups.md#getting-started-with-access-management) de usuarios en orden tooallow les tooperform determinadas acciones comunes.

Las organizaciones a las que preocupa la privacidad de los datos requieren la clasificación de datos para su solución. Si su infraestructura local actual ya está usando la clasificación de datos, es posible tooleverage Azure AD como repositorio principal de hello para la identidad del usuario. Una herramienta común que se usa localmente para la clasificación de datos se denomina [Data Classification Toolkit](https://msdn.microsoft.com/library/Hh204743.aspx) para Windows Server 2012 R2. Esta herramienta puede ayudar a tooidentify, clasificar y proteger los datos en servidores de archivos en la nube privada. También es posible tooleverage hello [Automatic File Classification](https://technet.microsoft.com/library/hh831672.aspx) en Windows Server 2012 tooaccomplish esto.

Si su organización no tiene la clasificación de datos en su lugar, pero necesita tooprotect los archivos confidenciales sin tener que agregar nuevos servidores locales, puede utilizar Microsoft [Azure Rights Management Service](https://technet.microsoft.com/library/JJ585026.aspx).  Azure RMS usa cifrado, identidad y autorización toohelp directivas segura los archivos y correos electrónicos y funciona en varios dispositivos: teléfonos, tabletas y equipos. Dado que Azure RMS es un servicio de nube, no es necesario tooexplicitly configurar relaciones de confianza con otras organizaciones para poder compartir contenido protegido con ellas. Si ya tienen un directorio de Office 365 o Azure AD, la colaboración entre organizaciones se admite automáticamente. También puede sincronizar solo Hola atributos de directorio que Azure RMS necesita toosupport una identidad común para las cuentas de Active Directory local, mediante el uso de Azure Active Directory Synchronization Services (AAD Sync) o Azure AD Connect.

Una parte vital de la administración de contenido es toounderstand quién tiene acceso a qué recursos, por lo tanto, es importante para la solución de administración de identidades de hello una capacidad de registro completo. Azure AD proporciona registro durante 30 días. Dicho registro incluye:

* Cambios en la pertenencia al rol (por ejemplo: usuario agrega el rol de administrador de tooGlobal)
* Actualizaciones de credenciales (por ejemplo, cambios de contraseña)
* Administración de dominios (por ejemplo, comprobar un dominio personalizado o eliminar un dominio)
* Adición o eliminación de aplicaciones
* Administración de usuarios (por ejemplo, agregar, eliminar o actualizar un usuario)
* Adición o eliminación de licencias

> [!NOTE]
> Lectura [seguridad de Microsoft Azure y administración de registros de auditoría](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow más información acerca de las capacidades de registro en Azure.
> Según como haya respondido a las preguntas de hello en [determinar los requisitos de administración de contenido](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), debe ser capaz de toodetermine cómo desea Hola toobe contenido administrado en su solución de identidad híbrida. Aunque todas las opciones que se muestran en la tabla 6 son capaces de integración con Azure AD, es importante toodefine que es más adecuada para sus necesidades empresariales.
>
>

| Opciones de administración de contenido | Ventajas | Desventajas |
| --- | --- | --- |
| Centralizada localmente (servidor de Active Directory Rights Management) |Control total sobre la infraestructura de servidor hello responsable de la clasificación de datos de Hola <br> Funcionalidad integrada de Windows Server, sin necesidad de suscripción o de licencia adicional <br> Se puede integrar con Azure AD en un escenario híbrido. <br> Admite funcionalidades de Information Rights Management (IRM) en Microsoft Online Services como Exchange Online y SharePoint Online, así como Office 365. <br> Admite productos de servidor de Microsoft locales, como Exchange Server , SharePoint Server y servidores de archivo que ejecutan Windows Server e infraestructura de clasificación de archivos (FCI). |Mantenimiento superior (atender con actualizaciones, configuración y posibles actualizaciones), desde TI posee Hola Server <br> Requiere una infraestructura de servidor local.<br> No saca provecho a las capacidades de Azure de forma nativa |
| Centralizado en hello nube (Azure RMS) |Más fácil toohello toomanage en comparación con solución local <br> Se puede integrar con AD DS en un escenario híbrido. <br>  Completamente integrado con Azure AD. <br> No requiere un servidor de forma local en el servicio de pedidos toodeploy Hola <br> Admite productos de servidor de Microsoft locales, como Exchange Server , SharePoint Server y servidores de archivo que ejecutan Windows Server e infraestructura de clasificación de archivos (FCI). <br> TI, puede tener un control completo sobre la clave de su inquilino con capacidad de BYOK. |Su organización debe tener una suscripción de nube que admita RMS  <br> Su organización debe tener una autenticación de usuario de Azure AD directory toosupport para RMS |
| Híbrida (Azure RMS integrado con Active Directory Rights Management Server local) |Este escenario acumula ventajas de Hola de ambos, centralizado en un entorno local y en la nube de Hola. |Su organización debe tener una suscripción de nube que admita RMS  <br> Su organización debe tener una autenticación de usuario de Azure AD directory toosupport para RMS, <br> Requiere una conexión entre el servicio en la nube de Azure y la infraestructura local |

## <a name="define-access-control-options"></a>Definición de opciones de control de acceso
Mediante el aprovechamiento de autenticación de hello, autorización y control de acceso capacidades disponibles en Azure AD será capaz de tooenable su toouse un repositorio central de identidad de empresa al permitir que los usuarios y socios toouse inicio de sesión único (SSO) como se muestra en hello ilustración siguiente:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Administración centralizada e integración total con otros directorios

Azure Active Directory ofrece toothousands de inicio de sesión único de aplicaciones SaaS y local de aplicaciones web. Lea hello [lista de compatibilidad de federación de Active Directory de Azure: proveedores de identidades de terceros que pueden ser utilizado tooimplement inicio de sesión único](https://msdn.microsoft.com/library/azure/jj679342.aspx) artículo para obtener más información acerca de hello terceros SSO que se han probado por Microsoft. Esta función permite organización tooimplement una variedad de escenarios de B2B manteniendo el control de administración de identidades y accesos de Hola. Sin embargo, durante Hola B2B diseñar el proceso es el método de autenticación de Hola de toounderstand importante que se usará en socio de Hola y valida si este método es compatible con Azure. Actualmente, estos son los métodos compatibles con Azure AD:

* Lenguaje de marcado de aserción de seguridad (SAML)
* OAuth
* Kerberos
* Tokens
* Certificados

> [!NOTE]
> leer [protocolos de autenticación de Azure Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow más detalles sobre cada protocolo y sus capacidades de Azure.
>
>

Utilizando el soporte de hello Azure AD, empresarial móvil, las aplicaciones pueden usar Hola mismo fácil servicios móviles autenticación experiencia tooallow empleados toosign en sus aplicaciones móviles con sus credenciales corporativas de Active Directory. Con esta característica es compatible con Azure AD como proveedor de identidades en servicios móviles junto con hello otros proveedores de identidad ya admitimos (que incluyen Microsoft Accounts, Id. de Facebook, Id. de Google y Twitter Id.). Si Hola aplicaciones usa Hola credencial del usuario situado en AD DS la compañía de hello en local, acceso de Hola de socios comerciales y los usuarios de una nube de hello debe ser transparente. Puede administrar del usuario las aplicaciones web de too(cloud-based) de control de acceso condicional, API web, Microsoft servicios en la nube, las aplicaciones de SaaS parte 3ª y aplicaciones cliente (móvil) nativo y tienen ventajas de Hola de seguridad, auditoría, reporting en un único Coloque. Sin embargo, es recomendable toovalidate esto en un entorno de no producción o con una cantidad limitada de usuarios.

> [!TIP]
> es importante toomention que Azure AD no tiene directivas de grupo ya tiene AD DS. En la directiva de tooenforce de orden para los dispositivos, necesita una solución de administración de dispositivos móviles como [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Una vez que se autentica el usuario de hello mediante Azure AD, es importante tendrá a nivel de Hola de tooevaluate de acceso del usuario de Hola. Hello nivel de acceso que Hola usuario tendrá sobre un recurso puede variar, mientras Azure AD puede agregar una capa de seguridad adicional por toosome controlar acceso a los recursos, también debe tener en cuenta que el propio recurso hello también puede tener su propia lista de control de acceso por separado, como control de acceso de Hola para archivos que se encuentran en un servidor de archivos. Hola siguiente ilustración resume los niveles Hola de control de acceso que puede haber en un escenario híbrido:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Cada interacción en el diagrama de hello mostrada en la figura X representa un escenario de control de acceso que puede estar cubierto por Azure AD. A continuación encontrará una descripción de cada escenario:

1. Tooapplications de acceso condicional que están hospedados en local: puede usar los dispositivos registrados con directivas de acceso para las aplicaciones que están configuradas toouse AD FS con Windows Server 2012 R2. Para obtener más información sobre cómo configurar el acceso condicional localmente, consulte [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-conditional-access.md).

2. Control de acceso toohello portal de Azure: Azure también le permite toohello portal de acceso de control mediante el control de acceso basado en roles (RBAC)). Este método permite la cantidad de hello empresa toorestrict Hola de operaciones que puede realizar un usuario individual en hello portal de Azure. Mediante RBAC toocontrol acceso toohello portal, los administradores de TI puede delegar el acceso mediante el uso de hello siguiendo métodos de administración de acceso:

* Asignación de roles basado en grupos: puede asignar acceso tooAzure AD grupos que se pueden sincronizar desde su Active Directory local. Esto le permite tooleverage hello las inversiones existentes que su organización ha realizado en las herramientas y los procesos de administración de grupos. También puede utilizar la característica de administración de grupos delegados Hola de Azure AD Premium.
* Aproveche integrada en roles de Azure: puede utilizar los tres roles: tooensure propietario, Colaborador y lector, que los usuarios y grupos tienen permiso toodo sólo hello las tareas que necesitan toodo sus trabajos.
* Acceso granular tooresources: puede asignar toousers de roles y grupos para una suscripción determinada, grupo de recursos o un recurso de Azure individual como un sitio Web o una base de datos. De esta manera, puede asegurarse de que los usuarios tengan acceso a los recursos hello tooall que necesitan y no tooresources de acceso que no es necesario toomanage.

> [!NOTE]
> Si está creando aplicaciones y desea que el control de acceso de hello toocustomize para ellos, también es posible toouse Roles de aplicación de Azure AD para la autorización. Revise este [ejemplo WebApp-RoleClaims-DotNet](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) acerca de cómo toobuild su aplicación toouse esta capacidad.
>
>

3. Acceso condicional para aplicaciones de Office 365 con Microsoft Intune: los administradores de TI pueden aprovisionar acceso condicional dispositivo directivas toosecure los recursos corporativos, mientras que en hello mismo tiempo permitir los trabajadores de información en hello tooaccess de dispositivos compatibles servicios. Para obtener más información, vea [Directivas de dispositivos de acceso condicional para servicios de Office 365](active-directory-conditional-access-device-policies.md).

4. Acceso condicional para aplicaciones de Saas: [esta característica](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) permite tooconfigure reglas de acceso de autenticación multifactor por aplicación y Hola capacidad tooblock acceso a los usuarios no en una red de confianza. Puede aplicar Hola la autenticación multifactor reglas tooall a los usuarios que se asignan toohello aplicación, o solo para los usuarios dentro de los grupos de seguridad especificados. Los usuarios pueden excluirse del requisito de la autenticación multifactor de hello si tienen acceso aplicación hello desde una dirección IP que interior en Hola de red de la organización.

Puesto que las opciones de hello para el control de acceso usan un enfoque multicapa, comparación entre esas opciones no son aplicables para esta tarea. Asegúrese de que se aprovechan todas las opciones disponibles para cada escenario que requiere acceso a los toocontrol tooyour recursos.

## <a name="define-incident-response-options"></a>Definición de las opciones de respuesta ante incidentes
Azure AD puede ayudar a TI tooidentity posible riesgos de seguridad en el entorno de hello mediante la supervisión de actividad del usuario, el departamento de TI puede aprovechan el acceso de Azure AD y capacidad toogain visibilidad Hola integridad y la seguridad del directorio de su organización de los informes de uso. Con esta información, un administrador de TI puede determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.  [Suscripción a Azure AD Premium](active-directory-get-started-premium.md) tiene un conjunto de informes de seguridad que puede permitir a TI tooobtain esta información. [informes de Azure AD](active-directory-view-access-usage-reports.md) se clasifican como se muestra a continuación:

* **Informes de anomalías**: contienen eventos que encontramos toobe anómalos de inicio de sesión. Nuestro objetivo es toomake, tanto de dicha actividad y le permiten toobe capaz toomake una decisión sobre si un evento es sospechoso.
* **Informe de aplicaciones integradas**: proporciona información sobre cómo se usan en la organización las aplicaciones en la nube. Azure Active Directory ofrece integración con miles de aplicaciones en la nube.
* **Informes de errores**: indican errores que pueden surgir al aprovisionar las aplicaciones de tooexternal de cuentas.
* **Informes específicos del usuario**: muestran los datos de actividad de dispositivo o de inicio de sesión de un usuario concreto.
* **Registros de actividad**: contienen un registro de todos los eventos auditados en hello últimas 24 horas, los últimos 7 días o 30 días, así como cambios de la actividad de grupo y la actividad de registro y restablecimiento de contraseña del último.

> [!TIP]
> Otro informe que también puede ayudar a Hola trabajando en un caso de equipo de respuesta a incidentes es hello [usuario con credenciales perdidas](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) informes.  Este informe muestra las coincidencias entre la lista de credenciales perdidas y su inquilino.
>
>

Otros importantes informes integrados en Azure AD que pueden usarse durante la investigación de la respuesta ante un incidentes son:

* **Actividad de restablecimiento de contraseña**: proporcionar información sobre cómo restablecer la contraseña se usa activamente en la organización de Hola Hola, administrador.
* **Actividad de registro de restablecimiento de contraseña**: proporciona información sobre los usuarios que registraron sus métodos para restablecer la contraseña y los métodos que seleccionados.
* **Actividades del grupo**: proporciona un historial de cambios toohello grupo (por ejemplo: los usuarios agregan o quitan) que se iniciaron en hello Panel de acceso.

Además toohello core funcionalidad de informes disponible en Azure AD Premium también se puede aprovechar durante un proceso de investigación de respuesta a incidentes, departamento de TI puede aprovechar la información de informe de auditoría tooobtain como:

* Cambios en la pertenencia al rol (por ejemplo: usuario agrega el rol de administrador de tooGlobal)
* Actualizaciones de credenciales (por ejemplo, cambios de contraseña)
* Administración de dominios (por ejemplo, comprobar un dominio personalizado o eliminar un dominio)
* Adición o eliminación de aplicaciones
* Administración de usuarios (por ejemplo, agregar, eliminar o actualizar un usuario)
* Adición o eliminación de licencias

Dado que las opciones de hello para la respuesta a incidentes usan un enfoque multicapa, comparación entre esas opciones no son aplicables para esta tarea. Asegúrese de que se aprovechan todas las opciones disponibles para cada escenario que requiere la funcionalidad de informes de Azure AD toouse como parte del proceso de respuesta a incidentes de su empresa.

## <a name="next-steps"></a>Pasos siguientes
[Determinación de las tareas de administración de identidades híbridas](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)
