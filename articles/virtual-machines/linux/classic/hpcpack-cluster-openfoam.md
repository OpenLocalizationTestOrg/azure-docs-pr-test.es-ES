---
title: "Ejecución de OpenFOAM con HPC Pack en máquinas virtuales Linux | Microsoft Docs"
description: "Implemente un clúster de Microsoft HPC Pack en Azure y ejecute un trabajo de OpenFOAM en varios nodos de ejecución de Linux en una red RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="381a2-103">Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="381a2-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="381a2-104">En este artículo se muestra una manera de ejecutar OpenFoam en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="381a2-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="381a2-105">Aquí se implementa un clúster de Microsoft HPC Pack con nodos de proceso de Linux en Azure y se ejecuta un trabajo de [OpenFoam](http://openfoam.com/) con Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="381a2-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="381a2-106">Puede usar máquinas virtuales compatibles con RDMA de Azure para los nodos de proceso para que se comuniquen a través de la red RDMA de Azure.</span><span class="sxs-lookup"><span data-stu-id="381a2-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="381a2-107">Otras opciones para ejecutar OpenFoam en Azure incluyen imágenes comerciales totalmente configuradas en Marketplace, como [OpenFoam 2.3 en CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/) de UberCloud, y la ejecución de [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="381a2-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="381a2-108">OpenFOAM (del inglés, operación y manipulación de campo abierto) es un paquete de software de código abierto de cálculo de dinámicas de fluidos (CFD) que se utiliza ampliamente en ingeniería y ciencias en organizaciones académicas y comerciales.</span><span class="sxs-lookup"><span data-stu-id="381a2-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="381a2-109">Incluye herramientas para la creación de mallas, especialmente snappyHexMesh, una herramienta de creación de mallas en paralelo para las geometrías complejas de CAD y para el preprocesamiento y el posprocesamiento.</span><span class="sxs-lookup"><span data-stu-id="381a2-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="381a2-110">Casi todos los procesos se ejecutan en paralelo, lo que permite a los usuarios aprovechar al máximo el hardware del equipo a su disposición.</span><span class="sxs-lookup"><span data-stu-id="381a2-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="381a2-111">Microsoft HPC Pack proporciona características para ejecutar aplicaciones HPC y paralelas a gran escala, incluidas las aplicaciones MPI, en clústeres de máquinas virtuales de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="381a2-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="381a2-112">HPC Pack también admite la ejecución de aplicaciones Linux HPC en máquinas virtuales de nodos de proceso Linux implementadas en un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="381a2-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="381a2-113">Consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para ver información básica relativa al uso de los nodos de proceso de Linux con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="381a2-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="381a2-114">Este artículo muestra cómo ejecutar una carga de trabajo de Linux MPI con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="381a2-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="381a2-115">Se supone que tiene cierta familiaridad con la administración del sistema Linux y con la ejecución de cargas de trabajo MPI en clústeres de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="381a2-116">Si usa versiones de MPI y OpenFOAM diferentes a las mostradas en este artículo, es posible que deba modificar algunos pasos de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="381a2-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="381a2-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="381a2-117">Prerequisites</span></span>
* <span data-ttu-id="381a2-118">**Clúster de HPC Pack con nodos de proceso de Linux compatibles con RDMA**: implemente un clúster de HPC Pack con nodos de proceso de Linux de tamaño A8, A9, H16r o H16rm mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o un [script de Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="381a2-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="381a2-119">Consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para ver los requisitos previos y los pasos para cada opción.</span><span class="sxs-lookup"><span data-stu-id="381a2-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="381a2-120">Si elige la opción de implementación de scripts de PowerShell, consulte el archivo de configuración de ejemplo en los archivos de ejemplo al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="381a2-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="381a2-121">Use esta configuración para implementar un clúster de HPC Pack basado en Azure que conste de un nodo principal de Windows Server 2012 R2 de tamaño A8 y 2 nodos de proceso SUSE Linux Enterprise Server 12 de tamaño A8.</span><span class="sxs-lookup"><span data-stu-id="381a2-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="381a2-122">Sustituya los valores apropiados por su nombre de suscripción y de servicio.</span><span class="sxs-lookup"><span data-stu-id="381a2-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="381a2-123">**Aspectos adicionales que debe conocer**</span><span class="sxs-lookup"><span data-stu-id="381a2-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="381a2-124">Para los requisitos previos de red de Linux RDMA en Azure, consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="381a2-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="381a2-125">Si elige la opción de implementar un script de Powershell, implemente todos los nodos de proceso de Linux en un servicio en la nube para usar la conexión de red RDMA.</span><span class="sxs-lookup"><span data-stu-id="381a2-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="381a2-126">Después de implementar los nodos de Linux, conéctese mediante SSH para realizar otras tareas administrativas.</span><span class="sxs-lookup"><span data-stu-id="381a2-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="381a2-127">En Azure Portal encontrará los detalles de conexión mediante SSH para las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="381a2-128">**Intel MPI** : para ejecutar OpenFOAM en nodos de proceso de SLES 12 HPC en Azure, necesita instalar el entorno de tiempo de ejecución de Intel MPI Library 5 desde el [sitio web Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="381a2-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="381a2-129">(Intel MPI 5 ya está instalado en las imágenes de HPC basadas en CentOS).  En un paso posterior, si es necesario, instale Intel MPI en los nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="381a2-130">Como preparativos para este paso, después de registrarse con Intel, siga el vínculo del mensaje de confirmación a la página web relacionada.</span><span class="sxs-lookup"><span data-stu-id="381a2-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="381a2-131">Después, copie el vínculo de descarga para el archivo .tgz de la versión correspondiente de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="381a2-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="381a2-132">Este artículo se basa en Intel MPI versión 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="381a2-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="381a2-133">**Paquete de origen OpenFOAM** : descargue el software del paquete de origen OpenFOAM para Linux desde el [sitio de OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="381a2-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="381a2-134">Este artículo se basa en la versión del paquete de origen 2.3.1, disponible para su descarga como OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="381a2-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="381a2-135">Siga las instrucciones que aparecen más adelante en este artículo para desempaquetar y compilar OpenFOAM en los nodos de ejecución de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="381a2-136">**EnSight** (opcional): para ver los resultados de la simulación de OpenFOAM, descargue e instale el programa de visualización y análisis [EnSight](https://www.ceisoftware.com/download/) .</span><span class="sxs-lookup"><span data-stu-id="381a2-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="381a2-137">Hay más información de licencia y descarga en el sitio web de EnSight.</span><span class="sxs-lookup"><span data-stu-id="381a2-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="381a2-138">Configuración de la confianza mutua entre nodos de proceso</span><span class="sxs-lookup"><span data-stu-id="381a2-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="381a2-139">La ejecución de un trabajo entre nodos en varios nodos de Linux requiere que los nodos confíen unos en otros (a través de **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="381a2-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="381a2-140">Al crear el clúster de HPC Pack con el script de implementación IaaS de Microsoft HPC Pack, el script establece automáticamente una confianza mutua permanente con la cuenta de administrador que especifique.</span><span class="sxs-lookup"><span data-stu-id="381a2-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="381a2-141">Para los usuarios sin privilegios de administrador que ha creado en el dominio del clúster, tiene que configurar la confianza mutua temporal entre los nodos cuando se les asigna un trabajo y destruir la relación una vez completado el trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="381a2-142">Para establecer la confianza para cada usuario, proporcione un par de claves RSA al clúster que usa HPC Pack para establecer la relación de confianza.</span><span class="sxs-lookup"><span data-stu-id="381a2-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="381a2-143">Generación de un par de claves RSA</span><span class="sxs-lookup"><span data-stu-id="381a2-143">Generate an RSA key pair</span></span>
<span data-ttu-id="381a2-144">Es fácil generar un par de claves RSA, con clave pública y clave privada, mediante la ejecución del comando de Linux **ssh keygen** .</span><span class="sxs-lookup"><span data-stu-id="381a2-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="381a2-145">Inicie sesión en un equipo con Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="381a2-146">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="381a2-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="381a2-147">Presione **Entrar** para usar la configuración predeterminada hasta que se complete el comando.</span><span class="sxs-lookup"><span data-stu-id="381a2-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="381a2-148">No escriba aquí una frase de contraseña. Cuando se le pida una contraseña, solo tiene que presionar **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="381a2-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generación de un par de claves RSA][keygen]
3. <span data-ttu-id="381a2-150">Cambie el directorio al directorio ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="381a2-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="381a2-151">La clave privada se almacena en id_rsa y la clave pública en id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="381a2-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Claves públicas y privadas][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="381a2-153">Adición del par de claves al clúster de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="381a2-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="381a2-154">Realice una conexión a Escritorio remoto en el nodo principal con la cuenta de administrador de HPC Pack (la cuenta de administrador que configuró al ejecutar el script de implementación).</span><span class="sxs-lookup"><span data-stu-id="381a2-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="381a2-155">Use los procedimientos estándar de Windows Server para crear una cuenta de usuario de dominio en el dominio de Active Directory del clúster.</span><span class="sxs-lookup"><span data-stu-id="381a2-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="381a2-156">Por ejemplo, use la herramienta Usuario y equipos de Active Directory en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="381a2-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="381a2-157">Los ejemplos de este artículo asumen que crean un usuario de dominio denominado hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="381a2-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="381a2-158">Cree un archivo denominado C:\cred.xml y copie los datos de la clave RSA en él.</span><span class="sxs-lookup"><span data-stu-id="381a2-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="381a2-159">Al final de este artículo se encuentra un ejemplo de archivo cred.xml.</span><span class="sxs-lookup"><span data-stu-id="381a2-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="381a2-160">Abra un símbolo del sistema y escriba el siguiente comando para establecer los datos de credenciales para la cuenta hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="381a2-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="381a2-161">Usa el parámetro **extendeddata** para pasar el nombre del archivo C:\cred.xml que creó para los datos clave.</span><span class="sxs-lookup"><span data-stu-id="381a2-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="381a2-162">Este comando se completa correctamente sin salida.</span><span class="sxs-lookup"><span data-stu-id="381a2-162">This command completes successfully without output.</span></span> <span data-ttu-id="381a2-163">Después de establecer las credenciales para las cuentas de usuario que se necesitan para ejecutar los trabajos, guarde el archivo cred.xml en una ubicación segura o elimínelo.</span><span class="sxs-lookup"><span data-stu-id="381a2-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="381a2-164">Si generó el par de claves RSA en uno de los nodos de Linux, no se olvide de eliminar las claves después de acabar de usarlas.</span><span class="sxs-lookup"><span data-stu-id="381a2-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="381a2-165">Si HPC Pack encuentra un archivo id_rsa o id_rsa.pub existentes, no establece una confianza mutua.</span><span class="sxs-lookup"><span data-stu-id="381a2-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="381a2-166">No se recomienda ejecutar un trabajo de Linux como administrador de clústeres en un clúster compartido, porque un trabajo enviado por un administrador se ejecuta bajo la cuenta raíz en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="381a2-167">Sin embargo, un trabajo enviado por un usuario sin privilegios de administrador se ejecuta en una cuenta de usuario de Linux local con el mismo nombre que el usuario de trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="381a2-168">En este caso, HPC Pack establece la confianza mutua para este usuario de Linux en todos los nodos asignados al trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="381a2-169">Puede configurar el usuario de Linux manualmente en los nodos de Linux antes de ejecutar el trabajo o bien HPC Pack crea el usuario automáticamente cuando se envía el trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="381a2-170">Si HPC Pack crea el usuario, HPC Pack lo elimina una vez finalizado el trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="381a2-171">Para reducir las amenazas de seguridad, HPC Pack quita las claves después de la finalización del trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="381a2-172">Configuración de un recurso compartido de archivos para nodos de Linux</span><span class="sxs-lookup"><span data-stu-id="381a2-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="381a2-173">Ahora, configure un recurso compartido SMB estándar en una carpeta en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="381a2-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="381a2-174">Para permitir que los nodos de Linux accedan a los archivos de aplicación con una ruta de acceso común, monte la carpeta compartida en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="381a2-175">Si lo desea, puede usar otra opción para compartir archivos, como un recurso compartido de archivos de Azure, recomendado para muchos escenarios, o un recurso compartido NFS.</span><span class="sxs-lookup"><span data-stu-id="381a2-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="381a2-176">Consulte la información y los pasos detallados sobre el uso compartido de archivos en [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="381a2-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="381a2-177">Cree una carpeta en el nodo principal y compártala con todos los usuarios estableciendo privilegios de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="381a2-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="381a2-178">Por ejemplo, comparta C:\OpenFOAM en el nodo principal como \\\\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="381a2-179">En donde *SUSE12RDMA-HN* es el nombre de host del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="381a2-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="381a2-180">Abra una ventana de Windows PowerShell y ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="381a2-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="381a2-181">El primer comando crea una carpeta denominada /openfoam en todos los nodos del grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="381a2-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="381a2-182">El segundo comando monta la carpeta compartida //SUSE12RDMA-HN/OpenFOAM en los nodos de Linux con los bits dir_mode y file_mode establecidos en 777.</span><span class="sxs-lookup"><span data-stu-id="381a2-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="381a2-183">El *nombre de usuario* y la *contraseña* del comando deben ser las credenciales de un usuario en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="381a2-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="381a2-184">El símbolo “\\`” en el segundo comando es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="381a2-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="381a2-185">“\\`,” significa que “,” (carácter de coma) forma parte del comando.</span><span class="sxs-lookup"><span data-stu-id="381a2-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="381a2-186">Instalación de MPI y OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="381a2-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="381a2-187">Para ejecutar OpenFOAM como un trabajo de MPI en la red RDMA, debe compilar OpenFOAM con las bibliotecas de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="381a2-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="381a2-188">En primer lugar, ejecute varios comandos **clusrun** para instalar las bibliotecas de Intel MPI (si todavía no están instaladas) y OpenFOAM en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="381a2-189">Use el recurso compartido de nodo principal configurado previamente para compartir los archivos de instalación entre los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="381a2-190">Estos pasos de instalación y compilación son ejemplos.</span><span class="sxs-lookup"><span data-stu-id="381a2-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="381a2-191">Necesita cierto conocimiento de la administración del sistema Linux para asegurarse de que los compiladores y las bibliotecas dependientes estén instalados correctamente.</span><span class="sxs-lookup"><span data-stu-id="381a2-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="381a2-192">Es posible que deba modificar ciertas variables de entorno u otros valores para sus versiones de Intel MPI y OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="381a2-193">Para más información, consulte [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Guía de instalación de la biblioteca Intel MPI para Linux) y [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Instalación del paquete de origen de OpenFOAM) para su entorno.</span><span class="sxs-lookup"><span data-stu-id="381a2-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="381a2-194">Instalación de Intel MPI</span><span class="sxs-lookup"><span data-stu-id="381a2-194">Install Intel MPI</span></span>
<span data-ttu-id="381a2-195">Guarde el paquete de instalación descargado para Intel MPI (l_mpi_p_5.0.3.048.tgz en este ejemplo) en C:\OpenFoam en el nodo principal para que los nodos de Linux puedan tener acceso a este archivo desde /openfoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="381a2-196">A continuación, ejecute **clusrun** para instalar la biblioteca Intel MPI en todos los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="381a2-197">Los siguientes comandos permiten copiar el paquete de instalación y extraerlo a /opt/intel en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="381a2-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="381a2-198">Para instalar la biblioteca Intel MPI de forma silenciosa, use un archivo silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="381a2-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="381a2-199">Puede encontrar un ejemplo en los archivos de ejemplo, al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="381a2-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="381a2-200">Coloque este archivo en la carpeta compartida /openfoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="381a2-201">Para más información acerca del archivo silent.cfg, consulte [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)(Guía de instalación de la biblioteca Intel MPI para Linux).</span><span class="sxs-lookup"><span data-stu-id="381a2-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="381a2-202">Asegúrese de que guarda el archivo silent.cfg como un archivo de texto con finales de línea de Linux (solo LF, no CR LF).</span><span class="sxs-lookup"><span data-stu-id="381a2-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="381a2-203">Este paso garantiza que se ejecuta correctamente en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="381a2-204">Instale la biblioteca Intel MPI en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="381a2-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="381a2-205">Configuración de MPI</span><span class="sxs-lookup"><span data-stu-id="381a2-205">Configure MPI</span></span>
<span data-ttu-id="381a2-206">Para realizar las pruebas, debe agregar las siguientes líneas al archivo /etc/security/limits.conf en cada uno de los nodos de Linux:</span><span class="sxs-lookup"><span data-stu-id="381a2-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="381a2-207">Reinicie los nodos de Linux después de actualizar el archivo limits.conf.</span><span class="sxs-lookup"><span data-stu-id="381a2-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="381a2-208">Por ejemplo, use el siguiente comando **clusrun** :</span><span class="sxs-lookup"><span data-stu-id="381a2-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="381a2-209">Después de reiniciar, asegúrese de que la carpeta compartida está montada como /openfoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="381a2-210">Compilación e instalación de OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="381a2-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="381a2-211">Guarde el paquete de instalación descargado para el paquete de origen de OpenFOAM (OpenFOAM-2.3.1.tgz en este ejemplo) en C:\OpenFoam en el nodo principal para que los nodos de Linux puedan tener acceso a este archivo desde /openfoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="381a2-212">A continuación, ejecute los comandos **clusrun** para compilar OpenFOAM en todos los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="381a2-213">Cree una carpeta /opt/OpenFOAM en cada nodo de Linux, copie el paquete de origen en esta carpeta y extráigalo allí.</span><span class="sxs-lookup"><span data-stu-id="381a2-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="381a2-214">Para compilar OpenFOAM con la biblioteca Intel MPI, configure primero algunas variables de entorno tanto para Intel MPI como para OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="381a2-215">Para definir las variables puede utilizar un script de bash llamado settings.sh.</span><span class="sxs-lookup"><span data-stu-id="381a2-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="381a2-216">Puede encontrar un ejemplo en los archivos de ejemplo, al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="381a2-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="381a2-217">Coloque este archivo (guardado con el fin de línea de Linux) en la carpeta compartida /openfoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="381a2-218">Este archivo también contiene la configuración para los tiempos de ejecución de MPI y OpenFOAM que utiliza posteriormente para ejecutar un trabajo de OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="381a2-219">Instale los paquetes dependientes necesarios para compilar OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="381a2-220">Dependiendo de la distribución de Linux, puede que primero necesite agregar un repositorio para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="381a2-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="381a2-221">Ejecute los comandos **clusrun** que sean similares al siguiente:</span><span class="sxs-lookup"><span data-stu-id="381a2-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="381a2-222">Si fuera necesario, use el script SSH con cada nodo de Linux para ejecutar los comandos y así confirmar que se ejecutan correctamente.</span><span class="sxs-lookup"><span data-stu-id="381a2-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="381a2-223">Ejecute el siguiente comando para compilar OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="381a2-224">El proceso de compilación tarda un tiempo en completarse y genera una gran cantidad de información de registro en la salida estándar, así que use la opción **/ interleaved** para mostrar el resultado intercalado.</span><span class="sxs-lookup"><span data-stu-id="381a2-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="381a2-225">El símbolo "\\`" en el segundo comando es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="381a2-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="381a2-226">"\\`&" significa que el "&" es una parte del comando.</span><span class="sxs-lookup"><span data-stu-id="381a2-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="381a2-227">Preparación para ejecutar un trabajo de OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="381a2-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="381a2-228">Prepárese ahora para ejecutar un trabajo MPI denominado sloshingTank3D, que es uno de los ejemplos de OpenFoam, en dos nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="381a2-229">Configuración de entorno en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="381a2-229">Set up the runtime environment</span></span>
<span data-ttu-id="381a2-230">Ejecute el siguiente comando en una ventana de Windows PowerShell en el nodo principal para configurar los entornos en tiempo de ejecución para MPI y OpenFOAM en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="381a2-231">(Este comando sólo es válido para SUSE Linux).</span><span class="sxs-lookup"><span data-stu-id="381a2-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="381a2-232">Preparación de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a2-232">Prepare sample data</span></span>
<span data-ttu-id="381a2-233">Use el recurso compartido del nodo principal configurado anteriormente para compartir archivos entre los nodos de Linux (montados como /openfoam).</span><span class="sxs-lookup"><span data-stu-id="381a2-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="381a2-234">Use el script ssh con uno de los nodos de ejecución de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="381a2-235">Ejecute el siguiente comando para configurar el entorno en tiempo de ejecución de OpenFOAM si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="381a2-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="381a2-236">Copie el ejemplo sloshingTank3D en la carpeta compartida y navegue hasta él.</span><span class="sxs-lookup"><span data-stu-id="381a2-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="381a2-237">Cuando use los parámetros predeterminados de este ejemplo, puede tardar decenas de minutos en ejecutarse; para que se ejecute más rápido, puede modificar algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="381a2-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="381a2-238">Una opción sencilla es modificar las variables de paso de tiempo deltaT y writeInterval en el archivo de sistema/controlDict.</span><span class="sxs-lookup"><span data-stu-id="381a2-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="381a2-239">Este archivo almacena todos los datos de entrada sobre el control de tiempo y los datos de solución de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="381a2-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="381a2-240">Por ejemplo, puede cambiar el valor de deltaT de 0,05 a 0,5 y el valor de writeInterval de 0,05 a 0,5.</span><span class="sxs-lookup"><span data-stu-id="381a2-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Modificar variables de paso][step_variables]
5. <span data-ttu-id="381a2-242">Especifique los valores deseados para las variables en el archivo system/decomposeParDict.</span><span class="sxs-lookup"><span data-stu-id="381a2-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="381a2-243">Este ejemplo utiliza dos nodos de Linux con 8 núcleos cada uno, así que establezca numberOfSubdomains en 16 y n de hierarchicalCoeffs en (1 1 16), lo que significa ejecutar OpenFOAM en paralelo con 16 procesos.</span><span class="sxs-lookup"><span data-stu-id="381a2-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="381a2-244">Para más información, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guía de usuario de OpenFOAM: 3.4 Ejecución de aplicaciones en paralelo).</span><span class="sxs-lookup"><span data-stu-id="381a2-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Descomponer procesos][decompose]
6. <span data-ttu-id="381a2-246">Ejecute los siguientes comandos desde el directorio sloshingTank3D para preparar los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="381a2-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="381a2-247">En el nodo principal, debería ver que los archivos de datos de ejemplo se copian en C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="381a2-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="381a2-248">(C:\OpenFoam es la carpeta compartida en el nodo principal).</span><span class="sxs-lookup"><span data-stu-id="381a2-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Archivos de datos en el nodo principal][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="381a2-250">Archivo de host para mpirun</span><span class="sxs-lookup"><span data-stu-id="381a2-250">Host file for mpirun</span></span>
<span data-ttu-id="381a2-251">En este paso creará un archivo de host (una lista de nodos de proceso) que utilizará el comando **mpirun** .</span><span class="sxs-lookup"><span data-stu-id="381a2-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="381a2-252">En uno de los nodos de Linux, cree un archivo denominado hostfile en /openfoam, de tal modo que se pueda encontrar este archivo en /openfoam/hostfile en todos los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="381a2-253">Escriba los nombres de los nodos de Linux en este archivo.</span><span class="sxs-lookup"><span data-stu-id="381a2-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="381a2-254">En este ejemplo, el archivo contiene los nombres siguientes:</span><span class="sxs-lookup"><span data-stu-id="381a2-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="381a2-255">También puede crear este archivo en C:\OpenFoam\hostfile en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="381a2-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="381a2-256">Si elige esta opción, guarde el script como archivo de texto con finales de línea de Linux (solo LF, no CR LF).</span><span class="sxs-lookup"><span data-stu-id="381a2-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="381a2-257">Esto garantiza que se ejecuta correctamente en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="381a2-258">**Contenedor de script de Bash**</span><span class="sxs-lookup"><span data-stu-id="381a2-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="381a2-259">Si tiene muchos nodos de Linux y quiere que el trabajo se ejecute solo en algunos, no es buena idea usar un archivo de host fijo, ya que no sabrá qué nodos se asignarán al trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="381a2-260">En este caso, escriba un contenedor de script de Bash para **mpirun** y así poder crear el archivo de host automáticamente.</span><span class="sxs-lookup"><span data-stu-id="381a2-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="381a2-261">Encontrará un contenedor de script de Bash de ejemplo denominado hpcimpirun.sh al final de este artículo, guárdelo como /openfoam/hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="381a2-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="381a2-262">Este script de ejemplo hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="381a2-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="381a2-263">Configura las variables de entorno para **mpirun**y algunos parámetros de comando adicionales para ejecutar el trabajo MPI a través de la red RDMA.</span><span class="sxs-lookup"><span data-stu-id="381a2-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="381a2-264">En este caso, establece las variables siguientes:</span><span class="sxs-lookup"><span data-stu-id="381a2-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="381a2-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="381a2-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="381a2-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="381a2-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="381a2-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="381a2-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="381a2-268">Crea un archivo de host según la variable del entorno $CCP_NODES_CORES, que establece el nodo principal de HPC cuando se activa el trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="381a2-269">El formato de $CCP_NODES_CORES sigue este patrón:</span><span class="sxs-lookup"><span data-stu-id="381a2-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="381a2-270">donde</span><span class="sxs-lookup"><span data-stu-id="381a2-270">where</span></span>
      
      * <span data-ttu-id="381a2-271">`<Number of nodes>` : número de nodos asignados a este trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="381a2-272">`<Name of node_n_...>` : nombre de cada nodo asignado a este trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="381a2-273">`<Cores of node_n_...>`: número de núcleos en el nodo asignado a este trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="381a2-274">Por ejemplo, si el trabajo necesita dos núcleos para ejecutarse, $CCP_NODES_CORES será similar a</span><span class="sxs-lookup"><span data-stu-id="381a2-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="381a2-275">Llama al comando **mpirun** y anexa dos parámetros a la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="381a2-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="381a2-276">`--hostfile <hostfilepath>: <hostfilepath>` : es la ruta de acceso del archivo de host que crea el script</span><span class="sxs-lookup"><span data-stu-id="381a2-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="381a2-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` : es una variable de entorno establecida por el nodo principal de HPC Pack, que almacena el número total de núcleos asignados a este trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="381a2-278">En este caso, especifica el número de procesos de **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="381a2-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="381a2-279">Envío de un trabajo OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="381a2-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="381a2-280">Ahora puede enviar un trabajo en el Administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="381a2-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="381a2-281">Debe pasar el script hpcimpirun.sh en las líneas de comandos para algunas de las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="381a2-282">Conéctese al nodo principal del clúster e inicie el administrador de clústeres de HPC.</span><span class="sxs-lookup"><span data-stu-id="381a2-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="381a2-283">En **Administración de recursos**, asegúrese de que los nodos de proceso de Linux están en el estado **En línea**.</span><span class="sxs-lookup"><span data-stu-id="381a2-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="381a2-284">Si no lo están, selecciónelos y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="381a2-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="381a2-285">En **Administración de trabajos**, haga clic en **Nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="381a2-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="381a2-286">Escriba un nombre para el trabajo como *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="381a2-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Detalles del trabajo][job_details]
5. <span data-ttu-id="381a2-288">En **Recursos del trabajo**, seleccione el tipo de recurso como “Nodo” y establezca el valor de Mínimo en 2.</span><span class="sxs-lookup"><span data-stu-id="381a2-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="381a2-289">Esta configuración ejecuta el trabajo de dos nodos de Linux, cada uno de los cuales tiene ocho núcleos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="381a2-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Recursos del trabajo][job_resources]
6. <span data-ttu-id="381a2-291">Haga clic en **Editar tareas** en el panel de navegación izquierdo y, luego, haga clic en **Agregar** para agregar una tarea al trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="381a2-292">Agregue cuatro tareas al trabajo con las siguientes líneas de comandos y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="381a2-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="381a2-293">La ejecución de `source /openfoam/settings.sh` configura los entornos en tiempo de ejecución de OpenFOAM y MPI, por lo que cada una de las siguientes tareas la llama antes que el comando OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="381a2-294">**Tarea 1**.</span><span class="sxs-lookup"><span data-stu-id="381a2-294">**Task 1**.</span></span> <span data-ttu-id="381a2-295">Ejecute **decomposePar** para generar archivos de datos para ejecutar **interDyMFoam** en paralelo.</span><span class="sxs-lookup"><span data-stu-id="381a2-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="381a2-296">Asigne un nodo a la tarea</span><span class="sxs-lookup"><span data-stu-id="381a2-296">Assign one node to the task</span></span>
     * <span data-ttu-id="381a2-297">**Línea de comandos** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="381a2-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="381a2-298">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="381a2-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="381a2-299">Consulte la siguiente figura.</span><span class="sxs-lookup"><span data-stu-id="381a2-299">See the following figure.</span></span> <span data-ttu-id="381a2-300">Configure las tareas restantes de forma similar.</span><span class="sxs-lookup"><span data-stu-id="381a2-300">You configure the remaining tasks similarly.</span></span>
     
     ![Detalles de la tarea 1][task_details1]
   * <span data-ttu-id="381a2-302">**Tarea 2**.</span><span class="sxs-lookup"><span data-stu-id="381a2-302">**Task 2**.</span></span> <span data-ttu-id="381a2-303">Ejecute **interDyMFoam** en paralelo para calcular el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="381a2-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="381a2-304">Asigne dos nodos a la tarea</span><span class="sxs-lookup"><span data-stu-id="381a2-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="381a2-305">**Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="381a2-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="381a2-306">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="381a2-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="381a2-307">**Tarea 3**.</span><span class="sxs-lookup"><span data-stu-id="381a2-307">**Task 3**.</span></span> <span data-ttu-id="381a2-308">Ejecute **reconstructPar** para combinar los conjuntos de directorios de tiempo de cada directorio de procesador_N_ en un único conjunto.</span><span class="sxs-lookup"><span data-stu-id="381a2-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="381a2-309">Asigne un nodo a la tarea</span><span class="sxs-lookup"><span data-stu-id="381a2-309">Assign one node to the task</span></span>
     * <span data-ttu-id="381a2-310">**Línea de comandos** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="381a2-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="381a2-311">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="381a2-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="381a2-312">**Tarea 4**.</span><span class="sxs-lookup"><span data-stu-id="381a2-312">**Task 4**.</span></span> <span data-ttu-id="381a2-313">Ejecute **foamToEnsight** en paralelo para convertir los archivos de resultados de OpenFOAM a formato EnSight y colocar los archivos de EnSight en un directorio denominado Ensight en el directorio de casos.</span><span class="sxs-lookup"><span data-stu-id="381a2-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="381a2-314">Asigne dos nodos a la tarea</span><span class="sxs-lookup"><span data-stu-id="381a2-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="381a2-315">**Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="381a2-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="381a2-316">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="381a2-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="381a2-317">Agregue dependencias a estas tareas por orden ascendente de tareas.</span><span class="sxs-lookup"><span data-stu-id="381a2-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Dependencias de las tareas][task_dependencies]
8. <span data-ttu-id="381a2-319">Haga clic en **Enviar** para ejecutar este trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="381a2-320">De forma predeterminada, HPC Pack envía el trabajo como cuenta del usuario que inició la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="381a2-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="381a2-321">Un cuadro de diálogo puede pedirle que escriba el nombre de usuario y la contraseña después de hacer clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="381a2-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Credenciales del trabajo][creds]
   
   <span data-ttu-id="381a2-323">En determinadas condiciones, HPC Pack recuerda la información de usuario que escribió y no muestra este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="381a2-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="381a2-324">Para que HPC Pack lo muestre de nuevo, escriba el siguiente comando en el símbolo del sistema y envíe el trabajo.</span><span class="sxs-lookup"><span data-stu-id="381a2-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="381a2-325">El trabajo puede tardar desde decenas de minutos a varias horas, según los parámetros que haya definido para el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="381a2-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="381a2-326">En el mapa de calor verá el trabajo en ejecución en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="381a2-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Mapa térmico][heat_map]
   
   <span data-ttu-id="381a2-328">En cada nodo se inician ocho procesos.</span><span class="sxs-lookup"><span data-stu-id="381a2-328">On each node, eight processes are started.</span></span>
   
   ![Procesos de Linux][linux_processes]
10. <span data-ttu-id="381a2-330">Cuando finalice el trabajo, busque los resultados del trabajo en las carpetas en C:\OpenFoam\sloshingTank3D y los archivos de registro en C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="381a2-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="381a2-331">Visualización de los resultados en EnSight</span><span class="sxs-lookup"><span data-stu-id="381a2-331">View results in EnSight</span></span>
<span data-ttu-id="381a2-332">Opcionalmente, puede usar [EnSight](https://www.ceisoftware.com/) para visualizar y analizar los resultados del trabajo de OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="381a2-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="381a2-333">Para obtener más información acerca de la visualización y la animación en EnSight, consulte esta [guía de vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="381a2-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="381a2-334">Después de instalar EnSight en el nodo principal, inícielo.</span><span class="sxs-lookup"><span data-stu-id="381a2-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="381a2-335">Abra C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="381a2-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="381a2-336">Verá un depósito en el visor.</span><span class="sxs-lookup"><span data-stu-id="381a2-336">You see a tank in the viewer.</span></span>
   
   ![Depósito de EnSight][tank]
3. <span data-ttu-id="381a2-338">Cree una **isosuperficie** a partir de **internalMesh** y elija la variable **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="381a2-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Crear una isosuperficie][isosurface]
4. <span data-ttu-id="381a2-340">Establezca el color del elemento **Isosurface_part** creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="381a2-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="381a2-341">Por ejemplo, establézcalo como water blue (azul agua).</span><span class="sxs-lookup"><span data-stu-id="381a2-341">For example, set it to water blue.</span></span>
   
   ![Editar color de la isosuperficie][isosurface_color]
5. <span data-ttu-id="381a2-343">Cree un **isovolumen** desde **walls** (muros) seleccionando **muros** (muros) en el panel **Parts** (Piezas) y haga clic en el botón **Isosurfaces** (Isosuperficies) de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="381a2-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="381a2-344">En el cuadro de diálogo, seleccione **Type** (Tipo) como **Isovolume** (Isovolumen) y establezca el valor mínimo de **intervalo de isovolumen** en 0,5.</span><span class="sxs-lookup"><span data-stu-id="381a2-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="381a2-345">Para crear el isovolumen, haga clic en **Create with selected parts**(Crear con piezas seleccionadas).</span><span class="sxs-lookup"><span data-stu-id="381a2-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="381a2-346">Establezca el color del elemento **Iso_volume_part** creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="381a2-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="381a2-347">Por ejemplo, establézcalo como deep water blue (azul marino).</span><span class="sxs-lookup"><span data-stu-id="381a2-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="381a2-348">Establezca el color para **muros**.</span><span class="sxs-lookup"><span data-stu-id="381a2-348">Set the color for **walls**.</span></span> <span data-ttu-id="381a2-349">Por ejemplo, establézcalo en transparent white (blanco transparente).</span><span class="sxs-lookup"><span data-stu-id="381a2-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="381a2-350">Ahora haga clic en **Reproducir** para ver los resultados de la simulación.</span><span class="sxs-lookup"><span data-stu-id="381a2-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Depósito resultante][tank_result]

## <a name="sample-files"></a><span data-ttu-id="381a2-352">Archivos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a2-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="381a2-353">Archivo de configuración XML de ejemplo para la implementación de clústeres mediante scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="381a2-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="381a2-354">Archivo cred.xml de ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a2-354">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="381a2-355">Archivo silent.cfg de ejemplo para instalar MPI</span><span class="sxs-lookup"><span data-stu-id="381a2-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="381a2-356">Script de ejemplo settings.sh</span><span class="sxs-lookup"><span data-stu-id="381a2-356">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="381a2-357">Script hpcimpirun.sh de ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a2-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
