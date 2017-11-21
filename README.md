# TA-cyberchef

CyberChef is known as "The Cyber Swiss Army Knife - a web app for encryption, encoding, compression and data analysis" 
and is available at [gchq/CyberChef](https://gchq.github.io/CyberChef). CyberChef is released under the Apache 2.0 Licence and is covered 
by Crown Copyright.

This Splunk technology add-on demostrates how to pivot out of Splunk and into CyberChef for additional analysis.

## Pre-requisites:

- Install Splunk Enterprise. This TA has been tested with version 7.x.
- Install [base64 custom search command written by Cedric Le Roux](https://splunkbase.splunk.com/app/1922/). This TA has been tested with version 1.1 of the base64 command.
- Install CyberChef, or decide to use the CyberChef demo system.


## Installation:

- Install this TA under `$SPLUNK_HOME/etc/apps`
- Restart Splunk


## Test:

Load this Splunk search:

```
 earliest=0 index=* 
 | head 1 
 | eval cchef="abcd1234" 
 | eval cchef_b64=cchef 
 | base64 field=cchef_b64 action=encode
```

In the result set, locate the field named cchef and observe the associated workflow actions.

Substitute these values for the cchef field in the search above to test different CyberChef recipes:

- CyberChef-From_Base64 -> "SGV5IHRoZXJlLCBTcGx1bmsgdXNlciE="
- CyberChef-From_Charcode -> "42 65 63 61 73 75 65 20 6e 69 6e 6a 61 73 20 61 72 65 20 74 6f 6f 20 62 75 73 79 2e 2e 2e"
- CyberChef-From_Hex -> "54 61 6b 65 20 74 68 65 20 53 48 20 6f 75 74 20 6f 66 20 49 54"
- CyberChef-From_Hexdump -> "43 6f 6f 6c 20 73 74 6f 72 79 2c 20 62 72 6f"
 
 
## Use more/different CyberChef Recipes:

The provided workflow actions only represent a few of the many CyberChef Recipes. To create a workflow action to a new/different recipe, update the URL in the workflow action definition. Use CyberChef itself to to determine the changes. For example, the CyberChef recipe to convert to binary is "To_Binary('Space')" which can be observed easily in the CyberChef URL.  


## Apply Workflow Actions to Different Fields:

To apply these workflow actions to a different field, do the following:

In this example we will apply CyberChef worklfow actions to a field called content_body.
- Create a base64 version of the field: `base64 field=content_body_b64 action=encode`
- Modify the workflow action definition to apply to content_body
- Modify the workflow action defineiton to pass $content_body_b54$ to Cyberchef


## To Use Your Own CyberChef Instance:

These workflow actions use the demo CyberChef instance provided by the creators of CyberChef. To use your own instance, simply set up an instance according the CyberChef instrsuctions then modify the URL in the workflow definition(s)
