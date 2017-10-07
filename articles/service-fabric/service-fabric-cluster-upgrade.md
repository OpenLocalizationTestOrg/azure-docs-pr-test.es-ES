---
title: "un clúster de Azure Service Fabric aaaUpgrade | Documentos de Microsoft"
description: "Actualizar código de hello Service Fabric o configuración que se ejecuta un clúster de Service Fabric, incluida la configuración de modo de actualización de clúster, actualizar certificados, agregar puertos de la aplicación, realizar revisiones del sistema operativo, y así sucesivamente. ¿Qué puede esperar cuando se realizan las actualizaciones de hello?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Actualización de un clúster de Azure Service Fabric
> [!div class="op_single_selector"]
> * [Clúster de Azure](service-fabric-cluster-upgrade.md)
> * [Clúster independiente](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Para cualquier sistema moderna, diseño de la actualización es tooachieving clave éxito a largo plazo de su producto. Un clúster de Azure Service Fabric es un recurso de su propiedad que está parcialmente administrado por Microsoft. En este artículo se describe lo que se administra automáticamente y lo que puede configurar usted mismo.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Controlar la versión de fabric de Hola que se ejecuta en el clúster
Puede establecer a su tejido automática de clúster tooreceive actualizaciones tal y como se publican por Microsoft o puede seleccionar una versión de fabric compatible que desee su toobe de clúster en.

Para ello, la configuración de clúster de configuración Hola "upgradeMode" en el portal de Hola o con el Administrador de recursos en tiempo de presentación de la creación o posterior en un clúster en vivo 

> [!NOTE]
> Asegúrese de tookeep seguro el clúster que ejecuta una versión compatible de tejido siempre. Como y cuando se anunciar el lanzamiento de Hola de una nueva versión de fabric de servicio, versión anterior de hello está marcado para finalización del soporte después de un mínimo de 60 días a partir de esa fecha. Hola Hola se anuncien nuevas versiones [en el blog del equipo de tejido de servicio de hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nueva versión de Hello es toochoose disponible. 
> 
> 

14 días anteriores toohello expiración de la versión de Hola el clúster se está ejecutando, se genera un evento de estado que coloca el clúster en un estado de mantenimiento de advertencia. clúster de Hello permanece en un estado de advertencia hasta que actualice la versión de fabric compatibles tooa.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Establecer el modo de actualización Hola a través del portal
Puede establecer tooautomatic de clúster de Hola o manual al crear el clúster de Hola.

![Create_Manualmode][Create_Manualmode]

Puede establecer tooautomatic de clúster de Hola o manual cuando está en un clúster activo, con hello administrar la experiencia. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Actualizar tooa nueva versión en un clúster que se establece el modo tooManual a través del portal.
tooupgrade tooa nueva versión, todo lo que necesita toodo es seleccionar versión disponible de hello en lista desplegable de Hola y guardar. actualización de Fabric Hola obtiene iniciada automáticamente. Hello las directivas de mantenimiento de clúster (una combinación del estado de nodo y de hello todas las aplicaciones que se ejecutan en el clúster de Hola de Hola) se respeten la actualización de hello tooduring.

Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. Desplácese hacia abajo en esta tooread documento más acerca de cómo tooset esas directivas personalizada del estado. 

Una vez que se han corregido problemas de Hola que dan como resultado de reversión de hello, necesitará de nuevo, actualización de hello tooinitiate por siguiente Hola mismo pasos como antes.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Establecer el modo de actualización Hola a través de una plantilla de administrador de recursos
Agregar Hola definición de recursos de "upgradeMode" configuración toohello Microsoft.ServiceFabric/clusters y conjunto Hola "clusterCodeVersion" tooone de hello admite versiones de tejido tal y como se muestra a continuación y, a continuación, implementar la plantilla de Hola. los valores válidos de Hola para "upgradeMode" son "Manual" o "Automático"

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>Actualizar tooa nueva versión en un clúster que se establece el modo de tooManual a través de una plantilla de administrador de recursos.
Al clúster de Hola se encuentra en modo Manual, tooupgrade tooa nueva versión, cambiar la versión admitida de tooa clusterCodeVersion"hello" y lo implementará. implementación de Hola de plantilla de hello, aparece de actualización de Fabric Hola obtiene iniciado automáticamente. Hello las directivas de mantenimiento de clúster (una combinación del estado de nodo y de hello todas las aplicaciones que se ejecutan en el clúster de Hola de Hola) se respeten la actualización de hello tooduring.

Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. Desplácese hacia abajo en esta tooread documento más acerca de cómo tooset esas directivas personalizada del estado. 

Una vez que se han corregido problemas de Hola que dan como resultado de reversión de hello, necesitará de nuevo, actualización de hello tooinitiate por siguiente Hola mismo pasos como antes.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Obtención de la lista de todas las versiones disponibles para todos los entornos de una suscripción determinada
Ejecutar Hola el siguiente comando y debe obtener un toothis similar de salida.

"supportExpiryUtc" le indica cuándo expira o ha expirado una determinada versión. Hello versión más reciente no tiene una fecha válida, tiene un valor de "9999-12-31T23:59:59.9999999", que simplemente significa que no se estableció aún fecha de expiración de Hola.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Comportamiento de actualización de fabric al modo de actualización de clúster de hello es automático
Microsoft mantiene el código de fabric de Hola y la configuración que se ejecuta en un clúster de Azure. Llevamos a cabo software toohello de las actualizaciones automáticas de supervisado según sea necesario. Estas actualizaciones podrían ser de código, de configuración o ambas. toomake seguro de que la aplicación no sufre ningún impacto o un impacto mínimo debido a las actualizaciones de toothese, llevamos a cabo las actualizaciones de Hola de hello siguientes fases:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Fase 1: La actualización se realiza con todas las directivas de mantenimiento de clústeres
Durante esta fase, las actualizaciones de hello continuar un dominio de actualización a la vez y, las aplicaciones de Hola que se estaban ejecutando en el clúster de hello siguen toorun sin tiempo de inactividad. Hello las directivas de mantenimiento de clúster (una combinación del estado de nodo y de hello todas las aplicaciones que se ejecutan en el clúster de Hola de Hola) se respeten la actualización de hello tooduring.

Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. A continuación, se envía un correo electrónico toohello propietario de la suscripción de Hola. correo electrónico de Hello contiene Hola siguiente información:

* Notificación de que ha surgido tooroll volver una actualización de clúster.
* Acciones correctoras sugeridas, si hay alguna.
* número de Hola de días (n) hasta que se ejecute la fase 2.

Intentamos hello tooexecute que mismo actualizar varias veces en caso de error en las actualizaciones por razones de infraestructura. Después de hello n días de correo electrónico de hello fecha Hola envió, avancemos tooPhase 2.

Si se cumplen las directivas de mantenimiento de clúster de hello, actualización de Hola se considera correcta y marcarse como completada. Esto puede ocurrir durante la actualización inicial de Hola o cualquiera de las retransmisiones de actualización de hello en esta fase. No hay ningún correo electrónico de confirmación de una ejecución correcta. Se trata de tooavoid enviar se demasiados correos electrónicos, recibir un correo electrónico deben considerarse como un toonormal de excepción. Se espera que la mayoría de hello clúster actualizaciones toosucceed sin afectar a la disponibilidad de las aplicaciones.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Fase 2: La actualización se realiza solo con las directivas de mantenimiento predeterminadas
las directivas de mantenimiento de Hello en esta fase se establecen de forma que número de Hola de las aplicaciones que estaban en buen estado en principio Hola de actualización de hello sigue siendo Hola mismo para hello duración del proceso de actualización de Hola. Como en la fase 1, las actualizaciones de hello fase 2 continuar un dominio de actualización a la vez y, las aplicaciones de Hola que se estaban ejecutando en el clúster de hello siguen toorun sin tiempo de inactividad. las directivas de mantenimiento de clúster de Hello (una combinación del estado de nodo y de hello que todas las aplicaciones que se ejecutan en el clúster de Hola de Hola) son toofor pegada Hola duración de la actualización de Hola.

Si las directivas de mantenimiento de clúster de hello no se cumplen en vigor, se revierte la actualización Hola. A continuación, se envía un correo electrónico toohello propietario de la suscripción de Hola. correo electrónico de Hello contiene Hola siguiente información:

* Notificación de que ha surgido tooroll volver una actualización de clúster.
* Acciones correctoras sugeridas, si hay alguna.
* número de Hola de días (n) hasta que se ejecute la fase 3.

Intentamos hello tooexecute que mismo actualizar varias veces en caso de error en las actualizaciones por razones de infraestructura. Se envía un recordatorio por correo electrónico un par de días antes de llegar a n días. Después de hello n días de correo electrónico de hello fecha Hola envió, avancemos tooPhase 3. Hola mensajes de correo electrónico que se enviarán en la fase 2 deben tener cuidados en serio y acciones correctoras deben tener cuidadas.

Si se cumplen las directivas de mantenimiento de clúster de hello, actualización de Hola se considera correcta y marcarse como completada. Esto puede ocurrir durante la actualización inicial de Hola o cualquiera de las retransmisiones de actualización de hello en esta fase. No hay ningún correo electrónico de confirmación de una ejecución correcta.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Fase 3: La actualización se realiza con directivas de mantenimiento agresivas
Estas directivas de mantenimiento en esta fase específicamente orientadas a la finalización de la actualización de hello en lugar de estado de Hola de aplicaciones de Hola. Muy pocas actualizaciones del clúster terminarán en esta fase. Si el clúster obtiene toothis fase, hay una gran probabilidad de que la aplicación pasa a ser incorrecto o que pierda la disponibilidad.

Toohello similar otros dos fases, las actualizaciones de la fase 3 continúe un dominio de actualización a la vez.

Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. Intentamos hello tooexecute que mismo actualizar varias veces en caso de error en las actualizaciones por razones de infraestructura. Después de eso, se ancla clúster hello, por lo que ya no recibirán soporte técnico o actualizaciones.

Propietario de la suscripción toohello, junto con las acciones correctoras de hello, se envía un correo con esta información. No esperamos que cualquier tooget de clústeres en un estado que ha fallado la fase 3.

Si se cumplen las directivas de mantenimiento de clúster de hello, actualización de Hola se considera correcta y marcarse como completada. Esto puede ocurrir durante la actualización inicial de Hola o cualquiera de las retransmisiones de actualización de hello en esta fase. No hay ningún correo electrónico de confirmación de una ejecución correcta.

## <a name="cluster-configurations-that-you-control"></a>Opciones de configuración de clúster controladas por el usuario
Además actualizar el modo de clúster de toohello capacidad tooset hello, estas son las configuraciones de Hola que puede cambiar en un clúster activo.

### <a name="certificates"></a>Certificados
Puede agregar nuevos o eliminar certificados para el clúster de Hola y de cliente a través del portal de hello fácilmente. Consulte demasiado[este documento para obtener instrucciones detalladas](service-fabric-cluster-security-update-certs-azure.md)

![Captura de pantalla que muestra las huellas digitales de certificado en hello portal de Azure.][CertificateUpgrade]

### <a name="application-ports"></a>Puertos de aplicación
Puede cambiar los puertos de la aplicación cambiando las propiedades de recurso de equilibrador de carga de Hola que están asociados con el tipo de nodo de Hola. Puede usar el portal de hello, o puede usar el Administrador de recursos PowerShell directamente.

Hola tooopen un nuevo puerto en todas las máquinas virtuales en un tipo de nodo siguientes:

1. Agregar un nuevo equilibrador de carga adecuado de toohello de sondeo.
   
    Si ha implementado el clúster mediante el portal de hello, equilibradores de carga de Hola se denominan "LB-nombre de grupo de recursos de hello-NodeTypename", uno para cada tipo de nodo. Puesto que los nombres de equilibrador de carga de hello son únicos solo dentro de un grupo de recursos, es mejor que una búsqueda en un grupo de recursos específico.
   
    ![Captura de pantalla que muestra cómo agregar un sondeo tooa equilibrador de carga de portal de Hola.][AddingProbes]
2. Agregar un nuevo equilibrador de carga de toohello de regla.
   
    Agregar un nuevo toohello de regla mismo equilibrador de carga mediante el uso de sondeo de Hola que creó en el paso anterior de Hola.
   
    ![Agregar un nuevo equilibrador de carga de tooa de regla en el portal de Hola.][AddingLBRules]

### <a name="placement-properties"></a>Propiedades de colocación
Para cada uno de los tipos de nodos de hello, puede agregar propiedades de selección de ubicación personalizada que desee toouse en sus aplicaciones. NodeType es una propiedad predeterminada que se puede usar sin agregarla explícitamente.

> [!NOTE]
> Para obtener más información sobre el uso de Hola de restricciones de posición, propiedades de nodo, y cómo toodefine, consulte toohello sección "Propiedades del nodo y las restricciones de colocación" Hola documento de servicio Administrador de recursos del clúster de tejido en [que describe el clúster ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Métricas de capacidad
Para cada uno de los tipos de nodos de hello, puede agregar las métricas de capacidad personalizado que desea que toouse en su carga de tooreport de aplicaciones. Para obtener detalles sobre el uso de Hola de carga de tooreport de las métricas de capacidad, consulte toohello documentos de servicio Administrador de recursos del clúster de tejido en [que describe su clúster](service-fabric-cluster-resource-manager-cluster-description.md) y [métricas y carga](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Configuración de la actualización de Service Fabric: directivas de mantenimiento
Puede especificar directivas de mantenimiento personalizado para la actualización de Service Fabric. Si ha configurado el clúster tooAutomatic actualizaciones de tejido, estas directivas obtener aplicada toohello fase 1 de las actualizaciones de tejido automática Hola.
Si se han establecido el tejido Manual del clúster de las actualizaciones, a continuación, estas directivas se aplican cada vez que seleccione una nueva versión desencadenar Hola sistema tookick desactivar actualización de fabric de hello en el clúster. Si no reemplaza las directivas de hello, se usan los valores predeterminados de Hola.

Puede especificar las directivas de mantenimiento personalizado de Hola o revisar la configuración actual de hello en la hoja de "actualización de fabric" Hola, mediante la selección Hola actualización configuración avanzada. Revise Hola siguiente sobre cómo. 

![Administración de las directivas de mantenimiento personalizado][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Personalización de la configuración de Service Fabric para el clúster
Consulte demasiado[configuración de tejido de clúster de tejido del servicio](service-fabric-cluster-fabric-settings.md) qué y cómo se puede personalizar.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Revisiones del sistema operativo en las máquinas virtuales que forman el clúster de Hola Hola
Consulte demasiado[revisión orquestación aplicación](service-fabric-patch-orchestration-application.md) que se pueden implementar en las revisiones de tooinstall de clúster de Windows Update de una manera de orquestaciones, mantener los servicios de hello disponibles todo el tiempo Hola. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Actualizaciones de sistema operativo en las máquinas virtuales que forman el clúster de Hola Hola
Si debe actualizar la imagen del sistema operativo hello en las máquinas virtuales del clúster de Hola Hola, se debe hacer una máquina virtual a la vez. Usted es responsable de esta actualización: todavía no se ha automatizado esta tarea.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo toocustomize algunos hello [configuración de tejido de clúster de tejido de servicio](service-fabric-cluster-fabric-settings.md)
* Obtenga información acerca de cómo demasiado[escalar el clúster de entrada y salida](service-fabric-cluster-scale-up-down.md)
* Obtenga información sobre [actualizaciones de aplicaciones](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
