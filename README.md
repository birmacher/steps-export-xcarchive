# Export Xcarchieve [![Bitrise Build Status](https://app.bitrise.io/app/4a77608299acdd22/status.svg?token=VqeMltyd51uDSQX9mc8JUQ&branch=master)](https://app.bitrise.io/app/4a77608299acdd22) [![GitHub License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://raw.githubusercontent.com/bitrise-steplib/steps-export-xcarchive/master/LICENSE)

This step allows you to export IPA from a generated Xcarchieve after archiving your project. Additionally with changing the settings you can also get a newly resigned IPA.

## Examples

### Export IPA after archiving a project

```yml
format_version: '8'
default_step_lib_source: https://github.com/bitrise-io/bitrise-steplib.git
project_type: ios
workflows:
  primary:
    steps:
      - activate-ssh-key@4:
      - git::git@github.com:bitrise-io/addons-ship-metadata-downloader-ios.git@update:
          inputs:
            - bitrise_ship_data_source: '$CONFIG_JSON_URL'
      - certificate-and-profile-installer@1.10: {}
      - export-xcarchive@3:
          inputs:
            - export_method: development
            - archive_path: $BITRISE_XCARCHIVE_PATH
            - product: app-clip
      - deploy-to-bitrise-io@1: {}
```

## Configuration

### Inputs

* [ ] Todo: Auto generate

You can configure the step with the following inputs

| Parameter | Description | Required | Default |
| --- | --- | --- | --- |
| archive_path | iOS or tvOS archive path | + | $BITRISE_XCARCHIVE_PATH |
| export_method | Select method for export | + | auto-detect |
| upload_bitcode | Include bitcode | + | yes |
| compile_bitcode | Rebuild from bitcode | + | yes |
| team_id | The Developer Portal team to use for this export | - | "" |
| product | Select a product to distribute | + | app |
| custom_export_options_plist_content | Custom export options plist content | - | "" |
| verbose_log | Enable verbose logging? | - | false |

### Outputs

* [ ] Todo: Auto generate

Step outputs environment variables that you can use as step inputs in the workflow

| Environment Variable | Description |
| --- | --- |
| $BITRISE_IPA_PATH | The created iOS or tvOS .ipa file's path. |
| $BITRISE_DSYM_PATH | The created iOS or tvOS .dSYM zip file's path. |
| $BITRISE_IDEDISTRIBUTION_LOGS_PATH | Path to the xcdistributionlogs zip |

## Contributing

1. Fork this repository
2. `git clone` it
3. Create a branch you'll work on
4. To use/test the step just follow the **How to use this Step** section
5. Do the changes you want to
6. Run/test the step before sending your contribution
  * You can also test the step in your `bitrise` project, either on your Mac or on [bitrise.io](https://www.bitrise.io)
  * You just have to replace the step ID in your project's `bitrise.yml` with either a relative path, or with a git URL format
  * (relative) path format: instead of `- original-step-id:` use `- path::./relative/path/of/script/on/your/Mac:`
  * direct git URL format: instead of `- original-step-id:` use `- git::https://github.com/user/step.git@branch:`
  * You can find more example of alternative step referencing at: https://github.com/bitrise-io/bitrise/blob/master/_examples/tutorials/steps-and-workflows/bitrise.yml
7. Once you're done just commit your changes & create a Pull Request
