---
title: una puerta de enlace de aplicaciones de Azure - plantillas aaaCreate | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate una puerta de enlace de la aplicación de Azure mediante el uso de la plantilla de Azure Resource Manager Hola"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Crear una puerta de enlace de la aplicación mediante el uso de la plantilla de Azure Resource Manager Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Plantilla del Administrador de recursos de Azure](application-gateway-create-gateway-arm-template.md)
> * [CLI de Azure](application-gateway-create-gateway-cli.md)

Azure Application Gateway es un equilibrador de carga de nivel 7. Proporciona conmutación por error y enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local. Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más. toofind una lista completa de las características admitidas, visite [información general de la puerta de enlace de aplicaciones](application-gateway-introduction.md)

Este artículo le guiará a través de la descarga y modificando una plantilla existente de Azure Resource Manager de GitHub e implementación de plantilla de Hola de hello CLI de Azure, PowerShell y GitHub.

Si simplemente está implementando la plantilla de Azure Resource Manager Hola directamente desde GitHub sin realizar ningún cambio, omitir toodeploy una plantilla de GitHub.

## <a name="scenario"></a>Escenario

En este escenario:

* Creará una instancia de Application Gateway con firewall de aplicaciones web.
* Creará una red virtual denominada VirtualNetwork1 con un bloque CIDR reservado de 10.0.0.0/16.
* Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.
* Configurar dos direcciones IP de back-end configurado previamente para los servidores web de hello desea tooload equilibrar Hola del tráfico. En este ejemplo de plantilla, hello direcciones IP de back-end son 10.0.1.10 y 10.0.1.11.

> [!NOTE]
> Los valores son parámetros de Hola para esta plantilla. plantilla de hello toocustomize, puede cambiar reglas, el agente de escucha de hello, SSL y otras opciones de archivo de hello azuredeploy.json.

![Escenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Descargar y comprender la plantilla de Azure Resource Manager Hola

Puede descargar Hola existente Azure Resource Manager plantilla toocreate una red virtual y dos subredes desde GitHub, realice los cambios que podría desee y volver a usarla. toodo por lo tanto, use Hola pasos:

1. Navegue demasiado[crear puerta de enlace de aplicaciones con el firewall de aplicación web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Haga clic en **azuredeploy.json** y luego en **RAW**.
1. Guarde la carpeta local de hello archivo tooa en el equipo.
1. Si está familiarizado con las plantillas de Azure Resource Manager, omitir toostep 7.
1. Abrir archivo Hola que ha guardado y mire el contenido de hello en **parámetros** en línea
1. Los parámetros de la plantilla de Azure Resource Manager proporcionan un marcador de posición para los valores que se pueden rellenar durante la implementación.

  | Parámetro | Descripción |
  | --- | --- |
  | **subnetPrefix** |Bloque CIDR de subred de puerta de enlace de aplicación Hola. |
  | **applicationGatewaySize** | Tamaño de puerta de enlace de aplicación Hola.  WAF solo permite tamaños medianos y grandes. |
  | **backendIpaddress1** |Dirección IP del primer servidor de web Hola. |
  | **backendIpaddress2** |Dirección IP del servidor web de la segunda Hola. |
  | **wafEnabled** | Establecer toodetermine si WAFS está habilitado.|
  | **wafMode** | Modo de servidor de aplicaciones web de Hola.  Las opciones disponibles son **prevención** o **detección**.|
  | **wafRuleSetType** | Tipo de conjunto de reglas para WAF.  Actualmente OWASP está Hola solo admite la opción. |
  | **wafRuleSetVersion** |Versión del conjunto de reglas. OWASP CRS 2.2.9 y 3.0 actualmente son opciones de hello compatible. |

1. Compruebe el contenido de hello en **recursos** y observe Hola propiedades siguientes:

   * **type**. Tipo de recurso que se está creando plantilla Hola. En este caso, es de tipo hello `Microsoft.Network/applicationGateways`, que representa una puerta de enlace de la aplicación.
   * **nombre**. Nombre de recurso de Hola. Uso de Hola de aviso de `[parameters('applicationGatewayName')]`, lo que significa que ese nombre Hola se proporciona como entrada por usted o por un archivo de parámetros durante la implementación.
   * **propiedades**. Lista de propiedades para el recurso de Hola. Esta plantilla utiliza la dirección IP pública y red virtual de Hola durante la creación de puerta de enlace de aplicaciones.

   > [!NOTE]
   > Para más información sobre las plantillas, visite el artículo de [referencia de plantillas de Resource Manager](/templates/)

1. Navegue hacia atrás demasiado[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Haga clic en **azuredeploy-paremeters.json** y luego en **Sin formato**.
1. Guarde la carpeta local de hello archivo tooa en el equipo.
1. Abrir archivo de Hola que ha guardado y modificar los valores de hello para los parámetros de Hola. Usar hello después valores toodeploy Hola aplicación puerta de enlace que se describe en nuestro escenario.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Guarde el archivo hello. Puede probar las plantillas JSON de Hola y parámetro mediante herramientas de validación de JSON en línea como [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Implementar la plantilla de Azure Resource Manager hello mediante PowerShell

Si nunca ha usado PowerShell de Azure, visite: [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) y seguir Hola instrucciones toosign en Azure y seleccione su suscripción.

1. Inicio de sesión tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Compruebe las suscripciones de hello para la cuenta de hello.

    ```powershell
    Get-AzureRmSubscription
    ```

    Son tooauthenticate solicitada con sus credenciales.

1. Elija qué su toouse de las suscripciones de Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Si es necesario, cree un grupo de recursos mediante el uso de hello **New-AzureResourceGroup** cmdlet. En el siguiente ejemplo de Hola, crear un grupo de recursos denominado AppgatewayRG en ubicación UU.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Ejecute hello **AzureRmResourceGroupDeployment New** cmdlet toodeploy Hola nueva red virtual mediante el uso de hello anteriores de archivos de plantilla y los parámetros que ha descargado y modificado.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Implementar la plantilla de Azure Resource Manager hello mediante Hola CLI de Azure

plantilla de Azure Resource Manager hello toodeploy ha descargado mediante la CLI de Azure, siga Hola pasos:

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](/cli/azure/install-azure-cli) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.

1. Si es necesario, hello ejecute `az group create` comando toocreate un grupo de recursos, como se muestra en el siguiente fragmento de código de hello. Observe la salida de hello de comando de Hola. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados. Para más información sobre los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (o --name)**. Nombre para el nuevo grupo de recursos Hola. En este escenario, es *appgatewayRG*.
    
    **-l (o --location)**. Región de Azure donde se crea el nuevo grupo de recursos Hola. En este escenario, es *westus*.

1. Ejecute hello `az group deployment create` cmdlet toodeploy Hola nueva red virtual mediante el uso de la plantilla de Hola y los parámetros de archivos que ha descargado y modificado en hello anterior paso. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Implementar plantilla de Azure Resource Manager hello mediante haga clic en implementar

Haga clic en implementar es toouse de otra manera plantillas del Administrador de recursos de Azure. Es una plantilla de toouse fácilmente con hello portal de Azure.

1. Vaya demasiado[crear una puerta de enlace de la aplicación con el servidor de aplicaciones web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Haga clic en **implementar tooAzure**.

    ![Implementar tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Rellene los parámetros de Hola para plantilla de implementación de hello en el portal de Hola y haga clic en **Aceptar**.

    ![parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** y haga clic en **compra**.

1. En la hoja de implementación de saludo personalizado, haga clic en **crear**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Proporciona plantillas del Administrador de tooResource de datos de certificado

Cuando se utiliza SSL con una plantilla, certificado Hola debe toobe proporcionado en una cadena de base64 en lugar de que se va a cargar. cadena base64 tooa .pfx o .cer tooconvert utilice uno de hello siga los comandos. Hello siguientes comandos convierten cadena base64 de hello certificado tooa, que se puede proporcionar toohello plantilla. Hola espera el resultado es una cadena que se puede almacenar en una variable y pegar en la plantilla de Hola.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, realice una de hello pasos:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Pasos siguientes

Si desea que tooconfigure la descarga de SSL, visite: [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).

Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, visite: [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).

Si desea más información acerca de las opciones de equilibrio de carga en general, visite:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

