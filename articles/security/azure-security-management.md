---
title: "seguridad de la administración remota de aaaEnhance en Azure | Documentos de Microsoft"
description: "En este artículo se describen los pasos para mejorar la seguridad en la administración remota de entornos de Microsoft Azure, incluidos servicios en la nube, Virtual Machines y aplicaciones personalizadas."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Administración de la seguridad en Azure
Los suscriptores de Azure pueden administrar sus entornos de nube desde diversos dispositivos, incluidas estaciones de trabajo de administración, equipos de desarrollador e incluso dispositivos de usuario final con privilegios que tengan permisos específicos para la tarea. En algunos casos, las funciones administrativas se realizan a través de consolas basadas en web como hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). En otros casos, puede haber tooAzure conexiones directas desde sistemas locales a través de redes privadas virtuales (VPN), servicios de Terminal Server, protocolos de aplicaciones de cliente o (mediante programación) hello API de administración de servicio de Azure (SMAPI). Además, los puntos de conexión de cliente pueden estar unidos a un dominio o aislados y no administrados, como tabletas o smartphones.

Aunque varias capacidades de administración y acceso proporcionan un amplio conjunto de opciones, esta variabilidad puede agregar la implementación en la nube tooa riesgo significativo. Puede ser difícil toomanage, realizar un seguimiento y auditar las acciones administrativas. Esta variabilidad también puede presentar las amenazas de seguridad a través de extremos de tooclient de acceso no reguladas que se usan para administrar servicios en la nube. El uso de estaciones de trabajo personales o generales para desarrollar y administrar infraestructuras abre la puerta a amenazas impredecibles que se producen tanto en la exploración web (por ejemplo, ataques a los sitios web más utilizados) como en el correo electrónico (tales como ingeniería social y suplantación de identidad [phishing]).

![][1]

Hola posible ataques aumenta en este tipo de entorno porque es un desafío de las directivas de seguridad de tooconstruct y mecanismos tooappropriately administrar interfaces de acceso a tooAzure (por ejemplo, SMAPI) desde los puntos de conexión muy variadas.

### <a name="remote-management-threats"></a>Amenazas de la administración remota
Los atacantes a menudo intentan conectarse de manera toogain con privilegios de poner en peligro las credenciales de cuenta (por ejemplo, mediante la fuerza bruta de contraseñas, suplantación de identidad y recopilación de credenciales), o bien engañar a los usuarios para ejecutar código perjudicial (por ejemplo, desde sitios Web dañino con las descargas ocultas o datos adjuntos de correo electrónico dañinos). En un entorno administrado de forma remota en la nube, cuenta infracciones pueden provocar tooan mayor riesgo due tooanywhere, acceso en cualquier momento.

Incluso con controles estrictos en las cuentas de administrador principal, las cuentas de usuario de nivel inferior pueden puntos débiles de tooexploit usado en la estrategia de seguridad de uno. Falta de aprendizaje de seguridad adecuadas puede provocar también toobreaches a través de la divulgación accidental o la exposición de información de la cuenta.

Cuando una estación de trabajo de usuario se usa también para realizar tareas administrativas, puede presentar muchos puntos de riesgo distintos, Si un usuario explorar hello web, utilizando herramientas de terceros 3rd y código abierto o abrir un archivo de documento dañinos contiene un caballo de Troya.

En general, más ataques dirigidos que puede ser resultado de las infracciones de datos realiza un seguimiento toobrowser vulnerabilidades, complementos (por ejemplo, Flash, PDF, Java) y ataques "phishing" (correo electrónico) en equipos de escritorio. Estas máquinas pueden tener nivel administrativo o los permisos de nivel de servicio tooaccess servidores de live o dispositivos para las operaciones cuando se usa para el desarrollo o administración de otros recursos de red.

### <a name="operational-security-fundamentals"></a>Fundamentos de la seguridad operativa
Para más segura administración y operaciones, puede minimizar la superficie expuesta a ataques de un cliente reduciendo el número de Hola de posibles puntos de entrada. Esto puede hacerse a través de los principios de seguridad: "segregación de controles" y "segregación de entornos".

Aislar funciones delicadas desde entre sí toodecrease Hola probabilidad de que un error en un nivel conduce tooa infracción en otro. Ejemplos:

