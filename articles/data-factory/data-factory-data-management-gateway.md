---
title: "puerta de enlace de administración de factoría de datos aaaData | Documentos de Microsoft"
description: Configurar una puerta de enlace de datos toomove datos entre hello y local en la nube. Utilice Data Management Gateway en toomove Data Factory de Azure los datos.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Data Management Gateway
Hola Data management gateway es un agente de cliente que debe instalar en los datos de toocopy del entorno local entre los almacenes de datos en la nube y locales. Hola de datos locales almacenes compatibles con factoría de datos se muestran en hello [admite orígenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sección.

En este artículo complementa tutorial Hola Hola [mover datos entre local y nube almacenes de datos](data-factory-move-data-between-onprem-and-cloud.md) artículo. En el tutorial de hello, crear una canalización que utiliza datos de toomove de puerta de enlace de Hola de una base de datos de SQL Server local tooan blobs de Azure. Este artículo proporciona detallada información detallada acerca de la puerta de enlace de administración de datos de Hola. 

Puede escalar horizontalmente una puerta de enlace de administración de datos mediante la asociación de varios máquinas locales con puerta de enlace de Hola. Puede escalar verticalmente aumentando el número de trabajos de movimiento de datos que pueden ejecutarse simultáneamente en un nodo. Esta característica también está disponible para una puerta de enlace lógica con un único nodo. Consulte el artículo [Escalado en Data Management Gateway en Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para más información.

> [!NOTE]
> Actualmente, la puerta de enlace admite solo la actividad de copia de Hola y la actividad de procedimiento almacenado de factoría de datos. No es puerta de enlace de posibles toouse Hola una actividad personalizada tooaccess local orígenes de datos.      

## <a name="overview"></a>Información general
### <a name="capabilities-of-data-management-gateway"></a>Funcionalidades de Data Management Gateway
Puerta de enlace de administración de datos proporciona Hola siguientes capacidades:

* Modelo de orígenes de datos locales y los orígenes de datos en la nube dentro Hola misma factoría de datos y moverán los datos.
* Tener un solo panel de vidrio para la supervisión y administración con la visibilidad del estado de la puerta de enlace desde la página de la factoría de datos de Hola.
* Administrar orígenes de datos de access tooon local de forma segura.
  * Toocorporate firewall requiere ningún cambio. Puerta de enlace solo realiza conexiones basadas en HTTP salientes tooopen internet.
  * Cifrar las credenciales de los almacenes de datos locales con su certificado.
* Mover datos de manera eficaz: problemas de red toointermittent paralela y resistente con lógica de reintento automático de los datos se transfieren.

### <a name="command-flow-and-data-flow"></a>Flujo de comandos y flujo de datos
Al utilizar toocopy de actividad copiar datos entre local y en la nube, actividad hello usa datos tootransfer puerta de enlace de toocloud de origen de datos local y viceversa.

Este es flujo de datos de alto nivel hello y resumen de pasos para copiar con puerta de enlace de datos: ![flujo de datos mediante la puerta de enlace](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Desarrollador de datos crea una puerta de enlace de una factoría de datos de Azure mediante cualquier hello [portal de Azure](https://portal.azure.com) o [Cmdlet de PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).
2. Desarrollador de datos crea un servicio vinculado para un almacén de datos local mediante la especificación de puerta de enlace de Hola. Como parte de la configuración de hello servicio vinculado, el programador de datos utiliza las credenciales y tipos de autenticación de hello establecer credenciales aplicación toospecify.  cuadro de diálogo aplicación se comunica con los datos de Hola Hola establecer credenciales almacenar tootest hello y conexión de puerta de enlace toosave las credenciales.
3. Puerta de enlace cifra las credenciales de hello con certificado de hello asociado con la puerta de enlace de hello (proporcionado por el desarrollador de datos), antes de guardar las credenciales de hello en la nube de Hola.
4. Servicio de factoría de datos se comunica con la puerta de enlace de hello para la programación y administración de trabajos a través de un canal de control que utiliza una cola de bus de servicio compartido de Azure. Cuando un trabajo de copia de la actividad necesita toobe iniciado, factoría de datos se pone en cola con solicitud de hello junto con información de credenciales. Puerta de enlace inicia el trabajo de hello después de sondear la cola de Hola.
5. puerta de enlace de Hola descifra las credenciales de hello con hello mismo certificado y, a continuación, conecta a un almacén de datos local toohello con las credenciales y el tipo de autenticación correcta.
6. puerta de enlace de Hello copia los datos desde un almacenamiento de nube local tooa de almacén, o viceversa según cómo esté configurada Hola actividad de copia en la canalización de datos de Hola. Para este paso, puerta de enlace de Hola se comunica directamente con los servicios de almacenamiento en la nube como almacenamiento de blobs de Azure por un canal seguro (HTTPS).

### <a name="considerations-for-using-gateway"></a>Consideraciones a la hora de usar la puerta de enlace
* Se puede utilizar una sola instancia de Data Management Gateway para varios orígenes de datos locales. Sin embargo, **una instancia única de la puerta de enlace es un generador de datos de Azure relacionados tooonly** y no puede compartirse con otro generador de datos.
* **Solo puede haber una instancia de Data Management Gateway** instalada en un equipo. Imagine que tiene dos generadores de datos que necesitan tooaccess los orígenes de datos local, necesita puertas de enlace de tooinstall en equipos locales en dos. En otras palabras, una puerta de enlace es factoría de datos específica de tooa relacionados
* Hola **puerta de enlace no es necesario toobe en hello mismo equipo como origen de datos de hello**. Sin embargo, con el origen de datos de toohello más de cerca de puerta de enlace reduce el tiempo Hola Hola puerta de enlace tooconnect toohello origen de datos. Se recomienda que instale la puerta de enlace de hello en un equipo que es diferente de hello uno ese origen de datos de hosts local. Cuando el origen de datos y la puerta de enlace de hello están en equipos diferentes, puerta de enlace de hello no compiten por los recursos con el origen de datos.
* Puede tener **varias puertas de enlace en distintos equipos conectarse toohello mismo origen de datos local**. Por ejemplo, puede tener dos puertas de enlace que sirve al factorías de dos datos pero Hola mismo origen de datos local se registra con ambos factorías de datos Hola.
* Si ya tiene una puerta de enlace instalada en el equipo que atiende a un escenario de **Power BI**, instale una **puerta de enlace independiente para Azure Data Factory** en otra máquina.
* Debe usar la puerta de enlace, incluso cuando utilice **ExpressRoute**.
* Considere el origen de datos como uno de tipo local (que está detrás de un firewall), aunque utilice **ExpressRoute**. Usar la conectividad de tooestablish de puerta de enlace de hello entre el servicio de Hola y el origen de datos de Hola.
* Debe **usar puerta de enlace de hello** aunque Hola almacén de datos está en la nube de hello en un **VM de IaaS de Azure**.

## <a name="installation"></a>Instalación
### <a name="prerequisites"></a>Requisitos previos
* Hola admitida **sistema operativo** versiones son Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Instalación de data management gateway de hello en un controlador de dominio no se admite actualmente.
* Es necesario .NET Framework 4.5.1 o posterior. Si está instalando la puerta de enlace en una máquina con Windows 7, instale .NET Framework 4.5 o posterior. Consulte [Requisitos de sistema de .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) para más información.
* Hola recomendada **configuración** de máquina de puerta de enlace de hello es al menos 2 GHz, 4 núcleos, 8 GB de RAM y disco de 80 GB.
* Si el equipo host de hello hiberna, puerta de enlace de hello no responde toodata solicitudes. Por lo tanto, configure una adecuada **plan de energía** en equipo Hola antes de instalar la puerta de enlace de Hola. Si se utiliza una máquina de hello toohibernate configurado, instalación de puerta de enlace de hello pide un mensaje.
* Debe ser un administrador en hello máquina tooinstall y configurar correctamente la puerta de enlace de administración de datos de Hola. Puede agregar usuarios adicionales toohello **puerta de enlace de administración de datos a los usuarios** grupo local de Windows. los miembros de Hola de este grupo son toouse capaz de hello **Administrador de configuración de Data Management Gateway** puerta de enlace de herramienta tooconfigure Hola.

Como copiar conseguirlo ejecuciones de actividad en una frecuencia determinada, hello uso de recursos (CPU, memoria) en la máquina de hello también sigue Hola mismo patrón con las horas punta y tiempos de inactividad. Utilización de recursos también depende en gran medida cantidad Hola de datos que se mueven. Cuando hay varios trabajos de copia en curso, puede ver que el uso de los recursos aumenta durante las horas pico.

### <a name="installation-options"></a>Opciones de instalación
Puerta de enlace de administración de datos puede instalarse en hello siguientes maneras:

* Al descargar un paquete de instalación MSI de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Hola MSI también puede ser utilizados tooupgrade existente datos administración puerta de enlace toohello versión más reciente, con todas las opciones que se conservan.
* Haciendo clic en el vínculo **Descargar e instalar la puerta de enlace de datos** en INSTALACIÓN MANUAL o en la opción **Instalar directamente en este equipo** en CONFIGURACIÓN RÁPIDA. Consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener instrucciones detalladas sobre cómo usar la configuración rápida. paso manual Hola le toohello centro de descarga.  las instrucciones de Hola para descargar e instalar la puerta de enlace de Hola desde el centro de descarga están en la sección siguiente Hola.

### <a name="installation-best-practices"></a>Procedimientos recomendados de instalación:
1. Configurar el plan de energía en la máquina de host de Hola para puerta de enlace de Hola para que hello máquina no hibernación. Si el equipo host de hello hiberna, puerta de enlace de hello no responde toodata solicitudes.
2. Copia de seguridad asociado a la puerta de enlace de Hola de certificado de Hola.

### <a name="install-hello-gateway-from-download-center"></a>Instale la puerta de enlace de Hola desde el centro de descarga
1. Navegue demasiado[página de descarga de Microsoft Data Management Gateway](https://www.microsoft.com/download/details.aspx?id=39717).
2. Haga clic en **descargar**, seleccione Hola versión adecuada (**32-bit** vs. **64 bits**) y haga clic en **Siguiente**.
3. Ejecute hello **MSI** directamente o guárdelo en disco duro de tooyour y ejecutar.
4. En hello **bienvenida** página, seleccione un **lenguaje** haga clic en **siguiente**.
5. **Aceptar** Hola contrato de licencia de usuario final y haga clic en **siguiente**.
6. Seleccione **carpeta** tooinstall Hola puerta de enlace y haga clic en **siguiente**.
7. En hello **tooinstall listo** página, haga clic en **instalar**.
8. Haga clic en **finalizar** toocomplete instalación.
9. Obtener clave de Hola de hello portal de Azure. Vea la siguiente sección de Hola para obtener instrucciones paso a paso.
10. En hello **puerta de enlace de registro** página de **Administrador de configuración de Data Management Gateway** ejecutando en el equipo, Hola lo siguiente:
    1. Pegue la clave de hello en texto hello.
    2. Si lo desea, haga clic en **clave de puerta de enlace de mostrar** texto de la tecla toosee Hola.
    3. Haga clic en **Registrar**.

### <a name="register-gateway-using-key"></a>Registro de la puerta de enlace mediante una clave
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Si aún no ha creado una puerta de enlace lógico en el portal de Hola
una puerta de enlace de clave de hello portal y get hello de hello toocreate **configurar** página, siga los pasos del tutorial Hola [mover datos entre local y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Si ya ha creado la puerta de enlace lógica de Hola en el portal de Hola
1. En el portal de Azure, navegue toohello **factoría de datos** página y haga clic en **servicios vinculados** icono.

    ![Página Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Hola **servicios vinculados** página, seleccione Hola lógico **puerta de enlace** que creó en el portal de Hola.

    ![puerta de enlace lógica](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Hola **puerta de enlace de datos** página, haga clic en **descargar e instalar la puerta de enlace de datos**.

    ![Descargar vínculo en el portal de Hola](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Hola **configurar** página, haga clic en **vuelva a crear clave**. Haga clic en Sí en el mensaje de advertencia de hello después de leerlo detenidamente.

    ![Volver a crear clave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Haga clic en siguiente toohello tecla del botón Copiar. clave de Hello es copiada toohello Portapapeles.

    ![Copiar clave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Notificaciones/iconos de la bandeja del sistema
Hello imagen siguiente muestra algunas de hello iconos de la bandeja que se ven.

![Iconos de la bandeja del sistema](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Si mueve el cursor sobre el mensaje de notificación/icono de bandeja de sistema hello, puede ver detalles acerca del estado de Hola de operación de puerta de enlace o actualizar hello en una ventana emergente.

### <a name="ports-and-firewall"></a>Puertos y firewall
Hay dos firewalls necesita tooconsider: **firewall corporativo** ejecuta en hello enrutador central de la organización de hello, y **firewall de Windows** configurado como un demonio en el equipo local de Hola donde hello puerta de enlace está instalado.  

![Firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

En el nivel de firewall corporativo, debe configurar siguiente Hola dominios y los puertos de salida:

| Nombres de dominio | Puertos | Descripción |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Usado para la comunicación con el back-end del servicio de movimiento de datos |
| *.core.windows.net |443 |Usado para la copia de almacenamiento provisional que usa el blob de Azure (si está configurado)|
| *.frontend.clouddatahub.net |443 |Usado para la comunicación con el back-end del servicio de movimiento de datos |


En el nivel de Firewall de Windows, normalmente se habilitan estos puertos de salida. Si no es así, puede configurar dominios de Hola y puertos según corresponda en el equipo de puerta de enlace.

> [!NOTE]
> 1. En función de su origen / receptores, puede tener dominios adicionales toowhitelist y puertos de salida en el firewall corporativo/Windows.
> 2. Para algunas bases de datos en la nube (por ejemplo: [base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), deberá toowhitelist dirección IP de la máquina de puerta de enlace en su configuración de firewall.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Copiar datos desde un almacén de datos de origen datos almacén tooa receptor
Asegúrese de que las reglas de firewall de hello están habilitadas correctamente en el firewall corporativo hello, firewall de Windows en la máquina de puerta de enlace de hello, y del almacén de datos de hello propio. Al habilitar estas reglas permite Hola origen de puerta de enlace tooconnect tooboth y receptor correctamente. Habilitar reglas para cada almacén de datos que están implicados en la operación de copia de Hola.

Por ejemplo, toocopy de **un receptor de base de datos de SQL Azure local tooan de almacén de datos o un receptor de almacenamiento de datos de SQL Azure**, Hola lo siguiente:

* Permita la comunicación **TCP** saliente en el puerto **1433** para el Firewall de Windows y el corporativo.
* La configuración de firewall Hola de SQL Azure tooadd Hola dirección IP del servidor lista de toohello máquina Hola de puerta de enlace de direcciones IP permitidas.

> [!NOTE]
> Si el firewall no permite el puerto de salida 1433, la puerta de enlace no podrá tener acceso directamente a Azure SQL. En este caso, puede usar [copia provisionalmente](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL base de datos de Azure y almacenamiento de datos de SQL Azure. En este escenario, sólo requeriría HTTPS (puerto 443) para el movimiento de datos Hola.
>
>


### <a name="proxy-server-considerations"></a>Consideraciones acerca del servidor proxy
Si su entorno de red corporativa usa un proxy de servidor tooaccess Hola internet, configure la configuración de proxy apropiada de toouse de puerta de enlace de administración de datos. Puede establecer el proxy de Hola durante la fase de registro inicial de Hola.

![Configuración del proxy durante el registro](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Puerta de enlace usa el servicio de nube de hello proxy server tooconnect toohello. Haga clic en el vínculo **Cambiar** durante la configuración inicial. Vea hello **la configuración de proxy** cuadro de diálogo.

![Configuración del proxy mediante el Administrador de configuración](media/data-factory-data-management-gateway/SetProxySettings.png)

Hay tres opciones de configuración:

* **No utilice el proxy**: puerta de enlace no utiliza los servicios de proxy tooconnect toocloud explícitamente.
* **Utilice el proxy de sistema**: puerta de enlace utiliza la configuración que es configurado en diahost.exe.config y diawp.exe.config de proxy de Hola.  Si no hay ningún proxy está configurado en diahost.exe.config y diawp.exe.config, puerta de enlace conecta toocloud servicio directamente sin tener que pasar a través de proxy.
* **Usar proxy personalizado**: configurar Hola HTTP toouse de configuración de proxy para la puerta de enlace, en lugar de utilizar las configuraciones de diahost.exe.config y diawp.exe.config.  La dirección y el puerto son obligatorios.  El nombre de usuario y la contraseña son opcionales según la configuración de autenticación del proxy.  Todos los valores son cifrados con el certificado de credencial de Hola de puerta de enlace de Hola y almacenados localmente en el equipo de host de puerta de enlace de Hola.

puerta de enlace de administración de datos de Hello servicio de Host se reiniciará automáticamente después de guardar la configuración de proxy de hello actualizado.

Después de puerta de enlace se ha registrado correctamente, si desea que tooview o actualizar la configuración de proxy, use el Administrador de configuración de Data Management Gateway.

1. Inicie el **Administrador de configuración de Data Management Gateway**.
2. Cambiar toohello **configuración** ficha.
3. Haga clic en **cambio** vincular en **HTTP Proxy** Hola de sección toolaunch **establecer Proxy HTTP** cuadro de diálogo.  
4. Tras hacer clic en hello **siguiente** botón, verá un cuadro de diálogo de advertencia que pregunta para el permiso toosave Hola configuración del servidor proxy y reinicie el servicio de Host de puerta de enlace de Hola.

Puede ver y actualizar el proxy HTTP mediante la herramienta Administrador de configuración.

![Configuración del proxy mediante el Administrador de configuración](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Si configura un servidor proxy con la autenticación NTLM, servicio de Host de puerta de enlace se ejecuta bajo la cuenta de dominio de Hola. Si cambia Hola contraseña de cuenta de dominio de hello más tarde, recuerde tooupdate valores de configuración para el servicio de Hola y reiniciarlo en consecuencia. Pagar toothis requisito, se recomienda que usar un servidor proxy de dominio dedicada cuenta tooaccess Hola que no requiere la contraseña de hello tooupdate con frecuencia.
>
>

### <a name="configure-proxy-server-settings"></a>Configuración de un servidor proxy
Si selecciona **usar el proxy de sistema** establecer para el proxy HTTP de hello, puerta de enlace usa Hola configuración del proxy de diahost.exe.config y diawp.exe.config.  Si no se especifica ningún proxy en diahost.exe.config y diawp.exe.config, puerta de enlace conecta toocloud servicio directamente sin tener que pasar a través de proxy. Hello siguiente procedimiento proporciona instrucciones para actualizar el archivo de hello diahost.exe.config.  

1. En el Explorador de archivos, constituyen una copia de seguridad del C:\Program Files\Microsoft datos administración Gateway\2.0\Shared\diahost.exe.config tooback archivo original de hello.
2. Inicie Notepad.exe como administrador y abra el archivo de texto C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Buscar etiqueta predeterminada de Hola para system.net tal y como se muestra en el siguiente código de hello:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   A continuación, puede agregar detalles del servidor proxy como se muestra en el siguiente ejemplo de Hola:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Propiedades adicionales se permiten dentro de hello etiqueta toospecify Hola requerido configuración del proxy como scriptLocation. Consulte demasiado[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) acerca de la sintaxis.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Guarde el archivo de configuración de hello en ubicación original de hello, a continuación, reinicie el servicio de Host de puerta de enlace de administración de datos, que recoge el cambio de Hola Hola. servicio de Hola toorestart: usar servicios applet de panel de control de Hola o de hello **Administrador de configuración de Data Management Gateway** > haga clic en hello **detener el servicio** , a continuación, haga clic en hello **Iniciar el servicio**. Si no se inicia el servicio de hello, es probable que se ha agregado una sintaxis de etiqueta XML incorrecta en el archivo de configuración de aplicación Hola que se ha editado.

> [!IMPORTANT]
> No olvide tooupdate **ambos** diahost.exe.config y diawp.exe.config.  


Además puntos toothese, también necesitará toomake seguro de que Microsoft Azure está en la lista blanca de direcciones de su empresa. lista de Hola de direcciones IP de Microsoft Azure puede descargarse desde hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Posibles síntomas de problemas relacionados con el firewall y el servidor proxy
Si encuentra errores toohello similar los siguiendo, es probable debido tooimproper configuración de servidor hello proxy o firewall que bloquea la puerta de enlace de conexión tooauthenticate de fábrica de tooData propio. Consulte tooprevious sección tooensure el servidor proxy y firewall se han configurado correctamente.

1. Al tratar de puerta de enlace de tooregister hello, recibirá Hola siguiente error: "clave de puerta de enlace de error tooregister Hola. Antes de intentar clave de puerta de enlace de tooregister Hola de nuevo, confirme que hello data management gateway está en estado conectado y Hola servicio de Host de Data Management Gateway se ha iniciado."
2. Al abrir el Administrador de configuración, verá el estado Desconectado o Conectando. Al ver los registros de eventos de Windows, en "Visor de eventos" > "Registros de aplicaciones y servicios" > "Data Management Gateway", aparecen mensajes de error como Hola siguiente error:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Apertura del puerto 8050 para el cifrado de credenciales
Hola **establecer credenciales** aplicación usa Hola puerto de entrada **8050** servicio Hola portal de Azure vinculado de puerta de enlace de toorelay credenciales toohello al configurar una implementación local. Durante la instalación de puerta de enlace, de forma predeterminada, instalación de puerta de enlace de hello lo abre en la máquina de puerta de enlace de Hola.

Si estás usando un firewall de terceros, puede abrir manualmente el puerto de hello 8050. Si experimenta el problema de firewall durante la instalación de puerta de enlace, también puede intentar usar Hola después de puerta de enlace de comando tooinstall Hola sin configurar firewall de Hola.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Si decide no tooopen puerto hello 8050 en la máquina de puerta de enlace de hello, use mecanismos que no sea hello **establecer credenciales** credenciales de almacén de datos de tooconfigure de aplicación. Por ejemplo, puede usar el cmdlet de PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) . Consulte la sección [Configuración de credenciales y seguridad](#set-credentials-and-securityy) para más información sobre cómo configurar las credenciales del almacén de datos.

## <a name="update"></a>Actualizar
De forma predeterminada, la puerta de enlace de administración de datos se actualiza automáticamente cuando hay disponible una versión más reciente de puerta de enlace de Hola. puerta de enlace de Hello no se actualiza hasta que se realizan todas las tareas de hello programado. No hay otras tareas se procesan por puerta de enlace de hello hasta que se complete la operación de actualización de Hola. Si se produce un error en la actualización de hello, puerta de enlace se revierte toohello una versión antigua.

Consulte hora de la actualización de hello programado en hello siguientes lugares:

* página de propiedades de puerta de enlace de Hola Hola portal de Azure.
* Página principal del programa Hola a Administrador de configuración de Data Management Gateway
* En un mensaje de notificación de la bandeja del sistema

pestaña de inicio de Hola de hello Administrador de configuración de Data Management Gateway muestra la programación de actualización de Hola y puerta de enlace de hello última hora Hola se ha instalado o actualizar.

![Programar actualizaciones](media/data-factory-data-management-gateway/UpdateSection.png)

Puede instalar la actualización de hello inmediatamente o esperar toobe de puerta de enlace de hello actualizado automáticamente en el momento de hello programado. Por ejemplo, hello siguiente imagen muestra Hola se muestra en hello puerta de enlace de Configuration Manager junto con el botón de actualización de Hola que puede hacer clic en tooinstall se inmediatamente el mensaje de notificación.

![Actualización en el Administrador de configuración de Data Management Gateway](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

mensaje de notificación de Hello en bandeja del sistema Hola sería como se muestra en hello después de imagen:

![Mensaje de la bandeja del sistema](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Vea Estado Hola de operación de actualización en la bandeja del sistema hello (manual o automática). Al iniciar el Administrador de configuración de puerta de enlace próxima vez, verá un mensaje en la notificación de hello barra esa puerta de enlace de Hola se ha actualizado junto con un vínculo demasiado[¿qué es el nuevo tema](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>característica de toodisable/Habilitar actualización automática
Se puede deshabilitar/Habilitar característica de actualización automática de hello haciendo Hola pasos:

[Para puerta de enlace de nodo único]
1. Inicie Windows PowerShell en la máquina de puerta de enlace de Hola.
2. Cambie la carpeta C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript de toohello.
3. Hola ejecución después de comando tooturn Hola la actualización automática de características desactivar (deshabilitar).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn vuelve a activar:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Para puerta de enlace escalable y altamente disponible de varios nodos (versión preliminar)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Inicie Windows PowerShell en la máquina de puerta de enlace de Hola.
2. Cambie la carpeta C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript de toohello.
3. Hola ejecución después de comando tooturn Hola la actualización automática de características desactivar (deshabilitar).   

    Se requiere un parámetro AuthKey adicional para la característica de puerta de enlace con alta disponibilidad (versión preliminar).
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn vuelve a activar:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Si tiene acceso a portal de Hola desde un equipo que es diferente de la máquina de puerta de enlace de hello, debe asegurarse de que aplicación de administrador de credenciales de hello puede conectarse toohello máquina de puerta de enlace. Si la aplicación hello no puede llegar a la máquina de puerta de enlace de hello, no permite también tooset credenciales para el origen de datos de Hola y el origen de datos de tootest conexión toohello.  

Cuando usas hello **establecer credenciales** aplicación, portal de Hola cifra las credenciales de Hola con certificado de hello especificado en hello **certificado** ficha de hello **puerta de enlace Administrador de configuración de** en la máquina de puerta de enlace de Hola.

Si desea obtener un enfoque basado en la API para cifrar las credenciales de hello, puede usar hello [AzureRmDataFactoryEncryptValue nuevo](https://msdn.microsoft.com/library/mt603802.aspx) las credenciales de tooencrypt de cmdlet de PowerShell. Hola cmdlet utiliza esa puerta de enlace está configurado toouse tooencrypt Hola credenciales de certificado de Hola. Agregue las credenciales cifradas toohello **EncryptedCredential** elemento de hello **connectionString** Hola JSON. Usar hello JSON con hello [AzureRmDataFactoryLinkedService New](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet u Hola Editor de generador de datos.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Hay otro enfoque para establecer las credenciales mediante el Editor de la Factoría de datos. Si crea un servidor SQL Server vinculado servicio mediante el editor de Hola y escriba las credenciales en texto sin formato, las credenciales de Hola se cifran mediante un certificado que posee el servicio Data Factory de Hola. NO utiliza certificados de hello que esa puerta de enlace está configurado toouse. Aunque este enfoque puede resultar un poco más rápido, en algunos casos es menos seguro. Por lo tanto, se recomienda seguir este enfoque solo para fines de desarrollo y pruebas.

## <a name="powershell-cmdlets"></a>Cmdlets de PowerShell
Esta sección se describe cómo toocreate y registrar una puerta de enlace mediante cmdlets de PowerShell de Azure.

1. Inicie **Azure PowerShell** en modo de administrador.
2. Inicie sesión en tooyour cuenta de Azure mediante la ejecución de hello siguiente comando y escriba sus credenciales de Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Hola de uso **AzureRmDataFactoryGateway New** cmdlet toocreate una puerta de enlace lógico como sigue:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Ejemplo de comando y salida**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. En Azure PowerShell, cambie la carpeta toohello: **C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript\**. Ejecutar **RegisterGateway.ps1** asociado a la variable local de hello **$Key** tal y como se muestra en el siguiente comando de Hola. Este script registra el agente de cliente de hello instalado en su equipo con puerta de enlace de lógica Hola que crear anteriormente.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Puede registrar la puerta de enlace de hello en un equipo remoto mediante hello IsRegisterOnRemoteMachine parámetro. Ejemplo:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Puede usar hello **AzureRmDataFactoryGateway Get** lista de cmdlets tooget Hola de puertas de enlace de la factoría de datos. Cuando Hola **estado** muestra **en línea**, significa que la puerta de enlace es toouse listo.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Puede quitar una puerta de enlace con hello **Remove-AzureRmDataFactoryGateway** descripción de cmdlet y actualización de una puerta de enlace con hello **AzureRmDataFactoryGateway conjunto** cmdlets. Para ver la sintaxis y otros detalles de estos cmdlets, consulte la documentación de referencia de los cmdlets de Factoría de datos.  

### <a name="list-gateways-using-powershell"></a>Enumeración de puertas de enlace con PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Eliminación de puerta de enlace con PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Pasos siguientes
* Para más información, consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) . En el tutorial de hello, crear una canalización que utiliza datos de toomove de puerta de enlace de Hola de una base de datos de SQL Server local tooan blobs de Azure.  
