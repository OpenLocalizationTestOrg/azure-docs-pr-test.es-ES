---
title: aaaCreate un bloc de notas de IPython/Jupyter | Documentos de Microsoft
description: "Obtenga información acerca de cómo se crea toodeploy Hola Bloc de notas de IPython/Jupyter en una máquina virtual Linux con el modelo de implementación de administrador de recursos de hello en Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Creación de una máquina virtual de Azure, e instalación y ejecución de cuadernos de Jupyter Notebook en Azure
Hola [Jupyter proyecto](http://jupyter.org), Hola anteriormente [IPython proyecto](http://ipython.org), proporciona una colección de herramientas para informática científica con eficaces shells interactivos que combinan la ejecución de código con la creación de hello de un documento de cálculo activo. Estos archivos del bloc de notas pueden contener texto arbitrario, fórmulas matemáticas, código de entrada, resultados, gráficos, vídeos y cualquier otra clase de contenido multimedia que pueda mostrar cualquier explorador web moderno. Si el usuario está absolutamente nueva tooPython y desea toolearn en un divertido, entorno interactivo o realice algunas grave paralelo/técnico informática, hello Jupyter Notebook es una excelente opción.

![Captura de pantalla de](./media/jupyter-notebook/ipy-notebook-spectral.png) utilizando SciPy y Matplotlib paquetes tooanalyze Hola la estructura de una grabación de sonido.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Dos formas de Jupyter: Azure Notebooks o implementación personalizada
Azure proporciona un servicio que puede usar demasiado[comenzar rápidamente a usar Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Mediante el uso de hello servicio de Azure Bloc de notas, puede obtener fácilmente interfaz web accesible del tooJupyter de acceso a los recursos de cálculo escalables con toda la eficacia de Hola de Python y sus muchas bibliotecas.  Puesto que la instalación de Hola se controla mediante el servicio de hello, los usuarios pueden acceder a estos recursos sin necesidad de hello para la administración y configuración por usuario de Hola.

Si el servicio de Bloc de notas de hello no funciona para su escenario continuar tooread este artículo que se le mostrará cómo toodeploy Hola Jupyter Notebook en Microsoft Azure, usando máquinas virtuales (VM) en Linux.

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Creación y configuración de una máquina virtual en Azure
primer paso de Hello es toocreate una máquina virtual (VM) que se ejecuta en Azure.
Esta máquina virtual es un sistema operativo completo en la nube de Hola y se usará para ejecutar hello Jupyter Notebook. Es capaz de ejecutar máquinas virtuales Linux y Windows Azure y se explicará el programa de instalación de Hola de Jupyter en ambos tipos de máquinas virtuales.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Crear una máquina virtual de Linux y abrir un puerto para Jupyter
Siga las instrucciones de hello proporcionadas [aquí] [ portal-vm-linux] toocreate una máquina virtual de hello *Ubuntu* distribución. En este tutorial se usa Ubuntu Server 14.04 LTS. Supondremos que el nombre de usuario de hello *azureuser*.

Después de que implementa la máquina virtual de hello necesitamos tooopen de una regla de seguridad en el grupo de seguridad de red de Hola.  Desde Hola portal de Azure, vaya demasiado**grupos de seguridad de red** y pestaña abierta Hola Hola de grupo de seguridad correspondiente tooyour VM. Necesita tooadd una regla de seguridad de entrada con hello después de configuración: **TCP** para el protocolo de hello,  **\***  para el puerto de origen (público) hello y **9999** para puerto de destino (privado) de Hola.

![Instantánea](./media/jupyter-notebook/azure-add-endpoint.png)

Mientras que en el grupo de seguridad de red, haga clic en **Interfaces de red** Nota hello y **dirección IP pública** porque será necesaria tooconnect tooyour VM en el paso siguiente Hola.

## <a name="install-required-software-on-hello-vm"></a>Instalar el software necesario en hello VM
toorun Hola Jupyter Notebook en la máquina virtual, se deben instalar primero Jupyter y sus dependencias. Conectar máquinas virtuales de linux tooyour mediante ssh y Hola de par de nombre de usuario y contraseña de Hola que eligió al crear máquinas virtuales. En este tutorial, se usará PuTTY y se conectará desde Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Instalación de Jupyter en Ubuntu
Instalar Anaconda, una distribución de python de ciencia de datos muy popular, mediante uno de los vínculos de hello proporcionados a partir de [Continuum Analytics](https://www.continuum.io/downloads).  Redactar Hola de este documento, Hola vínculos siguientes son hello más seguridad toodate versiones.

#### <a name="anaconda-installs-for-linux"></a>Instalaciones de Anaconda para Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Instalación de Anaconda3 2.3.0 de 64 bits en Ubuntu
Como ejemplo, se trata de cómo puede instalar Anaconda en Ubuntu

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Instantánea](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Configuración de Jupyter y uso de SSL
Después de instalar necesitamos tootake una archivos de configuración de momento toosetup Hola para Jupyter. Si experimenta problemas con la configuración de Jupyter puede ser útil toolook en hello [Jupyter documentación para ejecutar un servidor de Bloc de notas](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Siguiente se `cd` toohello perfil directory toocreate nuestro certificado SSL y editar el archivo de configuración de perfiles de Hola.

En Linux usar hello siguiente comando.

    cd ~/.jupyter

Usar hello después de certificado SSL de Hola de comando toocreate (Linux y Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Tenga en cuenta que puesto que vamos a crear un certificado SSL autofirmado, cuando se conecta el Bloc de notas toohello el explorador le proporcionará una advertencia de seguridad.  Para su uso en producción a largo plazo, deberá toouse un certificado debidamente firmado asociado a su organización.  Puesto que la administración de certificados está más allá del ámbito de Hola de esta demostración, se quedará certificado autofirmado tooa por ahora.

Además toousing un certificado, también debe proporcionar una contraseña tooprotect del Bloc de notas de uso no autorizado.  Por motivos de seguridad Jupyter utiliza contraseñas cifradas en su archivo de configuración, por lo que necesitará tooencrypt su contraseña en primer lugar.  IPython proporciona un toodo utilidad en un símbolo del sistema ejecute hello siguiente comando.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Esto le solicitará una contraseña y la confirmación y, a continuación, imprimirá la contraseña de Hola. Tenga en cuenta esto para hello siguiendo el paso.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

A continuación, se modificará el archivo de configuración del perfil de hello, que es el `jupyter_notebook_config.py` archivo directorio Hola se encuentra en.  Tenga en cuenta que este archivo no exista, basta con crear, si ese es el caso de hello.  Estearchivo tiene varios campos que, de manera predeterminada, se convierten en comentario.  Puede abrir este archivo con cualquier editor de texto de su gusto, y debe asegurarse de que al menos se Hola después de contenido. **Ser seguro tooreplace hello c.NotebookApp.password en la configuración de hello con sha1 Hola del paso anterior hello**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Ejecute hello Jupyter Notebook
En este momento se está listo toostart hello Jupyter Notebook. toodo, navegue toohello directory desee toostore blocs de notas y comenzar a servidor de Jupyter Notebook Hola con hello siguiente comando.

    /anaconda3/bin/jupyter-notebook

Ahora debería ser capaz de tooaccess su Jupyter Notebook en la dirección de hello `https://[PUBLIC-IP-ADDRESS]:9999`.

Al acceder primero el Bloc de notas, página de inicio de sesión de hello solicita la contraseña. Y una vez que inicie sesión, verá el saludo "Jupyter Notebook panel", que es el centro de ontrol para todas las operaciones de Bloc de notas.  Desde esta página se pueden crear cuadernos nuevos y abrir los existentes.

![Instantánea](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Uso de hello Jupyter Notebook
Si hace clic en hello **New** botón, verá Hola después de la página inicial.

![Instantánea](./media/jupyter-notebook/jupyter-untitled-notebook.png)

área de Hello marcados con un `In []:` símbolo del sistema es el área de entrada de hello, aquí puede escribir cualquier código Python válido y se ejecutará cuando se alcance `Shift-Enter` o haga clic en el icono "Reproducir" hello (Hola triángulo hacia la derecha en la barra de herramientas de hello).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Los documentos informáticos activos con medios enriquecidos son un potente paradigma.
Bloc de notas de Hello propio se sentirá muy natural tooanyone que ha usado Python y un procesador de textos, porque es en cierto modo una combinación de ambos: puede ejecutar bloques de código de Python, pero también puede mantener notas y cualquier otro texto cambiando demasiado estilo de hello de una celda de "Código" "Ma rkdown"mediante el menú desplegable de hello en la barra de herramientas.

Jupyter es mucho más que un simple procesador de texto, debido a que permite combinar informática y medios enriquecidos (texto, gráficos, vídeo y prácticamente todos los elementos que se pueden mostrar en un explorador web moderno). Puede combinar texto, código, vídeos, etc.

![Instantánea](./media/jupyter-notebook/jupyter-editing-experience.png)

Y la potencia de Hola de muchas bibliotecas excelente de Python para la informática científicos y técnicos, Hola siguiente captura de pantalla, se puede realizar un cálculo simple con hello mismo facilitar como un análisis de red compleja, todo ello en un entorno.

Este paradigma de mezcla potencia de Hola de web moderna Hola con cálculo en vivo ofrece muchas posibilidades y es ideal para la nube de hello; se puede utilizar Hola Bloc de notas:

* Como una exploración toorecord de Bloc de notas de cálculo del trabajo en un problema.
* el resultado es tooshare con compañeros, ya sea en forma de cálculo 'activo' o en copia impresa formatos (HTML, PDF).
* toodistribute y presente materiales teaching en vivo que implican el cálculo, por tanto, los alumnos inmediatamente pueden experimentar con el código real de hello, modificarlo y volver a ejecutan de forma interactiva.
* tooprovide "ejecutable del producto" que presentan los resultados de Hola de investigación de forma que puede reproducir inmediatamente, validar y ampliado por otras personas.
* Como plataforma de informática en colaboración: varios usuarios pueden iniciar sesión en toothe mismo servidor de Bloc de notas tooshare una sesión de cálculo activa.

Si se dejan de código fuente de toohello IPython [repositorio][repository], encontrará todo un directorio con ejemplos de Bloc de notas que se pueden descargar y, a continuación, experimentar con en su propia máquina virtual Jupyter de Azure.  Simplemente descargue hello `.ipynb` archivos de Hola de sitio y cargarlos en el panel de saludo de la máquina virtual de Azure del Bloc de notas (o descargarlos directamente en hello VM).

## <a name="conclusion"></a>Conclusión
Hola Jupyter Notebook proporciona una interfaz eficaz para tener acceso a power Hola del ecosistema de Python de hello en Azure de forma interactiva.  Abarca una amplia variedad de casos de uso que incluye la exploración simple y el aprendizaje de Python, análisis de datos y visualización, simulación e informática en paralelo. documentos de Bloc de notas de Hello resultantes contienen un registro completo de los cálculos de Hola que se llevan a cabo y se puede compartir con otros usuarios de Jupyter.  Hola Jupyter Notebook puede utilizarse como una aplicación local, pero es especialmente adecuado para las implementaciones de nube en Azure

las características básicas de Hola de Jupyter también están disponibles dentro de Visual Studio a través de la [Python Tools para Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS es un complemento gratuito y de código abiertode Microsoft que convierte a Visual Studio unentorno de desarrollo avanzado de Python, que incluye un editor avanzado con la integración de IntelliSense, depuración,creación de perfiles y la informática en paralelo.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
