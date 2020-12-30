# use-referee

⚽ A collection of ref-related hooks.

[![npm](https://img.shields.io/npm/v/use-referee?color=%2385f)](https://www.npmjs.com/package/use-referee) [![gzipped](https://img.shields.io/bundlephobia/minzip/use-referee?label=gzipped&color=%23d5e)](https://www.npmjs.com/package/use-referee) [![license](https://img.shields.io/github/license/bouchenoiremarc/use-referee?color=%23e48)](https://github.com/bouchenoiremarc/use-referee/blob/main/LICENSE)

## Installation

#### With yarn

```sh
yarn add use-referee
```

#### With npm

```sh
npm install use-referee
```

## Usage

#### `use-constant`

```tsx
useConstant<T>(value: Lazy<T>) => T
```

Given a (lazy) variable, `useConstant` returns it as is while never updating or mutating it on subsequent renders.

##### Example

Import `useConstant`.

```tsx
import { useConstant } from "use-referee"
```

Declare a constant from an initial (lazy) value.

```tsx
const id = useConstant(() => uuid())

/**
 * 💬
 *
 * → id: 123e4567-e89b-12d3-a456-426614174000
 */
```

#### `use-latest`

```tsx
useLatest<T>(value: T): MutableRefObject<T>
```

Given a variable, `useLatest` returns a ref which reflects its latest value—mutating itself on variable changes to do so.

##### Example

Import `useLatest`.

```tsx
import { useLatest } from "use-referee"
```

Pass it a variable and get a mutating ref of its latest value in return.

```tsx
const [state, setState] = useState(false)
const latest = useLatest(state)

/**
 * 💬
 *
 * → latest: { current: false }
 */

setState(true)

/**
 * 🧱
 *
 * Being a ref, `latest` will always reflect the latest `state`
 * value even when omitted from dependency lists (e.g. `[]`).
 */
useEffect(() => {
  /**
   * 💬
   *
   * → latest: { current: true }
   */
}, [])
```

#### `use-previous`

```tsx
usePrevious<T>(value: T) => T | undefined
```

Given a variable, `usePrevious` returns its previous value or `undefined` before an initial change has happened.

##### Example

Import `usePrevious`.

```tsx
import { usePrevious } from "use-referee"
```

Pass it a variable and get its previous value.

```tsx
const [state, setState] = useState(false)
const previous = usePrevious(state)

/**
 * 💬
 *
 * → previous: undefined
 */

setState(true)

/**
 * 💬
 *
 * → previous: false
 */

setState(false)

/**
 * 💬
 *
 * → previous: true
 */
```