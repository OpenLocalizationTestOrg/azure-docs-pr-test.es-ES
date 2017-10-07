---
title: "aaaData seguridad y prácticas recomendadas de cifrado | Documentos de Microsoft"
description: "Este artículo proporciona un conjunto de procedimientos recomendados para el cifrado y la seguridad de los datos con funcionalidades de Azure integradas."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Procedimientos recomendados de cifrado y seguridad de datos en Azure
Uno de toodata protección de claves de hello en la nube de hello es teniendo en cuenta posibles estados de hello en el que pueden producirse los datos y qué controles están disponibles para ese estado. Para el propósito de Hola de prácticas recomendadas de seguridad y cifrado de datos de Azure recomendaciones de hello será alrededor de hello siguiendo los Estados de los datos:

* En reposo: esto incluye información sobre todos los objetos de almacenamiento, los contenedores y los tipos que existen de forma estática en medios físicos, ya sean discos magnéticos u ópticos.
* En tránsito: Cuando se transfieren datos entre componentes, ubicaciones o programas, como a través de la red hello, a través de un bus de servicio (de local toocloud y viceversa, incluidas las conexiones híbridas como ExpressRoute), o durante una entrada/salida proceso, se piensa en él como en movimiento.

En este artículo, veremos un conjunto de procedimientos recomendados de cifrado y seguridad de datos en Azure. Estas prácticas recomendadas se derivan de nuestra experiencia con la seguridad de datos de Azure y las experiencias de hello y cifrado de los clientes como usted mismo.

Para cada procedimiento recomendado, explicaremos:

* ¿Qué recomienda Hola
* ¿Por qué desea tooenable este procedimiento recomendado
* ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
* Procedimiento recomendado de las alternativas posibles toohello
* ¿Cómo puede obtener información práctica recomendada de hello tooenable

En este artículo de seguridad de datos de Azure y prácticas recomendadas de cifrado se basa en una opinión de consenso y capacidades de la plataforma Windows Azure y conjuntos de características, tal como aparecen en tiempo de Hola que se escribió este artículo. Las opiniones y las tecnologías que cambian con el tiempo y este artículo será esos cambios se actualizaron en un tooreflect de forma periódica.

Entre los procedimientos recomendados de cifrado y seguridad de datos en Azure, se incluyen:

* Aplicación de Multi-Factor Authentication
* Uso del control de acceso basado en rol (RBAC)
* Cifrado de máquinas virtuales de Azure
* Uso de modelos de seguridad de hardware
* Administración con estaciones de trabajo seguras
* Habilitación del cifrado de datos SQL
* Protección de los datos en tránsito
* Aplicación del cifrado de datos a nivel de archivos

## <a name="enforce-multi-factor-authentication"></a>Aplicación de Multi-Factor Authentication
Hola primer paso de acceso a datos y el control de Microsoft Azure son usuario de hello tooauthenticate. [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) es un método de comprobación de la identidad del usuario que no se limita al nombre de usuario y la contraseña. Este método de autenticación le ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.

Al habilitar Azure MFA para los usuarios, agrega una segunda capa de inicios de sesión de seguridad toouser y las transacciones. En este caso, es posible que durante una transacción se acceda a un documento que se encuentra en un servidor de archivos o en SharePoint Online. MFA de Azure también ayuda a la probabilidad de hello tooreduce de TI que una credencial en peligro tenga los datos del acceso tooorganization.

Por ejemplo: si aplicar MFA de Azure para los usuarios y configurarlo toouse una llamada de teléfono o mensaje de texto como comprobación, si se ve comprometido la credencial del usuario de hello, el atacante de hello no ser capaz de tooaccess cualquier recurso ya que no tendrá teléfono del acceso toouser. Las organizaciones que no agregue este nivel adicional de protección de identidad sean más susceptibles de ataque de robo de credenciales, lo cual podría provocar el compromiso de toodata.

Una alternativa para las organizaciones que desean control de autenticación de hello tookeep local no se toouse [servidor Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), también denominado MFA local. Mediante este método se seguirá tooenforce capaz de la autenticación multifactor, manteniendo hello MFA server local.

