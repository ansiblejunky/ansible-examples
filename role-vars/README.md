# Ansible Role Variables
Run the example playbooks to understand how variables are exposed from within a role. Depending on how you bring the Role into the Play, variables are exposed differently.

## Test #1
Let us first look at an example Playbook that loads a role in various ways.
```
ansible-playbook test1.yml
```
[Test 1 Output Using Ansible 2.6](./test1_2.6_output.md)  
[Test 1 Output Using Ansible 2.7](./test1_2.7_output.md)

Before Ansible 2.7, you will notice the following behavior:
- Using `roles:` section in a Play results in the `defaults` and `vars` within the Role becoming **public**
- Using `import_role` module in a Play results in the `defaults` and `vars` within the Role remaining **private**
- Using `include_role` module in a Play results in the `defaults` and `vars` within the Role remaining **private**

As of Ansible 2.7, you will notice the following behavior:
- Using `roles:` section in a Play results in the `defaults` and `vars` within the Role becoming **public**
- Using `import_role` module in a Play results in the `defaults` and `vars` within the Role remaining **public**
- Using `include_role` module in a Play results in the `defaults` and `vars` within the Role remaining **private**

## Test #2
Now let us take it a bit further and test what happens when a Playbook first imports a role (`import_role`) and then this role performs an `include_role` task.  
```
ansible-playbook test2.yml
```
[Test 2 Output Using Ansible 2.6](./test2_2.6_output.md)  
[Test 2 Output Using Ansible 2.7](./test2_2.7_output.md)


Before Ansible 2.7, both the `import_role` and `include_role` result in the `defaults` and `vars` within the Role remaining **private**. You will notice the variables are **not** accessible from the Playbook level.

As of Ansible 2.7, the `import_role` results in the variables defined within `role_import_me/defaults` and `role_import_me/vars` folders to be public. This is expected. However, notice that the `role_include_me/defaults` and `role_include_me/vars` from the included role are now also **public**. This might be contrary to what you would assume.

So we ask the question, should the included role's `defaults` and `vars` be made private or public? The assumption here is: since we started with `import_role`, everything deeper than that will be made public.

## Force Public on Included Roles
In Ansible 2.7 a new module argument named `public` was added to the `include_role` module that dictates whether or not the role’s `defaults` and `vars` will be exposed outside of the role, allowing those variables to be used by later tasks. This value defaults to `public: False`, matching current behavior.

`import_role` does not support the `public` argument because it unconditionally exposes the role’s `defaults` and `vars` to the rest of the playbook. This functinality brings `import_role` into closer alignment with roles listed within the `roles:` header in a play.

There is an important difference between `include_role` (dynamic) and `import_role` (static).  Specifically regarding the way that role's variables are exposed. 

- `import_role` is a pre-processor, and the `defaults` and `vars` are evaluated at playbook parsing, making the variables available to tasks and roles listed at any point in the play
- `include_role` is a conditional task, and the `defaults` and `vars` are evaluated at execution time, making the variables available to tasks and roles listed after the `include_role` task

## Default Private Role Variables
Additionally, you should look at the following [configuration setting](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-private-role-vars) to make role variables inaccessible from other roles. This was introduced as a way to reset role variables to default values if a role is used more than once in a playbook.
