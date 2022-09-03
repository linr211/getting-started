# Front-end Globalization Solution

The front-end part(Anguar codes) uses Singleton Angular client(@vmw/ngx-vip) to provide globalization support.

## Configuration File

./loupestash/ui/ng2-app/libs/eni-infrastructure/l10n/src/lib/eni-ui-vip.config.ts

## Resource Files

./loupestash/ui/ng2-app/libs/eni-hybrid/src/lib/l10n/eni-backend.l10n.ts
./loupestash/ui/ng2-app/libs/eni-infrastructure/l10n/src/lib/eni-ui.app.l10n.ts

## Source Collection

Refer to the file: /loupestash/ui/ng2-app/docs/l10n.md

## Troubleshooting

Open the browser's dev mode to debug.

## local Testing

Input below commands on browser console to enable the pseudo testing:

```  
localStorage.setItem('vip.i18nEnabled',true );
localStorage.setItem('vip.pseudoEnabled',true);

``` 

## Remote Testing

Change the  parameter 'host' to a remote host and 'bundle_mode' to 'online' on the configuration file(eni-ui-vip.config.ts), e.g.

```  
host: 'https://g11n-vip-stg-1.eng.vmware.com:8090/'

```  