Para obtener más información sobre Azure MFA, lea el artículo de hello [Introducción a la autenticación multifactor Azure en la nube de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Uso del control de acceso basado en rol (RBAC)
Restringir el acceso en función de hello [necesita tooknow](https://en.wikipedia.org/wiki/Need_to_know) y [privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principios de seguridad. Esto es necesario para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos. Azure Control de acceso basado en roles (RBAC) puede ser usado tooassign permisos toousers, grupos y aplicaciones en un ámbito determinado. ámbito de Hola de una asignación de roles puede ser una suscripción, un grupo de recursos o un único recurso.

Puede aprovechar [funciones integradas de RBAC](../active-directory/role-based-access-built-in-roles.md) en Azure tooassign privilegios toousers. Considere el uso de *colaborador de la cuenta de almacenamiento* para operadores de la nube que necesitan cuentas de almacenamiento de toomanage y *clásico colaborador de cuenta de almacenamiento* cuentas de almacenamiento clásicas toomanage de rol. Para los operadores de nube que necesita toomanage las máquinas virtuales y la cuenta de almacenamiento, considere la posibilidad de agregarlos demasiado*colaborador de la máquina Virtual* rol.

Es posible que las organizaciones que no apliquen el control de acceso a los datos mediante funcionalidades como RBAC estén concediendo más privilegios de los necesarios a sus usuarios. Esto puede provocar toodata poner en peligro debido a algunos usuarios que tienen acceso toodata que no tienen en primer lugar en Hola.

Se puede obtener más información sobre la RBAC de Azure, lea el artículo de hello [Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Cifrado de máquinas virtuales de Azure
Para muchas organizaciones, el [cifrado de los datos en reposo](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. Azure cifrado de disco permite que los administradores de TI tooencrypt Windows y discos de máquina Virtual de IaaS de Linux (VM). Cifrado del disco Azure aprovecha característica BitLocker Hola sector estándar de Windows y la característica de DM Crypt de Hola de cifrado del volumen de tooprovide de Linux para hello OS y discos de datos de Hola.

Puedes sacar provecho de cifrado del disco de Azure toohelp proteger y proteger los datos toomeet sus requisitos de seguridad y cumplimiento organizativos. Las organizaciones también deben considerar el uso de cifrado toohelp mitigar los riesgos relacionados toounauthorized acceso a los datos. También se recomienda que cifrar unidades toowriting anterior confidencial toothem.

Asegúrese de tooencrypt seguro de los volúmenes de datos de la máquina virtual y el volumen de arranque datos de pedidos tooprotect almacenados en su cuenta de almacenamiento de Azure. Proteger las claves de cifrado de Hola y secretos aprovechando [el almacén de claves de Azure](../key-vault/key-vault-whatis.md).

Para los servidores de Windows local, considere la posibilidad de hello siguiendo los procedimientos recomendados de cifrado:

* Usar [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) para el cifrado de datos
* Almacene la información de recuperación en AD DS.
* Si hay cualquier problema que se han puesto en peligro las claves de BitLocker, se recomienda formatear o Hola unidad tooremove todas las instancias de metadatos de BitLocker de Hola de unidad de Hola o que descifrar y cifrar toda unidad de Hola de nuevo.

Las organizaciones que no se exija el cifrado de datos son más probable toodata toobe expuesta los problemas de integridad, por ejemplo, los usuarios no autorizados o malintencionados roben datos y puesto en peligro las cuentas tengan toodata de acceso no autorizado en un formato claro. Además de estos riesgos, las empresas que tienen toocomply con las normativas del sector, debe demostrar que están diligente y utiliza la seguridad de datos de hello seguridad correctas controles tooenhance.

Se puede obtener más información acerca del cifrado de disco de Azure, lea el artículo de hello [cifrado de disco de Azure para Windows y las máquinas virtuales de Linux IaaS](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Uso de módulos de seguridad de hardware
Las soluciones de cifrado de sector usan datos tooencrypt de claves secretas. Por lo tanto, es fundamental que estas claves se almacenen de forma segura. Administración de claves se convierte en una parte integral de protección de datos, puesto que se toostore aprovechado claves secretas que son datos de uso tooencrypt.

Cifrado de disco de Azure usa [el almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/) toohelp controlar y administrar claves de cifrado de disco y secretos en su suscripción de almacén de claves, asegurándose de que todos los datos en discos de máquina virtual de Hola se cifran en reposo en Azure almacenamiento de información. Debe usar las claves de tooaudit del almacén de claves de Azure y uso de directivas.

Hay muchos riesgos inherentes de toonot relacionados con controles de seguridad adecuados en lugar tooprotect Hola claves secretas que estaban tooencrypt usa los datos. Si los atacantes tienen acceso a las claves secretas toohello, se van a ser capaz de toodecrypt Hola datos y puedan tener acceso a información de tooconfidential.

Se puede obtener más información acerca de las recomendaciones generales para la administración de certificados en Azure, lea el artículo de hello [la administración de certificados en Azure: pros y los contras](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Para más información sobre Azure Key Vault, lea [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Administración con estaciones de trabajo seguras
Desde la mayoría de Hola Hola ataques Hola final del usuario de destino, el punto de conexión de Hola se convierte en uno de los puntos principales de Hola de ataque. Si un atacante pone en peligro el punto de conexión de hello, puede aprovechar los datos del tooorganization de acceso del usuario de hello credenciales toogain. La mayoría de los ataques de punto de conexión son tootake puede aprovechar los hechos de Hola que los usuarios finales son administradores en sus estaciones de trabajo locales.

Para reducir estos riesgos, use una estación de trabajo de administración segura. Se recomienda que use un [estaciones de trabajo de acceso con privilegios (PAW)](https://technet.microsoft.com/library/mt634654.aspx) superficie expuesta a ataques tooreduce hello en estaciones de trabajo. Estas estaciones de trabajo de administración seguras pueden ayudar a mitigar algunos de estos ataques y a garantizar la mayor seguridad de sus datos. Asegúrese de toouse seguro PATA tooharden y bloqueo hacia abajo de la estación de trabajo. Se trata de un garantías de alta seguridad tooprovide paso importante para cuentas confidenciales, tareas y protección de datos.

Falta de endpoint protection puede correr el riesgo de los datos, que seguro tooenforce las directivas de seguridad en todos los dispositivos que son datos de uso tooconsume, independientemente de la ubicación de datos de hello (en la nube o local).

Aprenderá más acerca de privilegios de acceso estación de trabajo, lea el artículo de hello [protección de acceso con privilegios](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>Habilitación del cifrado de datos SQL
[Cifrado de datos transparente de bases de datos de SQL Azure](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin requiere la aplicación de toohello de cambios.  TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica.

Incluso cuando se cifra el almacenamiento en su totalidad hello, es muy importante tooalso cifrar la base de datos. Se trata de una implementación de defensa de hello en el enfoque de profundidad para la protección de datos. Si utilizas [base de datos de SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) y desea que los datos confidenciales tooprotect como tarjeta de crédito o números de seguridad social, puede cifrar las bases de datos con FIPS cifrado de AES de 256 bits validado 140-2 que cumpla los requisitos de Hola de muchos estándares del sector (por ejemplo, HIPAA, PCI).

Es importante toounderstand que los archivos relacionados demasiado[extensión del grupo de búferes](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) no se cifran cuando una base de datos se cifra con TDE. Debe usar herramientas de cifrado de nivel de sistema de archivos como BitLocker o hello [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) para BPE archivos relacionados.

Desde un usuario autorizado, como un administrador de seguridad o una base de datos puede tener acceso a datos de hello incluso si la base de datos de Hola se cifra con TDE, también debe seguir las recomendaciones de Hola a continuación:

* Autenticación de SQL en el nivel de base de datos de Hola
* Autenticación de Azure AD mediante roles RBAC
* Los usuarios y las aplicaciones deben usar tooauthenticate cuentas independientes. Este modo puede limitar los permisos de hello concedidas toousers y las aplicaciones y reducir los riesgos de Hola de actividad malintencionada
* Implemente seguridad de nivel de base de datos mediante el uso de roles de base de datos fija (por ejemplo, db_datareader o db_datawriter), o bien puede crear roles personalizados para su aplicación toogrant objetos de base de datos de tooselected permisos explícitos

Las organizaciones que no usen el cifrado de nivel de base de datos pueden ser más susceptibles a ataques que podrían poner en peligro los datos ubicados en bases de datos SQL.

Se puede obtener más información acerca del cifrado de SQL TDE, lea el artículo de hello [cifrado de datos transparente con base de datos de SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Protección de los datos en tránsito
Proteger los datos en tránsito debe ser una parte esencial de su estrategia de protección de datos. Puesto que los datos se va a mover y hacia atrás desde varias ubicaciones, recomendación general hello es que siempre que usan los datos de tooexchange de protocolos SSL/TLS en diferentes ubicaciones. En algunas circunstancias, puede que desee canal de tooisolate Hola toda comunicación entre el local y la nube infraestructura mediante el uso de una red privada virtual (VPN).

Para los datos que se desplazan entre la infraestructura local y Azure, debe plantearse usar medidas de seguridad apropiadas, como HTTPS o VPN.

Las organizaciones que necesitan tener acceso toosecure desde varias estaciones de trabajo locales encuentra tooAzure, usar [Azure VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Para las organizaciones que necesitan acceso de toosecure desde una estación de trabajo encuentra tooAzure local, use [Point-to-Site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Los conjuntos de datos más grandes se pueden mover por medio de un vínculo WAN dedicado de alta velocidad como [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si elige toouse ExpressRoute, también puede cifrar los datos de hello en el uso de nivel de aplicación de hello [SSL/TLS](https://support.microsoft.com/kb/257591) u otros protocolos para conseguir una protección adicional.

Si interactúa con el almacenamiento de Azure a través de hello Portal de Azure, todas las transacciones se producen a través de HTTPS. [API de REST de almacenamiento](https://msdn.microsoft.com/library/azure/dd179355.aspx) a través de HTTPS, también puede ser usado toointeract con [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) y [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/).

Las organizaciones que no cumplan tooprotect datos en tránsito sean más susceptibles de [man-in-the-middle ataques](https://technet.microsoft.com/library/gg195821.aspx), [interceptaciones](https://technet.microsoft.com/library/gg195641.aspx) y secuestro de sesión. Estos ataques pueden ser el primer paso de Hola para obtener acceso a los datos tooconfidential.

Se puede obtener más información acerca de la opción de VPN de Azure, lea el artículo de hello [planificación y diseño para la puerta de enlace VPN](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Aplicación del cifrado de datos a nivel de archivos
Otra capa de protección que puede aumentar el nivel de Hola de seguridad de los datos está cifrando Hola propio archivo, independientemente de la ubicación del archivo de Hola.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de las directivas de cifrado, identidad y autorización utiliza proteger los archivos y correo electrónico. Azure RMS funciona en varios dispositivos (teléfonos, tabletas y PC) y los protege tanto dentro como fuera de su organización. Esta capacidad es posible ya que Azure RMS agrega un nivel de protección que conserva los datos de hello, incluso cuando sale de los límites de su organización.

Cuando usas Azure RMS tooprotect los archivos, que usa la criptografía estándar del sector con el soporte completo de [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Al aprovechar Azure RMS para proteger los datos, tiene garantía de Hola Hola permanece con el archivo hello, incluso si es toostorage copiada que no está bajo control de Hola de TI, como un servicio de almacenamiento en la nube. Hello mismo ocurre con los archivos compartidos a través de correo electrónico, archivo hello está protegido como un mensaje de correo electrónico de tooan datos adjuntos, con instrucciones de cómo tooopen Hola protege datos adjuntos.

Al planear la adopción de Azure RMS, recomendamos siguiente de hello:

* Instalar hello [aplicación RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Esta aplicación se integra con las aplicaciones de Office con la instalación de un complemento de Office con el que los usuarios pueden proteger los archivos directamente y de forma sencilla.
* Configurar aplicaciones y servicios toosupport Azure RMS
* Cree [plantillas personalizadas](https://technet.microsoft.com/library/dn642472.aspx) que reflejen sus requisitos empresariales. Por ejemplo: una plantilla para los datos más delicados que se deba aplicar a todos los correos electrónicos de mayor confidencialidad.

Las organizaciones que están débiles en [clasificación de datos](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) y protección de archivos puede ser más susceptible de sufrir pérdida de toodata. Sin protección de archivo adecuados, las organizaciones no tooobtain capaz de información empresarial, supervisar para controlar el abuso además de evitar accesos malintencionados toofiles.

Se puede obtener más información acerca de Azure RMS, lea el artículo de hello [Introducción a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
