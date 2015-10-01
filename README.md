cloner [![build status](https://secure.travis-ci.org/WebReflection/cloner.svg)](http://travis-ci.org/WebReflection/cloner)
==============

An ES5+ compatible utility to deep or shallow copy and merge objects.

### API
The module has two sub modules: `shallow` and `deep`.
Both of them will have two methods: `copy` and `merge`.

#### cloner.shallow.copy(object):shallowCopy
Will loop over all own keys and copy them to a new object. The equivalent operation can be described as such:

```js
// it's based on descriptors
Object.defineProperties(
  // it preserves inheritance
  Object.create(
    Object.getPrototypeOf(source)
  ),
  // it does shallow copy
  Reflect.ownKeys(source).reduce(function (d, k) {
    d[k] = Object.getOwnPropertyDescriptor(source, k);
  }, {})
  // or Reflect.getOwnPropertyDescriptors(source)
);
```
The `cloner.shallow.copy` utility is most likely what you are looking for instead of the underpowered `Object.assign` one.

#### cloner.shallow.merge(target, source1[, source2, sourceN]):target
Preserves what's already in the `target` and merge all own keys found in one or more passed sources.
```js
var a = {a: 1, b: 2};
var b = cloner.shallow.merge({a: 3}, a);

b; // {a: 3, b: 2}
```
Probably the best option to merge states, ideal for statics or immutable properties.


#### cloner.deep.copy(object):deepCopy
Same as `cloner.shallow.copy` beside the fact every single own key will be deeply copied.
Like its shallow counterpart, it does preserve inheritance and it's **recursion aware**, meaning it shouldn't fail with recursive properties, as already [tested](test/cloner.js).


### How to use
`npm install cloner` should do, otherwise [grab the file you like the most](build/) in here.

### License
```

```
