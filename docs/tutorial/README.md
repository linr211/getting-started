# ENI Back-end Localization

The back-end Localization includes RB(ERB) files and JSON files localization.

### RB(ERB) Files' Localization

The RB(ERB) files' localization use the way of integrating with Singleton Ruby client(gem 'singleton-client') which provides Localization support, the integration codes are defined in [loupestash/ui/lib/g11n/g11n.rb](../ui/lib/g11n/g11n.rb)

#### Singleton Ruby Client's Configuration File

[loupestash/ui/config/sgtnclient.yml](../ui/config/sgtnclient.yml)

#### Resource Files

Please refer the 'resource' part in file [loupestash/ui/config/vip_scanner.json](../ui/config/vip_scanner.json) about the resource files' path and component definition. All resource files defined here will be collected by vip_scanner to Singleton service as the sources.

#### Source Collection

Refer the [loupestash/tools/vip-scanner/README.md](../tools/vip-scanner/README.md).

### JSON Files' Localization

Refer the [JSON Globalization Design](https://confluence.eng.vmware.com/display/GQ/2.2+DB%28JSON%29+Gobalization+Design).

#### String Externalization

Refer [loupestash/tools/i18n/README.md](../tools/i18n/README.md) about how to run scripts to extract the sources.

By default, just run 'generate-i18n' task defined in the [makefile file](../ui/Makefile), after running please submit the latest generated properties under 'loupestash/resources/i18n/UI' to ENI code repo.

Note: the task 'generate-i18n' will be also executed by run 'make-bootstrap' in the building process.

#### Source Collection

Refer [loupestash/tools/vip-scanner/README.md](../tools/i18n/README.md) about how to run scripts to do source collection.

## Troubleshooting

Check the log file generated in the root path(e.g. /loupestash/ui/sgtnclient_d.log), the logs are produced by Singleton ruby client in every client's API call.

## local Testing

You need to manually prepare the bundle file and put it to 'loupestash/ui/config/translations/ENI/1.0.0', e.g. If you want to test localized strings in RB files, you need to define the bundle file with name 'messages_zh-Hans.json' and put it under './loupestash/ui/config/translations/ENI/1.0.0/rb/', the file's content will be loaded to Simplified Chinese UI as for your local testing.


## Remote Testing

Change the parameter 'vip_server' and 'bundle_mode' on the configuration file to connect remote Singleton instance for translation, e.g.

```  

  # Singleton server
  vip_server: http://g11n-vip-dev-1.eng.vmware.com:8090

  # mode: online/offline
  bundle_mode: online

```  
With this change, the localized content will be loaded from g11n-vip-dev-1.eng.vmware.com instance by the ruby client for your testing, your local translations under '/loupestash/ui/config/translations/ENI/1.0.0' won't be used.