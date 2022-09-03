# ENI Back-end Globalization Solution

The back-end globalization  solution includes RB(ERB) files and JSON files.

### RB(ERB)

The RB(ERB) files' localization integrates with Singleton Ruby client(gem 'singleton-client') to provide support, the integration codes are defined in ./loupestash/ui/lib/g11n/g11n.rb

#### Configuration File

./loupestash/ui/config/sgtnclient.yml

#### Resource Files

Please refer ./loupestash/ui/config/sgtnclient.yml about the resource file's definition.

#### Source Collection

Refer ./loupestash/tools/vip-scanner/README.md

### JSON

Refer https://confluence.eng.vmware.com/display/GQ/2.2+DB%28JSON%29+Gobalization+Design about the solution and design.

#### String Externalization

Refer /loupestash/tools/i18n/README.md about how to run scripts to extract the sources.

By default, just run 'generate-i18n' task defined in file ./loupestash/ui/Makefile, after running please submit the latest generated sources to code repo.

#### Source Collection

Refer ./loupestash/tools/vip-scanner/README.md

## Troubleshooting

Check the log file generated in the root path, e.g. /loupestash/ui/sgtnclient_d.log

## local Testing

Put the localized bundle files to './loupestash/ui/config/translations/ENI/1.0.0' file for the debugged component and locale, e.g. define a Simplified Chinese bundle file with name 'messages_zh-Hans.json' and put it under './loupestash/ui/config/translations/ENI/1.0.0/rb/', the content will be loaded to Simplified Chinese UI fo your local testing.


## Remote Testing

Change the  parameter 'vip_server' to a remote host and 'bundle_mode' to 'online' on the configuration file, e.g.

```  

  # Singleton server
  vip_server: http://g11n-vip-dev-1.eng.vmware.com:8090

  # mode: online/offline
  bundle_mode: online

```  
