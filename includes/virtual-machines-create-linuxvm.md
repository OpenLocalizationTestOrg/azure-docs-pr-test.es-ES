
1. Inicie sesión en tooyour suscripción de Azure siguiendo los pasos de hello enumerados en [conectar tooAzure de hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Asegúrese de que está en el modo de implementación clásica hello como sigue:

    ```azurecli
    azure config mode asm
    ```

3. Averiguar imagen de Linux de Hola que desea tooload de imágenes disponibles hello como sigue:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    En una ventana de símbolo del sistema de Windows, use **find** en lugar de grep.
   
4. Use `azure vm create` toocreate una máquina virtual con la imagen de Linux Hola de lista anterior Hola. En este paso se crea un servicio en la nube y una cuenta de almacenamiento. También puede conectar este servicio en la nube VM tooan existente con un `-c` opción. Crear un toolog de punto de conexión SSH en la máquina virtual de Linux toohello con hello `-e` opción. Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con hello `Ubuntu-14_04_4-LTS` imagen Hola `West US` ubicación y agrega un nombre de usuario `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Para una máquina virtual de Linux, debe proporcionar hello `-e` opción `vm create`. No es posible tooenable SSH una vez creada la máquina virtual de Hola. Para obtener más detalles sobre SSH, lea [cómo tooUse SSH con Linux en Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Puede comprobar atributos Hola de hello VM mediante hello `azure vm show` comando. Hello en el ejemplo siguiente se muestra información de máquina virtual denominada Hola `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Inicie la máquina virtual con hello `azure vm start` comando como sigue:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de estos comandos de máquina virtual de Azure CLI 1.0, lea hello [hello mediante Azure CLI 1.0 con API de implementación clásica de hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

