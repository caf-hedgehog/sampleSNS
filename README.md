laravelのデフォルトindex.phpにlocalhostでアクセスできなくて死んでます。
解決策ご存じの方は教えてください。
ちなみにnginxを使用していて、default.confで怒られています。("/var/www/laravel/public/index.php" is not found)
おそらく初期ページの指定が間違っているのではと思ってます。

===default.conf===

server {
  listen 80;
    index  index.php;
    root /var/www/laravel/public;

  location / {
    root /var/www/laravel/public;
    index  index.php;
    }

  location ~ \.php$ {

    try_files $uri =404;
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass app:9000;
    fastcgi_index index.php;
    include fastcgi_params;
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      fastcgi_param PATH_INFO $fastcgi_path_info;
  }
 }
