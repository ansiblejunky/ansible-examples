# Test #1 using Ansible 2.6
```yaml
PLAY [test playbook] ****************************************************************************************************************

TASK [role1 : Set variable] *********************************************************************************************************
ok: [localhost]

TASK [role1 : Register variable] ****************************************************************************************************
ok: [localhost] => {
    "msg": "test"
}

TASK [show role1 variables] *********************************************************************************************************
ok: [localhost] => (item=role1_main_setfact_var) => {
    "item": "role1_main_setfact_var",
    "role1_main_setfact_var": "1"
}
ok: [localhost] => (item=role1_main_register_var) => {
    "item": "role1_main_register_var",
    "role1_main_register_var": {
        "changed": false,
        "failed": false,
        "msg": "test"
    }
}
ok: [localhost] => (item=role1_defaults_var) => {
    "item": "role1_defaults_var",
    "role1_defaults_var": 1
}
ok: [localhost] => (item=role1_vars_var) => {
    "item": "role1_vars_var",
    "role1_vars_var": 1
}

TASK [workaround to expose the defaults in role2] ***********************************************************************************
ok: [localhost]

TASK [role2 : Set variable] *********************************************************************************************************
ok: [localhost]

TASK [role2 : Register variable] ****************************************************************************************************
ok: [localhost] => {
    "msg": "test"
}

TASK [show role2 variables] *********************************************************************************************************
ok: [localhost] => (item=role2_main_setfact_var) => {
    "item": "role2_main_setfact_var",
    "role2_main_setfact_var": "2"
}
ok: [localhost] => (item=role2_main_register_var) => {
    "item": "role2_main_register_var",
    "role2_main_register_var": {
        "changed": false,
        "failed": false,
        "msg": "test"
    }
}
ok: [localhost] => (item=role2_defaults_var) => {
    "item": "role2_defaults_var",
    "role2_defaults_var": 2
}
ok: [localhost] => (item=role2_vars_var) => {
    "item": "role2_vars_var",
    "role2_vars_var": "VARIABLE IS NOT DEFINED!"
}

TASK [include_role : role3] *********************************************************************************************************

TASK [role3 : Set variable] *********************************************************************************************************
ok: [localhost]

TASK [role3 : Register variable] ****************************************************************************************************
ok: [localhost] => {
    "msg": "test"
}

TASK [show role3 variables] *********************************************************************************************************
ok: [localhost] => (item=role3_main_setfact_var) => {
    "item": "role3_main_setfact_var",
    "role3_main_setfact_var": "3"
}
ok: [localhost] => (item=role3_main_register_var) => {
    "item": "role3_main_register_var",
    "role3_main_register_var": {
        "changed": false,
        "failed": false,
        "msg": "test"
    }
}
ok: [localhost] => (item=role3_defaults_var) => {
    "item": "role3_defaults_var",
    "role3_defaults_var": "VARIABLE IS NOT DEFINED!"
}
ok: [localhost] => (item=role3_vars_var) => {
    "item": "role3_vars_var",
    "role3_vars_var": "VARIABLE IS NOT DEFINED!"
}

PLAY RECAP **************************************************************************************************************************
localhost                  : ok=10   changed=0    unreachable=0    failed=0

```
