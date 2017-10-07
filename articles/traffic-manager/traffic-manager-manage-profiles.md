---
title: perfiles de Azure Traffic Manager aaaManage | Documentos de Microsoft
description: "La información contenida en este artículo le ayuda a crear, deshabilitar, habilitar y eliminar un perfil de Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Administrar un perfil del Administrador de tráfico de Azure

Perfiles de Traffic Manager usan enrutamiento del tráfico distribución métodos de hello toocontrol de servicios de nube de tráfico tooyour o los puntos de conexión de sitio Web. Este artículo se explica cómo toocreate y administrar estos perfiles.

## <a name="create-a-traffic-manager-profile"></a>Crear un perfil de Traffic Manager

Puede crear un perfil de Traffic Manager mediante Hola portal de Azure. Después de crear el perfil, puede configurar los puntos de conexión, supervisión y otras opciones en hello portal de Azure. Es compatible con el Administrador de tráfico too200 extremos por perfil. Sin embargo, la mayoría de los escenarios de uso tan solo requieren unos pocos puntos de conexión.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate un perfil de Traffic Manager

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/). 
2. En hello **concentrador** menú, haga clic en **New** > **red** > **ver todas**, haga clic en **tráfico Administrador de** hello tooopen de perfil **perfil del Administrador de tráfico crear** hoja, a continuación, haga clic en **crear**.
3. En hello **crear Traffic Manager perfil** hoja, completa, como sigue:
    1. En **Nombre**, proporcione un nombre para el perfil. Este nombre debe toobe único dentro de la zona de trafficmanager.net hello y da lugar a nombre DNS de hello <name>, trafficmanager.net, que es tooaccess usa el perfil de Traffic Manager.
    2. En **método de enrutamiento**, seleccione hello **prioridad** método de enrutamiento.
    3. En **suscripción**, seleccione suscripción Hola desees toocreate este perfil en
    4. En **grupo de recursos**, crear un nuevo tooplace de grupo de recursos de este perfil en.
    5. En **ubicación del grupo de recursos**, Seleccionar ubicación de Hola Hola del grupo de recursos. Esta configuración hace referencia toohello ubicación del grupo de recursos de hello y no tiene ningún efecto en el perfil de Traffic Manager que se va a implementar todo el mundo Hola.
    6. Haga clic en **Crear**.
    7. Una vez completada la implementación global Hola de su perfil de Traffic Manager, se muestra en el grupo de recursos correspondiente como uno de los recursos de Hola.

## <a name="disable-enable-or-delete-a-profile"></a>Deshabilitar, habilitar o eliminar un perfil

Puede deshabilitar un perfil existente para que Traffic Manager no hace referencia a los puntos de conexión de usuario solicitudes toohello configurado. Cuando se deshabilita un perfil de Traffic Manager, perfil de Hola y la información de hello incluida en el perfil de hello permanecen intactas y se pueden editar en la interfaz de Traffic Manager Hola.  Las referencias se reanudará cuando se vuelve a habilitar el perfil de Hola. Cuando se crea un perfil de Traffic Manager Hola portal de Azure, se habilita automáticamente. Si decide que un perfil ha dejado de ser necesario, puede eliminarlo.

### <a name="toodisable-a-profile"></a>toodisable un perfil

1. Si usas un nombre de dominio personalizado, cambiar registro CNAME de hello en el servidor DNS de Internet para que ya no apunta tooyour perfil de Traffic Manager.
2. Deja de tráfico que se ha dirigido toohello extremos a través de la configuración de perfil de Traffic Manager de Hola.
3. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de Hola Hola resultados que muestra de Hola.
3. Hola **perfil de Traffic Manager** hoja, haga clic en **Introducción**, en la hoja de información general de hello, haga clic en **deshabilitar**y, a continuación, confirme el perfil de Traffic Manager de hello toodisable.

### <a name="tooenable-a-profile"></a>tooenable un perfil

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de Hola Hola resultados que muestra de Hola.
3. Hola **perfil de Traffic Manager** hoja, haga clic en **Introducción**y, a continuación, en la hoja de información general de hello haga clic en **habilitar**.
5. Si usas un nombre de dominio personalizado, cree un registro de recurso CNAME en el nombre de dominio DNS de Internet server toopoint toohello de su perfil de Traffic Manager.
6. Tráfico es dirigido toohello puntos de conexión de nuevo.

### <a name="toodelete-a-profile"></a>toodelete un perfil

1. Asegúrese de que el registro de recursos DNS de hello en el servidor DNS de Internet ya no utiliza un registro de recurso CNAME que señala toohello nombre de dominio de su perfil de Traffic Manager.
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de Hola Hola resultados que muestra de Hola.
3. Hola **perfil de Traffic Manager** hoja, haga clic en **Introducción**, en la hoja de información general de hello, haga clic en **eliminar**y, a continuación, confirme el perfil de Traffic Manager de hello toodelete.

## <a name="next-steps"></a>Pasos siguientes

* [Agregación de un extremo](traffic-manager-endpoints.md)
* [Configuración del método de enrutamiento por prioridad](traffic-manager-configure-priority-routing-method.md)
* [Configuración del método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md) 
* [Configuración del método de enrutamiento ponderado](traffic-manager-configure-weighted-routing-method.md)
* [Configuración del método de enrutamiento de rendimiento](traffic-manager-configure-performance-routing-method.md)
