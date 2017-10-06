---
title: Unido aaaDomain arquitectura de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooplan Unidos al dominio HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planeamiento de clústeres de Hadoop unidos a un dominio de Azure en HDInsight

Hello Hadoop tradicional es un clúster de usuario único. Es apropiado para la mayor parte de las empresas que tienen equipos de aplicaciones pequeños que generan grandes cargas de trabajo de datos. A medida que aumenta la popularidad de Hadoop, muchas empresas empiezan a usar un modelo en el que los equipos de TI administran clústeres y varios equipos de aplicaciones comparten los clústeres. Por lo tanto, las funcionalidades de clústeres multiusuario que implica que se encuentran entre Hola más solicitadas funcionalidades de HDInsight de Azure.

En lugar de generar su propia autenticación multiusuario y la autorización, HDInsight se basa en el proveedor de identidades de más popular de hello--Active Directory (AD). funcionalidad de seguridad eficaz de Hello en AD puede ser usado toomanage autorización multiusuario en HDInsight. Mediante la integración de HDInsight con AD, puede comunicarse con los clústeres de hello mediante las credenciales de AD. HDInsight asigna un usuario tooa local Hadoop usuario de AD, por lo que todos los servicios que se ejecutan en HDInsight de Hola (Ambari, Hive thrift de Spark de servidor, Cazador, servidor etc.) funcionan sin problemas para usuario autenticado de Hola.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integración de HDInsight con AD y AD en la máquina virtual de IaaS

Mediante la integración de HDInsight con Azure AD o AD en VM de Iaas, nodos de clúster de HDInsight de hello son dominio tooa Unidos a un dominio. HDInsight crea a entidades de servicio para hello Hadoop servicios que se ejecutan en el clúster de Hola y las coloca en una unidad organizativa especificada (OU) en Azure AD o AD en VM de IaaS. HDInsight también crea asignaciones de DNS inversas en dominio de Hola para hello direcciones IP de los nodos de Hola que están toohello Unidos a un dominio.

Esta configuración se puede lograr mediante el uso de varias arquitecturas. Puede elegir entre Hola después de arquitecturas.

**HDInsight integrado con AD que se ejecuta en Azure IaaS**

Se trata de una arquitectura más sencilla de Hola para integrar HDInsight con Active Directory. Hola controlador de dominio de AD se ejecuta en uno (o varias) máquinas virtuales (VM) en Azure. Normalmente, estas máquinas virtuales se encuentran en una red virtual. Configure otra red virtual de clúster de HDInsight Hola. Para un directorio de línea de visión tooActive de HDInsight toohave, necesita toopeer estas redes virtuales mediante el uso de [emparejamiento de VNet a VNet](../virtual-network/virtual-network-create-peering.md). Si crea Hola Active Directory en ARM, a continuación, puede crear Hola Active Directory y HDInsight en Hola misma red virtual y no es necesario toodo emparejamiento. 

![Topología de clúster de HDInsight de unión a dominio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> En esta arquitectura, no puede usar el almacén de Azure Data Lake con clúster de HDInsight Hola.


Requisitos previos de Active Directory:

* Un [unidad organizativa](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) deben crearse, que se coloca dentro de máquinas virtuales de clúster de HDInsight de Hola y Hola entidades de servicio utilizadas por el clúster de Hola.
* [Protocolo ligero de acceso a directorios](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAP) debe configurarse para comunicarse con AD. Hola tooset de certificado que se usa seguridad LDAPS debe ser un certificado real (no un certificado autofirmado).
* Las zonas DNS inversas deben crearse en el dominio de hello para el intervalo de direcciones IP de Hola de subred de HDInsight de hello (por ejemplo, 10.2.0.0/24 en la imagen anterior de hello).
* Se necesita una cuenta de servicio o una cuenta de usuario. Utilice este clúster de HDInsight de cuenta toocreate Hola. Esta cuenta debe tener los siguientes permisos de hello:

    - Objetos de entidad de servicio de toocreate de permisos y objetos de equipo dentro de la unidad organizativa de Hola
    - Reglas de proxy DNS inversas de permisos toocreate
    - Dominio de Active Directory de permisos toojoin máquinas toohello

**HDInsight integrado con una instancia de Azure AD solo en la nube**

Para una instancia de Azure AD solo en la nube, configure un controlador de dominio para que HDInsight se pueda integrar con Azure AD. Esto se logra mediante el uso de [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS crea máquinas de controlador de dominio en la nube de Hola y proporciona las direcciones IP para ellos. Crea dos controladores de dominio para lograr alta disponibilidad.

Actualmente, Azure AD DS solo existe en redes virtuales clásicas. Solo es accesible mediante el uso de hello portal de Azure clásico. Hola HDInsight red virtual existe en el portal de Azure, que debe toobe Hola emparejar con la red virtual clásica de hello mediante el uso de intercambio de tráfico de red virtual a red virtual.

> [!NOTE]
> Emparejamiento entre una red virtual clásica y red virtual requiere que ambas redes virtuales están en un administrador de recursos de Azure Hola la misma región y en Hola misma suscripción de Azure.

![Topología de clúster de HDInsight de unión a dominio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Requisitos previos de Azure AD:

* Un [unidad organizativa](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) deben crearse dentro de la que colocar máquinas virtuales del clúster de HDInsight de Hola y Hola entidades de servicio utilizadas por el clúster de Hola.
* Al configurar Azure AD DS, se debe configurar [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md). Hola tooset de certificado que se usa seguridad LDAPS debe ser un certificado real (no un certificado autofirmado).
* Las zonas DNS inversas deben crearse en el dominio de hello para el intervalo de direcciones IP de Hola de subred de HDInsight de hello (por ejemplo, 10.2.0.0/24 en la imagen anterior de hello).
* [Hash de contraseña](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) deben sincronizarse desde Azure AD tooAzure AD DS.
* Se necesita una cuenta de servicio o una cuenta de usuario. Utilice este clúster de HDInsight de cuenta toocreate Hola. Esta cuenta debe tener los siguientes permisos de hello:

    - Objetos de entidad de servicio de toocreate de permisos y objetos de equipo dentro de la unidad organizativa de Hola
    - Reglas de proxy DNS inversas de permisos toocreate
    - Dominio de permisos toojoin máquinas toohello Azure AD

## <a name="next-steps"></a>Pasos siguientes
* tooconfigure un clúster de HDInsight Unidos a un dominio, consulte [configurar clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-configure.md).
* clústeres de HDInsight Unidos a un dominio de toomanage, consulte [administrar clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-manage.md).
* directivas de Hive tooconfigure y ejecución de las consultas de Hive, consulte [Hive configurar directivas para clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-run-hive.md).
* consultas de Hive toorun a través de SSH en clústeres de HDInsight Unidos a un dominio, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
