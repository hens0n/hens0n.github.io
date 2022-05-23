---
title: "Sharepoint"
date: 2022-05-17T15:03:53-05:00
draft: true
weight: 210
menu:
  notes:
    name: SharePoint
    identifier: notes-powershell-sharepoint
    parent: notes-powershell
    weight: 10
---



<!-- Variable -->
{{< note title="Get List Items" >}}

```bash
function Get-ListItems{
  param(
      [srtring]$sharepointSite,
      [srtring]$listTitle,
      [srtring]$selectedFields
    )
  $itemArry =@()
  $pageSize = 5000
  $pageId = 0
  $header = @{'Accept' = 'application/json; odata=verbose'}

  if ($selectedFields.Length -gt 0){
    $selectStatement = "&`$SELECT=$($selectedFields)"
  }

  while ($pageId){
    $uri = "$($sharepointSite)/_api/Web/Lists/GetByTitle('$($listTitle)')/Items?`$skiptoken=Paged=True%26p_ID=$($pageId)&`$top=$($pageSize)$($selectStatement)"

    #Get list Get-ListItems
    $response = Invoke-RestMethod -Method Get -Uri $uri -Headers $header -UseDefaultCredentials:$true
    $data = $response.ToString().Replace("""ID""","_ID") | ConvertFrom-Json

    if($data.d.results.Count -gt 0){
      #Add to the Array
      $itemsArray += $data.d.results
      #Get last id in the results set for next starting sharepointSite
      $pageId = $data.d.results[-1].id
    }
    else{
      $pageId =-1
    }
  }
  return $itemArry

}
```

{{< /note >}}