---
title: "Recursos de la aplicación Web de aaaMove tooanother grupo de recursos"
description: Se describen escenarios de Hola donde puede mover las aplicaciones Web y servicios de aplicaciones de tooanother de un grupo de recursos.
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Configuraciones admitidas para traslados
Puede mover los recursos de aplicación Web de Azure usando hello [mover la API de recursos del Administrador de recursos](../azure-resource-manager/resource-group-move-resources.md).

Las aplicaciones Web de Azure admite actualmente Hola mover los escenarios siguientes:

* Mover todo el contenido de un grupo de recursos (aplicaciones web, planes de servicio de aplicaciones y certificados) hello tooanother grupo de recursos. 
   > [!Note]
   > grupo de recursos de destino de Hello no puede contener cualquier recurso Microsoft.Web en este escenario.

* Mover grupo de recursos distinto de tooa de aplicaciones web individuales, mientras todavía hospedaje de ellos en su plan de servicio de aplicación actual (Hola aplicación servicio plan permanece en grupo de recursos de hello anterior).


