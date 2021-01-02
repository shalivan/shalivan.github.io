#### Attribute VOP, 
>Use it if you are picking up attributes from the other inputs or  if the name of the attribute you are fetching is dynamic, the Import Attribute VOP or Get Attribute VOPIt allows you to specify a string parameter as the name of the attribute along with the input.
Import Attribute VOP is only available in the SOP context (VOP SOP) and not any other contexts including the Volume VOP SOP.
Import Attribute VOPs need to account for all four inputs and from what I understand this is where the slight overhead may come from.
Parameter VOP 
 
####  Bind VOP
>NEW Bind VOPs support the pre-compliation of VOP HDA's, but are intended to pick up the first input attribute data only. USE BECAUSE:  
will hardocde the name of the attribute in to the compiled vex code.



#### Parameter (żółty)

