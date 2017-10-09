---
title: "aaaGet se inició con la integración de registros de Azure | Documentos de Microsoft"
description: "Conozca cómo tooinstall hello Azure iniciar servicio de integración e integrar los registros de almacenamiento de Azure, los registros de auditoría de Azure y las alertas del centro de seguridad de Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Azure Log Integration en registros de Diagnósticos de Azure y reenvío de eventos de Windows
Integración de registro de Azure (AzLog) le permite toointegrate sin procesar registros de los recursos de Azure en los sistemas de administración de eventos (SIEM) e información de seguridad local. Esta integración hace posible toohave un panel seguridad unificada para todos sus activos, local o en la nube de hello, por lo que puede agregar, correlacionar, analizar y alertas para los eventos de seguridad relacionados con las aplicaciones.
>[!NOTE]
Para obtener más información sobre la integración de registro de Azure, puede revisar hello [descripción de la integración de Azure registro](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

En este artículo le ayudará a empezar con la integración de registro de Azure al centrarse en las instalaciones de Hola de hello Azlog servicio e integrar servicios de hello con diagnósticos de Azure. Hola servicio de integración de registro de Azure, a continuación, será capaz de toocollect información de registro de eventos de Windows de Hola canal de eventos de seguridad de Windows desde máquinas virtuales implementadas en IaaS de Azure. Esto es muy similar demasiado "Reenvío de eventos" que ha usado en local.

>[!NOTE]
>salida de hello toobring Hola de capacidad de integración de registros de Azure en toohello Hola SIEM propio proporciona SIEM. Consulte el artículo de hello [integrar Azure registro integración con SIEM local](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) para obtener más información.

toobe muy claro - Hola servicio de integración de registro de Azure se ejecuta en un equipo físico o virtual que está usando Hola Windows Server 2008 R2 o una versión posterior del sistema operativo (Windows Server 2012 R2 o Windows Server 2016 se prefieren).

equipo físico de Hello puede ejecutar de forma local (o en un sitio de proveedor de hospedaje). Si decide que el servicio de integración de Azure registro de hello toorun en una máquina virtual, que la máquina virtual puede ubicarse localmente o en una nube pública, como Microsoft Azure.

Hola físico o máquina virtual que ejecuta el servicio de integración de Azure registro de hello requiere conectividad de red toohello nube pública de Azure. Pasos de este artículo proporcionan detalles acerca de la configuración de Hola.

## <a name="prerequisites"></a>Requisitos previos
Como mínimo, la instalación de Hola de AzLog necesario Hola siguientes elementos:
* Una **suscripción de Azure**. Si no tiene, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).
* A **cuenta de almacenamiento** que se puede utilizar para el registro de diagnóstico de Windows Azure (puede usar una cuenta de almacenamiento configurado previamente, o crear uno nuevo, se le mostrará cómo tooconfigure Hola cuenta de almacenamiento más adelante en este artículo)
  >[!NOTE]
  Puede que no sea necesaria una cuenta de almacenamiento en función del escenario. Para hello escenario de diagnósticos de Azure se describen en este artículo se necesita uno.
