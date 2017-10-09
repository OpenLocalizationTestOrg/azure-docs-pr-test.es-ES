---
title: "aaaRun OpenFOAM con HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
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
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="f60ac-103">Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure</span><span class="sxs-lookup"><span data-stu-id="f60ac-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="f60ac-104">Este artículo muestra una manera de toorun OpenFoam en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60ac-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="f60ac-105">Aquí se implementa un clúster de Microsoft HPC Pack con nodos de proceso de Linux en Azure y se ejecuta un trabajo de [OpenFoam](http://openfoam.com/) con Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="f60ac-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="f60ac-106">Puede usar máquinas virtuales de Azure compatibles con RDMA para nodos de proceso de hello, para que los nodos de proceso de hello comunican a través de la red RDMA de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="f60ac-107">Otro toorun opciones OpenFoam en Azure son totalmente configurado comerciales imágenes disponibles en hello Marketplace, como del UberCloud [OpenFoam 2.3 de CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)y mediante la ejecución en [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="f60ac-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f60ac-108">OpenFOAM (del inglés, operación y manipulación de campo abierto) es un paquete de software de código abierto de cálculo de dinámicas de fluidos (CFD) que se utiliza ampliamente en ingeniería y ciencias en organizaciones académicas y comerciales.</span><span class="sxs-lookup"><span data-stu-id="f60ac-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="f60ac-109">Incluye herramientas para la creación de mallas, especialmente snappyHexMesh, una herramienta de creación de mallas en paralelo para las geometrías complejas de CAD y para el preprocesamiento y el posprocesamiento.</span><span class="sxs-lookup"><span data-stu-id="f60ac-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="f60ac-110">Casi todos los procesos que se ejecutan en paralelo, lo que permite a los usuarios tootake aprovechar hardware del equipo a su disposición.</span><span class="sxs-lookup"><span data-stu-id="f60ac-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="f60ac-111">Microsoft HPC Pack proporciona características toorun HPC a gran escala y aplicaciones en paralelo, incluidas las aplicaciones de MPI, acerca de los clústeres de máquinas virtuales de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f60ac-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="f60ac-112">HPC Pack también admite la ejecución de aplicaciones Linux HPC en máquinas virtuales de nodos de proceso Linux implementadas en un clúster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f60ac-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="f60ac-113">Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para un toousing Introducción nodos con HPC Pack de ejecución de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="f60ac-114">Este artículo se explica cómo toorun una carga de trabajo de Linux MPI con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f60ac-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="f60ac-115">Se supone que tiene cierta familiaridad con la administración del sistema Linux y con la ejecución de cargas de trabajo MPI en clústeres de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="f60ac-116">Si se usan versiones de MPI y OpenFOAM diferente de Hola que se muestran en este artículo, podría tener toomodify algunos pasos de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="f60ac-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f60ac-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f60ac-117">Prerequisites</span></span>
* <span data-ttu-id="f60ac-118">**Clúster de HPC Pack con nodos de proceso de Linux compatibles con RDMA**: implemente un clúster de HPC Pack con nodos de proceso de Linux de tamaño A8, A9, H16r o H16rm mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o un [script de Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="f60ac-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="f60ac-119">Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para requisitos previos de Hola y pasos para cualquiera de las opciones.</span><span class="sxs-lookup"><span data-stu-id="f60ac-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="f60ac-120">Si elige Hola opción de implementación de secuencia de comandos de PowerShell, vea el archivo de configuración de ejemplo de Hola en archivos de ejemplo de Hola final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="f60ac-121">Utilice este clúster de HPC Pack toodeploy un basado en Azure de configuración que consta de un nodo principal de tamaño A8 Windows Server 2012 R2 y tamaño 2 A8 SUSE Linux Enterprise Server 12 nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="f60ac-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="f60ac-122">Sustituya los valores apropiados por su nombre de suscripción y de servicio.</span><span class="sxs-lookup"><span data-stu-id="f60ac-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="f60ac-123">**Aspectos adicionales tooknow**</span><span class="sxs-lookup"><span data-stu-id="f60ac-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="f60ac-124">Para los requisitos previos de red de Linux RDMA en Azure, consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f60ac-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="f60ac-125">Si usas Hola opción de implementación de secuencia de comandos de Powershell, implementar todos los nodos de proceso de Linux de hello dentro de la conexión de red de una nube servicio toouse Hola RDMA.</span><span class="sxs-lookup"><span data-stu-id="f60ac-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="f60ac-126">Después de implementar nodos de Linux de hello, conectar SSH tooperform las tareas administrativas adicionales.</span><span class="sxs-lookup"><span data-stu-id="f60ac-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="f60ac-127">Busca los detalles de conexión de SSH de Hola para cada VM de Linux en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60ac-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="f60ac-128">**Intel MPI** -toorun OpenFOAM en SLES 12 HPC nodos de cálculo en Azure, deberá tooinstall en tiempo de ejecución Hola Intel MPI biblioteca 5 de hello [Intel.com sitio](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="f60ac-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="f60ac-129">(Intel MPI 5 ya está instalado en las imágenes de HPC basadas en CentOS).  En un paso posterior, si es necesario, instale Intel MPI en los nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="f60ac-130">tooprepare para este paso después de registrarse con Intel, siga Hola vínculo de página de web relacionados de hello confirmación correo electrónico toohello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="f60ac-131">A continuación, el vínculo para archivo .tgz de hello para la versión adecuada de Hola de MPI Intel de descarga de Hola de copia.</span><span class="sxs-lookup"><span data-stu-id="f60ac-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="f60ac-132">Este artículo se basa en Intel MPI versión 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="f60ac-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="f60ac-133">**Módulo de origen OpenFOAM** -descargar el software de módulo de origen OpenFOAM de Hola de Linux de hello [sitio OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="f60ac-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="f60ac-134">Este artículo se basa en la versión del paquete de origen 2.3.1, disponible para su descarga como OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="f60ac-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="f60ac-135">Siga las instrucciones de hello más adelante en este artículo toounpack y compile OpenFOAM Hola compute en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="f60ac-136">**EnSight** (opcional): resultados de hello toosee de la simulación OpenFOAM, descargue e instale hello [EnSight](https://www.ceisoftware.com/download/) programa de visualización y análisis.</span><span class="sxs-lookup"><span data-stu-id="f60ac-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="f60ac-137">Información de licencia y descarga son en el sitio de EnSight Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="f60ac-138">Configuración de la confianza mutua entre nodos de proceso</span><span class="sxs-lookup"><span data-stu-id="f60ac-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="f60ac-139">Ejecutar un trabajo de entre nodos en varios nodos de Linux requiere Hola nodos tootrust entre sí (por **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="f60ac-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="f60ac-140">Cuando se crea el clúster de HPC Pack Hola con hello script de implementación de Microsoft HPC Pack IaaS, script de Hola configura automáticamente una confianza mutua permanente para cuenta de administrador de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="f60ac-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="f60ac-141">Para crear en el dominio del clúster de Hola de los usuarios sin privilegios de administrador, deberá tooset temporal confianza mutua entre los nodos de hello cuando un trabajo asignado toothem y destruir relación Hola una vez completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="f60ac-142">confianza tooestablish para cada usuario, proporcione un clúster de toohello de par de claves de RSA que HPC Pack se usa para la relación de confianza de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="f60ac-143">Generación de un par de claves RSA</span><span class="sxs-lookup"><span data-stu-id="f60ac-143">Generate an RSA key pair</span></span>
<span data-ttu-id="f60ac-144">Resulta fácil toogenerate un par de claves de RSA, que contiene una clave pública y una clave privada y, a continuación, ejecutando Hola Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="f60ac-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="f60ac-145">Inicie sesión en tooa equipo Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="f60ac-146">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="f60ac-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="f60ac-147">Presione **ENTRAR** toouse Hola predeterminados hasta que se complete el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="f60ac-148">No escriba aquí una frase de contraseña. Cuando se le pida una contraseña, solo tiene que presionar **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generación de un par de claves RSA][keygen]
3. <span data-ttu-id="f60ac-150">Cambie el directorio toohello ~/.ssh directorio.</span><span class="sxs-lookup"><span data-stu-id="f60ac-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="f60ac-151">clave privada de Hola se almacena en la clave pública de hello y id_rsa en id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="f60ac-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Claves públicas y privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="f60ac-153">Agregar clúster de HPC Pack en toohello Hola par de claves</span><span class="sxs-lookup"><span data-stu-id="f60ac-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="f60ac-154">Asegúrese de un nodo principal de escritorio remoto conexión tooyour con su cuenta de administrador de HPC Pack (cuenta de administrador Hola configurar cuando se ejecuta la secuencia de comandos de implementación de hello).</span><span class="sxs-lookup"><span data-stu-id="f60ac-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="f60ac-155">Utilice toocreate estándar de procedimientos de Windows Server una cuenta de usuario de dominio dominio del clúster de hello de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f60ac-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="f60ac-156">Por ejemplo, usar hello usuario de Active Directory y la herramienta de equipos en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="f60ac-157">ejemplos de Hello en este artículo se supone que crea un usuario de dominio denominado hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="f60ac-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="f60ac-158">Cree un archivo denominado C:\cred.xml y copiar datos de clave de RSA de hello en él.</span><span class="sxs-lookup"><span data-stu-id="f60ac-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="f60ac-159">Un ejemplo de archivo de cred.xml es final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="f60ac-160">Abra un símbolo del sistema y escriba el siguiente comando hello tooset credenciales datos para hello hpclab\hpcuser cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="f60ac-161">Usar hello **extendeddata** toopass parámetro Hola nombre del archivo de C:\cred.xml que creó para datos de clave de saludo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="f60ac-162">Este comando se completa correctamente sin salida.</span><span class="sxs-lookup"><span data-stu-id="f60ac-162">This command completes successfully without output.</span></span> <span data-ttu-id="f60ac-163">Después de establecer las credenciales de Hola Hola para cuentas de usuario que necesita toorun trabajos, almacenar el archivo de cred.xml hello en una ubicación segura o elimínelo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="f60ac-164">Si ha generado el par de claves RSA de hello en uno de los nodos de Linux, recuerde que las claves de hello toodelete cuando termine de utilizarlos.</span><span class="sxs-lookup"><span data-stu-id="f60ac-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="f60ac-165">Si HPC Pack encuentra un archivo id_rsa o id_rsa.pub existentes, no establece una confianza mutua.</span><span class="sxs-lookup"><span data-stu-id="f60ac-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f60ac-166">No se recomienda ejecutar un trabajo de Linux como un administrador de clústeres en un clúster compartido, porque un trabajo enviado por un administrador se ejecuta con la cuenta raíz de Hola Hola en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="f60ac-167">Sin embargo, un trabajo enviado por un usuario sin privilegios de administrador se ejecuta bajo una cuenta de usuario local de Linux con hello mismo nombre como usuario de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="f60ac-168">En este caso, HPC Pack establece la confianza mutua para este usuario de Linux en todos los nodos de hello asignados toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="f60ac-169">Puede configurar el usuario de Linux Hola manualmente hello en nodos de Linux antes de ejecutar el trabajo de Hola o HPC Pack crea usuario Hola automáticamente cuando se envía el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="f60ac-170">Si HPC Pack crea usuario hello, HPC Pack se elimina una vez completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="f60ac-171">amenazas de seguridad tooreduce, HPC Pack quita las claves de hello tras la finalización del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="f60ac-172">Configuración de un recurso compartido de archivos para nodos de Linux</span><span class="sxs-lookup"><span data-stu-id="f60ac-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="f60ac-173">Ahora debe configurar un recurso compartido de SMB estándar en una carpeta en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="f60ac-174">tooallow Hola Linux nodos tooaccess archivos de aplicación con una ruta de acceso común, montaje Hola compartido carpeta hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="f60ac-175">Si lo desea, puede usar otra opción para compartir archivos, como un recurso compartido de archivos de Azure, recomendado para muchos escenarios, o un recurso compartido NFS.</span><span class="sxs-lookup"><span data-stu-id="f60ac-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="f60ac-176">Vea el archivo hello compartir información y pasos detallados en [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f60ac-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="f60ac-177">Cree una carpeta en el nodo principal de Hola y compártala tooEveryone estableciendo privilegios de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="f60ac-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="f60ac-178">Por ejemplo, compartir C:\OpenFOAM en el nodo principal de hello como \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="f60ac-179">En este caso, *SUSE12RDMA HN* es Hola de nombre de host del nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="f60ac-180">Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f60ac-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="f60ac-181">Hola primer comando crea una carpeta denominada /openfoam en todos los nodos de grupo de LinuxNodes Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="f60ac-182">segundo comando de Hello monta Hola compartido carpeta //SUSE12RDMA-HN/OpenFOAM hello en nodos de Linux con dir_mode y file_mode too777 de conjunto de bits.</span><span class="sxs-lookup"><span data-stu-id="f60ac-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="f60ac-183">Hola *nombre de usuario* y *contraseña* Hola comando debe ser credenciales de Hola de un usuario en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="f60ac-184">Hola "\\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f60ac-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="f60ac-185">"\\`,"significa Hola"," (coma) forma parte del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="f60ac-186">Instalación de MPI y OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="f60ac-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="f60ac-187">toorun OpenFOAM como un trabajo de MPI en red RDMA de hello, deberá toocompile OpenFOAM con bibliotecas de MPI Intel Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="f60ac-188">En primer lugar, ejecutar varios **clusrun** comandos tooinstall bibliotecas de MPI de Intel (si no está ya instalado) y OpenFOAM en los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="f60ac-189">Recurso compartido de nodo principal de hello uso previamente configurado archivos de instalación de hello tooshare entre los nodos de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f60ac-190">Estos pasos de instalación y compilación son ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f60ac-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="f60ac-191">Debe conocer algo de tooensure de administración de sistema de Linux que las bibliotecas y compiladores dependientes están instaladas correctamente.</span><span class="sxs-lookup"><span data-stu-id="f60ac-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="f60ac-192">Podría necesitar toomodify determinadas variables de entorno u otras opciones para las versiones de MPI de Intel y OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="f60ac-193">Para más información, consulte [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Guía de instalación de la biblioteca Intel MPI para Linux) y [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Instalación del paquete de origen de OpenFOAM) para su entorno.</span><span class="sxs-lookup"><span data-stu-id="f60ac-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="f60ac-194">Instalación de Intel MPI</span><span class="sxs-lookup"><span data-stu-id="f60ac-194">Install Intel MPI</span></span>
<span data-ttu-id="f60ac-195">Guardar paquete de instalación descargado de Hola para Intel MPI (l_mpi_p_5.0.3.048.tgz en este ejemplo) en C:\OpenFoam en el nodo principal de Hola para nodos de Linux de hello pueden tener acceso a este archivo desde /openfoam.</span><span class="sxs-lookup"><span data-stu-id="f60ac-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="f60ac-196">A continuación, ejecute **clusrun** biblioteca de MPI Intel tooinstall en todos los nodos de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="f60ac-197">a continuación Hola comandos del paquete de instalación copia hello y extráigalo demasiado/opt/intel en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="f60ac-198">tooinstall Intel MPI Library en modo silencioso, utilice un archivo de silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="f60ac-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="f60ac-199">Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="f60ac-200">Coloque este archivo en hello comparte /openfoam de carpeta.</span><span class="sxs-lookup"><span data-stu-id="f60ac-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="f60ac-201">Para obtener más información sobre el archivo de silent.cfg hello, consulte [Intel MPI Library for Linux Installation Guide - instalación silenciosa](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="f60ac-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f60ac-202">Asegúrese de que guarda el archivo silent.cfg como un archivo de texto con finales de línea de Linux (solo LF, no CR LF).</span><span class="sxs-lookup"><span data-stu-id="f60ac-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="f60ac-203">Este paso garantiza que se ejecuta correctamente hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="f60ac-204">Instale la biblioteca Intel MPI en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="f60ac-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="f60ac-205">Configuración de MPI</span><span class="sxs-lookup"><span data-stu-id="f60ac-205">Configure MPI</span></span>
<span data-ttu-id="f60ac-206">Para las pruebas, deberá agregar Hola seguidas de cada uno de los nodos de Linux de hello las líneas toohello /etc/security/limits.conf:</span><span class="sxs-lookup"><span data-stu-id="f60ac-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="f60ac-207">Reinicie los nodos de Linux de Hola después de actualizar el archivo de hello limits.conf.</span><span class="sxs-lookup"><span data-stu-id="f60ac-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="f60ac-208">Por ejemplo, use Hola siguiente **clusrun** comando:</span><span class="sxs-lookup"><span data-stu-id="f60ac-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="f60ac-209">Después de reiniciar, asegúrese de que esa carpeta compartida Hola se monta como /openfoam.</span><span class="sxs-lookup"><span data-stu-id="f60ac-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="f60ac-210">Compilación e instalación de OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="f60ac-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="f60ac-211">Guardar el paquete de instalación descargado de Hola para hello tooC:\OpenFoam OpenFOAM del paquete de origen (OpenFOAM 2.3.1.tgz en este ejemplo) en el nodo principal de Hola para que los nodos de Linux de hello pueden tener acceso a este archivo desde /openfoam.</span><span class="sxs-lookup"><span data-stu-id="f60ac-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="f60ac-212">A continuación, ejecute **clusrun** comandos Hola a toocompile OpenFOAM en todos los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="f60ac-213">Cree una carpeta /opt/OpenFOAM en cada nodo de Linux, copia Hola paquete toothis carpeta de origen y extráigalo no existe.</span><span class="sxs-lookup"><span data-stu-id="f60ac-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="f60ac-214">toocompile OpenFOAM con hello Intel MPI Library, primero configure algunas variables de entorno para MPI de Intel y OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="f60ac-215">Usar un script de bash llamado settings.sh tooset Hola variables.</span><span class="sxs-lookup"><span data-stu-id="f60ac-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="f60ac-216">Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="f60ac-217">Coloque este archivo (que se guarda con el fin de línea de Linux) en hello comparte /openfoam de carpeta.</span><span class="sxs-lookup"><span data-stu-id="f60ac-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="f60ac-218">Este archivo también contiene valores de hello MPI y OpenFOAM tiempos de ejecución que utilice toorun más adelante un trabajo de OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="f60ac-219">Instale los paquetes dependientes necesitados toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="f60ac-220">Dependiendo de la distribución de Linux, puede que tenga tooadd un repositorio.</span><span class="sxs-lookup"><span data-stu-id="f60ac-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="f60ac-221">Ejecutar **clusrun** comandos toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="f60ac-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="f60ac-222">Si es necesario, Hola SSH tooeach Linux nodo toorun comandos tooconfirm que se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="f60ac-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="f60ac-223">Siguiente ejecución Hola comando toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="f60ac-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="f60ac-224">proceso de compilación de Hello tarda algún tiempo toocomplete y genera una gran cantidad de salida de toostandard de información de registro, por lo que usar hello **/ intercalar** opción de salida de hello toodisplay intercalada.</span><span class="sxs-lookup"><span data-stu-id="f60ac-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="f60ac-225">Hola "\\`" símbolo de comando hello es un símbolo de escape de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f60ac-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="f60ac-226">"\\`&" significa Hola "&" forma parte del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="f60ac-227">Preparar un trabajo de OpenFOAM de toorun</span><span class="sxs-lookup"><span data-stu-id="f60ac-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="f60ac-228">Ahora toorun listo de get un trabajo de MPI llamado sloshingTank3D, que es uno de los ejemplos de hello OpenFoam, en dos nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="f60ac-229">Configurar el entorno de tiempo de ejecución de Hola</span><span class="sxs-lookup"><span data-stu-id="f60ac-229">Set up hello runtime environment</span></span>
<span data-ttu-id="f60ac-230">tooset entornos en tiempo de ejecución de Hola de MPI y OpenFOAM hello en nodos de Linux, ejecute hello siguiente comando en una ventana de Windows PowerShell en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="f60ac-231">(Este comando sólo es válido para SUSE Linux).</span><span class="sxs-lookup"><span data-stu-id="f60ac-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="f60ac-232">Preparación de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f60ac-232">Prepare sample data</span></span>
<span data-ttu-id="f60ac-233">Recurso compartido de nodo principal de Hola de uso que configuró anteriormente tooshare archivos entre los nodos de Linux de hello (montados como /openfoam).</span><span class="sxs-lookup"><span data-stu-id="f60ac-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="f60ac-234">Nodos de proceso de tooone SSH de su Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="f60ac-235">Ejecute hello después comando tooset el entorno de tiempo de ejecución de hello OpenFOAM, si aún no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="f60ac-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="f60ac-236">Copie la carpeta compartida de hello sloshingTank3D ejemplo toohello y navegue tooit.</span><span class="sxs-lookup"><span data-stu-id="f60ac-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="f60ac-237">Cuando se usan parámetros de saludo predeterminado de este ejemplo, puede tardar decenas de minutos toorun, por lo que conviene toomodify algunos toomake de parámetros que ejecute más rápido.</span><span class="sxs-lookup"><span data-stu-id="f60ac-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="f60ac-238">Una opción simple es toomodify Hola tiempo paso variables deltaT y writeInterval en el archivo de sistema/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="f60ac-239">Este archivo almacena todos los datos de entrada relacionados con toohello control de tiempo de lectura y escritura y datos de la solución.</span><span class="sxs-lookup"><span data-stu-id="f60ac-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="f60ac-240">Por ejemplo, puede cambiar valor Hola de deltaT de 0,05 too0.5 y el valor de Hola de writeInterval de too0.5 0,05.</span><span class="sxs-lookup"><span data-stu-id="f60ac-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Modificar variables de paso][step_variables]
5. <span data-ttu-id="f60ac-242">Especifique los valores deseados para las variables de hello en el archivo de sistema/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="f60ac-243">Este ejemplo utiliza dos nodos de Linux cada con 8 núcleos, por tanto, establecer numberOfSubdomains too16 y n de hierarchicalCoeffs too(1 1 16), lo que significa que ejecuta OpenFOAM en paralelo con 16 procesos.</span><span class="sxs-lookup"><span data-stu-id="f60ac-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="f60ac-244">Para más información, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guía de usuario de OpenFOAM: 3.4 Ejecución de aplicaciones en paralelo).</span><span class="sxs-lookup"><span data-stu-id="f60ac-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Descomponer procesos][decompose]
6. <span data-ttu-id="f60ac-246">Ejecute hello siguientes comandos de datos de ejemplo de Hola sloshingTank3D directory tooprepare Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="f60ac-247">En el nodo principal de hello, debería ver los archivos de datos de ejemplo de Hola se copian en C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="f60ac-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="f60ac-248">(C:\OpenFoam es carpeta compartida de hello en el nodo principal de hello).</span><span class="sxs-lookup"><span data-stu-id="f60ac-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Archivos de datos en el nodo principal de Hola][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="f60ac-250">Archivo de host para mpirun</span><span class="sxs-lookup"><span data-stu-id="f60ac-250">Host file for mpirun</span></span>
<span data-ttu-id="f60ac-251">En este paso, creará un archivo de host (una lista de nodos de proceso) que hello **mpirun** comando usa.</span><span class="sxs-lookup"><span data-stu-id="f60ac-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="f60ac-252">En uno de los nodos de Linux de hello, cree un archivo denominado archivo de host en /openfoam, por lo que este archivo se puede alcanzar en /openfoam/hostfile en todos los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="f60ac-253">Escriba los nombres de los nodos de Linux en este archivo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="f60ac-254">En este ejemplo, archivo hello contiene Hola después de nombres:</span><span class="sxs-lookup"><span data-stu-id="f60ac-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="f60ac-255">También puede crear este archivo en C:\OpenFoam\hostfile en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="f60ac-256">Si elige esta opción, guarde el script como archivo de texto con finales de línea de Linux (solo LF, no CR LF).</span><span class="sxs-lookup"><span data-stu-id="f60ac-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="f60ac-257">Esto garantiza que se ejecuta correctamente hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="f60ac-258">**Contenedor de script de Bash**</span><span class="sxs-lookup"><span data-stu-id="f60ac-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="f60ac-259">Si tiene muchos nodos de Linux y desea que su toorun de trabajo sólo en algunas de ellas, no es un toouse buena idea un host fijo de archivos, porque no sabe qué nodos se asignarán tooyour trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="f60ac-260">En este caso, escribir un contenedor de secuencias de comandos de bash para **mpirun** toocreate Hola archivo host automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f60ac-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="f60ac-261">Puede buscar un contenedor de secuencias de comandos de bash en el ejemplo se llama hpcimpirun.sh final Hola de este artículo y guárdelo como /openfoam/hpcimpirun.sh. Este script de ejemplo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f60ac-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="f60ac-262">Establece las variables de entorno de Hola para **mpirun**y algún trabajo de MPI de adición comando parámetros toorun Hola a través de la red RDMA de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="f60ac-263">En este caso, Establece Hola siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="f60ac-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="f60ac-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="f60ac-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="f60ac-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="f60ac-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="f60ac-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="f60ac-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="f60ac-267">Crea un archivo de host según toohello $ de variable de entorno CCP_NODES_CORES, que se establece mediante el nodo principal de HPC de hello cuando se activa el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="f60ac-268">formato de Hola de $CCP_NODES_CORES sigue este patrón:</span><span class="sxs-lookup"><span data-stu-id="f60ac-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="f60ac-269">donde</span><span class="sxs-lookup"><span data-stu-id="f60ac-269">where</span></span>
      
      * <span data-ttu-id="f60ac-270">`<Number of nodes>`-número de Hola de nodos asignados toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="f60ac-271">`<Name of node_n_...>`-nombre de Hola de cada nodo asignada toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="f60ac-272">`<Cores of node_n_...>`-Hola número de núcleos en el trabajo de hello nodo toothis asignado.</span><span class="sxs-lookup"><span data-stu-id="f60ac-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="f60ac-273">Por ejemplo, si el trabajo de hello necesita toorun de dos nodos, es similar a $CCP_NODES_CORES</span><span class="sxs-lookup"><span data-stu-id="f60ac-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="f60ac-274">Hola llamadas **mpirun** comando y anexa la línea de comandos de dos parámetros toohello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="f60ac-275">`--hostfile <hostfilepath>: <hostfilepath>`-crea la ruta de acceso de Hola de script de Hola del archivo de host de Hola</span><span class="sxs-lookup"><span data-stu-id="f60ac-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="f60ac-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-una variable de entorno establecida por nodo de principal de HPC Pack hello, que almacena Hola número total de núcleos asignados toothis trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="f60ac-277">En este caso, especifica el número de Hola de procesos de **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="f60ac-278">Envío de un trabajo OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="f60ac-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="f60ac-279">Ahora puede enviar un trabajo en el Administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="f60ac-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="f60ac-280">Necesitará toopass Hola script hpcimpirun.sh en líneas de comandos de Hola para algunas de las tareas de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="f60ac-281">Conecte tooyour nodo principal del clúster e inicie el Administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="f60ac-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="f60ac-282">**En administración de recursos**, asegúrese de que sean nodos de proceso de Linux de Hola Hola **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="f60ac-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="f60ac-283">Si no lo están, selecciónelos y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="f60ac-284">En **Administración de trabajos**, haga clic en **Nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="f60ac-285">Escriba un nombre para el trabajo como *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="f60ac-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Detalles del trabajo][job_details]
5. <span data-ttu-id="f60ac-287">En **recursos de trabajo**, elija Hola tipo de recurso como "Nodo" y establezca Hola mínimo too2.</span><span class="sxs-lookup"><span data-stu-id="f60ac-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="f60ac-288">Esta configuración ejecuta el trabajo de hello en dos nodos de Linux, cada uno de los cuales tiene ocho núcleos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Recursos del trabajo][job_resources]
6. <span data-ttu-id="f60ac-290">Haga clic en **editar tareas** en Hola de navegación izquierdo y, a continuación, haga clic en **agregar** tooadd un trabajo de toohello de tarea.</span><span class="sxs-lookup"><span data-stu-id="f60ac-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="f60ac-291">Agregue cuatro tareas toohello trabajo con hello siguientes líneas de comandos y configuración.</span><span class="sxs-lookup"><span data-stu-id="f60ac-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f60ac-292">Ejecuta `source /openfoam/settings.sh` configura entornos en tiempo de ejecución OpenFOAM y MPI de hello, por lo que cada uno de los siguiente las tareas de hello lo llama antes de hello OpenFOAM comando.</span><span class="sxs-lookup"><span data-stu-id="f60ac-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="f60ac-293">**Tarea 1**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-293">**Task 1**.</span></span> <span data-ttu-id="f60ac-294">Ejecutar **decomposePar** toogenerate archivos de datos para ejecutar **interDyMFoam** en paralelo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="f60ac-295">Asignar una tarea de toohello de nodo</span><span class="sxs-lookup"><span data-stu-id="f60ac-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="f60ac-296">**Línea de comandos** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="f60ac-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="f60ac-297">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="f60ac-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="f60ac-298">Vea Hola figura siguiente.</span><span class="sxs-lookup"><span data-stu-id="f60ac-298">See hello following figure.</span></span> <span data-ttu-id="f60ac-299">Configurar las tareas restantes de Hola de forma similar.</span><span class="sxs-lookup"><span data-stu-id="f60ac-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Detalles de la tarea 1][task_details1]
   * <span data-ttu-id="f60ac-301">**Tarea 2**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-301">**Task 2**.</span></span> <span data-ttu-id="f60ac-302">Ejecutar **interDyMFoam** en el ejemplo de Hola a toocompute paralelas.</span><span class="sxs-lookup"><span data-stu-id="f60ac-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="f60ac-303">Asignar dos nodos toohello tarea</span><span class="sxs-lookup"><span data-stu-id="f60ac-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="f60ac-304">**Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="f60ac-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="f60ac-305">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="f60ac-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="f60ac-306">**Tarea 3**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-306">**Task 3**.</span></span> <span data-ttu-id="f60ac-307">Ejecutar **reconstructPar** toomerge Hola conjuntos de directorios de tiempo de cada directorio processor_N_ en un único conjunto.</span><span class="sxs-lookup"><span data-stu-id="f60ac-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="f60ac-308">Asignar una tarea de toohello de nodo</span><span class="sxs-lookup"><span data-stu-id="f60ac-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="f60ac-309">**Línea de comandos** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="f60ac-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="f60ac-310">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="f60ac-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="f60ac-311">**Tarea 4**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-311">**Task 4**.</span></span> <span data-ttu-id="f60ac-312">Ejecutar **foamToEnsight** en paralelo tooconvert archivos de resultados de hello OpenFOAM en EnSight, dar formato y coloque los archivos de EnSight de hello en un directorio denominado Ensight en directorio mayúsculas Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="f60ac-313">Asignar dos nodos toohello tarea</span><span class="sxs-lookup"><span data-stu-id="f60ac-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="f60ac-314">**Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="f60ac-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="f60ac-315">**Directorio de trabajo** : /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="f60ac-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="f60ac-316">Agregar tareas de toothese de dependencias de forma ascendente de la tarea.</span><span class="sxs-lookup"><span data-stu-id="f60ac-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Dependencias de las tareas][task_dependencies]
8. <span data-ttu-id="f60ac-318">Haga clic en **enviar** toorun este trabajo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="f60ac-319">De forma predeterminada, HPC Pack envía trabajo hello como su cuenta de usuario que ha iniciado la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="f60ac-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="f60ac-320">Tras hacer clic en **enviar**, verá un cuadro de diálogo solicitándole que tooenter Hola nombre y contraseña.</span><span class="sxs-lookup"><span data-stu-id="f60ac-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Credenciales del trabajo][creds]
   
   <span data-ttu-id="f60ac-322">En determinadas condiciones, HPC Pack recuerda la información de usuario de hello antes de entrada y no mostrar este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="f60ac-323">toomake HPC Pack mostrarla de nuevo, escriba Hola siguiente comando en un símbolo del sistema y, a continuación, enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="f60ac-324">trabajo con Hello tarda de decenas de minutos tooseveral horas según los parámetros de toohello que haya definido para el ejemplo hello.</span><span class="sxs-lookup"><span data-stu-id="f60ac-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="f60ac-325">En el mapa térmico de hello, vea trabajo hello en ejecución hello en nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="f60ac-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Mapa térmico][heat_map]
   
   <span data-ttu-id="f60ac-327">En cada nodo se inician ocho procesos.</span><span class="sxs-lookup"><span data-stu-id="f60ac-327">On each node, eight processes are started.</span></span>
   
   ![Procesos de Linux][linux_processes]
