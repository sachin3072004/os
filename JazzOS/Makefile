ASM=nasm
SRC_DIR=src
BUILD_DIR=build

# Create the floppy image
floppy_image: $(BUILD_DIR)/main.img
$(BUILD_DIR)/main.img: bootloader kernel
	dd if=/dev/zero of=$(BUILD_DIR)/main.img bs=512 count=2880
	mkfs.fat -F 12 -n "JAZZOS" $(BUILD_DIR)/main.img
	dd if=$(BUILD_DIR)/bootloader.bin of=$(BUILD_DIR)/main.img conv=notrunc
	mcopy -i $(BUILD_DIR)/main.img $(BUILD_DIR)/kernel.bin "::kernel.bin"

# Build the bootloader
bootloader: $(BUILD_DIR)/bootloader.bin
$(BUILD_DIR)/bootloader.bin: $(SRC_DIR)/bootloader/boot.asm
	$(ASM) $(SRC_DIR)/bootloader/boot.asm -f bin -o $(BUILD_DIR)/bootloader.bin

# Build the kernel
kernel: $(BUILD_DIR)/kernel.bin
$(BUILD_DIR)/kernel.bin: $(SRC_DIR)/kernel/main.asm
	$(ASM) $(SRC_DIR)/kernel/main.asm -f bin -o $(BUILD_DIR)/kernel.bin

