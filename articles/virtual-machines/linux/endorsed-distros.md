---
title: aaaEndorsed distribuciones de Linux | Documentos de Microsoft
description: Aprenda sobre Linux en las distribuciones aprobadas de Azure, incluyendo instrucciones para Ubuntu, CentOS, Oracle y SUSE.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux en distribuciones aprobadas por Azure
Asociados de proporcionan las imágenes de Linux en hello Azure Marketplace. Estamos trabajando con diversas Linux Comunidades tooadd aún más lista de distribución con el respaldo de toohello de tipos. En hello mientras tanto, para las distribuciones que no están disponibles de hello Marketplace, puede siempre hacer su propios Linux siguiendo las directrices de Hola a [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Distribuciones y versiones admitidas
Hello tabla siguiente enumeran las distribuciones de Linux de Hola y versiones que son compatibles con Azure. Consulte demasiado[imágenes de compatibilidad con Linux de Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) para obtener más información.

controladores de servicios de integración de Linux (LIS) Hola para Hyper-V y Azure son módulos de kernel que Microsoft directamente contribuye toohello ascendente kernel de Linux.  Algunos controladores LIS están integradas en el núcleo de la distribución de Hola de forma predeterminada. Hay distribuciones anteriores que se basan en Red Hat Enterprise (RHEL)/CentOS disponibles como descarga independiente en [Linux Integration Services versión 4.1 para Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Vea [requisitos de kernel de Linux](create-upload-generic.md#linux-kernel-requirements) para obtener más información acerca de los controladores LIS Hola.

Hola agente Linux de Azure ya está instalado previamente en imágenes de Azure Marketplace de Hola y normalmente está disponible desde el repositorio de paquetes de la distribución de Hola. El código fuente se puede encontrar en [GitHub](https://github.com/azure/walinuxagent).

| Distribución | Versión | Controladores | Agente |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3: [Descarga de LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4+: en kernel |Paquete: en el [repositorio](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/), en "WALinuxAgent" <br/>Código fuente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |En kernel |Código fuente: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+, 8.2+ |En kernel |Paquete: en el repositorio, en "waagent"  <br/>Código fuente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |En kernel |Paquete: en el repositorio, en "WALinuxAgent"  <br/>Código fuente: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |En kernel |Paquete: en el repositorio, en "WALinuxAgent"  <br/>Código fuente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES para SAP<br>11 SP4<br>12 SP1+|En kernel |Paquete:<p> para 11 en el repositorio [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools)<br>para 12, que se incluye en el módulo "Nube pública" en "python-azure-agent"<br/>Código fuente: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |En kernel |Paquete: En el repositorio [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) en "python-azure-agent" <br/>Código fuente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |En kernel |Paquete: en el repositorio, en "WALinuxAgent"  <br/>Código fuente: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Asociados

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Desde el sitio Web de Hola CoreOS:

*CoreOS está diseñado para la seguridad, coherencia y confiabilidad. En lugar de instalar paquetes a través de yum o apt, CoreOS usa Linux contenedores toomanage los servicios en un nivel más alto de abstracción. Un código y todas las dependencias de un servicio único se empaquetan dentro de un contenedor que se puede ejecutar en uno o varios equipos de CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ es una empresa de servicios que se especializa en hello desarrollo e implementación de soluciones profesionales mediante el uso de software gratuito y de consultoría independiente. Como especialistas en código abierto líderes en el sector, Credative goza de reconocimiento en el ámbito internacional y numerosos departamentos de TI recurren a su soporte técnico. Actualmente, Credativ está preparando con Microsoft imágenes de Debian correspondientes a Debian 8 (Jessie) y Debian antes de 7 (Wheezy). Las imágenes están diseñado especialmente toorun en Azure y se pueden administrar con facilidad a través de la plataforma de Hola. Credativ también admitirá mantenimiento a largo plazo de Hola y actualización de las imágenes de Debian Hola de Azure a través de sus centros de soporte técnico de origen abierto.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Estrategia de Oracle es toooffer una amplia gama de soluciones para nubes públicas y privadas. estrategia de Hello ofrece a los clientes elección y flexibilidad en la forma en que distribuyen software de Oracle en nubes de Oracle y otras nubes. Asociación de Oracle con Microsoft habilita los clientes de software de Oracle de toodeploy en nubes públicas y privadas de Microsoft con confianza Hola de certificación y soporte técnico de Oracle.  El compromiso y la inversión de Oracle en las soluciones de nubes públicas y privadas de Oracle siguen intactos.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Hola de los principales proveedores de todo el mundo de soluciones de código abierto, Red Hat ayuda a más del 90% de las empresas de Fortune 500 resolver desafíos de negocio, alinear su TI y estrategias empresariales y preparar para hello futuro de la tecnología. Red Hat hace esto ofreciendo soluciones seguras a través de un modelo de negocio abierto y un modelo de suscripción asequible y predecible.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server en Azure es una plataforma probada que brinda confiabilidad y seguridad de nivel superior para la informática en nube. Plataforma de Linux versátil de SUSE integra perfectamente con toodeliver de servicios de nube de Azure un entorno de nube fácil de administrar. Con más de 9,200 aplicaciones certificadas de más de 1 800 fabricantes independientes de software para SUSE Linux Enterprise Server, SUSE garantiza que las cargas de trabajo ejecuta admitidos en el centro de datos de Hola se pueden implementar con confianza en Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

La ingeniería de Canonical y la gobernanza de comunidad abierta impulsan el éxito de Ubuntu en la informática en la nube, servidor y cliente, incluidos servicios personales en la nube para consumidores. Visión del canónica de una plataforma totalmente unificada y libre en Ubuntu, desde teléfonos toocloud, proporciona una familia de interfaces coherentes para phone hello, Tablet PC, TV y el escritorio. Esta visión hace primera opción de Hola de Ubuntu para las diversas entidades de fabricantes de toohello de proveedores de nube pública de electrónica de consumo y un favorito entre técnicos individuales.

Con los desarrolladores y centros de ingeniería alrededor de Hola a todos, canónica es toopartner colocado de forma exclusiva con creadores de hardware, los proveedores de contenido y toomarket soluciones Ubuntu de toobring de los desarrolladores de software para equipos, servidores y dispositivos de mano.
