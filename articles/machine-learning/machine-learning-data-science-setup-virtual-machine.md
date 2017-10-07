---
title: "aaaSet una máquina virtual como un servidor de Bloc de notas de IPython | Documentos de Microsoft"
description: "Configure una máquina virtual de Azure para su uso en un entorno de ciencia de datos con el servidor de IPython para realizar análisis avanzados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configuración de una máquina virtual de Azure como servidor del Bloc de notas de IPython para realizar análisis avanzados
Este tema se muestra cómo tooprovision y configurar una máquina virtual de Azure para análisis avanzado que pueden usarse como parte de un entorno de ciencia de datos. máquina virtual de Windows Hello se configura herramientas como Bloc de notas de IPython, Explorador de almacenamiento de Azure, AzCopy, así como otras utilidades que son útiles para los proyectos de análisis avanzado de soporte técnico. Explorador de almacenamiento de Azure y AzCopy, por ejemplo, proporcionan a diversas formas rápidas de almacenamiento de blobs de tooupload datos tooAzure desde su equipo local o toodownload se tooyour el equipo local desde el almacenamiento de blobs.

## <a name="create-vm"></a>Paso 1: Crear un máquina virtual de Azure de propósito general
Si ya tiene una máquina virtual de Azure y simplemente desea tooset de un servidor de Bloc de notas de IPython en él, puede omitir este paso y continuar demasiado[paso 2: agregar un extremo para la máquina de virtual existente de notas de IPython tooan](#add-endpoint).

Antes de iniciar el proceso de Hola de creación de una máquina virtual en Azure, debe toodetermine tamaño de Hola de máquina de Hola que sea necesario tooprocess Hola datos para su proyecto. Las máquinas más pequeñas tienen menos memoria y menos núcleos de CPU que los equipos más grandes, pero también son menos costosas. Para obtener una lista de tipos de equipos y los precios, vea hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">precios de máquinas virtuales </a> página

1. Inicie sesión demasiado<a href="https://manage.windowsazure.com" target="_blank">portal de Azure clásico</a>y haga clic en **New** en la esquina izquierda inferior de Hola. Aparecerá una ventana. Seleccione **PROCESO** -> **MÁQUINA VIRTUAL** -> **DE LA GALERÍA**.
   
    ![Creación del espacio de trabajo][24]
2. Elija uno de hello siguientes imágenes:
   
   * Windows Server 2012 R2 Datacenter
   * Experiencia con Windows Server Essentials (Windows Server 2012 R2)
     
     A continuación, haga clic en el flecha de hello hacia la derecha en hello inferior derecho toogo Hola siguiente página de configuración.
     
     ![Creación del espacio de trabajo][25]
3. Escriba un nombre para la máquina virtual de hello desea toocreate, tamaño de select Hola de máquina de hello (predeterminado: A3) basado en tamaño Hola de máquina de hello datos hello es continuo tooprocess y cómo eficaz desea Hola máquina toobe (memoria hello y tamaño del número de núcleos de cálculo) , escriba un nombre de usuario y una contraseña para la máquina de Hola. A continuación, haga clic en el flecha de hello hacia la derecha toogo toohello la siguiente página de configuración.
   
    ![Creación del espacio de trabajo][26]
4. Seleccione hello **AFINIDAD región/grupo/red VIRTUAL** que contiene Hola **cuenta de almacenamiento** que está planeando toouse para esta máquina virtual y, a continuación, seleccione esa cuenta de almacenamiento. Agregar un extremo final Hola Hola **EXTREMOS** campo escribiendo Hola < nombre de punto de conexión de hello ("IPython" a continuación). Puede elegir cualquier cadena como hello **nombre** de punto de conexión de Hola y cualquier número entero entre 0 y 65536 es **disponibles** como hello **puerto público**. Hola **puerto privado** tiene toobe **9999**. Debe **evitar** el uso de los puertos públicos que ya estén asignados a servicios de Internet. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Puertos para Servicios de Internet</a> ofrece una lista de puertos que se han asignado y deben evitarse.
   
    ![Creación del espacio de trabajo][27]
5. Haga clic en el proceso de aprovisionamiento Hola marca de verificación toostart Hola virtual machine.
   
    ![Creación del espacio de trabajo][28]

Puede tardar 15-25 minutos toocomplete Hola máquina de proceso de aprovisionamiento. Una vez creada la máquina virtual de hello, estado de Hola de esta máquina debe aparecer como **ejecutando**.

![Creación del espacio de trabajo][29]

## <a name="add-endpoint"></a>Paso 2: Agregar un punto de conexión para la máquina de virtual existente de notas de IPython tooan
Si ha creado la máquina virtual de hello siguiendo las instrucciones de hello en el paso 1, punto de conexión de hello para el Bloc de notas de IPython ya se ha agregado y se puede omitir este paso.

Si ya existe la máquina virtual de Hola y necesita tooadd un punto de conexión para el Bloc de notas de IPython que va a instalar en el paso 3 siguiente, primer inicio de sesión tooAzure portal clásico, seleccione la máquina virtual de Hola y Agregar extremo de hello para el servidor de Bloc de notas de IPython. Hello en la ilustración siguiente se contiene una captura de pantalla de portal de hello después de punto de conexión de hello para el Bloc de notas de IPython se ha agregado la máquina virtual de Windows tooa.

![Creación del espacio de trabajo][17]

## <a name="run-commands"></a>Paso 3: Instalar Bloc de notas de IPython y otras herramientas de compatibilidad
Después de crear la máquina virtual de hello, utilice toolog de protocolo de escritorio remoto (RDP) en la máquina virtual de Windows toohello. Para obtener instrucciones, consulte [cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Hola abierto **símbolo** (**ventana de comandos de Powershell a no hello**) como un **administrador** y ejecución Hola siguiente comando.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Cuando finalice la instalación de hello, Hola servidor Bloc de notas de IPython se inicia automáticamente en hello *C:\\usuarios\\\<nombre de usuario\>\\documentos\\IPython Blocs de notas* directory.

Cuando se le solicite, escriba una contraseña para hello Bloc de notas de IPython y la contraseña de Hola de administrador del equipo de Hola. Esto permite Hola Bloc de notas de IPython toorun como un servicio en la máquina de Hola.

## <a name="access"></a>Paso 4: Acceso a IPython Notebook desde un explorador web
Hola tooaccess server IPython Bloc de notas, abra un sitio web browser y entrada *https://&#60;virtual nombre DNS del equipo >: &#60; número de puerto público >* en el cuadro de texto de dirección URL de Hola. En este caso, Hola *&#60; número de puerto público >* debe ser el número de puerto de Hola que especificó cuando hello extremo Bloc de notas de IPython se agregó.

Hola *&#60; nombre DNS de la máquina virtual >* puede encontrarse en hello portal de Azure clásico. Después de iniciar sesión en el portal clásico de toohello, haga clic en **máquinas virtuales**, seleccione máquina de Hola que creó y, a continuación, seleccione **panel**, nombre DNS de Hola se mostrará como sigue:

![Creación del espacio de trabajo][19]

Se producirá una advertencia que indica que *hay un problema con el certificado de seguridad del sitio Web* (Internet Explorer) o *la conexión no es privada* (Chrome), como se muestra en la siguiente Hola cifras. Haga clic en **sitio Web de toothis continuar (no recomendado)** (Internet Explorer) o **avanzadas** y, a continuación,  **continuar demasiado &#60;* Nombre DNS*> (no seguro) ** toocontinue (Chrome). A continuación, escriba contraseña de Hola que tooaccess anterior especificado Hola notas de IPython.

**Internet Explorer:**
![Crear área de trabajo][20]

**Chrome:**
![Crear área de trabajo][21]

Después de iniciar sesión toohello Bloc de notas de IPython, un directorio *DataScienceSamples* se mostrará en el Explorador de Hola. Este directorio contiene notas de IPython de ejemplo que se comparten entre tareas de ciencia de datos de Microsoft toohelp a los usuarios realizar. Estas notas de IPython de ejemplo se desprotegen del [ **repositorio de GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello las máquinas virtuales durante el proceso de instalación del servidor de Bloc de notas de IPython Hola. Microsoft mantiene y actualiza con frecuencia este repositorio. Los usuarios pueden visitar GitHub repositorio tooget Hola actualizada más recientemente ejemplo hello de notas de IPython.
![Creación del espacio de trabajo][18]

## <a name="upload"></a>Paso 5: Cargar un bloc de notas de IPython existente desde un servidor de Bloc de notas de IPython toohello de equipo local
Notas de IPython proporcionan una manera fácil de tooupload a los usuarios un bloc de notas de IPython existente en su servidor Bloc de notas de IPython en máquinas virtuales de hello toohello de equipos locales. Después de iniciar sesión toohello Bloc de notas de IPython en un explorador web, haga clic en hello **directory** ese Hola se carga en el Bloc de notas de IPython. A continuación, seleccione un tooupload de archivo de Bloc de notas de IPython .ipynb desde el equipo local de Hola Hola **Explorador de archivos**y arrastre y coloque toohello directory Bloc de notas de IPython en el Explorador de web Hola. Haga clic en hello **cargar** botón tooupload hello .ipynb archivo toohello server Bloc de notas de IPython. Otros usuarios podrán entonces empezar a usarlo desde sus exploradores web.

![Creación del espacio de trabajo][22]

![Creación del espacio de trabajo][23]

## <a name="shutdown"></a>Apagado y desasignación de la máquina virtual cuando no esté en uso
Las máquinas virtuales de Azure tienen unas tarifas del tipo **pague solo por lo que use**. tooensure que no están siendo factura cuando no se utiliza la máquina virtual, tiene toobe en hello **detenido (desasignado)** estado cuando no esté en uso.

> [!NOTE]
> Si apaga la máquina virtual de Hola desde dentro de hello VM (utilizando las opciones de energía de Windows), Hola VM se detiene, pero sigue siendo asignado. tooensure no continúa toobe factura, siempre se detendrá máquinas virtuales de hello [portal de Azure clásico](http://manage.windowsazure.com/). También puede detener Hola VM a través de Powershell mediante una llamada a **ShutdownRoleOperation** con "PostShutdownAction" igual demasiado "StoppedDeallocated".
> 
> 

tooshut hacia abajo y cancelar la asignación de máquina virtual de hello:

1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com/) con su cuenta.  
2. Seleccione **máquinas virtuales** de barra de navegación izquierda de Hola.
3. En la lista de Hola de máquinas virtuales, haga clic en nombre de hello de la máquina virtual, a continuación, vaya toohello **panel** página.
4. En la parte inferior de Hola de página de hello, haga clic en **apagado**.

![Apagado de máquina virtual][15]

se cancela la asignación de máquina virtual de Hello pero no se eliminarán. Puede reiniciar la máquina virtual en cualquier momento desde Hola portal de Azure clásico.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>La VM de Azure está listo toouse: ¿qué es el siguiente?
La máquina virtual está ahora listo toouse en los ejercicios de ciencia de datos. máquina virtual de Hello también está listo para su uso como un servidor de Bloc de notas de IPython de exploración de Hola y el procesamiento de datos y otras tareas junto con hello proceso de ciencia de datos de equipo y aprendizaje automático de Azure.

Hola pasos siguientes en hello proceso de ciencia de datos de equipo se asignan en hello [ruta de acceso de aprendizaje](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir los pasos que se mueven datos en HDInsight, proceso y ejemplo allí como preparación para el aprendizaje a partir de los datos de hello con el equipo de Azure El aprendizaje.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
