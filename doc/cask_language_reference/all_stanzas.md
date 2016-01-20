# All stanzas

## Required Stanzas

Each of the following stanzas is required for every Cask.

| name               | multiple occurrences allowed? | value       |
| ------------------ |------------------------------ | ----------- |
| `version`          | no                            | application version; give value of `:latest`  if versioned downloads are not offered
| `sha256`           | no                            | SHA-256 checksum of the file downloaded from `url`, calculated by the command `shasum -a 256 <file>`. Can be suppressed by using the special value `:no_check` (see also [Checksum Stanza Details](#checksum-stanza-details))
| `url`              | no                            | URL to the `.dmg`/`.zip`/`.tgz`/`.tbz2` file that contains the application. A [comment](#when-url-and-homepage-hostnames-differ-add-a-comment) should be added if the hostnames in the `url` and `homepage` stanzas differ (see also [URL Stanza Details](#url-stanza-details))
| `name`             | yes                           | a string providing the full and proper name defined by the vendor (see also [Name Stanza Details](#name-stanza-details))
| `homepage`         | no                            | application homepage; used for the `brew cask home` command
| `license`          | no                            | a symbol identifying the license category for the application (see also [License Stanza Details](#license-stanza-details))

## At Least One Artifact Stanza Is Also Required

Each Cask must declare one or more *artifacts* (i.e. something to install)

| name               | multiple occurrences allowed? | value       |
| ------------------ |------------------------------ | ----------- |
| `app`              | yes                           | relative path to an `.app` that should be linked into the `~/Applications` folder on installation (see also [App Stanza Details](#app-stanza-details))
| `pkg`              | yes                           | relative path to a `.pkg` file containing the distribution (see also [Pkg Stanza Details](#pkg-stanza-details))
| `binary`           | yes                           | relative path to a Binary that should be linked into the `/usr/local/bin` folder on installation
| `colorpicker`      | yes                           | relative path to a ColorPicker plugin that should be linked into the `~/Library/ColorPickers` folder on installation
| `font`             | yes                           | relative path to a Font that should be linked into the `~/Library/Fonts` folder on installation
| `input_method`     | yes                           | relative path to a Input Method that should be linked into the `~/Library/Input Methods` folder on installation
| `internet_plugin`  | yes                           | relative path to a Service that should be linked into the `~/Library/Internet Plug-Ins` folder on installation
| `prefpane`         | yes                           | relative path to a Preference Pane that should be linked into the `~/Library/PreferencePanes` folder on installation
| `qlplugin`         | yes                           | relative path to a QuickLook Plugin that should be linked into the `~/Library/QuickLook` folder on installation
| `screen_saver`     | yes                           | relative path to a Screen Saver that should be linked into the `~/Library/Screen Savers` folder on installation
| `service`          | yes                           | relative path to a Service that should be linked into the `~/Library/Services` folder on installation
| `audio_unit_plugin`| yes                           | relative path to an Audio Unit plugin that should be linked into the `~/Library/Audio/Components` folder on installation
| `vst_plugin`       | yes                           | relative path to a VST Plugin that should be linked into the `~/Library/Audio/VST` folder on installation
| `suite`            | yes                           | relative path to a containing directory that should be linked into the `~/Applications` folder on installation (see also [Suite Stanza Details](#suite-stanza-details))
| `artifact`         | yes                           | relative path to an arbitrary path that should be symlinked on installation. This is only for unusual cases. The `app` stanza is strongly preferred when linking `.app` bundles.
| `installer`        | yes                           | describes an executable which must be run to complete the installation (see [Installer Stanza Details](#installer-stanza-details))
| `stage_only`       | no                            | `true`. Assert that the Cask contains no activatable artifacts.

## Optional Stanzas

| name                   | multiple occurrences allowed? | value       |
| ---------------------- |------------------------------ | ----------- |
| `uninstall`            | yes                           | procedures to uninstall a Cask. Optional unless the `pkg` stanza is used. (see also [Uninstall Stanza Details](#uninstall-stanza-details))
| `zap`                  | yes                           | additional procedures for a more complete uninstall, including user files and shared resources (see also [Zap Stanza Details](#zap-stanza-details))
| `appcast`              | no                            | a URL providing an appcast feed to find updates for this Cask (see also [Appcast Stanza Details](#appcast-stanza-details))
| `depends_on`           | yes                           | a list of dependencies and requirements for this Cask (see also [Depends_on Stanza Details](#depends_on-stanza-details))
| `conflicts_with`       | yes                           | a list of conflicts with this Cask (*not yet functional* see also [Conflicts_with Stanza Details](#conflicts_with-stanza-details))
| `caveats`              | yes                           | a string or Ruby block providing the user with Cask-specific information at install time (see also [Caveats Stanza Details](#caveats-stanza-details))
| `preflight`            | yes                           | a Ruby block containing preflight install operations (needed only in very rare cases)
| `postflight`           | yes                           | a Ruby block containing postflight install operations (see also [Postflight Stanza Details](#flight-stanzas-details))
| `uninstall_preflight`  | yes                           | a Ruby block containing preflight uninstall operations (needed only in very rare cases)
| `uninstall_postflight` | yes                           | a Ruby block containing postflight uninstall operations
| `accessibility_access` | no                            | `true` if the application should be granted accessibility access
| `container :nested =>` | no                            | relative path to an inner container that must be extracted before moving on with the installation; this allows us to support dmg inside tar, zip inside dmg, etc.
| `container :type =>`   | no                            | a symbol to override container-type autodetect. May be one of: `:air`, `:bz2`, `:cab`, `:dmg`, `:generic_unar`, `:gzip`, `:otf`, `:pkg`, `:rar`, `:seven_zip`, `:sit`, `:tar`, `:ttf`, `:xar`, `:zip`, `:naked`. (example [parse.rb](https://github.com/caskroom/homebrew-cask/blob/ffdc9a1aa459d80a084ee0d24176409388efe71f/Casks/parse.rb#L12))
| `gpg`                  | no                            | *stub: not yet functional.*  (see also [GPG Stanza Details](#gpg-stanza-details))
| `auto_updates`         | no                            | `true`. Assert the Cask artifacts auto-update. (Use if `Check for Updates…` or similar is present in app menu)