---
title: "httpjson"
date: 2023-05-20T15:00:00-00:00
draft: false
weight: 210
menu:
  notes:
    name: httpjson
    identifier: notes-filebeat-httpson
    parent: notes-filebeat
    weight: 10
---




{{< note title="Filebeat httpjson" >}}

Filebeat httpjson example config for Proofpoint Isolation API

```yml
filebeat.inputs:
- type: httpjson
  interval: "1h"
  request.url: https://proofpointisolation.com/api/v2/reporting/useage-data/
  request.method: GET
  request.transforms:
    - set:
        target: url.params.to
        value: '[[formatDate (now)]]'
    - set:
        target: url.params.from
        value: '[[ formatDate (now (parseDuration "-1h")) ]]'
    - set:
        target: url.params.key
        value: 'your_api_key'
    - set:
        target: url.params.pageSize
        value: '100'
  response.split:
    target: body.data
    type: array
    keep_parent: false
  response.pagination:
    - set:
        target: url.value
        value: '[[ .last_response.url.value]]' 
    - set:
        target: url.params.jobId
        value: '[[.last_response.body.jobId]]'
        fail_on_template_error: true
    - set:
        target: url.params.pageToken
        value: '[[.last_response.body.pageToken]]'
        fail_on_template_error: true
  processors:
    - decode_json_fields:
        fields: ["message"]
        target: "json"

output.console:
  pretty: true
```

{{< /note >}}
