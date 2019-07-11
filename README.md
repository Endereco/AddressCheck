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

AddressCheck relies on CountryAutocomplete to provide country codes.

## Methods

### updateConfig(array extendedConfig)

Overwrite the existing config with a new one. New fields are created, existing ones are overwritten. Fields that are not overwritten keep their default value.

Example:

```
window.invAddressCheck = new AddressCheck(originalConfig); // Create AddressCheck object.

var newConfig = {
    'useWatcher': false // Disable automatic reinitiation if address fields are dynamically inserted.
}

window.invAddressCheck.updateConfig(newConfig);
```

### checkAddress(boolean force = false)

Triggers the address check procedure. Values from fields are read and sent to api. Returns a promise.

This function doesn't trigger the rendering of selection window. In order to render selection  window use renderVariants() method.

Normally checkAddress is called automatically once user leaves address fields. The rendering of the selection window also happens automatically.

In order to manually trigger the address check and draw a window following must be done.

Usage example:

```
// 1. Disable automatic trigger on blur 
var newConfig = {
    'checkOnBlur': false
}
window.invAddressCheck.updateConfig(newConfig); // Overwriting default config with new setting.

// 2. Trigger address check manually.

var promise = window.invAddressCheck.checkAddress(true); // Use true to force address check. normally it would only start, if fields have been changed.

promise.then( function($data) {
    // This will only be called on successfull request.
    // $data will contain the answer from the server
    
    $self.predictions = $data.result.predictions; // Save predictions in the address check object.

    window.invAddressCheck.renderVariants(); // Render selection window.
});

```

### renderVariants()

Renders the selection window.

Usage:
```
window.invAddressCheck.renderVariants(); // Render selection window.
```
