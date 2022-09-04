# ENI Backend Localization

The backend Localization includes RB(ERB) files and JSON files localization. The RB(ERB) files leverage Singleton ruby client's API to implement localization; the JSON files's UI contents are not localized on backend directly on run-time, instead, localized on front-end.


## Localization for RB and ERB Files

The RB(ERB) files' localization is implemented by integrating with Singleton Ruby client(gem 'singleton-client') which provides localization support, the current integration codes are defined in [loupestash/ui/lib/g11n/g11n.rb](../ui/lib/g11n/g11n.rb)

### Singleton Ruby Client's Configuration File

The Singleton ruby client's configuration file [loupestash/ui/config/sgtnclient.yml](../ui/config/sgtnclient.yml) is used to define the settings for communicating with Singleton service instance.

### Where to Define Resource Files

Refer the 'resource' part in file [loupestash/ui/config/vip_scanner.json](../ui/config/vip_scanner.json) about the resource files' path and components definition, e.g.

```
"resource": [
        {
            "parser": {
                "escape": "strip,decode_with_continue",
                "type": "properties"
        },
        "components": [
            {
            "component": "UI",
            "path": [
                "resources/i18n/UI/remediations.properties",
                "resources/i18n/UI/analytics.properties",
                "resources/i18n/UI/helps.properties"
                ]
            }
            ]
        },
        {
            "parser": {                                 
                "type": "rubyyml"
        },
        "components": [{
            "component": "erb",
            "path": [
                "ui/config/sources/erb/source.yml"  
                ]},
                {
                    "component": "devise",
                    "path": [
                        "ui/config/locales/devise.en.yml"  
                ]}
            ]
        }]
```

All the resource files defined in vip_scanner.json will can be collected for translation by the vip_scanner.

### How to Do Source Collection

Refer the [loupestash/tools/vip-scanner/README.md](../tools/vip-scanner/README.md) file about how to run the tool to do source collection.


## Localization for JSON Files

Refer the [JSON Globalization Design](https://confluence.eng.vmware.com/display/GQ/2.2+DB%28JSON%29+Gobalization+Design) document about how to implement the JSON files's localization.

### How to Externalize the Source from JSON Files

For new or updated localizable sources added in the json files, please refer [loupestash/tools/i18n/README.md](../tools/i18n/README.md) about how to run the scripts to extract the sources to properties files. By default, you can just run 'generate-i18n' task defined in the [makefile file](../ui/Makefile), e.g.

```
generate-i18n:
	python3 ../tools/i18n/json_prop_gen.py -c ../resources/i18n/UI -s ../resources/remediations/remediations.json -p remediations_res
	python3 ../tools/i18n/json_prop_gen.py -c ../resources/i18n/UI -s ../ui/resources/generated/remediations.json -p remediations_gen
	python3 ../tools/i18n/json_prop_gen.py -c ../resources/i18n/UI -s ../ui/resources/generated/analytics.json -p analytics
	python3 ../tools/i18n/json_prop_gen.py -c ../resources/i18n/UI -s ../resources/helps/helps.json -p helps
	python3 ../tools/i18n/ngx_json_gen.py -s ../resources/i18n/UI/remediations.properties -o ../ui/ng2-app/libs/eni-hybrid/src/lib/l10n/eni-backend.l10n.ts
	python3 ../tools/i18n/ngx_json_gen.py -s ../resources/i18n/UI/analytics.properties -o ../ui/ng2-app/libs/eni-hybrid/src/lib/l10n/eni-backend.l10n.ts
	python3 ../tools/i18n/ngx_json_gen.py -s ../resources/i18n/UI/helps.properties -o ../ui/ng2-app/libs/eni-hybrid/src/lib/l10n/eni-backend.l10n.ts
```

When it's done you could submit the latest generated properties file under 'loupestash/resources/i18n/UI' to ENI code repo so that the updated sources can be collected for translation

Notes: 
a) The task 'generate-i18n' will be also executed by run 'make-bootstrap' in the building process;
b) If there's new JSON file, you need to develop new parser on the existing file 'loupestash/tools/i18n/json_prop_gen.py' to extract the localizable content.

### How to Do Source Collection

Refer [loupestash/tools/vip-scanner/README.md](../tools/i18n/README.md) about how to run the scripts to generate the sources.

The source collection running is same with RB(ERB) files' as mention above, it's just to run the scanner to do it.


## Local I18n Testing

If you want to do local i18n testing to make sure i18n function works well, you can manually prepare the bundle file and put it to 'loupestash/ui/config/translations/ENI/1.0.0', e.g. If you want to test localized strings in RB files, you need to define the bundle file with name 'messages_zh-Hans.json' and put it under './loupestash/ui/config/translations/ENI/1.0.0/rb/', the file's content will be loaded to Simplified Chinese UI as for your local testing.


## Remote I18n Testing

For remote i18n testing, you needs to connect remote Singleton instance by changing the parameter 'vip_server' and 'bundle_mode' on the configuration file to , e.g.

```  

  # Singleton server
  vip_server: http://g11n-vip-dev-1.eng.vmware.com:8090

  # mode: online/offline
  bundle_mode: online

```  
With this change, the localized content will be loaded from g11n-vip-dev-1.eng.vmware.com instance by the Singleton ruby client for your testing, your local translations under '/loupestash/ui/config/translations/ENI/1.0.0' won't be used.



## Troubleshooting

As the backend localization is mainly via Singleton ruby client to get translation, so you could enable the logger's debug mode and check the log file generated in the root path(e.g. /loupestash/ui/sgtnclient_d.log).