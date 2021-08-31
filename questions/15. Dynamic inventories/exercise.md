# 15. Dynamic inventories

Create file in form of a dynamic inventory which meets following requirements:
* Is placed at `/home/automation/plays/scripts/dynamic_inventory`
* Contains definitions of 3 three groups - database, proxy, webservers
* Returns following hosts for `proxy` group
    * managed1.example.com
* Returns following hosts for `webservers` group
    * managed2.example.com
    * managed3.example.com
* Returns following hosts for `database` group
    * managed3.example.com
    * managed4.example.com
* Defines following vars for `database` group
    * `accessibility` with value `private`
* Defines following vars for `proxy` group
    * `accessibility` with value `public`
* Defines following vars for `managed2.example.com` host
    * `accessibility` with value `unknown`
* Returns json to stdout when called 
* Must be parsable by ansible
