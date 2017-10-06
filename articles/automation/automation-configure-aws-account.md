---
title: "aaaConfigure autenticación con Amazon Web Services | Documentos de Microsoft"
description: "Este artículo se describe cómo toocreate y validar una credencial AWS para runbooks de automatización de Azure, la administración de recursos AWS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "autenticación AWS, configurar aws"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: 6edaa000c1b206d80fe64b18c729dac124849070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Autenticación de Runbooks con Amazon Web Services
La automatización de las tareas comunes con recursos de Amazon Web Services (AWS) se puede realizar con los Runbooks de Automatización de Azure.  Puede automatizar muchas tareas en AWS mediante Runbooks de Automatización exactamente igual que con recursos de Azure.  Todo lo que se necesita son dos cosas:

* Una suscripción a AWS y un conjunto de credenciales.  En concreto, la clave de acceso y la clave secreta de AWS.  Para obtener más información, consulte el artículo de hello [utilizando las credenciales de AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Una suscripción a Azure y una cuenta de Automatización.  Para obtener más información sobre cómo configurar una cuenta de automatización de Azure, revise el artículo de hello [configurar Azure cuenta de ejecución](automation-sec-configure-azure-runas-account.md).  

tooauthenticate con AWS, debe especificar un conjunto de AWS credenciales tooauthenticate sus runbooks en ejecución de automatización de Azure. Si ya tiene una cuenta de automatización creada y desea toouse que tooauthenticate con AWS, puede seguir los pasos de Hola Hola pasos de la sección.  Si desea toodedicated una cuenta de recursos de runbooks como destino la AWS, primero debe crear un nuevo [automatización de la cuenta de ejecución](automation-sec-configure-azure-runas-account.md) (omitir Hola opción toocreate una entidad de servicio) y, a continuación, siga estos pasos Hola.

## <a name="configure-automation-account"></a>Configuración de la cuenta de Automatización
Para toocommunicate de automatización de Azure con AWS, primero deberá tooretrieve sus credenciales AWS y almacenarlas como activos de automatización de Azure.  Realizar Hola siguiendo los pasos que se describen en el documento AWS hello [administrar claves de acceso de su cuenta de AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate una tecla de acceso y copia hello **Id. de clave de acceso** y **clave secreta de acceso** (si lo desea descargar el archivo de clave toostore, en un lugar seguro).

Una vez haya creado y copiar las claves de seguridad AWS, deberá toocreate un recurso de credencial con una toosecurely de cuenta de automatización de Azure almacenarlos y hacer referencia a ellos con sus runbooks.  Siga los pasos de hello en la sección de hello **crear un nuevo recurso de credencial** en hello [credencial activos de automatización de Azure](automation-credentials.md) artículo y escriba Hola siguiente información:

1. Hola **nombre** cuadro, escriba **AWScred** o un valor adecuado siguiendo los estándares de nomenclatura.  
2. Hola **nombre de usuario** cuadro, escriba su **Id. de acceso** y su **clave secreta de acceso** en hello **contraseña** y **confirmar contraseña** cuadro.   

## <a name="next-steps"></a>Pasos siguientes
* Artículo de solución de hello Reivew [automatizar la implementación de una máquina virtual en Amazon Web Services](automation-scenario-aws-deployment.md) toolearn cómo toocreate runbooks tooautomate tareas AWS.

