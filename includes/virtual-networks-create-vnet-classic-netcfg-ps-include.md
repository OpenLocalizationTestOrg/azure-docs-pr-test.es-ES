## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="1394f-101">¿Cómo toocreate archivos de una red virtual con una configuración de red de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1394f-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="1394f-102">Azure utiliza un toodefine de archivo xml suscripción de tooa disponibles de todas las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1394f-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="1394f-103">Puede descargar este archivo, editar toomodify o eliminar las redes virtuales existentes y crear nuevas redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1394f-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="1394f-104">En este tutorial, aprenderá cómo toodownload este archivo, denominado archivo de configuración (o netcfg) de red tooas y editarlo toocreate una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="1394f-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="1394f-105">toolearn más información acerca del archivo de configuración de red de hello, vea hello [esquema de configuración de red virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="1394f-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="1394f-106">toocreate una red virtual con un archivo netcfg con PowerShell, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="1394f-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="1394f-107">Si nunca ha usado PowerShell de Azure, Hola completa los pasos de hello [cómo tooInstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) artículo, a continuación, inicie sesión en tooAzure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1394f-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="1394f-108">Desde la consola de PowerShell de Azure de hello, utilizar hello **AzureVnetConfig Get** cmdlet toodownload Hola red archivo tooa directorio de configuración de en el equipo mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1394f-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="1394f-109">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="1394f-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="1394f-110">Abrir archivo de Hola que guardó en el paso 2 con cualquier aplicación de editor de texto o XML y buscar hello  **<VirtualNetworkSites>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="1394f-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="1394f-111">Si ya tiene otras redes creadas, cada una de ellas se muestra como su propio elemento **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="1394f-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="1394f-112">red virtual de toocreate Hola descrita en este escenario, agregar Hola después XML justo debajo de hello  **<VirtualNetworkSites>**  elemento:</span><span class="sxs-lookup"><span data-stu-id="1394f-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="1394f-113">Guarde el archivo de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="1394f-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="1394f-114">Desde la consola de PowerShell de Azure de hello, utilizar hello **AzureVnetConfig conjunto** cmdlet tooupload Hola del archivo de configuración mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1394f-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="1394f-115">Salida que se devuelve:</span><span class="sxs-lookup"><span data-stu-id="1394f-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="1394f-116">Si **OperationStatus** no *correcto* Hola devolvía los resultados, vuelva a archivo xml de hello para errores y realiza el paso 6.</span><span class="sxs-lookup"><span data-stu-id="1394f-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="1394f-117">Desde la consola de PowerShell de Azure de hello, utilizar hello **Get AzureVnetSite** tooverify de cmdlet que Hola nueva red se agregó al ejecutar Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1394f-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="1394f-118">Hola devuelve resultados (abreviado) incluyen Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="1394f-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
