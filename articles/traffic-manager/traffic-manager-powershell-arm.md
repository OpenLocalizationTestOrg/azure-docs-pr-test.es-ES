---
title: aaaUsing PowerShell toomanage Traffic Manager de Azure | Documentos de Microsoft
description: Uso de PowerShell para Traffic Manager con Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Usar PowerShell toomanage Traffic Manager

Administrador de recursos de Azure es la interfaz de administración preferido de hello de servicios de Azure. Los perfiles de Traffic Manager se pueden administrar mediante las herramientas y las API basadas en Azure Resource Manager.

## <a name="resource-model"></a>Modelo de recursos

El Administrador de tráfico de Azure se configura con una colección de valores denominada perfil del Administrador de tráfico. Este perfil contiene la configuración de DNS, la configuración de enrutamiento de tráfico, punto de conexión de configuración de supervisión, y se enruta una lista de tráfico de toowhich de puntos de conexión de servicio.

Cada perfil de Traffic Manager se representa mediante un recurso de tipo "TrafficManagerProfiles". En el nivel de API de REST de Hola Hola URI para cada perfil es el siguiente:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configuración de Azure PowerShell

En estas instrucciones se usa PowerShell para Microsoft Azure. Hello siguiente artículo se explica cómo tooinstall y configurar Azure PowerShell.

* [¿Cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)

ejemplos de Hello en este artículo se supone que tiene un grupo de recursos existente. Puede crear un grupo de recursos mediante Hola siguiente comando:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager requiere que todos los grupos de recursos cuenten con una ubicación. Esta ubicación se utiliza como valor predeterminado de Hola para recursos creados en ese grupo de recursos. Sin embargo, puesto que los recursos de perfil de Traffic Manager son globales, no regionales, Hola elección de ubicación del grupo de recursos tiene ningún impacto en Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Creación de un perfil del Administrador de tráfico

