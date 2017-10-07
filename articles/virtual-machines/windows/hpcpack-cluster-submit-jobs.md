---
title: "clúster de aaaSubmit trabajos tooan HPC Pack en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset seguridad un toosubmit del equipo local trabajos tooan de clúster de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Enviar trabajos HPC desde un clúster de HPC Pack de tooan de equipo local implementado en Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configurar un tooa local cliente equipo toosubmit trabajos [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) clúster en Azure. Este artículo muestra cómo tooset un equipo local con cliente de herramientas toosubmit trabajo sobre clúster de toohello HTTPS en Azure. De esta forma, varios usuarios de clúster pueden enviar trabajos tooa basada en la nube clúster de HPC Pack, pero sin conexión directa toohello VM del nodo principal o tiene acceso a una suscripción de Azure.

![Enviar un clúster de tooa de trabajo en Azure][jobsubmit]

## <a name="prerequisites"></a>Requisitos previos
* **Nodo principal de HPC Pack implementado en una máquina virtual de Azure** -le recomendamos que use herramientas automatizadas, como un [plantilla de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) o un [script de PowerShell de Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nodo principal de toodeploy hello y clúster. Necesita el nombre DNS de hello del nodo principal de Hola y las credenciales de Hola de un administrador de clústeres para completar los pasos de hello en este artículo.
* **Equipo cliente**: se necesita un equipo cliente con Windows o Windows Server que pueda ejecutar utilidades de cliente de HPC Pack (consulte los [requisitos del sistema](https://technet.microsoft.com/library/dn535781.aspx)). Si solo desea portal web de toouse Hola HPC Pack o trabajos de toosubmit de API de REST, puede usar todos los equipos cliente de su elección.
* **Medios de instalación de HPC Pack** -tooinstall Hola utilidades de cliente de HPC Pack, paquete de instalación gratuito de hello para la versión más reciente de HPC Pack (HPC Pack 2012 R2) está disponible en la [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Asegúrese de que descargue Hola misma versión de HPC Pack que está instalado en la máquina virtual del nodo principal Hola.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Paso 1: Instalar y configurar componentes de web de hello en el nodo principal de Hola
tooenable un clúster de toohello REST interfaz toosubmit trabajos a través de HTTPS, se garantiza que los componentes web de HPC Pack de Hola estén configurados en el nodo principal de HPC Pack Hola. Si no están ya instalados, instale primero componentes web de hello ejecutando el archivo de instalación HpcWebComponents.msi Hola. A continuación, configure los componentes de Hola ejecutando script de PowerShell de HPC de Hola **Set-HPCWebComponents.ps1**.

Para obtener información detallada, vea [instalar componentes Web de hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Algunas plantillas de inicio rápido de Azure para HPC Pack instalación y configuración componentes de hello web automáticamente. Si usas hello [script de implementación de IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate clúster de hello, si lo desea, puede instalar y configurar componentes de hello web como parte de la implementación de Hola.
> 
> 

**componentes web de tooinstall Hola**

1. Conectar máquina virtual del nodo principal toohello mediante credenciales de Hola de un administrador de clústeres.
2. Desde la carpeta de programa de instalación de HPC Pack hello, ejecute HpcWebComponents.msi en el nodo principal de Hola.
3. Siga los pasos de Hola de componentes web de hello Asistente tooinstall Hola

**componentes web de tooconfigure Hola**

1. En el nodo principal de hello, inicie HPC PowerShell como administrador.
2. toochange ubicación toohello del directorio de script de configuración de hello, Hola de tipo siguiente comando:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure Hola interfaz REST e iniciar Hola servicio Web de HPC, Hola de tipo siguiente comando:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Cuando tooselect solicitada un certificado, elija el certificado de Hola corresponde toohello de nombre DNS público del nodo principal de Hola. Por ejemplo, si implementa el nodo principal de hello máquinas virtuales que usan el modelo de implementación clásica de hello, el nombre del certificado de hello es similar a CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Si utiliza el modelo de implementación del Administrador de recursos de hello, el nombre del certificado de hello aspecto CN =&lt;*HeadNodeDnsName*&gt;.&lt; *región*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Seleccionar este certificado más adelante cuando se envía el nodo principal de toohello trabajos desde un equipo local. No seleccione ni configure un certificado que corresponda toohello el nombre del equipo de nodo principal de Hola Hola dominio de Active Directory (por ejemplo, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. tooconfigure Hola portal web de envío de trabajos, Hola de tipo siguiente comando:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Una vez completado el script de Hola, detenga y reinicie Hola servicio Programador de trabajos de HPC escribiendo Hola siguientes comandos:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Paso 2: Instalar herramientas de cliente de HPC Pack hello en un equipo local
Si desea utilidades de cliente de HPC Pack tooinstall hello en el equipo, descargue los archivos de instalación de HPC Pack (instalación completa) de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Al comenzar la instalación de hello, elija la opción de instalación de Hola para hello **utilidades de cliente de HPC Pack**.

las herramientas de cliente de HPC Pack de hello toouse toosubmit trabajos toohello VM del nodo principal, también necesita tooexport un certificado desde el nodo principal de Hola e instalarlo en el equipo cliente de Hola. Hola certificado debe estar en. Formato CER.

**certificado de hello tooexport desde el nodo principal de Hola**

1. En el nodo principal de hello, agregue Hola certificados complemento tooa Microsoft Management Console para hello cuenta de equipo Local. Para obtener pasos complemento tooadd hello, consulte [agregar Hola complemento certificados de MMC de tooan](https://technet.microsoft.com/library/cc754431.aspx).
2. En el árbol de consola de hello, expanda **certificados – equipo Local** > **Personal**y, a continuación, haga clic en **certificados**.
3. Busque certificado Hola que configuró para los componentes de web de HPC Pack hello en [paso 1: instalar y configurar componentes de web de hello en el nodo principal de hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por ejemplo, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Haga clic en el certificado de Hola y haga clic en **todas las tareas** > **exportar**.
5. Hola Asistente para exportación de certificados, haga clic en **siguiente**y asegúrese de que **No, no exportar la clave privada de hello** está seleccionada.
6. Hola seguimiento restantes pasos del certificado de hello Asistente tooexport hello en DER binario codificado X.509 (. Formato CER).

**certificado de hello tooimport en el equipo de cliente hello**

1. Copie el certificado de Hola que exportó desde la carpeta de tooa de nodo principal de hello en el equipo cliente de Hola.
2. En el equipo de cliente hello, ejecute certmgr.msc.
3. En el administrador de certificados, expanda **Certificados – Usuario actual** > **Entidades de certificación raíz de confianza**, haga clic con el botón derecho en **Certificados** y, después, en **Todas las tareas** > **Importar**.
4. Hola Asistente para importación de certificados, haga clic en **siguiente** y seguimiento Hola pasos tooimport Hola certificado que exportó desde toohello del nodo principal de hello almacenar entidades de certificación raíz de confianza.

> [!TIP]
> Puede que vea una advertencia de seguridad, porque la entidad de certificación de hello en el nodo principal de hello no se reconoce por equipo de cliente de Hola. Para realizar pruebas, puede omitir esta importación de certificados de hello completa y de advertencia.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Paso 3: Ejecutar trabajos de prueba en clúster de Hola
tooverify la configuración, pruebe los trabajos en ejecución en Hola de clúster en Azure Hola local de equipo. Por ejemplo, puede usar herramientas de interfaz gráfica de usuario de HPC Pack o clúster de toohello de comandos de línea de comandos toosubmit trabajos. También puede utilizar los trabajos de toosubmit portal basado en web.

**comandos de envío de trabajos de toorun en el equipo de cliente hello**

1. En un equipo cliente donde se instalan utilidades de cliente de HPC Pack hello, inicie un símbolo del sistema.
2. Escriba un comando de ejemplo. Por ejemplo, toolist todos los trabajos en el clúster de hello, escriba un tooone similar de comando de hello siguientes, según el nombre DNS completo de hello del nodo principal de hello:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    o
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Use Hola nombre DNS completo del nodo principal de hello, no Hola dirección IP, en dirección URL de programador de Hola. Si especifica la dirección IP de hello, un error se parezca demasiado "certificado de servidor hello tooeither es necesario tener una cadena válida de confianza o toobe colocan en almacén raíz de confianza de hello."
   > 
   > 
3. Cuando se le solicite, escriba el nombre de usuario de hello (en forma de hello &lt;DomainName&gt;\\&lt;nombre de usuario&gt;) y la contraseña de administrador de clústeres HPC de Hola o de otro usuario del clúster que configuró. Puede elegir toostore credenciales Hola localmente para más operaciones de trabajo.
   
    Aparece una lista de trabajos.

**toouse Administrador de trabajos de HPC en el equipo de cliente hello**

1. Si anteriormente no almacenar las credenciales de dominio para un usuario del clúster al enviar un trabajo, puede agregar las credenciales de hello en el Administrador de credenciales.
   
    a. En el Panel de Control en el equipo de cliente hello, inicie el Administrador de credenciales.
   
    b. Haga clic en **Credenciales de Windows** > **Agregar una credencial genérica**.
   
    c. Especifique la dirección de Internet de hello (por ejemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler o https://&lt;HeadNodeDnsName&gt;.&lt; región&gt;.cloudapp.azure.com/HpcScheduler) y el nombre de usuario de hello (&lt;DomainName&gt;\\&lt;nombre de usuario&gt;) y la contraseña de administrador de clústeres de hello u otro usuario del clúster que configuró.
2. En el equipo de cliente hello, inicie el Administrador de trabajos de HPC.
3. Hola **Seleccionar nodo principal** cuadro de diálogo, tipo hello URL toohello nodo principal en Azure (por ejemplo, https://&lt;HeadNodeDnsName&gt;. cloudapp.net o https://&lt;HeadNodeDnsName&gt;. &lt;región&gt;. cloudapp.azure.com).
   
    Administrador de trabajos de HPC se abre y muestra una lista de trabajos en el nodo principal de Hola.

**portal web toouse Hola que ejecuta en el nodo principal de Hola**

1. Inicie un explorador web en el equipo cliente de Hola y escriba uno de hello después de direcciones, según el nombre DNS completo de hello del nodo principal de hello:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    o
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. En el cuadro de diálogo para la seguridad Hola que aparece, escriba las credenciales de administrador de clústeres HPC de hello en el dominio de Hola. (También puede agregar otros usuarios de clúster en distintos roles. Consulte [Administración de usuarios de clúster](https://technet.microsoft.com/library/ff919335.aspx)).
   
    portal web de Hola abre la vista de lista de trabajo de toohello.
3. toosubmit un trabajo de ejemplo que devuelve cadena Hola "¡Hello World" del clúster de hello, haga clic en **nuevo trabajo** en el panel de navegación izquierdo Hola.
4. En hello **nuevo trabajo** página, en **de páginas de envío**, haga clic en **HelloWorld**. aparece la página de envío de trabajos de Hola.
5. Haga clic en **Enviar**. Si se le solicite, proporcione las credenciales de dominio de hello del Administrador de clúster HPC de Hola. se envió el trabajo de Hola y Hola Id. de trabajo aparece en hello **Mis trabajos** página.
6. resultados de hello tooview de trabajo de Hola que ha enviado, haga clic en Id. de trabajo de hello y, a continuación, haga clic en **tareas vista** resultado del comando hello tooview (bajo **salida**).

## <a name="next-steps"></a>Pasos siguientes
* También puede enviar trabajos toohello Azure clúster con hello [API de REST de HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Si desea toosubmit trabajos del clúster desde un cliente Linux, vea Hola Python ejemplo Hola [HPC Pack 2012 R2 SDK y código de ejemplo](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
