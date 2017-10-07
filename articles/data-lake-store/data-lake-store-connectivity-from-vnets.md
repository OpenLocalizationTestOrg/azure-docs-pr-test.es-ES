---
title: "aaaConnect tooAzure almacén de Data Lake de redes virtuales | Documentos de Microsoft"
description: "Conectar el almacén de Data Lake de tooAzure de redes virtuales de Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Acceso a Azure Data Lake Store desde máquinas virtuales de una red virtual de Azure
Azure Data Lake Store es un servicio de PaaS que se ejecuta en direcciones IP de Internet pública. Cualquier servidor que se puede conectar toohello can de Internet pública suelen conectarse así los extremos de almacén de Data Lake tooAzure. De forma predeterminada, todas las máquinas virtuales que se encuentran en redes virtuales de Azure pueden tener acceso a Internet de hello y, por lo que pueden tener acceso a almacén de Azure Data Lake. Sin embargo, es posible tooconfigure las máquinas virtuales en una red virtual toonot tiene toohello de acceso a Internet. Para estas máquinas virtuales, almacén de Data Lake de tooAzure de acceso está restringido así. Bloquear acceso público a Internet para las máquinas virtuales en redes virtuales de Azure puede realizarse mediante cualquiera de hello enfoque.

* Configurando grupos de seguridad de red (NSG)
* Configurando rutas definidas por el usuario (UDR)
* Intercambiando las rutas a través de BGP (sector estándar Protocolo de enrutamiento dinámico) cuando ExpressRoute se usa ese bloque tener acceso a Internet toohello

En este artículo, aprenderá cómo tooenable tener acceso a almacén de toohello Azure Data Lake desde máquinas virtuales de Azure que hayan sido restringido tooaccess recursos usando uno de estos tres métodos Hola mencionados anteriormente.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Habilitar la conectividad tooAzure almacén de Data Lake desde máquinas virtuales con conectividad restringido
Almacén de Azure Data Lake de tooaccess desde máquinas virtuales de este tipo, debe configurarlos dirección IP de hello tooaccess donde hello cuenta de almacén de Azure Data Lake está disponible. Puede identificar las direcciones IP de Hola para las cuentas de almacén de Data Lake mediante la resolución de nombres DNS de Hola de sus cuentas (`<account>.azuredatalakestore.net`). Para ello, puede usar herramientas como **nslookup**. Abra un símbolo del sistema en el equipo y ejecute el siguiente comando de Hola.

    nslookup mydatastore.azuredatalakestore.net

salida de Hello es similar a la siguiente Hola. Hola valor contra **dirección** propiedad es la dirección IP de hello asociada a su cuenta de almacén de Data Lake.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Habilitación de la conectividad en las máquinas virtuales restringidas mediante NSG
Cuando se utiliza una regla NSG tooblock tener acceso a Internet, toohello, a continuación, puede crear otro NSG que permite acceso toohello dirección de IP del almacén de datos Lake. Obtenga más información sobre las reglas de NSG en la página donde se explica qué es [un grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md). Para obtener instrucciones sobre cómo ven los NSG toocreate [cómo NSG toomanage mediante Hola portal de Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Habilitación de la conectividad en las máquinas virtuales restringidas mediante UDR o ExpressRoute
Una vez rutas, UDRs o intercambian BGP rutas, tooblock usado toohello de acceso a Internet, una ruta especial debe toobe configurado para que las máquinas virtuales en estas subredes pueden tener acceso a los puntos de conexión de almacén de Data Lake. Para obtener más información, consulte el artículo donde se explica [qué son las rutas definidas por el usuario](../virtual-network/virtual-networks-udr-overview.md). Para obtener instrucciones sobre cómo crear UDR, consulte el artículo sobre cómo [crear UDR en Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Habilitación de la conectividad en las máquinas virtuales restringidas mediante ExpressRoute
Cuando se configura un circuito ExpressRoute, servidores locales de hello pueden tener acceso a almacén de Data Lake a través de emparejamiento público. Para obtener más información sobre cómo configurar ExpressRoute para pares públicos, consulte las [preguntas más frecuentes de ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Otras referencias
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Protección de los datos almacenados en Azure Data Lake Store](data-lake-store-security-overview.md)

