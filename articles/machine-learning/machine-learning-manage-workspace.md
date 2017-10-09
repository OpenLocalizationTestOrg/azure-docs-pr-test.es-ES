---
title: "un área de trabajo de aprendizaje automático de aaaManage | Documentos de Microsoft"
description: "Administrar el acceso a áreas de trabajo de aprendizaje automático de tooAzure, implementar y administrar los servicios web de API de aprendizaje automático"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Administración de un área de trabajo de Aprendizaje automático de Azure

> [!NOTE]
> Para obtener información sobre la administración de servicios Web en el portal de servicios Web de aprendizaje de máquina de hello, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).
> 
> 

Puede administrar áreas de trabajo de aprendizaje automático en cualquier portal de Azure de Hola u Hola portal de Azure clásico.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Usar hello portal de Azure

toomanage un área de trabajo en hello portal de Azure:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) con una cuenta de administrador de suscripción de Azure.
2. En cuadro de búsqueda de hello al principio de Hola de página de hello, escriba "áreas de trabajo de aprendizaje de la máquina" y, a continuación, seleccione **áreas de trabajo de aprendizaje automático**.
3. Haga clic en el área de trabajo de hello desee toomanage.

Además toohello información de administración de recursos estándar y las opciones disponibles, hacer lo siguiente:

- Vista **propiedades** : esta página muestra información de área de trabajo y recursos de Hola y puede cambiar suscripción Hola y el grupo de recursos que está conectada esta área de trabajo con.
- **Resincronizar claves de almacenamiento** -área de trabajo de hello mantiene la cuenta de almacenamiento de claves toohello. Si cambiar la cuenta de almacenamiento de hello las claves, puede hacer clic en **Resync claves** claves de hello toosynchronize con el área de trabajo de Hola.

Servicios de web de hello toomanage asociados a esta área de trabajo, usar el portal de servicios Web de aprendizaje de máquina de Hola. Vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) para obtener información completa.

