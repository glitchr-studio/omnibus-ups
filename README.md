# omnibus/ups

UPS for [glitchr/omnibus](https://github.com/glitchr-studio/omnibus): rates (Rating API, Shop),
shipments and labels (Shipping API), tracking (Tracking API) and UPS Access Points (Locator API)
- the REST APIs with OAuth2 client credentials.

```php
$gateway = (new UpsGatewayFactory($http))->create($options);   // $http: the application's HTTP client - none given, the factory makes its own; the options below
```

No framework needed: the package requires `glitchr/omnibus` and `symfony/http-client`. In a
Symfony application, the same through the bundle's configuration:

```yaml
omnibus:
    gateways:
        ups:
            factory: ups
            options:
                client_id: '%env(UPS_CLIENT_ID)%'
                client_secret: '%env(UPS_CLIENT_SECRET)%'
                account_number: '%env(UPS_ACCOUNT)%'   # the shipper account, 6 characters
                sandbox: true                           # the Customer Integration Environment
                rates: [...]                            # optional: configured prices instead of the Rating API
```

Shipment options: `label_format` (PDF, GIF or ZPL; UPS gives GIF for PDF requests), `description`.
Services by code: 11 Standard, 65 Saver, 07 Express, 08 Expedited, 03 Ground, 01 Next Day Air...

Credentials: an app in the [UPS Developer Portal](https://developer.ups.com) with the Rating,
Shipping, Tracking and Locator products, plus your shipper account number.

Built from UPS's published API documentation and tested on recorded answers; not yet run against
the Customer Integration Environment: that needs the credentials above.

License: LGPL-3.0-or-later.