* Las tareas administrativas no deben combinarse con las actividades que podrían dar lugar a riesgos de tooa (por ejemplo, malware en un correo electrónico del administrador que, a continuación, se infecta a un servidor de infraestructura).
* Una estación de trabajo que se utiliza para las operaciones de alta sensibilidad no debe ser Hola mismo sistema utilizado para fines de alto riesgo como Hola exploración de Internet.

Reducir la superficie expuesta a ataques del sistema de hello mediante la eliminación de software innecesario. Ejemplo:

* Estándar administrativa, soporte técnico o estación de trabajo de desarrollo debe no requiere la instalación de un cliente de correo electrónico u otras aplicaciones de productividad si propósito principal del dispositivo de hello es toomanage servicios en la nube.

Los sistemas que tienen tooinfrastructure de acceso de administrador componentes deben estar sujetos a riesgos de seguridad de posibles de las directivas más estrictos de toohello tooreduce. Ejemplos:

* Las directivas de seguridad pueden incluir la configuración de directiva de grupo que deniegan el acceso abierto de Internet del dispositivo de Hola y el uso de una configuración de firewall restrictiva.
* Uso de redes VPN con protocolo de seguridad de Internet (IPsec) si se necesita acceso directo.
* Configuración de dominios de Active Directory de desarrollo y administración independientes.
* Aislamiento y filtrado del tráfico de red de las estaciones de trabajo de administración.
* Uso de software antimalware.
* Implemente el riesgo de la autenticación multifactor tooreduce Hola de credenciales robadas.

La consolidación de los recursos de acceso y la eliminación de puntos de conexión no administrados también simplifica las tareas de administración.

### <a name="providing-security-for-azure-remote-management"></a>Seguridad para la administración remota de Azure
Azure proporciona seguridad Administradores de tooaid de mecanismos que administran servicios de nube de Azure y máquinas virtuales. Estos mecanismos incluyen:

* Autenticación y [control de acceso basado en rol](../active-directory/role-based-access-control-configure.md).
* Supervisión, registro y auditoría.
* Certificados y comunicación cifrada.
* Un portal de administración web.
* Filtrado de paquetes de red.

Con la configuración de seguridad de cliente e implementación de centro de datos de una puerta de enlace de administración, es datos y posibles toorestrict y monitor acceso toocloud aplicaciones de administrador.

> [!NOTE]
> Algunas de las recomendaciones de este artículo pueden provocar un aumento del uso de datos, de la red o de los recursos de proceso, lo que podría incrementar los costos de las licencias o las suscripciones.
>
>

## <a name="hardened-workstation-for-management"></a>Estación de trabajo protegida para administración
objetivo de Hola de protección de una estación de trabajo es tooeliminate todos los pero las funciones más importantes de hello necesario toooperate, hacer que la superficie de ataque potencial de hello tan pequeño como sea posible. Protección del sistema incluye minimizando Hola número de servicios instalados y aplicaciones, limitar la ejecución de la aplicación, restringir tooonly de acceso de red lo que se necesita, y mantener siempre toodate de actividad del sistema Hola. Además, el uso de estaciones de trabajo protegidas para la administración aísla las herramientas y las actividades administrativas de las demás tareas del usuario final.

Dentro de un entorno empresarial local, puede limitar la superficie expuesta a ataques de la infraestructura física a través de redes de administración dedicada, salas de servidores que tienen acceso de la tarjeta y estaciones de trabajo que se ejecutan en las áreas protegidas de red de Hola Hola. En una nube o el modelo de TI híbrida, el que se va a diligentes para servicios de administración segura puede ser más compleja debido a la falta de Hola de recursos de tooIT de acceso físico. La implementación de soluciones de protección requiere una cuidadosa configuración del software, procesos centrados en la seguridad y directivas completas.

Mediante una superficie con privilegios mínimos minimizada software en una estación de trabajo bloqueado para la administración de la nube y para el desarrollo de aplicaciones, puede reducir el riesgo de Hola de incidentes de seguridad mediante la estandarización de entornos de desarrollo y administración remotos Hola. Una configuración de estación de trabajo protegido puede ayudar a evitar poner en peligro hello las cuentas que son utilizados toomanage críticas en la nube recursos cerrando muchos accesos comunes utilizados por malware y vulnerabilidades de seguridad. En concreto, puede usar [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) y toocontrol de tecnología de Hyper-V y aislar el comportamiento del sistema de cliente y mitigar amenazas, incluido el correo electrónico o explorar Internet.

