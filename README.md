# ENI Globalization Solution

ENI uses VMWare Singleton solution for globalization: [https://github.com/vmware/singleton](https://github.com/vmware/singleton).


## Front-end

The front-end part use Singleton Angular client(@vmw/ngx-vip) to provide globalization support.

### Configuration File

./loupestash/ui/ng2-app/libs/eni-infrastructure/l10n/src/lib/eni-ui-vip.config.ts

### Resource Files
- ./loupestash/ui/ng2-app/libs/eni-hybrid/src/lib/l10n/eni-backend.l10n.ts
- ./loupestash/ui/ng2-app/libs/eni-infrastructure/l10n/src/lib/eni-ui.app.l10n.ts

## Source Collection

Refer to /loupestash/ui/ng2-app/docs/l10n.md.


## Back-end

The back-end globalization includes two parts RB(ERB) and JSON.

### RB(ERB)

The RB(ERB) files' localization integrates with Singleton Ruby client to provide support.

#### Configuration File

./loupestash/ui/config/sgtnclient.yml

#### Resource Files

Please refer to ./loupestash/ui/config/sgtnclient.yml about the file paths.

### Source Collection

Refer to ./loupestash/tools/vip-scanner/README.md

### JSON

Refer to https://confluence.eng.vmware.com/display/GQ/2.2+DB%28JSON%29+Gobalization+Design about the solution and design.

The JSON files' localization is custimized: the sources are moved to front-end, on run-time i to  on run-time call, it needs two steps:

Step 1: run parsers to generate the resource source files

Step 2: run scripts to move the source files to front-end file.

#### String Externalization

Refer to /loupestash/tools/i18n/README.md about how to run scripts to extract the sources.

By default, just run 'generate-i18n' task( in file ./loupestash/ui/Makefile) which can run all python tasks to extract the sources, please submit the latest generated. sources to code repo.

#### Source Collection

Refer to ./loupestash/tools/vip-scanner/README.md


## Troubleshooting

## local Testing

## Remote Testing