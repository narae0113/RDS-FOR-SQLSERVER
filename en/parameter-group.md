## Database > RDS for MS-SQL > Parameter Group

## Parameter group

RDS for MS-SQL provides the parameter group feature to apply the settings from the Microsoft SQL Server installed in the DB instance. A parameter group is a set of parameters that sets up the Microsoft SQL Server.
When the RDS for MS-SQL service is enabled, the basic parameter group “default.parameter-group” is provided. The basic parameter group cannot be deleted or changed.
A DB instance can use one parameter group, and the parameter group can be used by multiple DB instances at once.

### Creating or deleting a parameter group

A new parameter group can be created by copying an existing parameter group. The copied parameter group only copies parameters from the original parameter group and does not have any association with it.
The parameter group can be deleted only when no DB instance is using the parameter group; if there is a parameter group that is using it, it cannot be deleted.

## Parameters

Parameters have the following information:

* Name
  * Parameter name.
* Value
  * The value to be applied to the parameter.
* Permitted values
  * A range of values that can be applied to the parameter.
* Modifiable
  * Determines whether parameter can be modified.
* Applied type
  * Either “static” or “dynamic.”
  * If set to “Static,” the DB instance must be restarted to apply changes to the parameter.
  * If set to “Dynamic,” the parameter is applied immediately without DB instance restart.
* Data type
  * The type of the parameter value.

### Parameter variables, formulas, and functions

Certain parameters (e.g. “max server memory (mb)”) are better expressed as formulas that use values associated with the DB instance rather than static values. To support this, predefined variables, formulas, and functions can be used for the “numeric” data type.

* Formulas
  * “()”, “+”, “-”, “*”, “/” can be used. 
  * The result of a formula must always be an integer, and decimal places are discarded.
* Functions
  * `max(a, b, ...)`: returns the largest in the array.
  * `min(a, b, ...)`: returns the smallest in the array.
* Variables
  * “ramSizeByte”: memory size of the current DB instance type (in bytes).
  * “storageSizeByte”: DB instance storage size (in bytes).

The below example is the default value of the “max server memory (mb)” parameter, and shows selecting 3/4 the memory size of the DB instance type:

```
ramSizeByte * 3 / 4 / 1048576
```

### Changing parameters

Only a parameter group created by users can be changed, and new one can be created by copying one from the existing parameter groups.
If parameters inside a parameter group are changed, the changes are applied simultaneously to all DB instances that are using the parameter group. If any of the DB instances using the parameter group is in the middle of processing some other tasks, the parameter won't be changed.
If the applied type of the changed parameter is “Static,” the DB instance will restart.
