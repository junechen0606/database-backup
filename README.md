# laravel-permissions

#### 介绍
Back up the database data to a file
    
#### 使用说明

##### Mysql
备份数据

    ```
    // 创建备份文件
    $Database = new MysqlBackupOrRestore();
    if (false !== $Database->create()) {
        // 备份指定表
        foreach ($tables as $table) {
            $start = $Database->backup($table);
            while (0 !== $start) {
                if (false === $start) { // 出错
                    //备份出错！
                    return ;
                }
                $start = $Database->backup($table, $start[0]);
            }
        }
    } else {
        // 初始化失败，备份文件创建失败！
    }
    ```

恢复数据

    ```
    $item = [
        "name" => 'Backup.gz'
    ];
    $Database = new MysqlBackupOrRestore($item);
    $start = $Database->restore(0);

    // 循环导入数据
    while (0 !== $start) {
        if (false === $start) { // 出错
            //还原数据出错！
            return ;
        }
        $start = $Database->restore($start[0]);
    }
    ```