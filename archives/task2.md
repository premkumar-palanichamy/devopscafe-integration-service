**Task 2 :** 

How do you manage security credentials in a CI/CD environment, such that only the relevant people who need access to the credentials will be able to access it? For Example, you could take Jenkins as an example environment (or other environments based on your experience).

Provide the approach you will take.

I will use Jenkins plugin "Matrix Authorization Strategy" and configure permissions. Matrix Authorization allows configuring the lowest level permissions, such as starting new builds, configuring items, or deleting them, individually.

***Project-based configuration***

`Project-based matrix authorization allows configuring permissions for each item or agent independently.

Permission applying to such items or agents that are granted in the global configuration apply to all of them, unless they don't inherit global permissions (see below).`

***Permission inheritance***

`With project-based matrix authorization, permissions are by inherited from the global configuration and any parent entities (e.g. the folder a job is in) by default.

This can be changed. Depending on the entity being configured, all or a subset of the following inheritance strategies are available:

- Inherit permissions: This is the default behavior. Permissions explicitly granted on individual items or agents will only add to permissions defined globally or in any parent items.

- Inherit global configuration only: This will only inherit permissions granted globally, but not those granted on parent folders. This way, jobs in folders can control access independently from their parent folder.

- Do not inherit permissions: The most restrictive inheritance configuration. Only permissions defined explicitly on this agent or item will be granted.

- The only exception is Overall/Administer: It is not possible to remove access to an agent or item from Jenkins administrators.

Further, we can store jenkins users credentials in a secret manager tool like Keypass, AWS Secret Manager or Hashicorp vault and rotate the keys in intervals.`
