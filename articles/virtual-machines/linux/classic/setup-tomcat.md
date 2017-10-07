---
title: "aaaSet seguridad Apache Tomcat en una máquina virtual Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una Tomcat7 Apache mediante el uso de máquinas virtuales de Azure ejecutan Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="f6db2-103">Configuración de Tomcat7 en una máquina virtual con Linux con Azure</span><span class="sxs-lookup"><span data-stu-id="f6db2-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="f6db2-104">Apache Tomcat (o simplemente Tomcat, también se denominaba Tomcat Yakarta) es un contenedor de servlet desarrollado por hello Apache Software Foundation (ASF) y el servidor web de código abierto.</span><span class="sxs-lookup"><span data-stu-id="f6db2-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="f6db2-105">Tomcat implementa hello Servlet de Java y especificaciones de hello JavaServer Pages (JSP) de Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="f6db2-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="f6db2-106">Tomcat proporciona un entorno puro de servidor de web HTTP de Java en qué toorun código Java.</span><span class="sxs-lookup"><span data-stu-id="f6db2-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="f6db2-107">Configuración más sencilla de hello, Tomcat se ejecuta en un proceso de sistema operativo único.</span><span class="sxs-lookup"><span data-stu-id="f6db2-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="f6db2-108">Este proceso ejecuta una máquina virtual de Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="f6db2-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="f6db2-109">Todas las solicitudes HTTP desde un explorador tooTomcat se procesan como un subproceso independiente en el proceso de Tomcat Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f6db2-110">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f6db2-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f6db2-111">Este artículo trata cómo toouse Hola modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="f6db2-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="f6db2-112">Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.</span><span class="sxs-lookup"><span data-stu-id="f6db2-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f6db2-113">toouse un toodeploy de plantilla de administrador de recursos una VM de Ubuntu con Openjdk y Tomcat, consulte [este artículo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="f6db2-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="f6db2-114">En este artículo, instalará Tomcat7 en una imagen de Linux y la implementará en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db2-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="f6db2-115">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f6db2-115">You will learn:</span></span>  

* <span data-ttu-id="f6db2-116">¿Cómo toocreate una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db2-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="f6db2-117">¿Cómo tooprepare Hola máquina virtual para Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f6db2-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="f6db2-118">Cómo tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f6db2-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="f6db2-119">Se supone que ya tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db2-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="f6db2-120">Si no es así, puede suscribirse a una prueba gratuita en [Hola sitio Web de Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f6db2-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="f6db2-121">Si tiene una suscripción de MSDN, consulte [Precios especiales de Microsoft Azure: Ventajas de MSDN, MPN y Bizspark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="f6db2-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="f6db2-122">toolearn más información acerca de Azure, consulte [¿qué es Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="f6db2-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="f6db2-123">En este artículo se supone que tiene conocimientos prácticos básicos de Tomcat y Linux.</span><span class="sxs-lookup"><span data-stu-id="f6db2-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="f6db2-124">Fase 1: Creación de una imagen</span><span class="sxs-lookup"><span data-stu-id="f6db2-124">Phase 1: Create an image</span></span>
<span data-ttu-id="f6db2-125">En esta fase, creará una máquina virtual mediante una imagen de Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db2-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="f6db2-126">Paso 1: Generación de una clave de autenticación SSH</span><span class="sxs-lookup"><span data-stu-id="f6db2-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="f6db2-127">SSH es una herramienta importante para los administradores del sistema.</span><span class="sxs-lookup"><span data-stu-id="f6db2-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="f6db2-128">Pero no se recomienda configurar la seguridad del acceso mediante una contraseña determinada por personas.</span><span class="sxs-lookup"><span data-stu-id="f6db2-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="f6db2-129">Los usuarios malintencionados pueden acceder a su sistema si está protegido por un nombre de usuario y una contraseña débiles.</span><span class="sxs-lookup"><span data-stu-id="f6db2-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="f6db2-130">buenas noticias de Hello son que hay una forma de acceso remoto tooleave abrir y no se preocupe acerca de las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="f6db2-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="f6db2-131">Este método consiste en la autenticación con criptografía asimétrica.</span><span class="sxs-lookup"><span data-stu-id="f6db2-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="f6db2-132">Hello clave privada del usuario es hello que concede autenticación Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="f6db2-133">Incluso puede bloquear la cuenta de usuario de hello toonot permitir la autenticación de contraseña.</span><span class="sxs-lookup"><span data-stu-id="f6db2-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="f6db2-134">Otra ventaja de este método es que no es necesario toosign contraseñas diferentes en los servidores de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="f6db2-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="f6db2-135">Puede autenticar mediante clave privada de hello personal en todos los servidores, lo que evitará tener tooremember varias contraseñas.</span><span class="sxs-lookup"><span data-stu-id="f6db2-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="f6db2-136">Siga estos pasos toogenerate Hola autenticación la clave SSH.</span><span class="sxs-lookup"><span data-stu-id="f6db2-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="f6db2-137">Descargue e instale PuTTYgen desde Hola ubicación siguiente: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="f6db2-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="f6db2-138">Ejecute Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="f6db2-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="f6db2-139">Haga clic en **generar** claves de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="f6db2-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="f6db2-140">En el proceso de hello, puede crecer aleatoriedad con el mouse de hello móvil en área en blanco de hello en ventana hello.</span><span class="sxs-lookup"><span data-stu-id="f6db2-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="f6db2-141">![Captura de pantalla de generador de claves puTTY que muestra hello generar nuevo botón clave][1]</span><span class="sxs-lookup"><span data-stu-id="f6db2-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="f6db2-142">Una vez Hola generar proceso, Puttygen.exe mostrará la nueva clave pública.</span><span class="sxs-lookup"><span data-stu-id="f6db2-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Captura de pantalla de generador de claves puTTY que muestra la nueva clave pública de Hola y Hola guardar botón clave privada][2]
5. <span data-ttu-id="f6db2-144">Seleccione y copie la clave pública de Hola y guardarlo en un archivo denominado publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="f6db2-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="f6db2-145">No haga clic en **guardar de clave pública**, ya que es diferente de la clave pública de hello queremos Hola guarda el formato de archivo de la clave pública.</span><span class="sxs-lookup"><span data-stu-id="f6db2-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="f6db2-146">Haga clic en **Guardar clave privada** y guárdela en un archivo denominado privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="f6db2-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="f6db2-147">Paso 2: Crear la imagen de Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f6db2-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="f6db2-148">Hola [portal](https://portal.azure.com/), haga clic en **New** Hola de tareas de la barra toocreate una imagen.</span><span class="sxs-lookup"><span data-stu-id="f6db2-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="f6db2-149">A continuación, elija la imagen de Linux de Hola que se basa en sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="f6db2-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="f6db2-150">Hello en el ejemplo siguiente se usa Hola Ubuntu 14.04 imagen.</span><span class="sxs-lookup"><span data-stu-id="f6db2-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="f6db2-151">![Captura de pantalla de portal de Hola que muestra el botón nuevo Hola][3]</span><span class="sxs-lookup"><span data-stu-id="f6db2-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="f6db2-152">Para **nombre de Host**, especificar nombre de Hola de dirección URL de Hola que clientes de Internet y se utilizará tooaccess esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f6db2-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="f6db2-153">Definir la última parte del nombre DNS de hello, por ejemplo, tomcatdemo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="f6db2-154">Azure, a continuación, generará la dirección URL de hello como tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f6db2-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="f6db2-155">Para **clave de autenticación SSH**, copie el valor de clave de Hola desde archivo publicKey.pem de hello, que contiene la clave pública de hello generada por PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="f6db2-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="f6db2-156">![Cuadro clave de autenticación de SSH en el portal de Hola][4]</span><span class="sxs-lookup"><span data-stu-id="f6db2-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="f6db2-157">Configure otras opciones según sea necesario y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="f6db2-158">Fase 2: Preparación de la máquina virtual para Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="f6db2-159">En esta fase, configurará un punto de conexión para el tráfico de Tomcat y, a continuación, conecte la nueva máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="f6db2-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="f6db2-160">Paso 1: Abra Hola HTTP puerto tooallow web access</span><span class="sxs-lookup"><span data-stu-id="f6db2-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="f6db2-161">Los puntos de conexión en Azure constan de un protocolo TCP o UDP, junto con un puerto público y privado.</span><span class="sxs-lookup"><span data-stu-id="f6db2-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="f6db2-162">Hola privada Hola puerto es que el servicio de hello está escuchando máquina virtual de tooon Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="f6db2-163">Puerto público Hello es puerto Hola Hola servicio de nube de Azure escucha tooexternally para el tráfico entrante, basado en Internet.</span><span class="sxs-lookup"><span data-stu-id="f6db2-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="f6db2-164">El puerto TCP 8080 es el número de puerto predeterminado de Hola que Tomcat usa toolisten.</span><span class="sxs-lookup"><span data-stu-id="f6db2-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="f6db2-165">Si se abre este puerto con un punto de conexión de Azure, usted y otros clientes de Internet pueden acceder a páginas de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="f6db2-166">En el portal de hello, haga clic en **examinar** > **máquinas virtuales**y, a continuación, haga clic en la máquina virtual Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="f6db2-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="f6db2-167">![Captura de pantalla de directorio de máquinas virtuales de Hola][5]</span><span class="sxs-lookup"><span data-stu-id="f6db2-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="f6db2-168">tooadd una máquina virtual de tooyour de punto de conexión, haga clic en hello **extremos** cuadro.</span><span class="sxs-lookup"><span data-stu-id="f6db2-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="f6db2-169">![Captura de pantalla que muestra el cuadro de puntos de conexión de Hola][6]</span><span class="sxs-lookup"><span data-stu-id="f6db2-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="f6db2-170">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="f6db2-171">Para el extremo de hello, escriba un nombre de extremo de hello en **extremo**y, a continuación, escriba 80 en **puerto público**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="f6db2-172">Si se establece too80, no es necesario tooinclude número de puerto de hello en dirección URL de Hola que es usado tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="f6db2-173">Por ejemplo, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f6db2-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="f6db2-174">Si se establece el valor de tooanother, como 81, deberá tooadd Hola puerto número toohello URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="f6db2-175">Por ejemplo, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="f6db2-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="f6db2-176">Escriba 8080 en **Puerto privado**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="f6db2-177">De manera predeterminada, Tomcat escucha en el puerto TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="f6db2-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="f6db2-178">Si ha cambiado el puerto de escucha de predeterminado Hola de Tomcat, debe actualizar **puerto privado** toobe Hola igual Hola puerto de escucha de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="f6db2-179">![Captura de pantalla de interfaz de usuario que muestra Agregar comando, Puerto público y Puerto privado][7]</span><span class="sxs-lookup"><span data-stu-id="f6db2-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="f6db2-180">Haga clic en **Aceptar** tooadd Hola extremo tooyour virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f6db2-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="f6db2-181">Paso 2: Conectar imagen toohello que ha creado</span><span class="sxs-lookup"><span data-stu-id="f6db2-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="f6db2-182">Puede elegir cualquier máquina virtual SSH herramienta tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="f6db2-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="f6db2-183">En este ejemplo, se usa PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f6db2-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="f6db2-184">Obtener el nombre DNS de hello de la máquina virtual del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="f6db2-185">Haga clic en **Examinar** > **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="f6db2-186">Seleccione Hola nombre de la máquina virtual y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="f6db2-187">Hola **propiedades** icono, mire en hello **nombre de dominio** nombre DNS del cuadro de tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="f6db2-188">Obtener el número de puerto de Hola para las conexiones de SSH de hello **SSH** cuadro.</span><span class="sxs-lookup"><span data-stu-id="f6db2-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="f6db2-189">![Captura de pantalla que muestra el número de puerto de conexión de SSH de Hola][8]</span><span class="sxs-lookup"><span data-stu-id="f6db2-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="f6db2-190">Descargue [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="f6db2-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="f6db2-191">Después de la descarga, haga clic en el archivo ejecutable hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="f6db2-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="f6db2-192">En configuración de PuTTY, configurar las opciones básicas de hello con el nombre de host de Hola y el puerto número que se obtiene de las propiedades de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f6db2-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Captura de pantalla que muestra las opciones de nombre y el puertos de host de configuración PuTTY de Hola][9]

5. <span data-ttu-id="f6db2-194">En el panel izquierdo de hello, haga clic en **conexión** > **SSH** > **Auth**y, a continuación, haga clic en **examinar** toospecify ubicación de Hello del archivo de privateKey.ppk de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="f6db2-195">archivo privateKey.ppk de Hello contiene la clave privada de hello generadas por PuTTYgen anteriormente en hello "fase 1: crear una imagen" sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f6db2-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="f6db2-196">![Captura de pantalla que muestra la jerarquía de directorios de conexión de Hola y el botón Examinar][10]</span><span class="sxs-lookup"><span data-stu-id="f6db2-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="f6db2-197">Haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-197">Click **Open**.</span></span> <span data-ttu-id="f6db2-198">Puede recibir una alerta en un cuadro de mensaje.</span><span class="sxs-lookup"><span data-stu-id="f6db2-198">You might be alerted by a message box.</span></span> <span data-ttu-id="f6db2-199">Si se ha configurado el nombre DNS de Hola y el número de puerto correctamente, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f6db2-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="f6db2-200">![Captura de pantalla que muestra la notificación de Hola][11]</span><span class="sxs-lookup"><span data-stu-id="f6db2-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="f6db2-201">Se está tooenter solicitada su nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="f6db2-201">You are prompted tooenter your username.</span></span>  
![Captura de pantalla que muestra un caso donde el nombre de usuario de tooenter][12]

8. <span data-ttu-id="f6db2-203">Escribir nombre de usuario de Hola que usa máquinas virtuales de toocreate Hola Hola "fase 1: crear una imagen" anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f6db2-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="f6db2-204">Verá algo parecido a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6db2-204">You will see something like hello following:</span></span>  
![Captura de pantalla que muestra la confirmación de la autenticación de Hola][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="f6db2-206">Fase 3: Instalación del software</span><span class="sxs-lookup"><span data-stu-id="f6db2-206">Phase 3: Install software</span></span>
<span data-ttu-id="f6db2-207">En esta fase, instale el entorno de tiempo de ejecución de Java de hello, Tomcat7 y otros componentes de Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f6db2-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="f6db2-208">Java Runtime Environment</span><span class="sxs-lookup"><span data-stu-id="f6db2-208">Java runtime environment</span></span>
<span data-ttu-id="f6db2-209">Tomcat está escrito en Java.</span><span class="sxs-lookup"><span data-stu-id="f6db2-209">Tomcat is written in Java.</span></span> <span data-ttu-id="f6db2-210">Existen dos tipos de kits de desarrollo de Java (JDK): OpenJDK y JDK de Oracle.</span><span class="sxs-lookup"><span data-stu-id="f6db2-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="f6db2-211">Puede elegir Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="f6db2-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="f6db2-212">Tanto JDK tiene casi Hola el mismo código para las clases de Hola Hola API Java y código de hello para la máquina virtual de hello es diferente.</span><span class="sxs-lookup"><span data-stu-id="f6db2-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="f6db2-213">OpenJDK suele bibliotecas abiertas toouse, mientras que Oracle JDK tiende toouse cerrado los.</span><span class="sxs-lookup"><span data-stu-id="f6db2-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="f6db2-214">JDK de Oracle tiene más clases y algunos errores corregidos. Además, JDK de Oracle es más estable que OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f6db2-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="f6db2-215">Instalación de OpenJDK</span><span class="sxs-lookup"><span data-stu-id="f6db2-215">Install OpenJDK</span></span>  

<span data-ttu-id="f6db2-216">Usar hello después toodownload OpenJDK de comando.</span><span class="sxs-lookup"><span data-stu-id="f6db2-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="f6db2-217">toocreate un toocontain directory Hola archivos JDK:</span><span class="sxs-lookup"><span data-stu-id="f6db2-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f6db2-218">archivos JDK de hello tooextract en el directorio/usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="f6db2-219">Instalación de JDK de Oracle</span><span class="sxs-lookup"><span data-stu-id="f6db2-219">Install Oracle JDK</span></span>


<span data-ttu-id="f6db2-220">Usar hello siguientes toodownload comando Oracle JDK de sitio Web de Oracle Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="f6db2-221">toocreate un toocontain directory Hola archivos JDK:</span><span class="sxs-lookup"><span data-stu-id="f6db2-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f6db2-222">archivos JDK de hello tooextract en el directorio/usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="f6db2-223">tooset Oracle JDK como Hola máquina virtual Java a predeterminada:</span><span class="sxs-lookup"><span data-stu-id="f6db2-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="f6db2-224">Confirmación de que la instalación de Java es correcta</span><span class="sxs-lookup"><span data-stu-id="f6db2-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="f6db2-225">Puede utilizar un comando como Hola después tootest si Hola Java runtime environment está instalado correctamente:</span><span class="sxs-lookup"><span data-stu-id="f6db2-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="f6db2-226">Si ha instalado OpenJDK, verá un mensaje similar Hola siguiente: ![mensaje de instalación OpenJDK correcta][14]</span><span class="sxs-lookup"><span data-stu-id="f6db2-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="f6db2-227">Si ha instalado Oracle JDK, verá un mensaje similar Hola siguiente: ![mensaje de instalación de JDK correcta de Oracle][15]</span><span class="sxs-lookup"><span data-stu-id="f6db2-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="f6db2-228">Instalación de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-228">Install Tomcat7</span></span>
<span data-ttu-id="f6db2-229">Usar hello después comando tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="f6db2-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="f6db2-230">Si no utilizas Tomcat7, utilice variación correspondiente de Hola de este comando.</span><span class="sxs-lookup"><span data-stu-id="f6db2-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="f6db2-231">Confirmación de que la instalación de Tomcat7 es correcta</span><span class="sxs-lookup"><span data-stu-id="f6db2-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="f6db2-232">toocheck si Tomcat7 se instala correctamente, busque nombre DNS del servidor de Tomcat tooyour.</span><span class="sxs-lookup"><span data-stu-id="f6db2-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="f6db2-233">En este artículo, dirección URL de ejemplo de Hola es http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="f6db2-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="f6db2-234">Si ve un mensaje similar siguiente hello, Tomcat7 está instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f6db2-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="f6db2-235">![Mensaje de instalación Tomcat7 correcta][16]</span><span class="sxs-lookup"><span data-stu-id="f6db2-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="f6db2-236">Instalación de otros componentes de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="f6db2-237">Hay otros componentes de Tomcat opcionales que puede instalar.</span><span class="sxs-lookup"><span data-stu-id="f6db2-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="f6db2-238">Hola de uso **tomcat7 de búsqueda de caché apt sudo** comando toosee todos los componentes disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="f6db2-239">Usar hello después comandos tooinstall algunos componentes útiles.</span><span class="sxs-lookup"><span data-stu-id="f6db2-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="f6db2-240">Fase 4: Configuración de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="f6db2-241">En esta fase es donde se administra Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="f6db2-242">Inicio y detención de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="f6db2-243">servidor de Tomcat7 Hola se inicia automáticamente cuando se instala.</span><span class="sxs-lookup"><span data-stu-id="f6db2-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="f6db2-244">También puede iniciarlo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f6db2-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="f6db2-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="f6db2-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="f6db2-246">estado de hello tooview de Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="f6db2-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="f6db2-247">Servicios de Tomcat toorestart:</span><span class="sxs-lookup"><span data-stu-id="f6db2-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="f6db2-248">Administración de Tomcat7</span><span class="sxs-lookup"><span data-stu-id="f6db2-248">Tomcat7 administration</span></span>
<span data-ttu-id="f6db2-249">Puede editar tooset del archivo de configuración de hello Tomcat usuario sus credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="f6db2-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="f6db2-250">Usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f6db2-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="f6db2-251">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f6db2-251">Here is an example:</span></span>  
![Captura de pantalla que muestra el resultado del comando hello sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="f6db2-253">Crear una contraseña segura para el nombre de usuario de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="f6db2-254">Después de editar este archivo, debe reiniciar servicios Tomcat7 con hello después tooensure de comando que Hola cambios surten efecto:</span><span class="sxs-lookup"><span data-stu-id="f6db2-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="f6db2-255">Abra el explorador y escriba **http://<your tomcat server DNS name>/administrador/html** como Hola dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f6db2-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="f6db2-256">Por ejemplo hello en este artículo, dirección URL de hello es http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="f6db2-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="f6db2-257">Después de conectarse, verá algo similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-257">After connecting, you should see something similar toohello following:</span></span>  
![Captura de pantalla de hello Administrador de aplicaciones Web Tomcat][18]

## <a name="common-issues"></a><span data-ttu-id="f6db2-259">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="f6db2-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="f6db2-260">No puede acceder a la máquina virtual de hello con Tomcat y Moodle de hello Internet</span><span class="sxs-lookup"><span data-stu-id="f6db2-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="f6db2-261">Síntoma</span><span class="sxs-lookup"><span data-stu-id="f6db2-261">Symptom</span></span>  
  <span data-ttu-id="f6db2-262">Tomcat se está ejecutando pero no puede ver la página predeterminada de hello Tomcat con el explorador.</span><span class="sxs-lookup"><span data-stu-id="f6db2-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="f6db2-263">Posible causa principal</span><span class="sxs-lookup"><span data-stu-id="f6db2-263">Possible root cause</span></span>   

  * <span data-ttu-id="f6db2-264">puerto de escucha de Hello Tomcat no se Hola igual que el puerto privado de Hola de punto de conexión de su máquina virtual para el tráfico de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="f6db2-265">Compruebe su puerto público y privado configuración de punto de conexión del puerto y asegúrese de que el puerto privado hello es Hola igual Hola Tomcat el puerto de escucha.</span><span class="sxs-lookup"><span data-stu-id="f6db2-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="f6db2-266">Consulte la sección de este artículo "Fase 1: Crear una imagen" para obtener instrucciones acerca de cómo configurar puntos de conexión para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f6db2-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="f6db2-267">Hola toodetermine Tomcat puerto de escucha, abra /etc/httpd/conf/httpd.conf (versión de Red Hat) o /etc/tomcat7/server.xml (Debian versión).</span><span class="sxs-lookup"><span data-stu-id="f6db2-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="f6db2-268">De forma predeterminada, puerto de escucha de Tomcat hello es 8080.</span><span class="sxs-lookup"><span data-stu-id="f6db2-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="f6db2-269">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f6db2-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="f6db2-270">Si utilizas una máquina virtual como Debian o Ubuntu y desea que toochange Hola predeterminado puerto de Tomcat escuchar (por ejemplo 8081), también debe abrir los puertos de hello para el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="f6db2-271">En primer lugar, abra el perfil de hello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="f6db2-272">A continuación, quite la última línea de Hola y cambiar "no" demasiado "Sí".</span><span class="sxs-lookup"><span data-stu-id="f6db2-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="f6db2-273">firewall de Hello deshabilitó Hola puerto de escucha de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="f6db2-274">Sólo puede ver la página de hello Tomcat predeterminada desde el host local de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="f6db2-275">problema de Hello es muy probable que el puerto de hello, que es tooby escuchaba Tomcat, está bloqueado por firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="f6db2-276">Puede usar la página de Web de hello w3m herramienta toobrowse Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="f6db2-277">Hello siguientes comandos instalación w3m y examinar la página predeterminada de Tomcat de toohello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="f6db2-278">sudo yum install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="f6db2-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="f6db2-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="f6db2-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="f6db2-280">Solución</span><span class="sxs-lookup"><span data-stu-id="f6db2-280">Solution</span></span>

  * <span data-ttu-id="f6db2-281">Si Hola puerto de escucha de Tomcat no se hello igual como puerto privado de Hola de punto de conexión de hello para la máquina virtual de tráfico toohello, es necesario cambiar el puerto privado hello toobe Hola igual Hola puerto de escucha de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f6db2-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="f6db2-282">Si el problema de hello está provocado por firewall/iptables, agregue Hola después líneas demasiado/etcetera/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="f6db2-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="f6db2-283">segunda línea de Hello solo es necesario para el tráfico https:</span><span class="sxs-lookup"><span data-stu-id="f6db2-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="f6db2-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="f6db2-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="f6db2-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="f6db2-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="f6db2-286">Asegúrese de que líneas anteriores Hola se colocan por encima de todas las líneas que global se podrían restringir el acceso, como siguiente hello: - A -j rechazar--icmp-host-prohibido con rechazo de entrada</span><span class="sxs-lookup"><span data-stu-id="f6db2-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="f6db2-287">tooreload hello iptables, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="f6db2-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="f6db2-288">Esto se ha probado en CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="f6db2-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="f6db2-289">Permiso denegado al cargar el proyecto archivos demasiado/var/lib/tomcat7/aplicaciones Web /</span><span class="sxs-lookup"><span data-stu-id="f6db2-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="f6db2-290">Síntoma</span><span class="sxs-lookup"><span data-stu-id="f6db2-290">Symptom</span></span>
  <span data-ttu-id="f6db2-291">Al usar una máquina virtual SFTP cliente (por ejemplo, FileZilla) tooconnect tooyour y navegue demasiado/var/lib/tomcat7/aplicaciones Web/toopublish su sitio, obtendrá un siguiente de toohello similar de mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="f6db2-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="f6db2-292">Posible causa principal</span><span class="sxs-lookup"><span data-stu-id="f6db2-292">Possible root cause</span></span>
  <span data-ttu-id="f6db2-293">No tener ninguna carpeta de /var/lib/tomcat7/webapps de permisos tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="f6db2-294">Solución</span><span class="sxs-lookup"><span data-stu-id="f6db2-294">Solution</span></span>  
  <span data-ttu-id="f6db2-295">Necesita permiso de tooget de cuenta de hello raíz.</span><span class="sxs-lookup"><span data-stu-id="f6db2-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="f6db2-296">Puede cambiar la propiedad de Hola de esa carpeta de nombre de usuario raíz toohello que usó al aprovisionar la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="f6db2-297">Este es un ejemplo con el nombre de la cuenta de hello azureuser:</span><span class="sxs-lookup"><span data-stu-id="f6db2-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="f6db2-298">Usar permisos de hello -R opción tooapply Hola para todos los archivos dentro de un directorio demasiado.</span><span class="sxs-lookup"><span data-stu-id="f6db2-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="f6db2-299">Este comando también funciona para directorios.</span><span class="sxs-lookup"><span data-stu-id="f6db2-299">This command also works for directories.</span></span> <span data-ttu-id="f6db2-300">cambios en las opciones -R Hola Hola permisos para todos los archivos y directorios dentro del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="f6db2-301">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f6db2-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="f6db2-302">Este comando cambia la propiedad (usuario y grupo) de todos los archivos y directorios que están dentro del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="f6db2-303">Hello siguiente comando solo cambia Hola permisos de directorio de la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6db2-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="f6db2-304">Hola archivos y carpetas dentro del directorio de hello no cambian.</span><span class="sxs-lookup"><span data-stu-id="f6db2-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
