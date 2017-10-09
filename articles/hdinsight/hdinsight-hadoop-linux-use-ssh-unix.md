---
title: aaaUse SSH con Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Puede acceder a HDInsight mediante Secure Shell (SSH). Este documento proporciona información sobre la conexión tooHDInsight con hello ssh y comandos de scp de los clientes de Windows, Linux, Unix o macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "comandos hadoop en linux, comandos hadoop linux, hadoop macos, ssh hadoop, ssh hadoop clúster"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Conectar tooHDInsight (Hadoop) mediante SSH

Obtenga información acerca de cómo toouse [Shell seguro (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely conectar tooHadoop en HDInsight de Azure. 

HDInsight puede usar (Ubuntu) de Linux como sistema operativo de Hola para nodos de clúster de Hadoop de Hola. Hello siguiente tabla contiene información de dirección y el puerto de hello necesaria cuando se conecta con un cliente de SSH de HDInsight basados en tooLinux:

| Dirección | Port | Se conecta a... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Nodo perimetral (R Server en HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Nodo perimetral (cualquier otro tipo de clúster, si existe un nodo perimetral) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Nodo principal primario |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Nodo principal secundario |

> [!NOTE]
> Reemplace `<edgenodename>` con el nombre de hello del nodo de hello borde.
>
> Reemplace `<clustername>` con nombre hello del clúster.
>
> Si el clúster contiene un nodo del borde, se recomienda que se __siempre se conectará el nodo del borde de toohello__ mediante SSH. los nodos principales de Hello hospedan servicios de mantenimiento crítico toohello de Hadoop. nodo de Hello borde ejecuta solo lo que incluya en él.
>
> Para más información, consulte [Uso de nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>Clientes SSH

Los sistemas Linux, Unix y macOS proporcionan hello `ssh` y `scp` comandos. Hola `ssh` cliente es frecuente toocreate una sesión remota de línea de comandos con un sistema basado en Unix o Linux. Hola `scp` cliente es usado toosecurely copiar archivos entre el sistema remoto hello y cliente.

Microsoft Windows no proporciona un cliente de SSH de forma predeterminada. Hola `ssh` y `scp` los clientes están disponibles para Windows a través de los siguientes paquetes de saludo:

* [Shell de nube Azure](../cloud-shell/quickstart.md): Hola nube Shell proporciona un entorno intensiva de errores en el explorador y proporciona hello `ssh`, `scp`y otros comandos comunes de Linux.

* [Bash en Ubuntu en Windows 10](https://msdn.microsoft.com/commandline/wsl/about): Hola `ssh` y `scp` comandos están disponibles a través de hello intensiva de errores en la línea de comandos de Windows.

* [GIT (https://git-scm.com/)](https://git-scm.com/): Hola `ssh` y `scp` comandos están disponibles a través de la línea de comandos de GitBash Hola.

* [Escritorio de GitHub (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` y `scp` comandos están disponibles a través de la línea de comandos de Shell de GitHub Hola. Escritorio de GitHub puede ser configurado toouse Bash, Hola símbolo del sistema de Windows o PowerShell como línea de comandos Hola Hola Git Shell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): equipo de PowerShell de hello es migrar OpenSSH tooWindows y proporciona versiones de prueba.

    > [!WARNING]
    > paquete de OpenSSH Hola incluye componentes de servidor SSH de hello, `sshd`. Este componente inicia un servidor SSH en el sistema, lo que permite a otros usuarios tooconnect tooit. No configurar este componente o abrir el puerto 22 a menos que desee toohost un servidor SSH en el sistema. No es necesario toocommunicate con HDInsight.

También hay varios clientes SSH gráficos, como [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) y [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Aunque estos clientes pueden ser utilizados tooconnect tooHDInsight, proceso de Hola de conexión es diferente a usar hello `ssh` utilidad. Para obtener más información, consulte la documentación de Hola de cliente gráfica Hola que está usando.

## <a id="sshkey"></a>Autenticación: claves SSH

Utilizan SSH claves [criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate sesiones SSH. Claves de SSH son más seguras que las contraseñas y proporcionan un clúster de Hadoop de tooyour de acceso de forma sencilla toosecure.

Si su cuenta SSH se protege utilizando una clave, el cliente de hello debe proporcionar Hola que coinciden con clave privada al conectarse:

* La mayoría de los clientes puede ser toouse configurado un __clave predeterminada__. Por ejemplo, hello `ssh` cliente busca una clave privada en `~/.ssh/id_rsa` en entornos Linux y Unix.

* Puede especificar hello __clave privada de ruta de acceso tooa__. Con hello `ssh` client, hello `-i` parámetro es tooprivate clave de toospecify usado Hola ruta de acceso. Por ejemplo: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Si tiene __varias claves privadas__ para su uso con distintos servidores, considere la posibilidad de usar una utilidad como [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Hola `ssh-agent` utilidad puede ser usado tooautomatically Hola seleccione clave toouse al establecer una sesión de SSH.

> [!IMPORTANT]
>
> Si se protege la clave privada con una frase de contraseña, debe escribir frase de contraseña de hello cuando se usa la clave de Hola. Utilidades como `ssh-agent` puede almacenar en caché las contraseñas de Hola para su comodidad.

### <a name="create-an-ssh-key-pair"></a>Creación de un par de claves SSH

Hola de uso `ssh-keygen` comando toocreate archivos clave pública y privada. Hello siguiente comando genera un par de claves de RSA de 2048 bits que puede utilizarse con HDInsight:

    ssh-keygen -t rsa -b 2048

Le pedirá información durante el proceso de creación de claves de Hola. Por ejemplo, donde se almacenan las claves de Hola o si toouse una frase de contraseña. Una vez completado el proceso de hello, se crean dos archivos; una clave pública y una clave privada.

* Hola __clave pública__ es toocreate usado en un clúster de HDInsight. clave pública de Hello tiene una extensión de `.pub`.

* Hola __clave privada__ es tooauthenticate usado al clúster de HDInsight de toohello de cliente.

> [!IMPORTANT]
> Puede proteger las claves con una frase de contraseña. Una frase de contraseña es efectivamente una contraseña de la clave privada. Incluso si un usuario obtiene la clave privada, deben tener claves de hello frase de contraseña toouse Hola.

### <a name="create-hdinsight-using-hello-public-key"></a>Crear utilizando la clave pública de Hola de HDInsight

| Método de creación | ¿Cómo toouse Hola clave pública |
| ------- | ------- |
| **Portal de Azure** | Desactive la opción __usar la misma contraseña como inicio de sesión de clúster__y, a continuación, seleccione __clave pública__ como tipo de autenticación de SSH de Hola. Por último, seleccione el archivo de clave pública de Hola o pegar contenido de texto de Hola de archivo hello en hello __clave pública SSH__ campo.</br>![Cuadro de diálogo de clave pública SSH en la creación de clústeres de HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Hola de uso `-SshPublicKey` parámetro de hello `New-AzureRmHdinsightCluster` contenido Hola de cmdlet y pase de clave pública de hello como una cadena.|
| **CLI de Azure 1.0** | Hola de uso `--sshPublicKey` parámetro de hello `azure hdinsight cluster create` de comandos y pasar los contenidos de Hola de clave pública de hello como una cadena. |
| **Plantilla de Resource Manager** | Para obtener un ejemplo del uso de claves SSH con una plantilla, consulte la [implementación de HDInsight en Linux con una clave SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/). Hola `publicKeys` elemento Hola [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) archivo es tooAzure de claves de hello toopass usado al crear el clúster de Hola. |

## <a id="sshpassword"></a>Autenticación: contraseña

Las cuentas SSH se pueden proteger mediante una contraseña. Cuando se conecta tooHDInsight mediante SSH, son contraseña de hello tooenter solicitadas.

> [!WARNING]
> No se recomienda usar autenticación de contraseña para SSH. Las contraseñas pueden ser adivinadas y son vulnerables toobrute ataques de fuerza. En su lugar, recomendamos que use [claves SSH para la autenticación](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Creación de HDInsight usando una contraseña

| Método de creación | ¿Cómo toospecify Hola contraseña |
| --------------- | ---------------- |
| **Portal de Azure** | De forma predeterminada, Hola cuenta de usuario SSH tiene Hola misma contraseña que la cuenta de inicio de sesión de clúster de Hola. toouse una contraseña diferente, desactive la opción __usar la misma contraseña como inicio de sesión de clúster__y a continuación, escriba la contraseña de Hola Hola __contraseña SSH__ campo.</br>![Cuadro de diálogo de contraseña SSH en la creación de clústeres de HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Hola de uso `--SshCredential` parámetro de hello `New-AzureRmHdinsightCluster` cmdlet y pasar un `PSCredential` objeto que contiene el nombre de cuenta de usuario SSH de hello y una contraseña. |
| **CLI de Azure 1.0** | Hola de uso `--sshPassword` parámetro de hello `azure hdinsight cluster create` comando y proporcionar el valor de la contraseña de Hola. |
| **Plantilla de Resource Manager** | Para obtener un ejemplo del uso de contraseña con una plantilla, consulte la [implementación de HDInsight en Linux con una contraseña SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). Hola `linuxOperatingSystemProfile` elemento Hola [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) archivo es utilizado toopass Hola SSH cuenta nombre y la contraseña tooAzure al crear el clúster de Hola.|

### <a name="change-hello-ssh-password"></a>Cambiar la contraseña de SSH Hola

Para obtener información acerca de cómo cambiar la contraseña de cuenta de usuario SSH de hello, vea hello __cambiar contraseñas__ sección de hello [administrar HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) documento.

## <a id="domainjoined"></a>Autenticación: HDInsight unido a un dominio

Si usas un __Unidos a un dominio de clúster de HDInsight__, debe usar hello `kinit` comando después de conectarse mediante SSH. Este comando le pide un usuario de dominio y una contraseña y la sesión autentica con el dominio de Active Directory de Azure de hello asociada Hola clúster.

Para más información, consulte [Configuración de clústeres de HDInsight unidos a un dominio](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Conectar toonodes

Hola nodos principales y el nodo del borde (si hay alguno) puede tener acceso a través de hello internet en los puertos 22 y 23.

* Cuando se conecte toohello __head nodos__, utilizar el puerto __22__ tooconnect toohello principal head nodo y el puerto __23__ nodo principal de tooconnect toohello secundaria. Hola toouse de nombre de dominio completo es `clustername-ssh.azurehdinsight.net`, donde `clustername` es Hola nombre del clúster.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Cuando connectiung toohello __nodo del borde__, use el puerto de 22. Hola nombre de dominio completo es `edgenodename.clustername-ssh.azurehdinsight.net`, donde `edgenodename` es el nombre que proporcionó al crear nodo del borde Hola. `clustername`es el nombre de Hola de clúster de Hola.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> ejemplos de Hello anterior se supone que está usando la autenticación de contraseña, o que la autenticación de certificado se está produciendo automáticamente. Si usa un par de claves SSH para la autenticación y no se utiliza automáticamente el certificado de hello, usar hello `-i` la clave privada del parámetro toospecify Hola. Por ejemplo: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Una vez conectado, mensaje de Hola cambia tooindicate Hola SSH hello y nombre de nodo de usuario a que está conectado. Por ejemplo, cuando se conecta toohello de nodo principal principal como `sshuser`, mensaje de Hola es `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Conectar tooworker y nodos de Zookeeper

nodos de trabajador de Hola y Hola a Zookeeper nodos no sean directamente accesibles desde internet. Puede tener acceso desde nodos principales del clúster de Hola o nodos de borde. son las siguientes de Hello tooconnect tooother nodos de hello pasos generales:

1. Utilizar SSH tooconnect tooa head o borde nodo:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Desde Hola head de toohello conexión SSH o nodo del borde, use hello `ssh` comando tooconnect tooa trabajo nodo Hola clúster:

        ssh sshuser@wn0-myhdi

    tooretrieve una lista de nombres de dominio de Hola de nodos de hello en clúster de hello, vea hello [HDInsight administrar mediante el uso de Hola API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) documento.

Si Hola cuenta SSH se protege utilizando un __contraseña__, escriba la contraseña de hello al conectarse.

Si Hola cuenta SSH se protege utilizando __claves SSH__, asegúrese de que el reenvío de SSH está habilitado en el cliente de Hola.

> [!NOTE]
> Otra manera de toodirectly tener acceso a todos los nodos de clúster de hello es tooinstall HDInsight en una red Virtual de Azure. A continuación, puede unir el equipo remoto toohello mismo virtual de red y tener acceso directamente a todos los nodos de clúster de Hola.
>
> Para más información, consulte el documento sobre el [uso de una red virtual con HDInsight](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>Configuración del reenvío del agente SSH

> [!IMPORTANT]
> Hello pasos siguientes supone un sistema basado en UNIX o Linux y trabajar con intensiva de errores en Windows 10. Si estos pasos no funcionan para su sistema, puede necesitar tooconsult documentación de hello para el cliente SSH.

1. Abra `~/.ssh/config`con un editor de texto. Si este archivo no existe, puede crearlo si escribe `touch ~/.ssh/config` en la línea de comandos.

2. Agregar Hola después texto toohello `config` archivo.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Reemplace hello __Host__ información con la dirección de hello del nodo de hello conectarse toousing SSH. Hola anterior en el ejemplo se usa el nodo del borde de Hola. Esta entrada configura el reenvío para el nodo especificado Hola de agente SSH.

3. Agente SSH reenvío mediante el uso de hello siguiente comando de hello terminal de prueba:

        echo "$SSH_AUTH_SOCK"

    Este comando devuelve información toohello similar siguiente texto:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Si no se devuelve nada, `ssh-agent` no se está ejecutando. Para obtener más información, consulte la información de las secuencias de comandos de inicio de agente de hello en [mediante ssh-agent con ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) o consulte la documentación del cliente SSH.

4. Una vez haya comprobado que **ssh agente** está ejecutando, Hola de uso después de tooadd el agente de toohello clave privada SSH:

        ssh-add ~/.ssh/id_rsa

    Si la clave privada se almacena en un archivo diferente, reemplace `~/.ssh/id_rsa` con hello ruta toohello al archivo.

5. Conecte toohello nodo del borde de clúster o nodos principales del uso de SSH. A continuación, usar tooconnect tooa trabajo de hello SSH comando o nodo zookeeper. conexión de Hola se establece con la clave de hello reenviado.

## <a name="copy-files"></a>Copiar archivos

Hola `scp` utilidad puede ser usado toocopy archivos tooand de nodos individuales en el clúster de Hola. Por ejemplo, Hola después comando copias hello `test.txt` directorio nodo principal de la principal de toohello Hola sistema local:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Porque no se especifica ninguna ruta de acceso después de hello `:`, se coloca el archivo hello Hola `sshuser` directorio particular.

Hola siguientes ejemplo copias hello `test.txt` archivo de hello `sshuser` directorio particular en el sistema local de hello principal del nodo principal toohello:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`solo se puede acceder a sistema de archivos de Hola de nodos individuales dentro de clúster de Hola. No puede ser datos de tooaccess usado en el almacenamiento de hello HDFS compatible para clúster Hola.
>
> Usar `scp` cuando necesite tooupload un recurso para su uso desde una sesión de SSH. Por ejemplo, cargar un script de Python y, a continuación, ejecutar script de Hola desde una sesión de SSH.
>
> Para obtener información sobre cómo cargar directamente los datos en hello almacenamiento HDFS compatible, consulte Hola siguientes documentos:
>
> * [HDInsight mediante Azure Storage](hdinsight-hadoop-use-blob-storage.md).
>
> * [HDInsight mediante Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Pasos siguientes

* [Uso de la tunelización de SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)
* [Uso de una red virtual con HDInsight](hdinsight-extend-hadoop-virtual-network.md)
* [Uso de nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node)