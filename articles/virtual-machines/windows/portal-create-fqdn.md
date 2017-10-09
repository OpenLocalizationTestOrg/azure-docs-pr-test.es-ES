---
title: "aaaCreate FQDN para una máquina virtual de Windows en hello portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un nombre de dominio completo o FQDN, para un administrador de recursos según la máquina virtual en hello portal de Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Crear un nombre de dominio completo de hello portal de Azure para una VM de Windows

Cuando crea una máquina virtual (VM) en hello [portal de Azure](https://portal.azure.com), automáticamente se crea un recurso IP público para la máquina virtual de Hola. Utilice este Hola acceso de tooremotely de dirección IP virtual. Aunque el portal de hello no crea un [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN, puede crear uno una vez hello máquina virtual creada. En este artículo se muestra hello pasos toocreate un nombre DNS o el FQDN.

## <a name="create-a-fqdn"></a>Creación de un FQDN
En este artículo se supone que ya ha creado una máquina virtual. Si es necesario, puede [crear una máquina virtual en el portal de hello](quick-create-portal.md) o [con Azure PowerShell](quick-create-powershell.md). Una vez que la máquina virtual está en funcionamiento, siga estos pasos:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Ahora puede conectarse remotamente toohello máquina virtual con este nombre DNS como para el protocolo de escritorio remoto (RDP).

## <a name="next-steps"></a>Pasos siguientes
Ahora que la máquina virtual tiene un nombre DNS y una IP pública, puede implementar marcos o servicios de aplicaciones comunes, como IIS, SQL o SharePoint.

En [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) encontrará sugerencias sobre la creación de implementaciones de Azure.

