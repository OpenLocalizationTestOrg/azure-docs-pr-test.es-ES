---
title: "aaaOverview y arquitectura de SAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "Introducción a la arquitectura de cómo tooDeploy SAP HANA en Azure (instancias de gran tamaño)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Introducción y arquitectura de SAP HANA en Azure (instancias grandes)

## <a name="what-is-sap-hana-on-azure-large-instances"></a>¿Qué es SAP HANA en Azure (instancias grandes)?

SAP HANA en Azure (instancia grande) es una solución única tooAzure. Por otra parte tooproviding máquinas virtuales de Azure para el propósito de Hola de implementación y ejecución de SAP HANA, Azure ofrece Hola posibilidad toorun e implementar SAP HANA en servidores de reconstrucción completa que están dedicado tooyou como un cliente. Hola SAP HANA en la solución de Azure (instancias de gran tamaño) se basa en hardware sin sistema operativo de servidor/host no compartidos asignado tooyou como un cliente. el hardware del servidor Hello se incrusta en las marcas más grandes que contienen compute/servidor, la red y la infraestructura de almacenamiento. De manera combinada, cuenta con la certificación de HANA TDI. oferta de servicio de Hola de SAP HANA en Azure (instancias de gran tamaño) ofrece diversos tamaños a partir de unidades con 72 CPU y toounits de memoria de 768 GB que tienen 960 CPU y memoria de 20 TB o SKU de servidor diferente.

aislamiento de cliente Hello dentro de marca de la infraestructura de Hola se realiza en los inquilinos, que de forma detallada el siguiente aspecto:

- Redes: aislamiento de los clientes dentro de la pila de la infraestructura a través de redes virtuales por inquilino asignado al cliente. Un inquilino se asigna a tooa solo cliente. Un cliente puede tener varios inquilinos. aislamiento de red de Hola de inquilinos prohíbe la comunicación de red entre los inquilinos en el nivel de la infraestructura marca Hola. Incluso si los inquilinos pertenecen toohello mismo cliente.
- Los componentes de almacenamiento: aislamiento a través de máquinas virtuales de almacenamiento que tienen volúmenes de almacenamiento asignado tooit. Se pueden asignar volúmenes de almacenamiento máquina solo de tooone almacenamiento virtual. Una máquina virtual de almacenamiento se asigna a exclusivamente tooone solo inquilino de pila de certificados de infraestructura de SAP HANA TDI Hola. Como resultado los volúmenes de almacenamiento asignados de la máquina virtual de almacenamiento de tooa pueden tener acceso en un específico y relacionado inquilino solo. Y no son visibles entre distintos inquilinos implementada Hola.
- Servidor o host: un servidor o unidad de host no se comparte entre clientes o inquilinos. Un servidor o host implementado tooa customer, constituye una unidad atómica reconstrucción de proceso que se asigna un solo inquilino tooone. **No** se usa particiones de hardware ni de software, ya que podría dar lugar a que un cliente comparta un host o servidor con otro cliente. Volúmenes de almacenamiento que se asignan toohello almacenamiento de máquina del inquilino específico de hello son toosuch montado un servidor. Un inquilino puede tener un unidades de servidor toomany de diferentes SKU exclusivamente asignadas.
- Dentro de un SAP HANA en la marca de la infraestructura de Azure (instancia grande), muchos inquilinos diferentes se implementan y aislados comparándolas entre sí a través de conceptos de inquilino de hello en el nivel de red, almacenamiento y proceso. 


Estas unidades de servidor sin sistema operativo son compatible toorun SAP HANA solo. capa de aplicación de SAP de Hola o una capa de software intermedio de carga de trabajo se está ejecutando en máquinas virtuales de Microsoft Azure. marcas de infraestructura de Hello ejecutan Hola SAP HANA en Azure (instancia grande) unidades son toohello conectado red Azure redes principales, por lo tanto, que proporciona conectividad de baja latencia entre SAP HANA en las unidades de Azure (instancia grande) y máquinas virtuales de Azure.

Este documento es uno de los cinco documentos, que incluyen el tema de Hola de SAP HANA en Azure (instancia grande). En este documento, vamos a través de la arquitectura básica de hello, responsabilidades, los servicios que proporciona y en un alto nivel a través de las capacidades de solución de Hola. Para la mayoría de las áreas de hello, al igual que la red y conectividad, hello otros cuatro documentos están cubriendo detalles y explorar listas desplegables. documentación de Hola de SAP HANA en Azure (instancia grande) no tratan aspectos de la instalación de SAP NetWeaver o implementaciones de SAP NetWeaver en máquinas virtuales de Azure. En este tema se trata en la documentación independiente que se encuentra en hello mismo contenedor de documentación. 


cinco partes de Hola de esta guía tratan Hola temas siguientes:

