> [!uninotes] Year 2 Modules
> ```dataview
list 
from "04 Uni Notes/Year 3"
where file.name = regexreplace(file.folder, ".*/", "") AND file.name != "Year 3"
sort file.folder asc
> ```
