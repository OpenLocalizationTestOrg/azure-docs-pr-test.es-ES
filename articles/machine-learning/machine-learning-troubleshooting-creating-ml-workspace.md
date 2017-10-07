---
title: "Solucionar problemas: Crear y conectar el área de trabajo de aprendizaje automático de tooa | Documentos de Microsoft"
description: "Soluciones para problemas comunes de creación y la conexión de área de trabajo de aprendizaje automático de Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Guía de solución de problemas: crear y conectar el área de trabajo de aprendizaje automático de tooan
Esta guía proporciona soluciones para algunos de los desafíos más comunes al configurar áreas de trabajo de Aprendizaje automático de Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Propietario del espacio de trabajo
tooopen un área de trabajo en estudio de aprendizaje automático, debe ser firmado en toohello Account de Microsoft usa el área de trabajo de toocreate hello, o si debe tooreceive una invitación de área de trabajo de hello propietario toojoin Hola. De hello portal de Azure puede administrar Hola área de trabajo, que incluye el acceso de hello capacidad tooconfigure.

Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure].

[Administración de un área de trabajo de Aprendizaje automático de Azure]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Regiones permitidas
Aprendizaje automático se encuentra actualmente disponible en un número limitado de regiones. Si su suscripción no incluye una de estas regiones, verá el mensaje de error de hello, "No tiene suscripciones en hello permiten regiones."

toorequest que una región de ser agregado tooyour suscripción, cree una nueva solicitud de soporte técnico de Microsoft de hello portal de Azure, elija **facturación** como tipo de problema de Hola y seguir Hola solicita toosubmit su solicitud.

## <a name="storage-account"></a>Cuenta de almacenamiento
Hola servicio aprendizaje automático necesita un toostore de datos de la cuenta de almacenamiento. Puede usar una cuenta de almacenamiento existente, o puede crear una nueva cuenta de almacenamiento al crear el área de trabajo de aprendizaje automático nuevo hello (si tiene una cuenta de almacenamiento toocreate de cuota).

Después de crea el área de trabajo de hello nuevo aprendizaje automático, puede iniciar sesión tooMachine estudio de aprendizaje con cuenta de Microsoft hello que usa el área de trabajo de toocreate Hola. Si se produce el mensaje de error de hello, "Área de trabajo no encontrado" (toohello similar siguiente captura de pantalla), utilice Hola siguiendo los pasos toodelete las cookies del explorador.

![Espacio de trabajo no encontrado][screen3]

**cookies del explorador toodelete**

1. Si utiliza Internet Explorer, haga clic en hello **herramientas** situado en la esquina superior derecha de Hola y seleccione **opciones de Internet**.  

![Opciones de Internet][screen4]

2. En hello **General** , haga clic en **eliminar...**

![Pestaña General][screen5]

3. Hola **eliminar el historial de exploración** diálogo cuadro, asegúrese de que **Cookies y datos del sitio Web** está seleccionada y haga clic en **eliminar**.

![Eliminación de cookies][screen6]

Después de eliminarán las cookies de hello, reinicie el Explorador de hello y, a continuación, vaya toohello [aprendizaje automático de Microsoft Azure](https://studio.azureml.net) página. Cuando se le pida, escriba un nombre de usuario y una contraseña, Hola la misma cuenta de Microsoft que usa el área de trabajo de toocreate Hola.

## <a name="comments"></a>Comentarios

Nuestro objetivo es toomake Hola máxima uniformidad posible de experiencia de aprendizaje automático. Publique los comentarios y problemas en hello [foro de aprendizaje automático de Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nos ofrecerle un servicio mejor.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
