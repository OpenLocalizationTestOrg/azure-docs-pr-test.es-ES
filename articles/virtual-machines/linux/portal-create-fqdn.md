---
title: aaaCreate FQDN para una VM de Linux en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un nombre de dominio completo o FQDN, para un administrador de recursos según la máquina virtual en hello portal de Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Crear un nombre de dominio completo de hello portal de Azure para una VM de Linux

Cuando crea una máquina virtual (VM) en hello [portal de Azure](https://portal.azure.com), automáticamente se crea un recurso IP público para la máquina virtual de Hola. Utilice este Hola acceso de tooremotely de dirección IP virtual. Aunque el portal de hello no crea un [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN, puede agregar uno una vez hello máquina virtual creada. En este artículo se muestra hello pasos toocreate un nombre DNS o el FQDN.

## <a name="create-a-fqdn"></a>Creación de un FQDN
En este artículo se supone que ya ha creado una máquina virtual. Si es necesario, puede [crear una máquina virtual en el portal de hello](quick-create-portal.md) o [con hello Azure CLI](quick-create-cli.md). Una vez que la máquina virtual está en funcionamiento, siga estos pasos:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Ahora puede conectarse remotamente toohello el nombre de máquina virtual con este DNS como con `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Pasos siguientes
Ahora que la máquina virtual tiene un nombre DNS y una IP pública, puede implementar marcos y servicios de aplicaciones comunes, como nginx, MongoDB, Docker, etc.

También puede leer más sobre el [uso de Resource Manager](../../azure-resource-manager/resource-group-overview.md) para obtener sugerencias sobre la creación de las implementaciones de Azure.

