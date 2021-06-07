# A Vue mixin to save the state of a component to local or session storage

[![Latest Version on NPM](https://img.shields.io/npm/v/vue-save-state-session.svg?style=flat-square)](https://npmjs.com/package/vue-save-state-session)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![npm](https://img.shields.io/npm/dt/vue-save-state-session.svg?style=flat-square)](https://npmjs.com/package/vue-save-state-session)

This package provides a `SaveState` mixin that automatically saves any change in the state of your component to localStorage. The next time that component gets initialized it will restore its state from the saved values in local or session storage.

## Install

You can install the package via npm:

```bash
npm install -save vue-save-state-session
```

## Usage

In order to save the state of your component you'll need to add the `SaveState` mixin:

```js
import saveState from 'vue-save-state-session';

export default {

    mixins: [saveState],

    ...
}
```

Next you'll need to add a method called `getSaveStateConfig`:

```js
import saveState from 'vue-save-state';

export default {

    mixins: [saveState],
    
    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'cacheKey': 'nameOfYourComponent',
            };
        },
    },
}
```

With these steps done any change to the state of your component will get written to local storage. The value given in `cacheKey` determines to which key in local storage the state of this component will get written. When the component is created it'll restore its state from local storage.

## Only save certain properties of the state

There's also a configuration option to determine which properties of the state should be saved/restored:

```js
import saveState from 'vue-save-state-session';

export default {
    
    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'cacheKey': 'nameOfYourComponent',
                'saveProperties': ['title', 'text'],
            };
        },
    },
}
```
With this configuration only the `title` and `text` properties of your state will get saved/restored.

Alternatively you could specify which fields to ignore:

```js
import saveState from 'vue-save-state-session';

export default {

    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'cacheKey': 'nameOfYourComponent',
                'ignoreProperties': ['title'],
            };
        },
    },
}
```

In this scenario all fields except for the `title` property in your state will get saved/restored.

## Transforming the state on load

If you want to transform the values stored in local storage before loading the into the state of the component add an `onLoad` function to the object return by `getSaveStateConfig`.

```js
import saveState from 'vue-save-state-session';

export default {

    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'onLoad': (key, value) => {
                    //return a new value
                },
            };
        },
    },
}
```

## Use sessionStorage instead of localStorage

```js
import saveState from 'vue-save-state-session';

export default {

    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'cacheKey': 'nameOfYourComponent',
                'cacheType': 'sessionStorage',
            };
        },
    },
}
```
## Disable

Add ``dontSaveState`` property if you wish to temporarily disable the saveState function
```js
import saveState from 'vue-save-state-session';

export default {

    // ...

    methods: {

        getSaveStateConfig() {
            return {
                'cacheKey': 'nameOfYourComponent',
                'cacheType': 'sessionStorage',
                'dontSaveState': true
            };
        },
    },
}
```
## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ npm run test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please contact [Freek Van der Herten](https://github.com/freekmurze) instead of using the issue tracker.

## Credits

- Eric Tromas (eric.tromas@gmail.com)
- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
