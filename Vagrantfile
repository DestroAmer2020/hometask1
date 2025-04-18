Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos9s"
  config.vm.network "forwarded_port", guest: 8080, host: 8899

  config.vm.synced_folder "./www-content", "/home/vagrant/www-content"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL
     # Встановлюємо epel-release і nginx
     yum install -y epel-release
     yum install -y nginx

     # Видаляємо стандартний конфіг nginx
     rm -f /etc/nginx/conf.d/default.conf || true

     # Створюємо свій конфіг
     cat > /etc/nginx/conf.d/www-content.conf <<EOF
server {  
  listen       8080;
  server_name  localhost;

  location / {
      root   /home/vagrant/www-content;
      index  index.html index.htm;
  }
    error_page 404 /404.html;
}
EOF

     # Вимикаємо SELinux
     setenforce 0
     sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config

     # Дозволяємо порт 80 у фаєрволі
     firewall-cmd --permanent --add-port=80/tcp
     firewall-cmd --reload

     # Перезапускаємо nginx
     systemctl restart nginx
     systemctl enable nginx
  SHELL
end