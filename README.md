# minimal-reproduction-template

First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.

## Current behavior

When importing a preset with preset name and path with a tag and arguments, the last argument is mangled with the git tag/ref.

* The preset is fetched from the default/main branch
* the last argument has an extra `)#` and all the ref except its last character

For example, in this repo, we get the following package rule:

```jsonc
{
 "addLabel": [
   "import-without-ref",
   "this-label-has-been-added-only-in-the-latest-version"
 ],
 "description": ["This works"],
 "matchDepNames": ["abc/1/*"]
},
{
 "addLabel": [
   # Missing `d` at the end of the hash
   "import-with-first-commit-sha)#57be19420641ce81cbed0d73da53ef116da4f6d",
   # This label was not added in this version of the configuration
   "this-label-has-been-added-only-in-the-latest-version"
 ],
 "description": ["This does not work"],
 "matchDepNames": ["abc/2/*"]
},
{
 "addLabel": [
   # Missing `n` at the end of `main`
   "import-with-branch-name)#mai",
   "this-label-has-been-added-only-in-the-latest-version"
 ],
 "description": ["This does not work"],
 "matchDepNames": ["abc/3/*"]
}
```

## Expected behavior

The ref should be resolved and not mangled in the last argument, we should get the following packageRules

```jsonc
{
 "addLabel": [
   "import-without-ref",
   "this-label-has-been-added-only-in-the-latest-version"
 ],
 "description": ["This works"],
 "matchDepNames": ["abc/1/*"]
},
{
 "addLabel": [
   "import-with-first-commit-sha",
 ],
 "description": ["This does not work"],
 "matchDepNames": ["abc/2/*"]
},
{
 "addLabel": [
   "import-with-branch-name",
   "this-label-has-been-added-only-in-the-latest-version"
 ],
 "description": ["This does not work"],
 "matchDepNames": ["abc/3/*"]
}
```

## Link to the Renovate issue or Discussion

Put your link to the Renovate issue or Discussion here.
