# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Realizar una conexión remota tooa Kubernetes, DC/OS o Docker Swarm Cluster Server
Después de crear un clúster de servicio de contenedor de Azure, es necesario tooconnect toohello clúster toodeploy y administrar las cargas de trabajo. Este artículo describe cómo tooconnect toohello master VM de hello de clúster desde un equipo remoto. 

Hola Kubernetes, DC/OS, Docker Swarm clústeres y proporcionan extremos HTTP localmente. Para Kubernetes, este punto de conexión de forma segura se expone en Hola internet y puede tener acceso a él mediante la ejecución de hello `kubectl` herramienta de línea de comandos desde cualquier equipo conectado a internet. 

Para el controlador de dominio/OS y Docker Swarm, recomendamos que cree un túnel de shell seguro (SSH) desde el sistema de administración de clúster de toohello de equipo local. Después de establece el túnel de hello, puede ejecutar comandos que utilizan los extremos HTTP de Hola e interfaz web de vista Hola orchestrator (si está disponible) desde el sistema local. 

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de Kubernetes, DC/OS o Docker Swarm [implementado en Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA archivo de clave privada correspondiente toohello toohello agregada de clave pública clúster durante la implementación. Estos comandos dan por hecho es clave SSH privada hello en `$HOME/.ssh/id_rsa` en el equipo. Para más información, consulte estas instrucciones para [macOS y Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../articles/virtual-machines/linux/ssh-from-windows.md). Si Hola conexión SSH no funciona, puede que tenga demasiado [restablecer las claves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Conectar tooa Kubernetes clúster

Siga estos pasos tooinstall y configurar `kubectl` en el equipo.

> [!NOTE] 
> En Linux o Mac OS, podría necesitar toorun comandos de hello en esta sección utilizando `sudo`.
> 

### <a name="install-kubectl"></a>Instalación de kubectl
Una manera de tooinstall esta herramienta es hello toouse `az acs kubernetes install-cli` comando de CLI de Azure 2.0. toorun este comando, asegúrese de que se [instalado](/cli/azure/install-az-cli2) Hola 2.0 más reciente de CLI de Azure y registran en tooan cuenta de Azure (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Como alternativa, puede descargar hello más reciente `kubectl` cliente directamente desde hello [Kubernetes libera página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Para más información, consulte [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalación y configuración de kubectl).

### <a name="download-cluster-credentials"></a>Descarga de las credenciales del clúster
Una vez que tenga `kubectl` instalado, es necesario que los equipos del tooyour toocopy Hola clúster credenciales. Las credenciales de una manera toodo get hello es con hello `az acs kubernetes get-credentials` comando. Pase el nombre de Hola Hola del grupo de recursos y nombre hello del recurso de servicio de contenedor de hello:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Este comando descarga las credenciales del clúster Hola demasiado`$HOME/.kube/config`, donde `kubectl` espera toobe encuentra.

Como alternativa, puede usar `scp` toosecurely archivo de hello de copia de `$HOME/.kube/config` en el equipo local de hello maestro VM tooyour. Por ejemplo:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Si se encuentra en Windows, puede usar Bash en Ubuntu en Windows, el cliente de copia de archivo seguro PuTTy de Hola o una herramienta similar.

### <a name="use-kubectl"></a>Uso de kubectl

Una vez que tenga `kubectl` configurado, probar la conexión de hello haciendo una lista de nodos de hello en el clúster:

```bash
kubectl get nodes
```

Puede probar otros comandos `kubectl`. Por ejemplo, puede ver hello Kubernetes panel. En primer lugar, ejecute a un proxy de servidor de la API de Kubernetes toohello:

```bash
kubectl proxy
```

Hello Kubernetes UI está ahora disponible en: `http://localhost:8001/ui`.

Para obtener más información, vea hello [inicio rápido de Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Conectar el clúster de DC/OS o conjunto de tooa

Hola toouse DC/OS y clústeres de Docker Swarm implementados por el servicio de contenedor de Azure, siga estas toocreate instrucciones un túnel SSH de su sistema local de Linux, Mac OS o Windows. 

> [!NOTE]
> Estas instrucciones se centran en la tunelización de tráfico TCP a través de SSH. También puede iniciar una sesión interactiva de SSH con uno de los sistemas de administración de hello interna en el clúster, pero no se recomienda esto. Al trabajar directamente en un sistema interno, pueden producirse cambios en la configuración de manera involuntaria.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Creación de un túnel de SSH en Linux o macOS
Hola primera cosa que se realiza al crear un túnel SSH en Linux o Mac OS es nombre DNS toolocate Hola público de patrones de carga equilibrada de Hola. Siga estos pasos:


1. Hola [portal de Azure](https://portal.azure.com), busque el grupo de recursos de toohello que contiene el clúster del servicio de contenedor. Expanda el grupo de recursos de Hola para que se muestre cada recurso. 

2. Haga clic en hello **servicio de contenedor** recurso y haga clic en **Introducción**. Hola **Master FQDN** de hello clúster aparece bajo **Essentials**. Guarde este nombre para usarlo más adelante. 

    ![Nombre DNS público](./media/container-service-connect/pubdns.png)

    O bien, ejecute hello `az acs show` comando en su servicio de contenedor. Busque hello **Master perfil: fqdn** propiedad en la salida del comando Hola.

3. Ahora, abra un shell y ejecute hello `ssh` comando especificando Hola siguientes valores: 

    **LOCAL_PORT** es Hola el puerto TCP en lado de servicio de Hola de hello túnel tooconnect a. Para el conjunto, establezca este too2375. Para el controlador de dominio/OS, establezca este too80. 
    **REMOTE_PORT** es el puerto de Hola de punto de conexión de Hola que desea tooexpose. Para Swarm, utilice el puerto 2375. Para DC/OS, utilice el puerto 80.  
    **Nombre de usuario** es nombre de usuario de Hola que ha proporcionado al implementar el clúster de Hola.  
    **DNSPREFIX** es Hola prefijo DNS que proporcionó al implementar el clúster de Hola.  
    **REGIÓN** es región hello en el que se encuentra el grupo de recursos.  
    **PATH_TO_PRIVATE_KEY** [opcional] es Hola ruta de acceso toohello clave privada correspondiente clave pública toohello que proporcionó al crear el clúster de Hola. Utilice esta opción con hello `-i` marca.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Hola puerto de conexión de SSH es 2200 y no Hola puerto estándar 22. En un clúster con más de una máquina virtual principal, se trata de hello conexión puerto toohello primer patrón de máquina virtual.
  > 

  comando de Hello devuelve sin salida.

Ver ejemplos de hello para DC/OS y conjunto de hello las secciones siguientes.    

### <a name="dcos-tunnel"></a>Túnel de DC/OS
tooopen un túnel para los puntos de conexión de controlador de dominio/OS, ejecute un comando como Hola siguiente:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Asegúrese de que no haya otro proceso local enlazado al puerto 80. Si es necesario, puede especificar un puerto local distinto del 80, como el puerto 8080. Sin embargo, algunos vínculos de la interfaz de usuario web podrían no funcionar cuando se utiliza este puerto.
>

Ahora puede acceder a los puntos de conexión de Hola DC/OS desde el sistema local a través de hello las siguientes direcciones URL (suponiendo que el puerto local 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

De forma similar, puede llegar a API de rest de Hola para cada aplicación a través de este túnel.

### <a name="swarm-tunnel"></a>Túnel de Swarm
tooopen un punto de conexión de túnel toohello conjunto, al ejecutar un comando como Hola siguiente:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Asegúrese de que no haya otro proceso local enlazado al puerto 2375. Por ejemplo, si se ejecuta el demonio de Docker Hola localmente, se establece por toouse puerto 2375. Si es necesario, puede especificar un puerto local distinto al puerto 2375.
>

Ahora puede acceder mediante la interfaz de línea de comandos de Docker de hello (CLI de Docker) en el sistema local de clúster Docker Swarm Hola. Para obtener las instrucciones de instalación, consulte [Install Docker](https://docs.docker.com/engine/installation/) (Instalación de Docker).

Establecer el toohello de variable de entorno DOCKER_HOST puerto local que ha configurado para el túnel de Hola. 

```bash
export DOCKER_HOST=:2375
```

Ejecute comandos de Docker ese clúster de Docker Swarm toohello de túnel. Por ejemplo:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Creación de un túnel de SSH en Windows
Existen varias opciones para crear túneles de SSH en Windows. Si está ejecutando Bash en Ubuntu en Windows o una herramienta similar, puede seguir instrucciones túneles SSH de hello, que se explicó anteriormente en este artículo para macOS y Linux. Como alternativa en Windows, esta sección se describe cómo túnel de toouse toocreate PuTTY Hola.

1. [Descargar PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema de Windows.

2. Ejecute la aplicación hello.

3. Escriba un nombre de host que se compone del nombre de usuario de administrador de clúster de Hola y Hola de nombre DNS público del primer patrón de hello en clúster de Hola. Hola **nombre de Host** parece demasiado`azureuser@PublicDNSName`. Escriba 2200 de hello **puerto**.

    ![Configuración 1 de PuTTY](./media/container-service-connect/putty1.png)

4. Seleccione **SSH > Auth** (SSL > Aut.). Agregue un ruta de acceso tooyour archivo de clave privada (en formato. ppk) para la autenticación. Puede usar una herramienta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate este archivo de Hola clúster de hello toocreate usa claves de SSH.

    ![Configuración 2 de PuTTY](./media/container-service-connect/putty2.png)

5. Seleccione **SSH > túneles** y configure siguiente Hola reenviados puertos:

    * **Puerto de origen:** use el 80 para DC/OS o el 2375 para Swarm.
    * **Destino:** use localhost:80 para DC/OS o localhost:2375 para Swarm.

    Hola siguiente ejemplo se configura para DC/OS, pero tendrá un aspecto similar para Docker Swarm.

    > [!NOTE]
    > El puerto 80 no debe estar en uso cuando se cree este túnel.
    > 

    ![Configuración 3 de PuTTY](./media/container-service-connect/putty3.png)

6. Cuando haya terminado, haga clic en **sesión > Guardar** configuración de conexión de toosave Hola.

7. tooconnect toohello PuTTY de sesión, haga clic en **abiertos**. Cuando se conecta, puede ver la configuración del puerto de hello en el registro de eventos PuTTY de Hola.

    ![Registro de eventos de PuTTY](./media/container-service-connect/putty4.png)

Después de configurar el túnel de Hola para DC/OS, puede tener acceso a Hola relacionados con puntos de conexión en:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Después de configurar el túnel de Hola para Docker Swarm, abra su tooconfigure de configuración de Windows una variable de entorno de sistema denominada `DOCKER_HOST` con un valor de `:2375`. A continuación, puede tener acceso a clúster de conjunto de Hola a través de hello CLI de Docker.

## <a name="next-steps"></a>Pasos siguientes
Implementar y administrar contenedores en un clúster:

* [Trabajo con Azure Container Service y Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Administración de contenedores con la API de REST](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Trabajar con Docker Swarm y de saludo servicio de contenedor de Azure](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

