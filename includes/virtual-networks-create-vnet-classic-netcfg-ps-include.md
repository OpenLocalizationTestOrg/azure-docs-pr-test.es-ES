## <a name="how-to-create-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="bf007-101">Creación de una red virtual mediante un archivo de configuración de red desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf007-101">How to create a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="bf007-102">Azure utiliza un archivo xml para definir todas las redes virtuales disponibles para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="bf007-102">Azure uses an xml file to define all virtual networks available to a subscription.</span></span> <span data-ttu-id="bf007-103">Dicho archivo se puede descargar y editarlo para modificar o eliminar las redes virtuales existentes, y crear otras nuevas.</span><span class="sxs-lookup"><span data-stu-id="bf007-103">You can download this file, edit it to modify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="bf007-104">En este tutorial, aprenderá a descargar dicho archivo, denominado archivo de configuración de red (o netcfg) y a editarlo para crear una red virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="bf007-104">In this tutorial, you learn how to download this file, referred to as network configuration (or netcfg) file, and edit it to create a new virtual network.</span></span> <span data-ttu-id="bf007-105">Para más información acerca del archivo de configuración de red, consulte el artículo [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Esquema de configuración de Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="bf007-105">To learn more about the network configuration file, see the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="bf007-106">Para crear una red virtual con un archivo netcfg mediante PowerShell, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bf007-106">To create a virtual network with a netcfg file using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="bf007-107">Si es la primera vez que usa Azure PowerShell, siga los pasos del artículo [Overview of Azure PowerShell](/powershell/azureps-cmdlets-docs) (Introducción a Azure PowerShell), inicie sesión en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bf007-107">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in to Azure and select your subscription.</span></span>
2. <span data-ttu-id="bf007-108">En la consola de Azure PowerShell, use el cmdlet **AzureVnetConfig Get** para descargar el archivo de configuración de red a un directorio del equipo, para lo que debe ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bf007-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file to a directory on your computer by running the following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="bf007-109">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="bf007-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="bf007-110">Abra el archivo que guardó en el paso 2 con cualquier aplicación de edición de texto o XML, y busque el elemento **<VirtualNetworkSites>**.</span><span class="sxs-lookup"><span data-stu-id="bf007-110">Open the file you saved in step 2 using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="bf007-111">Si ya tiene otras redes creadas, cada una de ellas se muestra como su propio elemento **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="bf007-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="bf007-112">Para crear la red virtual que se describe en este escenario, agregue el siguiente código XML justo debajo del elemento **<VirtualNetworkSites>** :</span><span class="sxs-lookup"><span data-stu-id="bf007-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="bf007-113">Guarde el archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="bf007-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="bf007-114">En la consola de Azure PowerShell, use el cmdlet **Set-AzureVnetConfig** para cargar el archivo de configuración de red, para lo que se debe ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bf007-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="bf007-115">Salida que se devuelve:</span><span class="sxs-lookup"><span data-stu-id="bf007-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="bf007-116">Si el valor de **OperationStatus** no es *Correcto* en la salida devuelta, compruebe si el archivo xml contiene errores y vuelva a realizar el paso 6.</span><span class="sxs-lookup"><span data-stu-id="bf007-116">If **OperationStatus** is not *Succeeded* in the returned output, check the xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="bf007-117">En la consola de Azure PowerShell, use el cmdlet **Get-AzureVnetSite** para comprobar que se ha agregado la nueva red, para lo que debe ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bf007-117">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="bf007-118">La salida devuelta (abreviada) incluye el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="bf007-118">The returned (abbreviated) output includes the following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
