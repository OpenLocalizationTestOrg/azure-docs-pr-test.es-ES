---
title: "Inicio rápido de implementación de Kit de desarrollo de pila aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy Hola Kit de desarrollo de pila de Azure"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 7f9fcd3a620e2916a24e57990d93dc9ace2b1129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-deployment-quickstart"></a>Guía de inicio rápido de la implementación de Azure Stack Development Kit

Hola [Kit de desarrollo de Azure pila](azure-stack-poc.md) es un entorno de desarrollo y pruebas que puede implementar tooevaluate y mostrar los servicios y características de la pila de Azure. tooget, configúrelo y en ejecución, podrá necesita tooprepare Hola entorno hardware y ejecutar algunos scripts (operación tardará varias horas). Después de eso, puede iniciar sesión en el Administrador de toohello e inquilino portales toomanage pila de Azure y ofertas de prueba. 

1. [**Planee el hardware, software y red**](azure-stack-deploy.md). equipo de Hola que hospeda el kit de desarrollo de hello (host de kit de desarrollo de hello) debe cumplir requisitos de hardware, software y red. También debe elegir entre el uso de Azure Active Directory o de los Servicios de federación de Active Directory. Ser toocomply seguro con estos requisitos previos antes de comenzar la implementación para que el proceso de instalación de Hola se ejecuta sin problemas. 

2. [**Descargue y extraiga el paquete de implementación de hello**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit). Puede descargar el host de kit de desarrollo toohello del paquete de la implementación Hola o tooa otro equipo. Hola extrae archivos tardan hasta 60 GB de espacio libre en disco, por lo que usar otro equipo puede ayudar a reducir los requisitos de hardware de hello para el host de kit de desarrollo de Hola de implementación.

3. [**Preparar el host de kit de desarrollo de hello** ](azure-stack-run-powershell-script.md#prepare-the-development-kit-host) mediante el instalador de Hola. Después de este paso, el host de kit de desarrollo de hello arrancará toohello Cloudbuilder.vhdx (archivos de instalación de una unidad de disco duro virtual que incluye un sistema operativo de arranque y hello Azure pila).

4. [**Implementar el kit de desarrollo de hello** ](azure-stack-run-powershell-script.md#deploy-the-development-kit) en host de kit de desarrollo de Hola.

5. Si la implementación de la pila de Azure usa Azure Active Directory, debe [registrar pila de Azure con Azure](azure-stack-register.md) para que pueda [descargar elementos de Azure marketplace](azure-stack-download-azure-marketplace-item.md) tooAzure pila.

Después de completar estos pasos, tendrá un entorno de Development Kit con los portales del administrador y del inquilino. A continuación, puede [conectarse e inicie sesión en](azure-stack-connect-azure-stack.md) portal toohello. A continuación, puede iniciar la implementación de proveedores de recursos, crear [ofrece](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions), y rellenar hello Azure pila [marketplace](azure-stack-marketplace.md).
