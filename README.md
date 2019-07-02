# AddressCheck

Takes the entered address and validates it against our databases. Marks the correct address as such. If some fields need correction, offers variants to choose from.

## Installation

In order to pull the latest version:

### npm (preferred)

```
npm i addresscheck
```

### github

```
git clone https://github.com/Endereco/AddressCheck.git
```

Then include AddressCheck.js in `<header>` or before config.

## Configuration

In order to use address check you must specify the fields that make the address, some inner texts and some colors.

Here is an example configuration:

```

new AddressCheck({
    'streetSelector': 'input[name="register[billing][streetname]"]',
    'houseNumberSelector': 'input[name="register[billing][streetnumber]"]',
    'postCodeSelector': 'input[name="register[billing][zipcode]"]',
    'cityNameSelector': 'input[name="register[billing][city]"]',
    'countrySelector': 'select[name="register[billing][country]"]',
    'endpoint': 'https://example-domain.com/endpoint',
    'apiKey': '041c3c302746cf37722560a7a285690738a7db4e55b7aaf26a545ffabd318a83',
    'colors' : {
        'primaryColor' => '#fff',
        'primaryColorHover' => '#fff',
        'primaryColorText' => '#fff',
        'secondaryColor' => '#fff',
        'secondaryColorHover' => '#fff',
        'secondaryColorText' => '#fff',
        'warningColor' => '#fff',
        'warningColorHover' => '#fff',
        'warningColorText' => '#fff',
        'successColor' => '#fff',
        'successColorHover' => '#fff',
        'successColorText' => '#fff'
    },
    'texts': {
        'addressCheckHead' => 'Check address',
        'addressCheckButton' => 'Use selected address',
        'addressCheckArea1' => 'Your input: ',
        'addressCheckArea2' => 'Maybe you meant: '
    }
});
```

## Dependencies

AddressCheck relies on StatusIndicator to mark fields green on correct input.

AddressCheck also relies on Accounting to generate the tid and track transactions.
