---
title: Uso de SSH con Hadoop en Azure HDInsight | Microsoft Docs
description: "Puede acceder a HDInsight mediante Secure Shell (SSH). Este documento proporciona información sobre cómo conectarse a HDInsight utilizando los comandos ssh y scp desde clientes Windows, Linux, Unix o macOS."
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
ms.openlocfilehash: df0feb51469333bac42c779d860192d46f24ac62
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a><span data-ttu-id="9499a-105">Conexión a través de SSH con HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="9499a-105">Connect to HDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="9499a-106">Aprenda a usar [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) para conectarse de forma segura a Hadoop en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9499a-106">Learn how to use [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) to securely connect to Hadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="9499a-107">HDInsight puede usar Linux (Ubuntu) como sistema operativo para los nodos dentro del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9499a-107">HDInsight can use Linux (Ubuntu) as the operating system for nodes within the Hadoop cluster.</span></span> <span data-ttu-id="9499a-108">La tabla siguiente contiene la información de dirección y puerto que es necesaria para conectarse a HDInsight basado en Linux mediante un cliente SSH:</span><span class="sxs-lookup"><span data-stu-id="9499a-108">The following table contains the address and port information needed when connecting to Linux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="9499a-109">Dirección</span><span class="sxs-lookup"><span data-stu-id="9499a-109">Address</span></span> | <span data-ttu-id="9499a-110">Port</span><span class="sxs-lookup"><span data-stu-id="9499a-110">Port</span></span> | <span data-ttu-id="9499a-111">Se conecta a...</span><span class="sxs-lookup"><span data-stu-id="9499a-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="9499a-112">22</span><span class="sxs-lookup"><span data-stu-id="9499a-112">22</span></span> | <span data-ttu-id="9499a-113">Nodo perimetral (R Server en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9499a-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9499a-114">22</span><span class="sxs-lookup"><span data-stu-id="9499a-114">22</span></span> | <span data-ttu-id="9499a-115">Nodo perimetral (cualquier otro tipo de clúster, si existe un nodo perimetral)</span><span class="sxs-lookup"><span data-stu-id="9499a-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9499a-116">22</span><span class="sxs-lookup"><span data-stu-id="9499a-116">22</span></span> | <span data-ttu-id="9499a-117">Nodo principal primario</span><span class="sxs-lookup"><span data-stu-id="9499a-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9499a-118">23</span><span class="sxs-lookup"><span data-stu-id="9499a-118">23</span></span> | <span data-ttu-id="9499a-119">Nodo principal secundario</span><span class="sxs-lookup"><span data-stu-id="9499a-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="9499a-120">Reemplace `<edgenodename>` con el nombre del nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="9499a-120">Replace `<edgenodename>` with the name of the edge node.</span></span>
>
> <span data-ttu-id="9499a-121">Reemplace `<clustername>` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-121">Replace `<clustername>` with the name of your cluster.</span></span>
>
> <span data-ttu-id="9499a-122">Si el clúster contiene un nodo perimetral, se recomienda que __siempre se conecte al nodo perimetral__ mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-122">If your cluster contains an edge node, we recommend that you __always connect to the edge node__ using SSH.</span></span> <span data-ttu-id="9499a-123">Los nodos principales hospedan servicios que son críticos para el estado de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9499a-123">The head nodes host services that are critical to the health of Hadoop.</span></span> <span data-ttu-id="9499a-124">El nodo perimetral ejecuta solo lo que incluya en él.</span><span class="sxs-lookup"><span data-stu-id="9499a-124">The edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="9499a-125">Para más información, consulte [Uso de nodos perimetrales en HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span><span class="sxs-lookup"><span data-stu-id="9499a-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="9499a-126">Clientes SSH</span><span class="sxs-lookup"><span data-stu-id="9499a-126">SSH clients</span></span>

<span data-ttu-id="9499a-127">Los sistemas Linux, Unix y macOS proporcionan los comandos `ssh` y `scp`.</span><span class="sxs-lookup"><span data-stu-id="9499a-127">Linux, Unix, and macOS systems provide the `ssh` and `scp` commands.</span></span> <span data-ttu-id="9499a-128">El cliente `ssh` se usa normalmente para crear una sesión de línea de comandos remota con un sistema basado en Unix o Linux.</span><span class="sxs-lookup"><span data-stu-id="9499a-128">The `ssh` client is commonly used to create a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="9499a-129">El cliente `scp` se usa para copiar archivos entre el cliente y el sistema remoto de forma segura.</span><span class="sxs-lookup"><span data-stu-id="9499a-129">The `scp` client is used to securely copy files between your client and the remote system.</span></span>

<span data-ttu-id="9499a-130">Microsoft Windows no proporciona un cliente de SSH de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9499a-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="9499a-131">Los clientes `ssh` y `scp` están disponibles para Windows a través de los siguientes paquetes:</span><span class="sxs-lookup"><span data-stu-id="9499a-131">The `ssh` and `scp` clients are available for Windows through the following packages:</span></span>

* <span data-ttu-id="9499a-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): Cloud Shell proporciona un entorno Bash en el explorador y proporciona los comandos `ssh`, `scp` y otros comandos comunes de Linux.</span><span class="sxs-lookup"><span data-stu-id="9499a-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): The Cloud Shell provides a Bash environment in your browser, and provides the `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="9499a-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about) (Bash en Ubuntu en Windows 10): Los comandos `ssh` y `scp` están disponibles a través de Bash en la línea de comandos de Windows.</span><span class="sxs-lookup"><span data-stu-id="9499a-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): The `ssh` and `scp` commands are available through the Bash on Windows command line.</span></span>

* <span data-ttu-id="9499a-134">[Git (https://git-scm.com/)](https://git-scm.com/): Los comandos `ssh` y `scp` están disponibles a través de la línea de comandos GitBash.</span><span class="sxs-lookup"><span data-stu-id="9499a-134">[Git (https://git-scm.com/)](https://git-scm.com/): The `ssh` and `scp` commands are available through the GitBash command line.</span></span>

* <span data-ttu-id="9499a-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) Los comandos `ssh` y `scp` están disponibles a través de la línea de comandos GitHub Shell.</span><span class="sxs-lookup"><span data-stu-id="9499a-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) The `ssh` and `scp` commands are available through the GitHub Shell command line.</span></span> <span data-ttu-id="9499a-136">GitHub Desktop se puede configurar para usar Bash, el símbolo del sistema de Windows, o PowerShell como línea de comandos para el Git Shell.</span><span class="sxs-lookup"><span data-stu-id="9499a-136">GitHub Desktop can be configured to use Bash, the Windows Command Prompt, or PowerShell as the command line for the Git Shell.</span></span>

* <span data-ttu-id="9499a-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): el equipo de PowerShell está realizando la portabilidad de OpenSSH a Windows y proporciona versiones de prueba.</span><span class="sxs-lookup"><span data-stu-id="9499a-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): The PowerShell team is porting OpenSSH to Windows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9499a-138">El paquete OpenSSH incluye el componente de servidor SSH, `sshd`.</span><span class="sxs-lookup"><span data-stu-id="9499a-138">The OpenSSH package includes the SSH server component, `sshd`.</span></span> <span data-ttu-id="9499a-139">Este componente inicia un servidor SSH en el sistema, lo que permite a otros conectarse a él.</span><span class="sxs-lookup"><span data-stu-id="9499a-139">This component starts an SSH server on your system, allowing others to connect to it.</span></span> <span data-ttu-id="9499a-140">No configure este componente o abra el puerto 22 a menos que desee hospedar un servidor SSH en el sistema.</span><span class="sxs-lookup"><span data-stu-id="9499a-140">Do not configure this component or open port 22 unless you want to host an SSH server on your system.</span></span> <span data-ttu-id="9499a-141">No es necesario para comunicarse con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9499a-141">It is not required to communicate with HDInsight.</span></span>

<span data-ttu-id="9499a-142">También hay varios clientes SSH gráficos, como [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) y [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span><span class="sxs-lookup"><span data-stu-id="9499a-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="9499a-143">Aunque estos clientes se pueden usar para conectar con HDInsight, el proceso de conexión es diferente a usar la utilidad `ssh`.</span><span class="sxs-lookup"><span data-stu-id="9499a-143">While these clients can be used to connect to HDInsight, the process of connecting is different than using the `ssh` utility.</span></span> <span data-ttu-id="9499a-144">Para más información, consulte la documentación del cliente gráfico que esté usando.</span><span class="sxs-lookup"><span data-stu-id="9499a-144">For more information, see the documentation of the graphical client you are using.</span></span>

## <span data-ttu-id="9499a-145"><a id="sshkey"></a>Autenticación: claves SSH</span><span class="sxs-lookup"><span data-stu-id="9499a-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="9499a-146">Las claves SSH utilizan [criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) para autenticar las sesiones de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) to authenticate SSH sessions.</span></span> <span data-ttu-id="9499a-147">Las claves SSH son más seguras que las contraseñas y proporcionan una manera fácil para proteger el acceso al clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9499a-147">SSH keys are more secure than passwords, and provide an easy way to secure access to your Hadoop cluster.</span></span>

<span data-ttu-id="9499a-148">Si su cuenta SSH se protege utilizando una clave, el cliente tiene que proporcionar la clave privada correspondiente al conectarse:</span><span class="sxs-lookup"><span data-stu-id="9499a-148">If your SSH account is secured using a key, the client must provide the matching private key when you connect:</span></span>

* <span data-ttu-id="9499a-149">La mayoría de los clientes pueden configurarse para utilizar una __clave predeterminada__.</span><span class="sxs-lookup"><span data-stu-id="9499a-149">Most clients can be configured to use a __default key__.</span></span> <span data-ttu-id="9499a-150">Por ejemplo, el cliente `ssh` busca una clave privada en `~/.ssh/id_rsa` en entornos Linux y Unix.</span><span class="sxs-lookup"><span data-stu-id="9499a-150">For example, the `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="9499a-151">Puede especificar la __ruta de acceso a una clave privada__.</span><span class="sxs-lookup"><span data-stu-id="9499a-151">You can specify the __path to a private key__.</span></span> <span data-ttu-id="9499a-152">Con el cliente `ssh`, el parámetro `-i` se utiliza para especificar la ruta de acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9499a-152">With the `ssh` client, the `-i` parameter is used to specify the path to private key.</span></span> <span data-ttu-id="9499a-153">Por ejemplo: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9499a-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="9499a-154">Si tiene __varias claves privadas__ para su uso con distintos servidores, considere la posibilidad de usar una utilidad como [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span><span class="sxs-lookup"><span data-stu-id="9499a-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="9499a-155">La utilidad `ssh-agent` se puede usar para seleccionar automáticamente la clave que se usará al establecer una sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-155">The `ssh-agent` utility can be used to automatically select the key to use when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="9499a-156">Si se protege la clave privada con una frase de contraseña, tiene que escribir la frase de contraseña cuando se use la clave.</span><span class="sxs-lookup"><span data-stu-id="9499a-156">If you secure your private key with a passphrase, you must enter the passphrase when using the key.</span></span> <span data-ttu-id="9499a-157">Utilidades como `ssh-agent` puede almacenar en caché la contraseña para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="9499a-157">Utilities such as `ssh-agent` can cache the password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="9499a-158">Creación de un par de claves SSH</span><span class="sxs-lookup"><span data-stu-id="9499a-158">Create an SSH key pair</span></span>

