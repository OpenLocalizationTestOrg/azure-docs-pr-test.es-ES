---
title: "aaaEnable conexión a Escritorio remoto para un rol de servicios de nube de Azure | Documentos de Microsoft"
description: "¿Cómo tooconfigure la nube de azure conexiones de escritorio remoto de tooallow de aplicación de servicio"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal de Azure clásico](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Escritorio remoto permite escritorio de hello tooaccess de una función que se ejecuta en Azure. Puede usar un tootroubleshoot de conexión de escritorio remoto y diagnosticar problemas con la aplicación mientras se está ejecutando.

Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de módulos de escritorio remoto de hello en la definición de servicio o puede elegir tooenable escritorio remoto a través de hello extensión de escritorio remoto. Hello método preferido es extensión de escritorio remoto de hello toouse tal y como se puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello sin necesidad de tooredeploy la aplicación.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Configurar Escritorio remoto desde Hola portal de Azure
Hola portal de Azure utiliza el método de extensión de escritorio remoto de Hola por lo que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello. Hola **escritorio remoto** hoja para el servicio de nube permite tooenable escritorio remoto, Hola cambiar cuenta de administrador local usa máquinas virtuales de tooconnect toohello, certificado Hola utilizada en la autenticación y establece Hola fecha de expiración.

1. Haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **escritorio remoto**.

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Elija si desea tooenable escritorio remoto para un rol individual o para todos los roles, a continuación, cambie el valor de Hola de modificador de hello demasiado**habilitado**.

3. Rellene los campos de hello necesario para el nombre de usuario, contraseña, expiración y el certificado.

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación). tooprevent un reinicio, contraseña de Hola de hello certificado tooencrypt usado debe estar instalado en el rol de Hola. tooprevent un reinicio, [cargar un certificado de servicio en la nube hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, a continuación, devolver toothis cuadro de diálogo.
   >
   >
3. En **Roles**, seleccione el rol de Hola que desee tooupdate o seleccione **todos los** para todos los roles.

4. Después de terminar las actualizaciones de la configuración, haga clic en **Guardar**. Tardará unos minutos antes de que las instancias del rol son conexiones tooreceive listo.

## <a name="remote-into-role-instances"></a>Acceso remoto en instancias de rol
Una vez que Escritorio remoto está habilitado en los roles de hello, puede iniciar una conexión directamente desde Hola Portal de Azure:

1. Haga clic en **instancias** tooopen hello **instancias** hoja.
2. Seleccione una instancia de rol que tenga el Escritorio remoto configurado.
3. Haga clic en **conectar** toodownload un RDP de archivos para la instancia de rol de Hola.

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Haga clic en **abiertos** y, a continuación, **conectar** toostart Hola conexión a Escritorio remoto.

>[!NOTE]
> Si su servicio en la nube se encuentra detrás de un NSG, probablemente necesite toocreate reglas que permitan el tráfico en puertos **3389** y **20000**.  Escritorio remoto usa el puerto **3389**.  Instancias de servicio en la nube son carga equilibrada, por lo que directamente no se puede controlar qué tooconnect de instancia a.  Hola *RemoteForwarder* y *RemoteAccess* agentes administrar el tráfico RDP y permitir Hola cliente toosend una cookie RDP y especificar un tooconnect de una instancia individual a.  Hola *RemoteForwarder* y *RemoteAccess* agentes requieren ese puerto **20000*** abrirse, que pueden bloquearse si tienes un NSG.

## <a name="additional-resources"></a>Recursos adicionales

[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)
