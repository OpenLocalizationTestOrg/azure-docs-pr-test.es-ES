# <a name="container-service-frequently-asked-questions"></a>Preguntas más frecuentes sobre Azure Container Service

## <a name="orchestrators"></a>Orquestadores

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>¿Qué orquestadores de contenedor son compatibles con Azure Container Service? 

Hay compatibilidad con Kubernetes, Docker Swarm y DC/OS de código abierto. Para obtener más información, vea hello [Introducción](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>¿Se admite el modo de Docker Swarm? 

Actualmente no se admite el modo de conjunto, pero está en el plan de servicio de Hola. 

### <a name="does-azure-container-service-support-windows-containers"></a>¿Admite Azure Container Service contenedores de Windows?  

Los contenedores de Linux se admiten con todos los orquestadores. La compatibilidad de contenedores de Windows con Kubernetes está en versión preliminar.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>¿Se recomienda un organizador específico en Azure Container Service? 
Por lo general, no se recomienda un organizador específico. Si tiene experiencia con uno de orchestrators Hola admite, puede aplicar esa experiencia en el servicio de contenedor de Azure. Sin embargo, las tendencias de datos sugieren que DC/OS es productivo para cargas de trabajo de IoT y macrodatos, Kubernetes es adecuado para las cargas de trabajo nativo de la nube y Docker Swarm se conoce por su integración con herramientas de Docker y su fácil curva de aprendizaje.

Según el escenario, también puede crear y administrar soluciones de contenedor personalizadas con otros servicios de Azure. Estos servicios incluyen [Virtual Machines](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) y [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>¿Cuál es la diferencia de hello entre el servicio de contenedor de Azure y ACS motor? 
Servicio de contenedor de Azure es un servicio de Azure basado en SLA con características de hello portal de Azure, herramientas de línea de comandos de Azure y API de Azure. servicio de Hello permite que tooquickly implementar y administrar clústeres que ejecutan las herramientas de orquestación de contenedores estándar con un número relativamente pequeño de opciones de configuración. 

[Motor de ACS](http://github.com/Azure/acs-engine) es un proyecto de código abierto que permite la configuración de clúster de energía a los usuarios toocustomize Hola a todos los niveles. Esta configuración de hello tooalter de capacidad de infraestructura y software significa que no ofrecemos ningún SLA para el motor de ACS. Soporte técnico se controla a través del proyecto de código abierto de hello en GitHub, en lugar de hacerlo a través de canales oficiales de Microsoft. 

## <a name="cluster-management"></a>Administración de clústeres

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>¿Cómo se crean claves de SSH para el clúster?

Puede usar las herramientas estándar en su toocreate de sistema operativo un par clave SSH RSA pública y privada para la autenticación con máquinas virtuales de Linux de hello para el clúster. Para conocer los pasos, vea hello [OS X y Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) instrucciones. 

Si usa [comandos de CLI de Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un contenedor de servicio de clúster, SSH claves pueden generarse automáticamente para el clúster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>¿Cómo creo una entidad de servicio para el clúster de Kubernetes?

Un identificador de entidad de seguridad de servicio de Azure Active Directory y la contraseña también son necesario toocreate un clúster de Kubernetes en el servicio de contenedor de Azure. Para obtener más información, consulte [acerca de la entidad de seguridad de servicio de Hola para un clúster de Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Si usa [comandos de CLI de Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un Kubernetes servicio de Cluster Server, se pueden generar automáticamente las credenciales de la entidad de seguridad para el clúster.

### <a name="how-large-a-cluster-can-i-create"></a>¿Cómo de grande puedo crear un clúster?
Puede crear un clúster con 1, 3 o 5 nodos maestros. Puede elegir en nodos de agente de too100.

> [!IMPORTANT]
> Para clústeres más grandes y función hello que elija para los nodos de tamaño de máquina virtual, puede que tenga cuota de núcleos de hello tooincrease en su suscripción. toorequest un aumento de la cuota, abra un [solicitud de soporte técnico al cliente en línea](../articles/azure-supportability/how-to-create-azure-support-request.md) sin cargo. Si usa una [cuenta gratuita de Azure](https://azure.microsoft.com/free/), solo puede usar un número limitado de núcleos de proceso de Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>¿Cómo aumentar número Hola de maestros después de crear un clúster? 
Una vez creado el clúster de hello, número de Hola de maestros es fijo y no se puede cambiar. Durante la creación de hello de clúster de hello, lo ideal es que debe seleccionar a varios maestros para lograr alta disponibilidad.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>¿Cómo aumentar número Hola de agentes después de crear un clúster? 
Puede escalar número Hola de agentes en el clúster de hello mediante Hola portal de Azure o herramientas de línea de comandos. Consulte [Escalado de un clúster de Azure Container Service](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>¿Cuáles son las direcciones URL de Hola de mi maestros y los agentes? 
Hola las direcciones URL de clúster de recursos en el servicio de contenedor de Azure se basan en hello prefijo proporcionar y Hola nombre de hello Azure región elegida para la implementación de nombres DNS. Por ejemplo, nombre de dominio completo (FQDN) de hello del nodo principal de hello es de esta forma:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Puede encontrar direcciones URL utilizadas para el clúster en hello portal de Azure, Hola Explorador de recursos de Azure u otras herramientas de Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>¿Cómo se puede saber qué versión de orquestador se está ejecutando en mi clúster?

* Controlador de dominio/OS: Vea hello [documentación Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: ejecute `docker version`
* Kubernetes: ejecute `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>¿Cómo puedo actualizar orchestrator Hola después de la implementación?

Actualmente, el servicio de contenedor de Azure no proporciona ToolsVersion tooupgrade Hola de orchestrator Hola implementada en el clúster. Si Container Service es compatible con una versión posterior, puede implementar un nuevo clúster. Otra opción es toouse orchestrator-herramientas específicas de cada si están disponible tooupgrade un clúster in situ. Por ejemplo, consulte [DC/OS Upgrading](https://dcos.io/docs/1.8/administration/upgrading/) (Actualización de DC/OS).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>¿Dónde se encuentra el clúster toomy cadena de hello SSH conexión?

Puede encontrar la cadena de conexión de Hola Hola portal de Azure, o mediante las herramientas de línea de comandos de Azure. 

1. En el portal de hello, navegue toohello el grupo de recursos para la implementación de clústeres de Hola.  

2. Haga clic en **Introducción** y haga clic en vínculo hello **implementaciones** en **Essentials**. 

3. Hola **historial de implementación** hoja, haga clic en implementación de Hola que tiene un nombre que comienza con **acs microsoft** seguido de una fecha de implementación. Ejemplo: microsoft-acs-201701310000.  

4. En hello **resumen** página, en **salidas**, se proporcionan varios vínculos de clúster. **SSHMaster0** proporciona un SSH conexión cadena toohello primera maestro en el clúster de servicio de contenedor. 

Como se indicó anteriormente, también puede utilizar herramientas de Azure toofind Hola FQDN del maestro de Hola. Realizar una conexión SSH master toohello con hello FQDN del maestro de Hola y nombre de usuario de Hola que especificó al crear el clúster de Hola. Por ejemplo:

```bash
ssh userName@masterFQDN –A –p 22 
```

Para obtener más información, consulte [clúster de servicio de contenedor de Azure de conectar tooan](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Pasos siguientes

* [Más información](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) sobre Azure Container Service.
* Implementar un clúster de servicio de contenedor con hello [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) o [CLI de Azure 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
