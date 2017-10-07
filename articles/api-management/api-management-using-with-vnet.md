---
title: "aaaHow toouse administración de API de Azure con redes virtuales"
description: "Obtenga información acerca de cómo toosetup una conexión tooa virtual en administración de API de Azure y acceso web de servicios de red a través de él."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>¿Cómo toouse administración de API de Azure con redes virtuales
Redes virtuales de Azure (Vnet) le permiten tooplace cualquiera de los recursos de Azure en una red de internet no enrutables que controle el acceso a. Estas redes se pueden redes locales de tooyour conectado con varias tecnologías VPN. toolearn más sobre las redes virtuales de Azure de inicio con información de hello aquí: [información general de red Virtual de Azure](../virtual-network/virtual-networks-overview.md).

Administración de API de Azure se puede implementar dentro de la red virtual de hello (VNET), por lo que pueden tener acceso a servicios de back-end en red de Hola. Hola puerta de enlace de API y portal para desarrolladores, puede ser accesibles desde Internet de Hola o solo dentro de la red virtual de Hola a toobe configurado.

> [!NOTE]
> Azure API Management admite redes virtuales clásicas y de Azure Resource Manager.
>
>

## <a name="enable-vpn"></a>Habilitar la conexión de VNET
> [!NOTE]
> Conectividad de red virtual está disponible en hello **Premium** y **Developer** niveles. tooswitch entre las capas de hello, abra el servicio de administración de API en hello portal de Azure y luego hello **escala y precios** ficha. En hello **tarifa** sección, seleccione el nivel Premium o programador de Hola y haga clic en Guardar.
>

conectividad de red virtual tooenable, abra el servicio de administración de API en hello portal de Azure y hello **red Virtual** página.

![Menú Red virtual de API Management][api-management-using-vnet-menu]

Seleccione el tipo de acceso de hello deseado:

* **Externo**: portal de puerta de enlace y el desarrollador de la administración de API de hello son accesibles desde Hola red pública de internet a través de un equilibrador de carga externo. puerta de enlace de Hello puede tener acceso a recursos de red virtual de Hola.

![Emparejamiento público][api-management-vnet-public]

* **Interno**: portal de puerta de enlace y el desarrollador de la administración de API de hello son accesibles únicamente desde dentro de la red virtual de Hola a través de un equilibrador de carga interno. puerta de enlace de Hello puede tener acceso a recursos de red virtual de Hola.

![Emparejamiento privado][api-management-vnet-private]

Ahora verá una lista de todas las regiones donde se aprovisiona el servicio Administración de API. Seleccione una VNET y la subred de cada región. Hola lista se rellena con clásico y el Administrador de recursos de redes virtuales disponibles en las suscripciones de Azure que se configuran en la región de Hola que está configurando.

> [!NOTE]
> **Extremo de servicio** Hola diagrama anterior incluye puerta de enlace o Proxy, Portal para desarrolladores, Portal para desarrolladores, GIT y Hola punto de conexión de administración directa.
> **Extremo de administración** en hello diagrama anterior es el extremo de hello hospedada en la configuración del servicio toomanage de Hola a través del portal de Azure y Powershell.
> Además, tenga en cuenta que, aunque diagrama hello muestra las direcciones IP para sus diversos puntos de conexión, servicio de administración de API **sólo** responde en sus nombres de host configurado.

> [!IMPORTANT]
> Al implementar un tooa de instancia de administración de API de Azure Resource Manager VNET, servicio de hello debe estar en una subred dedicada que no contiene ningún otro recurso excepto instancias de administración de API de Azure. Si se realiza un intento de toodeploy un tooa de instancia de la administración de API de Azure subred VNET el Administrador de recursos que contiene otros recursos, la implementación de Hola se producirá un error.
>
>

![Selección de una VPN][api-management-setup-vpn-select]

Haga clic en **guardar** en la parte superior de Hola de pantalla de bienvenida.

> [!NOTE]
> Hola dirección VIP de la instancia de la administración de API de hello cambiará cada vez que red virtual está habilitada o deshabilitada.  
> Hola dirección VIP también cambia cuando se mueve la administración de API de **externo** demasiado**interno** o viceversa
>


