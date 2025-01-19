# SchduledTasks

``` bat
    #タスクの作成
    schtasks /create /tn <task_name> /tr <execution_file_path> /sc onlogon /rl highest
    #タスクの実行
    schtasks /run /tn <task_name>
```
