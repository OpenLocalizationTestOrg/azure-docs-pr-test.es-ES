Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure. 

Al volver a poner su propia imagen tooAzure o incluso arranque uno de imágenes de la plataforma de hello, puede haber muchas razones, ¿por qué se obtiene una máquina Virtual en un estado no sean de arranque. Estos permiten características tooeasily, diagnosticar y recuperarse de las máquinas virtuales de los errores de arranque.

Para máquinas de virtuales de Linux, puede ver fácilmente salida de hello de su registro de la consola de hello Portal:

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Sin embargo, Windows y máquinas virtuales de Linux, Azure también permite toosee una captura de pantalla de hello VM desde el hipervisor de hello:

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones. Tenga en cuenta, capturas de pantalla y salida pueden tardar hasta too10 minutos tooappear en su cuenta de almacenamiento.

## <a name="common-boot-errors"></a>Errores comunes de arranque

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [No se encontró un sistema operativo](https://support.microsoft.com/help/4010142)
- [Error de arranque o INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Habilitación del diagnóstico en una nueva máquina virtual
1. Al crear una nueva máquina Virtual desde el Portal de vista previa de hello, seleccione hello **Azure Resource Manager** de lista desplegable de modelo de implementación de hello:
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Configurar Hola cuenta de almacenamiento de hello en tooselect de supervisión opción que desee que tooplace estos archivos de diagnóstico.
 
    ![Creación de una máquina virtual](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Si va a implementar desde una plantilla de Azure Resource Manager, navegue tooyour recurso de máquina Virtual y anexar la sección de perfil de diagnóstico de Hola. Recuerde que el encabezado de la versión de API de "2015-06-15" toouse Hola.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. perfil de diagnóstico de Hello permite cuenta de almacenamiento de hello tooselect donde desea tooput estos registros.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy una muestra de la máquina Virtual con diagnósticos de arranque habilitada, consulte nuestro repositorio aquí.

## <a name="update-an-existing-virtual-machine"></a>Actualización de una máquina virtual existente ##

tooenable el diagnóstico de arranque a través de hello Portal, también puede actualizar una máquina Virtual existente a través de hello Portal. Diagnóstico de arranque de hello seleccione opción y guardar. Reinicie el efecto de hello VM tootake.

![Actualización de una máquina virtual existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

