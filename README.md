# Keycloak

version: `24.0.2`

See: https://www.keycloak.org/documentation

## Authorization Architecture

See: https://www.keycloak.org/docs/latest/authorization_services/index.html

![image](https://github.com/pydemia/keycloak/assets/18019100/972775e0-ff0f-4088-b2bb-d4a611a671c4)


* Resource Servers
Resource servers are managed using the Keycloak Administration Console.
There you can enable any registered client application as a resource server and start managing the resources and scopes you want to protect.
A resource can be a web page, a RESTFul resource, a file in your file system, an EJB, and so on. They can represent a group of resources (just like a Class in Java) or they can represent a single and specific resource.
For instance, you might have a Bank Account resource that represents all banking accounts and use it to define the authorization policies that are common to all banking accounts. However, you might want to define specific policies for Alice Account (a resource instance that belongs to a customer), where only the owner is allowed to access some information or perform an operation.
Resources can be managed using the Keycloak Administration Console or the Protection API. In the latter case, resource servers are able to manage their resources remotely.

![image](https://github.com/pydemia/keycloak/assets/18019100/0d294f38-6daf-4d11-849c-e2f56ba4aa72)

* Policies

![image](https://github.com/pydemia/keycloak/assets/18019100/06b1de1b-252d-4926-bcdb-497e4c3f6dcd)



* Permission

A permission associates the object being protected with the policies that must be evaluated to determine whether access is granted.

X CAN DO Y ON RESOURCE Z

where …​

X represents one or more users, roles, or groups, or a combination of them. You can also use claims and context here.

Y represents an action to be performed, for example, write, view, and so on.

Z represents a protected resource, for example, "/accounts".

---

## Create an Authorization Service

### Managing Resource Servers

1. Create a realm

2. Create a client app

* enable `Client Authentication`

3. Enable Authorization services

* enable `Authorization`
* enable some Authentication flow:
  - `Standard flow`
  - `Direct access grants`
  - `Service accounts roles`

* Show Sub-tabs in `Authorization`
  - Settings
    - Policy Enforcement Mode
      - Enforcing
      - Permissive
      - Disables
    - Dicision strategy
      - Unanimous: Negative if permissions are in conflict(one is P, another is N).
      - Affirmaative: Positive if permissions are in conflict(one is P, another is N).
    - Remote resource management: if False, resources can be managed only from the admin console.
  - Resource: An object being protected. An asset of an app and org.
  - Scope: A bounded extent of access that is possible to perform on a resource, like verbs. (ex. `view, edit, delete, or cost, etc.`)
  - Policy
  - Permission
    - __X__ CAN DO __Y__ ON RESOURCE __Z__
      - __X__: Users, roles, Groups, etc.
      - __Y__: An action. ex. write, view, ...
      - __Z__: 
  - Evaluate
  - Export

4. Configure it

* Resources
  - `Default Resource`: all resources(`/*`)
  - Type(`urn:<realm>:resources:default`): It can be used to group resources together
* Policies(referred to as the only from realm policy)
  - `Default Policy`: Javascript-based policy (`$evaluation.grant();`)
* Permission
  - `Default Permission`: Resource-based

5. Export and import the configuration

### Manage Resources and Scopes



### Manage Policies

### Manage Permissions

### Test the policies

