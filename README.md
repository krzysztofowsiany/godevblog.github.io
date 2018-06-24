## Branch names

### Release
    * when don't have a task:
        r[year-month-day]
        example: r18-06-25
    * have a task
        task_id
        example: task_123

### Hot fix
    * when don't have a task:
        h[day-hour-minute]
        example: h23-18-32 
    * have a task
        task_id
        example: task_333

### Fixture
    * when don't have a task
        f[year-month-day-name]
        example: f18-06-25-name_of_fixture
    * have a task
        task_id
        example: task_123234

## Finish branch
### Feature
    * with task
    Finish feature: task_id
    Message for commit
    
    * without task
    Finish feature
    Message for commit

### Hotfix
    * with task
    Finish hotfix: task_id
    Message for commit

    * without task
    Finish hotfix.
    Message for commit

### Release
    * with task
    Finish release: task_id
    Commit message

    * without task
    Finish release.
    Commit message