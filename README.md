# minimal-reproduction-template

First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.

## Current behavior

When importing a preset with preset name and path with a tag and arguments, the last argument is mangled with the git tag/ref.

For example, in this repo, we get the following package rule:

```jsonc
{
 "addLabel": ["bar"],
 "description": ["This works"],
 "matchDepNames": ["abc/1/*"]
},
{
 # Not obvious here, but the last char from the hash is missing
 "addLabel": ["bar)#57be19420641ce81cbed0d73da53ef116da4f6d"],
 "description": ["This does not work"],
 "matchDepNames": ["abc/2/*"]
},
{
 "addLabel": ["bar)#mai"],
 "description": ["This does not work"],
 "matchDepNames": ["abc/3/*"]
}
```



## Expected behavior

Explain the expected behavior here.

## Link to the Renovate issue or Discussion

Put your link to the Renovate issue or Discussion here.
