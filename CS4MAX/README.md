# Enhanced Calculator (Vanilla JS)

A small, dependency-free calculator with:

- **Advanced operations**: `+`, `-`, `×`, `÷`, **power** `^`, **percent** `%` ("A percent of B" → `A * B / 100`)
- **Negative & decimal numbers** with **result formatting** (fixed decimals)
- **Input validation** + **error highlighting** (red border + message)
- **One-click clear** of inputs, settings and result
- **History of calculations** (persisted in `localStorage`)
- **Batch/array calculations** via **Web Worker** (comma/space separated lists)
- **Modular architecture**: core logic in `src/Calculator.js` + small event system (Observer)
- **Cross-browser considerations**: lightweight polyfills for older environments
- **Automated tests** with **Jest**, including boundary checks
- **Responsive UI** for mobile

## Project structure

```
public/
  index.html
  styles.css
  app.js
  worker.js
src/
  Calculator.js
  EventBus.js
  utils.js
tests/
  calculator.test.js
package.json
jest.config.cjs
```

## Run in browser

Just open:

- `public/index.html`

(Any static server also works.)

## Run tests

Requires Node.js 18+.

```bash
npm install
npm test
```

## Notes

### Percent operator
`A % B` is interpreted as **A percent of B**:

- `25 % 200 = 50`

### Batch mode (arrays)
If you enter a list in either input (e.g. `1,2,3` or `1 2 3`), the app switches to **batch mode**:

- If both inputs are arrays, they must have equal length and the operation is **element-wise**.
- If only one side is an array, the scalar is broadcast to all elements.

Batch calculations are executed in a **Web Worker** to keep the UI responsive.

### Security note (server integration)
This project **never uses `innerHTML`** for user-controlled strings; it uses `textContent` to reduce XSS risk.
If you integrate with a server, validate/sanitize inputs server-side as well.