10. <span data-ttu-id="f60ac-329">Cuando finalice el trabajo de hello, buscar resultados de trabajo de hello en las carpetas bajo C:\OpenFoam\sloshingTank3D y archivos de registro de hello en C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="f60ac-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="f60ac-330">Visualización de los resultados en EnSight</span><span class="sxs-lookup"><span data-stu-id="f60ac-330">View results in EnSight</span></span>
<span data-ttu-id="f60ac-331">Utilizar opcionalmente [EnSight](https://www.ceisoftware.com/) toovisualize y analizar los resultados de Hola de trabajo de OpenFOAM Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="f60ac-332">Para obtener más información acerca de la visualización y la animación en EnSight, consulte esta [guía de vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="f60ac-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="f60ac-333">Después de instalar EnSight en el nodo principal de hello, inícielo.</span><span class="sxs-lookup"><span data-stu-id="f60ac-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="f60ac-334">Abra C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="f60ac-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="f60ac-335">Verá un depósito en el Visor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-335">You see a tank in hello viewer.</span></span>
   
   ![Depósito de EnSight][tank]
3. <span data-ttu-id="f60ac-337">Crear un **Isosurface** de **internalMesh**y, a continuación, elija variable hello **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Crear una isosuperficie][isosurface]
4. <span data-ttu-id="f60ac-339">Establecer color de Hola para **Isosurface_part** creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="f60ac-340">Por ejemplo, establézcala toowater azul.</span><span class="sxs-lookup"><span data-stu-id="f60ac-340">For example, set it toowater blue.</span></span>
   
   ![Editar color de la isosuperficie][isosurface_color]
