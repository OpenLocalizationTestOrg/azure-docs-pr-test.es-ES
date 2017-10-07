---
title: "un área de trabajo de aprendizaje automático de aaaCreate | Documentos de Microsoft"
description: "¿Cómo toocreate un área de trabajo de estudio de aprendizaje automático de Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Creación y uso compartido de un área de trabajo de Aprendizaje automático de Azure
Este menú vincula tootopics que describen cómo tooset seguridad Hola varios entornos de ciencia de datos utilizan por hello proceso de análisis de Cortana (CAP).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse estudio de aprendizaje automático de Azure, deberá toohave un área de trabajo de aprendizaje automático. Esta área de trabajo contiene herramientas de Hola que necesita toocreate, administrar y publicar experimentos.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate un área de trabajo
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign en y crear un área de trabajo, deberá toobe un administrador de suscripción de Azure. 
    >
    > 

2. Haga clic en **+ Nuevo**.

3. Seleccione **Intelligence + analytics**, haga clic en el **área de trabajo de Machine Learning** y, a continuación, haga clic en **Crear**.

4. Escriba la información de su área de trabajo.

    - Hola *nombre de área de trabajo* puede ser up too260 caracteres, no termina en un espacio. nombre de Hello no puede incluir estos caracteres:`< > * % & : \ ? + /`
    - Hola *plan del servicio web* elija (o cree), junto con los asociados de hello *tarifa* seleccione, se usa si implementa servicios web desde esta área de trabajo.

    ![Crear un área de trabajo](media/machine-learning-create-workspace/create-new-workspace.png)

5. Haga clic en **Crear**

Una vez implementado el área de trabajo de hello, puede abrirlo en estudio de aprendizaje automático.

1. Examinar tooMachine estudio de aprendizaje en [https://studio.azureml.net/](https://studio.azureml.net/).

2. Seleccione el área de trabajo en la esquina superior derecha de Hola.

    ![Selección del área de trabajo](media/machine-learning-create-workspace/open-workspace.png)

3. Haga clic en **my experiments** (Mis experimentos).

    ![Abrir experimentos](media/machine-learning-create-workspace/my-experiments.png)

Para obtener más información sobre cómo administrar un área de trabajo, consulte [Administración de un área de trabajo de Aprendizaje automático de Azure](machine-learning-manage-workspace.md).
Si se produce un problema al crear el área de trabajo, consulte [Guía de solución de problemas: crear y conectar el área de trabajo de aprendizaje automático de tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Uso compartido de un área de trabajo de Aprendizaje automático de Azure
Una vez que se crea un área de trabajo de aprendizaje automático, puede invitar a los usuarios tooyour área de trabajo tooshare acceso tooyour área de trabajo y todos los sus experimentos, conjuntos de datos, blocs de notas, etcetera. Puede agregar usuarios en uno de estos roles:

* **Usuario** -un usuario del área de trabajo puede crear, abrir, modificar y eliminar experimentos, conjuntos de datos, etc. en el área de trabajo de Hola.
* **Propietario** : puede invitar un propietario y quitar usuarios en área de trabajo de hello en suma toowhat un usuario pueden hacer.

> [!NOTE]
> cuenta de administrador de Hola que crea el área de trabajo de Hola se agrega automáticamente el área de trabajo de toohello como propietario del área de trabajo. Sin embargo, otros administradores o usuarios en que la suscripción no son automáticamente concedido acceso toohello área de trabajo, deberá tooinvite ellos explícitamente.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare un área de trabajo

1. Inicie sesión en tooMachine estudio de aprendizaje en [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. En el panel izquierdo de hello, haga clic en **configuración**

3. Haga clic en hello **usuarios** ficha

4. Haga clic en **invitar a más usuarios** final Hola de página Hola

    ![Configuración de Studio](media/machine-learning-create-workspace/settings.png)

5. Escriba una o varias direcciones de correo electrónico. los usuarios de Hello necesitan una cuenta válida de Microsoft o una cuenta profesional (de Azure Active Directory).

6. Seleccione si desea que los usuarios de hello tooadd como propietario o usuario.

7. Haga clic en hello **Aceptar** botón de marca de verificación.

Cada usuario que agregue recibirán un correo electrónico con instrucciones sobre cómo toosign en toohello comparte el área de trabajo.

> [!NOTE]
> Para los usuarios toobe puede toodeploy o administrar servicios web en esta área de trabajo, deben ser un colaborador o administrador de hello suscripción de Azure. 



