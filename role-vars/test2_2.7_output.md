# Test #2 Output using Ansible 2.7

```yaml
PLAY [test playbook] ****************************************************************************************************************

TASK [role_import_me : Set variable] ************************************************************************************************
ok: [localhost]

TASK [role_import_me : Register variable] *******************************************************************************************
ok: [localhost] => {
    "msg": "test"
}

TASK [role_include_me : Set variable] ***********************************************************************************************
ok: [localhost]

TASK [role_include_me : Register variable] ******************************************************************************************
ok: [localhost] => {
    "msg": "test"
}

TASK [show role_import_me variables] ************************************************************************************************
ok: [localhost] => (item=role_import_me_main_setfact_var) => {
    "item": "role_import_me_main_setfact_var",
    "role_import_me_main_setfact_var": "1"
}
ok: [localhost] => (item=role_import_me_main_register_var) => {
    "item": "role_import_me_main_register_var",
    "role_import_me_main_register_var": {
        "changed": false,
        "failed": false,
        "msg": "test"
    }
}
ok: [localhost] => (item=role_import_me_defaults_var) => {
    "item": "role_import_me_defaults_var",
    "role_import_me_defaults_var": 1
}
ok: [localhost] => (item=role_import_me_vars_var) => {
    "item": "role_import_me_vars_var",
    "role_import_me_vars_var": 1
}

TASK [show role_include_me variables] ***********************************************************************************************
ok: [localhost] => (item=role_include_me_main_setfact_var) => {
    "item": "role_include_me_main_setfact_var",
    "role_include_me_main_setfact_var": "1"
}
ok: [localhost] => (item=role_include_me_main_register_var) => {
    "item": "role_include_me_main_register_var",
    "role_include_me_main_register_var": {
        "changed": false,
        "failed": false,
        "msg": "test"
    }
}
ok: [localhost] => (item=role_include_me_defaults_var) => {
    "item": "role_include_me_defaults_var",
    "role_include_me_defaults_var": 1
}
ok: [localhost] => (item=role_include_me_vars_var) => {
    "item": "role_include_me_vars_var",
    "role_include_me_vars_var": 1
}

PLAY RECAP **************************************************************************************************************************
localhost                  : ok=6    changed=0    unreachable=0    failed=0
```