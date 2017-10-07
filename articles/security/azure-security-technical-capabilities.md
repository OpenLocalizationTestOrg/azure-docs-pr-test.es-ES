---
title: "las funcionalidades técnicas de seguridad aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de los servicios informáticos en la nube que incluyen una amplia selección de instancias de proceso y servicios que se pueden escalar arriba y abajo automáticamente toomeet hello las necesidades de su aplicación o enterprise."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Funcionalidades técnicas de seguridad de Azure

tooassist actuales y potenciales clientes Azure comprender y utilizar Hola varias funciones relacionadas con la seguridad está disponibles en y que lo rodea Hola plataforma Azure, Microsoft ha desarrollado una serie de notas del producto, información general de seguridad, los procedimientos recomendados, y Listas de comprobación. temas de Hello en cuanto a la amplitud y la profundidad de intervalo y se actualizan periódicamente. Este documento es parte de esa serie como se resume en la siguiente sección abstracta Hola. Se puede encontrar más información sobre esta serie de seguridad de Azure en (URL).

## <a name="azure-platform"></a>Plataforma Azure

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) es una plataforma en la nube compuesta de servicios de infraestructura y aplicaciones, con servicios de datos y análisis avanzado integrados, y herramientas y servicios para desarrolladores, que se hospeda dentro de los centros de datos de la nube pública de Microsoft. Los clientes usar Azure para muchos escenarios, desde el proceso, red y almacenamiento, toomobile y web app servicios básicos, escenarios de nube toofull como Internet de las cosas y capacidades diferentes y pueden utilizar con las tecnologías de código abierto e implementarse como híbrida en la nube u hospedado en centros de datos de un cliente. Azure proporciona tecnología de nube como bloques de creación toohelp empresas ahorrar costos, innovación rápidamente y administración sistemas de forma proactiva. Al compilar en, o migrar proveedor de nube de tooa de activos de TI, está confiando en tooprotect de capacidades de la organización sus aplicaciones y datos con los servicios de Hola y controles de Hola que proporcionan una seguridad de hello toomanage de sus activos en la nube.

Microsoft Azure es Hola solo informático proveedor de nube que ofrece una plataforma de aplicaciones seguras, coherente y la infraestructura como-servicio para los equipos toowork dentro de sus conocimientos adicionales en la nube diferentes y niveles de complejidad del proyecto, con datos integrados servicios y los análisis que descubran inteligencia de datos donde existe, a través de Microsoft y plataformas de terceros, abren marcos de trabajo y las herramientas, proporcionando alternativas para la integración en la nube con local también implementar servicios de nube de Azure en centros de datos locales. Como parte del programa Hola nube de confianza de Microsoft, los clientes confían en Azure seguridad líderes del sector, confiabilidad, cumplimiento de normas, privacidad y red amplia de Hola de personas, socios y procesos toosupport organizaciones en la nube de Hola.

Con Microsoft Azure, puede:

- Acelerar la innovación con nube Hola.

- Impulsar aplicaciones y decisiones empresariales con información.

- Compilar con libertad e implementar en cualquier parte.

- Proteger su negocio.

## <a name="scope"></a>Scope