- [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infraestructura y conectividad con SAP HANA en Azure (instancias grandes)](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [¿Cómo tooinstall y configure SAP HANA (instancias de gran tamaño) en Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Solución de problemas y supervisión de SAP HANA en Azure (instancias grandes)](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definiciones

Varias definiciones comunes se usan ampliamente en hello arquitectura y Guía de implementación técnica. Hola nota después de términos y sus significados:

- **IaaS**: infraestructura como servicio
- **PaaS**: plataforma como servicio
- **SaaS**: software como servicio
- **Componente de SAP:** una aplicación de SAP individual, como ECC, BW, Solution Manager o EP. Los componentes de SAP pueden basarse en tecnologías tradicionales, como ABAP o Java, o en una aplicación no basada en NetWeaver, como Business Objects.
- **Entorno SAP:** uno o más componentes SAP agrupan lógicamente tooperform una función empresarial, como desarrollo, QAS, aprendizaje, recuperación ante desastres o producción.
- **Panorama SAP:** hace referencia toohello todos activos de SAP en su entorno de TI. Hola panorama SAP incluye todos los entornos de producción y no es de producción.
- **Sistema SAP:** Hola combinación de capa de DBMS y la capa de aplicación de un sistema de desarrollo SAP ERP, sistema de prueba de SAP BW, sistema de producción de SAP CRM, etcetera. Las implementaciones de Azure no admiten la división de estas dos capas entre la infraestructura local y la de Azure. Esto significa que un sistema SAP debe implementarse de forma local o en Azure, pero no en ambos. Sin embargo, puede implementar diferentes sistemas de Hola de un panorama SAP en Azure o de forma local. Por ejemplo, podría implementar los sistemas de desarrollo y prueba de SAP CRM hello en Azure, al implementar Hola SAP CRM producción sistema local. Para SAP HANA en Azure (instancias grandes), está diseñado que hospedan la capa de aplicación de SAP de Hola de sistemas SAP en máquinas virtuales de Azure y Hola instancia SAP HANA relacionada en una unidad en la marca de la instancia de gran tamaño de HANA Hola.
- **Marca de la instancia de gran tamaño:** una pila de infraestructura de hardware que es SAP HANA TDI certificadas y dedicado instancias de SAP HANA toorun dentro de Azure.
- **SAP HANA en Azure (instancias de gran tamaño):** nombre oficial de oferta de hello en instancias HANA toorun Azure en SAP HANA TDI certificadas hardware que se implementa en marcas de instancia grande en diferentes regiones de Azure. Hola relacionadas con los términos **instancia grande de HANA** es corto para SAP HANA en Azure (instancias de gran tamaño) y es muy utilizado esta guía de implementación técnica.
- **Entre entornos:** describe un escenario donde las máquinas virtuales están implementada tooan suscripción de Azure que tiene el sitio a sitio, varios sitios o conectividad de ExpressRoute entre datacenter(s) de hello local y Azure. En la documentación habitual de Azure, este tipo de implementaciones se denominan "escenarios entre locales". motivo de Hola de conexión de hello es tooextend dominios locales, Active Directory/OpenLDAP local y en nivel local DNS en Azure. Hola horizontal local es extendido toohello activos de Azure de hello suscripciones de Azure. Con esta extensión, hello las máquinas virtuales puede formar parte del dominio local de Hola. Los usuarios de dominio del dominio local de hello pueden tener acceso a servidores de Hola y pueden ejecutar servicios en esas máquinas virtuales (por ejemplo, servicios de DBMS). Es posible la comunicación y resolución de nombres entre máquinas virtuales implementadas de forma local y en Azure. Como es típico de hello en qué SAP mayoría se implementan activos. Consulte las guías de Hola de [planificación y diseño para la puerta de enlace VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [crear una red virtual con una conexión de sitio a sitio mediante el portal de Azure de hello](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información.
- **Inquilino:** un cliente implementado en la marca de instancias grandes de HANA se aísla en un "inquilino". Un inquilino se aísla en hello redes, almacenamiento y capa de proceso de otros inquilinos. Por lo tanto, esa unidades de almacenamiento y proceso toohello asignado varios inquilinos no pueden verse entre sí o comunicarse entre sí en hello instancia grande de HANA marca de nivel. Un cliente puede elegir toohave implementaciones en varios inquilinos. Aún así, no hay ninguna comunicación entre los inquilinos en hello nivel de instancia grande de HANA marca.

Hay una variedad de recursos adicionales que se han publicado en el tema de saludo de la implementación de carga de trabajo SAP en la nube pública de Microsoft Azure. Se recomienda que cualquier persona planeación y ejecución de una implementación de SAP HANA en Azure sea consciente de las entidades de seguridad de Hola de IaaS de Azure y la implementación de Hola de cargas de trabajo SAP en IaaS de Azure y con experiencia. Hello siguientes recursos proporcionan más información y se deben hacer referencia antes de continuar:


- [Uso de soluciones SAP en Microsoft Azure Virtual Machines](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certificación

Además de hello certificación NetWeaver, SAP requiere una certificación especial para SAP HANA toosupport SAP HANA en determinadas infraestructuras, como IaaS de Azure.

Hola core nota de SAP NetWeaver y tooa grado certificación de SAP HANA, es [SAP nota #1928533 – aplicaciones SAP en Azure: tipos de productos compatibles y la máquina virtual de Azure](https://launchpad.support.sap.com/#/notes/1928533).

Esta nota [SAP Note #2316233 - SAP HANA on Microsoft Azure (Large Instances)](https://launchpad.support.sap.com/#/notes/2316233/E) (Nota de SAP 2316233: SAP HANA en Microsoft Azure [Instancias grandes]) también es relevante. Se ocupa de solución de hello descrita en esta guía. Además, son compatible toorun SAP HANA en el tipo de máquina virtual de GS5 Hola de Azure. [Información en este caso se publica en el sitio Web SAP de hello](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hello SAP HANA en la solución de Azure (instancias de gran tamaño) hace referencia tooin SAP nota #2316233 proporciona a Microsoft y a los clientes de SAP Hola capacidad toodeploy grandes SAP Business Suite, SAP Business Warehouse (BW), HANA S/4, BW/4HANA u otras cargas de trabajo de SAP HANA en Azure. solución de Hola se basa en hello SAP-HANA certificada marca de hardware dedicado ([integración SAP HANA adaptada centro de datos – TDI](https://scn.sap.com/docs/DOC-63140)). Ejecutar como un TDI de SAP HANA solución configurada proporciona confianza Hola de saber que todas las aplicaciones basadas en SAP HANA que (incluyendo SAP Business Suite en SAP HANA, SAP Business Warehouse (BW) en SAP HANA, S4/HANA y BW4/HANA) estarán toowork en hello infraestructura de hardware.

Toorunning comparado SAP HANA en máquinas virtuales de Azure esta solución tiene una ventaja, es mucho más grandes volúmenes de memoria. Si desea tooenable esta solución, hay algunos aspectos clave toounderstand:

- capa de aplicación de SAP de Hola y aplicaciones SAP no se ejecutan en máquinas virtuales de Azure (VM) que se hospedan en marcas de hardware de Azure habitual de Hola.
- Cliente de infraestructura local, centros de datos, y las implementaciones de aplicaciones son la plataforma de nube de Microsoft Azure toohello conectado a través de ExpressRoute de Azure (recomendado) o red privada Virtual (VPN). Active Directory (AD) y DNS también se extienden a Azure.
- instancia de base de datos de SAP HANA Hola para cargas de trabajo HANA se ejecuta en SAP HANA en Azure (instancias de gran tamaño). marca de la instancia grande de Hola está conectado en red de Azure, para que software que se ejecuta en máquinas virtuales de Azure pueda interactuar con hello HANA ejecutándose en instancias grandes HANA.
- El hardware de SAP HANA en Azure (Instancias grandes) es hardware dedicado que se proporciona en una infraestructura como servicio (IaaS) con SUSE Linux Enterprise Server o Red Hat Enterprise Linux preinstalado. Con máquinas de virtuales de Azure, más las actualizaciones y el sistema de operativo toohello de mantenimiento es su responsabilidad.
- Instalación de HANA o cualquier toorun componentes adicionales necesarios SAP HANA en las unidades de HANA grandes instancias es su responsabilidad como respectivas todas las operaciones en curso y las administraciones de SAP HANA en Azure.
- Además toohello soluciones que se describe aquí, puede instalar otros componentes de la suscripción de Azure que se conecta tooSAP HANA en Azure (instancias de gran tamaño).  Por ejemplo, los componentes que permiten la comunicación con o directamente la base de datos de SAP HANA toohello (servidores de salto, de RDP SAP HANA Studio, servicios de datos de SAP para escenarios de BI de SAP, o soluciones de supervisión de red).
- Como en Azure, Instancias grandes de HANA ofrece funcionalidades auxiliares de alta disponibilidad y recuperación ante desastres.

## <a name="architecture"></a>Arquitectura

En un nivel superior, hello SAP HANA en la solución de Azure (instancias de gran tamaño) tiene capa de aplicación de SAP de Hola que residen en máquinas virtuales de Azure y Hola capa de base de datos que residen en un hardware TDI SAP configurado ubicado en una marca de la instancia grande en Hola la misma región de Azure que está conectado tooAzure IaaS.

> [!NOTE]
> Necesita toodeploy capa de aplicación de SAP de hello en hello misma región de Azure como capa de DBMS de SAP de Hola. Esta regla está bien documentada en la información publicada sobre la carga de trabajo de SAP en Azure. 

Hello arquitectura global de SAP HANA en Azure (instancias de gran tamaño) proporciona una configuración de hardware certificado TDI de SAP (no virtualizados, bare metal, servidor de alto rendimiento para la base de datos de SAP HANA hello) y la capacidad de Hola y la flexibilidad de Azure tooscale recursos para hello SAP toomeet de capa de aplicación de sus necesidades.

![Introducción a la arquitectura de SAP HANA en Azure (Instancias grandes)](./media/hana-overview-architecture/image1-architecture.png)

arquitectura de Hola que se muestra se divide en tres secciones:

- **Derecha:** una infraestructura local donde se ejecutan diferentes aplicaciones en centros de datos con usuarios finales que acceden a aplicaciones de LOB (por ejemplo, SAP). Idealmente, esto local infraestructura está conectada, a continuación, tooAzure con Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Centro:** muestra IaaS de Azure y, en este caso, el uso de máquinas virtuales de Azure toohost SAP u otras aplicaciones que utilizan SAP HANA como un sistema DBMS. Instancias HANA menores que proporcionan la función con memoria de hello máquinas virtuales de Azure se implementan en máquinas virtuales de Azure junto con su nivel de aplicación. Consulte más información sobre [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).
<br />Las redes Azure son los sistemas SAP toogroup utilizado junto con otras aplicaciones en redes virtuales de Azure (redes virtuales). Estas redes virtuales conectan sistemas tooon locales, así como tooSAP HANA en Azure (instancias de gran tamaño).
<br />Para las aplicaciones de SAP NetWeaver y las bases de datos que son compatibles toorun en Microsoft Azure, consulte [SAP compatibilidad Nota #1928533 – aplicaciones SAP en Azure: tipos de productos compatibles y la máquina virtual de Azure](https://launchpad.support.sap.com/#/notes/1928533). Para obtener documentación sobre la implementación de soluciones de SAP en Azure, consulte:

  -  [Uso de SAP en máquinas virtuales (VM) Windows](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Uso de soluciones SAP en Microsoft Azure Virtual Machines](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Izquierda:** muestra Hola SAP HANA TDI certificadas hardware en la marca de la instancia de Azure grandes de Hola. las unidades de instancia grande de HANA Hola son toohello conectado redes virtuales de Azure de su suscripción utilizando la misma tecnología que conectividad Hola desde local a Azure Hola.

marca de la instancia de gran tamaño de Azure de Hello propio combina Hola de los componentes siguientes:

- **Informática:** servidores basados en procesadores Intel Xeon E7-8890v3 o Intel Xeon E7-8890v4 que proporcionan la capacidad de computación necesarios hello y están certificadas de SAP HANA.
- **Red:** unificado de un tejido de red de alta velocidad que interconecta Hola cálculo, almacenamiento y componentes de red local.
- **Almacenamiento:** una infraestructura de almacenamiento a la que se accede por medio de un tejido de red unificada. Capacidad de almacenamiento específica es proporcionado por función hello que se está implementando específico de SAP HANA en configuración de Azure (instancias de gran tamaño) (más capacidad de almacenamiento está disponible en un costo mensual adicional).

Dentro de infraestructura de varios inquilinos de Hola de marca de la instancia grande de hello, los clientes se implementan como inquilinos aislados. En la implementación de inquilino de hello, deberá tooname una suscripción de Azure dentro de la inscripción de Azure. Este curso toobe Hola suscripción de Azure Hola instancias grandes HANA va toobe sumándolo. Estos inquilinos tengan una suscripción de Azure toohello de relación de 1:1. Red conveniente resulta posible tooaccess una unidad de instancia grande de HANA implementado en un inquilino en una región de Azure de diferentes redes virtuales de Azure, que pertenece toodifferent suscripciones de Azure. Aunque las suscripciones de Azure necesitan toobelong toohello mismo inscripción de Azure. 

Al igual que con las máquinas virtuales de Azure, SAP HANA en Azure (Instancias grandes) se ofrece en varias regiones de Azure. En las capacidades de recuperación ante desastres de orden toooffer, puede elegir tooopt en. Marcas de tiempo de instancia grande diferentes dentro de una región geográfica políticos son conectado tooeach otros. Por ejemplo, marcas de instancia grande de HANA en nosotros oeste y este de EE. se conectan a través de un vínculo de red dedicado de propósito de saludo de la replicación de recuperación ante desastres. 

Al igual que puede elegir entre diferentes tipos de máquinas virtuales con Azure Virtual Machines, también puede elegir entre diferentes SKU de Instancias grandes de HANA que se adapten a distintos tipos de carga de trabajo de SAP HANA. SAP aplica proporciones de socket tooprocessor de memoria para diferentes cargas de trabajo en función de las generaciones de procesador de Intel hello, hay cuatro tipos diferentes de SKU que ofrece:

A partir de julio de 2017, SAP HANA en Azure (instancias de gran tamaño) está disponible en varias configuraciones de hello Azure regiones de nosotros oeste y este de EE., Australia Oriental, sudeste de Australia, Europa occidental y Europa del Norte:

| Solución de SAP | CPU | Memoria | Almacenamiento | Disponibilidad |
| --- | --- | --- | --- | --- |
| Optimizada para OLAP: SAP BW, BW/4HANA<br /> o SAP HANA para cargas de trabajo de OLAP genérico | SAP HANA en Azure S72<br /> – 2 procesadores Intel® Xeon® E7-8890 v3<br /> 36 núcleos de CPU y 72 subprocesos de CPU |  768 GB |  3 TB | Disponible |
| --- | SAP HANA en Azure S144<br /> – 4 procesadores Intel® Xeon® E7-8890 v3<br /> 72 núcleos de CPU y 144 subprocesos de CPU |  1,5 TB |  6 TB | No disponible |
| --- | SAP HANA en Azure S192<br /> – 4 procesadores Intel® Xeon® E7-8890 v4<br /> 96 núcleos de CPU y 192 subprocesos de CPU |  2,0 TB |  8 TB | Disponible |
| --- | SAP HANA en Azure S384<br /> – 8 procesadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU y 384 subprocesos de CPU |  4,0 TB |  16 TB | TooOrder listo |
| Optimizada para OLTP: SAP Business Suite<br /> en SAP HANA o S/4HANA (OLTP),<br /> OLTP genérico | SAP HANA en Azure S72m<br /> – 2 procesadores Intel® Xeon® E7-8890 v3<br /> 36 núcleos de CPU y 72 subprocesos de CPU |  1,5 TB |  6 TB | Disponible |
|---| SAP HANA en Azure S144m<br /> – 4 procesadores Intel® Xeon® E7-8890 v3<br /> 72 núcleos de CPU y 144 subprocesos de CPU |  3,0 TB |  12 TB | No disponible |
|---| SAP HANA en Azure S192m<br /> – 4 procesadores Intel® Xeon® E7-8890 v4<br /> 96 núcleos de CPU y 192 subprocesos de CPU  |  4,0 TB |  16 TB | Disponible |
|---| SAP HANA en Azure S384m<br /> – 8 procesadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU y 384 subprocesos de CPU |  6,0 TB |  18 TB | TooOrder listo |
|---| SAP HANA en Azure S384xm<br /> – 8 procesadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU y 384 subprocesos de CPU |  8,0 TB |  22 TB |  TooOrder listo |
|---| SAP HANA en Azure S576<br /> – 12 procesadores Intel® Xeon® E7-8890 v4<br /> 288 núcleos de CPU y 576 subprocesos de CPU |  12,0 TB |  28 TB | TooOrder listo |
|---| SAP HANA en Azure S768<br /> – 16 procesadores Intel® Xeon® E7-8890 v4<br /> 384 núcleos de CPU y 768 subprocesos de CPU |  16,0 TB |  36 TB | TooOrder listo |
|---| SAP HANA en Azure S960<br /> – 20 procesadores Intel® Xeon® E7-8890 v4<br /> 480 núcleos de CPU y 960 subprocesos de CPU |  20,0 TB |  46 TB | TooOrder listo |

- Núcleos de CPU = suma no hyper-threading de núcleos de CPU de suma de Hola de procesadores de Hola de unidad del servidor de Hola.
- Subprocesos de CPU = suma de subprocesos de proceso proporcionada por los núcleos de CPU de hyper-threading de suma de Hola de procesadores de Hola de unidad del servidor de Hola. Todas las unidades se configuran por toouse de forma predeterminada la tecnología Hyper-Threading.


Hello distintas configuraciones anteriores que están disponibles o 'no se ofrezcan ya' se hace referencia en [nota de soporte técnico de SAP &#2316233;: SAP HANA en Microsoft Azure (instancias de gran tamaño)](https://launchpad.support.sap.com/#/notes/2316233/E). las configuraciones de Hello, que están marcadas como 'Listo tooOrder' encontrarán en su entrada en la nota de SAP Hola pronto. Sin embargo, los SKU de instancia se puede ordenar ya para hello seis diferentes regiones de Azure Hola servicio de instancia grande de HANA está disponible.

configuraciones específicas de Hello elegidas dependen de la carga de trabajo, los recursos de CPU y memoria que desee. Es posible que hello tooleverage de carga de trabajo OLTP SKU que están optimizados para cargas de trabajo OLAP. 

hardware de Hello base para todas las ofertas de hello son SAP HANA TDI certificada. Sin embargo, podemos distinguir entre dos clases diferentes de hardware, que divide las SKU de hello en:

- S72, S72m, S144, S144m, S192 y S192m, que nos referiremos tooas hello 'Tipo clase' de SKU.
- S384, S384m, S384xm, S576, S768 y S960, que nos referiremos tooas Hola 'Clase de tipo II' de SKU.

Es importante toonote que una marca de la instancia de gran tamaño de HANA completa no está asignada exclusivamente para un solo cliente &#39; s utilizarán. Este hecho aplica toohello bastidores de recursos de proceso y almacenamiento conectados a través de un tejido de red implementado en Azure. Infraestructura de HANA instancias de gran tamaño, como Azure, implementa el cliente diferente &quot;inquilinos&quot; que están aisladas entre sí en hello después de tres niveles:

- Red: Aislamiento a través de redes virtuales dentro de la marca de la instancia de gran tamaño de HANA Hola.
- Almacenamiento: aislamiento a través de máquinas virtuales de almacenamiento que tienen volúmenes de almacenamiento asignados y aíslan los volúmenes de almacenamiento entre inquilinos.
- Proceso: Asignación dedicada de inquilino único de tooa de unidades de servidor. Sin particiones de hardware ni de software de las unidades de servidor. Sin uso compartido de una sola unidad de host o servidor entre los inquilinos. 

Por lo tanto, las implementaciones de Hola de unidades de instancias de gran tamaño de HANA entre varios inquilinos no están visible tooeach otro. Ni pueden HANA grandes instancia unidades implementados en distintos inquilinos comunicarse directamente con otro nivel de marca de instancia grande de HANA Hola. Solo HANA instancia unidades grandes dentro de un inquilino se pueden comunicar tooeach otro en hello nivel de instancia grande de HANA marca.
Un inquilino implementado en la marca de la instancia grande de Hola se asigna tooone conveniente facturación suscripción de Azure. Sin embargo, wise de red puede tener acceso desde las redes virtuales de Azure de otras suscripciones de Azure en Hola mismo inscripción de Azure. Si implementa con otra suscripción de Azure en hello misma región de Azure, también puede elegir tooask para un inquilino de instancia grande de HANA separado.

Sin embargo, existen diferencias notables entre ejecutar SAP HANA en Instancias grandes de HANA y ejecutar SAP HANA en instancias de Azure Virtual Machines implementadas en Azure:

- No hay ningún nivel de virtualización para SAP HANA en Azure (Instancias grandes). Obtenga un rendimiento de Hola de hardware sin sistema operativo subyacente de Hola.
- A diferencia de Azure, Hola SAP HANA en servidor de Azure (instancias de gran tamaño) está dedicado tooa específicas del cliente. No hay ninguna posibilidad de que un host o unidad de servidor tenga particiones de hardware o software. Como resultado, se utiliza una unidad de instancia grande de HANA tal como lo asignó como inquilino tooa todo y con esa tooyou como un cliente. Un reinicio o apagado del servidor hello no provocar automáticamente del sistema de operativo toohello y SAP HANA que se implementa en otro servidor. (Para tipo clase SKU, Hola única excepción es si un servidor puede surgir problemas y volver a implementar debe toobe realizado en otro servidor.)
- A diferencia de Azure, donde los tipos de procesador de host se seleccionan para la proporción de hello mejor precio/rendimiento, tipos de procesador de hello elegidos para SAP HANA en Azure (instancias de gran tamaño) se Hola realizando más alto de la línea de procesadores Intel E7v3 y E7v4 Hola.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Ejecución de varias instancias de SAP HANA en una unidad de instancia grande de HANA
Es posible toohost más de una instancia de SAP HANA de active en las unidades de instancia grande de HANA Hola. En orden toostill proporcionan capacidades de Hola de instantáneas de almacenamiento y recuperación ante desastres, esta configuración requiere un volumen por cada instancia. A partir de ahora, unidades de instancia grande de HANA Hola pueden subdividirse como sigue:

- S72, S72m, S144, S192: En incrementos de 256 GB con hello de 256 GB más pequeño a partir de unidad. Incrementos diferentes como 256 GB, 512 GB y así sucesivamente, pueden ser toohello combinado máximo de memoria de Hola de unidad de Hola.
- S144m y S192m: en incrementos de 256 GB con unidad más pequeña de 512 GB Hola. Incrementos diferentes al igual que 512 GB, 768 GB y así sucesivamente, pueden ser toohello combinado máximo de memoria de Hola de unidad de Hola.
- Tipo de clase II: en incrementos de 512 GB con hello más pequeño a partir de la unidad de 2 TB. Incrementos diferentes al igual que 512 GB, 1 TB, 1,5 TB y así sucesivamente, pueden ser toohello combinado máximo de memoria de Hola de unidad de Hola.

Algunos ejemplos de la ejecución de varias instancias de SAP HANA tendrían este aspecto:

| SKU | Tamaño de memoria | Tamaño de almacenamiento | Tamaños con varias bases de datos |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1 instancia de HANA de 768 GB<br /> o 1 instancia de 512 GB + 1 instancia de 256 GB<br /> o 3 instancias de 256 GB | 
| S72m | 768 GB | 3 TB | 3 instancias de HANA de 512 GB<br />o 1 instancia de 512 GB + 1 instancia de 1 TB<br />o 6 instancias de 256 GB<br />o 1 instancia de 1,5 TB | 
| S192m | 4 TB | 16 TB | 8 instancias de 512 GB<br />o 4 instancias de 1 TB<br />o 4 instancias de 512 GB + 2 instancias de 1 TB<br />o 4 instancias de 768 GB + 2 instancias de 512 GB<br />o 1 instancia de 4 TB |
| S384xm | 8 TB | 22 TB | 4 instancias de 2 TB<br />o 2 instancias de 4 TB<br />o 2 instancias de 3 TB + 1 instancia de 2 TB<br />o 2 instancias de 2,5 TB + 1 instancia de 3 TB<br />o 1 instancia de 8 TB |


Obtener la idea de Hola. Por supuesto, también hay otras variaciones. 


## <a name="operations-model-and-responsibilities"></a>Modelo de operaciones y responsabilidades

servicio de Hello proporcionado con SAP HANA en Azure (instancias de gran tamaño) se alinea con servicios de IaaS de Azure. Obtiene una instancia de Instancias grandes de HANA con un sistema operativo instalado que está optimizado para SAP HANA. Como con las máquinas virtuales de Azure IaaS, la mayoría de las tareas de Hola de protección Hola OS, instalar otro software necesario, instalar HANA, operativo Hola SO y HANA y actualizar Hola SO y HANA es su responsabilidad. Microsoft no exige que actualice el sistema operativo ni HANA.

![Responsabilidades de SAP HANA en Azure (Instancias grandes)](./media/hana-overview-architecture/image2-responsibilities.png)

Como puede ver en diagrama de hello anterior, SAP HANA en Azure (instancias de gran tamaño) es una infraestructura de varios inquilinos como una oferta de servicio. Y como resultado, división de Hola de responsabilidad por límite de infraestructura de sistema operativo de hello, para hello mayoría forma parte. Microsoft es responsable de todos los aspectos del servicio de hello debajo de línea de saludo del sistema operativo de Hola y el usuario es responsable por encima de la línea hello, incluido el sistema operativo de Hola. Para más recientes métodos locales que se puede emplear para cumplimiento de normas, seguridad, administración de aplicaciones, base y administración de sistema operativo pueden continuar toobe usa. sistemas de Hello aparecen como si estuvieran en la red en todo lo que respecta.

Sin embargo, este servicio está optimizado para SAP HANA, por lo que hay áreas donde usted y Microsoft necesitan capacidades de infraestructura subyacente de toowork toouse juntos Hola para obtener los mejores resultados.

Hola lista siguiente proporciona más detalles sobre cada una de las capas de Hola y sus responsabilidades:

**Redes:** todos Hola redes internas de marca de la instancia grande de hello ejecuta SAP HANA, el almacenamiento de toohello de acceso, con conectividad entre las instancias de hello (de escalabilidad horizontal y otras funciones), horizontal toohello de conectividad y conectividad tooAzure donde se hospeda la capa de aplicación de SAP de hello en máquinas virtuales de Azure. También incluye la conectividad de WAN entre centros de datos de Azure para la replicación con fines de recuperación ante desastres. Todas las redes se dividen en particiones por inquilino hello y se les aplique QOS.

**Almacenamiento:** Hola virtualiza el almacenamiento con particiones para todos los volúmenes necesarios para servidores de SAP HANA hello, así como para las instantáneas. 

**Servidores:** Hola dedicado servidores físicos toorun Hola bases de datos de SAP HANA asignado tootenants. Hola servidores de hello clase de tipo de SKU son abstraído del hardware. Con estos tipos de servidores, configuración del servidor Hola se recopilan y se mantiene en perfiles, que se pueden mover desde un hardware físico tooanother de hardware físico. Tal un movimiento (manual) de un perfil de las operaciones se pueden comparar un poco tooAzure servicio de recuperación. servidores de Hola de hello SKU de la clase de tipo II no ofrecen una función de este tipo.

**SDDC:** centros de software de administración de Hola que es datos toomanage usados como entidades definidas por software. Permite que Microsoft toopool recursos para escalabilidad, disponibilidad y razones de rendimiento.

**SO:** Hola SO que elija (SUSE Linux o Red Hat Linux) que se ejecuta en servidores de Hola. imágenes de SO Hola que se proporcionan son imágenes de hello proporcionadas por hello tooMicrosoft de proveedor de Linux individual a fin de Hola de SAP HANA en ejecución. Son toohave requiere una suscripción con un proveedor de Linux Hola para hello con optimización para SAP HANA de imagen específico. Sus responsabilidades consiste en registrar imágenes Hola con el proveedor del SO Hola. Desde el punto de Hola de entrega por Microsoft, también es responsable de cualquier revisión adicional del sistema operativo de Linux de Hola. Esta revisión también incluye paquetes adicionales que podrían ser necesarios para una correcta instalación de SAP HANA (consulte la documentación de la instalación de HANA del tooSAP y las notas de SAP) y que no se había incluido por el proveedor de Linux específico de hello en sus SAP HANA imágenes del sistema operativo optimizadas. responsabilidad de Hola de cliente de Hola también incluye la aplicación de revisiones de hello SO que es toomalfunction/optimización relacionada de hello sistema operativo y el hardware de servidor específico de controladores toohello relacionados. O cualquier seguridad o revisión funcional de hello SO. Es también responsabilidad del cliente la supervisión y planificación de capacidad de:

- Consumo de recursos de CPU
- Consumo de memoria
- Espacio en disco volúmenes toofree relacionados, IOPS y latencia
- Tráfico de volumen de red entre Instancias grandes de HANA y la capa de la aplicación de SAP

infraestructura subyacente de Hola de instancias de gran tamaño de HANA proporciona funcionalidad para copias de seguridad y restauración de volumen del sistema operativo Hola. Usar esta funcionalidad es también su responsabilidad.

**Middleware:** Hola instancia de SAP HANA, principalmente. La administración, las operaciones y la supervisión son responsabilidad suya. No hay funcionalidad proporcionado por el le permite toouse instantáneas de almacenamiento con fines de recuperación ante desastres y de copia de seguridad/restauración. Estas capacidades se proporcionan con la infraestructura de Hola. Pero sus responsabilidades incluyen también el diseño de la alta disponibilidad o la recuperación ante desastres con estas capacidades, aprovecharlas y supervisar que las instantáneas de almacenamiento se hayan ejecutado correctamente.

**Datos:** los datos administrados por SAP HANA y otros datos, como archivos de copia de seguridad que se encuentran en volúmenes o recursos compartidos de archivos. Sus responsabilidades incluyen supervisión de espacio libre en disco y administrar el contenido de hello en volúmenes de Hola y supervisión de la ejecución correcta de Hola de copias de seguridad de volúmenes de disco y las instantáneas de almacenamiento. Sin embargo, la ejecución correcta de los sitios de tooDR de replicación de datos es responsabilidad de Hola de Microsoft.

**Aplicaciones:** Hola instancias de la aplicación de SAP o, en el caso de aplicaciones de SAP, capa de aplicación Hola de esas aplicaciones. Sus responsabilidades incluyen la implementación, administración, operaciones y supervisión de esas aplicaciones relacionados toocapacity planeación de consumo de recursos de CPU, consumo de memoria, consumo de almacenamiento de Azure y consumo de ancho de banda de red en Redes virtuales de Azure y de redes virtuales de Azure tooSAP HANA en Azure (instancias de gran tamaño).

**WAN:** Hola conexiones establecer de las implementaciones de tooAzure locales para las cargas de trabajo. Todos nuestros clientes con instancias grandes de HANA usan Azure ExpressRoute para la conectividad. Esta conexión no es parte del programa Hola a SAP HANA en la solución de Azure (instancias grandes), por lo que usted es responsable de la instalación de Hola de esta conexión.

**Archivado:** podría ser preferible tooarchive copias de datos utilizando sus propios métodos de las cuentas de almacenamiento. El archivado conlleva tareas de administración, cumplimiento normativo, costos y operaciones. Es su responsabilidad generar copias de archivado y copias de seguridad en Azure, y almacenarlas con un método compatible.

Vea hello [SLA de SAP HANA en Azure (instancias de gran tamaño)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Ajuste de tamaño

El ajuste de tamaño para Instancias grandes de HANA es igual que para HANA en general. Existentes e implementado sistemas, desea toomove desde otro tooHANA RDBMS, SAP le ofrece una serie de informes que se ejecutan en los sistemas SAP existentes. Si se utiliza una base de datos de hello tooHANA movida, estos informes comprobación los datos de Hola y calcular los requisitos de memoria para la instancia HANA Hola. Leer Hola siguiendo las notas de SAP tooget obtener más información sobre cómo toorun estos informes y cómo tooobtain sus revisiones o versiones más recientes:

- [SAP Note #1793345 - Sizing for SAP Suite on HANA](https://launchpad.support.sap.com/#/notes/1793345) (Nota de SAP 1793345: Ajuste de tamaño para SAP Suite en HANA)
- [SAP Note #1872170 - Suite on HANA and S/4 HANA sizing report](https://launchpad.support.sap.com/#/notes/1872170) (Nota de SAP 1872170: Informe de ajuste de tamaño de Suite en HANA y S/4 HANA)
- [SAP Note #2121330 - FAQ: SAP BW on HANA Sizing Report](https://launchpad.support.sap.com/#/notes/2121330) (Nota de SAP 2121330: P+F: Informe de ajuste de tamaño de SAP BW en HANA)
- [SAP Note #1736976 - Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/1736976) (Nota de SAP 1736976: Informe de ajuste de tamaño para BW en HANA)
- [SAP Note #2296290 - New Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/2296290) (Nota de SAP 2296290: Nuevo informe de ajuste de tamaño para BW en HANA)

Para las implementaciones de campo verde, SAP Quick Sizer es requisitos de memoria de toocalculate disponible de implementación de Hola de software SAP en la parte superior HANA.

Requisitos de memoria de HANA son aumentar a medida que aumenta el volumen de datos, por lo que desea toobe consciente de consumo de memoria de hello ahora y ser capaz de toopredict ¿qué es continuo toobe en Hola futuras. En función de los requisitos de memoria de hello, puede asignar la demanda, a continuación, en uno de hello HANA grandes instancia SKU.

## <a name="requirements"></a>Requisitos

En esta lista se recopilan los requisitos para ejecutar SAP HANA en Azure (instancias grandes).

**Microsoft Azure:**

- Una suscripción de Azure que se puede vincula tooSAP HANA en Azure (instancias de gran tamaño).
- Contrato de soporte técnico Premier de Microsoft. Vea [SAP compatibilidad Nota #2015553-SAP en Microsoft Azure: requisitos previos de compatibilidad](https://launchpad.support.sap.com/#/notes/2015553) para obtener información específica relacionada con toorunning SAP en Azure. Con unidades de instancia grande de HANA 384 y más CPU, también necesita tooextend hello tooinclude de contrato de soporte técnico Premier respuesta rápida de Azure (ARR).
- Conocimiento de instancias de gran tamaño Hola HANA SKU que necesita después de realizar un cambio de tamaño ejercicio con SAP.

**Conectividad de red:**

- Azure ExpressRoute entre local tooAzure: tooconnect su tooAzure de centro de datos local, asegúrese de que tooorder una conexión como mínimo 1 GB/s de su ISP. 

**Sistema operativo:**

- Licencias para SUSE Linux Enterprise Server 12 for SAP Applications.

> [!NOTE] 
> Hola sistema operativo entregado por Microsoft no está registrado con SUSE ni está conectado a una instancia SMT.

- SUSE Linux Subscription Management Tool (SMT) implementada en Azure en una máquina virtual de Azure. Esto proporciona la capacidad de Hola para SAP HANA en Azure (instancias de gran tamaño) toobe registren y actualicen respectivamente mediante SUSE (porque no hay ningún acceso a internet en el centro de datos de instancias de gran tamaño de HANA). 
- Licencias para Red Hat Enterprise Linux 6.7 o 7.2 para SAP HANA.

> [!NOTE]
> Hola sistema operativo entregado por Microsoft no está registrado con Red Hat, ni tampoco TI conectado tooa instancia del Administrador de suscripción de Hat de color rojo.

- Red Hat Subscription Manager implementado en Azure en una máquina virtual de Azure. Hola rojo Hat suscripción Manager proporciona capacidad de Hola para SAP HANA en Azure (instancias de gran tamaño) toobe registren y actualicen respectivamente mediante Red Hat (porque no hay ningún acceso directo a internet desde dentro de inquilino de hello implementada en la marca de la instancia de Azure grandes de hello).
- SAP requiere toohave compatibilidad de contrato con el proveedor de Linux también. Este requisito no se borra solución Hola de HANA instancias de gran tamaño o hello hecho que su ejecución Linux en Azure. A diferencia de con algunas de las imágenes de la Galería de Azure de Linux de hello, Hola servicio cuota no se incluye en oferta de solución de Hola de HANA instancias de gran tamaño. Es como un cliente toofulfill Hola requisitos de SAP con respecto a los contratos de soporte técnico con un distribuidor de Linux Hola depende de usted.   
   - Para SUSE Linux, buscar Hola requisitos de compatibilidad de contrato en [SAP nota #1984787 - SUSE LINUX Enterprise Server 12: notas de instalación](https://launchpad.support.sap.com/#/notes/1984787) y [SAP nota #1056161 - SUSE admite la prioridad para las aplicaciones de SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Para Red Hat Linux, necesita niveles de suscripción correcta de hello toohave que incluyen soporte técnico y servicio (actualizaciones de sistemas operativos de toohello de HANA instancias de gran tamaño. Red Hat recomienda obtener una suscripción a "RHEL for SAP Business Applications". En lo que respecta al soporte técnico y los servicios, consulte [SAP Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167) (Nota de SAP 2002167: Instalación y actualización de Red Hat Enterprise Linux 7.x) y [SAP Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410) (Nota de SAP 1496410: Instalación y actualización de Red Hat Enterprise Linux 6.x) para obtener información detallada.

**Base de datos**

- Las licencias y los componentes de instalación de software para SAP HANA (Platform Edition o Enterprise Edition).

**Aplicaciones:**

- Las licencias y los componentes de instalación de software para las aplicaciones de SAP que se conectan tooSAP HANA y contratos de soporte técnico relacionados con SAP.
- Licencias y componentes de instalación de software para las aplicaciones de SAP no usan en relación tooSAP HANA en entorno de Azure (instancias de gran tamaño) y relacionada con contratos de soporte técnico.

**Habilidades:**

- Experiencia y conocimientos sobre IaaS de Azure y sus componentes.
- Experiencia y conocimientos sobre la implementación de cargas de trabajo de SAP en Azure.
- Personal certificado para la instalación de SAP HANA.
- SAP arquitecto habilidades toodesign alta disponibilidad y recuperación ante desastres alrededor de SAP HANA.

**SAP:**

- Se espera que sea un cliente de SAP y que tenga un contrato de soporte técnico con SAP.
- Especialmente para implementaciones en hello clase de tipo II de HANA grandes SKU de instancia, se recomienda encarecidamente tooconsult con SAP en versiones de SAP HANA y configuraciones posibles en hardware de escala vertical de tamaño grande.


## <a name="storage"></a>Storage

Hello distribución de almacenamiento para SAP HANA en Azure (instancias de gran tamaño) se configura SAP HANA en administración de servicios de Azure a través de SAP recomendada instrucciones, documentadas en hello [requisitos de almacenamiento de SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) notas del producto.

Hola HANA instancias grandes de tipo clase hello incluyen volumen de memoria de cuatro veces hello como volumen de almacenamiento. Para el tipo de hello clase II de unidades de la instancia de HANA grande, almacenamiento de hello no va toobe cuatro veces más. unidades de Hello vienen con un volumen, que sirve para almacenar copias de seguridad del registro de transacciones de HANA. Obtener más información en [cómo tooinstall y configure SAP HANA (instancias de gran tamaño) en Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Vea hello en cuanto a asignación de almacenamiento en la tabla siguiente. Hola tabla enumeran más o menos capacidad de Hola para volúmenes diferentes Hola proporcionada con diferentes unidades de instancia grande de HANA Hola.

| SKU de Instancias grandes de HANA | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1.024 GB | 1536 GB | 1.024 GB |
| S192m | 11.520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11.520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36.000 GB | 4100 GB | 2050 GB | 4100 GB |


Volúmenes implementados reales pueden variar un poco en función de la implementación y la herramienta de tamaños de volúmenes de hello tooshow usado.

Si subdivide una SKU de instancia grande de HANA, algunos ejemplos de los posibles fragmentos de división serían como sigue:

| Partición de memoria en GB | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1.024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Estos tamaños son números de volumen aproximada que pueden variar ligeramente en función de la implementación y herramientas usan toolook en volúmenes de Hola. También hay otros tamaños de partición posibles, como 2,5 TB. Estos tamaños de almacenamiento se calcularía con una fórmula similar que se usan para las particiones de hello anteriores. término de Hello 'partitions' no indica que sistema de operativo hello, memoria o recursos de CPU se de cualquier manera con particiones. Solo indica las particiones de almacenamiento para distintas instancias HANA Hola conviene toodeploy en una única unidad de instancia grande de HANA. 

Posible que tenga un cliente necesita más capacidad de almacenamiento, tendrá Hola posibilidad tooadd toopurchase más almacenamiento en unidades de 1 TB. Este almacenamiento adicional se puede agregar como volumen adicional o puede ser utilizado tooextend uno o varios de los volúmenes existentes de Hola. No es posible toodecrease tamaños de Hola de volúmenes de hello tal como se implementó originalmente y documentado principalmente por anterior Hola tabla (s). También no es nombres de Hola de posibles toochange de volúmenes de Hola o nombres de montaje. volúmenes de almacenamiento de Hello como se describió anteriormente son unidades de instancia grande de HANA de toohello adjunto como volúmenes NFS4.

Como un cliente puede elegir toouse instantáneas de almacenamiento de copia de seguridad/restauración y ante desastres con fines de recuperación. Puede encontrar más información sobre este tema en [Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Cifrado de datos en reposo
almacenamiento de Hello utilizado para instancias de gran tamaño de HANA permite un cifrado transparente de los datos de Hola tal y como se almacena en discos de Hola. Durante la implementación de una unidad de instancia grande de HANA, tener Hola opción toohave este tipo de cifrado está habilitado. También puede seleccionar toochange tooencrypted volúmenes después de la implementación de hello ya. Hola movimiento de volúmenes sin cifrar tooencrypted es transparente y no requiere un tiempo de inactividad. 

Se cifra con hello SKU de arranque de hello volumen Hola LUN se almacena en, la clase de tipo. En el caso de tipo hello clase II de SKU de HANA instancias de gran tamaño, debe tooencrypt Hola LUN de inicio con métodos de sistema operativo. 


## <a name="networking"></a>Redes

arquitectura de Hola de red de Azure es una implementación de toosuccessful de componente clave de aplicaciones SAP en instancias de HANA grandes. Por lo general, las implementaciones de SAP HANA en Azure (Instancias grandes) tienen un entorno de SAP más amplio con varias soluciones SAP distintas y diversos tamaños de base de datos, consumo de recursos de CPU y utilización de memoria. Es probable que no todos esos sistemas SAP estén basados en SAP HANA, por lo que el entorno de SAP probablemente sea un entorno híbrido que use:

- Sistemas SAP implementados localmente. Debido a los tamaños de tootheir, estos sistemas actualmente no se puede hospedar en Azure; un ejemplo típico sería un sistema SAP ERP de producción con Microsoft SQL Server (como base de datos de Hola) que requiere más CPU o pueden proporcionar recursos de memoria de máquinas virtuales de Azure.
- Sistemas SAP basados en SAP HANA implementados localmente.
- Sistemas SAP implementados en máquinas virtuales de Azure. Estos sistemas podrían estar desarrollo, pruebas, de espacio aislado, o instancias de producción para cualquiera de las aplicaciones basadas en SAP NetWeaver Hola que pueden implementar correctamente en Azure (en las máquinas virtuales), según la demanda de memoria y el consumo de recursos. Estos sistemas también podrían basarse en bases de datos como SQL Server (vea [SAP Support Note #1928533 – SAP Applications on Azure: Supported Products and Azure VM types](https://launchpad.support.sap.com/#/notes/1928533/E) [Nota de SAP 1928533: Aplicaciones de SAP en Azure: productos y tipos de máquina virtual de Azure admitidos]) o SAP HANA (vea [SAP HANA Certified IaaS Platforms](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) [Plataformas IaaS certificadas para SAP HANA]).
- Servidores de aplicaciones de SAP implementados en Azure (en máquinas virtuales) que aprovechan SAP HANA en Azure (Instancias grandes) en sellos de instancias grandes de Azure.

Aunque un entorno híbrido de SAP (con cuatro o más escenarios de implementación diferentes) es habitual, hay muchos casos de cliente de entornos de SAP completos que se ejecutan en Azure. Como las máquinas virtuales de Microsoft Azure cada vez son más eficaces, número de Hola de los clientes mover sus soluciones SAP en Azure está aumentando.

Funciones de red en el contexto de Hola de sistemas SAP implementado en Azure de Azure no es complicada. Se basa en hello siguientes principios:

- Redes virtuales de Azure (redes virtuales) necesita el circuito de ExpressRoute de Azure de toohello toobe conectado que se conecta la red local tooon.
- Un circuito de ExpressRoute conectarse normalmente tooAzure local debe tener un ancho de banda de 1 GB/s o superior. Este ancho de banda mínimo permite suficiente ancho de banda para transferir datos entre sistemas locales y sistemas que se ejecutan en máquinas virtuales de Azure (así como los sistemas de tooAzure de conexión de los usuarios finales local).
- Todos los sistemas SAP en Azure necesidad toobe configuran en redes virtuales de Azure toocommunicate entre sí.
- Active Directory y DNS hospedados localmente se extienden a Azure a través de ExpressRoute desde un entorno local.


> [!NOTE] 
> Desde un punto de vista facturación, solo una sola suscripción de Azure puede vincularse sólo tooone de inquilino único en una marca de la instancia grande en una región de Azure específica y, a la inversa puede vincularse a un solo inquilino de marca de la instancia grande solo tooone suscripción de Azure. Este hecho es tooany no es distinta de otros objetos facturables en Azure

¿Implementar SAP HANA en Azure (instancias de gran tamaño) en varias regiones de Azure, ha habían implementado el resultados en un toobe independiente del inquilino en hello marca de la instancia de gran tamaño. Sin embargo, puede ejecutar tanto en hello horizontal de la misma SAP en la misma suscripción de Azure siempre y cuando estas instancias forman parte del programa Hola. 

> [!IMPORTANT] 
> La única implementación compatible con SAP HANA en Azure (Instancias grandes) es la de Azure Resource Manager.

 

### <a name="additional-azure-vnet-information"></a>Información adicional sobre las redes virtuales de Azure

En orden tooconnect un tooExpressRoute de red virtual de Azure, debe crearse una puerta de enlace de Azure (consulte [acerca de las puertas de enlace de red virtual para ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Una puerta de enlace de Azure puede utilizarse con ExpressRoute tooan infraestructura fuera de Azure (o marca Azure grande de la instancia de tooan), o tooconnect entre redes virtuales de Azure (consulte [configurar una conexión de red virtual a red virtual para el Administrador de recursos con PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Puede conectar hello Azure de la puerta de enlace tooa como máximo cuatro diferentes conexiones de ExpressRoute siempre y cuando estas conexiones proceden de distintos enrutadores de bordes de empresa de MS (MSEE).  Para más información, vea [Infraestructura y conectividad con SAP HANA en Azure (instancias grandes)](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Hello rendimiento proporciona una puerta de enlace de Azure es distinto de los casos de uso (vea [acerca de la puerta de enlace VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). rendimiento máximo de Hello que podemos lograr con una puerta de enlace de red virtual es de 10 Gbps, mediante una conexión de ExpressRoute. Tenga en cuenta que copia archivos entre una máquina virtual de Azure que residen en una red virtual de Azure y un sistema local (como una secuencia de solo copia) no alcance el rendimiento total de Hola de puerta de enlace de hello diferentes SKU. tooleverage Hola completa ancho de banda de puerta de enlace de red virtual de hello, debe usar varias secuencias o copiar archivos diferentes flujos paralelos de un único archivo.


### <a name="networking-architecture-for-hana-large-instances"></a>Arquitectura de red para instancias grandes de HANA
Hola la arquitectura de redes para instancias de gran tamaño de HANA tal y como se muestra a continuación, se puede dividir en cuatro partes distintas:

- Las redes locales y tooAzure de conexión de ExpressRoute. Esta parte es el dominio de los clientes de Hola y tooAzure conectado a través de ExpressRoute. Esto forma parte de hello en parte inferior derecha de Hola de gráficos de hello siguientes.
- Redes de Azure con redes virtuales de Azure, como se explicó brevemente antes, que de nuevo tienen puertas de enlace. Se trata de un área donde necesita diseños de toofind Hola adecuado para sus requisitos de aplicaciones, seguridad y requisitos de cumplimiento. Uso de instancias de gran tamaño de HANA es otro punto de la cuenta en cuanto al número de redes virtuales y Azure toochoose de SKU de puerta de enlace de. Esto forma parte de hello en la esquina superior derecha de Hola de gráficos de Hola.
- Conectividad de instancias grandes de HANA a través de la tecnología de ExpressRoute en Azure. Microsoft implementa y controla esta parte. Todo lo que necesita toodo como un cliente es tooprovide algunos intervalos de direcciones IP y después de la implementación de Hola de sus activos en instancias grandes HANA conectarse Hola ExpressRoute circuit toohello VNet(s) de Azure (consulte [infraestructura de SAP HANA (instancias de gran tamaño) y conectividad en Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Redes en instancias grandes de HANA, lo que es principalmente transparente para usted como cliente.

![Red virtual de Azure conectado tooSAP HANA en Azure (instancias de gran tamaño) y local](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

hechos de Hola que usar instancias grandes de HANA no cambia Hola requisito tooget los activos locales conectados a través de ExpressRoute tooAzure. No cambia requisito hello para tener una o varias redes virtuales que se ejecutan las máquinas virtuales de Azure de hello qué nivel de aplicación de Hola de host que se conecta a instancias HANA toohello hospedadas en unidades de la instancia de HANA grande. 

las implementaciones de Hello diferencia tooSAP en puro Azure, viene con hechos de Hola que:

- unidades de instancia grande de HANA Hola de su inquilino de cliente se conectan a través de otro circuito de ExpressRoute en su VNet(s) de Azure. En condiciones de carga de orden tooseparate, Hola local tooAzure VNets ExpressRoute vínculos y los vínculos entre redes virtuales de Azure y las instancias de HANA grandes no comparten Hola mismo enrutadores.
- perfil de carga de trabajo de Hello entre la capa de aplicación de SAP de Hola y Hola HANA instancia es una naturaleza diferentes de muchas solicitudes pequeñas y ráfaga como tipo de datos transfiere (conjuntos de resultados) de SAP HANA en el nivel de aplicación Hola.
- Hola arquitectura de la aplicación de SAP es una latencia toonetwork más sensible que escenarios típicos donde obtiene intercambian datos entre local y Azure.
- puerta de enlace de red virtual de Hello tiene al menos dos conexiones de ExpressRoute y ambas conexiones compartan Hola ancho de banda máximo para los datos entrantes de puerta de enlace de red virtual de Hola.

latencia de red de Hello experimentada entre máquinas virtuales de Azure y las unidades de instancia HANA grandes puede ser mayor que una latencia de ida y vuelta de red típica de máquina virtual a la máquina virtual. Depende de la región de Azure hello, valores de hello medidos pueden superar clasificada como está por debajo del promedio en la ida y vuelta latencia Hola ms 0,7 [SAP nota #1100926 - preguntas más frecuentes: rendimiento de red](https://launchpad.support.sap.com/#/notes/1100926/E). Pero los clientes han implementado correctamente aplicaciones de SAP de producción basadas en SAP HANA en instancias grandes de SAP HANA. los clientes de Hola que implementado notifican grandes mejoras mediante la ejecución de sus aplicaciones SAP en SAP HANA según las unidades de la instancia de HANA grande. Pero debe probar exhaustivamente los procesos empresariales en instancias grandes de HANA en Azure.
 
En orden tooprovide determinista latencia entre máquinas virtuales de Azure e instancia grande de HANA, elección de Hola de hello SKU de puerta de enlace de red virtual de Azure es fundamental. A diferencia de los patrones de tráfico de hello entre locales y máquinas virtuales de Azure, patrón de tráfico de hello entre máquinas virtuales de Azure y HANA instancias de gran tamaño puede desarrollar ráfagas pequeños pero altos de solicitudes y toobe de volúmenes de datos transmitidos. En orden toohave tales ráfagas administra correctamente, es muy recomendable uso Hola de hello UltraPerformance SKU de puerta de enlace. Para clase de tipo II de HANA grandes instancia SKU hello, uso de Hola de puerta de enlace de hello UltraPerformance SKU como puerta de enlace de red virtual de Azure es obligatorio.  

> [!IMPORTANT] 
> Dada Hola total tráfico de red entre las capas de la base de datos y las aplicaciones de SAP de Hola Hola solo alto rendimiento o puerta de enlace de UltraPerformance SKU para redes virtuales se admite para conectar tooSAP HANA en Azure (instancias de gran tamaño). Para tipo II SKU de instancia de HANA grande, se admite solo Hola UltraPerformance SKU de puerta de enlace como puerta de enlace de red virtual de Azure.



### <a name="single-sap-system"></a>Único sistema SAP

infraestructura local de Hello mostrado anteriormente se conecta a través de ExpressRoute en Azure y Hola circuito de ExpressRoute se conecta a un enrutador de borde de Enterprise (MSEE) de Microsoft (vea [información general técnica de ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Una vez establecida, esa ruta se conecta a la red troncal de Microsoft Azure de Hola y todas las regiones de Azure son accesibles.

> [!NOTE] 
> Para ejecutar panoramas de SAP en Azure, conectar toohello MSEE más cercano toohello región de Azure en el panorama de SAP de Hola. Marcas de instancia grande Azure están conectadas a través de dedicado MSEE dispositivos toominimize latencia de red entre las máquinas virtuales de Azure en marcas de IaaS de Azure y la instancia grande.

puerta de enlace de red virtual para máquinas virtuales de Azure, alojar las instancias de aplicación de SAP, Hola Hello es conectado toothat circuito ExpressRoute y hello misma red virtual es tooa conectado independiente dedicado de enrutador de MSEE tooconnecting tooLarge instancia marcas.

Se trata de un ejemplo sencillo de un único sistema SAP, donde hello capa de aplicación de SAP hospedada en Azure y base de datos de SAP HANA Hola se ejecuta en SAP HANA en Azure (instancias de gran tamaño). Hola supone que ancho de banda de la puerta de enlace de red virtual de Hola de 2 GB/s o rendimiento de 10 GB/s no representa un cuello de botella.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Varios sistemas SAP o sistemas SAP grandes

Si se implementan varios sistemas SAP o grandes sistemas SAP conectarse tooSAP HANA en Azure (instancias grandes) &#39; rendimiento de hello s tooassume razonable de puerta de enlace de red virtual de hello puede convertirse en un cuello de botella. En este caso, necesita niveles de la aplicación hello toosplit en varias redes virtuales de Azure. También puede ser recomendable toocreate especial redes virtuales que se conectan instancias grandes tooHANA para casos como:

- Realizar copias de seguridad directamente desde Hola HANA instancias en instancias grandes HANA tooa VM en Azure que hospeda recursos compartidos de NFS
- Copiar las copias de seguridad de gran tamaño u otros archivos de instancia grande de HANA unidades toodisk espacio administrado de Azure.

Uso de redes virtuales independientes que host de máquinas virtuales que administrar el almacenamiento de hello evita impacto por archivo grande o transferencia de datos de instancias de gran tamaño de HANA tooAzure en hello puerta de enlace de red virtual que sirve de máquinas virtuales de Hola que ejecuta la capa de aplicación de SAP de Hola. 

Para una arquitectura de red más escalable:

- Aproveche varias redes virtuales de Azure para una sola capa de la aplicación de SAP más grande.
- Implementar una red virtual de Azure independiente para cada sistema SAP implementado, toocombining comparado estos sistemas SAP en subredes independientes en Hola misma red virtual.

 Una arquitectura de red más escalable para SAP HANA en Azure (Instancias grandes):

![Implementación de la capa de la aplicación de SAP en varias redes virtuales de Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Implementación de nivel de aplicación de SAP de Hola o componentes, a través de varias redes virtuales de Azure como se indicó anteriormente, introdujo la sobrecarga de latencia inevitable que se produjeron durante la comunicación entre las aplicaciones de hello hospedadas en esas redes virtuales de Azure. De forma predeterminada, el tráfico de red de hello entre máquinas virtuales de Azure encuentra en diferentes rutas de redes virtuales a través de hello enrutadores MSEE en esta configuración. Pero desde septiembre de 2016 es posible optimizar este enrutamiento. Hola forma toooptimize y reducir la cantidad de latencia de hello en la comunicación entre dos redes virtuales es emparejamiento redes virtuales de Azure en hello misma región. Incluso si esas redes virtuales se encuentran en suscripciones diferentes. Con red virtual de Azure emparejamiento, comunicación Hola entre máquinas virtuales en dos redes virtuales diferentes de Azure puede usar hello Azure red troncal toodirectly comunicarse entre sí. Por tanto, que muestra la latencia similares como si sería hello las máquinas virtuales en Hola misma red virtual. Mientras que el tráfico, direccionamiento intervalos de direcciones IP que están conectados a través de puerta de enlace de red virtual de Azure de hello, se enruta a través de Hola individual puerta de enlace de red virtual de hello red virtual. Puede obtener detalles acerca de la red virtual de Azure emparejamiento artículo hello [intercambio de tráfico de red virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Enrutamiento en Azure

Existen dos consideraciones importantes sobre el enrutamiento de red para SAP HANA en Azure (Instancias grandes):

1. SAP HANA en Azure (instancias de gran tamaño) solo son accesibles en las máquinas virtuales de Azure en la conexión de ExpressRoute de hello dedicado; no directamente desde el entorno local. Algunos clientes de administración y las aplicaciones que necesitan acceso directo, como SAP Solution Manager ejecuta de forma local, no se puede conectar la base de datos de SAP HANA toohello.

2. SAP HANA en las unidades de Azure (instancias de gran tamaño) tiene una dirección IP asignada desde la dirección de grupo de IP de servidor hello intervalo como cliente de hello enviado (vea [infraestructura de SAP HANA (instancias de gran tamaño) y la conectividad en Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información).  Esta dirección IP es accesible a través de hello Azure ExpressRoute que conecta tooHANA de redes virtuales de Azure en Azure (instancias de gran tamaño) y suscripciones. se asigna directamente la unidad de hardware toohello Hello dirección IP asignada fuera de ese intervalo de direcciones del grupo de IP de servidor y no es NAT'ed ya que esto era el caso de hello en hello las primeras implementaciones de esta solución. 

> [!NOTE] 
> Si necesita tooconnect tooSAP HANA en Azure (instancias de gran tamaño) en un _almacenamiento de datos_ escenario, donde las aplicaciones o los usuarios finales necesitan tooconnect toohello SAP HANA base de datos (ejecuta directamente), debe ser otro componente de red usar: un servidor proxy inverso tooroute datos, tooand de. Por ejemplo, F5 BIG-IP, NGINX con Traffic Manager implementado en Azure como solución de enrutamiento de tráfico y firewall virtual.

### <a name="internet-connectivity-of-hana-large-instances"></a>Conectividad a Internet de instancias grandes de HANA
Las instancias grandes de HANA NO tienen conectividad directa a Internet. Esto limita su capacidad para, por ejemplo registrar imagen del sistema operativo Hola directamente con el proveedor del SO Hola. Por lo tanto, tendrá que toowork con servidor de SLES SMT local o al administrador de suscripción de RHEL

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Cifrado de datos entre máquinas virtuales de Azure e instancias grandes de HANA
Los datos transferidos entre las instancias grandes de HANA y las máquinas virtuales de Azure no se cifran. Sin embargo, únicamente para el intercambio de hello entre hello lado HANA DBMS y las aplicaciones en función de JDBC/ODBC puede habilitar el cifrado de tráfico. Consulte [esta documentación de SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false).

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Uso de unidades de instancia grande de HANA en varias regiones

Puede que tenga otro toodeploy motivos SAP HANA en Azure (instancias de gran tamaño) en varias regiones de Azure, además de recuperación ante desastres. Quizás desee tooaccess HANA grandes instancias de cada una de las máquinas virtuales de hello implementadas en hello redes virtuales diferentes en regiones de Hola. Puesto que asignar las direcciones IP de hello toohello diferentes unidades de HANA grandes instancias no se propagan más allá de hello redes virtuales de Azure (que están conectados directamente a través de sus instancias de toohello de puerta de enlace), hay un ligero cambiar toohello introducida por encima de diseño de red virtual: un Puerta de enlace de red virtual Azure puede controlar cuatro circuitos ExpressRoute diferentes fuera MSEEs diferentes y cada red virtual que está conectado tooone de sellos de hello instancia grande puede ser la marca de la instancia grande de toohello conectado en otra región de Azure.

![Redes virtuales de Azure conectado tooAzure marcas de instancia grande en diferentes regiones de Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Hola por encima de la ilustración, se muestra cómo Hola diferentes redes virtuales de Azure en ambas regiones son circuitos ExpressRoute diferentes conectados tootwo tooconnect usado tooSAP HANA en Azure (instancias de gran tamaño) se encuentran en ambas regiones de Azure. las conexiones de Hello acaban de introducir son líneas rojas rectangular de Hola. Con estas conexiones, fuera de hello redes virtuales de Azure, máquinas virtuales de Hola que se ejecutan en una de esas redes virtuales puede tener acceso a cada uno de los diferentes unidades de instancias de gran tamaño de HANA Hola implementados en dos regiones de Hola. Como se ve en gráficos de hello anteriores, se supone que tiene dos conexiones de ExpressRoute de local toohello dos regiones de Azure; se recomienda por motivos de recuperación ante desastres.

> [!IMPORTANT] 
> Si se utilizan varios circuitos ExpressRoute, anteponiéndole la ruta de acceso de AS y la configuración de BGP de preferencia Local debe ser tooensure uso apropiado de enrutamiento del tráfico de.


