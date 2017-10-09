## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>¿Cómo toocreate archivos de una red virtual con una configuración de red de PowerShell
Azure utiliza un toodefine de archivo xml suscripción de tooa disponibles de todas las redes virtuales. Puede descargar este archivo, editar toomodify o eliminar las redes virtuales existentes y crear nuevas redes virtuales. En este tutorial, aprenderá cómo toodownload este archivo, denominado archivo de configuración (o netcfg) de red tooas y editarlo toocreate una nueva red virtual. toolearn más información acerca del archivo de configuración de red de hello, vea hello [esquema de configuración de red virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate una red virtual con un archivo netcfg con PowerShell, Hola completa pasos:

1. Si nunca ha usado PowerShell de Azure, Hola completa los pasos de hello [cómo tooInstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) artículo, a continuación, inicie sesión en tooAzure y seleccione su suscripción.
2. Desde la consola de PowerShell de Azure de hello, utilizar hello **AzureVnetConfig Get** cmdlet toodownload Hola red archivo tooa directorio de configuración de en el equipo mediante la ejecución de hello siguiente comando: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Resultado esperado:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Abrir archivo de Hola que guardó en el paso 2 con cualquier aplicación de editor de texto o XML y buscar hello  **<VirtualNetworkSites>**  elemento. Si ya tiene otras redes creadas, cada una de ellas se muestra como su propio elemento **<VirtualNetworkSite>**.
4. red virtual de toocreate Hola descrita en este escenario, agregar Hola después XML justo debajo de hello  **<VirtualNetworkSites>**  elemento:

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
   
5. Guarde el archivo de configuración de red de Hola.
6. Desde la consola de PowerShell de Azure de hello, utilizar hello **AzureVnetConfig conjunto** cmdlet tooupload Hola del archivo de configuración mediante la ejecución de hello siguiente comando: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Salida que se devuelve:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Si **OperationStatus** no *correcto* Hola devolvía los resultados, vuelva a archivo xml de hello para errores y realiza el paso 6.

7. Desde la consola de PowerShell de Azure de hello, utilizar hello **Get AzureVnetSite** tooverify de cmdlet que Hola nueva red se agregó al ejecutar Hola siguiente comando: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Hola devuelve resultados (abreviado) incluyen Hola siguiente texto:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