5. <span data-ttu-id="f60ac-342">Crear un **Iso-volume** de **paredes** seleccionando **paredes** en hello **elementos** panel y haga clic en hello **Isosurfaces**  botón de barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="f60ac-343">En el cuadro de diálogo de hello, seleccione **tipo** como **Isovolume** y establezca Hola Min de **Isovolume intervalo** too0.5.</span><span class="sxs-lookup"><span data-stu-id="f60ac-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="f60ac-344">toocreate Hola isovolume, haga clic en **crear con partes seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="f60ac-345">Establecer color de Hola para **Iso_volume_part** creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="f60ac-346">Por ejemplo, establézcala toodeep agua azul.</span><span class="sxs-lookup"><span data-stu-id="f60ac-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="f60ac-347">Establecer color de Hola para **paredes**.</span><span class="sxs-lookup"><span data-stu-id="f60ac-347">Set hello color for **walls**.</span></span> <span data-ttu-id="f60ac-348">Por ejemplo, establézcala tootransparent blanco.</span><span class="sxs-lookup"><span data-stu-id="f60ac-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="f60ac-349">Ahora haga clic en **reproducir** resultados de hello toosee de simulación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60ac-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Depósito resultante][tank_result]

## <a name="sample-files"></a><span data-ttu-id="f60ac-351">Archivos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f60ac-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="f60ac-352">Archivo de configuración XML de ejemplo para la implementación de clústeres mediante scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f60ac-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="f60ac-353">Archivo cred.xml de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f60ac-353">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="f60ac-354">Ejemplo silent.cfg archivo tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="f60ac-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="f60ac-355">Script de ejemplo settings.sh</span><span class="sxs-lookup"><span data-stu-id="f60ac-355">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="f60ac-356">Script hpcimpirun.sh de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f60ac-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
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
