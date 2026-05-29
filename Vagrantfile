Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/jammy64"
    config.ssh.forward_x11 = true

    config.vm.network "forwarded_port", guest: 3080, host: 3080

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "4096"
        vb.cpus = 4
    end

    # Provision 1: instalacion del sistema (root)
    config.vm.provision "shell", inline: <<-SHELL
        # 1. Configurar instalaciones no interactivas (evita que APT pregunte cosas)
        export DEBIAN_FRONTEND=noninteractive
        echo "wireshark-common wireshark-common/install-setuid boolean true" | debconf-set-selections

        # 2. Añadir el repositorio PPA oficial de GNS3 para tener ubridge, wireshark, etc.
        apt-get update
        apt-get install -y software-properties-common
        add-apt-repository -y ppa:gns3/ppa
        apt-get update

        # 3. Instalar dependencias del sistema, incluyendo qemu, libvirt y wireshark
        apt-get install -y \
            python3-pip \
            python3-sip \
            docker.io \
            x11-apps \
            ubridge \
            wireshark \
            qemu-kvm \
			xterm \
            libvirt-daemon-system \
            libvirt-clients \
            libxcb-cursor0 \
            libgl1 \
            libgles2 \
            libegl1 \
            libegl-mesa0 \
            libxkbcommon0 \
            libxkbcommon-x11-0 \
            libdbus-1-3 \
            libxcb-icccm4 \
            libxcb-image0 \
            libxcb-keysyms1 \
            libxcb-randr0 \
            libxcb-render-util0 \
            libxcb-shape0 \
            libxcb-xinerama0 \
            libxcb-xkb1 \
            libfontconfig1 \
            libfreetype6

        # 4. Ahora que los paquetes crearon los grupos, añadimos al usuario vagrant
        # Usamos || true por si acaso el grupo kvm se llama diferente en el box
        usermod -aG docker,ubridge,libvirt,kvm,wireshark vagrant || true

        # 5. Instalar GNS3 via pip
        pip3 install PyQt6 gns3-server gns3-gui
        ln -sf /usr/local/bin/gns3 /usr/bin/gns3
    SHELL

    # Provision 2: construccion de imagenes (usuario vagrant)
    config.vm.provision "shell", privileged: false, inline: <<-SHELL
        sg docker -c "docker build -t host-vzurera /vagrant/docker/host"
        sg docker -c "docker build -t router-vzurera /vagrant/docker/router"
    SHELL
end
