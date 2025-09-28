Confirma el VMID con qm list y mira su configuración:
qm list
cat /etc/pve/qemu-server/<VMID>.conf

Convertir LV a archivo qcow2 (recomendado)
sudo qemu-img convert -p -O qcow2 /dev/pve/vm-100-disk-1 /mnt/backup/vm-100-disk-1.qcow2

Copiar también el pequeño LV TPM (opcional, 4M)
sudo dd if=/dev/pve/vm-100-disk-2 of=/mnt/backup/vm-100-disk-2.raw bs=1M status=progress

Copiar el fichero de configuración de la VM
sudo cp /etc/pve/qemu-server/100.conf /mnt/backup/

Restauración en la nueva instalación (resumen rápido)
Copia el qcow2 a la ubicación de storage del nuevo Proxmox o conviértelo a LV:

# copiar a storage tipo directory
sudo rsync -aH --progress /mnt/backup/vm-100-disk-1.qcow2 /var/lib/vz/images/100/

# o crear LV y volcar raw
sudo lvcreate -n vm-100-disk-1 -L 60G pve
sudo qemu-img convert -p -O raw /mnt/backup/vm-100-disk-1.qcow2 /dev/pve/vm-100-disk-1

Copiar /mnt/backup/100.conf a /etc/pve/qemu-server/100.conf y ajustar si los storage names cambian.
