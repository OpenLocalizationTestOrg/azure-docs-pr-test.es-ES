---
title: 'aaaAzure muestras de CLI: servicio de aplicaciones | Documentos de Microsoft'
description: 'Ejemplos de la CLI de Azure: App Service'
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Ejemplos de la CLI de Azure

Hello tabla siguiente incluye vínculos toobash scripts creados con hello CLI de Azure.

| | |
|-|-|
|**Creación de la aplicación**||
| [Creación de una aplicación web e implementación de código desde GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure e implementa código proveniente de un repositorio público de GitHub. |
| [Creación de una aplicación web con implementación continua desde GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure con publicación continua desde un repositorio de GitHub de su propiedad. |
| [Creación de una aplicación web e implementación de código desde un repositorio local de GitHub](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure y configura la inserción de código desde un repositorio de Git local. |
| [Crear una aplicación web e implementar el entorno de ensayo de tooa de código](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure con una ranura de implementación para cambios en el código de ensayo. |
| [Creación de una aplicación web de ASP.NET Core en un contenedor de Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure en Linux y carga una imagen de Docker desde Docker Hub. |
|**Configuración de la aplicación**||
| [Asignar una aplicación web de tooa de dominio personalizado](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure y asigna un tooit de nombre de dominio personalizado. |
| [Enlazar una aplicación de web de tooa de certificado SSL personalizada](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure y enlaza el certificado SSL de Hola de un tooit de nombre de dominio personalizado. |
|**Escalado de la aplicación**||
| [Escalado manual de una aplicación web](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure y la escala a través de dos instancias. |
| [Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Crea dos aplicaciones web de Azure en dos regiones geográficas diferentes y hace que estén disponibles a través de un punto de conexión único mediante Azure Traffic Manager. |
|**Conectar tooresources de aplicación**||
| [Conectar un tooa de aplicación web base de datos SQL](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure y una base de datos SQL, a continuación, agrega la configuración de aplicación de hello base de datos conexión cadena toohello. |
| [Conectarse a una cuenta de almacenamiento de tooa de aplicación web](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una aplicación web de Azure y una cuenta de almacenamiento, a continuación, agrega la configuración de la aplicación hello almacenamiento conexión cadena toohello. |
| [Conectar una caché de redis de tooa de aplicación web](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure y una caché de redis, a continuación, agrega la configuración de aplicación de hello redis conexión detalles toohello.) |
| [Conectar un tooCosmos de aplicación web DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure y una base de datos de Cosmos y, a continuación, agrega la configuración de aplicación de Hola DB Cosmos conexión detalles toohello. |
|**Supervisión de la aplicación**||
| [Supervisión de una aplicación web con registros de servidor web](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una aplicación web de Azure, habilita el registro para el mismo y descarga el equipo local de hello registros tooyour. |
| | |