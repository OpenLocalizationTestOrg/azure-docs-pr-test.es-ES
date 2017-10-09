---
title: aaaGet iniciado en el DNS de Azure mediante Hola portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un DNS zona y este registro de DNS de Azure. Esto es una guía paso a paso toocreate y administrar la primera zona DNS y el registro mediante Hola portal de Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Introducción a DNS de Azure con hello portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI de Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-getstarted-cli.md)

Este artículo le guiará a través de hello pasos toocreate la primera zona DNS y el registro mediante Hola portal de Azure. También puede realizar estos pasos con Azure PowerShell u Hola CLI de Azure entre plataformas.

Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio. Cada registro DNS del dominio se crea luego en esta zona DNS. Por último, toopublish su DNS de la zona toohello Internet, necesitará servidores de nombres de hello tooconfigure para dominio de Hola. Cada uno de estos pasos se describe en hello pasos.

## <a name="create-a-dns-zone"></a>Creación de una zona DNS

1. Inicie sesión en toohello portal de Azure
2. En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.

    ![Zona DNS](./media/dns-getstarted-portal/openzone650.png)

4. En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:


   | **Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|contoso.com|nombre de Hola de zona DNS de Hola|
   |**Suscripción**|[Su suscripción]|Seleccione una zona DNS de suscripción toocreate hello en.|
   |**Grupos de recursos**|**Crear nuevo:** contosoDNSRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

> [!NOTE]
> grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola. ubicación de la zona DNS Hola siempre es "global" y no se muestra.

## <a name="create-a-dns-record"></a>Creación de un registro de DNS

Hello en el ejemplo siguiente se le guiará por el proceso de Hola de nueva creación de registro "A". Para otros tipos de registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md). 

1. Con hello crea zona DNS, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **contoso.com** de la zona DNS en hello todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **contoso.com** en hello **filtrar por nombre...** cuadro tooeasily tener acceso a la zona de DNS de Hola.

1. En parte superior de Hola de hello **zona DNS** hoja, seleccione **+ grabar conjunto** tooopen hello **Agregar conjunto de registros** hoja.

1. En hello **Agregar conjunto de registros** hoja, escriba Hola después de valores y haga clic en **Aceptar**. En este ejemplo, va a crear un registro A.

   |**Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|www|Nombre del registro de hello|
   |**Tipo**|Una | Tipo de toocreate de registro de DNS, los valores aceptables son A, AAAA, CNAME, MX, NS, SRV, TXT y PTR.  Para más información sobre los tipos de registro, visite [Información general sobre zonas y registros de DNS](dns-zones-records.md)|
   |**TTL**|1|Período de vida de la solicitud DNS de Hola.|
   |**Unidad de TTL**|Horas|Medición de tiempo para el valor de TTL.|
   |**Dirección IP**|ipAddressValue| Este valor es la dirección IP de Hola Hola DNS resuelve.|

## <a name="view-records"></a>Visualización de los registros

En la parte inferior de Hola de hoja de zona DNS de hello, puede ver registros de hello para la zona DNS de Hola. Se deben ver registros DNS y SOA de predeterminado de hello, que se crean en cada zona, además de todos los registros nuevos que haya creado.

![zona](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Actualización de los servidores de nombres

Una vez haya satisface que la zona DNS y los registros se han configurado correctamente, necesita tooconfigure su nombre de dominio toouse servidores de nombres DNS de Azure Hola. Esto permite a otros usuarios Hola Internet toofind los registros DNS.

servidores de nombres de Hello para la zona se proporcionan en hello portal de Azure:

![zona](./media/dns-getstarted-portal/viewzonens500.png)

Estos servidores de nombres deben configurarse con el registrador de nombres de dominio de hello (que adquirió nombre de dominio de hello). El registrador ofrece Hola opción tooset los servidores de nombres de hello para el dominio de Hola. Para obtener más información, consulte [delegar su tooAzure de dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, Hola completa pasos:

1. En el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **MyResourceGroup** grupo de recursos en hello todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **MyResourceGroup** en hello **filtrar por nombre...** grupo de recursos de cuadro tooeasily acceso Hola.
1. Hola **MyResourceGroup** hoja, haga clic en hello **eliminar** botón.
1. Hello portal requiere tootype Hola nombre del tooconfirm de grupo de recursos de Hola que desea que toodelete lo. Haga clic en **eliminar**, tipo *MyResourceGroup* nombre de grupo de recursos de hello, a continuación, haga clic en **eliminar**. Al eliminar un grupo de recursos eliminan todos los recursos en el grupo de recursos de hello, por lo que siempre puede tooconfirm seguro de contenido de Hola de un grupo de recursos antes de eliminarlo. portal de Hello elimina todos los recursos incluidos en el grupo de recursos de hello, a continuación, elimina el grupo de recursos de hello propio. Este proceso tarda varios minutos.


## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de DNS de Azure, consulte [Introducción a DNS de Azure](dns-overview.md).

toolearn más información acerca de la administración de registros DNS en DNS de Azure, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md).

