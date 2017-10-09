---
title: "características de seguridad de aaaAzure utilizadas con máquinas virtuales de Azure | Documentos de Microsoft"
description: " Información general de características de seguridad de Azure de hello básicas que puede usarse con máquinas virtuales de Azure. Máquinas virtuales de Azure dé Hola flexibilidad de virtualización sin necesidad de toobuy y mantener el hardware físico de Hola que ejecuta Hola VM. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Información general de seguridad de Azure Virtual Machines
Azure Virtual Machines permite implementar una amplia gama de soluciones informáticas con agilidad. Gracias a la compatibilidad con Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP y Azure BizTalk Services, puede implementar cualquier carga de trabajo y cualquier idioma en casi cualquier sistema operativo.

Un proporciona Hola flexibilidad de virtualización sin necesidad de toobuy y mantener el hardware físico de Hola de máquina virtual de Azure que ejecute máquina virtual de Hola.  Puede compilar e implementar las aplicaciones con garantía de Hola que los datos están protegidos y seguros en nuestros centros de datos muy seguro.

Con Azure, puede crear soluciones compatibles con seguridad mejorada que:

* Protegen sus máquinas virtuales de virus y malware.
* Protegen con cifrado su información confidencial.
* Protegen el tráfico de red.
* Identifican y detectan amenazas.
* Satisfacen los requisitos de cumplimiento.

objetivo de Hola de este artículo es tooprovide una visión general de las características de seguridad de Azure de hello principales que puede usarse con máquinas virtuales. También se proporcionan los vínculos tooarticles que proporcionan detalles de cada característica, por lo que puede obtener más información.  

en este artículo se trata toobe de capacidades de seguridad de Hello core Máquina Virtual de Azure:

* Antimalware
* Módulo de seguridad de hardware
* Cifrado de discos de máquinas virtuales
* Copia de seguridad de máquina virtual
* Azure Site Recovery
* Redes virtuales
* Informes y administración de directivas de seguridad
* Cumplimiento normativo

## <a name="antimalware"></a>Antimalware
Con Azure, puede usar el software antimalware de los proveedores de seguridad, como Microsoft, Symantec, Trend Micro y Kaspersky tooprotect las máquinas virtuales desde archivos malintencionados, adware y otras amenazas. Vea Hola aprendizaje sección más debajo toofind artículos en soluciones de socios.

Microsoft Antimalware para servicios en la nube y máquinas virtuales de Azure es una funcionalidad de protección en tiempo real que permite identificar y eliminar virus, spyware y otro software malintencionado.  Microsoft Antimalware proporciona configurable genera una alerta cuando conoce tooinstall de intentos de software malintencionado o no deseado propio o ejecutarse en los sistemas de Azure.

Microsoft Antimalware es una solución de agente único para aplicaciones y entornos de inquilino, toorun diseñado en segundo plano de hello sin intervención humana. Puede implementar la protección en función de las necesidades de Hola de las cargas de trabajo de aplicación, con cualquier básica proteger de forma predeterminada o avanzadas de configuración personalizada, incluida la supervisión de antimalware.

Al implementar y habilitar Microsoft Antimalware, Hola siguiendo las características básicas de está disponible:

* Protección en tiempo real: supervisa la actividad en los servicios en la nube y en máquinas virtuales toodetect y bloquear la ejecución de malware.
* Análisis programados - realiza periódicamente destino malware toodetect análisis, incluidos los programas que se ejecutan activamente.
* Corrección de malware: actúa automáticamente sobre el malware detectado y elimina o pone en cuarentena los archivos malintencionados y limpia las entradas del Registro malintencionadas.
* Las actualizaciones de firma - automáticamente instala hello más reciente protección firmas (las definiciones de virus) tooensure la protección está actualizada en una frecuencia predeterminada.
* Las actualizaciones de motor de antimalware: automáticamente actualizaciones Hola motor de Antimalware de Microsoft.
* Las actualizaciones de la plataforma de antimalware: automáticamente actualizaciones Hola plataforma Microsoft Antimalware.
* Protección activa - informa tooAzure telemetría metadatos acerca de las amenazas detectadas y recursos sospechosa tooensure rápida respuesta y permite firma sincrónico en tiempo real entrega a través de hello Microsoft Active Protection System (MAPS).
* Ejemplos de informes: proporciona y ejemplos de informes toohello Microsoft Antimalware service toohelp refinar servicio hello y solución de problemas de habilitar.
* Exclusiones: permite la aplicación y servicio administradores tooconfigure determinados archivos, procesos y unidades de tooexclude ellos de la protección y análisis de rendimiento y otras razones.
* Recopilación de eventos de antimalware: registra el estado del servicio antimalware hello, las actividades sospechosas y las acciones correctoras tomadas en el registro de eventos del sistema operativo de Hola y recopila en la cuenta de almacenamiento de Azure del cliente de Hola.

