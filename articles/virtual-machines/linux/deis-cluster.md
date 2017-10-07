---
title: "aaaDeploy Deis 3 nodos clúster | Documentos de Microsoft"
description: "Este artículo se describe cómo toocreate un nodo 3 Deis clúster en Azure mediante una plantilla de Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Implementación y configuración de un clúster Deis de 3 nodos en Azure
Este artículo le guiará a través de aprovisionamiento de un clúster [Deis](http://deis.io/) en Azure. Abarca todos los pasos de hello creen Hola certificados necesarios toodeploying y obtener un ejemplo de ajuste de escala **vaya** aplicación en clúster recién suministradas Hola.

Hello siguiente diagrama muestra hello arquitectura del sistema de hello implementado. Un administrador del sistema administra Hola clúster con Deis herramientas como **deis** y **deisctl**. Las conexiones se establecen a través de un equilibrador de carga de Azure, que reenvía Hola conexiones tooone del miembro de hello nodos en clúster de Hola. el acceso de los clientes de Hello implementar aplicaciones a través del equilibrador de carga de hello así. En este caso, el equilibrador de carga de hello reenvía Hola tráfico tooa Deis malla de enrutador, que routs más contenedores de Docker de tráfico toocorresponding hospedados en clúster de Hola.

  ![Diagrama de arquitectura del clúster Desis implementado](./media/deis-cluster/architecture-overview.png)

En orden toorun a través de pasos de hello, necesitará:

* Una suscripción de Azure activa. Si no tiene una, puede obtener una prueba gratuita en [azure.com](https://azure.microsoft.com/).
* Un trabajo o grupos de recursos de Azure de escuela id toouse. Si tiene una cuenta personal y un registro con un Id. de Microsoft, necesita demasiado[crear un identificador de trabajo del que el personal](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Cualquiera, dependiendo del sistema operativo de cliente: Hola [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [CLI de Azure para Mac, Linux y Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL está certificados necesarios de hello toogenerate usado.
* Un cliente Git como [Git Bash](https://git-scm.com/).
* aplicación de ejemplo de Hola tootest, también necesitará un servidor DNS. Puede usar los servidores o servicios DNS que admiten los registros de carácter comodín A.
* Un equipo toorun Deis herramientas de cliente. Puede usar un equipo local o en una máquina virtual. Puede ejecutar estas herramientas en casi cualquier distribución de Linux, pero las instrucciones siguientes hello usan Ubuntu.

## <a name="provision-hello-cluster"></a>Clúster de Hola de aprovisionamiento
En esta sección, usará un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) plantilla del repositorio de código abierto de hello [plantillas de inicio rápido de azure](https://github.com/Azure/azure-quickstart-templates). En primer lugar, deberá copiar hacia abajo de la plantilla de Hola. A continuación, creará un nuevo par de claves SSH para la autenticación. Y, a continuación, configurará un nuevo identificador para su clúster. Y por último, usará secuencias de comandos de Shell de Hola o clúster de hello PowerShell script tooprovision Hola.

1. Repositorio de Hola de clon: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Vaya a la carpeta de plantillas de toohello:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Cree un nuevo par de claves SSH mediante ssh-keygen:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Generar un certificado mediante Hola por encima de la clave privada:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Vaya demasiado[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nuevo token de clúster, que busca un resultado similar:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Cada clúster CoreOS debe toohave un token único de este servicio gratuito. Consulte [Documentación de CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) para obtener más detalles.
6. Modificar hello **nube config.yaml** tooreplace Hola existente de archivos **detección** token con el nuevo token de hello:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Modificar hello **azuredeploy parameters.json** archivo: certificado Hola abierto que creó en el paso 4 en un editor de texto. Copiar todo el texto entre `----BEGIN CERTIFICATE-----` y `-----END CERTIFICATE-----` en hello **sshKeyData** parámetro (deberá tooremove todos los caracteres de nueva línea).
8. Modificar hello **newStorageAccountName** parámetro. Se trata de una cuenta de almacenamiento de Hola para discos de sistema operativo de la máquina virtual. Este nombre de cuenta tiene toobe único global.
9. Modificar hello **publicDomainName** parámetro. Esto pasaría a formar parte del nombre DNS de hello asociado con IP pública del equilibrador de carga Hola. Hello FQDN final tendrá formato Hola de *[valor de este parámetro]*. *[Región]* . cloudapp.azure.com. Por ejemplo, si especifica nombre hello como deishbai32 y grupo de recursos de hello es región del oeste de Estados Unidos toohello implementado, Hola final equilibrador de carga FQDN tooyour será deishbai32.westus.cloudapp.azure.com.
10. Guarde el archivo de parámetros de Hola. Y, a continuación, puede aprovisionar clúster Hola con Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    o la CLI de Azure:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Cuando se aprovisiona el grupo de recursos de hello, puede ver todos los recursos de hello en el grupo de hello en el portal de Azure clásico. Como se muestra en la siguiente captura de pantalla, hello de hello grupo de recursos contiene una red virtual con tres máquinas virtuales, que se une toohello mismo conjunto de disponibilidad. grupo de Hello también contiene un equilibrador de carga, que tiene una dirección IP pública asociada.
    
    ![Hola aprovisiona el grupo de recursos en el portal de Azure clásico](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Instalar el cliente de Hola
Necesita **deisctl** toocontrol su Deis clúster. Aunque deisctl se instala automáticamente en todos los nodos de clúster de hello, es un deisctl de toouse buenas prácticas en un equipo administrativo independiente. Además, dado que todos los nodos se configuran con solo las direcciones IP privadas, deberá toouse SSH túnel a través del equilibrador de carga de hello, que tiene una dirección IP pública, las máquinas de nodo de tooconnect toohello. Hello siguientes son Hola pasos de configuración de deisctl en una máquina virtual o física Ubuntu independiente.

1. Instalar deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Agregue al agente toossh de clave privada:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Configure deisctl:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

plantilla de Hello define reglas NAT de entrada que se asignan 2223 tooinstance 1, 2224 tooinstance 2 y 2225 tooinstance 3. Esto proporciona redundancia para usar la herramienta de deisctl Hola. Puede examinar estas reglas en el Portal de Azure clásico:

![Reglas NAT en el equilibrador de carga de Hola](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Actualmente plantilla Hola solo admite clústeres de 3 nodos. Esto es debido a una limitación en la definición de la regla NAT de la plantilla del Administrador de recursos de Azure, que no admite la sintaxis del bucle.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Instale e inicie hello Deis plataforma
Ahora puede usar deisctl tooinstall e iniciar hello Deis plataforma:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Plataforma de saludo inicial tarda un tiempo (hasta 10 minutos). Especialmente, al iniciar el servicio del generador de hello puede tardar mucho tiempo. Y a veces tarda unos toosucceed intentos: operación Hola parezca toohang, pruebe a escribir `ctrl+c` toobreak ejecución de comando de Hola y vuelva a intentarlo.
> 
> 

Puede usar `deisctl list` tooverify si todos los servicios se están ejecutando:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

¡Enhorabuena! Ahora ya dispone de un clúster Deis en ejecución en Azure. A continuación, vamos a implementar un clúster de Go application toosee hello en acción de ejemplo.

## <a name="deploy-and-scale-a-hello-world-application"></a>Implementar y escalar una aplicación Hello World
Hello pasos siguientes muestran cómo toodeploy "Hola mundo" vaya clúster toohello de aplicación. Hola pasos se basan en [Deis documentación](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Para hello enrutamiento malla toowork correctamente, deberá toohave un registro de un comodín para el dominio que apunta toohello IP pública Hola de equilibrador de carga. Hello captura de pantalla siguiente muestra hello un registro de un registro de dominio de ejemplo en GoDaddy:
   
    ![Registro de Godaddy A](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Instalar deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Cree una nueva clave SSH y, a continuación, agregue hello tooGitHub de clave pública (por supuesto, también se puede reutilizar las claves existentes). toocreate un nuevo par de claves de SSH, use:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Agregar id_rsa.pub u Hola de clave pública de su elección, tooGitHub. Puede hacerlo mediante el uso de hello agregar SSH clave botón en la pantalla de configuración de claves SSH:
   
   ![Clave de GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Registre un nuevo usuario:
   
        deis register http://deis.[your domain]
   <p />
6. Agregue la clave SSH hello:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Cree una aplicación.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.inserción de git Hola desencadenará Docker imágenes toobe compiladas e implementadas, que le llevará unos minutos. Desde mi experiencia, en ocasiones, puede quedar paso 10 (repositorio de Pushing imágenes tooprivate). Cuando esto ocurre, puede detener el proceso de hello, remove Hola aplicación usando ' deis aplicaciones: destruir – a <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind el nombre de saludo de la aplicación. Si todo funciona, debería ver algo parecido a Hola siguiente al final de Hola de salidas de comandos:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Compruebe si funciona la aplicación hello:
   
        curl -S http://[your application name].[your domain]
   Debería ver lo siguiente:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Escala Hola aplicación too3 instancias:
    
        deis scale cmd=3
    <p />
11. Si lo desea, puede usar deis info tooexamine detalles de la aplicación. Hello resultados siguientes están en la implementación de aplicación:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Pasos siguientes
En este artículo le guía a través de todos los tooprovision de pasos de hello Deis un nuevo clúster en Azure mediante una plantilla de Azure Resource Manager. plantilla de Hello admite la redundancia en herramientas de conexiones, así como para las aplicaciones implementadas de equilibrio de carga. plantilla de Hello también evita el uso de direcciones IP públicas en los nodos de miembro, lo que ahorra valiosos recursos de IP pública y proporciona un entorno más seguro a las aplicaciones de toohost. toolearn más información, vea Hola siguientes artículos:

[Información general sobre Azure Resource Manager][resource-group-overview]  
[¿Cómo toouse Hola CLI de Azure][azure-command-line-tools]  
[Uso de Azure PowerShell con Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
