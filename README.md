# pooch-cache

A GitHub action to persist the [pooch](https://www.fatiando.org/pooch/latest/) cache between GitHub Actions runs.
This might sound redundant at first, but we have recently seen severe rate limiting by Zenodo, making pooch-downloaded
data unreliable in CI workflows. This is an attempt to improve that situation.

## Example usage

```yaml
  - uses: ssciwr/pooch-cache@v1
    with:
      name: myproject
      dois: |
        10.5281/zenodo.1234567
```
## Parameter reference

This is the full reference of parameters for this action:
* `name` (required): The name of the cache, as passed to `pooch.os_cache`. Note that this action
  is currently limited to working with pooch caches that use this helper function to determine their
  location. Working with arbitrary locations would make it more difficult to make the cache usable
  across multiple OS and I prioritized this much higher.
* `dois` (optional): A list of DOIs to download using pooch. Each DOI should be on its own line.
  This will download all files from those DOIs into the cache.
* `file_urls` (optional): A list of URLs to download using pooch. Requires `known_hashes` to be defined
  and be of same length. Each URL should be on its own line.
* `known_hashes` (optional): A list of known hashes for files defined with `file_urls`.
  Each hash should be on its own line, matching the order of file URLs.
* `base-urls` (optional): A list of base URLs to download regisered data from. Requires `registry_files`
  to be defined and be of the same length. Each URL should be on its own line.
* `registry_files` (optional): A list of registry files to download using pooch. Each file should be on its own line.
* `filename-whitelist` (optional): A list of filenames to whitelist for download. Can be used to not
  download all files found under the given DOIs/URLs but only those specified here. Each filename should be on its own line.

## Contributing & Licensing

This action is available under the MIT license. If you have improvements, please discuss them in an issue prior to submitting a pull request. Contributions are welcome!
