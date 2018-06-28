---
layout: post
title:  "Google Drive APIs"
date:   2018-06-28 11:00:00 +0700
categories: api google drive
---

### Download Files
ref [guides](https://developers.google.com/drive/api/v3/manage-downloads)

```clj
; return byte-array in :body
(http/get (str "https://www.googleapis.com/drive/v3/files/" file-id)
          {:headers      {"Authorization" (str "Bearer " access-token)}
           :query-params {"alt" "media"}})
```

### Search for Files in Folder
ref [guides](https://developers.google.com/drive/api/v3/search-parameters)

```clj
(http/get "https://www.googleapis.com/drive/v3/files"
          {:headers      {"Authorization" (str "Bearer " access-token)}
           :query-params {"pageSize"  1000
                          "pageToken" nextPageToken ; init with ""
                          "q"         (format "'%s' in parents and trashed = false" folder-id)}
           :as           :json})
```

### File view
`https://drive.google.com/file/d/<file-id>/view`

### Image thumbnail
`https://drive.google.com/thumbnail?id=<file-id>&sz=w800-h800`
