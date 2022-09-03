# ENI Back-end Localization Solution

The back-end Localization  solution includes RB(ERB) files and JSON files.

### RB(ERB) Files' Localization

The RB(ERB) files' localization integrates with Singleton Ruby client(gem 'singleton-client') to provide globalization support, the integration codes are defined in [../ui/lib/g11n/g11n.rb]

#### Singleton Ruby Client's Configuration File

./loupestash/ui/config/sgtnclient.yml

#### Resource Files

Please refer the 'resource' part in file ./loupestash/ui/config/vip_scanner.json about the resource files' path and component definition. All resource files defined here will be collected by vip_scanner to Singleton service as the English sources.

#### Source Collection

Refer the doc './loupestash/tools/vip-scanner/README.md'.

### JSON Files' Localization

Refer https://confluence.eng.vmware.com/display/GQ/2.2+DB%28JSON%29+Gobalization+Design about the solution and design.

#### String Externalization

Refer /loupestash/tools/i18n/README.md about how to run scripts to extract the sources.

By default, just run 'generate-i18n' task defined in file ./loupestash/ui/Makefile, after running please submit the latest generated sources to code repo; the task 'generate-i18n' will be also executed by run 'make-bootstrap' in building process.

#### Source Collection

Refer ./loupestash/tools/vip-scanner/README.md

## Troubleshooting

Check the log file generated in the root path, e.g. /loupestash/ui/sgtnclient_d.log, the logs are produced by Singleton ruby client in every client's API call.

## local Testing

You need to manually prepared the bundle file and put it to './loupestash/ui/config/translations/ENI/1.0.0', e.g. If you want to test something in RB files, you need to define the bundle file with name 'messages_zh-Hans.json'( as example) and put it under './loupestash/ui/config/translations/ENI/1.0.0/rb/', the content will be loaded to Simplified Chinese UI for your local testing.


## Remote Testing

Change the  parameter 'vip_server' and 'bundle_mode' on the configuration file to connect remote Singleton instance for translation, e.g.

```  

  # Singleton server
  vip_server: http://g11n-vip-dev-1.eng.vmware.com:8090

  # mode: online/offline
  bundle_mode: online

```  
With this change, the localized content will be loaded from g11n-vip-dev-1.eng.vmware.com instance by the ruby client for your testing, your local translations under './loupestash/ui/config/translations/ENI/1.0.0' won't be used.