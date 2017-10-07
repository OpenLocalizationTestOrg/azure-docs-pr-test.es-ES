---
title: "aaaApplication o específica del usuario maratón servicio | Documentos de Microsoft"
description: "Creación de un servicio de Marathon específico del usuario o la aplicación"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, Marathon, microservicios, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Creación de un servicio de Marathon específico del usuario o la aplicación
Azure Container Service proporciona un conjunto de servidores maestros en los que preconfiguramos Apache Mesos y Marathon. Éstas pueden ser utilizado tooorchestrate las aplicaciones en clúster de hello, pero recomendados no toouse Hola los servidores maestros para este propósito. Por ejemplo, ajustar la configuración de Hola de maratón requiere iniciar sesión en servidores maestros de Hola por sí mismos y realizar cambios, esto le anima únicos servidores maestros que son un poco diferentes de hello estándar y necesidad toobe atendido y administrado de forma independiente. Además, configuración de hello necesaria para un equipo podría no ser la configuración óptima de Hola para otro equipo.

En este artículo, explicaremos cómo tooadd un servicio de maratón de aplicación o del usuario.

Dado que este servicio pertenecerá tooa solo usuario o equipo, son tooconfigure libre, de manera que lo desean. Además, el servicio de contenedor de Azure se asegurará de que el servicio de hello sigue toorun. Si se produce un error en el servicio de hello, servicio de contenedor de Azure se reiniciará automáticamente. La mayoría de las veces de hello incluso no notarás que tenía el tiempo de inactividad.

## <a name="prerequisites"></a>Requisitos previos
[Implementar una instancia de servicio de contenedor de Azure](container-service-deployment.md) con orchestrator escriba DC/OS y [Asegúrese de que el cliente puede conectarse tooyour clúster](../container-service-connect.md). Además, el Hola lo siguiente.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Creación de un servicio de Marathon específico del usuario o la aplicación
Empiece por crear un archivo de configuración de JSON que define el nombre de hello del servicio de aplicación de Hola que desea toocreate. Aquí usamos `marathon-alice` como nombre de marco de Hola. Guardar archivo hello como algo parecido a `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

A continuación, use instancia maratón de Hola DC/OS CLI tooinstall Hola con opciones de Hola que se establecen en el archivo de configuración:

```bash
dcos package install --options=marathon-alice.json marathon
```

Ahora debería ver su `marathon-alice` servicio se ejecuta en la ficha de servicios de saludo de la interfaz de usuario del controlador de dominio/OS. Hello interfaz de usuario será `http://<hostname>/service/marathon-alice/` si desea tooaccess directamente.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Establecer Hola DC/OS CLI tooaccess servicio Hola
Opcionalmente puede configurar este nuevo servicio de la CLI de DC/OS tooaccess por establecer hello `marathon.url` propiedad toopoint toohello `marathon-alice` instancia como sigue:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Puede comprobar qué instancia de maratón con la que la CLI funciona contra Hola `dcos config show` comando. Puede revertir toousing su servicio de maratón maestro con el comando hello `dcos config unset marathon.url`.

