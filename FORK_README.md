# @nyamathshaik/fast-json-patch

⚠️ **Temporary Fork** - This is a fork of [fast-json-patch](https://github.com/Starcounter-Jack/JSON-Patch) with Date object support while [PR #330](https://github.com/Starcounter-Jack/JSON-Patch/pull/330) is pending.

## Installation

```bash
npm install @nyamathshaik/fast-json-patch
```

## What's Different

Native Date object support:
- Date objects preserved during cloning
- Date comparison by value (not reference)
- Patches contain actual Date objects

## Usage

```javascript
const { compare } = require('@nyamathshaik/fast-json-patch');

const obj1 = { time: new Date('2025-11-11T10:00:00Z') };
const obj2 = { time: new Date('2025-11-11T11:00:00Z') };

const patches = compare(obj1, obj2);
// [{ op: 'replace', path: '/time', value: Date(...) }]
```

## Migration

Once PR #330 is merged, switch back:

```bash
npm uninstall @nyamathshaik/fast-json-patch
npm install fast-json-patch@^3.2.0
```

No code changes needed!

## Links

- **PR**: https://github.com/Starcounter-Jack/JSON-Patch/pull/330
- **Fork**: https://github.com/nyamathshaik/JSON-Patch/tree/npm-publish-date-support
- **Original**: https://github.com/Starcounter-Jack/JSON-Patch