> [!IMPORTANT]
> Si quita API de administración de una red virtual o cambiar Hola uno se implementa en, Hola red virtual usada anteriormente puede permanecer bloqueado para too4 horas. Durante este periodo no se toodelete posibles Hola red virtual o implementar una nueva tooit de recursos.

## <a name="enable-vnet-powershell"></a>Habilitar una conexión de VNET con cmdlets de PowerShell
También puede habilitar la conectividad de red virtual con los cmdlets de PowerShell de Hola

* **Crear un servicio de administración de API dentro de una red virtual**: usar el cmdlet de hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate un servicio de administración de API de Azure dentro de una red virtual.

* **Implementar un servicio de administración de API existente dentro de una red virtual**: usar el cmdlet de hello [AzureRmApiManagementDeployment actualización](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove un servicio de administración de API de Azure existente dentro de una red Virtual.

## <a name="connect-vnet"></a>Conectar tooa web servicio hospedado en una red virtual
Después de que el servicio de administración de API es conectado toohello red virtual, acceso a los servicios back-end en él es similar a obtener acceso a servicios públicos. Solo tiene que escribir la dirección IP local Hola o nombre de host de hello (si un servidor DNS está configurado para la red virtual de hello) del servicio web en hello **dirección URL del servicio Web** campo cuando se crea una nueva API o editar una existente.

![Agregar una API desde VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Problemas comunes de configuración de red
A continuación se muestra una lista de problemas de errores de configuración comunes que pueden producirse al implementar el servicio de API Management en una red virtual.

* **Configuración del servidor DNS personalizado**: Hola servicio de administración de API depende de varios servicios de Azure. Cuando Administración de API se hospeda en una red virtual con un servidor DNS personalizado, necesita los nombres de host hello tooresolve de los servicios de Azure. Siga [estas](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) instrucciones sobre la configuración de DNS personalizado. Consulte la siguiente tabla de puertos de Hola y otros requisitos de red para referencia.

> [!IMPORTANT]
> Se recomienda que, si usa un servidor de DNS personalizado para hello red virtual, configure que **antes de** la implementación de un servicio de administración de API en él. De lo contrario se necesita demasiado Actualizar servicio de administración de API de Hola cada vez que cambie los servidores DNS hello (s) mediante la ejecución de hello [aplicar la operación de configuración de red](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Puertos necesarios para la administración de API**: tráfico entrante y saliente en la subred de hello en el que se implementa la administración de API puede controlarse mediante [grupo de seguridad de red][Network Security Group]. Si alguno de estos puertos no está disponible, es posible que API Management no funcione correctamente y sea inaccesible. Tener bloqueados uno o varios de estos puertos es otro problema común de una configuración incorrecta cuando se usa API Management con una red virtual.

Cuando una instancia de servicio de administración de API se hospeda en una red virtual, se utilizan puertos de hello en hello en la tabla siguiente.

| Puertos de origen/destino | Dirección | Protocolo de transporte | Propósito | Origen/destino | Tipo de acceso |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Entrada |TCP |TooAPI de comunicación de cliente Administración |INTERNET/VIRTUAL_NETWORK |Externo |
| * / 3443 |Entrada |TCP |Punto de conexión de administración para Azure Portal y Powershell |INTERNET/VIRTUAL_NETWORK |Externa e interna |
| * / 80, 443 |Salida |TCP |Dependencia en Azure Storage y Azure Service Bus |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| * / 1433 |Salida |TCP |Dependencia de Azure SQL |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| * / 11000 - 11999 |Salida |TCP |Dependencia de Azure SQL V12 |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| * / 14000 - 14999 |Salida |TCP |Dependencia de Azure SQL V12 |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| * / 5671 |Salida |AMQP |Dependencia de directiva de base de datos central de registro tooEvent y agente de supervisión |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| 6381 - 6383 / 6381 - 6383 |Entrada y salida |UDP |Dependencia de Redis Cache |VIRTUAL_NETWORK/VIRTUAL_NETWORK |Externa e interna |-
| * / 445 |Salida |TCP |Dependencia del recurso compartido de archivos de Azure para Git |VIRTUAL_NETWORK/INTERNET |Externa e interna |
| * / * | Entrada |TCP |Equilibrador de carga de la infraestructura de Azure | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Externa e interna |

* **Funcionalidad SSL**: certificado SSL de tooenable servicio de administración de API de Hola de generación y validación de cadena debe tooocsp.msocsp.com de conectividad de red saliente, mscrl.microsoft.com y crl.microsoft.com. Esta dependencia no es obligatoria, si cualquier certificado que cargue tooAPI administración contiene toohello entidad emisora de certificados raíz de hello cadena completa.

* **Acceso de DNS**: se requiere acceso saliente en el puerto 53 para establecer la comunicación con los servidores DNS. Si existe un servidor DNS personalizado en hello otro extremo de una puerta de enlace VPN, servidor DNS de hello debe ser accesible desde la subred de hello administración de API de hospedaje.

* **Supervisión de estado y las métricas**: extremos supervisión de red saliente conectividad tooAzure, que resolver en hello después dominios: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Configuración de ruta rápida**: una configuración de cliente común es toodefine su propia ruta predeterminada (0.0.0.0/0), que fuerza la salida Internet tráfico tooinstead flujo local. Este flujo de tráfico invariable, interrumpe la conectividad con la administración de API de Azure porque el tráfico saliente Hola está bloqueado de forma local o NAT con el conjunto irreconocible tooan de direcciones que ya no funcionan con varios extremos de Azure. solución Hello es toodefine uno (o más) definido por el usuario rutas ([UDRs][UDRs]) en la subred Hola que contiene Hola administración de API de Azure. Un UDR define las rutas de subred específica que se respetará en lugar de la ruta predeterminada de Hola.
  Si es posible, se recomienda hello toouse siguiente configuración:
 * configuración de ExpressRoute de Hello anuncia 0.0.0.0/0 y de forma predeterminada force túneles todo el tráfico saliente en local.
 * Hola UDR aplica toohello subred que contiene Hola administración de API de Azure define 0.0.0.0/0 con un tipo de próximo salto de Internet.
 Hola efecto combinado de estos pasos es que el nivel de subred de hello UDR tiene precedencia sobre hello ExpressRoute forzado túnel, lo que garantiza el acceso a Internet saliente desde Hola administración de API de Azure.

>[!WARNING]  
>Administración de API de Azure no es compatible con configuraciones de ExpressRoute que **incorrectamente entre-anunciar rutas de hello pública emparejamiento toohello privada emparejamiento ruta de acceso**. Las configuraciones de ExpressRoute con el emparejamiento público configurado recibirán anuncios de ruta de Microsoft para un amplio conjunto de intervalos de direcciones IP de Microsoft Azure. Si estos intervalos de direcciones se publicita entre incorrectamente en la ruta de intercambio de tráfico privado hello, obteniéndose hello es que todos los paquetes de red saliente de la subred de la instancia de administración de API de Azure de hello son red de local del cliente tooa incorrectamente un túnel forzado infraestructura. Este flujo de red interrumpe Azure API Management. problema de Hello solución toothis es toostop rutas de entre anuncios de Hola pública emparejamiento toohello privada emparejamiento ruta de acceso.


## <a name="troubleshooting"></a>Solución de problemas
Al realizar la red de tooyour de cambios, consulte demasiado[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate si Hola servicio de administración de API no ha perdido tooany de acceso del programa Hola a recursos críticos que depende de. estado de conectividad de Hello debe actualizarse cada 15 minutos.

## <a name="limitations"></a>Limitaciones
* Una subred que contenga instancias de API Management no puede contener otros tipos de recursos de Azure.
* subred de Hola y Hola administración de API de servicio debe estar en Hola misma suscripción.
* Una subred que contenga instancias de API Management no se puede mover a otras suscripciones.
* Cuando se usa una red virtual interna, solo estará disponible en una dirección IP interna intervalo Hola estipulados en [RFC 1918](https://tools.ietf.org/html/rfc1918), no se puede proporcionar una dirección IP pública.
* Para las implementaciones de administración de API de varias regiones, con las redes virtuales internas configuradas, los usuarios son responsables de administrar su propias como poseen Hola DNS de equilibrio de carga.


## <a name="related-content"></a>Contenido relacionado
* [Conectar un toobackend de red Virtual con la puerta de enlace Vpn](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Conexión a una red virtual a partir de diferentes modelos de implementación](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Cómo llama a toouse hello tootrace API Inspector de administración de API de Azure](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
