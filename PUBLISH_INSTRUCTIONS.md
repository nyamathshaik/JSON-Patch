# Instructions to Publish to npm

## Prerequisites

1. **npm account**: Create one at https://www.npmjs.com if you don't have one
2. **npm login**: Run `npm login` and enter your credentials

## Publishing Steps

### Step 1: Login to npm

```bash
cd /Users/nyamathshaik/fast-json-patch
npm login
```

Enter your:
- Username
- Password
- Email
- One-time password (if 2FA is enabled)

### Step 2: Build the Package

```bash
npm run build
```

This will:
- Clean the dist folders
- Compile TypeScript
- Generate CommonJS and ESM modules
- Run webpack

### Step 3: Test Locally (Optional but Recommended)

```bash
# Create a tarball
npm pack

# This creates @nyamathshaik-fast-json-patch-3.1.2-date-support.0.tgz

# Test in another project
cd /tmp
mkdir test-package
cd test-package
npm init -y
npm install /Users/nyamathshaik/fast-json-patch/@nyamathshaik-fast-json-patch-3.1.2-date-support.0.tgz

# Test it
node -e "const fjp = require('@nyamathshaik/fast-json-patch'); console.log(fjp)"
```

### Step 4: Publish to npm

```bash
cd /Users/nyamathshaik/fast-json-patch

# Dry run first (see what will be published)
npm publish --dry-run

# Actually publish
npm publish --access public
```

**Note**: The `--access public` flag is required for scoped packages (@nyamathshaik/*) to be publicly accessible.

### Step 5: Verify Publication

```bash
# Check on npm
npm view @nyamathshaik/fast-json-patch

# Or visit
# https://www.npmjs.com/package/@nyamathshaik/fast-json-patch
```

## Expected Output

```
npm notice
npm notice 📦  @nyamathshaik/fast-json-patch@3.1.2-date-support.0
npm notice === Tarball Contents ===
npm notice 1.1kB   LICENSE.txt
npm notice 18.2kB  README.md
npm notice 2.7kB   package.json
npm notice 1.9kB   index.d.ts
npm notice 407B    index.js
npm notice 659B    index.mjs
npm notice 611B    index.ts
...
npm notice === Tarball Details ===
npm notice name:          @nyamathshaik/fast-json-patch
npm notice version:       3.1.2-date-support.0
npm notice filename:      @nyamathshaik/fast-json-patch-3.1.2-date-support.0.tgz
npm notice package size:  XX.X kB
npm notice unpacked size: XXX.X kB
npm notice shasum:        xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
npm notice integrity:     xxxxxxxxxxxxxxxxxxxxx[...]xxxxxxxxxxxxx
npm notice total files:   XX
npm notice
npm notice Publishing to https://registry.npmjs.org/ with tag latest
+ @nyamathshaik/fast-json-patch@3.1.2-date-support.0
```

## Troubleshooting

### Error: 403 Forbidden

**Cause**: Not logged in or no permission
**Solution**:
```bash
npm login
npm publish --access public
```

### Error: Package name too similar

**Cause**: npm thinks it's too similar to existing package
**Solution**: The scoped package (@nyamathshaik/*) should avoid this

### Error: Version already exists

**Cause**: Version 3.1.2-date-support.0 already published
**Solution**:
```bash
# Bump version
npm version 3.1.2-date-support.1
git push fork feature/date-object-support
npm publish --access public
```

## After Publishing

### Update API-Workflow

```bash
cd /Users/nyamathshaik/uipath/API-Workflow/api-workflow-executor

# Update package.json
npm install @nyamathshaik/fast-json-patch@3.1.2-date-support.0

# Or manually edit package.json:
# "@nyamathshaik/fast-json-patch": "3.1.2-date-support.0"
```

### Create an Alias (Optional)

If you want to keep using `fast-json-patch` in your code:

```json
{
  "dependencies": {
    "fast-json-patch": "npm:@nyamathshaik/fast-json-patch@3.1.2-date-support.0"
  }
}
```

This installs `@nyamathshaik/fast-json-patch` but allows you to `require('fast-json-patch')`.

## Migration Back to Official Package

When PR #330 is merged:

```bash
cd /Users/nyamathshaik/uipath/API-Workflow/api-workflow-executor

# Uninstall fork
npm uninstall @nyamathshaik/fast-json-patch

# Install official version (assuming 3.2.0 includes Date support)
npm install fast-json-patch@^3.2.0

# No code changes needed!
```

## Deprecation Notice

Once the official package merges Date support, deprecate your fork:

```bash
npm deprecate @nyamathshaik/fast-json-patch "This fork is no longer needed. Use official fast-json-patch@^3.2.0 instead"
```

---

**Ready to publish?** Run the commands above!
