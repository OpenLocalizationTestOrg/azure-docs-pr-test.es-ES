---
title: "aaaUse SSH túnel tooaccess HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse una toosecurely de túnel SSH examinar recursos de web hospedados en los nodos de HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="ee53a-103">Usar la interfaz de usuario de tooaccess Ambari web túnel SSH, JobHistory, NameNode, Oozie y otra interfaces de usuario web</span><span class="sxs-lookup"><span data-stu-id="ee53a-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="ee53a-104">Clústeres de HDInsight basados en Linux proporcionan acceso tooAmbari interfaz de usuario web a través de Internet de hello, pero algunas características de interfaz de usuario de hello no están.</span><span class="sxs-lookup"><span data-stu-id="ee53a-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="ee53a-105">Por ejemplo, hello interfaz de usuario web para otros servicios que se exponen a través de Ambari.</span><span class="sxs-lookup"><span data-stu-id="ee53a-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="ee53a-106">Para todas las funcionalidades de la interfaz de usuario de web de hello Ambari, debe utilizar un encabezado de clúster de toohello de túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="ee53a-107">¿Por qué usar un túnel SSH?</span><span class="sxs-lookup"><span data-stu-id="ee53a-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="ee53a-108">Algunos de los menús de hello en Ambari solo funcionan a través de un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="ee53a-109">Estos menús se basan en sitios web y servicios que se ejecutan en otros tipos de nodo, como nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee53a-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="ee53a-110">A menudo, estos sitios web no están protegidos, por lo que no es seguro toodirectly exponen Hola a ellos en internet.</span><span class="sxs-lookup"><span data-stu-id="ee53a-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="ee53a-111">Hola siguientes interfaces de usuario Web requiere un túnel SSH:</span><span class="sxs-lookup"><span data-stu-id="ee53a-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="ee53a-112">Historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="ee53a-112">JobHistory</span></span>
* <span data-ttu-id="ee53a-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="ee53a-113">NameNode</span></span>
* <span data-ttu-id="ee53a-114">Pilas de subprocesos</span><span class="sxs-lookup"><span data-stu-id="ee53a-114">Thread Stacks</span></span>
* <span data-ttu-id="ee53a-115">Interfaz de usuario web de Oozie</span><span class="sxs-lookup"><span data-stu-id="ee53a-115">Oozie web UI</span></span>
* <span data-ttu-id="ee53a-116">Interfaz de usuario de registros y maestro de HBase</span><span class="sxs-lookup"><span data-stu-id="ee53a-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="ee53a-117">Si utiliza acciones de Script toocustomize el clúster, todos los servicios o utilidades que se instalación que exponen una interfaz de usuario web requieren un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="ee53a-118">Por ejemplo, si instala matiz mediante una acción de secuencia de comandos, debe utilizar un SSH túnel tooaccess Hola matiz interfaz de usuario web.</span><span class="sxs-lookup"><span data-stu-id="ee53a-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee53a-119">Si tiene acceso directo tooHDInsight a través de una red virtual, no es necesario toouse SSH túneles.</span><span class="sxs-lookup"><span data-stu-id="ee53a-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="ee53a-120">Para obtener un ejemplo de obtener acceso directamente a HDInsight a través de una red virtual, vea hello [red local de HDInsight conectar tooyour](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ee53a-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="ee53a-121">¿Qué es un túnel SSH?</span><span class="sxs-lookup"><span data-stu-id="ee53a-121">What is an SSH tunnel</span></span>

<span data-ttu-id="ee53a-122">[Secure Shell (SSH) túnel](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) enruta el tráfico enviado tooa puerto en la estación de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="ee53a-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="ee53a-123">Hola tráfico se enruta a través de un SSH conexión tooyour HDInsight nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="ee53a-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="ee53a-124">solicitud de saludo se resuelve como si se originó en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="ee53a-125">respuesta de Hello, a continuación, se enruta a través de estación de trabajo de hello túnel tooyour.</span><span class="sxs-lookup"><span data-stu-id="ee53a-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee53a-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ee53a-126">Prerequisites</span></span>

* <span data-ttu-id="ee53a-127">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-127">An SSH client.</span></span> <span data-ttu-id="ee53a-128">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ee53a-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="ee53a-129">Un explorador web que se puede configura un proxy SOCKS5 toouse.</span><span class="sxs-lookup"><span data-stu-id="ee53a-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="ee53a-130">compatibilidad de proxy SOCKS Hola integrada en Windows no admite SOCKS5 y no funciona con los pasos de hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="ee53a-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="ee53a-131">Hello exploradores siguientes se basan en la configuración de proxy de Windows y actualmente no realizar trabajo con pasos de hello en este documento:</span><span class="sxs-lookup"><span data-stu-id="ee53a-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="ee53a-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="ee53a-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="ee53a-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ee53a-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="ee53a-134">Google Chrome también se basa en la configuración de proxy de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="ee53a-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="ee53a-135">Sin embargo, se pueden instalar extensiones que admiten SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="ee53a-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="ee53a-136">Se recomienda [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="ee53a-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="ee53a-137"><a name="usessh"></a>Crear un túnel con el comando de hello SSH</span><span class="sxs-lookup"><span data-stu-id="ee53a-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="ee53a-138">Comando de uso Hola siguiente toocreate un túnel SSH con hello `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="ee53a-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="ee53a-139">Reemplace **nombre de usuario** con un usuario SSH para el clúster de HDInsight y reemplazar **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ee53a-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="ee53a-140">Este comando crea una conexión que enruta los clúster de tráfico toolocal puerto 9876 toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="ee53a-141">Hola opciones son:</span><span class="sxs-lookup"><span data-stu-id="ee53a-141">hello options are:</span></span>

* <span data-ttu-id="ee53a-142">**D 9876** -Hola puerto local que enruta el tráfico a través de túnel de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="ee53a-143">**C** : comprimir todos los datos, debido a que el tráfico web es principalmente texto.</span><span class="sxs-lookup"><span data-stu-id="ee53a-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="ee53a-144">**2** -force SSH tootry versión 2 del protocolo solo.</span><span class="sxs-lookup"><span data-stu-id="ee53a-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="ee53a-145">**q** : modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="ee53a-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="ee53a-146">**T** : deshabilitar la asignación seudotty, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ee53a-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ee53a-147">**n** : evitar la lectura de STDIN, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ee53a-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ee53a-148">**N** : no ejecutar un comando remoto, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ee53a-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ee53a-149">**f** -ejecutar en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="ee53a-150">Una vez que finaliza el comando de hello, el tráfico enviado tooport 9876 en equipo local hello es toohello enrutado nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="ee53a-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="ee53a-151"><a name="useputty"></a>Creación de un túnel mediante PuTTY</span><span class="sxs-lookup"><span data-stu-id="ee53a-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="ee53a-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) es un cliente SSH gráfico para Windows.</span><span class="sxs-lookup"><span data-stu-id="ee53a-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="ee53a-153">Usar hello siguiendo los pasos toocreate un túnel SSH mediante PuTTY:</span><span class="sxs-lookup"><span data-stu-id="ee53a-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="ee53a-154">Abra PuTTY y escriba la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="ee53a-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="ee53a-155">Si no está familiarizado con PuTTY, vea hello [PuTTY documentación (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="ee53a-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="ee53a-156">Hola **categoría** toohello de la sección izquierda del cuadro de diálogo de hello, expanda **conexión**, expanda **SSH**y, a continuación, seleccione **túneles**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="ee53a-157">Proporcionar Hola siguiente información en hello **reenvío de puerto de opciones que controlan SSH** formulario:</span><span class="sxs-lookup"><span data-stu-id="ee53a-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="ee53a-158">**Puerto de origen** -Hola puerto en el cliente de Hola que desea tooforward.</span><span class="sxs-lookup"><span data-stu-id="ee53a-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="ee53a-159">Por ejemplo, **9876**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-159">For example, **9876**.</span></span>

   * <span data-ttu-id="ee53a-160">**Destino** -Hola dirección SSH para clúster de HDInsight basados en Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ee53a-161">Por ejemplo, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="ee53a-162">**Dynamic** : habilita el enrutamiento dinámico del proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="ee53a-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![imagen de las opciones de tunelización](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="ee53a-164">Haga clic en **agregar** tooadd Hola configuración y, a continuación, haga clic en **abiertos** tooopen una conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="ee53a-165">Cuando se le solicite, inicie sesión en el servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="ee53a-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="ee53a-166">Usar túnel Hola desde el explorador</span><span class="sxs-lookup"><span data-stu-id="ee53a-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee53a-167">Hola pasos de este Hola de uso de la sección explorador Mozilla FireFox, ya que proporciona Hola misma configuración de proxy para todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="ee53a-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="ee53a-168">Otros exploradores modernos, como Google Chrome, pueden requerir una extensión como FoxyProxy toowork con túnel Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="ee53a-169">Configurar Hola explorador toouse **localhost** y puerto de Hola que ha utilizado al crear túnel Hola como un **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="ee53a-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="ee53a-170">Este es el aspecto de configuración de Firefox Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="ee53a-171">Si utiliza un puerto diferente 9876, cambiar hello toohello de puerto que utiliza:</span><span class="sxs-lookup"><span data-stu-id="ee53a-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![imagen de la configuración de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="ee53a-173">Seleccionar **DNS remoto** resuelve las solicitudes de sistema de nombres de dominio (DNS) mediante el uso de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="ee53a-174">Esta configuración resuelve DNS con la del nodo principal del clúster de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="ee53a-175">Compruebe que túnel Hola funciona al visitar un sitio como [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="ee53a-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="ee53a-176">Hola IP devuelve uno se utilizará en centros de datos de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="ee53a-177">Compruebe con la interfaz de usuario web de Ambari</span><span class="sxs-lookup"><span data-stu-id="ee53a-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="ee53a-178">Una vez que se ha establecido el clúster de hello, utilice Hola después tooverify de pasos que puede tener acceso a interfaces de usuario web del servicio de hello Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="ee53a-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="ee53a-179">En el explorador, vaya toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="ee53a-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="ee53a-180">Hola `headnodehost` dirección se envía a través de clústeres de toohello de túnel de Hola y resolver el nodo principal de toohello Ambari se ejecuta en.</span><span class="sxs-lookup"><span data-stu-id="ee53a-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="ee53a-181">Cuando se le solicite, escriba el nombre de usuario de administrador de hello (admin) y la contraseña para el clúster.</span><span class="sxs-lookup"><span data-stu-id="ee53a-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="ee53a-182">Se le pedirá una segunda vez mediante la interfaz de usuario de web de hello Ambari.</span><span class="sxs-lookup"><span data-stu-id="ee53a-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="ee53a-183">Si es así, vuelva a especificar información de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee53a-184">Cuando utiliza hello http://headnodehost:8080 dirección tooconnect toohello clúster, se conecta a través de túnel de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="ee53a-185">La comunicación está protegida mediante túnel SSH de hello en lugar de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ee53a-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="ee53a-186">tooconnect más Hola a internet a través de HTTPS, use https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="ee53a-187">En hello Ambari Web UI, seleccione HDFS en lista de hello de la izquierda de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Imagen con HDFS seleccionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="ee53a-189">Cuando se muestra la información del servicio HDFS hello, seleccione **vínculos rápidos**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="ee53a-190">Aparece una lista de nodos principales del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="ee53a-191">Seleccione uno de los nodos principales de hello y, a continuación, seleccione **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Imagen con menú de vínculos rápidos de hello expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="ee53a-193">Al seleccionar __Vínculos rápidos__, es posible que obtenga un indicador de espera.</span><span class="sxs-lookup"><span data-stu-id="ee53a-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="ee53a-194">Esta condición puede ocurrir si tiene una conexión lenta a Internet.</span><span class="sxs-lookup"><span data-stu-id="ee53a-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="ee53a-195">Espere un minuto o dos para hello datos toobe recibido del servidor de hello, vuelva a intentarlo lista Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="ee53a-196">Algunas entradas de hello **vínculos rápidos** menú puede quedar cortado por hello derecha de la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="ee53a-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="ee53a-197">Si es así, expanda menú hello mediante el mouse y utilice Hola flecha derecha tooscroll clave Hola pantalla toohello toosee derecho Hola resto del menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53a-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="ee53a-198">Se muestra un toohello similar de página después de la imagen:</span><span class="sxs-lookup"><span data-stu-id="ee53a-198">A page similar toohello following image is displayed:</span></span>

    ![Imagen de hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="ee53a-200">Observe la dirección URL de Hola para esta página; debe ser similar demasiado**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/clúster**.</span><span class="sxs-lookup"><span data-stu-id="ee53a-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="ee53a-201">Este identificador URI está usando el nombre de dominio completo interno de hello (FQDN) del nodo de Hola y solo está disponible cuando se usa un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ee53a-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee53a-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee53a-202">Next steps</span></span>

<span data-ttu-id="ee53a-203">Ahora que ha aprendido cómo toocreate y use un túnel SSH, vea Hola después de documento para otro toouse formas Ambari:</span><span class="sxs-lookup"><span data-stu-id="ee53a-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="ee53a-204">Administración de clústeres de HDInsight con Ambari</span><span class="sxs-lookup"><span data-stu-id="ee53a-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="ee53a-205">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ee53a-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