<span data-ttu-id="9499a-159">Use el comando `ssh-keygen` para crear archivos de clave pública y privada.</span><span class="sxs-lookup"><span data-stu-id="9499a-159">Use the `ssh-keygen` command to create public and private key files.</span></span> <span data-ttu-id="9499a-160">El comando siguiente genera un par de claves de RSA de 2048 bits que puede utilizarse con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9499a-160">The following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="9499a-161">Se le pedirá información durante el proceso de creación de claves.</span><span class="sxs-lookup"><span data-stu-id="9499a-161">You are prompted for information during the key creation process.</span></span> <span data-ttu-id="9499a-162">Por ejemplo, dónde se almacenan las claves o si se debe usar una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-162">For example, where the keys are stored or whether to use a passphrase.</span></span> <span data-ttu-id="9499a-163">Una vez completado el proceso, se crean dos archivos: una clave pública y una clave privada.</span><span class="sxs-lookup"><span data-stu-id="9499a-163">After the process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="9499a-164">La __clave pública__ se utiliza para crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9499a-164">The __public key__ is used to create an HDInsight cluster.</span></span> <span data-ttu-id="9499a-165">La clave pública tiene una extensión `.pub`.</span><span class="sxs-lookup"><span data-stu-id="9499a-165">The public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="9499a-166">La __clave privada__ se utiliza para autenticar el cliente al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9499a-166">The __private key__ is used to authenticate your client to the HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9499a-167">Puede proteger las claves con una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="9499a-168">Una frase de contraseña es efectivamente una contraseña de la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9499a-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="9499a-169">Incluso si alguien obtiene la clave privada, tienen que tener la frase de contraseña para poder usar la clave.</span><span class="sxs-lookup"><span data-stu-id="9499a-169">Even if someone obtains your private key, they must have the passphrase to use the key.</span></span>

