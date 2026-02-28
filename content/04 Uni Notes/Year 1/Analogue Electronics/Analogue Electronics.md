```dataview
table regexreplace(file.folder, ".*/", "") as "Folder"
from "04 Uni Notes/Year 1/Analogue Electronics"
where file.name != regexreplace(file.folder, ".*/", "") 
sort regexreplace(file.folder, ".*/", "") asc
```
