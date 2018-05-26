## 说明
 
    Swagger使API开发调试设计变得轻而易举，为开发人员，架构师和产品所有者提供易于使用的工具。

* 安装swagger-php
```
[mason @ projct]$ composer require zircote/swagger-php -vvv
    Reading ./composer.json
    Loading config file /Users/mason/.composer/config.json
    Loading config file /Users/mason/.composer/auth.json
    Loading config file ./composer.json
    Checked CA file /private/etc/ssl/cert.pem: valid
    ...中间省略10W行...
    > post-update-cmd: php artisan clear-compiled
    Executing command (CWD): php artisan clear-compiled
    > post-update-cmd: php artisan optimize
    Executing command (CWD): php artisan optimize
    Generating optimized class loader

```
* 配置文档总纲
```
<?php
/**
 * 文档说明（可以在项目下弄一个空文件）
 *
 * @SWG\Swagger(
 *   schemes={"http"},
 *   @SWG\Info(
 *     version="1.0",
 *     title="XX-API文档",
 *   ),
 * )
 */
```
* 编写文档实例
```
<?php

class RegisterMobileController extends Controller
{

    /**
     *  用户注册API
     *
     * @SWG\Get(path="/1.0/user/register/mobile",
     *   tags={"用户模块"},
     *   summary="用户注册",
     *   description="新用户注册",
     *   operationId="RegisterMobile",
     *   @SWG\Parameter(
     *     in="query",
     *     name="username",
     *     type="string",
     *     description="用户名",
     *     required=true,
     *   ),
     *   @SWG\Parameter(
     *     in="query",
     *     name="password",
     *     type="string",
     *     description="密码",
     *     required=true,
     *   ),
     *   @SWG\Response(response="default", description="操作成功")
     * )
     */
    public function run()
    {
        return ['data'=>'succ'];        
    }


```
* 生成文档
```
[mason @ projct]$ vendor/bin/swagger app/controllers/ -o public/

    Swagger-PHP 2.0.13
    ------------------
    [INFO] Required @SWG\Info() not found
    
        get /2.0/user/accessdev/list
        get /1.0/user/register/mobile
    -----------------------
    2 operations documented
    -----------------------
    Written to /Users/mason/project/php_project/public/swagger.json

```
* 配置swagger-ui
```
<script>
       window.onload = function () {
           const ui = SwaggerUIBundle({
               url: "http://www.xxx-xxx.com/swagger.json",//你的swagger.json路径
               dom_id: '#swagger-ui',
               deepLinking: true,
               //validatorUrl: null, //去掉右下角的错误
               //filter: '',//显示搜索TAG
               presets: [
                   SwaggerUIBundle.presets.apis,
                   SwaggerUIStandalonePreset
               ],
               plugins: [
                   SwaggerUIBundle.plugins.DownloadUrl
               ],
               layout: "StandaloneLayout"
           })
           window.ui = ui
   
       }
</script>

```
引：https://github.com/zircote/swagger-php/tree/master/Examples