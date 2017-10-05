---
title: "Uso de la tunelización de SSH para acceder a Azure HDInsight | Microsoft Docs"
description: "Obtenga información acerca de cómo usar un túnel SSH para ir con seguridad a los recursos web alojados en los nodos de HDInsight basados en Linux."
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="ffa03-103">Uso de la tunelización SSH para tener acceso a la interfaz de usuario Ambari Web, JobHistory, NameNode, Oozie y otras interfaces de usuario web</span><span class="sxs-lookup"><span data-stu-id="ffa03-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="ffa03-104">Los clústeres de HDInsight basados en Linux proporcionan acceso a la interfaz de usuario web de Ambari en Internet, pero no a algunas características de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="ffa03-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="ffa03-105">Por ejemplo, la interfaz de usuario web para otros servicios que se muestran en Ambari.</span><span class="sxs-lookup"><span data-stu-id="ffa03-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="ffa03-106">Para usar la funcionalidad completa de la interfaz de usuario web de Ambari, use un túnel SSH para el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="ffa03-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="ffa03-107">¿Por qué usar un túnel SSH?</span><span class="sxs-lookup"><span data-stu-id="ffa03-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="ffa03-108">Algunos de los menús de Ambari solo funcionan a través de un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="ffa03-109">Estos menús se basan en sitios web y servicios que se ejecutan en otros tipos de nodo, como nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ffa03-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="ffa03-110">A menudo, estos sitios web no están protegidos, por lo que no es seguro exponerlos directamente en internet.</span><span class="sxs-lookup"><span data-stu-id="ffa03-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="ffa03-111">Las siguientes interfaces de usuario web requieren un túnel SSH:</span><span class="sxs-lookup"><span data-stu-id="ffa03-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="ffa03-112">Historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="ffa03-112">JobHistory</span></span>
* <span data-ttu-id="ffa03-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="ffa03-113">NameNode</span></span>
* <span data-ttu-id="ffa03-114">Pilas de subprocesos</span><span class="sxs-lookup"><span data-stu-id="ffa03-114">Thread Stacks</span></span>
* <span data-ttu-id="ffa03-115">Interfaz de usuario web de Oozie</span><span class="sxs-lookup"><span data-stu-id="ffa03-115">Oozie web UI</span></span>
* <span data-ttu-id="ffa03-116">Interfaz de usuario de registros y maestro de HBase</span><span class="sxs-lookup"><span data-stu-id="ffa03-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="ffa03-117">Si usa las acciones de script para personalizar el clúster, todos los servicios o utilidades que instale y expongan una interfaz de usuario web requerirán un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="ffa03-118">Por ejemplo, si instala Hue mediante una acción de script, debe usar un túnel SSH para tener acceso a la interfaz de usuario web de Hue.</span><span class="sxs-lookup"><span data-stu-id="ffa03-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffa03-119">Si tiene acceso directo a HDInsight a través de una red virtual, no es necesario usar túneles SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="ffa03-120">Para ver un ejemplo de acceso directo a HDInsight a través de una red virtual, consulte el documento [Conexión de HDInsight a la red local](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="ffa03-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="ffa03-121">¿Qué es un túnel SSH?</span><span class="sxs-lookup"><span data-stu-id="ffa03-121">What is an SSH tunnel</span></span>

<span data-ttu-id="ffa03-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) (Tunelización de Secure Shell [SSH]) enruta el tráfico enviado a un puerto en la estación de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="ffa03-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="ffa03-123">El tráfico se enruta a través de una conexión SSH al nodo principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ffa03-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="ffa03-124">La solicitud se resuelve como si se originara en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="ffa03-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="ffa03-125">A continuación, la respuesta se enruta a través del túnel a la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ffa03-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffa03-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ffa03-126">Prerequisites</span></span>

* <span data-ttu-id="ffa03-127">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-127">An SSH client.</span></span> <span data-ttu-id="ffa03-128">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ffa03-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="ffa03-129">Un explorador web que se puede configurar para usar un proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="ffa03-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="ffa03-130">La compatibilidad con el proxy SOCKS integrada en Windows no incluye SOCKS5 y no funciona con los pasos descritos en este documento.</span><span class="sxs-lookup"><span data-stu-id="ffa03-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="ffa03-131">Los siguientes exploradores se basan en la configuración de proxy de Windows y actualmente no funcionan con los pasos descritos en este documento:</span><span class="sxs-lookup"><span data-stu-id="ffa03-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="ffa03-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="ffa03-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="ffa03-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ffa03-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="ffa03-134">Google Chrome también se basa en la configuración de proxy de Windows.</span><span class="sxs-lookup"><span data-stu-id="ffa03-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="ffa03-135">Sin embargo, se pueden instalar extensiones que admiten SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="ffa03-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="ffa03-136">Se recomienda [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="ffa03-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="ffa03-137"><a name="usessh"></a>Creación de un túnel con el comando SSH</span><span class="sxs-lookup"><span data-stu-id="ffa03-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="ffa03-138">Use el siguiente comando para crear un túnel SSH con el comando `ssh` .</span><span class="sxs-lookup"><span data-stu-id="ffa03-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="ffa03-139">Reemplace **USERNAME** por un usuario SSH para su clúster de HDInsight y reemplace **CLUSTERNAME** por el nombre de su clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ffa03-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="ffa03-140">Este comando crea una conexión que enruta el tráfico al puerto local 9876 al clúster a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="ffa03-141">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="ffa03-141">The options are:</span></span>