toocreate un perfil de Traffic Manager, use hello `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Hello en la tabla siguiente describe los parámetros de hello:

| Parámetro | Descripción |
| --- | --- |
| Nombre |nombre de recurso de Hola para hello recursos de perfil de Traffic Manager. Perfiles en hello mismo grupo de recursos debe tener nombres únicos. Este nombre es independiente de nombre DNS de hello usado para las consultas DNS. |
| ResourceGroupName |nombre de Hola de hello grupo contenedor Hola perfil recurso. |
| TrafficRoutingMethod |Especifica Hola enrutamiento de tráfico usa el método toodetermine qué extremo se devuelve como respuesta una consulta DNS. Los valores posibles son "Performance", "Weighted" o "Priority". |
| RelativeDnsName |Especifica la parte hostname de Hola Hola del nombre de DNS proporcionada por este perfil de Traffic Manager. Este valor se combina con el nombre de dominio DNS de hello utilizada Azure Traffic Manager tooform Hola nombre de dominio completo (FQDN) del perfil de Hola. Por ejemplo, el valor de Hola de "contoso" se convierte en 'contoso.trafficmanager.net'. |
| TTL |Especifica Hola DNS Time-to-Live (TTL), en segundos. Este TTL informa a los solucionadores de DNS Local hello y los clientes DNS cuánto toocache las respuestas DNS para este perfil de Traffic Manager. |
| MonitorProtocol |Especifica el estado del extremo de hello protocolo toouse toomonitor. Los valores posibles son "HTTP" y "HTTPS". |
| MonitorPort |Especifica Hola el puerto TCP utilizado toomonitor estado del extremo. |
| MonitorPath |Especifica el nombre de dominio de punto de conexión de hello ruta de acceso relativa toohello utiliza tooprobe mantenimiento del extremo. |

Hola cmdlet crea un perfil de Traffic Manager en Azure y devuelve un tooPowerShell de objeto de perfil correspondiente. En este momento, el perfil de hello no contiene ningún punto de conexión. Para obtener más información acerca de cómo agregar perfil de Traffic Manager tooa de puntos de conexión, vea [agregar extremos de Traffic Manager](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Obtención de un perfil del Administrador de tráfico

tooretrieve un objeto de perfil de Traffic Manager existente, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Este cmdlet devuelve un objeto del perfil del Administrador de tráfico.

## <a name="update-a-traffic-manager-profile"></a>Actualización de un perfil de Traffic Manager

Para modificar perfiles de Traffic Manager, se sigue un proceso de tres pasos:

1. Recuperar Hola perfil mediante `Get-AzureRmTrafficManagerProfile` o usar perfil Hola devuelto por `New-AzureRmTrafficManagerProfile`.
2. Modificar perfil Hola. Puede agregar y quitar puntos de conexión o cambiar los parámetros del perfil o el punto de conexión. Estos cambios son operaciones fuera de línea. Objeto local de hello en la memoria que representa el perfil de hello sólo va a cambiar.
3. Confirmar cambios mediante hello `Set-AzureRmTrafficManagerProfile` cmdlet.

Todas las propiedades de perfil pueden cambiarse excepto RelativeDnsName del perfil de hello. toochange Hola RelativeDnsName, debe eliminar el perfil y un nuevo perfil con un nombre nuevo.

Hola siguiente ejemplo muestra cómo toochange Hola TTL del perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Existen tres tipos de puntos de conexión de Administrador de tráfico:

1. Los **puntos de conexión de Azure** son servicios hospedados en Azure.
2. Los **puntos de conexión externos** son servicios hospedados fuera de Azure.
3. **Anidar extremos** son jerarquías de tooconstruct uso anidado de perfiles de Traffic Manager. Los puntos de conexión anidados hacen posibles configuraciones avanzadas de enrutamiento del tráfico para aplicaciones complejas.

En los tres casos, se pueden agregar puntos de conexión de dos maneras:

1. Mediante el proceso de tres pasos descrito antes. ventaja de Hola de este método es que pueden realizarse varios cambios de punto de conexión en una única actualización.
2. Usando el cmdlet New-AzureRmTrafficManagerEndpoint de Hola. Este cmdlet agrega un perfil de Traffic Manager de punto de conexión tooan existente en una sola operación.

## <a name="adding-azure-endpoints"></a>Adición de puntos de conexión de Azure

Los puntos de conexión de Azure hacen referencia a servicios hospedados en Azure. Se admiten dos tipos de puntos de conexión de Azure:

1. Aplicaciones web de Azure 
2. Recursos de Azure PublicIpAddress (que pueden ser tooa adjunto de equilibrador de carga o una máquina virtual de NIC). Hola PublicIpAddress debe tener un nombre DNS asignado toobe utilizado en el Administrador de tráfico.

En cada caso:

* servicio de Hola se especifica mediante hello 'elemento targetResourceId' parámetro de `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.
* Hello 'Target' y 'EndpointLocation' están implícito en el elemento TargetResourceId Hola.
* Especificar hello 'Weight' es opcional. Pesos solo se usan si el perfil de hello es el método de enrutamiento del tráfico de toouse configurado hello 'Weighted'. En caso contrario, se pasan por alto. Si se especifica, el valor de hello debe ser un número entre 1 y 1000. valor predeterminado de Hello es '1'.
* Hola especificando 'Priority' es opcional. Las prioridades se usan solo si el perfil de hello es el método de enrutamiento del tráfico de toouse configurado hello 'Priority'. En caso contrario, se pasan por alto. Los valores válidos son de 1 too1000 con valores más bajos que indica una prioridad más alta. Si se especifica para un punto de conexión, se debe especificar para todos los puntos de conexión. Si se omite, los valores predeterminados a partir de '1' se aplican en orden de Hola que se enumeran los puntos de conexión de Hola.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Ejemplo 1: Incorporación de puntos de conexión de aplicación web mediante `Add-AzureRmTrafficManagerEndpointConfig`

En este ejemplo, se crea un perfil de Traffic Manager y agregue dos extremos de aplicación Web con hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Ejemplo 2: Incorporación de un punto de conexión de publicIpAddress mediante `New-AzureRmTrafficManagerEndpoint`

