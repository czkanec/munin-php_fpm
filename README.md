munin-php_fpm
=============


## PHP config
<code>nano /etc/php/5.6/fpm/pool.d/www.conf</code> <br>
uncomment 
> pm.status_path = /status


## munin config
<code>nano /etc/munin/plugin-conf.d/munin-node</code>

> [php-fpm_*]<br>
> user www-data<br>
> env.SOCKET /run/php/php5.6-fpm.sock<br>
> env.URL_PATH /status<br>
> env.CACHE_TIME 1


## munin plugin
<code>sudo apt install -y libfcgi0ldbl</code> <br>
<code>cd /usr/share/munin/plugins</code> <br>
<code>wget https://raw.githubusercontent.com/czkanec/munin-php_fpm/master/php-fpm_</code> <br>
<code>chmod +x php-fpm_</code> <br>
<code>munin-node-configure --shell</code>



### get php status page over socket
<code>sudo -u www-data bash -c "export SCRIPT_NAME=/status; export SCRIPT_FILENAME=/status; export QUERY_STRING=full; export REQUEST_METHOD=GET; cgi-fcgi -bind -connect /var/run/php/php5.6-fpm.sock"</code>
