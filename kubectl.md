kubectl api-resources
 - lists all resouces
 - useful if you forget a resource name, API version, KIND, and etc.. 


 kubectl explain pods
 - provides more information regarding that resource
 - similar to man command in linux
 - lists the fields that belong to that resource

 kubectl explain pods.field
 - lists the fields within pods.field section.

 kubectl explain pods --recursive
 - lists all fields the way you should put them in a yaml file.

 


