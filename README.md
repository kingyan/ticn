安装步骤

添加站点

以宝塔为例，首先创建站点绑定域名并设置 DNS 解析，如 xx.com，随后设置伪静态，以 NGINX 为例。

copy

try_files $uri $uri/ /index.php$is_args$args;

location ~ /\.env {

    deny all;

}

下载源码

使用命令下载源码并安装依赖，在此之前要先安装 PHP7.3+ 和 composer。

copy

cd /www/wwwroot/xx.com

git clone https://github.com/xytoki/TCShare.git

mv TCShare/* ./

rm -rf TCShare

composer config repo.packagist composer https://mirrors.aliyun.com/composer/

composer self-update

composer clear

composer update --lock

修改配置

进入网站目录，创建 .env 文件，填入如下内容保存。

copy

XS_KEY_ct=ctyun

XS_KEY_ct_FD=safebox

XS_KEY_ct_AK=600102343

XS_KEY_ct_SK=93c6a3491a5e1d93af0e44b470798148

XS_APP_1=/

XS_APP_1_KEY=ct

XS_APP_1_NAME="LOGI"

XS_APP_1_THEME=mdui

XS_APP_1_BASE=/

接着，打开 xx.com，点击 Click here to get a token，在新页登录天翼账户并授权，完毕后便安装成功。

创建目录

登录 天翼云盘 APP，在 我的应用 目录创建 safebox，并将要分享的文件放入，再次打开 xx.com 即可看到文件。今后每月你都要访问 xx.com/-renew 登录天翼账户重新授权。

免费部署

如果你没有服务器，可以在腾讯云 SCF 上安装，一个人用每月应该不会超过 1 元。前面的步骤都一样，安装 PHP 和 composer，随后执行命令 安装依赖 ，再 添加配置文件 ，最后 上传腾讯云 SCF，如果你不会安装 PHP，加文末 QQ 群获取源码直接上传。

自动签到

最后，手动签到平均每天可得 80M+ 空间，一年就是 28G+，文末群组含自动签到方法，感兴趣可加。