punto focal de Hola de estas notas del producto se refiere a las características de seguridad y funcionalidad que admite componentes de núcleo de Microsoft Azure, es decir, [almacenamiento de Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-introduction), [bases de datos de SQL de Microsoft Azure](https://docs.microsoft.com/azure/sql-database/), [Modelo de máquina virtual de Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/  ), herramientas de Hola y de infraestructura que administrar todo. Estas notas del producto se centran en Microsoft Azure funcionalidades técnicas disponible tooyou como clientes toofulfil su rol en la protección de seguridad de Hola y privacidad de sus datos.

importancia de Hola de descripción de este modelo de responsabilidad compartida es esencial para los clientes que se van a mover toohello en la nube. Proveedores de nube ofrecen considerables ventajas para los esfuerzos de seguridad y cumplimiento de normas, pero las siguientes ventajas no exime al cliente hello protejan sus usuarios, aplicaciones y ofertas de servicio.

Para las soluciones de IaaS, cliente hello es responsable o tiene una responsabilidad compartida para poder proteger y administrar el sistema operativo de hello, configuración de red, las aplicaciones, identidad, los clientes y datos.  Compilación soluciones de PaaS en las implementaciones de IaaS, sigue siendo responsable de cliente Hola o tiene una responsabilidad compartida para poder proteger y administrar aplicaciones, identidad, los clientes y datos. Para las soluciones de SaaS, Nonetheless, cliente hello continúa toobe responsable. Debe asegurarse de que se clasifican los datos correctamente y que comparten un toomanage responsabilidad sus usuarios y dispositivos de extremo.

Este documento no proporciona cobertura detallada de cualquiera de hello relacionados con los componentes de la plataforma de Microsoft Azure como sitios Web de Azure, Azure Active Directory, HDInsight, servicios multimedia y otros servicios que se disponen en capa encima del componentes principales de Hola. Aunque se proporciona un nivel mínimo de información general, se da por supuesto que los lectores están familiarizados con los conceptos básicos de Azure, tal y como se describen en otras referencias proporcionadas por Microsoft y que se incluyen en los vínculos que se indican en estas notas del producto.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Responsabilidad de usuario (cliente) de seguridad disponibles las funcionalidades técnicas toofulfil - panorama general

Microsoft Azure proporciona servicios que pueden ayudar a los clientes satisfagan necesidades de cumplimiento de normas, la privacidad y la seguridad Hola. Hola siguiente le ayudará a comprender varios servicios de Azure disponibles para los usuarios toobuild una infraestructura de aplicación seguros y conformes basan en estándares del sector de imagen.

![Funcionalidades técnicas de seguridad disponibles. Panorama general](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Administración y control de identidades y del acceso de usuarios (Protección)

Azure le ayuda a proteger información laboral y personal habilitando se toomanage identidades de usuario y las credenciales y controlar el acceso.

### <a name="azure-active-directory"></a>Azure Active Directory

Extensión identity and access management soluciones ayuda de Microsoft TI proteger tooapplications de acceso y recursos a través del centro de datos corporativo hello y en la nube de Hola, habilitación de niveles adicionales de validación, como la autenticación multifactor y condicional directivas de acceso. La supervisión de actividades sospechosas mediante auditorías, alertas e informes de seguridad avanzados contribuye a minimizar los posibles problemas de seguridad. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) proporciona toothousands de inicio de sesión único de acceso tooweb aplicaciones se ejecutan de forma local y en la nube (SaaS).

Ventajas de seguridad de Azure Active Directory (AD) incluyen la capacidad de hello:

- Crear y administrar una identidad única para cada usuario en toda la empresa híbrida, lo que mantiene los usuarios, grupos y dispositivos sincronizados.

- Proporcionar acceso de inicio de sesión único en aplicaciones de tooyour incluidos miles de aplicaciones de SaaS preintegradas.

- Habilitar la seguridad del acceso de las aplicaciones mediante la aplicación de Multi-Factor Authentication basado en reglas para las aplicaciones locales y en la nube.

- Aprovisionamiento de acceso remoto seguro tooon local web aplicaciones a través de Proxy de aplicación de Azure AD.

El [portal de Azure Active Directory](http://aad.portal.azure.com/) está disponible como parte de Azure Portal. En este panel, puede obtener una visión general del estado de Hola de su organización y profundizar fácilmente en administración de directorio de hello, usuarios o acceso a la aplicación.

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Las siguientes son las principales funcionalidades de administración de identidades de Azure:

- Inicio de sesión único

- Multi-Factor Authentication

- Supervisión de seguridad, alertas e informes basados en aprendizaje automático

- Administración de identidades y acceso de consumidores

- Registro de dispositivos

- Privileged Identity Management

- Protección de identidad

#### <a name="single-sign-on"></a>Inicio de sesión único

[Inicio de sesión único (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) significa ser capaz de tooaccess todas las aplicaciones de Hola y recursos que necesita toodo business, debe iniciar sesión en una sola vez usando una cuenta de usuario único. Una vez iniciado sesión, puede tener acceso a todas las aplicaciones de Hola que necesita sin necesidad de ser necesario tooauthenticate (por ejemplo, escriba una contraseña) una segunda vez.

Muchas organizaciones confían en el modelo de software como servicio (SaaS), como Office 365, Box y Salesforce para la productividad del usuario final. Históricamente, tooindividually necesita el personal de TI crear y actualizar cuentas de usuario en cada aplicación SaaS, y los usuarios tenían tooremember una contraseña para cada aplicación SaaS.

[Azure AD amplía en local de Active Directory en la nube de hello](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), habilitar toouse a los usuarios de su organización principal cuenta toonot solo inicio de sesión tootheir dispositivos Unidos a dominio y recursos de la empresa, pero también todos hello web y aplicaciones de SaaS se necesita para realizar su trabajo.

No solo a los usuarios no tiene toomanage varios conjuntos de nombres de usuario y contraseñas, acceso a la aplicación puede ser desaprovisionados por completo o aprovisionamiento automáticamente en función de grupos de la organización y su estado como un empleado. [Azure AD presenta los controles de regulación de acceso y seguridad](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) que le permiten toocentrally administrar el acceso de los usuarios en aplicaciones de SaaS.

#### <a name="multi-factor-authentication"></a>Multi-Factor Authentication

[Azure la autenticación multifactor (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) es un método de autenticación que requiere el uso de Hola de más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones. [MFA ayuda a proteger](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) acceder a toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona autenticación sólida mediante una gran variedad de opciones de verificación, como llamadas telefónicas, mensajes de texto, notificaciones de aplicaciones móviles, códigos de verificación y tokens OAuth de terceros.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Supervisión de seguridad, alertas e informes basados en aprendizaje automático

La supervisión y las alertas de seguridad, así como los informes basados en el aprendizaje automático que identifican patrones de acceso incoherentes, puede ayudarle a proteger su negocio. Puede usar el acceso de Active Directory de Azure y visibilidad de toogain de informes de uso de integridad de Hola y seguridad del directorio de su organización. Con esta información, administradores de directorios pueden determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.

Hola portal de Azure clásico o a través de [portal de Azure Active directory](http://aad.portal.azure.com/), [informes](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) se clasifican en hello siguientes maneras:

- Informes de anomalías: contienen eventos que encontramos toobe anómalos de inicio de sesión. Nuestro objetivo es toomake, tanto de dicha actividad y le permiten toobe toodecide capaz de determinar si un evento es sospechoso.

- Informes de aplicaciones integradas: proporcionan información sobre cómo se usan en su organización aplicaciones en la nube. Azure Active Directory ofrece integración con miles de aplicaciones en la nube.

- Informes de errores: indican errores que pueden surgir al aprovisionar las aplicaciones de tooexternal de cuentas.

- Informes específicos del usuario: muestran los datos de actividad de dispositivo o de inicio de sesión de un usuario concreto.

- Registros de actividad: contienen un registro de todos los eventos auditados en hello últimas 24 horas, los últimos 7 días, o últimos 30 días y cambios de la actividad de grupo y la actividad de registro y restablecimiento de contraseña.

#### <a name="consumer-identity-and-access-management"></a>Administración de identidades y acceso de consumidores

[Azure B2C Directory Active](https://azure.microsoft.com/services/active-directory-b2c/) es un servicio de administración de identidades globales, y alta disponibilidad para las aplicaciones orientadas al consumidor que escala toohundreds de millones de identidades. Se puede integrar en plataformas móviles y web. Los consumidores pueden iniciar sesión tooall sus aplicaciones a través de experiencias personalizables mediante sus cuentas sociales existentes o crear nuevas credenciales.

Hola pasado, los desarrolladores de aplicaciones que deseaban demasiado[registre e inicie sesión en los consumidores](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) en sus aplicaciones habría escribe su propio código. Y ha utilizado las contraseñas y nombres de usuario de toostore de bases de datos o sistemas de local. Azure B2C de directorio Active ofrece una administración de identidades consumidor de mejor manera toointegrate en las aplicaciones con ayuda de Hola de una plataforma segura y basada en estándares y un conjunto grande de directivas extensibles de su organización.

El uso de Azure Active Directory B2C permite a los consumidores registrarse en las aplicaciones con sus cuentas de redes sociales existentes (Facebook, Google, Amazon, LinkedIn) o creando nuevas credenciales (dirección de correo electrónico y contraseña o nombre de usuario y contraseña).

Registro de dispositivos

[Registro de dispositivos de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) es Hola base basado en dispositivos [acceso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) escenarios. Cuando se registra un dispositivo, registro de dispositivo de Azure Active Directory proporciona dispositivo Hola con una identidad que sea el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión. dispositivo de Hello autenticado y los atributos de hello de dispositivo de hello, se pueden tooenforce usa directivas de acceso condicional para las aplicaciones que se hospedan en la nube de Hola y local.

Cuando se combina con un [administración de dispositivos móviles (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) solución como Intune, los atributos de dispositivo de hello en Azure Active Directory se actualizan con información adicional sobre el dispositivo de Hola. Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas.

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) le permite administrar, controlar y supervisar las identidades con privilegios y obtener acceso a tooresources en Azure AD, así como otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.

En ocasiones, los usuarios necesitan toocarry operaciones con privilegios en recursos de Azure u Office 365 u otras aplicaciones de SaaS. Esto suele significar que las organizaciones tienen toogive tener acceso ellas con privilegios permanentes en Azure AD. Esto representa un riesgo de seguridad creciente para los recursos hospedados en la nube porque las organizaciones no pueden supervisar suficientemente qué hacen esos usuarios con sus privilegios administrativos. Además, si se pone en peligro una cuenta de usuario que tiene acceso con privilegios, esta situación podría afectar a su seguridad en la nube global. Identity Management de Azure AD privilegios ayuda a tooresolve este riesgo.

Azure AD Privileged Identity Management le permite:

- Ver qué usuarios son administradores de Azure AD

- Habilitar a petición "justo a tiempo" acceso administrativo tooMicrosoft Online Services, como Office 365 e Intune

- Obtener informes sobre el historial de acceso de administrador y sobre los cambios en las asignaciones de administrador

- Obtener alertas sobre los roles con privilegios de acceso tooa

#### <a name="identity-protection"></a>Protección de identidad

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) es un servicio de seguridad que proporciona una vista consolidada de eventos de riesgo y puntos vulnerables que afectan a las identidades de su organización. Identity Protection usa las funcionalidades de detección de anomalías existentes de Azure Active Directory (disponibles mediante informes de actividad anómala de Azure AD) e introduce nuevos tipos de eventos de riesgo que pueden detectar anomalías en tiempo real.

## <a name="secured-resource-access-in-azure"></a>Acceso protegido a los recursos de Azure

El control de acceso de Azure se inicia desde una perspectiva de facturación. propietario de Hola de una cuenta de Azure, tiene acceso visitando hello [centro de cuentas de Azure](https://account.windowsazure.com/subscriptions), es hello Administrador de cuenta (AA). Las suscripciones son un contenedor para la facturación, pero también actúan como límite de seguridad: cada suscripción tiene un administrador de servicios (SA) que puede agregar, quitar y modificar recursos de Azure en esa suscripción mediante el uso de hello [portal de Azure clásico](https://manage.windowsazure.com/). Hola predeterminado SA de una suscripción nueva es Hola AA, pero Hola AA puede cambiar el SA Hola Hola centro de cuentas de Azure.

![Acceso protegido a los recursos de Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Las suscripciones también tienen una asociación con un directorio. directorio de Hello define un conjunto de usuarios. Estos pueden ser usuarios del trabajo de Hola o la escuela que creó el directorio de hello, o pueden ser usuarios externos (es decir, Accounts de Microsoft). Las suscripciones son accesibles mediante un subconjunto de esos usuarios del directorio que se ha asignado como administrador de servicios (SA) o Coadministrador (CA); Hello solo excepción es que, por razones heredadas, Accounts de Microsoft (anteriormente Windows Live ID) pueden asignarse como SA o CA sin estar presentes en el directorio de Hola.

Las empresas orientada a servicios de seguridad deben centrarse en conceder a los empleados que necesitan los permisos exactos Hola. Demasiados permisos pueden exponer un tooattackers de cuenta. Si se conceden muy pocos, los empleados no podrán realizar su trabajo de manera eficaz. Gracias al [control de acceso basado en roles (RBAC) de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), podrá abordar este problema, ya que es posible realizar una administración avanzada del acceso para Azure.

![Acceso protegido a los recursos ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

Usar RBAC, puede separar los derechos en el equipo y conceder solo Hola mucha toousers de acceso que necesitan tooperform sus trabajos. En lugar de proporcionar a todos los empleados permisos no restringidos en los recursos o la suscripción de Azure, puede permitir solo determinadas acciones. Por ejemplo, un empleado de uso RBAC toolet administrar máquinas virtuales en una suscripción, mientras que otro puede administrar SQL bases de datos dentro de Hola misma suscripción.

![Acceso protegido a los recursos de Azure (RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Cifrado y seguridad de datos en Azure (protección)

Uno de toodata protección de claves de hello en la nube de hello es teniendo en cuenta posibles estados de hello en el que pueden producirse los datos y qué controles están disponibles para ese estado. Para el cifrado y seguridad de datos de Azure siguientes procedimientos recomendados de hello existiría Hola siguiendo los Estados de los datos.

- En reposo: esto incluye información sobre todos los objetos de almacenamiento, los contenedores y los tipos que existen de forma estática en medios físicos, ya sean discos magnéticos u ópticos.

- En tránsito: Cuando se transfieren datos entre componentes, ubicaciones o programas, como a través de la red hello, a través de un bus de servicio (de local toocloud y viceversa, incluidas las conexiones híbridas como ExpressRoute), o durante una entrada/salida proceso, se piensa en él como en movimiento.

### <a name="encryption--rest"></a>Cifrado en reposo

Cifrado en reposo de siguientes Hola tooachieve:

Admitir al menos uno de hello recomendada detallados en hello después de tabla tooencrypt datos de modelos de cifrado.

| Modelos de cifrado |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Cifrado de servidor | Cifrado de servidor | Cifrado de servidor | Cifrado de cliente
| Cifrado del lado del servidor mediante claves administradas del servicio | Cifrado del lado del servidor mediante claves administradas por el cliente en Azure Key Vault | Cifrado del lado del servidor mediante claves locales administradas por el cliente |
| • Proveedores de recursos azure realizar operaciones de cifrado y descifrado de Hola <br> • Microsoft administra las claves de Hola <br>• Funcionalidad de nube completa | • Proveedores de recursos azure realizar operaciones de cifrado y descifrado de Hola<br>• El cliente controla las claves mediante Azure Key Vault<br>• Funcionalidad de nube completa | • Proveedores de recursos azure realizar operaciones de cifrado y descifrado de Hola <br>• El cliente controla claves local <br> • Funcionalidad de nube completa| • Los servicios de Azure no pueden ver los datos descifrados <br>• Los clientes almacenan las claves en ubicaciones locales (o en otras ubicaciones protegidas). Las claves no son servicios tooAzure disponibles <br>• Funcionalidad de nube reducida|

### <a name="enabling-encryption-at-rest"></a>Habilitación del cifrado de datos en reposo

**Identificación de todas las ubicaciones de los almacenes de datos**

objetivo de Hola de cifrado en reposo es tooencrypt todos los datos. Al hacerlo, elimina la posibilidad de Hola de que falten datos importantes o todas las ubicaciones persistentes. Enumerar todos los datos almacenados por la aplicación. 

> [!Note] 
> No solo "application data" o "PII', pero los datos relacionados con tooapplication incluido cuenta metadatos (asignaciones de suscripción, información de contrato, PII).

Tenga en cuenta lo que almacena usa toostore datos. Por ejemplo:

- Almacenamiento externo (por ejemplo, SQL Azure, Document DB, HDInsights, Data Lake, etc.)

- Almacenamiento temporal (cualquier caché local que incluye datos de inquilino)

- Caché en memoria (puede poner en archivo de paginación de Hola.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Aprovechar cifrado existente de hello en el soporte técnico de rest de Azure

Para cada almacén que use, aprovechar Hola existente cifrado en el soporte técnico de Rest.

- Azure Storage: consulte [Cifrado del servicio Azure Storage para datos en reposo](https://docs.microsoft.com/azure/storage/storage-service-encryption),

- SQL Azure: consulte [Cifrado de datos transparente (TDE), SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)

- Almacenamiento en máquina virtual y disco local ([Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

Para el almacenamiento en máquina virtual y disco local use Azure Disk Encryption allí donde sea compatible:

IaaS

Deben usar los servicios con las máquinas virtuales de IaaS (Windows o Linux) [cifrado del disco de Azure](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) volúmenes tooencrypt que contiene los datos del cliente.

PaaS v2

Servicios que se ejecutan en PaaS v2 Service Fabric utilizar cifrado de disco de Azure para el conjunto de escala de máquinas virtuales [VMSS] tooencrypt sus máquinas virtuales v2 de PaaS.

PaaS v1

Actualmente, no se admite Azure Disk Encryption en PaaS v1. Por lo tanto, debe utilizar el nivel de aplicación tooencrypt de cifrado de datos en reposo almacenados.  Esto incluye, aunque sin limitarse a ellos, los datos de la aplicación, los archivos temporales, los registros y volcados de memoria.

La mayoría de servicios debe tratar de cifrado de hello tooleverage de un proveedor de recursos de almacenamiento. Algunos servicios tienen toodo explícita cifrado, por ejemplo, conservar ninguno material de clave (certificados, raíz / maestro de claves) deben estar almacenados en el almacén de claves.

Si se admite el cifrado de lado de servicio con las claves administradas por el cliente es necesario toobe forma hello tooget Hola para clave de cliente toous. Hola compatible y recomienda toodo de manera que mediante la integración con el almacén de claves de Azure (claves). En este caso, los clientes pueden agregar y administrar sus claves en Azure Key Vault. Un cliente puede obtener información sobre cómo toouse claves a través de [Introducción al almacén de claves](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate al almacén de claves de Azure, debe agregar código toorequest una clave de claves cuando sea necesario para el descifrado.

- Vea [almacén de claves de Azure: paso a paso](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) para obtener información acerca de cómo toointegrate con claves.

Si se admiten claves administradas por el cliente, debe tooprovide experiencia del usuario para hello cliente toospecify qué toouse el almacén de claves (o URI del almacén de clave).

Como el cifrado en reposo implica cifrado Hola de datos host, infraestructura e inquilino, pérdida de Hola de claves de hello debido a error toosystem o actividad malintencionada puede significar se pierden todos los datos de hello cifrado. Por lo tanto, es fundamental que el cifrado en la solución de Rest tiene una recuperación ante desastres integral caso toosystem resistente errores y actividades malintencionadas.

Servicios que implementan el cifrado en reposo suelen ser las claves de cifrado de toohello siendo vulnerable o ha dejado de datos sin cifrar en la unidad de host de hello (por ejemplo, en el archivo de paginación de Hola de sistema operativo del host Hola.) Por lo tanto, deben asegurarse de servicios se cifra el volumen de host de Hola para sus servicios. toofacilitate este equipo proceso ha habilitado la implementación de Hola de cifrado de Host, que utiliza [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP y extensiones toohello DCM servicio y agente tooencrypt Hola volumen de host.

La mayoría de los servicios se implementa en máquinas virtuales estándar de Azure. Estos servicios deben realizar el [cifrado del host](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) automáticamente cuando Compute lo habilite. Para aquellos servicios que se ejecutan en clústeres administrados de Compute, el cifrado del host se habilita de forma automática cuando se implementa Windows Server 2016.

### <a name="encryption-in-transit"></a>Cifrado en tránsito

Proteger los datos en tránsito debe ser una parte esencial de su estrategia de protección de datos. Puesto que se mueven datos y hacia atrás desde varias ubicaciones, recomendación general de Hola es que siempre que usan los datos de tooexchange de protocolos SSL/TLS en diferentes ubicaciones. En algunas circunstancias, puede que desee canal de tooisolate Hola toda comunicación entre el local y la nube infraestructura mediante el uso de una red privada virtual (VPN).

Para los datos que se desplazan entre la infraestructura local y Azure, debe plantearse usar medidas de seguridad apropiadas, como HTTPS o VPN.

Las organizaciones que necesitan tener acceso toosecure desde varias estaciones de trabajo locales encuentra tooAzure, usar [Azure VPN de sitio a sitio](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Para las organizaciones que necesitan acceso de toosecure desde una estación de trabajo encuentra tooAzure local, use [Point-to-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Los conjuntos de datos más grandes se pueden mover por medio de un vínculo WAN dedicado de alta velocidad como [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si elige toouse ExpressRoute, también puede cifrar los datos de hello en el uso de nivel de aplicación de hello [SSL/TLS](https://support.microsoft.com/kb/257591) u otros protocolos para conseguir una protección adicional.

Si interactúa con el almacenamiento de Azure a través de hello Portal de Azure, todas las transacciones se producen a través de HTTPS. [API de REST de almacenamiento](https://msdn.microsoft.com/library/azure/dd179355.aspx) a través de HTTPS, también puede ser usado toointeract con [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) y [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/).

Las organizaciones que no cumplan tooprotect datos en tránsito sean más susceptibles de [man-in-the-middle ataques](https://technet.microsoft.com/library/gg195821.aspx), [interceptaciones](https://technet.microsoft.com/library/gg195641.aspx)y secuestro de sesión. Estos ataques pueden ser el primer paso de Hola para obtener acceso a los datos tooconfidential.

Se puede obtener más información acerca de la opción de VPN de Azure, lea el artículo de hello [planificación y diseño para la puerta de enlace VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Aplicación del cifrado de datos a nivel de archivos

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de las directivas de cifrado, identidad y autorización utiliza proteger los archivos y correo electrónico. Azure RMS funciona en varios dispositivos (teléfonos, tabletas y PC) y los protege tanto dentro como fuera de su organización. Esta capacidad es posible ya que Azure RMS agrega un nivel de protección que conserva los datos de hello, incluso cuando sale de los límites de su organización.

Cuando usas Azure RMS tooprotect los archivos, que usa la criptografía estándar del sector con el soporte completo de [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Al aprovechar Azure RMS para proteger los datos, tiene garantía de Hola Hola permanece con el archivo hello, incluso si es toostorage copiada que no está bajo control de Hola de TI, como un servicio de almacenamiento en la nube. Hello mismo ocurre con los archivos compartidos a través de correo electrónico, archivo hello está protegido como un mensaje de correo electrónico de tooan datos adjuntos, con instrucciones de cómo tooopen Hola protege datos adjuntos.
Al planear la adopción de Azure RMS, recomendamos siguiente de hello:

- Instalar hello [aplicación RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Esta aplicación se integra con las aplicaciones de Office con la instalación de un complemento de Office con el que los usuarios pueden proteger los archivos directamente y de forma sencilla.

- Configurar aplicaciones y servicios toosupport Azure RMS

- Cree [plantillas personalizadas](https://technet.microsoft.com/library/dn642472.aspx) que reflejen sus requisitos empresariales. Por ejemplo: una plantilla para los datos más delicados que se deba aplicar a todos los correos electrónicos de mayor confidencialidad.

Las organizaciones que están débiles en [clasificación de datos](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) y protección de archivos puede ser más susceptible de sufrir pérdida de toodata. Sin protección de archivo adecuados, las organizaciones no tooobtain capaz de información empresarial, supervisar para controlar el abuso además de evitar accesos malintencionados toofiles.

> [!Note]
> Se puede obtener más información acerca de Azure RMS, lea el artículo de hello [Introducción a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Protección de la aplicación (protección)
Aunque es responsable de proteger la infraestructura de Hola y la plataforma que se ejecuta la aplicación en Azure, es su responsabilidad toosecure su propia aplicación. En otras palabras, necesita toodevelop, implementar y administrar el contenido y el código de la aplicación de una manera segura. Sin esto, el código de aplicación o el contenido puede seguir siendo vulnerable toothreats.

### <a name="web-application-firewall-waf"></a>Firewall de aplicaciones web (WAF)
[Firewall de aplicaciones web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) es una característica de [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) que proporciona a las aplicaciones una protección centralizada contra vulnerabilidades de seguridad comunes.

Servidor de aplicaciones Web se basa en reglas de hello [conjuntos de reglas de núcleo OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 o 2.2.9. Las aplicaciones web son cada vez más los objetivos de ataques malintencionados que aprovechan vulnerabilidades comunes conocidas, como Comunes entre estas vulnerabilidades de seguridad son los ataques de inyección de SQL, scripting entre sitios ataques tooname algunos. Evitar estos ataques en el código de aplicación puede ser complicada y pueden requerir riguroso mantenimiento, supervisión en varias capas de la topología de la aplicación hello y aplicación de revisiones. Un servidor de seguridad de la aplicación web centralizada le ayuda a hacer mucho más fácil la administración de seguridad y ofrece una mejor seguridad a los administradores de tooapplication frente a amenazas o intrusiones. Una solución WAFS también puedan reaccionar de amenaza para la seguridad tooa más rápido por una vulnerabilidad conocida en una ubicación central en comparación con la protección de cada una de las aplicaciones web individuales de la aplicación de revisiones. Puertas de enlace de aplicaciones existentes pueden ser puerta de enlace de la aplicación de firewall habilitado de tooa convertido web aplicación fácilmente.

Algunos de hello web las vulnerabilidades más comunes que firewall de la aplicación web protege contra incluye:

- Protección contra la inyección de código SQL

- Protección contra scripts entre sitios

- Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos

- Protección contra infracciones del protocolo HTTP

- Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación

- Prevención contra bots, rastreadores y escáneres

- Detección de errores de configuración comunes en aplicaciones (es decir, Apache, IIS, etc.)

> [!Note]
> Para una lista más detallada de las reglas y los mecanismos de protección, consulte siguiente hello [principales de conjuntos de reglas](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure también ofrece varios toohelp fácil de usar características proteger el tráfico entrante y saliente de la aplicación. Azure también le ayuda a los clientes proteger el código de aplicación proporcionando externamente proporciona funcionalidad tooscan la aplicación web en busca de vulnerabilidades.

- [Proteger su aplicación web mediante diversos medios de autenticación y autorización](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Configurar la autenticación de Azure Active Directory en la aplicación](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Proteger el tráfico tooyour aplicación habilitando Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Forzar todo el tráfico entrante a través de la conexión HTTPS](http://microsoftazurewebsitescheatsheet.info/)

  - [Habilitar Seguridad de transporte estricto (HSTS)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Restringir el acceso tooyour aplicación mediante la dirección IP del cliente](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Restringir el acceso tooyour aplicación mediante el comportamiento del cliente: frecuencia de solicitud y simultaneidad](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Examinar el código de la aplicación web en búsqueda de vulnerabilidades mediante Tinfoil Security Scanning](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [Configurar la autenticación mutua de TLS toorequire certificados de cliente tooconnect tooyour web app](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Configurar un certificado de cliente para la conexión de uso de la aplicación toosecurely tooexternal recursos](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Quite las herramientas de tooavoid de encabezados de servidor estándar de huellas digitales de la aplicación](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Conectar de forma segura la aplicación con los recursos de una red privada mediante VPN de punto a sitio](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Conectar de forma segura la aplicación con los recursos de una red privada mediante conexiones híbridas](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure usa el servicio de aplicación Hola misma solución Antimalware que se usa servicios en la nube y máquinas virtuales. toolearn más información, consulte tooour [documentación Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Protección de la red (protección)
Microsoft Azure incluye una sólida toosupport de infraestructura de red de su aplicación y los requisitos de conectividad de servicio. Conectividad de red es posible entre los recursos ubicados en Azure, entre locales y recursos y tooand de hello Internet y Azure hospedado de Azure.

Hola [infraestructura de red de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permite toosecurely conectar tooeach de recursos de Azure con [redes virtuales (Vnet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Una red virtual es una representación de su propia red en la nube de Hola. Una red virtual es lógico de aislamiento de red dedicada tooyour suscripción de hello nube de Azure. Puede conectar redes locales de redes virtuales tooyour.

![Protección de la red (protección)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Si se necesita un control de acceso de nivel de red básica (basado en IP hello y dirección TCP o UDP protocolos), puede usar [grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Un grupo de seguridad de red (NSG) es un básico firewall de filtrado de paquetes con estado y permite toocontrol acceso tomando como base un [5-tupla](https://www.techopedia.com/definition/28190/5-tuple).

Las redes de Azure es compatible con comportamiento de enrutamiento de hello capacidad toocustomize hello para el tráfico de red en las redes virtuales de Azure. Para ello, puede configurar [rutas definidas por el usuario](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) en Azure.

[La tunelización forzada](https://www.petri.com/azure-forced-tunneling) es un mecanismo que puede utilizar tooensure que los servicios no están permitidas tooinitiate una toodevices de conexión en hello Internet.

Azure es compatible con dedicado de red de un vínculo WAN conectividad tooyour local y una red Virtual de Azure con [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). vínculo de Hello entre Azure y el sitio utiliza una conexión dedicada que no pasa por hello Internet pública. Si su aplicación de Azure se ejecuta en varios centros de datos, puede usar [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute solicitudes procedentes de usuarios cambien en todas las instancias de la aplicación hello. También es posible distribuir tooservices de tráfico que no se ejecutan en Azure si son accesibles desde Internet Hola.

## <a name="virtual-machine-security-protect"></a>Seguridad de máquina virtual (protección)

[Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/) permite implementar una amplia gama de soluciones informáticas con agilidad. Gracias a la compatibilidad con Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP y Azure BizTalk Services, puede implementar cualquier carga de trabajo y cualquier idioma en casi cualquier sistema operativo.

Con Azure, puede usar [software antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) de proveedores de seguridad, como Microsoft, Symantec, Trend Micro y Kaspersky tooprotect las máquinas virtuales desde archivos malintencionados, adware y otras amenazas.

Microsoft Antimalware para servicios en la nube y máquinas virtuales de Azure es una funcionalidad de protección en tiempo real que permite identificar y eliminar virus, spyware y otro software malintencionado. Microsoft Antimalware proporciona configurable genera una alerta cuando conoce tooinstall de intentos de software malintencionado o no deseado propio o ejecutarse en los sistemas de Azure.

[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) es una solución escalable que protege los datos de su aplicación sin necesidad de realizar ninguna inversión y afrontando unos costos operativos mínimos. Los errores de una aplicación pueden dañar los datos, y los errores humanos pueden crear errores en las aplicaciones. Con Copia de seguridad de Azure, las máquinas virtuales que ejecutan Windows y Linux están protegidas.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) ayuda a coordinar la replicación, la conmutación por error y la recuperación de aplicaciones y cargas de trabajo para que estén disponibles desde una ubicación secundaria si la ubicación principal deja de funcionar.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Garantía de cumplimiento normativo: Lista de comprobación de diligencia debida para Cloud Services (protección)

Microsoft desarrollada [Hola lista de comprobación de diligencia vencimiento de nube servicios](https://aka.ms/cloudchecklist.download) toohelp organizaciones tomar las debidas diligencia tal y como se tienen en cuenta una nube de toohello de movimiento. Proporciona una estructura de una organización de cualquier tamaño y tipo: privadas empresas y organizaciones del sector público, incluidas la administración pública en todos los niveles y las ONG: tooidentify su propio rendimiento, servicio, administración de datos y objetivos de gobernanza y requisitos. Esto les permite ofertas de hello toocompare de proveedores de servicios de nube diferente, formación en última instancia de base de Hola para un contrato de servicio de nube.

lista de comprobación de Hello proporciona un marco que alinea a la cláusula con un nuevo estándar internacional de contratos de servicio de nube, ISO/IEC 19086. Esta norma ofrece un conjunto unificado de consideraciones de toohelp de las organizaciones a tomar decisiones sobre la adopción de la nube y crear un terreno común para la comparación de ofertas de servicio de nube.

lista de comprobación de Hello promueve una nube de toohello exhaustivamente investigados movimiento, proporciona orientación estructurada y un enfoque coherente y repetible para elegir un proveedor de servicios de nube.

La adopción de la nube ya no es solo una decisión tecnológica. Como requisitos de la lista de comprobación describe todos los aspectos de una organización, sirven a tooconvene todas las claves internos-dirigentes: hello CIO y CISO, así como legal, el riesgo de profesionales de administración, la adquisición y el cumplimiento. Esto aumenta la eficiencia de Hola de proceso de toma de decisiones de Hola y decisiones de terreno en sonido razonamiento, lo que reduce la probabilidad de Hola de tooadoption obstáculos imprevistos.

Además, Hola lista de comprobación:

- Muestra temas de discusión de clave para encargados de tomar decisiones al principio de hello del proceso de adopción de hello en la nube.

- Admite las discusiones de negocio exhaustiva acerca de la normativa y objetivos de la organización de Hola para privacidad, la información personal identificable (PII) y la seguridad de los datos.

- Ayuda a las organizaciones a identificar posibles problemas que pudieran afectar a un proyecto en la nube.

- Proporciona un conjunto coherente de preguntas con hello mismos términos, definiciones, métricas y los resultados de cada proveedor, el proceso de hello toosimplify de la comparación de ofertas de proveedores de servicios de nube diferente.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Validación de la seguridad de la infraestructura y aplicaciones de Azure (detección)

[Seguridad operativa Azure](https://docs.microsoft.com/azure/security/azure-operational-security) hace referencia toohello servicios, los controles y características disponibles toousers para proteger sus datos, aplicaciones y otros activos de Microsoft Azure.

![validación de seguridad (detección)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Seguridad operativa de Azure se basa en un marco que incorpora el conocimiento de hello adquirido a través de una varias funciones que son único tooMicrosoft, incluidos Hola del ciclo de vida de desarrollo seguridad de Microsoft (SDL), Hola centro de respuesta de seguridad de Microsoft programa y conocimiento profundo del panorama de amenazas de ciberseguridad de Hola.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) es hello solución de administración de TI para la nube híbrida de Hola. Por sí solas o tooextend le ofrece la implementación existente de System Center, OMS Hola obtener la máxima flexibilidad y control para la administración basada en la nube de su infraestructura.

![Microsoft Operations Management Suite (OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Con OMS, puede administrar cualquier instancia en cualquier nube, incluidas las locales o de Azure, AWS, Windows Server, Linux, VMware y OpenStack, con un costo menor que las soluciones de la competencia. Creado para Hola a todos en la nube en primer lugar, OMS ofrece un nuevo toomanaging enfoque su empresa que la forma hello más rápido y más rentable toomeet nuevos negocios desafíos y adaptarse a nuevas cargas de trabajo, aplicaciones y entornos de nube.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) proporciona servicios de supervisión para OMS recopilando datos de los recursos administrados en un repositorio central. Estos datos podrían incluir eventos, datos de rendimiento o datos personalizados proporcionadas a través de la API de Hola. Una vez recopilados, datos de hello están disponibles para las alertas, el análisis y la exportación.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Este método permite tooconsolidate datos desde una variedad de orígenes, por lo que puede combinar datos de los servicios de Azure con el contenido existente en entorno local. Separa claramente también colección Hola de datos de Hola de acción de hello realizada en los datos para que todas las acciones están disponibles tooall tipos de datos.

### <a name="azure-security-center"></a>Azure Security Center

[Centro de seguridad de Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Hola de ayuda a evitar, detectar y responder toothreats con una mayor visibilidad de y control sobre la seguridad de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Centro de seguridad analiza el estado de seguridad de Hola de las recursos de Azure tooidentify vulnerabilidades de seguridad. Una lista de recomendaciones le guía a través del proceso de Hola de configuración de controles necesarios.

Algunos ejemplos son:

- Aprovisionamiento antimalware toohelp identificar y quitar software malintencionado

- Configuración de red seguridad reglas y grupos toocontrol tráfico tooVMs

- Aprovisionamiento de los firewalls de aplicación web toohelp defenderse contra los ataques que tienen como destino las aplicaciones web

- Implementación de actualizaciones del sistema que faltan.

- Direccionamiento de las configuraciones de sistema operativo que no coincide con hello recomienda líneas de base

Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de recursos de Azure, redes de Hola y soluciones de socios comerciales, como programas antimalware y firewalls. Cuando se detecten amenazas, se creará una alerta de seguridad. Como ejemplos se incluye la detección de:

- VM en peligro que se comunican con direcciones IP malintencionadas conocidas

- Malware avanzado detectado mediante la generación de informes de errores de Windows.

- Ataques de fuerza bruta contra VM

- Alertas de seguridad de programas antimalware y firewalls integrados

### <a name="azure-monitor"></a>Azure Monitor

[Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) proporciona punteros tooinformation en determinados tipos de recursos. Ofrece visualización, consulta, enrutamiento, alertas, escalado automático y automatización en datos de hello infraestructura de Azure (registro de actividad) y cada recurso de Azure individual (registros de diagnóstico).

Las aplicaciones de nube son complejas y tienen muchas partes móviles. La supervisión proporciona tooensure de datos que mantiene la aplicación y en ejecución en un estado correcto. También ayuda a toostave off posibles problemas o solucionar problemas más allá de los.

![Monitor de Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) Además, puede usar supervisión toogain profundo información sobre los datos acerca de la aplicación. Esa información puede ayudarle a rendimiento de la aplicación de tooimprove o mantenimiento o automatizar acciones que en caso contrario requerirían intervención manual.

La auditoría de la seguridad de la red es fundamental para detectar vulnerabilidades de red y asegurar el cumplimiento de la seguridad de TI y el modelo de gobierno reglamentario. Con la vista de grupo de seguridad, se puede recuperar las reglas del grupo de seguridad de red y seguridad Hola configurado, así como Hola reglas de seguridad eficaz. Con hello obtener lista de reglas que se aplican, se puede determinar una vulnerabilidad de la red de ss y puertos de Hola que están abiertos.

### <a name="network-watcher"></a>Network Watcher

[Monitor de red](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) es un servicio regional que le permite toomonitor y diagnosticar condiciones en un nivel de red en, a y desde Azure. Diagnóstico de red y herramientas de visualización disponibles con Monitor de red ayudan a comprender, diagnosticar y obtener red tooyour de visión en Azure. Este servicio incluye captura de paquetes, próximo salto, comprobación de flujo de IP, vista de grupos de seguridad y registros de flujo de NSG. Supervisión del nivel de escenario, proporciona una vista de tooend de final de los recursos de red en la supervisión de recursos de red de tooindividual de contraste.

### <a name="storage-analytics"></a>Análisis de almacenamiento

[Análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) puede almacenar métricas que incluyen datos de estadísticas y la capacidad de transacciones agregados acerca del servicio de almacenamiento de tooa de solicitudes. Las transacciones se notifican en nivel de operación Hola API, así como a nivel de servicio de almacenamiento de Hola y capacidad se notifica en el nivel de servicio de almacenamiento de Hola. Datos de métricas que pueden ser utilizados tooanalyze uso de servicios de almacenamiento, diagnosticar problemas con las solicitudes realizadas en el servicio de almacenamiento de Hola y el rendimiento de hello tooimprove de las aplicaciones que utilizan un servicio.

### <a name="application-insights"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) es un servicio de Application Performance Management (APM) extensible para desarrolladores web en varias plataformas. Usar toomonitor la aplicación web en directo. Se detectarán automáticamente las anomalías de rendimiento. Incluye análisis eficaces herramientas toohelp que diagnosticar problemas y toounderstand qué hacer un usuario con la aplicación. Se ha diseñado toohelp continuamente mejorar el rendimiento y facilidad de uso. Funciona para las aplicaciones en una amplia variedad de plataformas como. NET, Node.js y J2EE, hospedado en local o en la nube de Hola. Se integra con el proceso de devOps y tiene diversas herramientas de desarrollo de tooa de puntos de conexión.

Supervisa:

- **Tasas de solicitud, tiempos de respuesta y tasas de error** - Averigüe qué páginas que son las más conocidas, en qué momento del día y dónde están los usuarios. Vea qué páginas presentan mejor rendimiento. Si los tiempos de respuesta y las tasas de error aumentan cuando hay más solicitudes, quizás tiene un problema de recursos.

- **Tasas de dependencia, tiempos de respuesta y tasa de error** - Averigüe si los servicios externos le ralentizan.

- **Excepciones** : analizar Hola agregado las estadísticas, o seleccionar instancias concretas y profundizar en seguimiento de la pila de Hola y las solicitudes relacionadas. Se notifican tanto las excepciones de servidor como las de explorador.

- **Vistas de página y rendimiento de carga** - Notificados por los exploradores de los usuarios.

- **Llamadas AJAX desde páginas web**: Tasas, tiempos de respuesta y tasas de error.

- **Número de usuarios y sesiones**.

- **Contadores de rendimiento** de las máquinas de servidor de Windows o Linux, como CPU, memoria y uso de la red.

- **Diagnóstico de host** de Docker o Azure.

- **Registros de seguimiento de diagnóstico** de la aplicación - De esta forma puede correlacionar eventos de seguimiento con las solicitudes.

- **Eventos personalizados y las métricas** que es usted quien escribe en el código de cliente o servidor de hello, eventos de negocio de tootrack como elementos vendidos o juegos ganados.
infraestructura de Hola para su aplicación normalmente se compone de muchos componentes, puede ser una máquina virtual, cuenta de almacenamiento y red virtual, o una aplicación web, base de datos, servidor de base de datos y 3 servicios de terceros. Estos componentes no se ven como entidades independientes, sino como partes de una sola entidad relacionadas e interdependientes. Desea toodeploy, administrar y supervisar como un grupo. [El Administrador de recursos Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) permite toowork con recursos de hello en la solución como un grupo.

Puede implementar, actualizar o eliminar todos los recursos de hello para la solución en una única operación coordinada. Para realizar la implementación se usa una plantilla, que puede funcionar en distintos entornos, como producción, pruebas y ensayo. Administrador de recursos proporciona seguridad, auditoría y etiquetado características toohelp administrar sus recursos después de la implementación.

**ventajas de Hola de usar el Administrador de recursos**

Administrador de recursos ofrece varias ventajas:

- Puede implementar, administrar y supervisar todos los recursos de hello para la solución como un grupo, en lugar de controlar estos recursos individualmente.

- Repetidamente, puede implementar la solución a lo largo del ciclo de vida de desarrollo de Hola y estar seguro de que los recursos se implementan en un estado coherente.

- Puede administrar la infraestructura mediante plantillas declarativas en lugar de scripts.

- Puede definir las dependencias de hello entre los recursos, por lo que se implementan en el orden correcto de Hola.

- Puede aplicar tooall servicios de control de acceso en el grupo de recursos porque el Control de acceso basado en roles (RBAC) se integra de forma nativa en plataforma de administración de Hola.

- Puede aplicar etiquetas tooresources toologically organizar todos los recursos de hello en su suscripción.

- Puede aclarar la facturación de su organización mediante la visualización de los costos de un grupo de recursos de uso compartido Hola la misma etiqueta.

> [!Note]
> Administrador de recursos proporciona un nuevo toodeploy de manera y administrar sus soluciones. Si ha usado Hola modelo de implementación anterior y desea toolearn acerca de los cambios de hello, consulte [descripción de administrador de recursos e implementación clásico](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Pasos siguientes

Obtener más información acerca de la seguridad con la lectura de algunos de nuestros detallados temas de seguridad:

- [Auditoría y registro](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Delitos informáticos](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Diseño y seguridad operativa](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Cifrado](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Administración de identidades y acceso](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Seguridad de las redes](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Administración de amenazas](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
