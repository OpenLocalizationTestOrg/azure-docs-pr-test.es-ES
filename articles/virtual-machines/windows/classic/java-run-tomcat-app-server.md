---
title: "servidor de aplicaciones de Java de aaaRun en una máquina virtual de Azure clásico | Documentos de Microsoft"
description: "Este tutorial usa recursos creados con el modelo de implementación clásica de Hola y muestra cómo toocreate una Virtual de Windows del equipo y configurar servidor de aplicaciones de Apache Tomcat toorun."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>¿Cómo toorun un servidor de aplicaciones de Java en una máquina virtual creado con el modelo de implementación clásica de Hola
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para una plantilla de administrador de recursos toodeploy una aplicación Web con Java 8 y Tomcat, consulte [aquí](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Con Azure, puede usar capacidades de servidor de un tooprovide de máquina virtual. Por ejemplo, una máquina virtual que se ejecuta en Azure puede ser toohost configurado un servidor de aplicaciones Java, como Apache Tomcat.

Después de completar esta guía, tendrá una descripción de cómo toocreate una máquina virtual ejecuta en Azure y configurar un servidor de aplicaciones Java toorun. Aprenderá y realizar Hola siguientes tareas:

* Cómo toocreate un virtual del equipo que tiene un Kit de desarrollo de Java (JDK) ya instalado.
* ¿Cómo tooremotely inicie sesión en la máquina virtual de tooyour.
* ¿Cómo tooinstall un servidor de aplicaciones de Java: Apache Tomcat--en la máquina virtual.
* ¿Cómo toocreate un extremo para la máquina virtual.
* ¿Cómo tooopen un puerto en Hola de firewall para el servidor de aplicaciones.

Hola completado resultados de la instalación de Tomcat que se ejecuta en una máquina virtual.

![Máquina virtual que ejecuta Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate una máquina virtual
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).  
2. Haga clic en **New**, haga clic en **proceso**, a continuación, haga clic en **ver todas** en hello **aplicaciones destacadas**.
3. Haga clic en **JDK**, haga clic en **JDK 8** en hello **JDK** panel.  
   Imágenes de máquina virtual que admiten **JDK 6** y **JDK 7** están disponibles si tiene aplicaciones heredadas que no están listo toorun en JDK 8.
4. En el panel de hello JDK 8, seleccione **clásico**, a continuación, haga clic en **crear**.
5. Hola **Fundamentos** hoja:
   1. Especifique un nombre para la máquina virtual de Hola.
   2. Escriba un nombre para el Administrador de Hola Hola **nombre de usuario** campo. Recuerde que este nombre y Hola contraseña asociada que aparece más adelante en el siguiente campo de Hola. Necesario cuando inicias sesión remotamente en máquina virtual de toohello.
   3. Escriba una contraseña en hello **nueva contraseña** campo y vuelva a escribirla en hello **Confirmar contraseña** campo. Esta contraseña es de hello cuenta de administrador.
   4. Seleccione Hola adecuado **suscripción**.
   5. Para hello **grupo de recursos**, haga clic en **crear nuevo** y escriba Hola nombre de un nuevo grupo de recursos. O bien, haga clic en **utilizar existente** y seleccione uno de los grupos de recursos disponibles Hola.
   6. Seleccione una ubicación donde reside Hola virtual machine, tales como **Ee.uu. Central sur**.
6. Haga clic en **Siguiente**.
7. Hola **tamaño de la imagen de máquina Virtual** hoja, seleccione **estándar A1** o cualquier otra imagen apropiada.
8. Haga clic en **Seleccionar**.

9. Hola **configuración** hoja, haga clic en **Aceptar**. Puede usar valores predeterminados de hello proporcionados por Azure.  
10. Hola **resumen** hoja, haga clic en **Aceptar**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely inicio de sesión en la máquina virtual de tooyour
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Virtual Machines (clásico)**. Si es necesario, haga clic en **más servicios** en esquina Hola inferior izquierda en categorías de servicio de Hola. Hola **máquinas virtuales (clásicas)** entrada aparece en hello **proceso** grupo.
3. Haga clic en el nombre de Hola de máquina virtual de Hola que desea toosign en.
4. Una vez iniciada la máquina virtual de hello, un menú en la parte superior de hello del panel de hello permite las conexiones.
5. Haga clic en **Conectar**.
6. Responder mensajes toohello como máquina virtual de toohello de tooconnect necesarios. Normalmente, se guardan o abren archivos .rdp de Hola que contiene los detalles de conexión de Hola. Podría tiene toocopy Hola dirección url: puerto como parte último hello de la primera línea del archivo .rdp de hello de Hola y pegarlos en una aplicación de inicio de sesión remota.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall un servidor de aplicaciones de Java en la máquina virtual
Puede copiar una máquina virtual de tooyour de servidor de la aplicación de Java, o puede instalar a un servidor de aplicaciones de Java a través de un instalador.

Este tutorial usa Tomcat como tooinstall de servidor de aplicaciones de Java de Hola.

1. Después de iniciar sesión en la máquina virtual de tooyour, abra una sesión de explorador demasiado[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Haga doble clic en el vínculo de Hola para **instalador del servicio de Windows de 32 bits o 64 bits**. Mediante esta técnica, Tomcat se instala como servicio de Windows.
3. Cuando se le solicite, elija el programa de instalación de toorun Hola.
4. Dentro de hello **el programa de instalación de Apache Tomcat** asistente, siga Hola solicita tooinstall Tomcat. Para fines de Hola de este tutorial, acepte las opciones predeterminadas de hello es correcto. Cuando llegue a hello **finalización Hola Asistente para la instalación de Apache Tomcat** cuadro de diálogo, puede comprobar si lo desea **ejecutar Apache Tomcat** toohave ahora el inicio de Tomcat. Haga clic en **finalizar** toocomplete Hola proceso de instalación de Tomcat.

## <a name="toostart-tomcat"></a>toostart Tomcat

Puede iniciar manualmente Tomcat, abra un símbolo del sistema en la máquina virtual y ejecutar el comando hello **net&nbsp;iniciar&nbsp;Tomcat8**.

Una vez que se está ejecutando Tomcat, puede tener acceso a Tomcat escribiendo la dirección URL de hello <http://localhost: 8080> en el Explorador de la máquina virtual Hola.

toosee Tomcat ejecutando desde equipos externos, necesita toocreate un punto de conexión y abrir un puerto.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate un extremo para la máquina virtual
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Virtual Machines (clásico)**.
3. Haga clic en el nombre de Hola de máquina virtual de Hola que está ejecutando el servidor de aplicaciones Java.
4. Haga clic en **Extremos**.
5. Haga clic en **Agregar**.
6. Hola **Agregar extremo** cuadro de diálogo:
   1. Especifique un nombre para el punto de conexión de hello; Por ejemplo, **HttpIn**.
   2. Seleccione **TCP** para el protocolo de saludo.
   3. Especifique **80** para puerto público Hola.
   4. Especifique **8080** para puerto privado Hola.
   5. Seleccione **deshabilitado** para hello flotante dirección IP.
   6. Deje la lista de control de acceso de hello tal cual.
   7. Haga clic en hello **Aceptar** botón cuadro de diálogo de tooclose hello y crear el punto de conexión de Hola.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen un puerto en firewall de hello para la máquina virtual
1. Inicie sesión en la máquina virtual de tooyour.
2. Haga clic en **Inicio de Windows**.
3. Haga clic en **Panel de control**.
4. Haga clic en **Sistema y seguridad**, **Firewall de Windows** y luego en **Configuración avanzada**.
5. Haga clic en **Reglas de entrada** y después en **Nueva regla**.  
   ![Nueva regla de entrada][NewIBRule]
6. Para hello **tipo de regla**, seleccione **puerto**y, a continuación, haga clic en **siguiente**.  
   ![Puerto de nueva regla de entrada][NewRulePort]
7. En hello **protocolo y puertos** pantalla, seleccione **TCP**, especifique **8080** como hello **puerto local específico**y, a continuación, haga clic en **Siguiente**.  
  ![Nueva regla de entrada][NewRuleProtocol]
8. En hello **acción** pantalla, seleccione **Permitir conexión hello**y, a continuación, haga clic en **siguiente**.
   ![Acción de nueva regla de entrada][NewRuleAction]
9. En hello **perfil** pantalla, asegúrese de que **dominio**, **privada**, y **público** están seleccionadas y, a continuación, haga clic en **siguiente** .
   ![Perfil de nueva regla de entrada][NewRuleProfile]
10. En hello **nombre** pantalla, especifique un nombre para la regla de hello, como **HttpIn** (nombre de la regla de Hola no es necesario toomatch Hola extremo nombre, sin embargo) y, a continuación, haga clic en **finalizar**.  
    ![Nombre de la nueva regla de entrada][NewRuleName]

En este momento, el sitio web de Tomcat debe ser visible desde un explorador externo. En la ventana de dirección del explorador de hello, escriba una dirección URL de formulario de hello  **http://*su\_DNS\_nombre*. cloudapp.net**, donde ***su\_DNS\_nombre*** es Hola nombre DNS que especificó cuando creó la máquina virtual de Hola.

## <a name="application-lifecycle-considerations"></a>Consideraciones acerca del ciclo de vida de las aplicaciones
* Puede crear su propio archivo de aplicación web (WAR) y agregar toohello **móviles** carpeta. Por ejemplo, cree un proyecto web dinámico de Java Service Page (JSP) básico y expórtelo como archivo WAR. A continuación, copie Hola WAR toohello Apache Tomcat **móviles** carpeta en la máquina virtual de hello, a continuación, ejecútelo en un explorador.
* De forma predeterminada cuando se instala el servicio Tomcat hello, establecerla toostart manualmente. Se puede cambiar lo toostart automáticamente mediante el complemento Servicios de Hola. Inicie el complemento Servicios de hello haciendo clic en **inicio de Windows**, **herramientas administrativas**y, a continuación, **Services**. Haga doble clic en hello **Apache Tomcat** de servicio y establezca **tipo de inicio** demasiado**automática**.

    ![Si se establece automáticamente un toostart de servicio][service_automatic_startup]

    Hello ventaja de tener Tomcat iniciar automáticamente es que empieza a ejecutarse cuando se reinicia la máquina virtual de hello (por ejemplo, después de que se instalan las actualizaciones de software que precisan un reinicio).

## <a name="next-steps"></a>Pasos siguientes
Puede obtener información acerca de otros servicios (por ejemplo, el almacenamiento de Azure, service bus y base de datos SQL) que tal vez desee tooinclude con las aplicaciones de Java. Ver información de hello disponible en hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
