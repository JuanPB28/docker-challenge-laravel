# Laravel Project

## How to use
...

### No puedo añadir todos los servicios desde el 'docker compose up -d ...' porque alugnos servicios dependen de 'workspace' y hay un error en el script del instalador o algo por el estilo, ya que da un error relacionado con la instalación de node en el contenedor o algo relacionado: 

[internal] load build definition from Dockerfile
	transferring 73028/0 0.011
[internal] load metadata for docker.io/laradock/workspace:master-8.3
[internal] load .dockerignore
[internal] load build context
	transferring 446/0 0.005
[  1/116] FROM docker.io/laradock/workspace:master-8.3@sha256:f7e17e946182ce8e7d70c5b0039134b0b556c43b223ceb3d348d129e2685e61f
[  3/116] RUN set -xe;     apt-get update -yqq &&     pecl channel-update pecl.php.net &&     groupadd -g 1000 laradock &&     useradd -l -u 1000 -g laradock -m laradock -G docker_env &&     usermod -p "*" laradock -s /bin/bash &&     apt-get install -yqq       apt-utils       libzip-dev zip unzip       php8.3-zip       nasm &&       php -m | grep -q 'zip'
[  2/116] RUN if [ false = true ]; then     sed -i "s@http://.*archive.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list;     sed -i "s@http://.*security.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list;   fi;
[  4/116] RUN ln -snf /usr/share/zoneinfo/UTC+1 /etc/localtime && echo UTC+1 > /etc/timezone
[  5/116] COPY ./aliases.sh /root/aliases.sh
[  6/116] COPY ./aliases.sh /home/laradock/aliases.sh
[  7/116] RUN sed -i 's/\r//' /root/aliases.sh &&     sed -i 's/\r//' /home/laradock/aliases.sh &&     chown laradock:laradock /home/laradock/aliases.sh &&     echo "" >> ~/.bashrc &&     echo "# Load Custom Aliases" >> ~/.bashrc &&     echo "source ~/aliases.sh" >> ~/.bashrc && 	  echo "" >> ~/.bashrc
[  8/116] RUN echo "" >> ~/.bashrc &&     echo "# Load Custom Aliases" >> ~/.bashrc &&     echo "source ~/aliases.sh" >> ~/.bashrc && 	  echo "" >> ~/.bashrc
[  9/116] COPY ./composer.json /home/laradock/.composer/composer.json
[ 10/116] COPY ./auth.json /home/laradock/.composer/auth.json
[ 11/116] RUN chown -R laradock:laradock /home/laradock/.composer
[ 12/116] RUN echo "" >> ~/.bashrc &&     echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc
[ 13/116] RUN set -eux;       if [ "2" = "1" ] || [ "2" = "2" ] || [ "2" = "2.2" ]; then           composer self-update --2;       else           composer self-update 2;       fi
	+ [ 2 = 1 ]
	+ [ 2 = 2 ]
	+ composer self-update --2
	Storing "stable" as default update channel for the next self-update run.
	You are already using the latest available Composer version 2.8.2 (2.x channel).
[ 14/116] RUN if [ true = true ]; then     composer global install ;fi
	Changed current directory to /home/laradock/.composer
	No composer.lock file present. Updating dependencies to latest instead of installing from lock file. See https://getcomposer.org/install for more information.
	Loading composer repositories with package information
	Updating dependencies
	Nothing to modify in lock file
	Writing lock file
	Installing dependencies from lock file (including require-dev)
	Nothing to install, update or remove
	Generating autoload files
