<p align="center">
  <img src="https://cdn.mangose.app/assets/mangose.png" width="200" alt="Mangose Logo" />
</p>

# Mangose Factory Tutorial

## Example factory diagram

<img src="https://github.com/Mangose/mangose-factory/blob/d33bfa81881d7e57f7e1dd3dcea1db4b618dca7a/assets/factory-diagram-example.png"/>


## Example factory code
```json
{
  "factories": [
    {
      "name": "Test name",
      "event": "task",
      "steps": [
        {
          "action": "if",
          "where": "task.name",
          "is": "<task.name>",
          "ok": [
            {
              "action": "set",
              "name": "wired_task_name",
              "value": "<task.name>"
            },
            {
              "action": "log",
              "message": "Hello <wired_task_name>"
            }
          ],
          "fallback": [
            {
              "action": "log",
              "message": "Bye <task.name>"
            }
          ]
        },
        {
          "action": "request",
          "type": "get",
          "url": "http://example.com/<wired_task_name>"
        },
        {
          "action": "set",
          "name": "var_name",
          "value": "<request>"
        },
        {
          "action": "update",
          "element": "task",
          "id": "<task.id>",
          "property": "name",
          "value": "<var_name>"
        },
        {
          "action": "log",
          "message": "Workspace <workspace.name>"
        }
      ]
    }
  ]
  
}
```

## Events types
```js
task // create and update task
reminder // at remind notification
duedate // at deadline
```

## Conditions
```json
{
  "action": "if",
  "where": "task.name",
  "is": "<task.name>",
  "ok": [
    {
      "action": "log",
      "message": "If true"
    }
  ],
  "fallback": [
    {
      "action": "log",
      "message": "If false"
    }
  ]
}
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

### Requesat url and save response to <request>
```
{
  "action": "request",
  "type": "get",
  "url": "url"
},
```
### Set varable
```
{
  "action": "set",
  "name": "var_name",
  "value": "<request>"
},
```
### Update task
```
{
  "action": "update",
  "element": "task",
  "id": "<task.id>",
  "property": "name",
  "value": "<var_name>"
}
```