En este ejemplo, un recurso de dirección IP público se agrega toohello perfil de Traffic Manager. la dirección IP pública Hola debe tener un nombre DNS configurado y puede estar enlazado cualquier NIC de un equilibrador de carga de la máquina virtual o tooa toohello.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Adición de puntos de conexión externos

El tráfico Manager usa extremos externos toodirect tráfico tooservices hospedado fuera de Azure. Al igual que en el caso de los puntos de conexión de Azure, los puntos de conexión externos se pueden agregar mediante `Add-AzureRmTrafficManagerEndpointConfig` seguido de `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.

Cuando se especifican puntos de conexión externos:

* nombre de dominio de punto de conexión de Hello debe especificarse con el parámetro de 'Target' hello
* Si se utiliza el método de enrutamiento de tráfico 'Rendimiento' hello, hello 'EndpointLocation' es necesario. De lo contrario, es opcional. Hola valor debe ser un [nombre de la región de Azure válida](https://azure.microsoft.com/regions/).
* Hola 'Peso' y 'Priority' es opcional.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Ejemplo 1: Incorporación de puntos de conexión externos mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`

En este ejemplo, se crea un perfil de Traffic Manager, agregar dos extremos externos y confirmar los cambios de Hola.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Ejemplo 2: Incorporación de puntos de conexión externos mediante `New-AzureRmTrafficManagerEndpoint`

En este ejemplo, se agrega un perfil existente de tooan de extremo externo. perfil de Hola se especifica utilizando nombres de grupos de recursos y perfil Hola.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Adición de puntos de conexión "Anidados"

Cada perfil del Administrador de tráfico especifica un único método de enrutamiento del tráfico. Sin embargo, hay escenarios que requieren el enrutamiento del tráfico más sofisticadas de hello enrutamiento proporcionada por un solo perfil de Traffic Manager. Puede anidar ventajas de hello toocombine de los perfiles de Traffic Manager de más de un método de enrutamiento de tráfico. Perfiles anidados permiten toooverride Hola predeterminado Traffic Manager comportamiento toosupport mayor y las implementaciones de aplicaciones más complejas. Para ejemplos más detallados, consulte [Perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md).

Extremos anidados se configuran en el perfil de hello primaria, con un tipo de punto de conexión concreto, 'NestedEndpoints'. Cuando se especifican puntos de conexión anidados:

