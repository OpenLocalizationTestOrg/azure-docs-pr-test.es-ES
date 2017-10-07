---
title: "aaaHow toouse administración de API de Azure con red virtual interna | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosetup y configurar la administración de API de Azure en red virtual interna."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Uso de Azure API Management con una red virtual interna
Con redes virtuales de Azure (redes virtuales), administración de API puede administrar las API no es accesible en hello Internet. Una serie de tecnologías VPN es conexiones de hello toomake disponibles y administración de API se pueden implementar en dos modos principales dentro de hello red virtual:
* Externo
* Interno

## <a name="overview"></a>Información general
Cuando se implementa la API de administración en un modo de red Virtual interna, solo son visibles dentro de una red Virtual que controlan el acceso a todos los extremos de servicio de hello (puerta de enlace, portal para desarrolladores, portal para desarrolladores, la administración directa y Git). Ninguno de los extremos de servicio de Hola se registran en hello servidor DNS público.

Usar administración de API en modo interno, puede lograr Hola los escenarios siguientes
* Hacer que las API se hospeden de manera segura en su centro de datos privado accesible por terceros que estén fuera de él por medio de conexiones de sitio a sitio o VPN de ExpressRoute.
* Habilitar escenarios de nube híbrida mediante la exposición de las API basadas en la nube y las API locales a través de una puerta de enlace común.
* Administrar las API hospedadas en diversas ubicaciones geográficas mediante un único punto de conexión de puerta de enlace. 

## <a name="enable-vpn"></a>Creación de API Management en una red virtual interna
servicio de administración de API de red Virtual interna de Hola se hospeda detrás de un Balancer(ILB) de carga interno. Hola dirección IP de hello ILB está en hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervalo.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Habilitación de la conexión de red virtual mediante Azure Portal
En primer lugar crear servicio de administración de API de hello, siga los pasos de hello [servicio de administración de API crear][Create API Management service]. A continuación, configurar Administración de API toobe implementado dentro de una red Virtual.

![Menú para configurar API Management en una red virtual interna][api-management-using-internal-vnet-menu]

Después de implementación de Hola se realiza correctamente, debería ver Hola dirección IP Virtual interna de su servicio en el panel de Hola.

![Panel de API Management con red virtual interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Habilitación de una conexión de VNET con cmdlets de PowerShell
También puede habilitar la conectividad de red virtual con los cmdlets de PowerShell de Hola.

* **Crear un servicio de administración de API dentro de una red virtual**: usar el cmdlet de hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate una administración de API de Azure del servicio dentro de una red virtual y configurar tipo de red virtual interna de toouse Hola.

* **Implementar un servicio de administración de API existente dentro de una red virtual**: usar el cmdlet de hello [AzureRmApiManagementDeployment actualización](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove una administración de API de Azure de servicio dentro de una red Virtual y configurar toouse Tipo de red virtual interna.

## <a name="apim-dns-configuration"></a>Configuración de DNS
Cuando se usa API Management en el modo de red virtual externa, DNS está administrado por Azure. Para el modo de red Virtual interna, tener toomanage su propio DNS.

> [!NOTE]
> Servicio de administración de API no escucha toorequests proveniente de direcciones IP. Sólo responde toorequests toohello nombre de host configurado en sus puntos de conexión de servicio (que incluye puerta de enlace, portal para desarrolladores, publisher Portal, punto de conexión de administración directa y git).

### <a name="access-on-default-host-names"></a>Acceso en nombres de host predeterminados:
Cuando se crea un servicio de administración de API en la nube pública de Azure, denominado "contoso" por ejemplo, hello siguientes extremos de servicio se configuran de forma predeterminada.

>   Puerta de enlace o proxy: contoso.azure-api.net

> Portal para desarrolladores y portal para editores: contoso.portal.azure-api.net

> Punto de conexión de administración directa: contoso.management.azure-api.net

>   GIT: contoso.scm.azure-api.net

tooaccess estos puntos de conexión de servicio de administración de API, puede crear una máquina Virtual en una red de subred conectada toohello Virtual en el que se implementa la API de administración. Suponiendo que Hola dirección IP Virtual interna para el servicio 10.0.0.5, puede hacer Hola asignación del archivo de hosts (% SystemDrive%\drivers\etc\hosts) como se indica a continuación:

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

A continuación, puede tener acceso a todos los extremos de servicio de Hola de hello Máquina Virtual que creó. Si utiliza un servidor DNS personalizado en una red virtual, también puede crear registros D de DNS y tener acceso a estos puntos de conexión desde cualquier lugar de la red virtual. 

### <a name="access-on-custom-domain-names"></a>Acceso en nombres de dominio personalizado:
Si no desea hello tooaccess servicio de administración de API con nombres de host de hello predeterminado, puede configurar los nombres de dominio personalizados para todos los extremos de servicio como a continuación

![Configuración de dominio personalizado para API Management][api-management-custom-domain-name]

A continuación, puede crear registros en el servidor DNS tooaccess estos puntos de conexión que solo son accesibles desde dentro de la red Virtual.

## <a name="related-content"></a>Contenido relacionado
* [Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues] (Problemas comunes de configuración de red al configurar API Management en la red virtual)
* [P+F de Virtual Network](../virtual-network/virtual-networks-faq.md)
* [Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx) (Creación de registro D en DNS)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
