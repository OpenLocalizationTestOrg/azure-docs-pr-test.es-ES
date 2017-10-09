---
title: "aaaSetting de un clúster de Service Fabric mediante Visual Studio | Documentos de Microsoft"
description: "Describe cómo tooset seguridad un tejido de servicio de clúster mediante el uso de la plantilla de Azure Resource Manager creada por un proyecto del grupo de recursos de Azure en Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Configuración de un clúster de Service Fabric mediante Visual Studio
Este artículo describe cómo agrupar tooset seguridad un tejido de servicio de Azure mediante Visual Studio y una plantilla de Azure Resource Manager. Se usará una plantilla de hello Azure en Visual Studio recursos grupo proyecto toocreate. Una vez creada la plantilla de hello, se puede implementar directamente tooAzure desde Visual Studio. También puede utilizarse desde un script o como parte de la instalación de integración continua (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Creación de una plantilla de clúster de Service Fabric con un proyecto de grupo de recursos de Azure
tooget iniciado, abra Visual Studio y cree un proyecto del grupo de recursos de Azure (está disponible en hello **nube** carpeta):

![Cuadro de diálogo Nuevo proyecto con el proyecto del Grupo de recursos de Azure seleccionado][1]

Puede crear una nueva solución de Visual Studio para este proyecto o agregar tooan de solución existente.

> [!NOTE]
> Si no ve el proyecto del grupo de recursos de Azure hello en el nodo de la nube de hello, no tiene instalado el SDK de Azure de Hola. Inicie el instalador de plataforma Web ([instalarla ahora](http://www.microsoft.com/web/downloads/platform.aspx) si aún no lo tiene) y, a continuación, busque "Azure SDK para. NET" y la versión de Hola de instalación que sea compatible con su versión de Visual Studio.
> 
> 

Una vez alcanzado el botón Aceptar hello, Visual Studio le solicitará que plantilla de administrador de recursos de hello tooselect desea toocreate:

![Seleccione el cuadro de diálogo Plantilla de Azure con la plantilla del clúster de Service Fabric seleccionado][2]

Vuelva a Seleccionar plantilla de servicio de Cluster Server tejido hello y botón Hola posicionamiento Aceptar. Ahora ha creado proyectos de Hola y plantilla de administrador de recursos de Hola.

## <a name="prepare-hello-template-for-deployment"></a>Preparar la plantilla de hello para la implementación
Antes de clúster de hello toocreate implementado plantilla hello, debe proporcionar valores para parámetros de plantilla de hello necesario. Estos valores de parámetro se leen de hello `ServiceFabricCluster.parameters.json` archivo, que se encuentra en hello `Templates` carpeta de proyecto del grupo de recursos de Hola. Abra el archivo hello y proporcione Hola siguientes valores:

| Nombre de parámetro | Descripción |
| --- | --- |
| adminUserName |nombre de Hola de cuenta de administrador de Hola para las máquinas de Service Fabric (nodos). |
| certificateThumbprint |Hola huella digital del certificado de Hola que protege el clúster de Hola. |
| sourceVaultResourceId |Hola *Id. de recurso* de almacén de claves de Hola donde se almacena el certificado de Hola que protege el clúster de Hola. |
| certificateUrlValue |dirección URL de Hola de certificado de seguridad de clúster de Hola. |

plantilla de administrador de recursos de Visual Studio Service Fabric Hola crea un clúster seguro que está protegido por un certificado. Este certificado se identifica mediante Hola última tres parámetros de plantilla (`certificateThumbprint`, `sourceVaultValue`, y `certificateUrlValue`), y debe existir en un **el almacén de claves de Azure**. Para obtener más información sobre cómo toocreate Hola certificado de seguridad de clúster, consulte [escenarios de seguridad de clúster de Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artículo.

## <a name="optional-change-hello-cluster-name"></a>Opcional: cambie el nombre del clúster de Hola
Cada clúster de Service Fabric tiene un nombre. Cuando se crea un clúster de tejido de Azure, el nombre del clúster determina (junto con la región de Azure Hola) nombre de sistema de nombres de dominio (DNS) de hello para el clúster de Hola. Por ejemplo, si asigna el nombre del clúster `myBigCluster`y Hola ubicación (región de Azure) del grupo de recursos de Hola que hospedará el nuevo clúster de Hola es este de EE., nombre DNS de hello del clúster de hello será `myBigCluster.eastus.cloudapp.azure.com`.

De forma predeterminada el nombre del clúster de Hola se genera automáticamente y realiza único adjuntando un prefijo de sufijo aleatorio tooa "clúster". Resulta muy fácil toouse plantilla de hello como parte de un **integración continua** sistema (CI). Si desea que toouse un nombre específico para el clúster, uno que sea significativo tooyou, establezca el valor de Hola de hello `clusterName` variable en el archivo de plantilla del Administrador de recursos de hello (`ServiceFabricCluster.json`) nombre tooyour elegido. Es variable primera Hola definida en ese archivo.

## <a name="optional-add-public-application-ports"></a>Opcional: agregar puertos de aplicación pública
También puede toochange puertos de la aplicación pública de hello para el clúster de hello antes de implementarlo. De forma predeterminada, la plantilla de hello abre dos puertos TCP públicos (80 y 8081). Si necesita más de las aplicaciones, modifique la definición de equilibrador de carga de Azure de hello en plantilla Hola. definición de Hola se almacena en el archivo de plantilla principal hello (`ServiceFabricCluster.json`). Abra el archivo y busque `loadBalancedAppPort`. Cada puerto se asocia con tres artefactos:

1. Una variable de plantilla que define el valor de puerto TCP de hello para el puerto de hello:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *sondeo* que define cómo con frecuencia y durante cuánto tiempo Hola equilibrador de carga de Azure intenta toouse un nodo de Service Fabric específico antes de desistir sobre tooanother uno. Hola sondeos forman parte de hello recurso de equilibrador de carga. Aquí está la definición de sondeo de Hola para hello primera aplicación de puerto:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *regla de equilibrio de carga* que enlaza el puerto de Hola y sondeo hello, que habilita el equilibrio de carga entre un conjunto de nodos de clúster de Service Fabric:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Si las aplicaciones de Hola que planea toodeploy toohello clúster necesitan más puertos, puede agregarlos mediante sondeo adicional creando y definiciones de la regla de equilibrio de carga. Para obtener más información acerca de cómo toowork con el equilibrador de carga de Azure a través de plantillas de administrador de recursos, consulte [empezar a crear un equilibrador de carga interno mediante una plantilla de](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Implementar la plantilla de hello mediante Visual Studio
Después de haber guardado Hola a todos los valores de parámetro necesario en el`ServiceFabricCluster.param.dev.json` archivo, está listo toodeploy Hola plantilla y crear el clúster de Service Fabric. Haga clic en proyecto de grupo de recursos de hello en el Explorador de soluciones de Visual Studio y elija **implementar | Implementación nueva...** . Si es necesario, Visual Studio mostrará hello **implementar tooResource grupo** cuadro de diálogo, que le pide que tooauthenticate tooAzure:

![Implementar el cuadro de diálogo de grupo de tooResource][3]

cuadro de diálogo de Hello le permite elegir un grupo de recursos de administrador de recursos existente para el clúster de Hola y proporciona Hola toocreate opción uno nuevo. Normalmente tiene sentido toouse un grupo de recursos independiente para un clúster de Service Fabric.

Una vez alcanzado el botón de hello implementar, Visual Studio le pedirá que valores de parámetro de plantilla tooconfirm Hola. Hola posicionamiento **guardar** botón. Un parámetro no tiene un valor persistente: contraseña de la cuenta administrativa de Hola para clúster Hola. Deberá tooprovide un valor de contraseña cuando Visual Studio le pide uno.

> [!NOTE]
> A partir de Azure SDK 2.9, Visual Studio admite contraseñas de lectura de **Azure Key Vault** durante la implementación. En el cuadro de diálogo de parámetros de plantilla de hello, observe que hello `adminPassword` cuadro de texto del parámetro tiene un pequeño icono de "clave" en hello derecho. Este icono permite tooselect un secreto de almacén de claves existente como contraseña administrativa de hello para el clúster de Hola. Siempre que se toofirst seguro de habilitar el acceso de administrador de recursos de Azure para la implementación de plantilla en hello avanzada de las directivas de acceso de su almacén de claves. 
> 
> 

Puede supervisar el progreso de Hola Hola proceso de implementación en la ventana de salida de hello Visual Studio. Cuando se haya completado la implementación de la plantilla de hello, el nuevo clúster está toouse listo!

> [!NOTE]
> Si PowerShell nunca ha usado tooadminister Azure de la máquina de Hola que está usando ahora, deberá toodo un poco mantenimiento.
> 
> 1. Habilitar PowerShell scripting ejecutando hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) comando. Para los equipos de desarrollo es normalmente aceptable una directiva "sin restricciones".
> 2. Decidir si tooallow de recopilación de datos de diagnóstico de comandos de PowerShell de Azure y ejecute [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) o [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) según sea necesario. Esto evita solicitudes innecesarias durante la implementación de la plantilla.
> 
> 

Si hay algún error, vaya toohello [portal de Azure](https://portal.azure.com/) y grupo de recursos de hello abierto que ha implementado en. Haga clic en **toda la configuración de**, a continuación, haga clic en **implementaciones** en la hoja de configuración de Hola. Una implementación de grupo de recursos con errores deja allí una información de diagnóstico detallada.

> [!NOTE]
> Clústeres de Service Fabric requieren un cierto número de nodos toobe la disponibilidad de toomaintain y conservan el estado - tooas que se hace referencia "mantenga el quórum". Por lo tanto, no es seguro tooshut hacia abajo todas las máquinas de hello en clúster de Hola a menos que primero ha llevado a cabo una [una copia de seguridad completa del estado del](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información acerca de cómo configurar el clúster de Service Fabric mediante Hola portal de Azure](service-fabric-cluster-creation-via-portal.md)
* [Obtenga información acerca de cómo toomanage e implementar aplicaciones de Service Fabric mediante Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
