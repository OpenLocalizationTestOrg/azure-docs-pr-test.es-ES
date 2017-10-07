---
title: "aplicación de contenedor de aaaEnable access tooAzure DC/OS | Documentos de Microsoft"
description: "¿Cómo tooenable público tener acceso a contenedores de tooDC/OS en el servicio de contenedor de Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Habilitar la aplicación de servicio de contenedor de Azure de acceso público tooan
Cualquier contenedor de DC/OS Hola ACS [grupo de agente pública](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) es toohello expuesto automáticamente internet. De forma predeterminada, los puertos **80**, **443** y **8080** están abiertos y se puede tener acceso a cualquier contenedor (público) que escucha en esos puertos. Este artículo muestra cómo tooopen más puertos para las aplicaciones de servicio de contenedor de Azure.

## <a name="open-a-port-portal"></a>Abrir un puerto (portal)
En primer lugar, necesitamos tooopen puerto de Hola que deseamos.

1. Inicie sesión en el portal de toohello.
2. Encontrar el grupo de recursos Hola que implementó Hola servicio de contenedor de Azure para.
3. Seleccione el equilibrador de carga del agente de hello (que se denomina similar demasiado**XXXX-XXXX-agent-lb**).
   
    ![Equilibrador de carga de Azure Container Service](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Haga clic en **Sondeos** y luego en **Agregar**.
   
    ![Sondeos del equilibrador de carga de Azure Container Service](./media/container-service-enable-public-access/add-probe.png)
5. Rellene el formulario de sondeo de Hola y haga clic en **Aceptar**.
   
   | Campo | Description |
   | --- | --- |
   | Nombre |Un nombre descriptivo del sondeo de Hola. |
   | Port |puerto de Hola de hello contenedor tootest. |
   | Ruta de acceso |(Cuando está en modo de HTTP) Hola tooprobe de ruta de acceso relativa de sitio Web. HTTPS no es compatible. |
   | Intervalo |cantidad de Hola de tiempo entre el sondeo intenta, en segundos. |
   | Umbral incorrecto |Número de sondeo consecutivos intentos antes de considerar que el contenedor de hello incorrecto. |
6. En Propiedades de Hola Hola agente del equilibrador de carga, haga clic en **reglas de equilibrio de carga** y, a continuación, **agregar**.
   
    ![Reglas del equilibrador de carga de Azure Container Service](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Rellene el formulario de equilibrador de carga de Hola y haga clic en **Aceptar**.
   
   | Campo | Description |
   | --- | --- |
   | Nombre |Nombre descriptivo del equilibrador de carga de Hola. |
   | Port |puerto de entrada públicos de Hola. |
   | Puerto back-end |Puerto público interno de Hola Hola contenedor tooroute del tráfico de. |
   | Grupo back-end |contenedores de Hello en este grupo será el destino de Hola para este equilibrador de carga. |
   | Sondeo |Hola toodetermine sondeo utilizado si un destino en hello **grupo back-end** es correcto. |
   | Persistencia de la sesión |Determina cómo debe controlar el tráfico de un cliente durante Hola de sesión de Hola.<br><br>**Ninguno**: solicitudes sucesivas del mismo cliente pueda ser controlada por ningún contenedor de Hola.<br>**Cliente IP**: las solicitudes sucesivas de hello misma dirección IP del cliente se administran mediante Hola mismo contenedor.<br>**Cliente IP y protocolo**: las solicitudes sucesivas de hello misma combinación de IP y el protocolo de cliente se controlan mediante Hola mismo contenedor. |
   | Tiempo de espera inactividad |(Sólo TCP) En minutos, Hola tookeep tiempo abrir un cliente TCP o HTTP sin tener que depender *keep-alive* mensajes. |

## <a name="add-a-security-rule-portal"></a>Agregar una regla de seguridad (portal)
A continuación, necesitamos tooadd una regla de seguridad que enruta el tráfico desde el puerto abierto a través del firewall de Hola.

1. Inicie sesión en el portal de toohello.
2. Encontrar el grupo de recursos Hola que implementó Hola servicio de contenedor de Azure para.
3. Seleccione hello **pública** grupo de seguridad de red de agente (que se denomina similar demasiado**XXXX agente público nsg XXXX**).
   
    ![Grupo de seguridad de red de Azure Container Service](./media/container-service-enable-public-access/agent-nsg.png)
4. Seleccione **Reglas de seguridad de entrada** y luego **Agregar**.
   
    ![Reglas de grupos de seguridad de red de Azure Container Service](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Rellene tooallow de regla de firewall de hello el puerto público y haga clic en **Aceptar**.
   
   | Campo | Description |
   | --- | --- |
   | Nombre |Un nombre descriptivo de la regla de firewall de Hola. |
   | Prioridad |Rango de prioridad para la regla de Hola. Hola inferior Hola número Hola Hola prioridad. |
   | Origen |Restringir Hola entrantes IP dirección intervalo toobe permitirán o denegarán según esta regla. Use **cualquier** toonot especificar una restricción. |
   | Servicio |Seleccionar un conjunto de servicios predefinidos a los que vaya destinada esta regla de seguridad. De lo contrario utilice **personalizado** toocreate su propio. |
   | Protocol |Restringir el tráfico basado en **TCP** o **UDP**. Use **cualquier** toonot especificar una restricción. |
   | Intervalo de puertos |Cuando **servicio** es **personalizado**, especifica el intervalo de Hola de puertos que afecte esta regla. Puede usar un único puerto, como **80** o un intervalo como **1024-1500**. |
   | Acción |Permitir o denegar el tráfico que cumple los criterios de Hola. |

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de la diferencia de hello entre [públicos y privados de los agentes de DC/OS](container-service-dcos-agents.md).

Obtenga más información sobre cómo [administrar contenedores de DC/OS](container-service-mesos-marathon-ui.md).