* punto de conexión de Hello debe especificarse con el parámetro de 'elemento targetResourceId' hello
* Si se utiliza el método de enrutamiento de tráfico 'Rendimiento' hello, hello 'EndpointLocation' es necesario. De lo contrario, es opcional. Hola valor debe ser un [nombre de la región de Azure válida](http://azure.microsoft.com/regions/).
* Hola 'Peso' y 'Priority' es opcional, como para los extremos de Azure.
* parámetro de 'MinChildEndpoints' Hello es opcional. valor predeterminado de Hello es '1'. Si número Hola de puntos de conexión disponibles cae por debajo del umbral, perfil principal de hello considera perfil secundario de hello 'Degradado' y desvía tráfico toohello otros extremos en el perfil de hello primario.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Ejemplo 1: Incorporación de puntos de conexión anidados mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`

En este ejemplo, se crear primarias y secundarias de Traffic Manager nuevos perfiles, agrega a secundario hello como elemento primario toohello anidadas de punto de conexión y confirmar los cambios de Hola.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Por razones de brevedad en este ejemplo, no se ha agregado los otros extremos toohello secundarias o primarias perfiles.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Ejemplo 2: Incorporación de puntos de conexión anidados mediante `New-AzureRmTrafficManagerEndpoint`

En este ejemplo, agregamos un perfil secundario existente como un perfil de primario de extremo anidada tooan existente. perfil de Hola se especifica utilizando nombres de grupos de recursos y perfil Hola.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Actualización de un punto de conexión de Administrador de tráfico

Hay dos tooupdate formas un punto de conexión de administrador de tráfico existente:

1. Obtener perfil de Traffic Manager de hello mediante `Get-AzureRmTrafficManagerProfile`, actualizar las propiedades de punto de conexión de hello en el perfil de Hola y confirmar los cambios de hello mediante `Set-AzureRmTrafficManagerProfile`. Este método tiene la ventaja de Hola de ser tooupdate capaz de más de un punto de conexión en una sola operación.
2. Obtener el punto de conexión de administrador de tráfico de hello mediante `Get-AzureRmTrafficManagerEndpoint`, actualizar las propiedades de punto de conexión de Hola y confirmar los cambios de hello mediante `Set-AzureRmTrafficManagerEndpoint`. Este método es más sencillo, ya que no requieren la indización en la matriz de puntos de conexión de hello en el perfil de Hola.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Ejemplo 1: Actualización de puntos de conexión mediante `Get-AzureRmTrafficManagerProfile` y `Set-AzureRmTrafficManagerProfile`

En este ejemplo, se modifique la prioridad de hello en dos puntos de conexión dentro de un perfil existente.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Ejemplo 2: Actualización de un punto de conexión mediante `Get-AzureRmTrafficManagerEndpoint` y `Set-AzureRmTrafficManagerEndpoint`

En este ejemplo, se modifique el peso de Hola de un solo punto de conexión en un perfil existente.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Habilitación y deshabilitación de puntos de conexión y perfiles

Traffic Manager permite extremos individuales toobe habilitados y deshabilitados, además de permitir la habilitación y deshabilitación de perfiles completos.
Estos cambios pueden realizarse por los recursos de extremo o un perfil de hello obtener/actualizar/configuración. toostreamline estas operaciones comunes, también se admiten a través de los cmdlets dedicados.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Ejemplo 1: Habilitación y deshabilitación de un perfil de Administrador de tráfico

tooenable un perfil de Traffic Manager, use `Enable-AzureRmTrafficManagerProfile`. perfil de Hello puede especificarse mediante un objeto de perfil. Hello objeto de perfil se puede pasar a través de la canalización de Hola o mediante el uso de hello '-TrafficManagerProfile' parámetro. En este ejemplo, especificamos perfil Hola por nombre de grupo de recursos y perfil Hola.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable un perfil de Traffic Manager:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Hola Disable-AzureRmTrafficManagerProfile cmdlet pide confirmación. Este mensaje se puede suprimir con hello '-Force' parámetro.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Ejemplo 2: Habilitación y deshabilitación de un punto de conexión de Administrador de tráfico

usar un punto de conexión de administrador de tráfico, tooenable `Enable-AzureRmTrafficManagerEndpoint`. Hay el punto de conexión de dos maneras toospecify Hola

1. Mediante un objeto TrafficManagerEndpoint pasado a través de la canalización de Hola o con hello '-TrafficManagerEndpoint' parámetro
2. Uso de nombre de punto de conexión de hello, tipo de extremo, nombre del perfil y el nombre del grupo de recursos:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Toodisable del mismo modo, un punto de conexión de administrador de tráfico:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Al igual que con `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet pide confirmación. Este mensaje se puede suprimir con hello '-Force' parámetro.

## <a name="delete-a-traffic-manager-endpoint"></a>Eliminación de un punto de conexión de Administrador de tráfico

tooremove extremos individuales, utilice hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Este cmdlet solicita confirmación. Este mensaje se puede suprimir con hello '-Force' parámetro.

## <a name="delete-a-traffic-manager-profile"></a>Eliminación de un perfil del Administrador de tráfico

toodelete un perfil de Traffic Manager, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, especificar los nombres de grupo de recursos y perfil de hello:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Este cmdlet solicita confirmación. Este mensaje se puede suprimir con hello '-Force' parámetro.

Hola perfil toobe elimina también puede especificarse mediante un objeto de perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Se puede canalizar igualmente esta secuencia:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Pasos siguientes

[Supervisión del Administrador de tráfico](traffic-manager-monitoring.md)

[Consideraciones de rendimiento sobre el Administrador de tráfico](traffic-manager-performance-considerations.md)