En una estación de trabajo protegido, una cuenta de usuario estándar (que bloquea la ejecución de nivel administrativo) ejecuta el Administrador de Hola y aplicaciones asociadas se controlan mediante una lista de permitidos. elementos básicos de Hola de una estación de trabajo protegido son los siguientes:

* Análisis y revisión activos. Implementar software antimalware, realizar análisis de vulnerabilidad regular y actualizar todas las estaciones de trabajo mediante la actualización de seguridad más reciente de Hola de manera oportuna.
* Funcionalidad limitada Desinstale todas las aplicaciones que no sean necesarias y deshabilite los servicios innecesarios (inicio).
* Protección de la red. Usar administración de tooAzure relacionadas de las direcciones URL, puertos y direcciones IP solo es válidas de tooallow de reglas de Firewall de Windows. Asegúrese de que esa estación de trabajo de toohello conexiones remotas entrantes también se bloquean.
* Restricción de la ejecución. Permitir sólo un conjunto de archivos ejecutables predefinidos que son necesarios para administración toorun (denominada tooas "denegación predeterminada"). De forma predeterminada, los usuarios deben ser denegados el permiso lista de admisión de toorun cualquier programa a menos que se defina explícitamente en Hola.
* Privilegios mínimos. Los usuarios de estación de trabajo de administración no deben tener privilegios administrativos en la propia máquina local de Hola. De esta manera, no pueden cambiar configuración del sistema de Hola o archivos de sistema de hello, ya sea intencionada o accidentalmente.

