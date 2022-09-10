---
title: "Ingest Pipeline"
date: 2022-09-09T15:02:44-05:00
draft: false
weight: 210
menu:
  notes:
    name: Ingest Pipeline
    identifier: notes-elasticsearch-ingestpipelines
    parent: notes-elasticsearch
    weight: 10
---




{{< note title="Script Processor: Painless Lowercase ArrayList of Maphashes" >}}

```java
if(ctx.field_name !=l null){
  ArrayList lower_array = new ArrayList();
  for (item in ctx.field_name){
    ArrayList temp = new ArrayList();
    for(map_entry in item.entrySet()){
      temp.add([map_entry.getKey().toLowerCase():map_entry.getValue()])
    }
    lower_array.add(temp);
  }
  ctx.field_name = lower_array;
}
```

{{< /note >}}
