---
title: control de acceso de soporte de firewall de base de datos de Cosmos aaaAzure & IP | Documentos de Microsoft
description: "Obtenga información acerca de cómo son compatibles con directivas de control de acceso IP de toouse de firewall en cuentas de base de datos de la base de datos de Azure Cosmos."
keywords: Control de acceso IP, compatibilidad con el firewall
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Compatibilidad con un firewall de Azure Cosmos DB
toosecure los datos almacenados en una cuenta de base de datos de la base de datos de Azure Cosmos, Azure Cosmos DB proporcionaba compatibilidad para un secreto según [modelo de autorización](https://msdn.microsoft.com/library/azure/dn783368.aspx) que utiliza un código de autenticación de mensaje seguro basado en Hash (HMAC). Ahora, además toohello secreto basado en modelo de autorización, base de datos de Azure Cosmos admite directiva controlada por los controles de acceso basado en IP para la compatibilidad con firewall de entrada. Este modelo es muy similar reglas de firewall toohello de un sistema de base de datos tradicional y proporciona un nivel adicional de seguridad toohello cuenta de base de datos de la base de datos de Azure Cosmos. Con este modelo, ahora puede configurar una toobe de cuenta de base de datos de base de datos de Azure Cosmos accesible sólo desde un conjunto de equipos aprobado o servicios en la nube. Tener acceso a recursos de base de datos de Cosmos tooAzure de estos conjuntos de aprobados de servicios y máquinas seguirán necesitando Hola llamador toopresent un token de autorización válido.

## <a name="ip-access-control-overview"></a>Introducción al control de acceso IP
De forma predeterminada, una cuenta de base de datos de la base de datos de Azure Cosmos es accesible desde internet público como solicitud Hola está acompañado por un token de autorización válido. control de acceso basado en directiva de tooconfigure IP, el usuario de hello debe proporcionar conjunto Hola de direcciones IP o intervalos de direcciones IP de CIDR formulario toobe incluidos como lista de direcciones IP de cliente para una cuenta de base de datos determinada de elementos permitido de Hola. Una vez que se aplique esta configuración, se bloquearán todas las solicitudes procedentes de máquinas de fuera de esta lista permitida por servidor hello.  conexión de Hello flujo de proceso de control de acceso basado en IP Hola se describe en hello siguiente diagrama.

![Diagrama que muestra el proceso de conexión de hello para el control de acceso basado en IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Conexiones desde servicios en la nube
En Azure, los servicios en la nube son una forma muy común de hospedar lógica de servicio de nivel intermedio mediante Azure Cosmos DB. tooenable acceso tooan cuenta de base de datos de base de datos de Azure Cosmos desde un servicio de nube, dirección IP pública de hello del servicio de nube de hello debe ser agregado toohello permitida la lista de direcciones IP asociadas a su cuenta de base de datos de la base de datos de Azure Cosmos por [configuración Hola directiva de control de acceso IP](#configure-ip-policy).  Esto garantiza que todas las instancias de rol de servicios en la nube tienen acceso tooyour cuenta de base de datos de la base de datos de Azure Cosmos. Puede recuperar direcciones IP para los servicios de nube en hello portal de Azure, como se muestra en la siguiente captura de pantalla de Hola.

![Captura de pantalla muestra la dirección IP pública de Hola para un servicio de nube que se muestran en hello portal de Azure](./media/firewall-support/public-ip-addresses.png)

Al escalar horizontalmente su servicio de nube mediante la adición de las instancias de rol adicionales, esas nuevas instancias tendrán automáticamente cuenta de base de datos de base de datos de Azure Cosmos acceso toohello ya que forman parte del programa Hola mismo servicio en la nube.

## <a name="connections-from-virtual-machines"></a>Conexiones desde máquinas virtuales
[Máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/) o [conjuntos de escalas de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) también puede ser usado toohost de servicios de nivel intermedio con la base de datos de Azure Cosmos.  Hola tooconfigure acceso de tooallow de cuenta de base de datos de base de datos de Azure Cosmos desde máquinas virtuales, las direcciones IP públicas de máquina virtual o conjunto de escalas de máquina virtual debe estar configurado como uno de hello permitida direcciones IP para la cuenta de base de datos de la base de datos de Azure Cosmos por [configurar Directiva de control de acceso IP de hello](#configure-ip-policy). Puede recuperar direcciones IP para máquinas virtuales en hello portal de Azure, como se muestra en la siguiente captura de pantalla de Hola.

![Captura de pantalla muestra una dirección IP pública de una máquina virtual que muestra en hello portal de Azure](./media/firewall-support/public-ip-addresses-dns.png)

Cuando se agrega el grupo de toohello de instancias de máquina virtual adicional, se proporcionan automáticamente cuenta de base de datos de base de datos de Azure Cosmos acceso tooyour.

## <a name="connections-from-hello-internet"></a>Hola de conexiones de internet
Cuando el acceso a una base de datos de Azure Cosmos la base de datos cuenta desde un equipo en hello internet, hello dirección IP del cliente o intervalo de direcciones IP de la máquina de hello debe ser agregado toohello lista de direcciones IP para la cuenta de base de datos de la base de datos de Azure Cosmos Hola de elementos permitido. 

## <a id="configure-ip-policy"></a>Configurar la directiva de control de acceso IP de Hola
Directiva de control de acceso de Hello IP se puede establecer en hello portal de Azure, o mediante programación a través [CLI de Azure](cli-samples.md), [Azure Powershell](powershell-samples.md), o hello [API de REST](/rest/api/documentdb/) actualizando hello `ipRangeFilter` propiedad. Los intervalos o direcciones IP deben ir separados por una coma y no deben contener espacios. Ejemplo: "13.91.6.132,13.91.6.1/24". Al actualizar la cuenta de base de datos a través de estos métodos, ser toopopulate seguro todos Hola propiedades tooprevent restablecer la configuración de toodefault.

> [!NOTE]
> Al habilitar una directiva de control de acceso IP para la cuenta de base de datos de la base de datos de Azure Cosmos, todos los acceso tooyour cuenta de base de datos de base de datos de Azure Cosmos de máquinas de fuera Hola configurado permite lista de intervalos de direcciones IP están bloqueados. En virtud de este modelo, exploración de operación de plano de datos de Hola desde el portal de hello también será bloqueado tooensure Hola integridad de control de acceso.

desarrollo de toosimplify, Hola portal de Azure le ayuda a identificar y agregar IP de Hola de su toohello de equipo cliente, lista de permitidos para que las aplicaciones que se ejecutan en el equipo pueden tener acceso a la cuenta de base de datos de Azure Cosmos Hola. Tenga en cuenta que se detecta la dirección IP de cliente de hello aquí tal como se muestra en el portal de Hola. Es posible dirección IP del cliente Hola de su equipo, pero también podría ser Hola de dirección IP de la puerta de enlace de red. No olvide tooremove con anterioridad tooproduction continuo.

Directiva de control de acceso IP de tooset Hola Hola portal de Azure, navegue hoja de cuenta de base de datos de Azure Cosmos toohello, haga clic en **Firewall** en el menú de navegación de hello, a continuación, haga clic en **ON** 

![Captura de pantalla muestra cómo tooopen Hola hoja de Firewall en hello portal de Azure](./media/firewall-support/azure-portal-firewall.png)

En el nuevo panel de hello, especifique si hello portal de Azure puede tener acceso a la cuenta de hello y otras direcciones e intervalos según corresponda, a continuación, haga clic en **guardar**.  

> [!NOTE]
> Cuando se habilita una directiva de control de acceso IP, necesitará la dirección IP de Hola de tooadd para hello acceso toomaintain de portal de Azure. direcciones IP de portal Hola son:
> |Region|Dirección IP|
> |------|----------|
> |Todas las regiones, a excepción de las especificadas a continuación| 104.42.195.92|
> |Alemania|51.4.229.218|
> |China|139.217.8.252|
> |Gobierno de EE. UU.: Arizona|52.244.48.71|
>

![Captura de pantalla muestra cómo tooconfigure configuración del firewall en hello portal de Azure](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Solución de problemas de directiva de control de acceso IP de Hola
### <a name="portal-operations"></a>Operaciones del portal
Al habilitar una directiva de control de acceso IP para la cuenta de base de datos de la base de datos de Azure Cosmos, todos los acceso tooyour cuenta de base de datos de base de datos de Azure Cosmos de máquinas de fuera Hola configurado permite lista de intervalos de direcciones IP están bloqueados. Por lo tanto, si desea que las operaciones del plano de datos del portal de tooenable como navegar por las colecciones y consultar documentos, debe tooexplicitly permitir acceso de portal de Azure con hello **Firewall** hoja en el portal de Hola. 

![Captura de pantalla muestra cómo tooenable acceso toohello portal de Azure](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK y API de Rest
Por motivos de seguridad, acceso a través de SDK o API de REST de máquinas no en la lista de elementos permitidos de hello devolverá un genérico respuesta de no encuentra 404 con ningún detalle adicional. Compruebe que IP Hola permitido lista configurada para la configuración de directiva correcta de base de datos de Azure Cosmos base de datos cuenta tooensure hello es aplicado tooyour cuenta de base de datos de la base de datos de Azure Cosmos.

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre las sugerencias de rendimiento relacionadas con la red, consulte [Sugerencias de rendimiento](performance-tips.md).