> [!NOTE]
> toodeploy o administrar los nuevos servicios web debe tener asignado un colaborador o se implementa el rol de administrador en el servicio web de hello suscripción toowhich Hola. Si se invitar a otra área de trabajo de aprendizaje de automático de tooa de usuario, debe asignarlos tooa rol Colaborador o administrador de suscripción de Hola para poder implementar o administrar los servicios web. 
> 
>Para obtener más información sobre cómo establecer permisos de acceso, consulte [ver las asignaciones de acceso para usuarios y grupos en el portal de Azure - versión preliminar pública de hello](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Usar hello portal de Azure clásico

Con hello portal de Azure clásico, puede administrar las áreas de trabajo de aprendizaje automático para:

* Supervisar la utilización de área de trabajo de Hola
* Configurar tooallow de área de trabajo de Hola o denegar el acceso
* Administrar los servicios Web creados en el área de trabajo de Hola
* Eliminar área de trabajo de Hola

Además, la pestaña panel Hola proporciona información general sobre el uso del área de trabajo y una vista rápida de la información del área de trabajo.  

> [!TIP]
> En estudio de aprendizaje automático de Azure, en hello **servicios WEB** ficha, puede agregar, actualizar o eliminar un servicio Web de aprendizaje de máquina.
> 
> 

toomanage un área de trabajo en hello portal de Azure clásico:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con su Microsoft Azure cuenta - usar cuenta de hello que esté asociada con hello suscripción de Azure.
2. En el panel de servicios de Microsoft Azure hello, haga clic en **aprendizaje automático**.
3. Haga clic en el área de trabajo de hello desee toomanage.

página de área de trabajo de Hello tiene tres pestañas:

* **PANEL** -permite el uso del área de trabajo de tooview e información
* **CONFIGURAR** -permite el área de trabajo de toomanage access toohello
* **SERVICIOS WEB** -permite los servicios Web de toomanage que se han publicado desde esta área de trabajo

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor cómo se usa el área de trabajo de Hola
Haga clic en hello **panel** ficha.

En el panel de hello, puede ver el uso general del área de trabajo y obtener una vista rápida de la información del área de trabajo.

* Hola **proceso** gráfico muestra los recursos de proceso de hello usándola por área de trabajo de Hola. Puede cambiar Hola vista toodisplay relativa o valores absolutos, y puede cambiar el período de tiempo de hello muestra en el gráfico de Hola.
* **Información general del uso** muestra el almacenamiento de Azure que usa el área de trabajo de Hola.
* **Vista rápida** : proporciona un resumen de la información del área de trabajo y vínculos útiles.

> [!NOTE]
> Hola **inicio de sesión tooML Studio** vínculo abre estudio de aprendizaje automático con hello Account Microsoft ha iniciado sesión en. Hola Account Microsoft utiliza toosign en toohello toocreate portal clásico un área de trabajo de Azure no automáticamente tiene permiso tooopen esa área de trabajo. tooopen un área de trabajo, debe iniciar sesión en toohello Account de Microsoft que se ha definido como propietario de hello del área de trabajo de Hola o necesita tooreceive una invitación de área de trabajo de hello propietario toojoin Hola.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant o suspender el acceso a los usuarios
Haga clic en hello **configurar** ficha.

Desde la ficha de configuración de hello hacer lo siguiente:

* Suspender el área de trabajo de access toohello aprendizaje automático, haga clic en Denegar. Los usuarios ya no estará tooopen capaz de área de trabajo hello en estudio de aprendizaje automático. toorestore acceso, haga clic en permitir.

toomanage cuentas adicionales que tengan acceso toohello área de trabajo en estudio de aprendizaje automático, haga clic en **inicio de sesión tooML Studio** en hello **panel** pestaña (Véase la nota de hello precedente con respecto a  **Sign-In tooML Studio**). Se abre el área de trabajo de hello en estudio de aprendizaje automático. Desde aquí, haga clic en hello **configuración** ficha y, a continuación, **usuarios**. Puede hacer clic en **invitar a más usuarios** toogive a los usuarios tener acceso a área de trabajo de toohello, o seleccione un usuario y haga clic en **quitar**.

### <a name="toomanage-web-services-in-this-workspace"></a>toomanage los servicios web en esta área de trabajo
Haga clic en hello **servicios WEB** ficha.

Esto muestra una lista de servicios web publicados desde esta área de trabajo.
toomanage un servicio web, haga clic en nombre de hello en la página del servicio Web Hola lista tooopen Hola.

Un servicio web puede tener uno o varios puntos de conexión definidos.

* Puede definir varios puntos de conexión en el punto de conexión de adición toohello "Default". tooadd Hola de punto de conexión, haga clic en **administrar extremos** final Hola del portal de servicios Web de Azure Machine Learning de hello panel tooopen Hola.
* toodelete un punto de conexión (no se puede eliminar el punto de conexión de Hola "Default"), haga clic en casilla de verificación de hello en principio Hola de fila del punto de conexión de Hola y haga clic en **eliminar**. Esto quita el punto de conexión de Hola Hola servicio Web.
  
  > [!NOTE]
  > Si una aplicación está utilizando el extremo del servicio web hello cuando se elimina el punto de conexión de hello, aplicación hello recibirá un Hola error próxima vez que intente servicio de hello tooaccess.
  > 
  > 

Haga clic en nombre de Hola de un tooopen de punto de conexión de servicio Web. 

En el panel de hello, puede ver el uso general del servicio Web durante un período de tiempo. Puede seleccionar tooview período Hola desde el menú desplegable periodo de hello en la esquina superior derecha de Hola de gráficos de uso de Hola. panel de Hello muestra hello siguiente información:

* **Las solicitudes de un período** muestra un gráfico de paso del número de Hola de solicitudes Hola período de tiempo seleccionado. Puede ayudarlo a identificar si se están experimentando picos de uso.
* **Las solicitudes de solicitudes y respuestas** muestra hello número total de llamadas de solicitud-respuesta servicio Hola ha recibido a través hello período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de tiempo de respuesta de solicitud de proceso** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Las solicitudes por lote** muestra hello el número total de servicio de Hola de solicitudes por lotes ha recibido a través Hola período de tiempo seleccionado y no se pudo cuántos de ellos.
* **Promedio de latencia de trabajo** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.
* **Errores** muestra agregación del número de errores que se han producido hello en el servicio web de llamadas a toohello.
* **Los costos de servicios** muestra hello cargos para el plan de facturación de hello asociado con el servicio de Hola.

Hola en página de configuración, puede actualizar Hola propiedades siguientes:

* **Descripción** permite tooenter una descripción para el servicio Web de Hola. La descripción es un campo obligatorio.
* **Registro** permite error tooenable o deshabilitar el registro en el extremo de Hola. Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).
* **Habilitar los datos de ejemplo** permite tooprovide datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio. Si ha creado el servicio web de hello en estudio de aprendizaje automático, datos de ejemplo de Hola procede de datos de hello su tootrain usa el modelo. Si ha creado el servicio de hello mediante programación, los datos de Hola se toman de los datos de ejemplo de Hola proporcionados como parte del paquete de hello JSON.