Puede aplicar todo esto mediante [objetos de directiva de grupo](https://www.microsoft.com/download/details.aspx?id=2612) (GPO) en servicios de dominio de Active Directory (AD DS) y aplicarla a través de las cuentas de administración de tooall de dominio de administración (local).

### <a name="managing-services-applications-and-data"></a>Administración de servicios, aplicaciones y datos
Configuración de servicios de nube de Azure se realiza a través de hello portal de Azure o SMAPI, a través de la interfaz de línea de comandos de Windows PowerShell de Hola o una aplicación personalizada que aprovecha las ventajas de estas interfaces RESTful. Los servicios que usan estos mecanismos son Azure Active Directory (Azure AD), Almacenamiento de Azure, Sitios web de Azure y Red virtual de Azure, entre otros.

Máquina virtual: implementa aplicaciones proporcionan sus propias herramientas de cliente e interfaces según sea necesario, como Hola Microsoft Management Console (MMC), una consola de administración de la empresa (por ejemplo, Microsoft System Center ni sobre Windows Intune) o administración de otro aplicación: Microsoft SQL Server Management Studio, por ejemplo. Estas herramientas suelen residir en una red de cliente o en un entorno empresarial. Pueden depender de protocolos de red específicos, como el Protocolo de escritorio remoto (RDP), que requiere conexiones directas con estado. Algunos pueden tener interfaces habilitadas para web que no deben estar abiertamente publicado o accesible a través de Internet de Hola.

Puede restringir la administración de servicios de acceso tooinfrastructure y plataforma en Azure mediante el uso de [la autenticación multifactor](../multi-factor-authentication/multi-factor-authentication.md), [certificados de administración X.509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)y las reglas de firewall. Hola portal de Azure y SMAPI requieren seguridad de capa de transporte (TLS). Sin embargo, servicios y aplicaciones que se implementación en Azure requieren tootake las medidas de protección que son adecuadas en función de la aplicación. Estos mecanismos se suelen habilitar más fácilmente mediante una configuración de estación de trabajo protegida estándar.

### <a name="management-gateway"></a>Puerta de enlace de administración
toocentralize todos los administrativo acceso y simplificar la supervisión y el registro, puede implementar una dedicado [puerta de enlace de escritorio remoto](https://technet.microsoft.com/library/dd560672) server (puerta de enlace de escritorio remoto) en sus instalaciones de red, conectado tooyour entorno de Azure.

Puerta de enlace de Escritorio remoto es un servicio de proxy RDP basado en directivas que aplica requisitos de seguridad. La implementación de Puerta de enlace de Escritorio remoto junto con Windows Server Network Access Protection (NAP) ayuda a garantizar que solo podrán conectarse los clientes que cumplen los criterios de mantenimiento de seguridad específicos establecidos por Servicios de dominio de Active Directory (AD DS) y Objetos de directiva de grupo (GPO). Además:

* Aprovisionar un [certificado de administración de Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) en hello puerta de enlace de escritorio remoto para que esté permitido de host solo hello tooaccess Hola portal de Azure.
* Unir toohello de puerta de enlace de escritorio remoto de hello mismo [dominio de administración](http://technet.microsoft.com/library/bb727085.aspx) como Hola estaciones de trabajo. Esto es necesario cuando se usa una VPN con IPsec de sitio a sitio o ExpressRoute dentro de un dominio que tenga un tooAzure de confianza unidireccional AD o si está realizando una federación credenciales entre sus instalaciones en instancia de AD DS y Azure AD.
* Configurar un [directiva de autorización de conexión de cliente](http://technet.microsoft.com/library/cc753324.aspx) toolet Hola puerta de enlace de escritorio remoto Compruebe que nombre de la máquina cliente hello es válido (Unidos a un dominio) y tooaccess permitidos Hola portal de Azure.
* Utilice IPsec para [VPN de Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther proteger el tráfico de administración de robo de interceptación y token o considere la posibilidad de un vínculo aislado de Internet a través de [ExpressRoute de Azure](https://azure.microsoft.com/documentation/services/expressroute/).
* Habilite la autenticación multifactor (mediante [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) o la autenticación de tarjeta inteligente para los administradores que inician sesión mediante Puerta de enlace de Escritorio remoto.
* Configurar origen de [restricciones de dirección IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) o [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) en número de hello Azure toominimize de extremos de administración permitidos.

## <a name="security-guidelines"></a>Directrices de seguridad
En general, lo que ayuda toosecure estaciones de trabajo para su uso con la nube de hello es similar toohello prácticas que se usan para cualquier estación de trabajo local, por ejemplo, minimizar la compilación y permisos restrictivos. Algunos aspectos exclusivos de administración en la nube son más analogía tooremote o administración fuera de banda empresarial. Se trata de uso de Hola y auditoría de credenciales, acceso remoto con seguridad mejorada y la detección de amenazas y respuesta.

### <a name="authentication"></a>Autenticación
También puede utilizar direcciones IP de origen de tooconstrain de restricciones de inicio de sesión de Azure para tener acceso a herramientas administrativas y auditar las solicitudes de acceso. toohelp Azure identificar a los clientes de administración (estaciones de trabajo o las aplicaciones), puede configurar SMAPI (a través de herramientas desarrollados por el cliente como cmdlets de Windows PowerShell) y toobe de certificados de administración de cliente de hello toorequire de portal de Azure Además tooSSL los certificados instalados. Se recomienda también que el acceso de administrador requiera autenticación multifactor.

Algunas aplicaciones o servicios que se implementan en Azure pueden tener sus propios mecanismos de autenticación para el acceso de usuario final y de administrador, mientras que otras aprovechan toda la funcionalidad de Azure AD. Dependiendo de si se están realizando una federación credenciales a través de los servicios de federación de Active Directory (AD FS), mediante la sincronización de directorios o mantenimiento de cuentas de usuario únicamente en hello en la nube, con [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (parte de Azure AD Premium) le ayuda a administrar los ciclos de vida de identidades entre los recursos de Hola.

### <a name="connectivity"></a>Conectividad
Varios mecanismos es tooyour de conexiones de cliente segura disponible toohelp redes virtuales de Azure. Dos de estos mecanismos, [VPN de sitio a sitio](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) y [point-to-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), habilitar el uso de saludo de la industria de IPsec estándar (S2S) o hello [Secure Socket de protocolo de túnel](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) para el cifrado y protocolo de túnel. Cuando Azure conectarse management toopublic orientada a servicios de Azure como Hola portal de Azure, Azure requiere la transferencia de hipertexto protocolo seguro (HTTPS).

Una estación de trabajo reforzado independiente que no se conecta tooAzure a través de una puerta de enlace de escritorio remoto debe usar Hola basada en SSTP point-to-site VPN toocreate Hola conexión inicial toohello red Virtual de Azure y, a continuación, establecer tooindividual de conexión RDP virtual máquinas de túnel VPN de Hola.

### <a name="management-auditing-vs-policy-enforcement"></a>Auditoría de administración y aplicación de directivas 
Por lo general, hay dos métodos que ayudan a los procesos de administración de toosecure: auditoría y la directiva de cumplimiento. Ambos proporcionarán controles completos, pero que pueden no ser posibles en todas las situaciones. Además, cada enfoque tiene diferentes niveles de riesgo, el costo y el esfuerzo asociado con la administración de seguridad, especialmente en lo referente toohello nivel de confianza que se colocan en usuarios y arquitecturas de sistema.

Supervisión, registro y auditoría de proporcionan una base para el seguimiento y la descripción de las actividades administrativas, pero puede que no siempre sea factible tooaudit todas las acciones en completar detalle debido toohello cantidad de datos generado. Eficacia de Hola Hola de directivas de administración de auditoría es un procedimiento recomendado, sin embargo.

La aplicación de directivas que incluyen controles estrictos de acceso coloca mecanismos de programación que rigen la acciones del administrador, y ayuda a garantizar que se están usando todas las medidas de protección posibles. Registro proporciona una prueba de cumplimiento en el registro de tooa de adición de quién hizo qué, desde dónde y cuándo. Registro también le permite tooaudit y crosscheck información acerca de cómo los administradores siguen las directivas, y proporciona una evidencia de actividades

## <a name="client-configuration"></a>Configuración de cliente
Se recomiendan tres configuraciones principales para una estación de trabajo protegida. diferenciadores más importantes de Hello entre ellos son costo, la facilidad de uso y la accesibilidad, al tiempo que mantiene un perfil de seguridad similar a través de todas las opciones. Hello en la tabla siguiente proporciona un análisis breve de hello tooeach de ventajas y riesgos. (Tenga en cuenta que "PC corporativos" hace referencia tooa PC configuración de escritorio estándar que se pueden implementar para todos los usuarios del dominio, independientemente de las funciones.)

| Configuración | Ventajas | Desventajas |
| --- | --- | --- |
| Estación de trabajo protegida independiente |Estación de trabajo estrechamente controlada |mayor costo para escritorios dedicados |
| - | Menor riesgo de vulnerabilidades de la aplicación |Mayor esfuerzo de administración |
| - | Clara separación de las tareas | - |
| Equipo corporativo como máquina virtual |Menores costos de hardware | - |
| - | Separación de roles y aplicaciones | - |
| Toogo de Windows con el cifrado de unidad BitLocker |Compatibilidad con la mayoría de los equipos |Seguimiento de activos |
| - | Rentabilidad y portabilidad | - |
| - | Entorno de administración aislado |- |

Es importante que hello protegido de la estación de trabajo es el host de hello y no hello invitado, sin nada entre Hola host hardware hello y sistema operativo. Hola "origen limpio al principio" (también conocido como "seguro origen") significa que hospedan Hola debe ser hello más protegido. En caso contrario, hello reforzado workstation (invitado) es un asunto tooattacks en sistema de hello en el que se hospeda.

Puede aislar aún más las funciones administrativas a través de imágenes de sistema dedicado para cada estación de trabajo protegido que tienen sólo herramientas de Hola y permisos necesitan para administrar Active Azure y aplicaciones con local AD DS unos GPO específicos para hello en la nube tareas necesarias.

Para entornos de TI que carecen de infraestructura local (por ejemplo, no hay acceso tooa ADDS locales de instancia para los GPO porque todos los servidores están en la nube de hello), un servicio como [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) puede simplificar la implementación y mantenimiento configuraciones de estación de trabajo.

### <a name="stand-alone-hardened-workstation-for-management"></a>Estación de trabajo protegida independiente para administración
Con una estación de trabajo protegida independiente, los administradores tienen un equipo o un portátil que usan para las tareas administrativas, y otro equipo o portátil diferente para las tareas no administrativas. Una estación de trabajo dedicado toomanaging los servicios de Azure no tiene otras aplicaciones instaladas. Además, el uso de estaciones de trabajo que admiten un [Módulo de plataforma segura](https://technet.microsoft.com/library/cc766159) (TPM) o una tecnología de criptografía de nivel de hardware similar ayuda a autenticar dispositivos e impedir ciertos ataques. TPM también puede admitir la protección de volumen completo de la unidad del sistema hello mediante el uso de [cifrado de unidad BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

En caso de estación de trabajo independiente reforzado hello (que se muestra a continuación), instancia local de Hola de Firewall de Windows (o un servidor de seguridad de cliente de otros fabricantes) está configurado tooblock conexiones, como RDP de entrada. Administrador de Hello puede iniciar sesión toohello protegido de la estación de trabajo e iniciar una sesión RDP que se conecta tooAzure después de establecer una VPN de conectarse a una red Virtual de Azure, pero no pueden iniciar sesión tooa corporativa PC y use RDP tooconnect toohello reforzado estación de trabajo sí mismo.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Equipo corporativo como máquina virtual
En casos donde un independiente reforzado estación de trabajo independiente es costo prohibitivo o supone un inconveniente, Hola protegido de la estación de trabajo puede alojar un tareas no administrativas tooperform de máquina virtual.

![][3]

tooavoid varios riesgos de seguridad que pueden surgir del uso de una estación de trabajo para la administración de sistemas y otras tareas de trabajo diario, puede implementar un toohello de máquina virtual de Hyper-V de Windows protegido estación de trabajo. Esta máquina virtual puede usarse como Hola PC corporativos. entorno de equipo corporativo Hola puede permanecer aislada de Hola Host, lo cual reduce su superficie de ataque y quita las actividades diarias del usuario de hello (por ejemplo, correo electrónico) de coexistencia con las tareas administrativas confidenciales.

máquina de virtual PC corporativo Hola se ejecuta en un espacio protegido y proporciona a las aplicaciones de usuario. host de Hello sigue siendo un "origen limpio" y aplica las directivas de red estricta en el sistema de operativo Hola raíz (por ejemplo, bloqueo acceso RDP desde la máquina virtual de hello).

### <a name="windows-toogo"></a>TooGo de Windows
Toorequiring alternativo otro una estación de trabajo independiente reforzado es toouse una [tooGo Windows](https://technet.microsoft.com/library/hh831833.aspx) unidad, una característica que admite una capacidad de arranque USB del lado cliente. Windows tooGo permite ejecutar desde una unidad flash USB cifrada de la imagen del sistema aislado de tooan de usuarios tooboot un equipo compatible. Proporciona controles adicionales para puntos de conexión de administración remota ya imagen Hola puede ser totalmente administrado por un grupo de TI corporativo, con las directivas de seguridad estricta, una compilación de SO mínima, y admite TPM.

En la figura de Hola a continuación, imagen portátil hello es un sistema Unidos a un dominio que está preconfigurado tooconnect solo tooAzure, requiere la autenticación multifactor y bloquea todo el tráfico de administración no. Si un arranque a otro usuario hello misma imagen corporativa de PC toohello estándar y los intentos de obtener acceso a la puerta de enlace de escritorio remoto para herramientas de administración de Azure, se bloquea la sesión de Hola. Windows tooGo se convierte en el sistema operativo de nivel de raíz de Hola y capas adicionales no son necesario (sistema operativo, hipervisor, máquina virtual de host) que pueden ser más vulnerables toooutside los ataques.

![][4]

Es importante toonote que las unidades flash USB se pierden más fácilmente que un equipo de escritorio promedio. Uso de BitLocker tooencrypt Hola volumen completo, junto con una contraseña segura, resulta menos probable que un atacante puede utilizar imagen de la unidad de hello fines perjudicial. Además, si se pierde la unidad flash USB de hello, revocar y [emitir un nuevo certificado de administración](https://technet.microsoft.com/library/hh831574.aspx) junto con una contraseña rápida restablecimiento puede reducir la exposición. Los registros de auditoría administrativas residen dentro de Azure, no en cliente hello, reduce aún más la posible pérdida de datos.

## <a name="best-practices"></a>Prácticas recomendadas
Considere la posibilidad de hello las siguientes directrices adicionales cuando se administra las aplicaciones y datos en Azure.

### <a name="dos-and-donts"></a>Consejos
No dé por sentado que ya se ha bloqueado una estación de trabajo que otros requisitos de seguridad comunes no es necesario toobe cumplen. riesgo potencial de Hello es superior a causa de los niveles de acceso con privilegios elevados que normalmente poseen las cuentas de administrador. En tabla Hola siguiente se muestran ejemplos de los riesgos y sus prácticas de seguridad alternativas.

| No | Sí |
| --- | --- |
| No envíe por correo electrónico credenciales de acceso de administrador ni otros secretos (por ejemplo, certificados SSL o de administración) |Mantenga la confidencialidad; para ello, entregue los nombres y las contraseñas de las cuentas de palabra (pero no los almacene en buzones de voz), realice una instalación remota de los certificados de cliente y servidor (a través de una sesión cifrada), descárguelos desde un recurso compartido de red protegido o distribúyalos manualmente mediante soportes físicos extraíbles. |
| - | Administre activamente los ciclos de vida de sus certificados de administración. |
| No almacene contraseñas de cuentas sin cifrar o sin hash en almacenamiento de aplicaciones (por ejemplo, en hojas de cálculo, recursos compartidos de archivos o sitios de SharePoint). |Establecer los principios de administración de seguridad y directivas de protección del sistema y aplicarlas tooyour entorno de desarrollo. |
| - | Use [5.5 del Kit de herramientas de mejorado mitigación experiencia](https://technet.microsoft.com/security/jj653751) certificado fijar reglas sitios SSL/TLS de tooAzure de tooensure el acceso adecuado. |
| No comparta cuentas ni contraseñas entre los administradores o reutilice contraseñas en diferentes cuentas de usuario o servicios, especialmente las de medios sociales o de otras actividades no administrativas. |Crear un toomanage de cuenta de Microsoft dedicado su suscripción de Azure: una cuenta que no se utiliza para el correo electrónico personal. |
| No envíe archivos de configuración por correo electrónico. |Los perfiles y los archivos de configuración deben instalarse desde un origen de confianza (por ejemplo, una unidad flash USB cifrada), no desde un mecanismo que pueda verse comprometido fácilmente, como el correo electrónico. |
| No use contraseñas de inicio de sesión simples o débiles. |Aplique directivas de contraseña segura, ciclos de expiración (cambiar en el primer uso), tiempos de espera de la consola y bloqueos de cuentas automáticos. Use un sistema de administración de contraseñas de cliente con autenticación multifactor para el acceso al almacén de contraseñas. |
| No exponga toohello de puertos de administración Internet. |Bloquear los puertos de Azure y acceso a la administración de toorestrict direcciones IP. Para obtener más información, vea hello [seguridad de red de Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) notas del producto. |
| - | Use NAP, VPN y firewalls para todas las conexiones de administración. |

## <a name="azure-operations"></a>Operaciones de Azure
Dentro de las operaciones que Microsoft realiza con Azure, los ingenieros de operaciones y el personal de soporte técnico que tienen acceso a los sistemas de producción de Azure usan [equipos de estación de trabajo protegidos con máquinas virtuales](#stand-alone-hardened-workstation-for-management) aprovisionadas en ellos para el acceso a las aplicaciones y a la red corporativa interna (como correo electrónico, intranet, etc.). Todos los equipos de estación de trabajo de administración tienen TPM, unidad de arranque del host de hello está cifrada con BitLocker y están combinadas tooa especial unidad organizativa (OU) en el dominio corporativo principal de Microsoft.

La protección del sistema se aplica mediante la directiva de grupo, con actualizaciones de software centralizadas. Para el análisis y auditoría, registros de eventos (por ejemplo, seguridad y AppLocker) se recopilan desde estaciones de trabajo de administración y se guardan tooa de ubicación central.

Además, dedicados jump-red de Microsoft que requieren autenticación en dos fases están los cuadros de red de producción del tooAzure tooconnect usado.

## <a name="azure-security-checklist"></a>Lista de comprobación de seguridad de Azure
Minimizar el número de Hola de tareas que los administradores pueden realizar en una estación de trabajo protegido ayuda a minimizar la superficie expuesta a ataques hello en su entorno de administración y desarrollo. Hola de uso después de tecnologías toohelp proteger su estación de trabajo protegido:

* Protección de Internet Explorer. Explorador de Internet Explorer de Hello (o cualquier explorador web, para este propósito) es un punto de entrada de la clave para código perjudicial debido tooits amplia interacciones con servidores externos. Revise las directivas de cliente y aplique la ejecución en modo protegido, la deshabilitación de complementos, la deshabilitación de descargas de archivos y el uso del filtrado [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Asegúrese de que se muestran las advertencias de seguridad. Aproveche las ventajas de las zonas de Internet y crear una lista de sitios de confianza para los que ha configurado una protección razonable. Bloquee todos los demás sitios y el código en el explorador, como ActiveX y Java.
* Usuario estándar Se ejecuta como un usuario estándar ofrece una serie de beneficios, hello más importantes de los cuales es que el robo de credenciales de administrador a través de software malintencionado es más difícil. Además, una cuenta de usuario estándar no tiene privilegios elevados en el sistema operativo de hello raíz, y muchas opciones de configuración y las API no tienen acceso de forma predeterminada.
* AppLocker. Puede usar [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict Hola programas y secuencias de comandos que los usuarios pueden ejecutar. Puede ejecutar AppLocker en modo auditoría o cumplimiento. De forma predeterminada, AppLocker tiene una regla de permiso que permite a los usuarios que tienen un toorun de token de administrador todo el código de cliente de Hola. Esta regla existe tooprevent administradores de bloqueo por sí mismos out, y se aplica solo tooelevated símbolos (tokens). Consulte también el tema sobre la integridad del código, que forma parte de la [seguridad fundamental](http://technet.microsoft.com/library/dd348705.aspx) de Windows Server.
* Firma del código. La firma del código de todas las herramientas y scripts que usan los administradores es un mecanismo fácil de administrar para la implementación de directivas de bloqueo de aplicaciones. Valores hash no se escalan con el código de toohello cambios rápidos y rutas de acceso de archivo no proporcionan un alto nivel de seguridad. Las reglas de AppLocker se deben combinar con un PowerShell [directiva de ejecución](http://technet.microsoft.com/library/ee176961.aspx) que solo permite código firmado específico y los scripts toobe [ejecuta](http://technet.microsoft.com/library/hh849812.aspx).
* Directiva de grupo. Crear una directiva de administración global que es la estación de trabajo tooany aplicada de dominio que se usa para la administración (y bloquear el acceso desde todos los demás) y las cuentas de toouser autenticar en esas estaciones de trabajo.
* Aprovisionamiento con seguridad mejorada. Proteger la imagen de protegido de la estación de trabajo de línea base toohelp proteger contra la manipulación. Usar las medidas de seguridad como el cifrado y las imágenes de toostore de aislamiento, máquinas virtuales y las secuencias de comandos y restringir el acceso (quizás use una auditable en/check-desprotección proceso).
* Aplicación de revisiones. Mantener una compilación coherente (o tiene imágenes independientes para el desarrollo, operaciones y otras tareas administrativas), buscar cambios malware habitualmente, mantener acumulación hello toodate y activar solo máquinas cuando se necesitan.
* Cifrado. Asegúrese de que las estaciones de trabajo de administración tienen un TPM toomore habilitar con seguridad [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) y BitLocker. Si usas Windows tooGo, use solo las claves USB cifradas con BitLocker.
* Gobierno. Usar interfaces de Windows de todos los administradores de hello, como el uso compartido de archivos de toocontrol de GPO de AD DS. Incluya las estaciones de trabajo de administración de procesos de auditoría, supervisión y registro. Realice un seguimiento del acceso y uso de los administradores y programadores.

## <a name="summary"></a>Resumen
Usar una configuración de estación de trabajo protegida para administrar los servicios en la nube de Azure, las máquinas virtuales y las aplicaciones puede ayudarle a evitar muchos riesgos y amenazas que pueden derivar de la administración remota de la infraestructura de TI esencial. Azure y Windows proporcionar mecanismos que puede emplear toohelp protección y controlan el comportamiento de las comunicaciones, la autenticación y el cliente.

## <a name="next-steps"></a>Pasos siguientes
Hello siguientes recursos están disponible tooprovide obtener información general sobre Azure y relacionados con servicios de Microsoft, en elementos de toospecific adición al que hace referencia en este documento:

* [Proteger el acceso con privilegios](https://technet.microsoft.com/library/mt631194.aspx) : obtener detalles técnicos de Hola para diseñar y crear una estación de trabajo administrativo segura para la administración de Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) : Obtenga información acerca de las capacidades de la plataforma Windows Azure que protegen Hola tejido de Azure y hello las cargas de trabajo que ejecutan en Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) , donde pueden informar de las vulnerabilidades de seguridad de Microsoft, incluidos los problemas con Azure, o a través de correo electrónico demasiado[secure@microsoft.com](mailto:secure@microsoft.com)
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : no se retrase toodate en hello más reciente en la seguridad de Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
