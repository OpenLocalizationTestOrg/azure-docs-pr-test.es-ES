Las soluciones de nube de Azure están integradas en máquinas virtuales (emulación de hardware de equipo físico), para habilitar el empaquetado ágil de implementaciones de software y mejorar la consolidación de los recursos respecto al hardware físico. [Docker](https://www.docker.com) hello y contenedores ecosistema de docker tiene formas de hello drásticamente expandido puede desarrollar, distribuir y administrar software distribuido. Código de la aplicación en un contenedor está aislada de la máquina virtual del host de Hola y otros contenedores en Hola misma máquina virtual. Este aislamiento ofrece más agilidad en el desarrollo e implementación.

Azure ofrece Hola después de los valores de Docker:

* [Muchos](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [diferentes](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) formas toocreate Docker hospeda para contenedores toosuit su situación
* Hola [servicio de contenedor de Azure](https://azure.microsoft.com/documentation/services/container-service/) crea clústeres de hosts de contenedor con orchestrators como **maratón** y **swarm**.
* [El Administrador de recursos Azure](../articles/azure-resource-manager/resource-group-overview.md) y [plantillas de grupo de recursos](../articles/resource-group-authoring-templates.md) toosimplify implementar y actualizar aplicaciones complejas distribuidas
* integración con una matriz grande de ambas herramientas de administración de configuración patentadas y de código abierto

Y dado que puede crear mediante programación las máquinas virtuales y Linux contenedores en Azure, también puede usar máquinas virtuales y contenedor *orquestación* herramientas toocreate grupos de máquinas virtuales (VM) y aplicaciones de toodeploy dentro de ambos Linux contenedores y ahora [contenedores de Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

En este artículo no solo se explica estos conceptos en un nivel alto, también contiene gran cantidad de información de toomore de vínculos, tutoriales, y productos relacionados con uso toocontainer y clúster en Azure. Si conoce todo esto y solo desea que los vínculos de hello, aquí está en [herramientas para trabajar con contenedores](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>diferencia de Hello entre máquinas virtuales y contenedores
Las máquinas virtuales se ejecutan en un entorno de virtualización de hardware aislado proporcionado por un [hipervisor](http://en.wikipedia.org/wiki/Hypervisor). En Azure, Hola [máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/) servicio controla todo lo que para usted: crear máquinas virtuales mediante la elección de sistema operativo de Hola y configuración &mdash;o cargue una imagen de máquina virtual personalizada. Máquinas virtuales son una tecnología de eficacia comprobada, "reforzado batalla", y hay muchas herramientas disponibles toomanage Hola SO y las aplicaciones que contienen.  Aplicaciones en una máquina virtual se ocultan en sistemas operativos de host de Hola. Desde el punto de vista de Hola de una aplicación o un usuario en una máquina virtual, Hola VM aparece toobe un equipo físico autónomo.

[Contenedores de Linux](http://en.wikipedia.org/wiki/LXC) y los creados y hospedados mediante herramientas de docker, no use un aislamiento de tooprovide de hipervisor. Con los contenedores, host de contenedor de hello usa el proceso y características de aislamiento de sistema de archivos del contenedor de hello Linux kernel tooexpose toohello, sus aplicaciones, ciertas características de kernel y su propio sistema aislado de archivos. Desde el punto de vista de Hola de aplicaciones que se ejecutan dentro de un contenedor, el contenedor de hello aparece toobe una única instancia del sistema operativo. Una aplicación contenida no puede ver los procesos ni otros recursos situado fuera de su contenedor.

Se utilizan mucho menos recursos en un contenedor de Docker que los que se usan en una máquina virtual. Contenedores de docker emplean un aislamiento y ejecución de modelo de aplicación, que no comparte el kernel de Hola de host de Docker Hola. contenedor Hello tiene mucho menor consumo de disco que no incluya Hola todo el sistema operativo. El tiempo de inicio y el espacio en disco necesario son mucho menores que en una máquina virtual.
Contenedores de Windows ofrecen Hola mismas ventajas como contenedores de Linux para las aplicaciones que se ejecutan en Windows. Contenedores de Windows admiten el formato de imagen de Docker de Hola y API de Docker, pero también se pueden administrar con PowerShell. Se encuentran disponibles dos tiempos de ejecución de contenedores con los contenedores de Windows, de Windows Server y de Hyper-V. Los contenedores de Hyper-V proporcionan un nivel adicional de aislamiento porque hospedan cada contenedor en una máquina virtual superoptimizada. toolearn más información acerca de los contenedores de Windows consulte [acerca de los contenedores de Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget a trabajar con contenedores de Windows en Azure, obtenga información acerca de cómo demasiado[implementar un clúster de servicio de contenedor de Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>¿Para qué son buenos los contenedores?

Los contenedores pueden mejorar:

* se pueden desarrollar y compartir código de la velocidad de la aplicación Hello
* velocidad de Hola y se puede probar una aplicación de confianza
* velocidad de Hola y se puede implementar una aplicación de confianza

Los contenedores se ejecutan en un host contenedor, es decir, un sistema operativo y, en Azure, eso significa una máquina virtual de Azure. Incluso si ya le encanta idea Hola de contenedores, va tooneed una infraestructura VM hospeda contenedores de hello, pero Hola ventajas son las que los contenedores no prestan atención en qué máquina virtual se está ejecutando (aunque si desea que el contenedor de hello un Linux o Windows entorno de ejecución será importante, por ejemplo).


## <a name="what-are-containers-good-for"></a>¿Para qué son buenos los contenedores?
Son muy importantes para muchas cosas, pero éstos animen a&mdash;igual que [servicios en la nube](https://azure.microsoft.com/services/cloud-services/) y [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;Hola creación de servicio de single, orientada a servicios de microservicio aplicaciones distribuidas, en la aplicación que el diseño se basa en partes más de small, admite composición en lugar de en componentes mayores y más fuertemente acoplados.

Esto es especialmente cierto en entornos de nube pública como Azure, en los que se alquilan máquinas virtuales cuando y donde lo desea. No sólo obtiene aislamiento y una implementación rápida y herramientas de orquestación, pero puede tomar decisiones de infraestructura de aplicaciones más eficaces.

Por ejemplo, podría disponer actualmente de una implementación compuesta por 9 máquinas virtuales de Azure de un tamaño grande para una aplicación distribuida de alta disponibilidad. Si los componentes de Hola de esta aplicación se pueden implementar en contenedores, podría ser capaz de toouse solo 4 máquinas virtuales e implementar los componentes de aplicación dentro de 20 contenedores para ofrecer redundancia y equilibrio de carga.

Esto es sólo un ejemplo, por supuesto, pero si puede hacer esto en el escenario, puede ajustar los picos de toousage con más contenedores en lugar de más máquinas virtuales de Azure y usar hello restantes carga general de CPU de forma mucho más eficaz que el anterior.

Además, hay muchos escenarios que no prestan tooa microservicios enfoque; sabrá mejor si microservicios y contenedores le permitirá.

### <a name="container-benefits-for-developers"></a>Ventajas del contenedor para los desarrolladores
En general, resulta fácil toosee que la tecnología de contenedor es un paso hacia delante, pero hay ventajas más específicos, así. ¡Eche ejemplo hello de contenedores de Docker. En este tema no se profundizar profundamente en Docker ahora (leer [¿qué es Docker?](https://www.docker.com/whatisdocker/) para ese caso, o [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), pero Docker y su ecosistema ofrecen enormes beneficios tooboth a los desarrolladores y TI profesionales de TI.

Los desarrolladores aprovechar contenedores tooDocker rápidamente, ya encima de las que hace uso de contenedores de Linux y Windows easy:

* Se puede usar comandos simple, incremental toocreate una imagen fija que sea fácil toodeploy y se puede automatizar la creación de esas imágenes mediante un dockerfile
* Pueden compartir las imágenes fácilmente mediante sencillos, [git](https://git-scm.com/)-el estilo de inserción y extracción comandos demasiado[público](https://registry.hub.docker.com/) o [registros docker privada](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Pueden pensar en componentes de aplicación asilados en lugar de equipos
* Pueden usar un gran número de herramientas que comprenden los contenedores docker y diferentes imágenes base

### <a name="container-benefits-for-operations-and-it-professionals"></a>Ventajas de los contenedores para las operaciones y los profesionales de TI
TI y profesionales de operaciones también se beneficiarán de la combinación de Hola de contenedores y máquinas virtuales.

* los servicios independientes están aislados del entorno de ejecución del host de máquina virtual
* se puede verificar que el código independiente es idéntico
* los servicios independientes pueden iniciarse, detenerse y moverse rápidamente entre entornos de producción, pruebas y desarrollo

Características como estos&mdash;y hay más&mdash;excitar empresas establecidas, donde las organizaciones de tecnología de información profesional tienen trabajo Hola de recursos para adaptarlos&mdash;incluidos pura potencia de procesamiento&mdash; toohello tareas necesarias toonot solo permanecen en la empresa, pero aumentar la satisfacción del cliente y no llegar. Las pequeñas empresas, ISV y las nuevas empresas tienen exactamente Hola mismo requisito, pero podría describirlo diferente.

## <a name="what-are-virtual-machines-good-for"></a>¿Para qué resultan buenas las máquinas virtuales?
Las máquinas virtuales proporcionan backbone Hola de informática en nube, y que no cambia. Si las máquinas virtuales iniciar más lentamente, tienen una mayor superficie de disco y no se asignan directamente tooa microservicios arquitectura, tienen ventajas muy importantes:

1. De forma predeterminada, tienen protecciones de seguridad predeterminadas mucho más sólidas para el equipo host
2. Admiten cualquier configuración de aplicación y sistema operativo principal
3. Tienen ecosistemas de herramienta antiguos de comando y control
4. Proporcionan ejecución Hola contenedores de toohost de entorno

último elemento de Hello es importante, porque una aplicación independiente todavía requiere un sistema operativo específico y el tipo de CPU, en función de llamadas Hola hará que la aplicación hello. Es importante tooremember instalar contenedores en máquinas virtuales debido a que contienen aplicaciones Hola desea toodeploy; los contenedores no son reemplazos para máquinas virtuales o sistemas operativos.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Comparación de características de alto nivel de máquinas virtuales y contenedores
Hello tabla siguiente se describen en un gran tipo hello de nivel de característica diferencias que&mdash;sin requerir mucho trabajo adicional&mdash;existen entre las máquinas virtuales y Linux contenedores. Tenga en cuenta que puede ser más o menos deseable dependiendo de su propia aplicación necesita algunas características, y que al igual que con todo el software, trabajo adicional que proporciona una mayor compatibilidad con características, especialmente en el área de Hola de seguridad.

| Característica | Máquinas virtuales | Contenedores |
|:--- | --- | --- |
| Compatibilidad con la seguridad "Predeterminada" |mayor tooa |tooa ligeramente menor grado |
| Memoria en disco necesaria |Sistema operativo más aplicaciones completos |Solo requisitos de aplicación |
| Tiempo consumido toostart |Significativamente más largo: el arranque del SO más la carga de la aplicación |Considerablemente más corta: solo aplicaciones necesitan toostart porque ya se está ejecutando el kernel |
| Portabilidad |Portable con la preparación adecuada |Portable en formato de imagen; suelen ser más pequeños |
| Automatización de imágenes |Varía considerablemente dependiendo del sistema operativo y las aplicaciones |[Registro docker](https://registry.hub.docker.com/); otros |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Creación y administración de grupos de máquinas virtuales y contenedores
En este momento, cualquier arquitecto, desarrollador o especialista en operaciones de TI podrá pensar: "Puedo automatizar TODO esto; esta es realmente un centro de datos como servicio".

Es correcto, puede ser y cualquier número de sistemas, muchos de los cuales puede ya utiliza, que puede administrar grupos de máquinas virtuales de Azure e inyectar código personalizado con scripts, a menudo con hello [CustomScriptingExtension para Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) o Hola [CustomScriptingExtension para Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Puede automatizar &mdash;y es posible que ya lo haya hecho&mdash; sus implementaciones de Azure mediante PowerShell o scripts de la CLI de Azure.

Estas capacidades son a menudo, a continuación, como migrados tootools [Puppet](https://puppetlabs.com/) y [Chef](https://www.chef.io/) tooautomate Hola creación de y la configuración para las máquinas virtuales a escala. (Estos son algunos vínculos demasiado[uso de estas herramientas con Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Plantillas de grupo de recursos de Azure
Más recientemente, Azure presentó hello [administración de recursos de Azure](../articles/resource-manager-deployment-model.md) API de REST y toouse de herramientas de PowerShell y la CLI de Azure actualizada se fácilmente. Puede implementar, modificar o volver a implementar topologías de toda la aplicación con [plantillas de Azure Resource Manager](../articles/resource-group-authoring-templates.md) con el uso de la API de administración de recursos de Azure de hello:

* Hola [portal de Azure con plantillas](https://github.com/Azure/azure-quickstart-templates)&mdash;sugerencia, use el botón de "DeployToAzure" hello
* Hola [CLI de Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Implementación y administración de todos los grupos de máquinas virtuales y contenedores de Azure
Hay varios sistemas conocidos que pueden implementar todos los grupos de máquinas virtuales e instalar Docker (u otros sistemas de host del contenedor de Linux) en ellos como un grupo automatizable. Para obtener vínculos directos, vea hello [contenedores y herramientas](#containers-and-vm-technologies) sección, a continuación. Existen varios sistemas que realizan esta extensión mayor o menor de tooa y esta lista no es exhaustiva. Dependiendo de su conjunto de habilidades y escenarios, puede que resulten útiles o no.

Docker tiene su propio conjunto de herramientas de creación de máquinas virtuales ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) y una herramienta de administración de clústeres con contenedor de Docker de equilibrio de carga ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Además, Hola [extensión de máquina virtual de Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) incluye compatibilidad predeterminada con [ `docker-compose` ](https://docs.docker.com/compose/), que puede implementar configurado contenedores de aplicaciones entre varios contenedores.

Además, puede probar el [sistema operativo de centro de datos de Mesosphere (DCOS)](http://docs.mesosphere.com). DCOS se basa en código abierto de hello [mesos](http://mesos.apache.org/) "kernel de sistemas distribuidos" que permite tootreat su centro de datos como un servicio direccionable. DCOS tiene paquetes integrados para varios sistemas importantes como [Spark](http://spark.apache.org/) y [Kafka](http://kafka.apache.org/) (y otros), así como servicios integrados como [Marathon](https://mesosphere.github.io/marathon/) (un sistema de control de contenedores) y [Chronos](https://mesos.github.io/chronos/) (un programador distribuido). Mesos se deriva de las lecciones aprendidas en Twitter, AirBnb y otras empresas de escala web. También puede usar **swarm** como motor de orquestaciones de Hola.

Además, [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) es un sistema de código abierto para la administración de grupos de máquinas virtuales y contenedores derivado de las lecciones aprendidas en Google. También es posible usar [kubernetes con tejido compatibilidad con redes de tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) está abierto "Plataforma como-servicio" (PaaS) que hace más fácil toodeploy de origen y administrar aplicaciones en sus servidores. Deis se basa en Docker y CoreOS tooprovide una ligera PaaS con un flujo de trabajo inspiradas en Heroku.

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html) es una distribución de Linux con una superficie optimizada, compatibilidad con Docker y su propio sistema de contenedor denominado [rkt](https://github.com/coreos/rkt), también tiene una herramienta de administración de grupos de contenedores denominada [fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu, otra distribución de Linux muy popular, admite Docker muy bien, pero también admite [clústeres de Linux (estilo LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Herramientas para trabajar con máquinas virtuales de Azure y contenedores
Para trabajar con contenedores y máquinas virtuales de Azure se usan herramientas. En esta sección se proporciona una lista de solo algunos de los conceptos más importantes o útiles de Hola y herramientas sobre los contenedores, grupos y configuración de mayor de Hola y herramientas de orquestación que se usan con ellas.

> [!NOTE]
> Esta área cambia muy rápidamente y mientras se hará nuestro tookeep mejor en este tema y sus vínculos de toodate, también podría ser una tarea imposible. ¡Asegúrese de que buscar en interesantes tookeep asuntos seguridad toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Contenedores y tecnologías de máquina virtual
Algunas tecnologías de contenedor de Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS y rkt](https://github.com/coreos/rkt)
* [Proyecto de contenedor abierto](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Vínculos de contenedor de Windows:

* [Contenedores de Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Vínculos de Visual Studio Docker:

* [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Herramientas de Docker:

* [Docker daemon](https://docs.docker.com/installation/#installation)
* Clientes Docker
  * [Cliente de Windows Docker en Chocolatey](https://chocolatey.org/packages/docker)
  * [Instrucciones de instalación de Docker](https://docs.docker.com/installation/#installation)

Docker en Microsoft Azure:

* [Extensión de VM de Docker para Linux en Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Guía de usuario de la extensión de máquina virtual de Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Uso de hello extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Uso de hello extensión de máquina virtual Docker de hello portal de Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [¿Cómo toouse máquina docker en Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Cómo toouse docker con el conjunto en Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Introducción a Docker y Compose en Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Con un toocreate de plantilla de grupo de recursos de Azure un host Docker en Azure rápidamente](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Hola compatibilidad integrada para `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) para aplicaciones independientes
* [Implementación de su propio Docker Registry privado en Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Distribuciones de Linux y ejemplos de Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configuración, administración del clúster y orquestación de contenedor:

* [Flota en CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Completar la Guía de implementación de clúster de tooautomated Kubernetes con CoreOS y el tejido](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Visualizador de Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Sistema operativo de centro de datos de Mesosphere (DCOS)](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) y [Hudson](http://hudson-ci.org/)

  * [Complemento de agente de máquina virtual de Jenkins para Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [Repositorio de GitHub: Complemento de almacenamiento de Jenkins para Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Terceros: Complemento esclavo de Hudson para Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Terceros: Complemento de almacenamiento de Hudson para Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Automation](https://azure.microsoft.com/services/automation/)

  * [Vídeo: ¿Cómo tooUse automatización de Azure con máquinas virtuales de Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* PowerShell DSC para Linux

  * [Blog: Cómo toodo DSC de Powershell para Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: DSC de cliente Docker](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Pasos siguientes
Desproteja [Docker](https://www.docker.com) y [Contenedores de Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
