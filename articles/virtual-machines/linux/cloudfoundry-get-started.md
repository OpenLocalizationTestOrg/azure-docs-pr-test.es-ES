---
title: aaaGetting Started with Foundry en la nube en Microsoft Azure | Documentos de Microsoft
description: "Ejecución de OSS o Pivotal Cloud Foundry en Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry en Azure

Cloud Foundry es una plataforma como servicio (PaaS) de código abierto para compilar, implementar y operar aplicaciones de factor 12 desarrolladas en diversos lenguajes y marcos. Este documento describe opciones de hello que tiene para ejecutar Foundry en la nube en Azure y cómo puede comenzar a trabajar.

## <a name="cloud-foundry-offerings"></a>Ofertas de Cloud Foundry

Hay dos formas de nube Foundry toorun disponible en Azure: nube Foundry (OSS CF) y esencial en la nube Foundry (PCF) de código abierto. CF de OSS es un completamente [código abierto](https://github.com/cloudfoundry) versión de nube Foundry administrados por hello en la nube Foundry Foundation. Esencial Foundry en la nube es una distribución empresarial de nube Foundry de crucial Software Inc. Nos centramos en algunas de las diferencias de hello entre dos ofertas de Hola.

### <a name="open-source-cloud-foundry"></a>Cloud Foundry de código abierto

Puede implementar sistemas operativos en la nube Foundry en Azure primero implementando un director de BOSH y, a continuación, implementar Foundry en la nube, con hello [instrucciones proporcionadas en GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn más sobre el uso de OSS CF, vea hello [documentación](https://docs.cloudfoundry.org/) proporcionada por hello en la nube Foundry Foundation.

Microsoft ofrece compatibilidad de mejor esfuerzo para CF de sistemas operativos a través de hello después de canales de la Comunidad:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>Canal bosh-azure-cpi en [Cloud Foundry Slack](https://slack.cloudfoundry.org/)
- [Lista de correo cf-bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problemas de GitHub para hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) y [broker de servicio](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> nivel de Hola de compatibilidad para los recursos de Azure, como máquinas virtuales de hello en el que se ejecuta en la nube Foundry, se basa en su contrato de soporte técnico de Azure. Compatibilidad con la Comunidad de mejor esfuerzo solo aplica a componentes toohello específicos de Foundry la nube.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

Esencial Foundry nube incluye Hola misma plataforma principal como distribución de hello OSS, junto con un conjunto de herramientas de administración de propietario y soporte técnico empresarial. toorun PCF en Azure, debe adquirir una licencia de Pivotal. Esta oferta PCF Hola de hello Azure marketplace incluye una licencia de prueba de 90 días.

Hola herramientas incluyen [esencial de Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), una aplicación web que simplifica la implementación y administración de una base de Foundry en la nube, y [fundamental dentro de aplicaciones de administrador](https://docs.pivotal.io/pivotalcf/console/), una aplicación web para administrar los usuarios y aplicaciones.

Además toohello canales de soporte técnico enumerados para CF de sistemas operativos anteriores, una licencia PCF da derecho toocontact Pivotal para soporte técnico. Microsoft y Pivotal también han habilitado los flujos de trabajo de compatibilidad que permiten toocontact de cualquiera de las partes para obtener ayuda y tienen su consulta enrute adecuadamente según donde se encuentra el problema de Hola.

## <a name="azure-service-broker"></a>Agente de servicio de Azure

Nube Foundry encarecidamente hello ["factor de doce app"](https://12factor.net/) metodología, lo que promueve una separación clara de los procesos de aplicación sin estado y con estado realizar una copia de los servicios. [Servicio corredores de bolsa](https://docs.cloudfoundry.org/services/api.html) ofrecen un tooprovision de forma coherente y enlazar tooapplications de servicios de copia de seguridad. Hola [agente del servicio de Azure](https://github.com/Azure/meta-azure-service-broker) proporciona algunos Hola claves servicios de Azure a través de este canal, incluido el almacenamiento de Azure y SQL Azure.

Si usas esencial Foundry en la nube, Hola service broker está también [disponible como un icono](https://docs.pivotal.io/azure-sb/installing.html) de hello red esencial.

## <a name="related-resources"></a>Recursos relacionados

### <a name="visual-studio-team-services-plugin"></a>Complemento de Visual Studio Team Services

En la nube Foundry es idóneo tooagile: desarrollo de software, incluido el uso de Hola de integración continua (CI) y la entrega continua (CD). Si usar sus proyectos de Visual Studio Team Services (VSTS) toomanage y desearía tooset de una canalización de CI/CD Foundry en la nube de destino, puede usar hello [VSTS nube Foundry generar extensión](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). resulta sencillo tooconfigure Hello complemento y automatizar las implementaciones tooCloud Foundry, si se ejecuta en Azure o en otro entorno.

## <a name="next-steps"></a>Pasos siguientes

- [Implementar esencial Foundry en la nube de hello Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Implementar un tooCloud aplicación Foundry en Azure](./cloudfoundry-deploy-your-first-app.md)
