---
title: "Powershell"
date: 2022-05-17T15:02:44-05:00
draft: true
weight: 210
menu:
  notes:
    name: General
    identifier: notes-powershell-general
    parent: notes-powershell
    weight: 10
---

<!-- Variable -->
{{< note title="Variable" >}}

```bash
New-Object System.Math
```

{{< /note >}}

<!-- Condition -->
{{< note title="Condition" >}}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

{{< /note >}}