[ 15/116] RUN if [ false = false ]; then     rm /home/laradock/.composer/auth.json ;fi
[ 16/116] RUN if [  ]; then     composer config -g repo.packagist composer  ;fi
[ 17/116] RUN echo "" >> ~/.bashrc &&     echo 'export PATH="~/.composer/vendor/bin:$PATH"' >> ~/.bashrc
[ 18/116] RUN echo "" >> ~/.bashrc &&     echo 'export PATH="/var/www/vendor/bin:$PATH"' >> ~/.bashrc
[ 19/116] COPY ./crontab /etc/cron.d
[ 20/116] RUN chmod -R 644 /etc/cron.d
[ 21/116] COPY ./ca-certificates/* /usr/local/share/ca-certificates/
[ 22/116] RUN update-ca-certificates
	Updating certificates in /etc/ssl/certs...
	0 added, 0 removed; done.
	Running hooks in /etc/ca-certificates/update.d...
	done.
[ 23/116] RUN if [ false = true ]; then     apt-get -qq -y install mysql-client &&     curl -fsSL -o /usr/local/bin/drush https://github.com/drush-ops/drush/releases/download/8.4.6/drush.phar | bash &&     chmod +x /usr/local/bin/drush &&     drush core-status ;fi
[ 24/116] RUN if [ false = true ]; then     curl -fsSL -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar | bash &&     chmod +x /usr/local/bin/wp ;fi
[ 25/116] RUN set -eux;     if [ false = true ]; then       apt-get -yqq install php8.3-bz2;     fi;     if [ false = true ]; then       apt-get -yqq install php8.3-gmp;     fi;     if [ false = true ]; then         apt-get -yqq install php8.3-gnupg;     fi;     if [ false = true ]; then       apt-get -yqq install libssh2-1-dev php8.3-ssh2;     fi;     if [ false = true ]; then       apt-get -yqq install libxml2-dev php8.3-soap;     fi;     if [ false = true ]; then       apt-get -yqq install libxslt-dev php8.3-xsl;     fi
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
[ 26/116] RUN set -eux;     if [ false = true ]; then         apt-get install -yqq libldap2-dev php8.3-ldap;     fi;     if [ false = true ]; then         apt-get install -yqq smbclient php8.3-smbclient coreutils;     fi;     if [ false = true ]; then         apt-get install -yqq php8.3-imap;     fi;     if [ false = true ]; then         apt-get install -yqq subversion;     fi
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
	+ [ false = true ]
[ 27/116] RUN if [ false = true ]; then   apt-get install -yqq pkg-config php-xml php8.3-xml &&   if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ] || { [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && { [ $(php -r "echo PHP_MINOR_VERSION;") = "4" ] || [ $(php -r "echo PHP_MINOR_VERSION;") = "3" ] ;} ;}; then     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]; then       pecl install xdebug-3.3.0;     else       pecl install xdebug-3.1.6;     fi;   else     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then       pecl install xdebug-2.5.5;     else       if [ $(php -r "echo PHP_MINOR_VERSION;") = "0" ]; then         pecl install xdebug-2.9.0;       else         pecl install xdebug-2.9.8;       fi     fi   fi &&   echo "zend_extension=xdebug.so" >> /etc/php/8.3/cli/conf.d/20-xdebug.ini ;fi
[ 28/116] COPY ./xdebug.ini /etc/php/8.3/cli/conf.d/xdebug.ini
[ 29/116] RUN if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ] || { [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && { [ $(php -r "echo PHP_MINOR_VERSION;") = "4" ] || [ $(php -r "echo PHP_MINOR_VERSION;") = "3" ] ;} ;}; then   sed -i "s/xdebug.remote_host=/xdebug.client_host=/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_connect_back=0/xdebug.discover_client_host=false/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_port=9000/xdebug.client_port=9000/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.profiler_enable=0/; xdebug.profiler_enable=0/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.profiler_output_dir=/xdebug.output_dir=/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_mode=req/; xdebug.remote_mode=req/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_autostart=0/xdebug.start_with_request=yes/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_enable=0/xdebug.mode=debug/" /etc/php/8.3/cli/conf.d/xdebug.ini ;else   sed -i "s/xdebug.remote_autostart=0/xdebug.remote_autostart=1/" /etc/php/8.3/cli/conf.d/xdebug.ini &&   sed -i "s/xdebug.remote_enable=0/xdebug.remote_enable=1/" /etc/php/8.3/cli/conf.d/xdebug.ini ;fi
[ 30/116] RUN sed -i "s/xdebug.cli_color=0/xdebug.cli_color=1/" /etc/php/8.3/cli/conf.d/xdebug.ini
[ 31/116] RUN if [ false = true ]; then   if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]  || { [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && [ $(php -r "echo PHP_MINOR_VERSION;") != "0" ]; }; then     pecl install pcov &&     echo "extension=pcov.so" >> /etc/php/8.3/cli/php.ini &&     echo "pcov.enabled" >> /etc/php/8.3/cli/php.ini   ;fi ;fi
[ 32/116] RUN if [ false = true ]; then     apt-get install -y --force-yes php8.3-phpdbg ;fi
[ 33/116] RUN if [ false = false -a false = true ]; then     curl -L https://packages.blackfire.io/gpg.key | apt-key add - &&     echo "deb http://packages.blackfire.io/debian any main" | tee /etc/apt/sources.list.d/blackfire.list &&     apt-get update -yqq &&     apt-get install blackfire-agent ;fi
[ 34/116] COPY insecure_id_rsa /tmp/id_rsa
[ 35/116] COPY insecure_id_rsa.pub /tmp/id_rsa.pub
[ 36/116] RUN if [ false = true ]; then     rm -f /etc/service/sshd/down &&     cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys         && cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub         && cat /tmp/id_rsa >> /root/.ssh/id_rsa         && rm -f /tmp/id_rsa*         && chmod 644 /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub     && chmod 400 /root/.ssh/id_rsa     && cp -rf /root/.ssh /home/laradock     && chown -R laradock:laradock /home/laradock/.ssh ;fi
[ 37/116] RUN if [ false = true ]; then     apt-get install -yqq pkg-config &&     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then       pecl install mongo;       echo "extension=mongo.so" >> /etc/php/8.3/mods-available/mongo.ini;       ln -s /etc/php/8.3/mods-available/mongo.ini /etc/php/8.3/cli/conf.d/30-mongo.ini;       php -m | grep -oiE '^mongo$';     else       if [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && [ $(php -r "echo PHP_MINOR_VERSION;") != "4" ]; then         if [ $(php -r "echo PHP_MINOR_VERSION;") = "0" ] || [ $(php -r "echo PHP_MINOR_VERSION;") = "1" ]; then           pecl install mongodb-1.9.2;         else           pecl install mongodb-1.16.2;         fi;       else         pecl install mongodb;       fi;       echo "extension=mongodb.so" >> /etc/php/8.3/mods-available/mongodb.ini;       ln -s /etc/php/8.3/mods-available/mongodb.ini /etc/php/8.3/cli/conf.d/30-mongodb.ini;       php -m | grep -oiE '^mongodb$';     fi; fi
[ 38/116] RUN if [ false = true ]; then     apt-get install -yqq librabbitmq-dev &&     if [ 8.3 = "7.3" ]       || [ 8.3 = "7.2" ]       || [ 8.3 = "7.1" ]       || [ 8.3 = "7.0" ]       || [ 8.3 = "5.6" ]; then       printf "\n" | pecl install amqp-1.11.0;     else       printf "\n" | pecl install amqp;     fi &&     echo "extension=amqp.so" >> /etc/php/8.3/mods-available/amqp.ini &&     ln -s /etc/php/8.3/mods-available/amqp.ini /etc/php/8.3/cli/conf.d/30-amqp.ini &&     php -m | grep -oiE '^amqp$' ;fi
[ 39/116] RUN if [ false = true ]; then     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]; then       echo "PHP Driver for Cassandra is not supported for PHP 8.0.";     else       apt-get install libgmp-dev -yqq &&       curl https://downloads.datastax.com/cpp-driver/ubuntu/18.04/dependencies/libuv/v1.35.0/libuv1-dev_1.35.0-1_amd64.deb -o libuv1-dev.deb &&       curl https://downloads.datastax.com/cpp-driver/ubuntu/18.04/dependencies/libuv/v1.35.0/libuv1_1.35.0-1_amd64.deb -o libuv1.deb &&       curl https://downloads.datastax.com/cpp-driver/ubuntu/18.04/cassandra/v2.16.0/cassandra-cpp-driver-dev_2.16.0-1_amd64.deb -o cassandra-cpp-driver-dev.deb &&       curl https://downloads.datastax.com/cpp-driver/ubuntu/18.04/cassandra/v2.16.0/cassandra-cpp-driver_2.16.0-1_amd64.deb -o cassandra-cpp-driver.deb &&       dpkg -i libuv1.deb &&       dpkg -i libuv1-dev.deb &&       dpkg -i cassandra-cpp-driver.deb &&       dpkg -i cassandra-cpp-driver-dev.deb &&       rm libuv1.deb libuv1-dev.deb cassandra-cpp-driver-dev.deb cassandra-cpp-driver.deb &&       cd /usr/src &&       git clone https://github.com/datastax/php-driver.git &&       cd /usr/src/php-driver/ext &&       phpize &&       mkdir /usr/src/php-driver/build &&       cd /usr/src/php-driver/build &&       ../ext/configure > /dev/null &&       make clean >/dev/null &&       make >/dev/null 2>&1 &&       make install &&       echo "extension=cassandra.so" >> /etc/php/8.3/mods-available/cassandra.ini &&       ln -s /etc/php/8.3/mods-available/cassandra.ini /etc/php/8.3/cli/conf.d/30-cassandra.ini;     fi ;fi
[ 40/116] RUN if [ false = true ]; then     add-apt-repository -y ppa:ondrej/pkg-gearman &&     apt-get update &&     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ]; then       apt-get install php8.3-gearman -y      ; else       apt-get install php-gearman -y      ;fi ;fi
[ 41/116] RUN if [ true = true ]; then     apt-get update     && apt-get install -yqq php8.3-redis ;fi
	Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [128 kB]
	Hit:2 http://ppa.launchpad.net/ondrej/php/ubuntu focal InRelease
	Hit:3 http://archive.ubuntu.com/ubuntu focal InRelease
	Get:4 http://archive.ubuntu.com/ubuntu focal-updates InRelease [128 kB]
	Get:5 http://security.ubuntu.com/ubuntu focal-security/main Sources [413 kB]
	Get:6 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [1,275 kB]
	Get:7 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [4,083 kB]
	Get:8 http://archive.ubuntu.com/ubuntu focal-backports InRelease [128 kB]
	Get:9 http://archive.ubuntu.com/ubuntu focal-updates/main Sources [752 kB]
	Get:10 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [4,546 kB]
	Fetched 11.5 MB in 2s (6,594 kB/s)
	Reading package lists...
	Selecting previously unselected package php8.3-redis.
	(Reading database ...(Reading database ... 5%
(Reading database ... 10%
(Reading database ... 15%
(Reading database ... 20%
(Reading database ... 25%
(Reading database ... 30%
(Reading database ... 35%
(Reading database ... 40%
(Reading database ... 45%
(Reading database ... 50%
(Reading database ... 55%
(Reading database ... 60%(Reading database ... 65%(Reading database ... 70%(Reading database ... 75%(Reading database ... 80%(Reading database ... 85%(Reading database ... 90%(Reading database ... 95%(Reading database ... 100%
(Reading database ... 28346 files and directories currently installed.)
	Preparing to unpack .../php8.3-redis_6.0.2-4+ubuntu20.04.1+deb.sury.org+1_amd64.deb ...
	Unpacking php8.3-redis (6.0.2-4+ubuntu20.04.1+deb.sury.org+1) ...
	Setting up php8.3-redis (6.0.2-4+ubuntu20.04.1+deb.sury.org+1) ...
	Processing triggers for php8.3-cli (8.3.13-1+ubuntu20.04.1+deb.sury.org+1) ...
[ 42/116] RUN set -eux;     if [ false = true ]; then       if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then         echo '' | pecl -q install swoole-2.0.10;       elif [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && [ $(php -r "echo PHP_MINOR_VERSION;") = "0" ]; then         echo '' | pecl -q install swoole-4.3.5;       elif [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ] && [ $(php -r "echo PHP_MINOR_VERSION;") = "1" ]; then         echo '' | pecl -q install swoole-4.5.11;       elif [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ]; then         echo '' | pecl -q install swoole-4.8.12;       elif [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]; then         echo '' | pecl -q install swoole-5.1.2;       else         echo '' | pecl -q install swoole;       fi;       echo "extension=swoole.so" >> /etc/php/8.3/mods-available/swoole.ini;       ln -s /etc/php/8.3/mods-available/swoole.ini /etc/php/8.3/cli/conf.d/20-swoole.ini;       php -m | grep -q 'swoole';     fi
	+ [ false = true ]
[ 43/116] RUN set -eux;     if [ false = true ]; then       if [ $(php -r "echo PHP_MAJOR_VERSION;") != "5" ]; then         echo '' | pecl -q install xlswriter &&         echo "extension=xlswriter.so" >> /etc/php/8.3/mods-available/xlswriter.ini &&         ln -s /etc/php/8.3/mods-available/xlswriter.ini /etc/php/8.3/cli/conf.d/20-xlswriter.ini &&         php -m | grep -q 'xlswriter';       else         echo "PHP Extension for xlswriter is not supported for PHP 5.0";       fi     ;fi
	+ [ false = true ]
[ 44/116] RUN if [ "false" = true ]; then     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "7" ]; then       pecl install taint &&       echo "extension=taint.so" >> /etc/php/8.3/mods-available/taint.ini &&       ln -s /etc/php/8.3/mods-available/taint.ini /etc/php/8.3/cli/conf.d/20-taint.ini &&       php -m | grep -q 'taint';     fi ;fi
[ 45/116] RUN if [ false = true ]; then     apt-get -yqq install libpng16-16 ;fi
[ 46/116] RUN if [ false = true ]; then     if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then       pecl -q install inotify-0.1.6 &&       echo "extension=inotify.so" >> /etc/php/8.3/mods-available/inotify.ini &&       ln -s /etc/php/8.3/mods-available/inotify.ini /etc/php/8.3/cli/conf.d/20-inotify.ini;     else       pecl -q install inotify &&       echo "extension=inotify.so" >> /etc/php/8.3/mods-available/inotify.ini &&       ln -s /etc/php/8.3/mods-available/inotify.ini /etc/php/8.3/cli/conf.d/20-inotify.ini     ;fi ;fi
[ 47/116] RUN if [ true = true ]; then     if [ $(php -r "echo PHP_MAJOR_VERSION;") != "5" ]; then         printf "\n" | pecl -q install ast-1.0.10 &&         echo "extension=ast.so" >> /etc/php/8.3/mods-available/ast.ini &&         phpenmod -v 8.3 -s cli ast     ;fi ;fi
	configuration option "php_ini" is not set to php.ini location
	You should add "extension=ast.so" to php.ini
[ 48/116] RUN if [ false = true ]; then     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 47FE03C1     && add-apt-repository -y ppa:hadret/fswatch     || apt-get update -yqq     && apt-get -y install fswatch ;fi
[ 49/116] RUN if [ false = true ]; then     apt-get install -yqq graphviz ;fi
[ 50/116] RUN if [ false = true ]; then     if [ 8.3 != "8.3" ]       && [ 8.3 != "8.0" ]; then       curl -L -o /tmp/ioncube_loaders_lin_x86-64.tar.gz https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz       && tar zxpf /tmp/ioncube_loaders_lin_x86-64.tar.gz -C /tmp       && mv /tmp/ioncube/ioncube_loader_lin_8.3.so $(php -r "echo ini_get('extension_dir');")/ioncube_loader.so       && echo "zend_extension=ioncube_loader.so" >> /etc/php/8.3/mods-available/ioncube.ini       && ln -s /etc/php/8.3/mods-available/ioncube.ini /etc/php/8.3/cli/conf.d/0ioncube.ini       && rm -rf /tmp/ioncube*       && php -m | grep -oiE '^ionCube Loader$'     ;fi ;fi
[ 51/116] RUN if [ false = true ]; then     apt-get -y install mysql-client &&     curl https://github.com/hechoendrupal/drupal-console-launcher/releases/download/1.9.7/drupal.phar -L -o drupal.phar &&     mv drupal.phar /usr/local/bin/drupal &&     chmod +x /usr/local/bin/drupal ;fi
[ 52/116] RUN if [ true = true ]; then     mkdir -p /home/laradock/.nvm &&     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash         && . /home/laradock/.nvm/nvm.sh         && nvm install node         && nvm use node         && nvm alias node         && npm cache clear --force         && npm config set fetch-retries 2         && npm config set fetch-retry-factor 10         && npm config set fetch-retry-mintimeout 10000         && npm config set fetch-retry-maxtimeout 60000         && if [  ]; then         npm config set registry          ;fi         && if [ true = true ]; then         npm install -g gulp         ;fi         && if [ false = true ]; then         npm install -g bower         ;fi         && if [ true = true ]; then         npm install -g @vue/cli         ;fi         && if [ false = true ]; then         npm install -g @angular/cli         ;fi         && if [ false = true ]; then         npm install -g npm-check-updates         ;fi ;fi
	% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
	Dload  Upload   Total   Spent    Left  Speed
	0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--0100 15916  100 15916    0     0  75075      0 --:--:-- --:--:-- --:--:-- 75075
	=> Downloading nvm from git to '/home/laradock/.nvm'
	=>Cloning into '/home/laradock/.nvm'...
	* (HEAD detached at FETCH_HEAD)
	master
	=> Compressing and cleaning up git repository
	
	=> Appending nvm source string to /home/laradock/.bashrc
	=> Appending bash_completion source string to /home/laradock/.bashrc
	=> Installing Node.js version node
	Downloading and installing node v23.1.0...
	Downloading https://nodejs.org/dist/v23.1.0/node-v23.1.0-linux-x64.tar.xz...
	#1.8%##########13.9%#####################                                                     29.6%###############################                                           43.8%##########################################                                58.4%######################################################                    75.9%##################################################################        92.7%######################################################################## 100.0%
	Computing checksum with sha256sum
	Checksums matched!
	Now using node v23.1.0 (npm v10.9.0)
	Creating default alias: [0;32mdefault[0m [0;90m->[0m [0;32mnode[0m ([0;90m->[0m [0;32mv23.1.0[0m)
	=> Node.js version node has been successfully installed
	=> Close and reopen your terminal to start using nvm or run the following to use it now:
	
	export NVM_DIR="$HOME/.nvm"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
	[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
	v23.1.0 is already installed.
	/bin/sh: 3319: [: -ne: unexpected operator
	/bin/sh: 3323: [: -ne: unexpected operator
	Now using node v23.1.0 (npm v10.9.0)
	/bin/sh: 3335: [: -ne: unexpected operator
	Now using node v23.1.0 (npm v10.9.0)
	[0;32mnode[0m [0;90m->[0m [0;32mstable[0m ([0;90m->[0m [0;32mv23.1.0[0m) [0;37m(default)[0m
	npm warn using --force Recommended protections disabled.
	(node:3512) ExperimentalWarning: CommonJS module /home/laradock/.nvm/versions/node/v23.1.0/lib/node_modules/npm/node_modules/debug/src/node.js is loading ES Module /home/laradock/.nvm/versions/node/v23.1.0/lib/node_modules/npm/node_modules/supports-color/index.js using require().
	Support for loading ES Module in require() is an experimental feature and might change at any time
	(Use `node --trace-warnings ...` to show where the warning was created)
	(node:3567) ExperimentalWarning: CommonJS module /home/laradock/.nvm/versions/node/v23.1.0/lib/node_modules/npm/node_modules/debug/src/node.js is loading ES Module /home/laradock/.nvm/versions/node/v23.1.0/lib/node_modules/npm/node_modules/supports-color/index.js using require().
	Support for loading ES Module in require() is an experimental feature and might change at any time
	(Use `node --trace-warnings ...` to show where the warning was created)

