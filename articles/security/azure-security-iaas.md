---
title: "aaaSecurity mejores prácticas para IaaS cargas de trabajo en Azure | Documentos de Microsoft"
description: " migración de Hola de cargas de trabajo tooAzure IaaS pone oportunidades tooreevaluate nuestros diseños "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Procedimientos de seguridad recomendados para cargas de trabajo de IaaS de Azure

Cuando inició pensar sobre infraestructura de tooAzure de mover las cargas de trabajo como servicio (IaaS), probablemente percibe que algunas consideraciones están familiarizadas. Puede que ya tenga experiencia en la protección de entornos virtuales. Cuando se mueve tooAzure IaaS, puede aplicar sus conocimientos para la protección de entornos virtuales y usar un nuevo conjunto de opciones toohelp seguro los activos.

Comencemos diciendo que deberíamos no esperamos toobring recursos locales como tooAzure uno a uno. nuevos desafíos de Hola y nuevas opciones de hello poner una oportunidad existente de tooreevaluate deigns, herramientas y procesos.

La responsabilidad de la seguridad se basa en tipo de Hola de servicio de nube. Hello siguiente gráfico resume el saldo de Hola de responsabilidad de Microsoft y:


![Áreas de responsabilidad](./media/azure-security-iaas/sec-cloudstack-new.png)


Trataremos algunas de las opciones de hello disponibles en Azure que puede ayudar a cumplir los requisitos de seguridad de su organización. Tenga en cuenta que los requisitos de seguridad pueden variar para diferentes tipos de cargas de trabajo. Ninguno de estos procedimientos recomendados puede por sí solo proteger sus sistemas. Al igual que cualquier otra cosa en la seguridad, dispone de opciones adecuadas de toochoose hello y vea cómo soluciones Hola pueden se complementan entre sí rellenando los huecos.

## <a name="use-privileged-access-workstations"></a>Uso de estaciones de trabajo con privilegios de acceso

Las organizaciones a menudo caer en las redes toocyberattacks porque los administradores realizan acciones al usar cuentas con privilegios elevados. Normalmente, no lo hacen de forma malintencionada, sino porque la configuración y los procesos existentes lo permiten. La mayoría de estos usuarios comprender el riesgo de Hola de estas acciones desde un punto de vista conceptual, pero más ventajoso toodo ellos.

Hacer las cosas como comprobar el correo electrónico y exploración Hola Internet parecen lo suficientemente inofensivo. Pero podría exponer toocompromise de cuentas con privilegios elevados por malintencionado actores que pueden usar actividades de búsqueda, mensajes de correo electrónico especialmente diseñados u otra empresa tooyour de técnicas toogain acceso. Se recomienda encarecidamente el uso de Hola de estaciones de trabajo de administración segura para llevar a cabo todas las tareas de administración de Azure, como una manera de reducir el riesgo de exposición tooaccidental.

Las estaciones de trabajo con privilegios de acceso (PAW) proporcionan un sistema operativo dedicado para tareas delicadas, que está protegido contra ataques de Internet y vectores de amenazas. Separación de estas tareas críticas y las cuentas de Hola estaciones de trabajo de uso diario y dispositivos ofrece protección segura frente a ataques de suplantación de identidad, aplicación y vulnerabilidades de sistema operativo, diversos ataques de suplantación y ataques de robo de credenciales como pulsaciones de teclas registro, Pass-the-Hash y Pass-the-Ticket.

Hola PATA enfoque es una extensión de hello establecido y recomienda práctica toouse una cuenta administrativa individualmente asignada que es independiente de una cuenta de usuario estándar. Un PAW proporciona una estación de trabajo de confianza para esas cuentas confidenciales.