* **Dos sistemas**: una máquina que se ejecutará el servicio de integración de Azure registro de hello y una máquina que se van a supervisar y tienen su información de registro que se envía el equipo del servicio de toohello Azlog.
   * Un equipo que desea toomonitor: se trata de una máquina virtual que se ejecuta como un [Máquina Virtual de Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Una máquina que se ejecutará el servicio de integración de Azure registro de hello; esta máquina recopilará información de registro de hello todos los que más adelante se importará en su SIEM.
    * Este sistema puede encontrarse en un entorno local o en Microsoft Azure.  
    * Necesita toobe ejecuta un x64 versión de Windows server 2008 R2 SP1 o posterior y tener .NET 4.5.1 instalado. Puede determinar la versión de .NET de hello instalado por el siguiente artículo de hello titulado [Cómo: determinar qué .NET Framework versiones están instaladas](https://msdn.microsoft.com/library/hh925568)  
    Debe tener conectividad toohello cuenta de almacenamiento Azure utiliza para el registro de diagnóstico de Azure. Se proporcionarán instrucciones más adelante en este artículo sobre cómo puede confirmar esta conectividad.

Para ver una demostración rápida del proceso de Hola de creación de una máquina virtual mediante el portal de Azure Hola Eche un vistazo en hello vídeo a continuación.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Consideraciones de la implementación
Mientras se está probando la integración de registro de Azure, puede usar cualquier sistema que cumpla los requisitos mínimos del sistema operativo de Hola. Sin embargo, para un saludo del entorno de producción carga puede requerir tooplan para ajustar la escala vertical u horizontalmente.

Puede ejecutar varias instancias del servicio de integración de Azure registro de hello (una instancia por máquina física o virtual) si el volumen de eventos es alto. Además, puede equilibrar la carga cuentas de almacenamiento de diagnósticos de Azure para Windows (WAD) y el número de Hola de instancias de toohello tooprovide de suscripciones deben basarse en su capacidad.
>[!NOTE]
En este momento tenemos no recomendaciones específicas para cuando tooscale instancias de Azure iniciar máquinas de integración (es decir, las máquinas que se ejecutan el servicio de integración de Azure registro de hello), o para las cuentas de almacenamiento o suscripciones. Las decisiones de escalado deben basarse en las observaciones del rendimiento en cada una de estas áreas.

También tiene Hola opción tooscale seguridad toohelp de servicio de integración de Azure registro de hello mejorar el rendimiento. Hola siguientes métricas de rendimiento puede ayudarle a ajustar el tamaño de máquinas de Hola que elegir servicio de integración de toorun Hola registros de Azure:
* En una máquina con 8 procesadores (núcleos), una instancia única de Azlog Integrator puede procesar aproximadamente 24 millones de eventos por día (~1M/hora).

* En una máquina con 4 procesadores (núcleos), una instancia única de Azlog Integrator puede procesar aproximadamente 1,5 millones de eventos por día (~62 500/hora).

## <a name="install-azure-log-integration"></a>Instalación de la integración de registro de Azure
tooinstall integración de registro de Azure, necesita hello toodownload [integración de Azure log](https://www.microsoft.com/download/details.aspx?id=53324) archivo de instalación. Ejecutar procesos a través de la rutina de instalación de Hola y decida si desea que tooMicrosoft de información de telemetría de tooprovide.  

![Pantalla de instalación con la casilla de telemetría activada](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Le recomendamos que permita a los datos de telemetría de toocollect de Microsoft. Puede desactivar la recopilación de datos de telemetría si quita la marca de esta opción.
>


Hola servicio de integración de registro de Azure recopila los datos de telemetría de máquina de hello en el que está instalado.  

Los datos de telemetría recopilados son:

* Excepciones que se producen durante la ejecución de la integración de registro de Azure.
* Estadísticas sobre el número de Hola de eventos procesados y consultas
* Estadísticas sobre cuáles son las opciones de la línea de comandos de Azlog.exe que se usan.

se explica el proceso de instalación de Hola Hola vídeo a continuación.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Pasos posteriores a la instalación y validación
Después de completar la rutina de configuración básica de hello, está listo paso tooperform pasos posteriores a la instalación y validación:
1. Abra una ventana de PowerShell con privilegios elevados y vaya demasiado**c:\Program Files\Microsoft Azure registro integración**
2. Hola primero necesita tootake consiste hello tooget que azlog Cmdlets importado. Puede hacerlo mediante la ejecución de script de Hola **LoadAzlogModule.ps1** (aviso Hola ". \" en el siguiente comando de hello). Escriba **.\LoadAzlogModule.ps1** y presione **ENTRAR**.  
Debería ver algo parecido a lo que aparece en la siguiente ilustración de Hola. </br></br>
![Pantalla de instalación con la casilla de telemetría activada](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Ahora debe tooconfigure AzLog toouse un entorno de Azure específico. Un "entorno de Azure" es Hola "type" del centro de datos de nube de Azure que desee toowork con. Aunque hay varios entornos de Azure en este momento, opciones actualmente relevantes de hello son **nube de Azure** o **AzureUSGovernment**.   En el entorno de PowerShell con privilegios elevados, asegúrese de que se encuentra en **C:\Archivos de programa\Microsoft Azure Log Integration\**. </br></br>
    Una vez allí, ejecute el comando de hello: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (para anuncios de Azure)

      >[!NOTE]
      Comando de Hola se ejecuta correctamente, no recibirá ningún tipo de información.  Si desea que la nube de Azure de US Government hello toouse, usaría **AzureUSGovernment** (para Hola - variable de nombre) para hello nube del gobierno de Estados Unidos. No se admiten otras nubes de Azure en este momento.  
4. Para poder supervisar un sistema necesitará Hola nombre de cuenta de almacenamiento de hello en uso para diagnósticos de Azure.  Hola portal de Azure vaya demasiado**máquinas virtuales** y busque la máquina virtual de Hola que va a supervisar. Hola **propiedades** sección, elija **configuración de diagnóstico**.  Haga clic en **agente** y tome nota del nombre de cuenta de almacenamiento Hola especificado. Necesitará este nombre de cuenta para un paso posterior.
![Configuración de diagnóstico de Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Configuración de diagnóstico de Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Si no se habilitó la supervisión durante la creación de la máquina virtual se le ofrecerá Hola opción tooenable, como se indicó anteriormente.
5. Ahora se tendrá que cambiar nuestro toohello atrás de atención máquina de integración de registros de Azure. Necesitamos tooverify que haya conectividad toohello cuenta de almacenamiento del sistema de Hola donde instaló la integración de registro de Azure. equipo físico de Hola o máquina virtual que ejecuta la integración de Azure registro de servicio necesita tener acceso a toohello almacenamiento cuenta tooretrieve información registrada por diagnósticos de Azure según la configuración de cada uno de Hola Hola supervisan sistemas.  
  1. Puede descargar el explorador de Azure Storage [aquí](http://storageexplorer.com/).
  2. Ejecutar procesos a través de la rutina de instalación de Hola
  3. Cuando completa la instalación de hello haga clic en **siguiente** y deje la casilla de verificación de hello **iniciar Microsoft Azure Storage Explorer** activada.  
  4. Inicie sesión en tooAzure.
  5. Compruebe que puede ver la cuenta de almacenamiento de Hola que ha configurado para diagnósticos de Azure.  
![Cuentas de almacenamiento](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Observe que hay unas cuantas opciones en las cuentas de almacenamiento. Una de ellas es **Tablas**. En **Tablas** debería ver una denominada **WADWindowsEventLogsTable**. </br></br>
   ![Cuentas de almacenamiento](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Integración de registros de Diagnósticos de Azure
En este paso, configurará máquina Hola ejecutando hello Azure registro integración tooconnect toohello almacenamiento cuenta de servicio que contiene los archivos de registro de hello.
toocomplete este paso tendrá algunas cosas por adelantado.  
* **FriendlyNameForSource:** se trata de un nombre descriptivo que se puede aplicar toohello cuenta de almacenamiento que ha configurado toostore información de máquina virtual de hello diagnósticos de Azure
* **StorageAccountName:** trata Hola nombre de cuenta de almacenamiento de Hola que especificó cuando configuró diagnotics de Azure.  
* **StorageKey:** trata de clave de almacenamiento de Hola Hola cuenta de almacenamiento donde se almacena la información de diagnóstico de Azure de Hola para esta máquina virtual.  

Lleve a cabo Hola después de la clave de almacenamiento de hello tooobtain de pasos:
 1. Examinar toohello [portal de Azure](http://portal.azure.com).
 2. En el panel de navegación de Hola de hello Azure de la consola, desplácese toohello inferior y haga clic en **más servicios.**

 ![Más servicios](./media/security-azure-log-integration-get-started/more-services.png)
 3. Escriba **almacenamiento** en hello **filtro** cuadro de texto. Haga clic en **Cuentas de almacenamiento** (esta opción aparecerá después de escribir **Almacenamiento**).

   ![Cuadro Filtrar](./media/security-azure-log-integration-get-started/filter.png)
 4. Aparecerá una lista de cuentas de almacenamiento, haga doble clic en la cuenta de hello que asigna almacenamiento tooLog.

   ![lista de cuentas de almacenamiento](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Haga clic en **las claves de acceso** en hello **configuración** sección.

  ![Claves de acceso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Copia **key1** y colóquelo en una ubicación segura que puede tener acceso para el paso siguiente de saludo.

   ![dos claves de acceso](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. En el servidor de Hola que instaló integración del registro de Azure, abra un símbolo del sistema con privilegios elevados (tenga en cuenta que estamos utilizando una ventana de símbolo del sistema con privilegios elevados aquí, no una consola de PowerShell con privilegios elevados).
 8. Navegue demasiado**c:\Program Files\Microsoft Azure registro integración**
 9. Ejecute ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> Por ejemplo ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` si desea que tooshow de Id. de suscripción de hello seguridad en XML de eventos de hello, anexar nombre descriptivo de hello suscripción ID toohello: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` o, por ejemplo,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Esperar hasta too60 minutos, a continuación, ver los eventos de Hola que se haya extraído de la cuenta de almacenamiento de Hola. tooview, abra **Visor de eventos > registros de Windows > eventos reenviados** en hello Azlog Integrator.

Aquí puede ver un vídeo a través de pasos de hello explicado anteriormente.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>¿Qué ocurre si datos no aparecen en carpeta de eventos reenviados Hola?
Si después de una hora datos no aparecen en hello **eventos reenviados** carpeta, a continuación:

1. Compruebe el servicio de integración de Azure registro de hello máquina ejecución hello y confirme que puede tener acceso a Azure. tootest conectividad, intente tooopen hello [portal de Azure](http://portal.azure.com) desde el Explorador de Hola.
2. Asegúrese de que cuenta de usuario de hello **Azlog** tiene permiso de escritura en la carpeta de hello **users\Azlog**.
  <ol type="a">
   <li>Abra el **Explorador de Windows** .</li>
  <li> Navegue demasiado**c:\users** </li>
  <li> Haga clic con el botón derecho en **c:\users\Azlog** .</li>
  <li> Haga clic en **Seguridad**  .</li>
  <li> Haga clic en **Service\Azlog NT** y comprobar los permisos de hello para la cuenta de hello. Si no está presente en esta pestaña cuenta de Hola o si los permisos adecuados de hello no son actualmente muestran qué puede conceder derechos de la cuenta de hello en esta pestaña.</li>
  </ol>
3.Cuenta de almacenamiento seguro Hola agregan en comando hello **agregar origen de Azlog** aparece al ejecutar el comando de hello **lista de orígenes de Azlog**.
4. Vaya demasiado**Visor de eventos > registros de Windows > aplicación** toosee si hay algún error registrado en la integración de Azure registro de hello.


Si surge algún problema durante la instalación de Hola y configuración, abra una [solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md), seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.

Otra opción de compatibilidad es hello [foro de MSDN de integración de Azure registro](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Aquí Comunidad Hola puede admitir entre sí con preguntas, respuestas, consejos y sugerencias sobre cómo tooget más Hola de integración de registro de Azure. Además, el equipo de integración de registro de Azure de hello supervisa este foro y le ayudará a cada vez que se puede.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la integración de registro de Azure, vea Hola siguientes documentos:

* [Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Integración de registros de Microsoft Azure para registros de Azure): Centro de descarga para obtener información, los requisitos del sistema y las instrucciones de instalación de la integración de registros de Azure.
* [Integración de registro de introducción tooAzure](security-azure-log-integration-overview.md) : este documento presenta la integración de registro tooAzure, sus capacidades claves y su funcionamiento.
* [Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : esta entrada de blog muestra cómo tooconfigure Azure registro toowork integración con soluciones de socios Splunk y ArcSight de HP, IBM QRadar. Se trata de nuestro Consejo actual en cómo tooconfigure Hola componentes SIEM. Primero póngase en contacto con el proveedor de SIEM para obtener más detalles.
* [Preguntas más frecuentes sobre la integración de registro de Azure (P+F)](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre la integración de registro de Azure.
* [Integración de centro de seguridad de integración de registro de alertas con Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) : este documento muestra cómo las alertas toosync centro de seguridad, junto con los eventos de seguridad de máquina virtual recopilados por diagnósticos de Azure y registros de actividad de Azure, con los análisis de registros o una solución SIEM.
* [Nuevas características de diagnóstico de Azure y los registros de auditoría de Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : esta entrada de blog presenta tooAzure los registros de auditoría y otras características que le ayudarán a obtienen información sobre las operaciones de Hola de los recursos de Azure.
