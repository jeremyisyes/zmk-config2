# BLe Chiffre ZMK Config

**Note:** This repository is locked at an old version of ZMK which still uses Zephyr 2.5. All of the ZMK documentation links below point at a site containing documentation accurate to that version, which will hopefully remain available.

If those links stop working you can check [the current documentation](https://zmk.dev/docs), but bear in mind that the information there may not be usable with this repo unless it is modernized.

## Instructions

1. You will need to [sign up for a GitHub account](https://github.com/signup), and [fork this repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo#forking-a-repository) so you can edit it.
2. Navigate to the **Actions** tab and click the "I understand my workflows, go ahead and run them" button to enable builds.
   ![Actions tab with "I understand my workflows" button](https://i.imgur.com/B7cTAE6.png)
3. Edit the [config/ble_chiffre.conf](config/ble_chiffre.conf) to add/enable/disable features. Edit [config/ble_chiffre.keymap](config/ble_chiffre.keymap) to change the keymap.
4. After committing your changes, your firmware will begin compiling. Assuming there are no typos or other problems, it will eventually be [downloadable from the Actions tab](https://deploy-preview-1195--zmk.netlify.app/docs/user-setup#installing-the-firmware).
5. [Flash the firmware](https://deploy-preview-1195--zmk.netlify.app/docs/user-setup#flashing-uf2-files).

## Common Questions/Problems

### There was an error and the build didn't finish.

#### There is probably an error in your keymap.

[Clicking into the details of the action](https://docs.github.com/en/actions/quickstart#viewing-your-workflow-results) will show the error log. While very long, this log will often show the exact line number causing the problem in your keymap so it is worth reading closely.

Carefully double-check the last changes you made. ZMK syntax is very different from QMK syntax. Note that when editing keymaps, each ZMK code is generally preceded by a reference categorizing what that code does.

For example: the letter "Z" is categorized as a **k**ey **p**ress. To add the letter "Z" to a keymap, it must be written `&kp Z`.

A few more examples below:

| QMK | ZMK |
| --- | --- |
| `KC_A` | `&kp A` |
| `QK_BOOT` | `&bootloader` |
| `LT(1, KC_SPACE)` | `&lt 1 SPACE` |

There are many, many more differences. Don't forget to [check the ZMK docs](https://deploy-preview-1195--zmk.netlify.app/docs/features/keymaps).

[nickcoutsos's in-browser keymap editor](https://nickcoutsos.github.io/keymap-editor) aims to provide a GUI for remapping, which may be helpful.

### I edited the keymap/configuration and flashed, but nothing was updated.

#### Make sure you are editing the files in the [config](config) folder.

Changes made in the `boards/arm` folder will be overridden or ignored; your customizations belong in [config](config).

### After disconnecting the keyboard from Bluetooth, it won't reconnect.

#### Forget the Bluetooth connection on both the BLe Chiffre and the host, then try re-pairing.

If you don't remember which profile on the BLe Chiffre was used to connect to a specific device, this may mean cycling through each (`&bt BT_PRV`/`&bt BT_NXT`) and clearing them (`&bt BT_CLR`) one by one. [See ZMK's documentation for more info](https://deploy-preview-1195--zmk.netlify.app/docs/behaviors/bluetooth#bluetooth-pairing-and-profiles).

## Further Troubleshooting Resources

- [ZMK's troubleshooting page](https://deploy-preview-1195--zmk.netlify.app/docs/troubleshooting)
- Ask the ZMK experts in [ZMK's Discord](https://zmk.dev/community/discord/invite)
- Stop by #help in [the 40% Discord](https://discord.gg/40percent)
