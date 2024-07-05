fastlane documentation
----

# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```sh
xcode-select --install
```

For _fastlane_ installation instructions, see [Installing _fastlane_](https://docs.fastlane.tools/#installing-fastlane)

# Available Actions
How It works:
- Install using brew or gem
  ```sh
  brew install fastlane
  ```
  `or`
  ```sh
  sudo gem install fastlane
  ```
- Go to inside folder and initialised fastlane using below command(It created Fastlane folder inside your app folder) and that will created ‘Fastlane’ and ‘Appfile’
  ```sh
  fastlane init
  ```
- Inside Faslane file can make command to execute to export app into App Store, Testflight or Adhoc
  
- Now Consider on ADHOC exporting method
  ```sh
  default_platform(:ios)
  
  platform :ios do
    desc "Build and upload a new Ad Hoc release"
    lane :build do
      increment_build_number
      get_certificates()
      get_provisioning_profile(adhoc: true)
      build_app(export_method: "ad-hoc")
    end
  end

  ```
-  After entering that need to execute in Terminal by using below command 
(ex :  lane : build => ```fastlane build``` || lane :anyname => ```fastlane anyname```

-  After using this, we will configure your app distribution email and logged into your account through the fastlane. We have to provide that data through the terminal.
  
-  As mentioned on 4. That build code do => first step increment build number, after that create certificate automatically , after creating adhoc profile and get that adhoc profile, certificates into our folder, after create export by using adhoc profile and export .ipa files with AppName.app.dSYM.zip zip file.

- Now Customised on ADHOC exporting method as our own way
  ```sh
  default_platform(:ios)

  platform :ios do
    desc "Build and upload a new Ad Hoc release"
    lane :adhocExport do
  
      # Prompt for version and environment
      version = UI.input("Enter the version (e.g., 1.0.0):")
      environment = UI.select("Enter the environment (/UAT/DEV/SIT):", %w{UAT DEV SIT})
  
      output_directory = "../Distribute App/SOLO - v #{version} - #{environment}" # Directory to save the IPA file
  
  
      # Increment the build number if necessary
      increment_build_number
  
      # Build the app
      build_app(
        export_method: "ad-hoc",
        output_directory: output_directory,
        export_options: {
          provisioningProfiles: {
            "com.hnb.digital.payApp" => "SOLO Adhoc Yesh"
          },
          method: "ad-hoc",
          signingStyle: "manual"
        }
      )
  
    end
  end
  end 
  ```


## iOS

### ios build

```sh
[bundle exec] fastlane ios build
```

Build and upload a new Ad Hoc release automatically create Certificates and Provisioning Profile

### ios adhocExport

```sh
[bundle exec] fastlane ios adhocExport
```

Build and upload a new Ad Hoc release

----

This README.md is auto-generated and will be re-generated every time [_fastlane_](https://fastlane.tools) is run.

More information about _fastlane_ can be found on [fastlane.tools](https://fastlane.tools).

The documentation of _fastlane_ can be found on [docs.fastlane.tools](https://docs.fastlane.tools).
