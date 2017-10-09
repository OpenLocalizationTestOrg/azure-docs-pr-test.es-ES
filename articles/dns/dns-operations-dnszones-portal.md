---
title: 'aaaManage DNS zonas en DNS de Azure: portal de Azure | Documentos de Microsoft'
description: "Puede administrar zonas DNS con hello portal de Azure. Este artículo describe cómo eliminar tooupdate y cómo crear las zonas DNS en el DNS de Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>¿Cómo toomanage zonas de DNS en Hola portal de Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-dnszones-cli.md)

Este artículo muestra cómo toomanage su DNS zonas mediante el uso de hello portal de Azure. También puede administrar las zonas DNS con hello multiplataforma [CLI de Azure](dns-operations-dnszones-cli.md) o hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

1. Inicie sesión en toohello portal de Azure
2. En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:


   | **Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|contoso.com|nombre de Hola de zona DNS de Hola|
   |**Suscripción**|[Su suscripción]|Seleccione una zona DNS de suscripción toocreate hello en.|
   |**Grupos de recursos**|**Crear nuevo:** contosoDNSRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

> [!NOTE]
> grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es "global" y no se muestra.

## <a name="list-dns-zones"></a>Enumeración de zonas DNS

En la consulta Hola portal de Azure, navegue demasiado**más servicios** > **redes** > **zonas DNS**. Cada zona DNS tiene su propio recurso, información como el número de conjuntos de registros y los servidores de nombres están visibles en esta vista. columna de Hello **servidores de nombres** no está en la vista predeterminada de hello, tooadd clic **columnas**, seleccione **servidores de nombres** y haga clic en **realiza**.

![enumeración de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Eliminar una zona DNS

Navegue tooa zona DNS en el portal de Hola. En hello **zona DNS** hoja, haga clic en **elimine la zona**. Son tooconfirm solicitada son que deseaba un zona DNS toodelete Hola. Eliminar una zona DNS, también elimina todos los registros de Hola que figuran en la zona de Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toowork con la zona DNS y registros visitando [Introducción a DNS de Azure mediante el portal de Azure de hello](dns-getstarted-portal.md).
