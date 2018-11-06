# Ansible Examples

## Description
Testing variable names using both underscore and dashes. This example emphasizes the importance of using only **underscore** with variable names, role names, etc.  A consistent style is additionally important and brings value.

Programming languages typically prefer using underscore instead of dashes for variable naming. With respect to Ansible it is important to understand the following:
- Python does **not** support using dashes at all
- Jinja templating engine interprets the dash as a subtraction math operation.

For example:
If you attempt to reference a variable that uses a dash in the name, such as `{{ one-two }}`. It will be interpreted as `{{ one - two }}`, which means `one` minus `two`. This will typically generate an error because the variables `one` and `two` are not defined. However in the case the variables are defined, then it will attempt the subraction operation.

## Usage
```
ansible-playbook test.yml
```