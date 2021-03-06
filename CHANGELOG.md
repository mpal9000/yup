
## 0.8.3
- document `stripUnknown`
- add `recursive` option
- add `noUnknown()` test to objects

## 0.8.2
- default for objects now adds keys for all fields, not just fields with non empty defaults

## 0.8.1
- bug fix

## 0.8.0
__breaking__
- `test` functions are now passed `path` and `context` values along with the field value. Only breaks if using the callback style of defining custom validations

## 0.7.0
__breaking__
- the `validation()` method has been renamed to `test()` and has a new signature requiring a `name` argument
- exclusive validations now trump the previous one instead of defering to it e.g: `string().max(10).max(15)` has a max of `15` instead of `10`

__other changes__
- expose advanced signature for custom validation tests, gives finer grained control over how tests are added
- added the `abortEarly` (default: `true`) option
- transforms are passed an addition parameter: 'originalValue' you allow recovering from a bad transform further up the chain (provided no one mutated the value)

## 0.6.3
- fix `concat()` method and add tests

## 0.6.2
- fix validations where nullable fields were failing due to `null` values e.g `string.max()`

## 0.6.1
- fix export error

## 0.6.0
__breaking__
- Removed the `extend` and `create` methods. Use whatever javascript inheritance patterns you want instead.
- the resolution order of defaults and coercions has changed. as well as the general handling of `null` values.
  + Number: `null` will coerce to `false` when `nullable()` is not specified. `NaN` values will now fail `isType()` checks
  + String: `null` will coerce to `''` when `nullable()` is not specified
  + Date: Invalid dates will not be coerced to `null`, but left as invalid date, This is probably not a problem for anyone as invalid dates will also fail `isType()` checks
- default values are cloned everytime they are returned, so it is impossible to share references to defaults across schemas. No one should be doing that anyway
- stopped pretending that using schemas as conditions in `when()` actually worked (it didn't)

__other changes__
- `transform()` now passes the original value to each transformer. Allowing you to recover from a bad transform.
- added the `equals()` alias for `oneOf`
- 
## 0.5.0
__breaking__
- isValid is now async, provide a node style callback, or use the promise the method returns to read the validity. This change allows for more robust validations, specifically remote ones for client code (or db queries for server code). The cast method is still, and will remain, synchronous.
- 
__other changes__
- added validate method (also async) which resolves to the value, and rejects with a new ValidationError