Obtener más información: toolearn más información acerca de tooprotect de software antimalware sus máquinas virtuales, vea:

* [Microsoft Antimalware para Cloud Services y Virtual Machines de Azure](azure-security-antimalware.md)
* [Implementación de soluciones antimalware en Azure Virtual Machines](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [¿Cómo tooinstall y configurar trendmicro Deep Security como un servicio en una VM de Windows](../virtual-machines/windows/classic/install-trend.md)
* [¿Cómo tooinstall y configurar Symantec Endpoint Protection en una VM de Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Soluciones de seguridad en hello Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Módulo de seguridad de hardware
Las protecciones del cifrado y la autenticación se pueden mejorar si se mejora de la clave de seguridad. Puede simplificar la administración de Hola y seguridad de los secretos críticos y claves almacenándolos en el almacén de claves de Azure. El almacén de claves proporciona Hola opción toostore las claves en los estándares de hardware seguridad tooFIPS certificada de módulos (HSM) 140-2 nivel 2. Sus claves de cifrado de SQL Server para copias de seguridad o [cifrado de datos transparente](https://msdn.microsoft.com/library/bb934049.aspx) se pueden almacenar en el Almacén de claves con otras claves y secretos de sus aplicaciones. Permisos y acceso a los elementos protegido de toothese se administran a través de [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Más información:

* [¿Qué es el Almacén de claves de Azure?](../key-vault/key-vault-whatis.md)
* [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md)
* [Blog del Almacén de claves de Azure](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Cifrado de discos de máquinas virtuales
Azure Disk Encryption es una nueva funcionalidad que permite cifrar los discos de máquinas virtuales de Azure de Windows y Linux. Cifrado de disco de Azure utiliza el estándar del sector de hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) característica de Windows y hello [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt) característica de cifrado de volumen de Linux tooprovide hello OS y discos de datos de Hola.

solución de Hola se integra con el almacén de claves de Azure toohelp controlar y administrar claves de cifrado de disco de Hola y secretos en su suscripción de almacén de claves, asegurándose de que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.

Más información:

* [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Azure Disk Encryption for Linux and Windows Virtual Machines (Azure Disk Encryption para máquinas virtuales Linux y Windows)](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Cifrado de una máquina virtual de Azure](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Copia de seguridad de máquina virtual
Azure Backup es una solución escalable que protege los datos de su aplicación sin necesidad de realizar ninguna inversión y afrontando unos costos operativos mínimos. Los errores de una aplicación pueden dañar los datos, y los errores humanos pueden crear errores en las aplicaciones. Con Azure Backup, las máquinas virtuales que ejecutan Windows y Linux están protegidas.

Más información:

* [¿Qué es Azure Backup?](../backup/backup-introduction-to-azure-backup.md)
* [Azure Backup](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [P+F del servicio Azure Backup](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Una parte importante de la estrategia BCDR de su organización es pensar en cómo se producen tookeep corporativa cargas de trabajo y aplicaciones de seguridad y ejecución cuando se planean e interrupciones imprevistas. Azure Site Recovery ayuda a coordinar la replicación, la conmutación por error y la recuperación de aplicaciones y cargas de trabajo para que estén disponibles desde una ubicación secundaria si la ubicación principal deja de funcionar.

Site Recovery:

* **Simplifica la estrategia BCDR** : Site Recovery resulta fácil toohandle replicación, conmutación por error y recuperación de varias cargas de trabajo de negocio y aplicaciones desde una sola ubicación. Site recovery organiza la replicación y la conmutación por error pero no intercepta los datos de su aplicación ni obtiene información alguna sobre ella.
* **Proporciona replicación flexible** : con Site Recovery puede replicar las cargas de trabajo que se ejecutan en máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos de Windows o Linux.
* **Admite la conmutación por error y recuperación** : recuperación del sitio proporciona las conmutaciones por error de prueba toosupport de recuperación ante desastres sin afectar a entornos de producción. También puede ejecutar conmutaciones por error planeadas sin pérdidas de datos para interrupciones previstas o conmutaciones por error con una pérdida de datos mínima (según la frecuencia de replicación) ante desastres inesperados. Después de la conmutación por error, puede tooyour conmutación por recuperación los sitios primarios. Site Recovery proporciona planes de recuperación que pueden incluir scripts y libros de Azure Automation para que pueda personalizar la conmutación por error y la recuperación de aplicaciones de varios niveles.
* **Elimina el centro de datos secundario** : puede replicar al sitio secundario en local tooa o tooAzure. Usar Azure como destino de recuperación ante desastres elimina Hola costo y la complejidad de mantenimiento de un sitio secundario. Los datos replicados se almacenan en Azure Storage.
* **Se integra con tecnologías de BCDR existentes** : Site Recovery se asocia con otras características de BCDR de la aplicación. Por ejemplo, puede utilizar Site Recovery tooprotect Hola SQL Server back-end de cargas de trabajo corporativos. Esto incluye compatibilidad nativa para conmutación por error de SQL Server AlwaysOn toomanage Hola de grupos de disponibilidad.

Más información:

* [¿Qué es Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
* [¿Cómo funciona Azure Site Recovery?](../site-recovery/site-recovery-components.md)
* [¿Qué cargas de trabajo se pueden proteger con Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Redes virtuales
Las máquinas virtuales necesita conectividad de red. toosupport ese requisito, Azure requiere toobe de máquinas virtuales conectada tooan red Virtual de Azure. Red Virtual de Azure es una construcción lógica que se basa en el tejido de red físico de Azure Hola. Cada red virtual lógica de Azure está aislada de todas las demás redes virtuales de Azure. Este aislamiento ayuda a garantizar que el tráfico de red en sus implementaciones no es accesible tooother clientes de Microsoft Azure.

Más información:

* [Azure Network Security Overview (Información general sobre Azure Network Security)](security-network-overview.md)
* [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md)
* [Networking features and partnerships for Enterprise scenarios (Características de red y asociaciones para escenarios empresariales)](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Informes y administración de directivas de seguridad
Centro de seguridad de Azure le ayuda a evitar, detectar y responder toothreats y proporciona que mayor visibilidad en y control sobre, seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Azure Security Center le ayuda a optimizar y controlar la seguridad de máquinas virtuales al:

* Proporcionar [recomendaciones de seguridad](../security-center/security-center-recommendations.md) para máquina virtual, como aplicar actualizaciones del sistema, configurar puntos de conexión de listas de control de acceso, habilitar antimalware, habilitar grupos de seguridad de red y aplicar cifrado de discos.
* Supervisión del estado de Hola de sus máquinas virtuales

Más información:

* [Introducción tooAzure centro de seguridad](../security-center/security-center-intro.md)
* [Preguntas más frecuentes sobre el Centro de seguridad de Azure](../security-center/security-center-faq.md)
* [Guía de planeamiento y operaciones de Azure Security Center](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Cumplimiento normativo
Azure Virtual Machines tiene las certificaciones de FISMA, FedRAMP, HIPAA, PCI DSS nivel 1 y otros programas de cumplimiento fundamentales. Esta certificación resulta más fácil para sus propios requisitos de cumplimiento de las aplicaciones de Azure toomeet y para su negocio tooaddress una amplia gama de requisitos de regulación nacionales e internacionales.

Más información:

* [Centro de confianza de Microsoft: conformidad](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Trusted Cloud: Microsoft Azure Security, Privacy, and Compliance (La nube de confianza: Seguridad, privacidad y cumplimiento de Microsoft Azure)](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
