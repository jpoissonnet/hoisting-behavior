# Why ?

I noticed a weird behavior with the shamefully-hoist global configuration overriding the local public-hoist-pattern

If you set globally shamefully-hoist to true, and locally public-hoist-pattern to "foo", the local configuration is ignored.
**I am not sure whether this is a bug or not but if not we could add a warning in the documentation.**

# How to reproduce ?

- Clone this repository

- Beware to have unset the global shamefully-hoist config

You can check the current configuration with `pnpm config get`
To unset the global config, run `pnpm config --global delete shamefully-hoist`

- Run `pnpm install`

- Check your root node_modules, in the .bin you should see the `jest` binary which confirms that `jest` is hoisted

- Now run `pnpm config --global set shamefully-hoist false`

- Run `pnpm install` it should ask to recreate the `node_modules`

- If you check the `node_modules` you will see that there is no trace left of jest

# Expected behavior

Hoisting should work with the local configuration overriding the global one.

# Fix

We should add a warning in the documentation if this is not a bug or work on a fix to make the local public-hoist-pattern override the global shamefully-hoist configuration.
