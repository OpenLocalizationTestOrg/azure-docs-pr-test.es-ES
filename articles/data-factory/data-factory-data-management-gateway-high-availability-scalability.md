---
title: disponibilidad de aaaHigh con data management gateway en Data Factory de Azure | Documentos de Microsoft
description: "Este artículo explica cómo puede escalar horizontalmente una puerta de enlace de administración de datos mediante la adición de más nodos y escalar verticalmente aumentando el número de trabajos simultáneos que se pueden ejecutar en un nodo."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Data Management Gateway - Alta disponibilidad y escalabilidad (versión preliminar)
Este artículo le ayuda a configurar una solución de alta disponibilidad y escalabilidad con Data Management Gateway.    

> [!NOTE]
> En este artículo se da por supuesto que ya está familiarizado con los conceptos básicos de Data Management Gateway. Para más información, consulte [Data Management Gateway](data-factory-data-management-gateway.md).

>**La versión preliminar de esta característica es compatible oficialmente con Data Management Gateway versión 2.12.xxxx.x y superior**. Asegúrese de que está utilizando la versión 2.12.xxxx.x o superior. Descargar la versión más reciente de Hola de Data Management Gateway [aquí](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Información general
Puede asociar las puertas de enlace de administración de datos que se instalan en varios equipos local con una sola puerta de enlace lógico desde el portal de Hola. Estos equipos se llaman **nodos**. Puede tener hasta demasiado**cuatro nodos** asociados con una puerta de enlace lógico. Hola ventajas de tener varios nodos (máquinas locales con la puerta de enlace instalada) para una puerta de enlace lógico son:  

- Mejorar el rendimiento del movimiento de datos entre los equipos locales y los almacenes de datos en la nube.  
- Si uno de los nodos de hello deja de funcionar por algún motivo, otros nodos siguen estando disponibles para mover datos de Hola. 
- Si uno de los nodos de hello necesita toobe desconectado por mantenimiento, otros nodos siguen estando disponibles para mover datos de Hola.

También puede configurar el número de Hola de **trabajos de movimiento de datos simultáneas** que puede ejecutar en un tooscale nodo la capacidad de Hola de mover datos entre local y nube almacenes de datos. 

Con hello portal de Azure, puede supervisar estado de Hola de esos nodos, que le ayudará a decidir si tooadd o quitar un nodo de puerta de enlace lógica de Hola. 

## <a name="architecture"></a>Arquitectura 
Hello diagrama siguiente proporciona información general de la arquitectura de Hola de escalabilidad y la característica de disponibilidad de hello Data Management Gateway: 

![Data Management Gateway - Alta disponibilidad y escalabilidad](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A **puerta de enlace lógico** es puerta de enlace de hello agregar factoría de datos de tooa Hola portal de Azure. Anteriormente, solo era posible asociar un único equipo de Windows local con Data Management Gateway instalado con una puerta de enlace lógica. Ese equipo de puerta de enlace local se llama nodo. Ahora, puede asociar una demasiado**cuatro nodos físicos** con una puerta de enlace lógico. Una puerta de enlace lógica con varios nodos se denomina **puerta de enlace multi-nodo**.  

Todos estos nodos están **activos**. Todas ellas pueden procesar datos de toomove de trabajos de movimiento de datos entre local y nube almacenes de datos. Uno de los nodos de hello actúe como distribuidor y de trabajo. Otros nodos de grupos de hello son nodos de trabajador. A **distribuidor** nodo extrae datos movimiento tareas y trabajos del servicio de nube de Hola y distribuye nodos tooworker (incluido él mismo). A **trabajo** nodo ejecuta datos de toomove de trabajos de movimiento de datos entre local y nube almacenes de datos. Todos los nodos son de trabajo. Únicamente un nodo puede ser a la vez distribuidor y nodo de trabajo.    

Normalmente, puede iniciar con un nodo y **escalar horizontalmente** tooadd más nodos como Hola nodos existentes se desborda con carga de movimiento de datos de Hola. También puede **escalar verticalmente** Hola capacidad de movimiento de datos de un nodo de puerta de enlace aumentando el número de Hola de trabajos simultáneos que se permiten toorun en el nodo de Hola. Esta funcionalidad también está disponible con una puerta de enlace de un único nodo (incluso cuando no está habilitada la característica de escalabilidad y disponibilidad de hello). 

Una puerta de enlace con varios nodos mantiene las credenciales del almacén de datos de hello sincronizados en todos los nodos. Si hay un problema de conectividad de nodo a nodo, las credenciales de hello pueden no estar sincronizadas. Al establecer las credenciales para un almacén de datos local que usa una puerta de enlace, guarda las credenciales en el nodo de distribuidor/trabajo Hola. Hola distribuidor nodo se sincroniza con otros nodos de trabajador. Este proceso se conoce como **credenciales sincronización**. Hola de canal de comunicación entre los nodos puede **cifrados** por un certificado público de SSL/TLS. 

## <a name="set-up-a-multi-node-gateway"></a>Configuración de una puerta de enlace de varios nodos
En esta sección se da por supuesto que ha realizado a través de hello siguiendo dos artículos o que están familiarizados con conceptos en los siguientes artículos: 

- [Data Management Gateway](data-factory-data-management-gateway.md) -ofrece una introducción detallada de puerta de enlace de Hola.
- [Movimiento de datos entre equipos locales y almacenes de datos en la nube](data-factory-move-data-between-onprem-and-cloud.md): contiene un tutorial con instrucciones paso a paso para usar una puerta de enlace con un único nodo.  

> [!NOTE]
> Antes de instalar una puerta de enlace de administración de datos en un equipo de Windows local, vea Requisitos previos descritos en [artículo principal de hello](data-factory-data-management-gateway.md#prerequisites).

1. Hola [tutorial](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), al crear una puerta de enlace lógico, habilitar hello **alta disponibilidad y escalabilidad** característica. 

    ![Data Management Gateway: habilitar alta disponibilidad y escalabilidad](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. Hola **configurar** , utilice cualquiera **el programa de instalación de Express** o **el programa de instalación Manual** vincular tooinstall una puerta de enlace en el primer nodo de hello (una máquina local de Windows).

    ![Data Management Gateway: instalación rápida o manual](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Si utiliza la opción de configuración rápida de hello, comunicación de nodo a nodo Hola se realiza sin cifrado. nombre de nodo de Hello es igual que el nombre de la máquina de Hola. Utilice el programa de instalación manual si comunicación de nodo a nodo Hola necesita toobe cifrado o si desea toospecify un nombre de nodo de su elección. Los nombres de nodo no se puede editar más adelante.
3. Si elige **instalación rápida**
    1. Vea Hola siguiente mensaje después de puerta de enlace de hello está instalado correctamente:

        ![Data Management Gateway: instalación rápida correcta](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Iniciar el Administrador de configuración de administración de datos para la puerta de enlace de Hola siguiendo [estas instrucciones](data-factory-data-management-gateway.md#configuration-manager). Vea el nombre de la puerta de enlace de hello, nombre de nodo, estado, etcetera.

        ![Data Management Gateway: instalación correcta](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Si elige **instalación manual**:
    1. Descargar paquete de instalación de Hola desde Microsoft Download Center hello, ejecute tooinstall puerta de enlace en el equipo.
    2. Hola de uso **clave de autenticación** de hello **configurar** puerta de enlace de página tooregister Hola.
    
        ![Data Management Gateway: instalación correcta](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. Hola **nuevo nodo de puerta de enlace** página, puede proporcionar un personalizado **nombre** toohello nodo de puerta de enlace. De forma predeterminada, el nombre de nodo es igual que el nombre de la máquina de Hola.    

        ![Data Management Gateway: especificar nombre](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. En la página siguiente de hello, puede elegir si demasiado**habilitar el cifrado para la comunicación de nodo a nodo**. Haga clic en **omitir** toodisable cifrado (valor predeterminado).

        ![Data Management Gateway: habilitar cifrado](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Solo se admite el cambio del modo de cifrado cuando se tiene un nodo de puerta de enlace único en la puerta de enlace lógica de Hola. modo de cifrado de hello toochange cuando una puerta de enlace tiene varios nodos, Hola lo siguiente: eliminar todos los nodos de hello excepto uno, cambiar el modo de cifrado de hello y, a continuación, agregar nodos de Hola de nuevo.
        > 
        > Consulte la sección [requisitos de los certificados TLS/SSL](#tlsssl-certificate-requirements) para obtener una lista de los requisitos para utilizar un certificado TLS/SSL. 
    5. Después de hello puerta de enlace se instala correctamente, haga clic en iniciar el Administrador de configuración:
    
        ![Instalación manual: iniciar Configuration Manager](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. consulte el Administrador de configuración de Data Management Gateway en el nodo hello (máquina de Windows local), que muestra el estado de conectividad, **nombre de puerta de enlace**, y **nombre de nodo**.  

        ![Data Management Gateway: instalación correcta](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Si va a aprovisionar la puerta de enlace de hello en una VM de Azure, puede usar [esta plantilla de administrador de recursos de Azure en GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Esta secuencia de comandos crea una puerta de enlace lógico, Establece las máquinas virtuales con software de Data Management Gateway instalado y éstos registra con puerta de enlace lógica de Hola. 
6. En el portal de Azure, inicie hello **puerta de enlace** página: 
    1. En página de inicio del generador de datos hello en el portal de hello, haga clic en **servicios vinculados**.
    
        ![Página principal de Factoría de datos](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Seleccione hello **puerta de enlace** toosee hello **puerta de enlace** página:
    
        ![Página principal de Factoría de datos](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Vea hello **puerta de enlace** página:   

        ![Puerta de enlace con la vista de un solo nodo](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Haga clic en **agregar nodo** en tooadd de barra de herramientas de hello una puerta de enlace de nodo toohello lógico. Si tiene previsto toouse el programa de instalación rápida, realice este paso de la máquina local de Hola que se agregará como una puerta de enlace de toohello del nodo. 

    ![Data Management Gateway: menú agregar nodo](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. Los pasos son similar toosetting primer nodo de Hola. Hola UI del Administrador de configuración permite establecer el nombre de nodo de hello si elige la opción de instalación manual de hello: 

    ![Configuration Manager: instalación de la segunda puerta de enlace](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Después de puerta de enlace de hello está instalado correctamente en el nodo de hello, herramienta de administrador de configuración de hello muestra hello después de pantalla:  

    ![Configuration Manager: instalación correcta de la segunda puerta de enlace](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Si abre hello **puerta de enlace** página en el portal de hello, verá dos nodos de puerta de enlace ahora: 

    ![Puerta de enlace con dos nodos en el portal de Hola](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete un nodo de puerta de enlace, haga clic en **eliminar nodo** en la barra de herramientas de hello, seleccione el nodo de Hola que desee toodelete y, a continuación, haga clic en **eliminar** de barra de herramientas de Hola. Esta acción elimina el nodo seleccionado Hola de grupo de Hola. Tenga en cuenta que esta acción no desinstala el software de puerta de enlace de administración de datos de Hola de nodo hello (máquina de Windows local). Use **agregar o quitar programas** en el Panel de Control en puerta de enlace de hello local toouninstall Hola. Cuando se desinstala la puerta de enlace de nodo de hello, se elimina automáticamente en el portal de Hola.   

## <a name="upgrade-an-existing-gateway"></a>Actualización de una puerta de enlace existente
Puede actualizar una existente puerta de enlace toouse Hola alta disponibilidad y la característica de escalabilidad. Esta característica solo funciona con nodos que tengan la puerta de enlace de hello datos administración de versión > = 2.12.xxxx. Puede ver versión de Hola de data management gateway instalado en una máquina de hello **ayuda** ficha del programa Hola a Administrador de configuración de Data Management Gateway. 

1. Actualizar la puerta de enlace de Hola Hola local machine toohello versión más reciente, siga por descargar y ejecutar un paquete de instalación MSI desde hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Consulte la sección [Instalación](data-factory-data-management-gateway.md#installation) para más información.  
2. Navegue toohello portal de Azure. Iniciar hello **página de la factoría de datos** de la factoría de datos. Haga clic en vinculado servicios mosaico toolaunch hello **página de servicios vinculados**. Seleccione Hola Hola de toolaunch de puerta de enlace **página puerta de enlace**. Haga clic en y habilitar **característica de vista previa** tal como se muestra en hello después de imagen: 

    ![Data Management Gateway: habilitar característica versión preliminar](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Una vez habilitada la característica de vista previa de hello en el portal de hello, cierre todas las páginas. Vuelva a abrir hello **página puerta de enlace** toosee Hola nueva vista previa interfaz de usuario (UI).
 
    ![Data Management Gateway: habilitación correcta de la característica versión preliminar](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Data Management Gateway: interfaz de usuario de la versión preliminar](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Durante la actualización de Hola, nombre del primer nodo de hello es nombre de Hola de máquina de Hola. 
3. Ahora, agregue un nodo. Hola **puerta de enlace** página, haga clic en **agregar nodo**.  

    ![Data Management Gateway: menú agregar nodo](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Siga las instrucciones de hello anterior sección tooset nodo Hola. 

### <a name="installation-best-practices"></a>Procedimientos recomendados de instalación

- Configurar el plan de energía en la máquina de host de Hola para puerta de enlace de Hola para que hello máquina no hibernación. Si el equipo host de hello hiberna, puerta de enlace de hello no responde toodata solicitudes.
- Copia de seguridad asociado a la puerta de enlace de Hola de certificado de Hola.
- Asegúrese de que todos los nodos son de una configuración similar (recomendada) para un rendimiento ideal. 
- Agregar al menos dos nodos tooensure alta disponibilidad.  

### <a name="tlsssl-certificate-requirements"></a>Requisitos del certificado TLS/SSL
Aquí son los requisitos de Hola de certificado TLS/SSL de Hola que se usa para proteger las comunicaciones entre los nodos de la puerta de enlace:

- certificado de Hello debe ser una confianza pública X509 certificado v3.
- Todos los nodos de la puerta de enlace deben confiar en este certificado. 
- Se recomienda que utilice certificados emitidos por una entidad de certificación pública (CA).
- Se admite cualquier tamaño de clave compatible con Windows Server 2012 R2 para los certificados SSL.
- No se admiten certificados que utilizan claves CNG.
- Se admiten certificados comodín. 


## <a name="monitor-a-multi-node-gateway"></a>Supervisión de una puerta de enlace de varios nodos
### <a name="multi-node-gateway-monitoring"></a>Supervisión de una puerta de enlace de varios nodos
Hola portal de Azure, puede ver la instantánea casi en tiempo real de la utilización de recursos (CPU, memoria, network(in/out), etc.) en cada nodo junto con los Estados de los nodos de puerta de enlace. 

![Data Management Gateway: supervisión de varios nodos](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

Puede habilitar **configuración avanzada** en hello **puerta de enlace** página toosee avanzada métricas como **red**(in/out), **rol e & stado de credencial**, que es útil para depurar problemas de puerta de enlace, y **trabajos simultáneos** (ejecutando / límite) que puede ser modificado / según corresponda cambió durante la optimización del rendimiento. Hello siguiente tabla proporcionan descripciones de las columnas de hello **nodos de puerta de enlace** lista:  

Propiedad de supervisión | Descripción
:------------------ | :---------- 
Nombre | Nombre de puerta de enlace lógica de Hola y nodos asociados a la puerta de enlace de Hola.  
Estado | Estado de la puerta de enlace lógica de Hola y nodos de puerta de enlace de Hola. Ejemplo: En línea, Sin conexión, Limitado, etc. Para obtener información acerca de estos estados, consulte la sección [Estado de la puerta de enlace](#gateway-status). 
Versión | Muestra la versión de Hola de puerta de enlace lógica de Hola y cada nodo de puerta de enlace. versión de Hola de puerta de enlace lógica de Hola se determina en función de la versión de la mayoría de los nodos de grupo de Hola. Si hay nodos con versiones diferentes en el programa de instalación de puerta de enlace lógico de hello, solo los nodos de hello con Hola mismo número de versión como función de la lógica de la puerta de enlace de hello correctamente. Otros están en modo limited hello y necesitan toobe actualizado manualmente (solo en caso de que se produce un error en la actualización automática). 
Memoria disponible | Memoria disponible en un nodo de la puerta de enlace. Este valor es una instantánea casi en tiempo real. 
Uso de CPU | Uso de CPU de un nodo de la puerta de enlace. Este valor es una instantánea casi en tiempo real. 
Redes (Entrada/Salida) | Uso de red de un nodo de la puerta de enlace. Este valor es una instantánea casi en tiempo real. 
Trabajos simultáneos (En ejecución / Límite) | Número de trabajos o tareas que se ejecutan en cada nodo. Este valor es una instantánea casi en tiempo real. Límite significa Hola máxima simultáneas de trabajos para cada nodo. Este valor se define basándose en el tamaño de la máquina de Hola. Puede aumentar Hola límite tooscale la ejecución de trabajo simultáneas en escenarios avanzados, donde CPU / memoria / red es en exceso, pero las actividades se agote. Esta funcionalidad también está disponible con una puerta de enlace de un único nodo (incluso cuando no está habilitada la característica de escalabilidad y disponibilidad de hello). Para más información, consulte la sección [Consideraciones para el escalado](#scale-considerations). 
Rol | Hay dos tipos de roles: distribuidor y de trabajo. Todos los nodos son trabajadores, lo que significa que todos ellos pueden tener trabajos tooexecute usado. Hay solo un nodo de distribuidor, que es usado toopull tareas y trabajos de servicios en la nube y enviarlos toodifferent nodos de trabajador (incluido él mismo). 

![Data Management Gateway: supervisión avanzada de varios nodos](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Estado de la puerta de enlace

Hello tabla siguiente proporciona los Estados posibles de un **nodo de puerta de enlace**: 

Estado  | Comentarios/Escenarios
:------- | :------------------
En línea | Conectado el nodo del servicio de factoría de tooData.
Sin conexión | El nodo está sin conexión.
Actualizando | nodo de Hola se va a actualizar automáticamente.
Limitado | Pagar tooConnectivity problema. Puede ser debido a la emisión de puerto 8050 tooHTTP, problema de conectividad del bus de servicio o problema de sincronización de credenciales. 
Inactivo | Nodo se encuentra en una configuración diferente de la configuración de Hola de otros nodos de mayoría.<br/><br/> Un nodo puede estar inactivo cuando no puede conectarse tooother nodos. 


Hello tabla siguiente proporciona los Estados posibles de un **puerta de enlace lógico**. estado de la puerta de enlace de Hello depende de Estados de nodos de la puerta de enlace de Hola. 

Estado | Comentarios
:----- | :-------
Debe registrarse | Ningún nodo aún está registrado toothis lógico puerta de enlace
En línea | Los nodos de la puerta de enlace están en línea
Sin conexión | Ningún nodo está en línea.
Limitado | No todos los nodos de la puerta de enlace están en buen estado. Este estado es una advertencia de que alguno de los nodos podría estar inactivo. <br/><br/>Puede ser debido a toocredential problema de sincronización en el nodo de distribuidor o de trabajo. 

### <a name="pipeline-activities-monitoring"></a>Supervisión de canalización y actividades
Hola portal de Azure proporciona una canalización de supervisión con detalles de nivel de nodo específico. Por ejemplo, muestra las actividades que se ejecutaron en cada nodo. Esta información puede ser útil para comprender los problemas de rendimiento en un nodo determinado, digamos debido a la limitación de toonetwork. 

![Data Management Gateway: supervisión de varios nodos para canalizaciones](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Data Management Gateway: detalles de canalización](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Consideraciones de escala

### <a name="scale-out"></a>Escalado horizontal
Cuando Hola **memoria disponible sea baja** hello y **el uso de CPU es alto**, agregar un nuevo nodo ayuda a escalar horizontalmente la carga de hello en los equipos. Si se producen errores en las actividades de vencimiento nodo tootime horizontal o puerta de enlace está sin conexión, será útil si agrega una puerta de enlace de toohello del nodo.
 
### <a name="scale-up"></a>Escalado vertical
Cuando Hola disponible memoria y CPU no se utilizan también, pero la capacidad inactiva hello es 0, se debe escalar verticalmente aumentando el número de Hola de trabajos simultáneos que se pueden ejecutar en un nodo. También puede que desee tooscale seguridad cuando las actividades se agota el tiempo porque la puerta de enlace de hello está sobrecargado. Como se muestra en hello después de la imagen, puede aumentar la capacidad máxima de Hola para un nodo. Se recomienda duplicándolo toostart con.  

![Data Management Gateway: consideraciones de escala](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Problemas conocidos y cambios relevantes

- Actualmente, puede tener hasta toofour nodos de puerta de enlace física para una sola puerta de enlace lógico. Si tiene más de cuatro nodos por motivos de rendimiento, envíe un correo electrónico demasiado[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Volver a no se puede registrar un nodo de puerta de enlace con la clave de autenticación de Hola desde otro tooswitch de lógica de la puerta de enlace de puerta de enlace lógico Hola actual. toore el registro, desinstale la puerta de enlace de Hola de nodo de hello, reinstalar la puerta de enlace de Hola y registrarlo con clave de autenticación de Hola para hello otra puerta de enlace lógico. 
- Si se requiere el proxy HTTP para todos los nodos de puerta de enlace, configurar servidor proxy de hello en diahost.exe.config y diawp.exe.config y use Hola server manager toomake seguro ha Hola a todos los nodos del mismo diahost.exe.config y diawip.exe.config. Consulte la sección [configurar el proxy](data-factory-data-management-gateway.md#configure-proxy-server-settings) para más información. 
- toochange el modo de cifrado para la comunicación de nodo a nodo en el Administrador de configuración de puerta de enlace, elimine todos los nodos de hello en el portal de hello excepto uno. A continuación, agregar nodos al cambiar el modo de cifrado de Hola.
- Usar un certificado SSL oficial si opta por canal de comunicación de nodo a nodo hello tooencrypt. Certificado autofirmado puede provocar problemas de conectividad como Hola mismo certificado no puede ser de confianza en la lista de entidad de certificación en otros equipos. 
- No se puede registrar una puerta de enlace lógico de la tooa del nodo puerta de enlace cuando la versión del nodo hello es anterior a la versión de la lógica de la puerta de enlace de Hola. Eliminar todos los nodos de puerta de enlace lógica de Hola desde portal para que pueda registrar un node(downgrade) versión menor. Si elimina todos los nodos de una puerta de enlace lógico, instalar y registrar manualmente nuevos nodos toothat lógico puerta de enlace. La instalación rápida no se admite en este caso.
- No se puede usar el programa de instalación rápida tooinstall nodos tooan lógico puerta de enlace existente, que todavía se está usando credenciales de la nube. Puede comprobar donde se almacenan las credenciales de Hola de hello Administrador de configuración de puerta de enlace en la ficha de configuración de Hola.
- No se puede usar el programa de instalación rápida tooinstall nodos tooan lógico puerta de enlace existente, que tiene habilitado el cifrado de nodo a nodo. Como establecer el modo de cifrado de hello implica agregar manualmente los certificados, instalación de express es no hay más de una opción. 
- Para la copia de archivos desde el entorno local, no debe usar \\localhost o C:\archivos puesto que localhost o la unidad local podrían no ser accesibles en todos los nodos. En su lugar, use \\ubicación de los archivos ServerName\files toospecify.


## <a name="rolling-back-from-hello-preview"></a>Reversión de vista previa de Hola 
tooroll de vista previa de hello, elimine todos los nodos pero un nodo. No importa qué nodos, eliminar, pero asegúrese de que tener al menos un nodo de puerta de enlace lógica de Hola. Puede eliminar un nodo mediante la desinstalación de puerta de enlace en la máquina de Hola o mediante el uso de hello portal de Azure. En el portal de Azure, en Hola Hola **factoría de datos** página, haga clic en Hola de vinculado servicios toolaunch **servicios vinculados** página. Seleccione Hola Hola de toolaunch de puerta de enlace **puerta de enlace** página. En la página de la puerta de enlace de hello, puede ver nodos Hola asociados a la puerta de enlace de Hola. Hola página permite eliminar un nodo de puerta de enlace de Hola.
 
Después de eliminar, haga clic en **características de vista previa** Hola la misma página de portal de Azure y deshabilitar la característica de vista previa de Hola. Restablecimiento de la puerta de enlace puerta de enlace tooone nodo GA (disponibilidad general).


## <a name="next-steps"></a>Pasos siguientes
Revisar Hola siguientes artículos:
- [Data Management Gateway](data-factory-data-management-gateway.md) -ofrece una introducción detallada de puerta de enlace de Hola.
- [Movimiento de datos entre equipos locales y almacenes de datos en la nube](data-factory-move-data-between-onprem-and-cloud.md): contiene un tutorial con instrucciones paso a paso para usar una puerta de enlace con un único nodo. 