Para más información y para obtener una guía de implementación, consulte [Estaciones de trabajo con privilegios de acceso](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Uso de Multi-factor Authentication

Hola anteriores, el perímetro de la red era toocontrol usa acceso toocorporate datos. En un mundo en la nube en primer lugar, mobile en primer lugar, la identidad es plano de control de hello: se usa servicios de tooIaaS de toocontrol acceso desde cualquier dispositivo. También utiliza tooget visibilidad y una visión general de dónde y cómo es que se usan los datos. Proteger Hola identidad digital de los usuarios de Azure es la piedra angular Hola de protección de las suscripciones del robo de identidad y otros cybercrimes.

Uno de los pasos más beneficiosos Hola puede tener toosecure en una cuenta es tooenable autenticación en dos fases. Autenticación en dos fases es una manera de autenticar mediante algo en la contraseña de tooa de adición. Ayuda a mitigar el riesgo de Hola de acceso por alguien que administra tooget contraseña de otra persona.

[La autenticación multifactor Azure](../multi-factor-authentication/multi-factor-authentication.md) ayuda a proteger la toodata de acceso y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura a través de una gran variedad de opciones sencillas de comprobación (llamadas telefónicas, mensajes de texto o notificaciones de aplicaciones móviles). Los usuarios elegir método de Hola que prefieran.

toouse de manera más fácil de Hola la autenticación multifactor es la aplicación móvil de hello Authenticator de Microsoft que se puede usar en dispositivos móviles que ejecutan Windows, iOS y Android. Con la versión más reciente de Hola de Windows 10 y la integración de Hola de local de Active Directory con Azure Active Directory (Azure AD), [Windows Hello para empresas](../active-directory/active-directory-azureadjoin-passport-deployment.md) puede usarse para los recursos de tooAzure de inicio de sesión único sin problemas. En este caso, dispositivo Hola 10 de Windows se utiliza como segundo factor de hello para la autenticación.

Para cuentas que administran la suscripción de Azure y para las cuentas que pueden iniciar sesión en toovirtual máquinas, mediante la autenticación multifactor ofrece un nivel de seguridad mucho mayor que el uso de solo una contraseña. Otras formas de autenticación en dos fases podrían funcionar perfectamente, pero su implementación puede ser complicada si no están ya en producción.

Hello captura de pantalla siguiente muestra algunas de las opciones de hello disponibles para la autenticación multifactor de Azure:

![Opciones de Multi-Factor Authentication](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Limitación y restricción del acceso administrativo

Protección de las cuentas de Hola que pueden administrar su suscripción de Azure es muy importante. compromiso de Hola de cualquiera de esas cuentas niega valor Hola del programa Hola a todos los otros pasos que puede tardar la confidencialidad de hello tooensure e integridad de los datos. Hace muy poco tiempo, se muestra en hello [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) pérdida de información confidencial, los ataques internos suponen una amenaza para la enorme toohello seguridad general de una organización.

Evaluar a individuos para derechos administrativos toothese similar de criterios siguientes:

- ¿Llevan a cabo tareas que requieran privilegios administrativos?
- ¿Con qué frecuencia se realizan tareas de hello?
- ¿Hay una razón concreta por qué no se puede realizar tareas de hello otro administrador en su nombre?

Documente todos los demás privilegios de hello toogranting alternativas conocidos y por qué cada uno de ellos no es aceptable.

uso de Hola de administración just-in-time evita la existencia innecesarios Hola de cuentas con derechos elevados durante los períodos cuando no se necesitan esos derechos. Las cuentas tienen derechos elevados durante un tiempo limitado para que los administradores puedan hacer su trabajo. A continuación, dichos derechos se quitan al final de Hola de un desplazamiento o cuando se complete una tarea.

Puede usar [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, supervisar y controlar el acceso de su organización. Le ayuda a tener en cuenta las acciones de Hola que toman los usuarios de su organización. También ofrece administración just-in-time tooAzure AD introduciendo el concepto de Hola de administradores elegibles. Se trata de usuarios que hayan cuentas con hello posibles toobe concedido derechos de administrador. Estos tipos de usuarios pueden pasar por un proceso de activación y se les puede otorgar derechos de administrador durante un tiempo limitado.


## <a name="use-devtest-labs"></a>Uso de DevTest Labs

Uso de Azure para entornos de desarrollo y laboratorios permite las organizaciones toogain actuar con agilidad en desarrollo y pruebas por los retrasos de hello alejada teniendo que presenta la adquisición de hardware. Desgraciadamente, una falta de familiaridad con Azure o un toohelp desea acelerar su adopción podría provocar Hola administrador toobe excesivamente permisivo con asignación de derechos. Este riesgo puede exponer involuntariamente Hola organización toointernal ataques. A algunos usuarios se les puede otorgar mucho más acceso del que deberían tener.

Hola [laboratorios de desarrollo y pruebas de Azure](../devtest-lab/devtest-lab-overview.md) utiliza el servicio [Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-what-is.md) (RBAC). Mediante el uso de RBAC, puede separar los derechos en el equipo en roles que concedan solo nivel de Hola de acceso necesarios para los usuarios toodo sus trabajos. Incluye roles predefinidos (propietario, usuario de laboratorio y colaborador). Puede incluso usar a estos asociados de roles tooassign derechos tooexternal y simplifican considerablemente la colaboración.

Dado que los laboratorios de desarrollo y pruebas utiliza RBAC, es posible toocreate adicional, [roles personalizados](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). Laboratorios de desarrollo y pruebas no solo simplifica la administración de Hola de permisos, simplifica el proceso de Hola de obtención de entornos aprovisionados. También le ayuda resolver otros desafíos típicos de los equipos que trabajan en entornos de desarrollo y pruebas. Requiere cierta preparación, pero a largo plazo hello, facilitará cosas para su equipo.

Algunas de las características clave de Azure DevTest Labs incluyen:

- Las opciones de control administrativo sobre hello toousers disponible. Administrador de Hello puede administrar centralmente cosas como tamaños VM permitidos, número máximo de máquinas virtuales y las máquinas virtuales se inician y apagar.
- Automatización de la creación de entornos de laboratorio.
- Seguimiento de costos.
- Distribución simplificada de máquinas virtuales para realizar trabajo colaborativo temporal.
- Autoservicio que permite a los usuarios tooprovision sus laboratorios mediante plantillas.
- Administración y limitación del consumo.

![Uso de toocreate un laboratorio de prácticas de desarrollo y pruebas](./media/azure-security-iaas/devtestlabs.png)

Sin ningún costo adicional está asociado con el uso de Hola de laboratorios de desarrollo y pruebas. creación de Hello de laboratorios, directivas, plantillas y artefactos es gratuita. Se paga por solo hello Azure recursos que se utilizan en sus laboratorios, como máquinas virtuales, las cuentas de almacenamiento y redes virtuales.



## <a name="control-and-limit-endpoint-access"></a>Control y límite de acceso a puntos de conexión

Hospedaje de laboratorios o sistemas de producción en Azure significa que los sistemas necesitan toobe accesible desde Internet Hola. De forma predeterminada, una nueva máquina virtual de Windows tiene el puerto RDP hello es accesible desde Internet hello y una máquina virtual Linux tiene puerto SSH de hello abrir. Llevar a cabo pasos toolimit expuesta extremos es riesgo de hello toominimize necesarios de acceso no autorizado.

Tecnologías de Azure pueden ayudar a limitar los puntos de conexión de hello acceso toothose administrativas. Por ejemplo, puede usar grupos de seguridad de red ([NSG](../virtual-network/virtual-networks-nsg.md)). Al usar el Administrador de recursos de Azure para la implementación, los NSG limitan el acceso de Hola de todas las redes toojust Hola extremos de administración (RDP o SSH). Cuando piense en los NSG, piense en las ACL del enrutador. Puede utilizarlos comunicación de red de tootightly control hello entre varios segmentos de las redes de Azure. Se trata de redes toocreating similares en redes perimetrales u otras redes aisladas. No inspeccionar el tráfico de hello, pero ayudan con la segmentación de red.


En Azure, puede configurar una [VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) desde la red local. Una VPN de sitio a sitio extiende sus instalaciones en nube de toohello de red. Esto le ofrece otra oportunidad toouse NSG, ya que también puede modificar hello NSG toonot permitir el acceso desde cualquier lugar que no sea la red local de Hola. A continuación, puede requerir que la administración se realiza por primera toohello conexión red de Azure a través de VPN.

opción de VPN de sitio a sitio Hola podría ser muy útil en casos donde se hospedan los sistemas de producción que se integran estrechamente con sus recursos locales en Azure.

Como alternativa, puede usar hello [point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) opción en situaciones donde desea que los sistemas de toomanage que no necesita tener acceso a recursos locales de tooon. Esos sistemas pueden aislarse en su propia red virtual de Azure. Los administradores pueden VPN en hello Azure hospedan entorno a partir de su estación de trabajo administrativo.

>[!NOTE]
>Puede usar cualquier Hola de tooreconfigure de opción de VPN que ACL hello NSG toonot permiten puntos de conexión de acceso toomanagement de hello Internet.

Otra opción que merece la pena considerar es la implementación de una [puerta de enlace de Escritorio remoto](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md). También puede usar esta implementación toosecurely conectar tooRemote escritorio servidores a través de HTTPS, mientras aplica más detallada controla las conexiones de toothose.

Características que tendrás que acceder a tooinclude:

- Las opciones de administración toolimit conexiones toorequests desde sistemas específicos.
- Autenticación mediante tarjeta inteligente o Azure Multi-Factor Authentication.
- Control sobre qué sistemas un usuario puede conectar puerta de enlace de toovia Hola.
- Control sobre el redireccionamiento de dispositivos y discos.

## <a name="use-a-key-management-solution"></a>Uso de una solución de administración de claves

Administración de claves segura es esencial tooprotecting datos en la nube de Hola. Con [Azure Key Vault](../key-vault/key-vault-whatis.md) puede almacenar de forma segura claves de cifrado y pequeños secretos como contraseñas en módulos de seguridad de hardware (HSM). Para tener mayor seguridad, puede importar o generar las claves en HSM.

Microsoft procesa las claves en los HSM validados de FIPS 140-2 nivel 2 (hardware y firmware). Supervise y audite el uso de claves con registros de Azure: registros de canalizaciones en Azure o el sistema de administración de eventos e información de seguridad (SIEM) para análisis adicionales y la detección de amenazas.

Cualquiera con una suscripción a Azure puede crear y usar instancias de Key Vault. Aunque Key Vault beneficia a los desarrolladores y a los administradores de seguridad, un administrador que sea responsable de los servicios de Azure en una organización lo puede implementar y administrar.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Cifrado de discos virtuales y almacenamiento en disco

[Cifrado del disco Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) direcciones Hola a riesgo de robo de datos o la exposición de accesos no autorizados que se logra al mover un disco. disco de Hello puede ser sistema tooanother adjunta como una manera de omitir otros controles de seguridad. Utiliza el cifrado de disco [BitLocker](https://technet.microsoft.com/library/hh831713) en Windows y Crypt DM en el sistema operativo de Linux tooencrypt y unidades de datos. Cifrado de disco de Azure se integra con el almacén de claves toocontrol y administrar claves de cifrado de Hola. Está disponible para máquinas virtuales estándar y máquinas virtuales con Premium Storage.

Para más información, consulte [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](azure-security-disk-encryption.md).

El [cifrado del servicio Azure Storage](../storage/common/storage-service-encryption.md) ayuda a proteger los datos en reposo. Se habilita a nivel de cuenta de almacenamiento de Hola. Cifra los datos tal y como se escriben en nuestros centros de datos y los descifra automáticamente cuando accede a ellos. Admite Hola los escenarios siguientes:

- Cifrado de blobs en bloques, blobs en anexos y blobs en páginas
- Cifrado de los discos duros virtuales y las plantillas archivadas recuperado tooAzure en local
- Cifrado de discos de datos y SO subyacente para las máquinas virtuales de IaaS creadas con los VHD

Antes de continuar con el cifrado de Azure Storage, debe saber que existen dos limitaciones:

- No está disponible en las cuentas de almacenamiento clásico.
- Solo cifra los datos escritos después de que el cifrado esté habilitado.

## <a name="use-a-centralized-security-management-system"></a>Usa un sistema de administración de seguridad centralizado.

Los servidores necesitan toobe supervisado para la aplicación de revisiones, configuración, eventos y actividades que se pueden considerar cuestiones de seguridad. tooaddress los problemas, puede usar [centro de seguridad](https://azure.microsoft.com/services/security-center/) y [Operations Management Suite seguridad y cumplimiento](https://azure.microsoft.com/services/security-center/). Estas dos opciones ir más allá de la configuración de hello en el sistema operativo de Hola. También proporcionan supervisión de configuración de Hola de hello infraestructura, como la configuración de red y el uso de dispositivo virtual subyacente.

## <a name="manage-operating-systems"></a>Administración de sistemas operativos

En una implementación de IaaS, son sigue siendo responsable de la administración de Hola de sistemas de Hola que implemente, al igual que cualquier otro servidor o estación de trabajo en su entorno. Aplicación de revisiones, protección, asignaciones de derechos y cualquier otra actividad relacionada con toohello mantenimiento del sistema siguen siendo su responsabilidad. Para los sistemas que se integran estrechamente con los recursos locales, es recomendable toouse Hola mismas herramientas y procedimientos que usa en local para cosas como los antivirus, antimalware, aplicación de revisiones y copia de seguridad.

### <a name="harden-systems"></a>Sistemas de protección
Debe proteger todas las máquinas virtuales de IaaS de Azure para que exponen extremos de servicio que son necesarios para las aplicaciones de Hola que están instaladas. Para las máquinas virtuales de Windows, siga las recomendaciones de Hola que Microsoft publica como líneas de base para hello [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) solución.

Security Compliance Manager es una herramienta gratuita. Puede usar tooquickly configurar y administrar escritorios, centro de datos tradicional y en la nube privada y pública mediante Directiva de grupo y System Center Configuration Manager.

Security Compliance Manager proporciona directivas listas para implementar y paquetes de Administración de configuración deseada de demostrada eficacia. Estas líneas de base se basan en las recomendaciones de la [Guía de seguridad de Microsoft](https://technet.microsoft.com/en-us/library/cc184906.aspx) y en los procedimientos recomendados del sector. Le ayudan a administrar el desfase de la configuración, a solucionar los requisitos de cumplimiento y a reducir las amenazas de seguridad.

Puede usar la configuración actual de hello tooimport Security Compliance Manager de los equipos mediante el uso de dos métodos diferentes. En primer lugar, puede importar directivas de grupo basadas en Active Directory. En segundo lugar, puede importar la configuración de Hola de una "copia maestra" equipo de referencia mediante el uso de hello [LocalGPO herramienta](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback la directiva de grupo local de Hola. A continuación, puede importar directiva de grupo local de hello en el Administrador de cumplimiento de normas de seguridad.

Comparar sus prácticas recomendadas de estándares tooindustry, personalizarlos y crear nuevas directivas y paquetes de configuración de administración de configuración deseada. Se han publicado las bases de referencia de todos los sistemas operativos compatibles, incluida Actualización de aniversario de Windows 10 y Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Instalación y administración de antimalware

En entornos hospedados por separado desde el entorno de producción, puede usar un toohelp de extensión antimalware proteger las máquinas virtuales y servicios en la nube. Dicha extensión se integra con [Azure Security Center](../security-center/security-center-intro.md).


[Microsoft Antimalware](azure-security-antimalware.md) incluye características como la protección en tiempo real, los análisis programados, la corrección de malware, las actualizaciones de firmas, las actualizaciones del motor, los ejemplos de informes, la colección de eventos de exclusión y la [compatibilidad con PowerShell](https://msdn.microsoft.com/library/dn771715.aspx).

![Azure Antimalware](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Instalar actualizaciones de seguridad más recientes de Hola
Algunos de hello primeros las cargas de trabajo que mueven los clientes tooAzure son laboratorios y sistemas de uso externo. Si las máquinas virtuales hospedados en Azure hospedar aplicaciones o servicios que necesitan toobe accesible toohello Internet, debe prestar atención a aplicación de revisiones. Aplicar la revisión más allá del sistema operativo de Hola. Revisiones vulnerabilidades en aplicaciones de otros fabricantes también pueden provocar tooproblems que puede evitarse si la administración de revisiones adecuado está en su lugar.

### <a name="deploy-and-test-a-backup-solution"></a>Implementación y comprobación de una solución de copia de seguridad

Al igual que las actualizaciones de seguridad, una copia de seguridad necesita hello toobe administra igual que controlar cualquier otra operación. Esto es así de los sistemas que forman parte de su entorno de producción extender toohello en la nube. Sistemas de prueba y desarrollo deben seguir las estrategias de copia de seguridad que proporcionan capacidades de restauración que son similares a los de toowhat usuarios han acostumbrado a, en función de su experiencia con entornos locales.

Las cargas de trabajo de producción se mueven tooAzure debe integrarse con las soluciones de copia de seguridad existentes cuando sea posible. O bien, puede usar [copia de seguridad de Azure](../backup/backup-azure-arm-vms.md) toohelp abordará los requisitos de copia de seguridad.


## <a name="monitor"></a>Supervisión

[Centro de seguridad](../security-center/security-center-intro.md) proporciona tooidentify posibles vulnerabilidades de seguridad de la evaluación continua del estado de seguridad de Hola de los recursos de Azure. Una lista de recomendaciones le guía a través del proceso de Hola de configuración de controles necesarios.

Algunos ejemplos son:

- Aprovisionamiento antimalware toohelp identificar y quitar software malintencionado.
- Configuración de seguridad reglas y grupos toocontrol tráfico toovirtual máquinas de la red.
- Aprovisionamiento de firewalls de aplicación web toohelp defenderse contra los ataques que tienen como destino las aplicaciones web.
- Implementación de actualizaciones del sistema que faltan.
- Direccionamiento de las configuraciones de sistema operativo que no coincide con hello recomienda líneas de base.

Hello imagen siguiente muestra algunas de las opciones de Hola que se pueden habilitar en el centro de seguridad.

![Directivas de Azure Security Center](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) es una solución de administración de TI basada en la nube de Microsoft que ayuda a administrar y proteger infraestructuras locales y en la nube. Dado que Operations Management Suite se implementa como un servicio basado en la nube, se puede implementar rápidamente y con una inversión mínima en recursos de infraestructura.

Las características nuevas se ofrecen automáticamente, lo que supone un ahorro en costos de mantenimiento continuo y actualización. Operations Management Suite también se integra con System Center Operations Manager. Tiene toohelp de diferentes componentes que administra mejor las cargas de trabajo Azure, incluido un [seguridad y cumplimiento](../operations-management-suite/oms-security-getting-started.md) módulo.

Puede usar las características de seguridad y cumplimiento de normas de hello en información de Operations Management Suite tooview acerca de los recursos. Hola información está organizada en cuatro categorías principales:

- **Dominios de seguridad**: explore detalladamente los registros de seguridad con el tiempo. Acceda a evaluaciones de malware, evaluación de actualizaciones, información de seguridad de red, información de identidad y acceso y equipos con eventos de seguridad. Aprovechar las ventajas del panel de acceso rápido toohello centro de seguridad de Azure.
- **Problemas importantes**: identificar el número de problemas activos Hola y Hola gravedad de estos problemas rápidamente.
- **Detecciones (versión preliminar)**: identifique patrones de ataque mediante la visualización de alertas de seguridad a medida que se producen contra sus recursos.
- **Inteligencia de amenazas**: identificar ataque Hola de patrones de visualización del número total de Hola de servidores con tráfico malintencionado IP saliente, tipo de amenaza malintencionados y un mapa que muestra dónde proceden estas direcciones IP.
- **Consultas comunes de seguridad**: ver una lista de seguridad más comunes de hello las consultas puede utilizar toomonitor en su entorno. Al hacer clic en una de las consultas, Hola **búsqueda** hoja se abre y muestra los resultados de Hola para esa consulta.

Hello captura de pantalla siguiente muestra un ejemplo de Hola información que se pueden mostrar Operations Management Suite.

![Líneas de base de seguridad de Operations Management Suite](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Pasos siguientes


* [Blog del equipo de seguridad de Azure](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)
* [Patrones y procedimientos recomendados de seguridad en Azure](security-best-practices-and-patterns.md)
