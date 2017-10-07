---
title: aaaMicrosoft centro de datos Virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toobuild los virtuales del centro de datos de Azure"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Centro de datos virtual de Microsoft Azure
**Microsoft Azure**: muévase más rápido, ahorre dinero, integre aplicaciones locales y datos

## <a name="overview"></a>Información general
Migrar tooAzure de aplicaciones local, incluso sin realizar cambios importantes (un enfoque conocido como "Levantar y mover"), proporciona las organizaciones Hola ventajas de una infraestructura segura y rentable. Sin embargo, toomake Hola más de la agilidad de hello posible con la informática en nube, las empresas deben evolucionar sus ventajas de tootake de arquitecturas de las capacidades de Azure. Microsoft Azure ofrece servicios e infraestructura a gran escala, funcionalidades de calidad empresarial, confiabilidad y numerosas opciones de conectividad híbrida. Los clientes pueden elegir Hola a tooaccess servicios de estas en la nube, ya sea a través de Internet o con ExpressRoute de Azure, que proporciona conectividad de red privada. plataforma de Microsoft Azure Hola permite a los clientes tooseamlessly ampliar su infraestructura en la nube de Hola y crear arquitecturas de varios niveles. Además, los socios de Microsoft proporcionan capacidades mejoradas, ya que ofrece servicios de seguridad y aparatos virtuales que están optimización toorun en Azure.

Este artículo proporciona información general sobre patrones y diseños que pueden ser utilizado toosolve Hola conceptos arquitectónicos de escala, rendimiento y seguridad, que muchos clientes que se enfrentan al pensar en mover masivamente toohello en la nube. Información general sobre cómo distintos roles de TI toofit organizativas en administración de Hola y gobernanza del sistema de hello también se trata, con los requisitos de toosecurity énfasis y optimizar los costos.

## <a name="what-is-a-virtual-data-center"></a>¿Qué es un centro de datos virtual?
Hola primeros días, soluciones de nube estaban diseñados toohost relativamente aislado, aplicaciones, en espectro pública Hola. Este método funcionó bien unos años. Sin embargo, como ventajas Hola de nube que hizo evidentes soluciones y varias cargas de trabajo a gran escala se hospedarse en nube de hello, dirige la seguridad, confiabilidad y rendimiento y costo aspectos de las implementaciones en uno o más regiones pasara a ser fundamentales a lo largo de Hola ciclo de vida del servicio de nube de Hola.

Hello diagrama de implementación de nube siguiente muestra algunos ejemplos de brechas de seguridad (cuadro rojo) y el espacio para los dispositivos virtuales de la red de optimización en cargas de trabajo (cuadro amarillo).

[![0]][0]

Hola centro de datos virtuales (vDC) ha surgido desde esta necesidad de ajuste de escala en las cargas de trabajo de empresa de toosupport y Hola necesario toodeal con problemas de hello introducidos al admitir aplicaciones a gran escala en la nube pública de Hola.

Una vDC no es simplemente hello las cargas de aplicaciones en la nube de hello, pero también red hello, seguridad, administración e infraestructura (por ejemplo, DNS y servicios de directorio). Normalmente también proporciona un tooan de espera de conexión privada red o centro de datos local. Como las cargas de trabajo cada vez más desplazan tooAzure, es importante toothink sobre Hola admite la infraestructura y los objetos situados en estas cargas de trabajo. Pensar detenidamente sobre cómo se estructuran los recursos puede evitar la proliferación de Hola de cientos de "islas de cargas de trabajo" que deben administrarse por separado con el flujo de datos independientes, modelos de seguridad y desafíos de cumplimiento de normas.

Un centro de datos virtual es esencialmente una colección de entidades independientes, aunque relacionadas, con funciones, características e infraestructura de soporte en común. Al ver las cargas de trabajo como un vDC integrado, puede obtener bajo costo debido tooeconomies de escala, seguridad optimizado a través de los datos y el componente de flujo de centralización, junto con operaciones más fáciles, administración y auditorías de cumplimiento.

> [!NOTE]
> Es importante toounderstand que Hola vDC es **no** un producto independiente de Azure, pero la combinación de Hola de diversas características y capacidades demasiado cumple exactamente sus requisitos. vDC es una manera de pensar acerca de las cargas de trabajo y uso de Azure toomaximize los recursos y la capacidad en la nube de Hola. Hola DC virtual es, por tanto, un enfoque modular en cómo toobuild los servicios de TI en hello Azure, respeta organizativas roles y responsabilidades.

Hola vDC le ayudarán a las empresas cargas de trabajo y las aplicaciones en Azure para hello los escenarios siguientes:

-   Hospedaje de varias cargas de trabajo relacionadas
-   Migrar las cargas de trabajo de un tooAzure del entorno local
-   Implementación de requisitos de seguridad y acceso compartido o centralizado para las cargas de trabajo
-   Combinación de DevOps e IT centralizada adecuada para una gran empresa

