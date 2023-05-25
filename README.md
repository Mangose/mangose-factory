<p align="center">
  <img src="https://cdn.mangose.app/assets/mangose.png" width="200" alt="Mangose Logo" />
</p>

# Mangose Factory Tutorial

## Example factory code
```yaml
event_task:
  steps:
    - action: if
      where: task.name
      is: <task.name>
      ok:
        - action: set
          name: wired_task_name
          value: <task.name>
        - action: log
          message: 'Hello <wired_task_name>'
      fallback:
        - action: log
          message: 'Bye <task.name>'
    - action: request
      type: get
      url: 'http://example.com/<wired_task_name>'
    - action: set
      name: var_name
      value: <request>
    - action: update
      element: task
      id: <task.id>
      property: 'name'
      value: '<var_name>'
    - action: log
      message: 'Workspace <workspace.name>'
```

## Events types
```js
task // create and update task
reminder // at remind notification
duedate // at deadline
```

## Conditions
```yaml
- action: if
  where: task.name
  is: <task.name> #is - condition type (more below), <task.name> varable
  ok:
    - action: log
      message: 'If true'
  fallback:
    - action: log
      message: 'If false'
```


## Condition types
```js
is
qt
lt
qte
lte
not
contain
not-contain
```

## More actions
```yaml

# requesat url and save response to <request>
- action: request
  type: get
  url: 'url'
  
# set varable
- action: set
  name: var_name
  value: <request>

# update task
- action: update
  element: task #for now only task
  id: <task.id> # only taks in active space
  property: 'name' # name, done, archived
  value: '<var_name>' # new value 
```