* <span data-ttu-id="ffa03-142">**D 9876** : el puerto local que enruta el tráfico a través del túnel.</span><span class="sxs-lookup"><span data-stu-id="ffa03-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="ffa03-143">**C** : comprimir todos los datos, debido a que el tráfico web es principalmente texto.</span><span class="sxs-lookup"><span data-stu-id="ffa03-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="ffa03-144">**2** : forzar a SSH a que intente solo la versión 2 del protocolo.</span><span class="sxs-lookup"><span data-stu-id="ffa03-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="ffa03-145">**q** : modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="ffa03-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="ffa03-146">**T** : deshabilitar la asignación seudotty, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ffa03-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ffa03-147">**n** : evitar la lectura de STDIN, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ffa03-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ffa03-148">**N** : no ejecutar un comando remoto, debido a que solo estamos desviando un puerto.</span><span class="sxs-lookup"><span data-stu-id="ffa03-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="ffa03-149">**f** : ejecutar en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="ffa03-149">**f** - Run in the background.</span></span>

<span data-ttu-id="ffa03-150">Una vez que se completa el comando, el tráfico enviado al puerto 9876 de la máquina local se enruta al nodo principal del cluster.</span><span class="sxs-lookup"><span data-stu-id="ffa03-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="ffa03-151"><a name="useputty"></a>Creación de un túnel mediante PuTTY</span><span class="sxs-lookup"><span data-stu-id="ffa03-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="ffa03-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) es un cliente SSH gráfico para Windows.</span><span class="sxs-lookup"><span data-stu-id="ffa03-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="ffa03-153">Use los siguientes pasos para crear un túnel SSH con PuTTY:</span><span class="sxs-lookup"><span data-stu-id="ffa03-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="ffa03-154">Abra PuTTY y escriba la información de conexión.</span><span class="sxs-lookup"><span data-stu-id="ffa03-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="ffa03-155">Si no está familiarizado con PuTTY, consulte la [documentación de PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="ffa03-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="ffa03-156">En la sección **Category** (Categoría) a la izquierda del cuadro de diálogo, expanda **Connection** (Conexión), **SSH** y, a continuación, seleccione **Tunnels** (Túneles).</span><span class="sxs-lookup"><span data-stu-id="ffa03-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="ffa03-157">Proporcione la siguiente información en el formulario **Options controlling SSH port forwarding** (Opciones que controlan el desvío de puertos SSH):</span><span class="sxs-lookup"><span data-stu-id="ffa03-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="ffa03-158">**Source port** : el puerto en el cliente que desea desviar.</span><span class="sxs-lookup"><span data-stu-id="ffa03-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="ffa03-159">Por ejemplo, **9876**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-159">For example, **9876**.</span></span>

   * <span data-ttu-id="ffa03-160">**Destination** : la dirección SSH del clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="ffa03-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ffa03-161">Por ejemplo, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="ffa03-162">**Dynamic** : habilita el enrutamiento dinámico del proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="ffa03-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![imagen de las opciones de tunelización](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="ffa03-164">Haga clic en **Add** (Agregar) para agregar la configuración y, a continuación, en **Open** (Abrir) para abrir una conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="ffa03-165">Cuando se le solicite, inicie sesión en el servidor.</span><span class="sxs-lookup"><span data-stu-id="ffa03-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="ffa03-166">Uso del túnel desde el explorador</span><span class="sxs-lookup"><span data-stu-id="ffa03-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffa03-167">Los pasos de esta sección usan el explorador Mozilla FireFox, ya que proporciona la misma configuración de proxy para todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="ffa03-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="ffa03-168">Otros exploradores modernos, como Google Chrome, pueden requerir una extensión como FoxyProxy para funcionar con el túnel.</span><span class="sxs-lookup"><span data-stu-id="ffa03-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="ffa03-169">Configure el explorador para usar **localhost** y el puerto que utilizó al crear el túnel como un proxy **SOCKS v5**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="ffa03-170">La configuración de Firefox se verá de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="ffa03-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="ffa03-171">Si usa un puerto que no es 9876, cambie el puerto al que usa:</span><span class="sxs-lookup"><span data-stu-id="ffa03-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![imagen de la configuración de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="ffa03-173">La selección de **DNS remoto** resuelve las solicitudes del sistema de nombres de dominio (DNS) mediante el uso del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ffa03-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="ffa03-174">Esta configuración resuelve el DNS con el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="ffa03-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="ffa03-175">Compruebe que el túnel funciona, para ello, visite un sitio como [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="ffa03-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="ffa03-176">La dirección IP devuelta debe ser una que use el centro de datos de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa03-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="ffa03-177">Compruebe con la interfaz de usuario web de Ambari</span><span class="sxs-lookup"><span data-stu-id="ffa03-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="ffa03-178">Una vez que se ha establecido el clúster, siga estos pasos para comprobar que puede tener acceso a las interfaces de usuario web del servicio desde la web de Ambari:</span><span class="sxs-lookup"><span data-stu-id="ffa03-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="ffa03-179">En el explorador, vaya a http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="ffa03-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="ffa03-180">La dirección `headnodehost` se envía al clúster a través del túnel y se resuelve en el nodo principal en el que se ejecuta Ambari.</span><span class="sxs-lookup"><span data-stu-id="ffa03-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="ffa03-181">Cuando se le solicite, escriba el nombre de usuario administrador (admin) y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="ffa03-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="ffa03-182">Es posible que se le pida una segunda vez mediante la interfaz de usuario web de Ambari.</span><span class="sxs-lookup"><span data-stu-id="ffa03-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="ffa03-183">Si es así, vuelva a escribir la información.</span><span class="sxs-lookup"><span data-stu-id="ffa03-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ffa03-184">Si utiliza la dirección de http://headnodehost:8080 para conectarse al clúster, se está conectando a través del túnel.</span><span class="sxs-lookup"><span data-stu-id="ffa03-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="ffa03-185">La comunicación se protege si usa el túnel SSH en lugar de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ffa03-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="ffa03-186">Para conectarse a través de Internet mediante HTTPS, use https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="ffa03-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="ffa03-187">En la interfaz de usuario de Ambari Web, seleccione HDFS en la lista de la izquierda de la página.</span><span class="sxs-lookup"><span data-stu-id="ffa03-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Imagen con HDFS seleccionado](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="ffa03-189">Cuando se muestra la información del servicio HDFS, seleccione **Vínculos rápidos**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="ffa03-190">Aparece una lista de los nodos del clúster principal.</span><span class="sxs-lookup"><span data-stu-id="ffa03-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="ffa03-191">Seleccione uno de los nodos principales y luego seleccione **IU de NameNode**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Imagen con el menú Vínculos rápidos expandido](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="ffa03-193">Al seleccionar __Vínculos rápidos__, es posible que obtenga un indicador de espera.</span><span class="sxs-lookup"><span data-stu-id="ffa03-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="ffa03-194">Esta condición puede ocurrir si tiene una conexión lenta a Internet.</span><span class="sxs-lookup"><span data-stu-id="ffa03-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="ffa03-195">Espere un minuto o dos hasta que se reciban los datos del servidor e intente de nuevo la lista.</span><span class="sxs-lookup"><span data-stu-id="ffa03-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="ffa03-196">Algunas entradas en el menú **Vínculos rápidos** pueden quedar cortadas en el lado derecho de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="ffa03-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="ffa03-197">Si es así, expanda el menú con el mouse y use la tecla de dirección derecha para desplazarse por la pantalla hacia la derecha para ver el resto del menú.</span><span class="sxs-lookup"><span data-stu-id="ffa03-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="ffa03-198">Aparece una página similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="ffa03-198">A page similar to the following image is displayed:</span></span>

    ![Imagen de la interfaz de usuario de NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="ffa03-200">Observe la dirección URL de esta página, debe ser similar a **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="ffa03-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="ffa03-201">Este identificador URI usa el nombre de dominio completo interno (FQDN) del nodo y solo es accesible si se usa un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="ffa03-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa03-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffa03-202">Next steps</span></span>

<span data-ttu-id="ffa03-203">Ahora que ha aprendido a crear y usar un túnel SSH, consulte el documento siguiente para conocer otras formas de usar Ambari:</span><span class="sxs-lookup"><span data-stu-id="ffa03-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="ffa03-204">Administración de clústeres de HDInsight con Ambari</span><span class="sxs-lookup"><span data-stu-id="ffa03-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="ffa03-205">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ffa03-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