Hola ventajas de hello toounlock clave de vDC, que es una topología centralizada (concentrador y radios) con una combinación de características de Azure: [red virtual de Azure][VNet], [NSG] [ NSG], [Emparejamiento de VNet][VNetPeering], [rutas definidas por el usuario (UDR)][UDR]y la identidad de Azure con [ Control de acceso Base de roles (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>¿Quién necesita un centro de datos virtual?
Cualquier cliente de Azure que necesita toomove más de un par de cargas de trabajo en Azure puede beneficiarse de pensar acerca del uso de recursos comunes. Dependiendo de la magnitud de hello, incluso única aplicaciones pueden beneficiarse del uso de patrones de Hola y componentes utilizan toobuild una vDC.

Si su organización tiene una seguridad de TI, red, centralizada, o equipo/departamento de cumplimiento, una vDC puede ayudar a aplicar la directiva puntos, la segregación de servicio y garantizar la uniformidad de hello subyacente componentes comunes dando tanto los equipos de la aplicación libertad y control sea adecuado para sus requisitos.

Las organizaciones que buscan tooDevOps pueden utilizar conceptos de vDC hello tooprovide autorizado focos de recursos de Azure y asegurarse de que tienen control total dentro de ese grupo (ya sea suscripción o grupo de recursos en una suscripción común), pero la red de Hola y los límites de seguridad permanecen compatibles tal como se define mediante una directiva centralizada en un concentrador de red virtual y un grupo de recursos.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Consideraciones sobre la implementación de un centro de datos virtual
Al diseñar una vDC, hay varios tooconsider esencial problemas:

-   Servicios de identidad y directorio
-   Infraestructura de seguridad
-   En la nube toohello conectividad
-   Conectividad dentro de la nube de Hola

##### <a name="identity-and-directory-service"></a>*Servicios de identidad y directorio*
Servicios de identidad y directorio son un aspecto clave de todos los datos de recursos, tanto de forma local y en la nube de Hola. Identidad es aspectos relacionados tooall de acceso y autorización tooservices dentro de vDC Hola. toohelp Asegúrese de que sólo los usuarios autorizados y procesos de acceder a su cuenta de Azure y recursos, Azure usa varios tipos de credenciales para la autenticación. Estos incluyen contraseñas (tooaccess Hola cuenta de Azure), las claves de cifrado, firmas digitales y certificados. [*Azure Multi-Factor Authentication* (MFA)][MFA] es una capa adicional de seguridad para el acceso a los servicios de Azure. Azure MFA proporciona autenticación firme con una gama de opciones de comprobación sencilla: llamada de teléfono, mensaje de texto o notificación de aplicación móvil y permiten a los clientes toochoose método de hello que prefieran.

Cualquier empresa de gran tamaño debe toodefine un proceso de administración de identidades que describe la administración de Hola de identidades individuales, su autenticación, autorización, roles y privilegios dentro de o entre vDC Hola. objetivos de Hola de este proceso deben ser tooincrease seguridad y productividad al reducir el costo, tiempo de inactividad y las tareas manuales repetitivas.

La empresas y organizaciones pueden requerir una combinación exigente de servicios para diferentes líneas de negocio (LOB) y los empleados a menudo tienen distintos roles cuando están implicados en proyectos diferentes. Una vDC requiere buena cooperación entre distintos equipos, cada uno con las definiciones de rol específico, tooget sistemas que se ejecutan con buena gobernanza. matriz Hola de responsabilidades y acceso, derechos puede ser muy complejo. La administración de identidad en el centro de datos virtual se implementa a través de [*Azure Active Directory* (AAD)][AAD] y el control de acceso basado en roles (RBAC).

Un servicio de directorio es una infraestructura de información compartida para buscar, gestionar, administrar y organizar los elementos cotidianos y los recursos de red. Estos recursos pueden incluir volúmenes, carpetas, archivos, impresoras, usuarios, grupos, dispositivos y otros objetos. Cada recurso de red de Hola se considera un objeto por el servidor de directorio de Hola. La información sobre un recurso se almacena como una colección de atributos asociada a ese recurso u objeto.

Todos los servicios de negocio en línea de Microsoft dependen de Azure Active Directory (AAD) para el inicio de sesión y otras necesidades de identidad. Azure Active Directory es solución en la nube de administración de acceso e identidades completa y de alta disponibilidad que combina una administración de acceso a aplicaciones, gobernancia de identidades avanzada y servicios de directorio fundamentales. AAD se puede integrar con local de Active Directory tooenable único de sesión para todas las basada en la nube y hospedadas localmente las aplicaciones de (local). atributos de usuario de Hola de local de Active Directory pueden tener tooAAD sincronizan automáticamente.

Un administrador global único es tooassign no son necesario todos los permisos en una vDC. En su lugar, cada departamento específico (o grupo de usuarios o servicios en hello servicio de directorio) puede tener Hola permisos necesarios toomanage sus propios recursos dentro de una vDC. La estructura de permisos requiere un equilibrio. Demasiados permisos pueden disminuir el rendimiento y muy pocos permisos o permisos flexibles pueden aumentar los riesgos de seguridad. Azure Control de acceso basado en roles (RBAC) ayuda a tooaddress este problema, ya que ofrece administración de acceso específico para los recursos de vDC.

##### <a name="security-infrastructure"></a>*Infraestructura de seguridad*
Infraestructura de seguridad, en el contexto de Hola de una vDC es principalmente relacionados toohello segregación de tráfico del hello vDC segmento de red virtual específica, y cómo fluye la entrada y salida toocontrol a lo largo de vDC Hola. Azure se basa en una arquitectura multiinquilino que impide que el tráfico no autorizado y no intencionado entre implementaciones, con aislamiento de red virtual (VNet), listas de control de acceso (ACL), equilibradores de carga y filtros de direcciones IP, junto con directivas de flujo de tráfico. La traducción de direcciones de red (NAT) se usa para separar el tráfico de red interno del tráfico externo.

Hola tejido de Azure asigna recursos de infraestructura tootenant cargas de trabajo y administra las comunicaciones tooand desde máquinas virtuales (VM). Hola hipervisor Azure exige la memoria y el proceso de separación entre las máquinas virtuales y segura a los inquilinos tooguest SO de tráfico de red de las rutas.

##### <a name="connectivity-toohello-cloud"></a>*En la nube toohello conectividad*
Hola vDC necesita conectividad con redes externas toooffer services toocustomers y socios o los usuarios internos. Esto suele significar conectividad toohello Internet pero tooon local redes y centros de datos.

Los clientes pueden generar su toocontrol de directivas de seguridad qué y cómo vDC específico que hospedan servicios son accesibles a/desde Hola a Internet a través de dispositivos de red Virtual (con el filtrado de inspección del tráfico y) y directivas de enrutamiento personalizadas y (filtrado de red Enrutamiento definidos por el usuario y grupos de seguridad de red).

Las empresas suelen necesitan centros de datos de tooconnect VDC tooon local u otros recursos. conectividad de Hello entre redes de Azure y local, por tanto, es un aspecto fundamental al diseñar una arquitectura de efectivo. Las empresas tienen una interconexión entre vDC y local toocreate de dos maneras diferentes en Azure: tránsito a través de Internet de Hola o privadas conexiones directas.

Un [ **Azure VPN de sitio a sitio** ] [ VPN] es un servicio de interconexión sobre Hola Internet entre redes locales y cifra vDC hello, establecida a través de segura conexiones (túneles IPsec/IKE). Conexión de sitio a sitio de Azure es toocreate rápida, flexible y no requiere ninguna adquisición adicional, como todas las conexiones de conectarán a través de internet de Hola.

[**ExpressRoute** ] [ ExR] es un servicio de conectividad de Azure que le permite crear conexiones privadas entre hello y vDC redes locales. Las conexiones ExpressRoute no pasan más de Hola Internet pública y ofrecen una mayor seguridad, confiabilidad y velocidades más altas (arriba Gbps too10) junto con latencia coherente. ExpressRoute es muy útil para VDC, como los clientes pueden obtener ventajas de Hola de reglas de cumplimiento de normas asociadas con conexiones privadas de ExpressRoute.

La implementación de conexiones ExpressRoute implica tomar contacto con un proveedor de servicios de ExpressRoute. Para los clientes que necesitan toostart rápidamente, es común tooinitially uso conectividad de tooestablish VPN de sitio a sitio entre Hola vDC y -los recursos locales y, a continuación, migrar tooExpressRoute conexión.

##### <a name="connectivity-within-hello-cloud"></a>*Conectividad dentro de la nube de Hola*
[Redes virtuales] [ VNet] y [emparejamiento de VNet] [ VNetPeering] es servicios de conectividad dentro de una vDC de redes de hello básico. Una red virtual garantiza un límite de aislamiento para los recursos de vDC natural e intercambio de tráfico de red virtual permite interiores entre distintas redes virtuales dentro de hello misma región de Azure. Control de tráfico dentro de una red virtual y entre redes virtuales necesita toomatch reglas de un conjunto de seguridad especificado a través de listas de Control de acceso ([grupo de seguridad de red][NSG]), [aparatos virtuales de red ] [ NVA]y tablas de enrutamiento personalizadas ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Información general del centro de datos virtual

### <a name="topology"></a>Topología
Hola extendido centro de datos Virtual dentro de una única región de Azure de modelo de concentrador y radios

[![1]][1]

Centro de Hello es zona central Hola que controla e inspecciona el tráfico de entrada o salida entre las diferentes zonas: Internet, de forma local, y Hola radios. topología de concentrador y radio Hola ofrece Hola departamento de TI un directivas de seguridad de tooenforce de manera eficaz en una ubicación central, al tiempo que reduce la posibilidad de Hola de una configuración incorrecta y la exposición.

concentrador de Hello contiene los componentes de servicio comunes Hola utilizados por los radios de Hola. Estos son algunos ejemplos típicos de servicios centrales comunes:

-   infraestructura de Active Directory de Windows Hello (con hello relacionado con el servicio ADFS) necesario para la autenticación de usuario de terceros acceso desde las redes de confianza antes de obtener acceso toohello las cargas de trabajo en Hola radio
-   Un servicio tooresolve los nombres de DNS para cargas de trabajo de hello en hello radios, tooaccess recursos locales y en Internet Hola
-   Una infraestructura de PKI, tooimplement inicio de sesión único en las cargas de trabajo
-   Control de flujo (TCP/UDP) entre los radios de hello e Internet
-   Control de flujo entre radio hello y local
-   Si lo desea, control de flujo entre un radio y otro

Hola vDC reduce el costo total mediante la infraestructura de hello concentrador compartida entre varios radios.

rol de Hola de cada radio puede ser toohost diferentes tipos de cargas de trabajo. Hello radios también pueden proporcionar un enfoque modular para implementaciones repetibles (por ejemplo, desarrollo y pruebas, pruebas de aceptación de usuario, el entorno de preproducción y producción) de hello mismas cargas de trabajo. Hola radios pueden ser usado toosegregate y permitir que varios grupos dentro de su organización (por ejemplo, los grupos de DevOps). Dentro de un radio, es posible toodeploy una carga de trabajo básico o complejos cargas de trabajo de varios niveles con tráfico de control entre las capas de Hola.

##### <a name="subscription-limits-and-multiple-hubs"></a>Límites de la suscripción y múltiples concentradores
En Azure, todos los componentes, cualquier tipo hello, se implementan en una suscripción de Azure. aislamiento de Hola de componentes de Azure en distintas suscripciones de Azure puede satisfacer los requisitos de Hola de LOB diferentes, como la configuración de niveles diferenciados de acceso y autorización.

Una única vDC puede escalar un número toolarge de radios, sin embargo, al igual que con todos los sistemas de TI, no hay límite de plataformas. implementación de base de datos central Hello está enlazado tooa suscripción específica de Azure, que tiene restricciones y límites (por ejemplo, ver el número máximo de emparejamientos de red virtual - [suscripción de Azure y límites de servicio, cuotas y restricciones] [ Limits] para obtener más información). En casos donde los límites pueden ser un problema, puede escalar la arquitectura de hello más allá al extender el modelo de Hola desde un clúster de tooa único concentrador-radios de concentrador y radios. Varios concentradores en una o más regiones de Azure pueden estar conectados entre sí mediante ExpressRoute o una red privada virtual de sitio a sitio.

[![2]][2]

aumenta el esfuerzo de hello costo y la administración del sistema de Hola Hola introducción de varios centros y escalabilidad solo se justifica (ejemplos: límites del sistema o redundancia) y replicación regional (ejemplos: recuperación de desastres o de rendimiento del usuario final). En escenarios que requieren varios concentradores, todos los concentradores de hello deben procurar hello toooffer mismo conjunto de servicios para facilitar la operativa.

##### <a name="interconnection-between-spokes"></a>Interconexión entre los radios
Dentro de un radio único, es posible tooimplement cargas de trabajo de varios niveles complejas. Las configuraciones de varios niveles pueden implementarse utilizando subredes (uno para cada capa) en hello hello filtrado y la misma red virtual flujos mediante los NSG.

En Hola otro lado, un arquitecto puede toodeploy una carga de trabajo de varios nivel entre varias redes virtuales. Con el emparejamiento de VNet, radios pueden conectarse tooother radios Hola mismo concentrador o concentradores diferentes. Un ejemplo típico de este escenario es el caso de hello en servidores de procesamiento de la aplicación están en un radio (VNet), mientras se implementa la base de datos de hello en un radio diferentes (VNet). En este caso, es fácil toointerconnect radios Hola con intercambio de tráfico de red virtual y, por tanto, evitar tránsito a través de concentrador de Hola. Una revisión cuidadosa de la arquitectura y seguridad debe ser realizada tooensure que omitiendo concentrador hello no omite auditoría puntos que solo pueden existir en el concentrador de Hola o seguridad importante.

[![3]][3]

Radios también pueden ser radio tooa interconectados que actúa como concentrador. Este método crea una jerarquía de dos niveles: hello en el nivel superior de hello (nivel 0) se convierten en hello concentrador de radios inferior (nivel 1) de la jerarquía de Hola. radios Hola de vDC necesitan tooforward Hola tráfico toohello concentrador central tooreach red de toohello local o internet. Una arquitectura con dos niveles de concentrador presenta enrutamiento complejo que quita las ventajas de Hola de una relación simple radial.

Aunque Azure permite topologías complejas, uno de los principios básicos de hello del concepto de vDC hello es repetibilidad y la simplicidad. toominimize esfuerzo de administración, diseño radial simple de hello es hello recomendada vDC arquitectura de referencia.

### <a name="components"></a>Componentes
Un centro de datos virtual se compone de cuatro tipos de componentes básicos: **infraestructura**, **redes perimetrales**, **cargas de trabajo** y **supervisión**.

Cada tipo de componente consta de varias características de Azure y recursos. Los controladores de dominio virtuales se compone de instancias de varios tipos de componentes y varias variaciones de hello mismo tipo de componente. Por ejemplo, puede tener muchas instancias de cargas de trabajo diferentes, separadas lógicamente, que representan las distintas aplicaciones. Puede utilizar estos distintos tipos de componentes e instancias tooultimately compilar Hola vDC.

[![4]][4]

Hello arquitectura de alto nivel anterior de una vDC muestra distintos tipos de componentes utilizados en distintas zonas de topología de concentrador radios Hola. diagrama de Hello muestra los componentes de infraestructura en distintas partes de la arquitectura de Hola.

Como procedimiento recomendado (para centros de datos locales y virtuales), los derechos de acceso y privilegios deben estar basados en grupos. Trabajar con grupos, en lugar de usuarios individuales le ayuda a mantener las directivas de acceso de forma coherente a través de los distintos equipos y ayuda a minimizar los errores de configuración. Asignar y quitar usuarios tooand de grupos adecuados y le ayuda a mantener actualizados los privilegios de Hola de un usuario específico.

Cada grupo de roles debe tener un prefijo único en los nombres que hace fácil tooidentify el grupo al que está asociado a las cargas de trabajo. Por ejemplo, una carga de trabajo que hospeda un servicio de autenticación podría tener grupos denominados *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps y AuthServiceInfraOps.* Del mismo modo para centralizada roles o roles no relacionada con el servicio específico de tooa, podría estar precedidos de "Corp" *CorpNetOps* por ejemplo.

Muchas organizaciones usan una variación de hello siguientes grupos tooprovide un desglose de las funciones principal:

-   Hola *grupo de TI central (Corp)* tiene componentes de infraestructura (por ejemplo, redes y seguridad) del toocontrol Hola de derechos de propiedad y, por tanto, necesita el rol de hello toohave de colaborador de suscripción de hello (y tener el control de concentrador de Hello) y los derechos de colaborador en hello radios de red. Las organizaciones de gran tamaño con frecuencia dividen estas responsabilidades de administración entre varios equipos como: un grupo de operaciones de red (CorpNetOps, con el foco exclusivo en la red) y un grupo de operaciones de seguridad (CorpSecOps, responsable de las directivas de seguridad y firewall). En este caso, dos grupos distintos necesitan toobe creado para la asignación de estos roles personalizados.
-   Hola *dev & grupo de prueba (AppDevOps)* tiene cargas de trabajo de hello responsabilidad toodeploy (aplicaciones o servicios). Este grupo toma Hola de colaborador de la máquina Virtual para las implementaciones de IaaS o uno o roles del colaborador PaaS más (vea [funciones integradas para controlar el acceso Azure Role-Based][Roles]). Hola, opcionalmente, desarrollo y equipo de pruebas que necesite toohave visibilidad en las directivas de seguridad (NSG) y directivas de enrutamiento (UDR) dentro de concentrador de Hola o un radio específico. Por lo tanto, en roles de toohello de adición de colaborador para cargas de trabajo, este grupo también necesitaría rol Hola de lector de red.
-   Hola *group de funcionamiento y mantenimiento (CorpInfraOps o AppInfraOps)* tienen Hola la responsabilidad de administrar cargas de trabajo de producción. Este grupo debe toobe un colaborador de suscripción en las cargas de trabajo en las suscripciones de producción. Algunas organizaciones también pueden evaluar si necesita un grupo de equipo de soporte técnico de extensión adicionales con rol de Hola de colaborador de suscripción en producción y en la suscripción de concentrador central de hello, en orden toofix posibles problemas de configuración de producción de hello entorno.

Una vDC estructurada de forma que los grupos creados para los grupos de TI centrales Hola administración central de hello tienen grupos correspondientes en el nivel de carga de trabajo de Hola. Además toomanaging recursos solo Hola central TI grupos de concentradores sería capaz de toocontrol externos acceso y permisos de nivel superior en la suscripción de Hola. Sin embargo, los grupos de cargas de trabajo sería toocontrol capaz de recursos y los permisos de su red virtual de forma independiente en TI Central.

Hola vDC necesidades toobe con particiones toosecurely host varios proyectos en diferentes líneas de negocios (LOB). Todos los proyectos requieren diferentes entornos aislados (desarrollo, UAT, producción). El uso de suscripciones de Azure independientes para cada uno de estos entornos proporciona un aislamiento natural.

[![5]][5]

Hello diagrama anterior muestra hello relación entre proyectos de una organización, los usuarios, grupos y los entornos de Hola donde hello Azure componentes se implementan.

Normalmente, en TI, un entorno (o nivel) es un sistema en el que se implementan y ejecutan varias aplicaciones. Las empresas de tamaño grande usan un entorno de desarrollo (en el que se realizan originalmente los cambios y pruebas) y un entorno de producción (el que los usuarios finales utilizan). Esos entornos están separados, a menudo con varios entornos entre ellos de ensayo tooallow fase de implementación (implementación), las pruebas y reversión en caso de problemas. Arquitecturas de implementación varían considerablemente, pero normalmente se siguen proceso básico de Hola de a partir de desarrollo (desarrollo) y terminando en producción (PROD).

Una arquitectura común para estos tipos de entornos de varios niveles se compone de DevOps (desarrollo y pruebas), UAT (ensayo) y entornos de producción. Las organizaciones pueden aprovechar único o AD de Azure de varios inquilinos toodefine acceso y derechos de entornos de toothese. Hello diagrama anterior muestra un caso de que haya dos diferentes se usan los inquilinos de Azure AD: uno para DevOps y UAT, hello y otro exclusivamente para la producción.

Hola presencia de Azure AD diferentes inquilinos exige la separación de hello entre entornos. Hola el mismo grupo de usuarios (por ejemplo, TI Central) necesita tooauthenticate mediante un tooaccess URI diferentes un inquilino de AD diferente modificar roles de Hola o permisos de hello ya sea DevOps o entornos de producción de un proyecto. presencia de hello entornos diferentes, otro usuario autenticación tooaccess reduce posibles interrupciones y otros problemas causados por errores humanos.

#### <a name="component-type-infrastructure"></a>Tipo de componente: infraestructura
Este tipo de componente es donde reside la mayor parte de la compatibilidad de la infraestructura de Hola. También es donde los equipos de TI central, seguridad y cumplimiento dedican la mayor parte de su tiempo.

[![6]][6]

Componentes de la infraestructura proporcionan una interconexión entre distintos componentes de un vDC de Hola y están presentes en el concentrador de Hola y Hola radios. Hello responsable de la administración y mantenimiento de componentes de la infraestructura de Hola se suele asignar toohello central TI o equipo de seguridad.

Una de las tareas principales de Hola Hola, equipo de infraestructura de TI es coherencia de hello tooguarantee de esquemas de direcciones IP a través de la empresa de Hola. Hola privada IP dirección espacio asignado toohello vDC necesita toobe coherente y no se superponen con direcciones IP privadas asignadas en las redes locales.

Mientras NAT en hello enrutadores perimetrales local o en Azure entornos pueden evitar conflictos de direcciones IP, agrega componentes de la infraestructura de complicaciones tooyour. Simplicidad de administración es uno de sus principales objetivos de Hola de vDC, por lo que usar NAT toohandle IP preocupaciones no es una solución recomendada.

Componentes de la infraestructura contienen Hola siguiente funcionalidad:

-   [**Servicios de identidad y directorio**][AAD]. Tipo de recurso de acceso tooevery en Azure se controla mediante una identidad que se almacenan en un servicio de directorio. almacenes de servicio de directorio de Hello no solo Hola lista de usuarios, sino que también Hola tooresources de derechos de acceso en una suscripción de Azure específica. Estos servicios pueden existir solo en la nube, o se pueden sincronizar con la identidad local almacenada en Active Directory.
-   [**Red virtual**][VPN]. Las redes virtuales son uno de los componentes principales de una vDC y habilitar toocreate un límite de aislamiento de tráfico en hello plataforma Windows Azure. Una red virtual se compone de uno o varios segmentos de red virtual, cada uno con un prefijo de red IP específico (una subred). Hola red Virtual define un área de perímetro interno en máquinas virtuales de IaaS y PaaS servicios pueden establecer comunicaciones privadas. Máquinas virtuales (y los servicios de PaaS) en una red virtual no se puede comunicar directamente tooVMs (y los servicios de PaaS) en una red virtual diferente, aunque ambas redes virtuales se crean por Hola mismo cliente, en Hola misma suscripción. El aislamiento consiste en una propiedad fundamental que garantiza que las máquinas virtuales del cliente y la comunicación sigan siendo privadas en una red virtual.
-   [**UDR**][UDR]. Enruta el tráfico en una red Virtual de forma predeterminada en función de la tabla de enrutamiento de sistema de Hola. Una ruta para definir el usuario es una tabla de enrutamiento personalizada que los administradores de red pueden asociar tooone o más subredes toooverwrite Hola comportamiento de la tabla de enrutamiento de sistema de Hola y definir una ruta de acceso de comunicación en una red virtual. presencia de Hola de UDRs garantiza que el tráfico de salida de hello radio atraviesan una VM personalizadas específicas o dispositivos de red Virtual y equilibradores de carga presentes en el concentrador de hello en radios Hola.
-   [**NSG**][NSG]. Un grupo de seguridad de red (NSG) es una lista de reglas de seguridad que actúa como filtro de tráfico en direcciones IP de origen y destino, protocolos y puertos IP de origen y destino. Hola NSG puede ser aplicada tooa subred, una tarjeta NIC Virtual asociada a una máquina virtual de Azure, o ambos. Hola NSG son esencial tooimplement un control de flujo correctos en concentrador de Hola y Hola radios. nivel de Hola de seguridad de hello NSG es una función de los puertos que abrir y su finalidad. Los clientes pueden aplicar filtros adicionales por VM con firewalls basados en host, como IPtables u Hola Firewall de Windows.
-   **DNS**. resolución de nombres de Hola de recursos en redes virtuales de una vDC Hola se proporciona a través de DNS. ámbito de Hola de resolución de nombres predeterminado de hello DNS es toohello limitada red virtual. Por lo general, un servicio DNS personalizado debe toobe implementado en el concentrador de hello como parte de los servicios de common, pero a los consumidores Hola principal de los servicios DNS residen en radio Hola. Si es necesario, los clientes pueden crear una estructura jerárquica de DNS con la delegación de DNS zonas toohello radios.
-   [**Administración de la suscripción][SubMgmt] y del [Grupo de recursos][RGMgmt]**. Una suscripción define un límite natural toocreate varios grupos de recursos en Azure. Los recursos de una suscripción se ensamblan juntos en contenedores lógicos llamados grupos de recursos. Hola grupo de recursos representa un recurso de hello tooorganize grupo lógico de un vDC.
-   [**RBAC**][RBAC]. A través de RBAC, es posible toomap rol organizativo junto con derechos tooaccess Azure recursos específicos, lo que permite tooonly usuarios toorestrict un determinado subconjunto de acciones. Con RBAC, puede conceder acceso mediante la asignación de hello rol adecuado toousers, grupos y aplicaciones dentro de ámbito relevantes de Hola. ámbito de Hola de una asignación de roles puede ser una suscripción de Azure, un grupo de recursos o un único recurso. RBAC permite la herencia de permisos. Un rol asignado en un ámbito primario también concede acceso toohello los elementos secundarios incluidos en él. Usar RBAC, puede separar los derechos y conceda solo Hola mucha toousers de acceso que necesitan tooperform sus trabajos. Por ejemplo, un empleado de uso RBAC toolet administrar máquinas virtuales en una suscripción, mientras que otro puede administrar bases de datos de SQL en hello misma suscripción.
-   [**Emparejamiento de redes virtuales**][VNetPeering]. Hello usa la característica fundamentales toocreate Hola infraestructura de una vDC es emparejamiento de red virtual, un mecanismo que conecta dos redes virtuales (redes virtuales) en hello misma región a través de la red de Hola Hola Azure del centro de datos.

#### <a name="component-type-perimeter-networks"></a>Tipo de componente: redes perimetrales
[Red perimetral] [ DMZ] componentes (también conocido como una red DMZ) le permiten tooprovide conectividad de red con su redes del centro de datos físico, junto con cualquier tooand de conectividad de Internet de Hola o en local. También es donde probablemente los equipos de red y seguridad empleen la mayor parte de su tiempo.

Los paquetes entrantes deben fluyen a través de dispositivos de seguridad de hello en el concentrador de hello, como firewall de hello, identificadores y direcciones IP, antes de llegar a los servidores back-end de hello en hello radios. Paquetes de vinculado a Internet de las cargas de trabajo de hello también deben fluyen a través de dispositivos de seguridad de hello en la red perimetral de hello para la aplicación de directivas, inspección y auditoría fines, antes de abandonar la red Hola.

Componentes de la red perimetral proporcionan Hola siguientes características:

-   [Redes virtuales][VNet], [UDR][UDR], [NSG][NSG]
-   [Aplicación virtual de red][NVA]
-   [Equilibrador de carga][ALB]
-   [Application Gateway][AppGW] / [WAF][WAF]
-   [Direcciones IP públicas][PIP]

Por lo general, Hola central TI y los equipos de seguridad tienen la responsabilidad de la definición de requisitos y las operaciones de redes perimetrales de Hola.

[![7]][7]

Hello diagrama anterior muestra el cumplimiento Hola de dos los perímetros con acceso toohello internet y una implementación local de red, ambos residentes en el concentrador de Hola. En un único concentrador, puede escalar toointernet de red perimetral de hello toosupport grandes cantidades de LOB, con varias granjas de servidores de seguridad de aplicaciones de Web (WAFs) o firewalls.

[**Redes virtuales** ] [ VNet] concentrador Hola normalmente se basa en una red virtual con varias subredes toohost Hola tipo diferente de los servicios de filtrado e inspeccionando el tráfico tooor de Hola a internet a través de NVAs, WAFs, y las puertas de enlace de la aplicación de Azure.

[**UDR**][UDR] Con UDR, los clientes pueden implementar un firewall, IDS/IPS y otras aplicaciones virtuales y enrutar el tráfico de red a través de estas aplicaciones de seguridad para la aplicación de directivas de límites de seguridad, auditoría e inspección. UDRs pueden crearse en ambos tooguarantee de radios de hello y concentrador de Hola que transita de tráfico a través de Hola VM personalizadas específicos, dispositivos de red Virtual y equilibradores de carga de vDC Hola. tooguarantee que el tráfico generado a partir de máquinas virtuales residentes en hello radio tránsito toohello correcta aparatos virtuales, es necesario un UDR toobe establecido en subredes de Hola de radio de hello estableciendo la dirección IP front-end de Hola de equilibrador de carga interno de hello como Hola de próximo salto. equilibrador de carga interno de Hello distribuye aparatos virtuales Hola tráfico interno toohello (grupo de back-end de equilibradores de carga).

[![8]][8]

[**Dispositivos virtuales de red** ] [ NVA] en el concentrador de hello, Hola red perimetral con toohello de acceso a internet normalmente se administra a través de una granja de servidores de seguridad o Firewalls de aplicación Web (WAFs).

LOB diferentes normalmente utilizan muchas aplicaciones web, y estas aplicaciones suelen toosuffer desde varias vulnerabilidades y puntos débiles potenciales. Firewalls de las aplicaciones Web son que un tipo especial de producto usado toodetect ataques en aplicaciones web (HTTP/HTTPS) en mayor profundidad que un servidor de seguridad genérico. En comparación con la tecnología de firewall tradición, WAFs tienen un conjunto de servidores de web interna de características específicas tooprotect frente a amenazas.

Una granja de servidores de firewall es grupo de servidores de seguridad que trabajan en tándem en hello mismo comunes de administración con un conjunto de reglas tooprotect hello las cargas de trabajo hospedados en radios hello y redes locales tooon con control de acceso. Una granja de servidores de firewall se menor especializado software comparado con un WAFS, pero tiene una gran aplicación ámbito toofilter e inspeccionar de cualquier tipo de tráfico de entrada y salida. Las granjas de servidores de Firewall se implementan normalmente en Azure a través de dispositivos virtuales de red (NVAs), que están disponibles en hello Azure marketplace.

Se recomienda toouse una conjunto de NVAs para tráfico que se origina en Internet de hello y otro para el tráfico que se origina en local. Utilizar únicamente un conjunto de NVAs para ambos es un riesgo de seguridad, tal y como no proporciona ningún perímetro de seguridad entre dos conjuntos de Hola de tráfico de red. Usar NVAs independientes reduce la complejidad de hello de la comprobación de las reglas de seguridad y deja claro qué reglas corresponden toowhich solicitud de red entrante.

La mayoría de las empresas de tamaño grande administran varios dominios. DNS de Azure puede ser toohost usado Hola registros DNS para un dominio en particular. Como ejemplo, hello dirección de IP Virtual (VIP) de equilibrador de carga externo Azure hello (o WAFs Hola) se puede registrar en el registro de un registro DNS de Azure Hola.

[**Azure Load Balancer**][ALB] El equilibrador de carga de Azure ofrece un servicio de nivel 4 (TCP, UDP) de alta disponibilidad que puede distribuir el tráfico entrante entre instancias del servicio definidas en un conjunto de equilibrio de carga. El tráfico enviado toohello equilibrador de carga de los puntos de conexión front-end (puntos de conexión IP públicas o privadas puntos de conexión IP) se puede redistribuir con o sin el conjunto de tooa de traducción de direcciones del grupo de direcciones IP de back-end (ejemplos que se va a; Dispositivos de red virtuales o máquinas virtuales).

Cuando un sondeo no deja de equilibrador de carga toorespond Hola enviar instancia incorrecto de tráfico toohello y equilibrador de carga de Azure puede sondear el estado Hola de hello así varias instancias del servidor. En una vDC, tenemos presencia de Hola de un equilibrador de carga externo en el concentrador de hello (por ejemplo, equilibrar Hola tráfico tooNVAs) y, en radios hello (tooperform tareas como equilibrar el tráfico entre diferentes máquinas virtuales de una aplicación de varios niveles).

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway es una aplicación virtual dedicada que cuenta con un controlador de entrega de aplicaciones (ADC) que se ofrece como servicio y que proporciona numerosas funcionalidades de equilibrio de carga de nivel 7 para la aplicación. Permite productividad de granja de servidores web toooptimize mediante la descarga de CPU intensivo SSL terminación toohello aplicación puerta de enlace. También proporciona otras capacidades de enrutamiento de capa 7 incluida round-robin distribución del tráfico entrante, afinidad de sesión basado en cookies, enrutamiento basado en la ruta de acceso de direcciones URL y Hola capacidad toohost varios sitios Web detrás de una sola puerta de enlace de la aplicación. Un servidor de aplicaciones web (WAFS) también se proporciona como parte de la puerta de enlace de aplicaciones de hello WAFS SKU. Esta SKU proporciona protección de aplicaciones tooweb vulnerabilidades de web y vulnerabilidades de seguridad comunes. Application Gateway puede configurarse como una puerta de enlace orientada a Internet, una puerta de enlace solo para uso interno o una combinación de las dos. 

[**Direcciones IP públicas** ] [ PIP] Hola de habilitar características de Azure algunas tooassociate servicio extremos tooa dirección IP pública que permita tooyour recursos toobe acceso desde internet. Este extremo usa la dirección interna de traducción de direcciones de red (NAT) tooroute tráfico toohello y el puerto en hello red virtual de Azure. Esta ruta de acceso es la forma principal de hello toopass tráfico externo en la red virtual de Hola. direcciones IP públicas de Hello pueden ser configurado toodetermine qué tráfico se pasa en, y cómo y dónde se traduce en toohello de red virtual.

#### <a name="component-type-monitoring"></a>Tipo de componente: supervisión
Componentes de supervisión proporcionan visibilidad y las alertas de todos los Hola otros tipos de componentes. Todos los equipos deben tener acceso toomonitoring para los componentes de Hola y servicios que tienen acceso. Si tiene un equipos de escritorio o las operaciones de ayuda centralizada, tienen datos toohello toohave integrado acceso que proporciona estos componentes.

Recursos hospedan en Azure ofrece diferentes tipos de registro y la supervisión de comportamiento de hello tootrack de servicios de Azure. Gobierno y el control de cargas de trabajo en Azure es según no solo en recopilar datos de registro, pero también las acciones de tootrigger de capacidad Hola basadas en eventos notificados específicos.

Hay dos tipos principales de registros en Azure:

-   [**Registros de actividad** ] [ ActLog] (conocido también como "Registro operativo") proporcionan una visión general de las operaciones de Hola que se realizaron en los recursos Hola suscripción de Azure. Estos registros informa de los eventos de plano de control de Hola para las suscripciones. Todos los recursos de Azure generan registros de auditoría.

-   [**Registros de diagnóstico de Azure** ] [ DiagLog] son registros generados por un recurso que proporcionan datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso. contenido de Hola de estos registros varía según el tipo de recurso.

[![9]][9]

En una vDC, es muy importante tootrack hello NSG registros, especialmente esta información:

-   [**Registros de eventos**][NSGLog]: proporciona información sobre qué reglas NSG son tooVMs aplicados y roles de una instancia en función de la dirección MAC.
-   [**Registros de contador**][NSGLog]: realiza un seguimiento de cuántas veces cada NSG regla fue ejecutado toodeny o permitir el tráfico.

Todos los registros se pueden almacenar en cuentas de Azure Storage con fines de auditoría, análisis estático o copia de seguridad. Cuando los registros de Hola se almacenan en una cuenta de almacenamiento de Azure, los clientes pueden usar diferentes tipos de marcos de trabajo tooretrieve, preparación, analizar y visualizar este estado de hello tooreport los datos y el mantenimiento de recursos de nube.

Las grandes empresas deben ya han adquirido un marco estándar para la supervisión de sistemas locales y puede extender que framework toointegrate registros generan por las implementaciones de nube. Para organizaciones que desean tookeep todos Hola inicio de sesión en la nube hello, [Microsoft Operations Management Suite (OMS)] [ OMS] es una excelente opción. Puesto que OMS se implementa como un servicio basado en la nube, puede hacer que funcione rápidamente con una inversión mínima en servicios de infraestructura. OMS puede también integrarse con componentes de System Center, como System Center Operations Manager tooextend sus inversiones de administración existente en la nube de Hola.

Análisis de registros de OMS es un componente de hello OMS framework toohelp recopilar, correlacionar, búsqueda y actuar en los datos de rendimiento y registro generan por sistemas operativos, aplicaciones, en la nube infraestructura componentes. Ofrece a los clientes visión operativa en tiempo real mediante búsqueda integrada y paneles personalizados tooanalyze todos los registros de Hola a través de todas las cargas de trabajo en una vDC.

#### <a name="component-type-workloads"></a>Tipo de componente: cargas de trabajo
Los componentes de carga de trabajo son donde residen los servicios y aplicaciones reales. También es donde los equipos de desarrollo de aplicaciones dedican la mayor parte de su tiempo.

posibilidades de carga de trabajo de Hello son realmente infinitas. siguiente Hola es algunos de los tipos posibles de la carga de trabajo hello:

**Aplicaciones de líneas de negocio internas**

Aplicaciones de línea de negocio son la operación en curso toohello críticos de equipo las aplicaciones de una empresa. Las aplicaciones de línea de negocio tienen algunas características comunes:

-   **Interactividad**. Las aplicaciones de línea de negocio son interactivas por naturaleza: los datos se captan y se devuelven resultados e informes.
-   **Controladas por datos**. Las aplicaciones LOB son intensivo con bases de datos de acceso frecuente toohello u otra unidad de almacenamiento de datos.
-   **Integradas**. Integración de la oferta de aplicaciones con otros sistemas dentro o fuera de la organización de Hola de LOB.

**A los sitios web (accesibles desde Internet o Internal) nuestros clientes** mayoría de las aplicaciones que interactúan con hello Internet es sitios web. Azure ofrece Hola capacidad toorun un sitio web en una VM de IaaS o desde una [aplicaciones Web de Azure] [ WebApps] sitio (PaaS). Las aplicaciones Web de Azure admite la integración con redes virtuales que permiten la implementación de Hola de hello las aplicaciones Web en radio Hola de una vDC. Con hello integración de red virtual, no es necesario tooexpose un punto de conexión de Internet para las aplicaciones pero puede usar Hola recursos internet no es enrutable dirección privada de la red privada virtual en su lugar.

**Datos/análisis big** al tooscale tooa gran volumen necesita datos, las bases de datos no pueden ajustar correctamente. Tecnología de Hadoop ofrece un sistema toorun distribuida consultas en paralelo en gran número de nodos. Los clientes tienen cargas de trabajo de hello opción toorun datos en las máquinas virtuales IaaS o PaaS ([HDInsight][HDI]). HDInsight admite la implementación en una red virtual basada en ubicación, puede ser clúster tooa implementada en un radio de vDC Hola.

**Eventos y mensajería**
[Azure Event Hubs][EventHubs] es un servicio de ingesta de telemetría de hiperescala que recopila, transforma y almacena millones de eventos. Como una plataforma de transmisión por secuencias distribuida, se ofrece una latencia baja y retención de tiempo configurable, permitiéndole tooingest grandes cantidades de telemetría en Azure y leen datos desde varias aplicaciones. Con Event Hubs, una única transmisión puede admitir canalizaciones en tiempo real y basadas en lotes.

Se puede implementar un servicio de mensajería en la nube altamente confiable entre aplicaciones y servicios con [Azure Service Bus][ServiceBus] que ofrece mensajería asincrónica entre cliente y servidor, junto con mensajería de estructura primero en entrar primero en salir (FIFO) y funcionalidades de publicación y suscripción.

[![10]][10]

### <a name="multiple-vdc"></a>Múltiples centros de datos virtuales
Hasta ahora, este artículo se ha centrado en una única vDC, que describe los componentes básicos de Hola y arquitectura que contribuyen vDC resistente tooa. Características de Azure como conjuntos de disponibilidad de equilibrio, NVAs, de carga de Azure, conjuntos de escalas, junto con otros mecanismos de contribuyan sistema tooa que le permiten toobuild niveles de SLA sólidos en los servicios de producción.

Sin embargo, una única vDC se hospeda en una única región e interrupción toomajor vulnerable que podrían afectar a toda esa región. Los clientes que desee tooachieve SLA alto necesitan servicios de hello tooprotect a través de las implementaciones de hello mismo proyecto en dos (o más) VDC, coloca en diferentes regiones.

En cuestiones de tooSLA de adición, hay varios escenarios comunes donde implementar varios VDC tiene sentido:

-   Presencia regional y global
-   Recuperación ante desastres
-   Tráfico de toodivert mecanismo entre el controlador de dominio

#### <a name="regionalglobal-presence"></a>Presencia regional y global
Los centros de datos de Azure están presentes en varias regiones de todo el mundo. Al seleccionar varios centros de datos de Azure, los clientes necesitan tooconsider dos factores relacionados: distancias geográficas y latencia. Los clientes necesitan la distancia geográfica de hello tooevaluate entre VDC hello y distancia de hello entre vDC hello y los usuarios finales de hello, mejor experiencia de usuario de toooffer Hola.

Hola región de Azure donde se hospeda VDC también necesitará tooconform con requisitos de las normas establecidos por cualquier jurisdicción en la que opera la organización.

#### <a name="disaster-recovery"></a>Recuperación ante desastres
implementación de Hola de un plan de recuperación ante desastres es muy relacionados toohello tipo de carga de trabajo que se trate y el estado de carga de trabajo de hello capacidad toosynchronize Hola entre VDC diferentes. Lo ideal es que, la mayoría de los clientes desea toosynchronize datos de aplicaciones entre las implementaciones que se ejecuta en dos diferentes VDC tooimplement una conmutación por error rápida mecanismo. Mayoría de las aplicaciones es toolatency confidencial y que podría hacer posible tiempo de espera y retraso en la sincronización de datos.

La sincronización o la supervisión de latido de aplicaciones en diferentes centros de datos virtuales exige comunicación entre ellos. Dos centros de datos virtuales en regiones diferentes pueden estar conectados a través de:

-   Privada el emparejamiento de ExpressRoute centros de vDC Hola una vez conectado toohello mismo circuito de ExpressRoute
-   varios circuitos ExpressRoute conectan a través de la red troncal corporativa y la malla vDC circuitos ExpressRoute de toohello conectado
-   Conexiones VPN de sitio a sitio entre los concentradores de los centros de datos virtuales en cada región de Azure

Hola conexión ExpressRoute suele mecanismo Hola preferido de vencimiento más ancho de banda y latencia coherente cuando tránsito por hello red troncal de Microsoft.

Una aplicación distribuida entre dos (o más) VDC diferentes ubicado en regiones diferentes no hay ningún toovalidate receta mágica. Los clientes deben ejecutar tooverify Hola latencia de red calificación pruebas y ancho de banda de las conexiones de Hola y de destino si la replicación de datos sincrónica o asincrónica es adecuada y puede ser el objetivo de tiempo de recuperación óptimo de hello (RTO) para su cargas de trabajo.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Tráfico de toodivert mecanismo entre el controlador de dominio
Una técnica eficaz toodivert Hola el tráfico entrante en una tooanother de controlador de dominio se basa en DNS. [Azure Traffic Manager] [ TM] usa Hola sistema de nombres de dominio (DNS) mecanismo toodirect hello para el usuario final tráfico toohello más adecuado extremo público en una vDC específica. A través de sondeos, Traffic Manager comprueba periódicamente el estado del servicio Hola de extremos públicos en VDC diferentes y, en caso de error de esos puntos de conexión, lo enruta automáticamente vDC secundaria toohello.

Traffic Manager funciona en Azure extremos públicos y se puede utilizar, por ejemplo, tooAzure de tráfico toocontrol/desviar las máquinas virtuales y aplicaciones Web en hello adecuado vDC. Traffic Manager es resistente incluso de cara de Hola de un error de la región de Azure completo y puede controlar la distribución de Hola de tráfico de usuario para los extremos de servicio en VDC diferentes en función de varios criterios (por ejemplo, error de un servicio en un vDC específico, o para seleccionar Hola vDC con menor latencia de red hello para el cliente de hello).

### <a name="conclusion"></a>Conclusión
Hola centro de datos Virtual es una migración de enfoque toodata center en la nube de Hola que utiliza una combinación de características y capacidades toocreate una arquitectura escalable de Azure que maximiza el uso de recursos de nube, lo que reduce los costos y simplificar el sistema Gobierno de. concepto de vDC Hola se basa en una topología de concentrador radios, proporciona los servicios compartidos comunes en el concentrador de Hola y permitir aplicaciones y cargas de trabajo específicas en hello radios. Una vDC coincide con la estructura del Hola de roles de la empresa, donde diferentes departamentos (TI Central, DevOps, funcionamiento y mantenimiento) funcionan conjuntamente, cada uno con una lista específica de los roles y tareas. Una vDC satisface los requisitos de Hola para una migración "Elevación y Mayús", pero también proporciona muchas ventajas toonative implementaciones en la nube.

## <a name="references"></a>Referencias
Hola siguientes características se ha descrito en este documento. Haga clic en hello vínculos toolearn más.

| | | |
|-|-|-|
|Características de red|Equilibrio de carga|Conectividad|
|[Redes virtuales de Azure][VNet]</br>[Grupos de seguridad de red][NSG]</br>[Registros NSG][NSGLog]</br>[Enrutamiento definido por el usuario][UDR]</br>[Aplicaciones virtuales de red][NVA]</br>[Direcciones IP públicas][PIP]|[Azure Load Balancer (L3) ][ALB]</br>[Application Gateway (L7) ][AppGW]</br>[Firewall de aplicaciones web][WAF]</br>[Azure Traffic Manager][TM] |[Emparejamiento de redes virtuales][VNetPeering]</br>[Red privada virtual][VPN]</br>[ExpressRoute][ExR]
|Identidad</br>|Supervisión</br>|Prácticas recomendadas</br>|
|[Azure Active Directory][AAD]</br>[Multi-Factor Authentication][MFA]</br>[Control de acceso basado en roles][RBAC]</br>[Roles predeterminados de AAD][Roles] |[Registros de actividad][ActLog]</br>[Registros de diagnóstico][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Procedimientos recomendados en redes perimetrales][DMZ]</br>[Administración de suscripciones][SubMgmt]</br>[Administración de grupos de recursos][RGMgmt]</br>[Límites de la suscripción de Azure][Limits] |
|Otros servicios de Azure|
|[Azure Web Apps][WebApps]</br>[HDInsights (Hadoop) ][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>Pasos siguientes
 - Explorar [emparejamiento de VNet][VNetPeering], Hola tecnología subyacente para vDC concentrador y radio diseños
 - Implemente [AAD] [ AAD] tooget partió [RBAC] [ RBAC] exploración
 - Desarrollar un modelo de administración de recursos y la suscripción y RBAC modelar toomeet Hola estructura, requisitos y las directivas de su organización. Planeación de la actividad más importante de Hello. Siempre que resulte práctico, planee reorganizaciones, fusiones, nuevas líneas de producto, etc.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Ejemplos de superposición de componentes" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Ejemplo genérico de centro de datos virtual con concentrador y radios"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Clúster de concentradores y radios"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Radio a radio"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Diagrama de nivel de bloque de hello vDC"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Usuarios, grupos, suscripciones y proyectos"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Diagrama de infraestructura de alto nivel"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Diagrama de infraestructura de alto nivel"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "Emparejamiento de redes virtuales y redes perimetrales"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Diagrama de alto nivel para supervisión"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Diagrama de alto nivel para cargas de trabajo"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
