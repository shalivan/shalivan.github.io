
### Strings

##### sprintf

`s@name = sprintf("piece_%d", i@class);` - name from class nad string  
`s@name = sprintf("%s %d", "piece", @ptnum); - `
`@newextention = sprintf("_%03d", @ptnum)` - set ptnum as a 3 digits number (001, 002)  


##### itoa
>cast to string (int to string)

`s@name = "piece"+itoa(i@class);` - Name from class attrib. (Connectivity sop)   
`s@name = "packed_prim"+itoa(@primnum);` - Name from packed primitive number   
`s@name = "say_my_name"+itoa(nearpoint(1,@P));` - Closest point to this primitive   

##### -

`s@name = point(1,"name",nearpoint(1,@P));` - Get point attrib from the closest point   
`@i = match("name", s@group);` - check if string match attrib  >> `match(a, b)`  - short:`a ~~= b`    
`if (match("/obj/.../texture_material", s@shop_materialpath)) @group_mygroup = 1;` - if material

###  Strings Operations
`s@[]pathsplith = split(path, "/")` - splits the string in pieces based on the "/"  
`@newpath = join(pathsplit, "_")` - merges the elements of an array with "_"   
`@filename = pop(pathsplit)` - removes the last element from the array and addign to new var  

`@name = string[0:1];` - H
`@name = string[0:1];` - Hello worl



opdigits("oriev548.hip") << return 548...




https://www.sidefx.com/docs/houdini/vex/functions/opdigits.html
