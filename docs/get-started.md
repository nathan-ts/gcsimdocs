---
sidebar_position: 2
---

# Getting Started

To get started, head over to our [Github release page](https://github.com/genshinsim/gcsimui/releases) where you can find the latest release.

Depending on your operating system, you will want to download the correct installer:

- **Windows**: Download the file ending in `.msi`
- **Mac OSX**: Download the file ending in `.dmg`
- **Linux**: You have the option of either the `.deb` or `.AppImage`

![download page](2022-01-02-21-12-47.png)

## Installation instructions

### Windows

- Download the latest `.msi` file following the instructions above
- Run the `.msi` file. Windows Defender SmartScreen may present a warning that this is an unrecognized app. This is because the app is not signed (signing require paying for a license from Microsoft). Simply click `More info` and and `Run anyways` ![](2022-01-02-23-07-31.png) ![](2022-01-02-23-08-29.png)
- Windows UAC will prompt you for Administrative priviledges. Click `Yes` at the prompt. The application requires administrative priviledges in order to install Webview2 library which is not bundled by default with Windows.
- Follow the instructions to finish the installation.

### Mac OSX

No instructions available yet :(

### Linux

No instructions available. Sorry you're on your own :(

## Advanced users

## Command line tool

Advanced users can build the command line tool directly from source. The git repo is located [here](https://github.com/genshinsim/gcsim). You will need to have go installed. Use the following command to run the tool:

```shell
cd cmd/gcsim
go run .
```