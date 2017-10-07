---
title: toocreate de filtro de paquetes de FreeBSD aaaUse un firewall en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy una NAT FreeBSD de firewall PF en Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>¿Cómo toocreate de filtro de paquetes de FreeBSD toouse un firewall seguro en Azure
Este artículo se detallan cómo toodeploy un firewall NAT con filtro de compresor de FreeBSD a través de la plantilla del Administrador de recursos de Azure para el escenario común de servidor web.

## <a name="what-is-pf"></a>¿Qué es el filtro de paquetes (PF)?
PF es un filtro de paquetes con estado con licencia para BSD, una pieza central del software de cortafuegos. Esta herramienta se ha desarrollado rápidamente y ahora tiene varias ventajas con respecto a otros firewalls disponibles. Traducción de direcciones de red (NAT) está en PF desde el día uno, a continuación, el programador de paquetes y administración de cola activa se han integrado en PF, mediante la integración de hello ALTQ y lo que puede configurar mediante la configuración de PF. Características como pfsync y CARP para conmutación por error y redundancia, authpf para la autenticación de sesión y proxy ftp tooease Firewall Hola difíciles de protocolo FTP, también han extendido PF. En resumen, PF es un firewall eficaz y con numerosas características. 

## <a name="get-started"></a>Primeros pasos
Si está interesado en la configuración de un firewall seguro en la nube de Hola para los servidores web, vamos a empezar a trabajar. También puede aplicar scripts de hello usados en este tooset de plantilla de Azure Resource Manager de su topología de red.
plantilla de Azure Resource Manager Hola configurar una máquina virtual de FreeBSD que realiza /redirection NAT con dos máquinas virtuales de FreeBSD y PF con el servidor de web Nginx de hello instalado y configurado. Además tooperforming NAT para dos servidores web de hello salida tráfico, máquina virtual NAT/redirección de hello intercepta las solicitudes HTTP y los redirigirá toohello dos servidores web en modo round-robin. Hola red virtual usa Hola privadas no enrutables IP dirección espacio 10.0.0.2/24 y puede modificar Hola parámetros de plantilla de Hola. plantilla de Azure Resource Manager Hello también define una tabla de rutas para hello toda red virtual, que es una colección de rutas individuales usa rutas de Azure predeterminado toooverride en función de la dirección IP de destino de Hola. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Implementación a través de la CLI de Azure
Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login). Cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un nombre de grupo de recursos `myResourceGroup` en hello `West US` ubicación.

```azurecli
az group create --name myResourceGroup --location westus
```

A continuación, implementar la plantilla de hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) con [Crear implementación de grupo az](/cli/azure/group/deployment#create). Descargar [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) en Hola la misma ruta de acceso y definir sus propios valores de recursos, como `adminPassword`, `networkPrefix`, y `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Después de aproximadamente cinco minutos, obtendrá información Hola de `"provisioningState": "Succeeded"`. Puede ssh toohello front-end VM (NAT) o tener acceso a servidor de web Nginx en un explorador mediante la dirección IP pública de Hola o FQDN del servidor front-end de hello VM (NAT). Hello en el ejemplo siguiente se enumera FQDN y la dirección IP pública que asigna toohello front-end VM (NAT) en hello `myResourceGroup` grupo de recursos. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Pasos siguientes
¿Desea tooset seguridad su propia NAT en Azure? El código abierto es gratis, pero ¿es eficaz? PF es una buena elección. Mediante la plantilla de hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), solo necesita tooset de cinco minutos de un firewall NAT con FreeBSD de equilibrio de carga round robin PF en Azure para el escenario común de servidor web. 

Si desea que la oferta de hello toolearn de FreeBSD en Azure, consulte demasiado[tooFreeBSD de introducción en Azure](freebsd-intro-on-azure.md).

Si desea más información acerca de PF tooknow, consulte demasiado[manual de FreeBSD](https://www.freebsd.org/doc/handbook/firewalls-pf.html) o [manual del usuario PF](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
