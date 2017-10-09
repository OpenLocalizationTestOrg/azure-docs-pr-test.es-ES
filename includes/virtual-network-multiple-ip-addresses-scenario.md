## <a name="scenario"></a>Escenario
Una máquina virtual con una sola NIC es la red virtual tooa creado y está conectado. Hola VM requiere tres diferentes *privada* IP direcciones y dos *público* direcciones IP. se asignan direcciones IP de Hello toohello siguiendo las configuraciones de IP:

* **IPConfig-1:** asigna un dirección IP privada *estática* y una dirección IP pública *estática*.
* **IPConfig-2:** asigna un dirección IP privada *estática* y una dirección IP pública *estática*.
* **IPConfig-3:** asigna un dirección IP privada *estática* y ninguna dirección IP pública.
  
    ![Varias direcciones IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

las configuraciones IP de Hola son toohello asociado de NIC cuando se crea la NIC de Hola y Hola NIC es toohello adjunto VM cuando se crea Hola VM. tipos de Hola de direcciones IP usadas para el escenario de hello tienen fines ilustrativos. Puede asignar cualquier dirección IP y tipo de asignación que necesite.

> [!NOTE]
> Aunque Hola los pasos de este artículo asigna todos los tooa de configuraciones de IP única NIC, también puede asignar varias IP configuraciones tooany NIC en una VM de varias NIC. toolearn cómo leer toocreate una máquina virtual con varias NIC hello [crear una máquina virtual con varias NIC](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) artículo.