### <a name="create-hdinsight-using-the-public-key"></a><span data-ttu-id="9499a-170">Creación de HDInsight usando la clave pública</span><span class="sxs-lookup"><span data-stu-id="9499a-170">Create HDInsight using the public key</span></span>

| <span data-ttu-id="9499a-171">Método de creación</span><span class="sxs-lookup"><span data-stu-id="9499a-171">Creation method</span></span> | <span data-ttu-id="9499a-172">Cómo usar la clave pública</span><span class="sxs-lookup"><span data-stu-id="9499a-172">How to use the public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="9499a-173">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="9499a-173">**Azure portal**</span></span> | <span data-ttu-id="9499a-174">Desactive la opción __Utilizar la misma contraseña que en el inicio de sesión del clúster__y, a continuación, seleccione __Clave pública__ como el tipo de autenticación de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as the SSH authentication type.</span></span> <span data-ttu-id="9499a-175">Por último, seleccione el archivo de clave pública o pegue el contenido de texto del archivo en el campo __Clave pública SSH__.</span><span class="sxs-lookup"><span data-stu-id="9499a-175">Finally, select the public key file or paste the text contents of the file in the __SSH public key__ field.</span></span></br><span data-ttu-id="9499a-176">![Cuadro de diálogo de clave pública SSH en la creación de clústeres de HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="9499a-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="9499a-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9499a-177">**Azure PowerShell**</span></span> | <span data-ttu-id="9499a-178">Use el parámetro `-SshPublicKey` del cmdlet `New-AzureRmHdinsightCluster` y pase el contenido de la clave pública como una cadena.</span><span class="sxs-lookup"><span data-stu-id="9499a-178">Use the `-SshPublicKey` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass the contents of the public key as a string.</span></span>|
| <span data-ttu-id="9499a-179">**CLI de Azure 1.0**</span><span class="sxs-lookup"><span data-stu-id="9499a-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9499a-180">Use el parámetro `--sshPublicKey` del comando `azure hdinsight cluster create` y pase el contenido de la clave pública como una cadena.</span><span class="sxs-lookup"><span data-stu-id="9499a-180">Use the `--sshPublicKey` parameter of the `azure hdinsight cluster create` command and pass the contents of the public key as a string.</span></span> |
| <span data-ttu-id="9499a-181">**Plantilla de Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="9499a-181">**Resource Manager Template**</span></span> | <span data-ttu-id="9499a-182">Para obtener un ejemplo del uso de claves SSH con una plantilla, consulte la [implementación de HDInsight en Linux con una clave SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span><span class="sxs-lookup"><span data-stu-id="9499a-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="9499a-183">El elemento `publicKeys` en el archivo [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) se usa para pasar las claves a Azure al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-183">The `publicKeys` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used to pass the keys to Azure when creating the cluster.</span></span> |

## <span data-ttu-id="9499a-184"><a id="sshpassword"></a>Autenticación: contraseña</span><span class="sxs-lookup"><span data-stu-id="9499a-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="9499a-185">Las cuentas SSH se pueden proteger mediante una contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="9499a-186">Cuando se conecta a HDInsight usando SSH, se le pedirá que escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-186">When you connect to HDInsight using SSH, you are prompted to enter the password.</span></span>

> [!WARNING]
> <span data-ttu-id="9499a-187">No se recomienda usar autenticación de contraseña para SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="9499a-188">Las contraseñas se pueden adivinar y son vulnerables a ataques por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="9499a-188">Passwords can be guessed and are vulnerable to brute force attacks.</span></span> <span data-ttu-id="9499a-189">En su lugar, recomendamos que use [claves SSH para la autenticación](#sshkey).</span><span class="sxs-lookup"><span data-stu-id="9499a-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="9499a-190">Creación de HDInsight usando una contraseña</span><span class="sxs-lookup"><span data-stu-id="9499a-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="9499a-191">Método de creación</span><span class="sxs-lookup"><span data-stu-id="9499a-191">Creation method</span></span> | <span data-ttu-id="9499a-192">Cómo especificar la contraseña</span><span class="sxs-lookup"><span data-stu-id="9499a-192">How to specify the password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="9499a-193">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="9499a-193">**Azure portal**</span></span> | <span data-ttu-id="9499a-194">De forma predeterminada, la cuenta de usuario SSH tiene la misma contraseña que la cuenta de inicio de sesión de clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-194">By default, the SSH user account has the same password as the cluster login account.</span></span> <span data-ttu-id="9499a-195">Para usar una contraseña diferente, desactive la opción __Utilizar la misma contraseña que en el inicio de sesión del clúster__y, a continuación, escriba la contraseña en el campo __Contraseña SSH__.</span><span class="sxs-lookup"><span data-stu-id="9499a-195">To use a different password, uncheck __Use same password as cluster login__, and then enter the password in the __SSH password__ field.</span></span></br><span data-ttu-id="9499a-196">![Cuadro de diálogo de contraseña SSH en la creación de clústeres de HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="9499a-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="9499a-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9499a-197">**Azure PowerShell**</span></span> | <span data-ttu-id="9499a-198">Use el parámetro `--SshCredential` del cmdlet `New-AzureRmHdinsightCluster` y pase un objeto `PSCredential` que contiene el nombre de cuenta de usuario SSH y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-198">Use the `--SshCredential` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains the SSH user account name and password.</span></span> |
| <span data-ttu-id="9499a-199">**CLI de Azure 1.0**</span><span class="sxs-lookup"><span data-stu-id="9499a-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9499a-200">Use el parámetro `--sshPassword` del comando `azure hdinsight cluster create` y proporcione el valor de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9499a-200">Use the `--sshPassword` parameter of the `azure hdinsight cluster create` command and provide the password value.</span></span> |
| <span data-ttu-id="9499a-201">**Plantilla de Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="9499a-201">**Resource Manager Template**</span></span> | <span data-ttu-id="9499a-202">Para obtener un ejemplo del uso de contraseña con una plantilla, consulte la [implementación de HDInsight en Linux con una contraseña SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span><span class="sxs-lookup"><span data-stu-id="9499a-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="9499a-203">El elemento `linuxOperatingSystemProfile` en el archivo [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) se usa para pasar el nombre de cuenta de SSH y la contraseña a Azure al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-203">The `linuxOperatingSystemProfile` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used to pass the SSH account name and password to Azure when creating the cluster.</span></span>|

### <a name="change-the-ssh-password"></a><span data-ttu-id="9499a-204">Cambio de contraseña de SSH</span><span class="sxs-lookup"><span data-stu-id="9499a-204">Change the SSH password</span></span>

<span data-ttu-id="9499a-205">Para información acerca de cómo cambiar la contraseña de cuenta de usuario SSH, consulte la sección __Cambio de contraseñas__ del documento sobre [administración de HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords).</span><span class="sxs-lookup"><span data-stu-id="9499a-205">For information on changing the SSH user account password, see the __Change passwords__ section of the [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="9499a-206"><a id="domainjoined"></a>Autenticación: HDInsight unido a un dominio</span><span class="sxs-lookup"><span data-stu-id="9499a-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="9499a-207">Si está usando un __clúster de HDInsight unido a un dominio__, tiene que utilizar el comando `kinit` después de conectarse con SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-207">If you are using a __domain-joined HDInsight cluster__, you must use the `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="9499a-208">Este comando le pide un usuario de dominio y una contraseña y autentica la sesión con el dominio de Azure Active Directory asociado con el clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-208">This command prompts you for a domain user and password, and authenticates your session with the Azure Active Directory domain associated with the cluster.</span></span>

<span data-ttu-id="9499a-209">Para más información, consulte [Configuración de clústeres de HDInsight unidos a un dominio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9499a-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-to-nodes"></a><span data-ttu-id="9499a-210">Conexión a nodos</span><span class="sxs-lookup"><span data-stu-id="9499a-210">Connect to nodes</span></span>

<span data-ttu-id="9499a-211">Los nodos principales y el nodo perimetral (si hay alguno) son accesibles a través de Internet en los puertos 22 y 23.</span><span class="sxs-lookup"><span data-stu-id="9499a-211">The head nodes and edge node (if there is one) can be accessed over the internet on ports 22 and 23.</span></span>

* <span data-ttu-id="9499a-212">Cuando se conecte a los __nodos principales__, use el puerto __22__ para conectarse al nodo principal primario y el puerto __23__ para conectarse al nodo principal secundario.</span><span class="sxs-lookup"><span data-stu-id="9499a-212">When connecting to the __head nodes__, use port __22__ to connect to the primary head node and port __23__ to connect to the secondary head node.</span></span> <span data-ttu-id="9499a-213">El nombre de dominio completo que se debe usar es `clustername-ssh.azurehdinsight.net`, donde `clustername` es el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-213">The fully qualified domain name to use is `clustername-ssh.azurehdinsight.net`, where `clustername` is the name of your cluster.</span></span>

    ```bash
    # Connect to primary head node
    # port not specified since 22 is the default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect to secondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="9499a-214">Al conectarse al __nodo perimetral__, utilice el puerto 22.</span><span class="sxs-lookup"><span data-stu-id="9499a-214">When connectiung to the __edge node__, use port 22.</span></span> <span data-ttu-id="9499a-215">El nombre de dominio completo es `edgenodename.clustername-ssh.azurehdinsight.net`, donde `edgenodename` es el nombre que proporcionó al crear el nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="9499a-215">The fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating the edge node.</span></span> <span data-ttu-id="9499a-216">`clustername` es el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-216">`clustername` is the name of the cluster.</span></span>

    ```bash
    # Connect to edge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="9499a-217">En los ejemplos anteriores se supone que está usando la autenticación con contraseña, o que la autenticación de certificados se está produciendo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9499a-217">The previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="9499a-218">Si usa un par de claves SSH para la autenticación y el certificado no se utiliza automáticamente, use el parámetro `-i` para especificar la clave privada.</span><span class="sxs-lookup"><span data-stu-id="9499a-218">If you use an SSH key-pair for authentication, and the certificate is not used automatically, use the `-i` parameter to specify the private key.</span></span> <span data-ttu-id="9499a-219">Por ejemplo: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9499a-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="9499a-220">Una vez conectado, el símbolo del sistema cambia para indicar el nombre de usuario SSH y el nodo al que está conectado.</span><span class="sxs-lookup"><span data-stu-id="9499a-220">Once connected, the prompt changes to indicate the SSH user name and the node you are connected to.</span></span> <span data-ttu-id="9499a-221">Por ejemplo, cuando se conecta al nodo principal primario como `sshuser`, el símbolo del sistema es `sshuser@hn0-clustername:~$`.</span><span class="sxs-lookup"><span data-stu-id="9499a-221">For example, when connected to the primary head node as `sshuser`, the prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-to-worker-and-zookeeper-nodes"></a><span data-ttu-id="9499a-222">Conexión a los nodos de Zookeeper y de trabajo</span><span class="sxs-lookup"><span data-stu-id="9499a-222">Connect to worker and Zookeeper nodes</span></span>

<span data-ttu-id="9499a-223">Los nodos de trabajo y los nodos de Zookeeper no son directamente accesibles desde Internet.</span><span class="sxs-lookup"><span data-stu-id="9499a-223">The worker nodes and Zookeeper nodes are not directly accessible from the internet.</span></span> <span data-ttu-id="9499a-224">Solo se puede acceder a ellos desde los nodos principales y perimetrales del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-224">They can be accessed from the cluster head nodes or edge nodes.</span></span> <span data-ttu-id="9499a-225">Estos son los pasos generales para conectarse a otros nodos:</span><span class="sxs-lookup"><span data-stu-id="9499a-225">The following are the general steps to connect to other nodes:</span></span>

1. <span data-ttu-id="9499a-226">Use SSH para conectarse al nodo principal o perimetral:</span><span class="sxs-lookup"><span data-stu-id="9499a-226">Use SSH to connect to a head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="9499a-227">En la conexión SSH con el nodo principal o perimetral, use el comando `ssh` para conectarse a un nodo de trabajador en el clúster:</span><span class="sxs-lookup"><span data-stu-id="9499a-227">From the SSH connection to the head or edge node, use the `ssh` command to connect to a worker node in the cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="9499a-228">Para recuperar una lista de los nombres de dominio de los nodos del clúster, consulte [Administración de clústeres de HDInsight con la API de REST de Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes).</span><span class="sxs-lookup"><span data-stu-id="9499a-228">To retrieve a list of the domain names of the nodes in the cluster, see the [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="9499a-229">Si la cuenta SSH se protege utilizando un __contraseña__, escriba la contraseña al conectarse.</span><span class="sxs-lookup"><span data-stu-id="9499a-229">If the SSH account is secured using a __password__, enter the password when connecting.</span></span>

<span data-ttu-id="9499a-230">Si la cuenta SSH se protege utilizando __claves SSH__, asegúrese de que el reenvío de SSH está habilitado en el cliente.</span><span class="sxs-lookup"><span data-stu-id="9499a-230">If the SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on the client.</span></span>

> [!NOTE]
> <span data-ttu-id="9499a-231">Otra manera de obtener acceso directo a todos los nodos del clúster es instalar HDInsight en una instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="9499a-231">Another way to directly access all nodes in the cluster is to install HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="9499a-232">A continuación, puede unir la máquina remota a la misma red virtual y tener acceso directamente a todos los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-232">Then, you can join your remote machine to the same virtual network and directly access all nodes in the cluster.</span></span>
>
> <span data-ttu-id="9499a-233">Para más información, consulte el documento sobre el [uso de una red virtual con HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="9499a-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="9499a-234">Configuración del reenvío del agente SSH</span><span class="sxs-lookup"><span data-stu-id="9499a-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9499a-235">Los pasos siguientes presuponen un sistema basado en Linux o UNIX y funcionan con Bash en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9499a-235">The following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="9499a-236">Si estos pasos no funcionan en su sistema, es posible que deba consultar la documentación para el cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-236">If these steps do not work for your system, you may need to consult the documentation for your SSH client.</span></span>

1. <span data-ttu-id="9499a-237">Abra `~/.ssh/config`con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9499a-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="9499a-238">Si este archivo no existe, puede crearlo si escribe `touch ~/.ssh/config` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="9499a-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="9499a-239">Agregue al archivo `config` el texto siguiente.</span><span class="sxs-lookup"><span data-stu-id="9499a-239">Add the following text to the `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="9499a-240">Reemplace la información de __Host__ con la dirección del nodo al que se conecta a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-240">Replace the __Host__ information with the address of the node you connect to using SSH.</span></span> <span data-ttu-id="9499a-241">El ejemplo anterior utiliza el nodo perimetral.</span><span class="sxs-lookup"><span data-stu-id="9499a-241">The previous example uses the edge node.</span></span> <span data-ttu-id="9499a-242">Esta entrada configura el reenvío del agente SSH para el nodo especificado.</span><span class="sxs-lookup"><span data-stu-id="9499a-242">This entry configures SSH agent forwarding for the specified node.</span></span>

3. <span data-ttu-id="9499a-243">Use el siguiente comando desde el terminal para probar el desvío del agente SSH:</span><span class="sxs-lookup"><span data-stu-id="9499a-243">Test SSH agent forwarding by using the following command from the terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="9499a-244">Este comando devuelve información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="9499a-244">This command returns information similar to the following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="9499a-245">Si no se devuelve nada, `ssh-agent` no se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="9499a-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="9499a-246">Consulte la información de los scripts de inicio del agente en [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) (Uso de ssh-agent con ssh) o la documentación del cliente SSH para más información.</span><span class="sxs-lookup"><span data-stu-id="9499a-246">For more information, see the agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="9499a-247">Una vez que haya comprobado que **ssh-agent** está en ejecución, use lo siguiente para agregar la clave privada SSH al agente:</span><span class="sxs-lookup"><span data-stu-id="9499a-247">Once you have verified that **ssh-agent** is running, use the following to add your SSH private key to the agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="9499a-248">Si la clave privada está almacenada en un archivo distinto, reemplace `~/.ssh/id_rsa` por la ruta de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="9499a-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with the path to the file.</span></span>

5. <span data-ttu-id="9499a-249">Conecte con el nodo perimetral o nodos principales del clúster usando SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-249">Connect to the cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="9499a-250">A continuación, use el comando SSH para conectarse a un nodo de trabajo o de zookeeper.</span><span class="sxs-lookup"><span data-stu-id="9499a-250">Then use the SSH command to connect to a worker or zookeeper node.</span></span> <span data-ttu-id="9499a-251">La conexión se establece mediante la clave reenviada.</span><span class="sxs-lookup"><span data-stu-id="9499a-251">The connection is established using the forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="9499a-252">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="9499a-252">Copy files</span></span>

<span data-ttu-id="9499a-253">La utilidad `scp` puede utilizarse para copiar archivos a los nodos individuales del clúster y desde ellos.</span><span class="sxs-lookup"><span data-stu-id="9499a-253">The `scp` utility can be used to copy files to and from individual nodes in the cluster.</span></span> <span data-ttu-id="9499a-254">Por ejemplo, el siguiente comando copia el directorio `test.txt` desde el sistema local en el nodo principal primario:</span><span class="sxs-lookup"><span data-stu-id="9499a-254">For example, the following command copies the `test.txt` directory from the local system to the primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="9499a-255">Dado que no se especifica ninguna ruta de acceso después de `:`, el archivo se coloca en el directorio principal `sshuser`.</span><span class="sxs-lookup"><span data-stu-id="9499a-255">Since no path is specified after the `:`, the file is placed in the `sshuser` home directory.</span></span>

<span data-ttu-id="9499a-256">En el ejemplo siguiente, se copia el archivo `test.txt` desde el directorio principal `sshuser` al nodo principal primario del sistema local:</span><span class="sxs-lookup"><span data-stu-id="9499a-256">The following example copies the `test.txt` file from the `sshuser` home directory on the primary head node to the local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="9499a-257">`scp` solo puede tener acceso al sistema de archivos de los nodos individuales dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-257">`scp` can only access the file system of individual nodes within the cluster.</span></span> <span data-ttu-id="9499a-258">No se puede utilizar para acceder a datos en el almacenamiento compatible con HDFS para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9499a-258">It cannot be used to access data in the HDFS-compatible storage for the cluster.</span></span>
>
> <span data-ttu-id="9499a-259">Use `scp` cuando necesite cargar un recurso para utilizarse desde una sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-259">Use `scp` when you need to upload a resource for use from an SSH session.</span></span> <span data-ttu-id="9499a-260">Por ejemplo, cargue un script de Python y, a continuación, ejecútelo desde una sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="9499a-260">For example, upload a Python script and then run the script from an SSH session.</span></span>
>
> <span data-ttu-id="9499a-261">Para obtener información sobre cómo cargar directamente los datos en el almacenamiento compatible con HDFS, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="9499a-261">For information on directly loading data into the HDFS-compatible storage, see the following documents:</span></span>
>
> * <span data-ttu-id="9499a-262">[HDInsight mediante Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9499a-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="9499a-263">[HDInsight mediante Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="9499a-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9499a-264">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9499a-264">Next steps</span></span>

* [<span data-ttu-id="9499a-265">Uso de la tunelización de SSH con HDInsight</span><span class="sxs-lookup"><span data-stu-id="9499a-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="9499a-266">Uso de una red virtual con HDInsight</span><span class="sxs-lookup"><span data-stu-id="9499a-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="9499a-267">Uso de nodos perimetrales en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9499a-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)